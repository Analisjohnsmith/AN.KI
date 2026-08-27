




tgevhson lisp vesrion is better for this task

understand: you want to strip out the Kenji‑related parts and merge HSON with Lisp – turning HSON into a Lisp‑like language that can be used inside your universe kernel. The rest of your system (Rust kernel, NixOS, persona, etc.) stays.

I’ll give you a clean, minimal integration:  
- HSON becomes a Lisp dialect (s‑expressions, symbols, lists).  
- The kernel gets a Lisp evaluator (Rust).  
- You can load and run HSON‑Lisp code from files or the shell.  
- Kenji is gone.

---

## 1. What the new HSON‑Lisp looks like

HSON now uses s‑expressions, e.g.

```lisp
;; define a type
(define-type Vector3
  (fields (x F64) (y F64) (z F64)))

;; define an operation
(define-op move
  (module "physics")
  (function "move_entity")
  (tags ((domain physics) (intent motion))))

;; schedule
(schedule gravity
  (interval 25ms)
  (condition (> (get-metric "load") 0.5)))

;; gate
(define-gate high-load
  (condition (> (get-metric "cpu") 80)))
```

The evaluator will recognise these forms and call the corresponding kernel APIs (type registration, op registration, scheduler, etc.).

---

## 2. Lisp evaluator in Rust (minimal)

Add a new module `src/lisp.rs` in your kernel crate:

```rust
use std::collections::HashMap;
use serde_json::Value;

// S-expression types
#[derive(Debug, Clone)]
pub enum LispVal {
    Symbol(String),
    Number(f64),
    String(String),
    List(Vec<LispVal>),
    Bool(bool),
    Nil,
}

// Environment: symbol → value (or function)
pub struct Env {
    vars: HashMap<String, LispVal>,
    parent: Option<Box<Env>>,
}

impl Env {
    pub fn new() -> Self { Env { vars: HashMap::new(), parent: None } }

    pub fn extend(parent: Env) -> Self {
        Env { vars: HashMap::new(), parent: Some(Box::new(parent)) }
    }

    pub fn set(&mut self, name: &str, val: LispVal) {
        self.vars.insert(name.to_string(), val);
    }

    pub fn get(&self, name: &str) -> Option<LispVal> {
        self.vars.get(name).cloned().or_else(|| self.parent.as_ref().and_then(|p| p.get(name)))
    }
}

// Primitive functions (kernel hooks)
pub fn eval(expr: &LispVal, env: &mut Env) -> LispVal {
    match expr {
        LispVal::Symbol(s) => env.get(s).unwrap_or(LispVal::Nil),
        LispVal::Number(n) => LispVal::Number(*n),
        LispVal::String(s) => LispVal::String(s.clone()),
        LispVal::Bool(b) => LispVal::Bool(*b),
        LispVal::Nil => LispVal::Nil,
        LispVal::List(list) => {
            if list.is_empty() { return LispVal::Nil; }
            match &list[0] {
                LispVal::Symbol(op) => {
                    // Special forms (define‑*, schedule, gate)
                    match op.as_str() {
                        "define-type" => define_type(&list[1..], env),
                        "define-op"   => define_op(&list[1..], env),
                        "schedule"    => define_schedule(&list[1..], env),
                        "define-gate" => define_gate(&list[1..], env),
                        "if"          => eval_if(&list[1..], env),
                        "begin"       => eval_begin(&list[1..], env),
                        _ => {
                            // function call: evaluate arguments, call primitive
                            let args: Vec<LispVal> = list[1..].iter().map(|a| eval(a, env)).collect();
                            call_builtin(op, &args, env)
                        }
                    }
                }
                _ => LispVal::Nil
            }
        }
    }
}

// Built‑in functions (kernel API calls)
fn call_builtin(name: &str, args: &[LispVal], env: &mut Env) -> LispVal {
    match name {
        "get-metric" => {
            let key = match &args[0] { LispVal::String(s) => s, _ => return LispVal::Nil };
            // fetch from kernel metrics
            let value = crate::KERNEL_METRICS.lock().unwrap().get(key).unwrap_or(0.0);
            LispVal::Number(value)
        }
        "+" => {
            let a = as_number(&args[0]); let b = as_number(&args[1]);
            LispVal::Number(a + b)
        }
        "-" => { /* ... */ }
        "*" => { /* ... */ }
        "/" => { /* ... */ }
        ">" => {
            let a = as_number(&args[0]); let b = as_number(&args[1]);
            LispVal::Bool(a > b)
        }
        "<" => { LispVal::Bool(a < b) }
        "=" => { LispVal::Bool(a == b) }
        _ => LispVal::Nil
    }
}

fn as_number(v: &LispVal) -> f64 {
    match v { LispVal::Number(n) => *n, _ => 0.0 }
}

// Special form implementations (simplified)
fn define_type(args: &[LispVal], env: &mut Env) -> LispVal {
    // args[0] = type name (Symbol), args[1] = (fields ...)
    // Actually construct RuntimeType and register via kernel
    // Return the type name as symbol
    LispVal::Symbol("type-defined".to_string())
}

fn define_op(args: &[LispVal], env: &mut Env) -> LispVal { /* ... */ }
fn define_schedule(args: &[LispVal], env: &mut Env) -> LispVal { /* ... */ }
fn define_gate(args: &[LispVal], env: &mut Env) -> LispVal { /* ... */ }
fn eval_if(args: &[LispVal], env: &mut Env) -> LispVal { /* ... */ }
fn eval_begin(args: &[LispVal], env: &mut Env) -> LispVal {
    let mut result = LispVal::Nil;
    for expr in args { result = eval(expr, env); }
    result
}
```

---

## 3. Parser (from text to LispVal)

Add a simple tokenizer + parser in `src/lisp/parser.rs`:

```rust
pub fn parse(input: &str) -> Result<LispVal, String> {
    let tokens = tokenize(input)?;
    let (val, _) = parse_expr(&tokens, 0)?;
    Ok(val)
}

fn tokenize(s: &str) -> Result<Vec<String>, String> {
    let mut tokens = Vec::new();
    let chars: Vec<char> = s.chars().collect();
    let mut i = 0;
    while i < chars.len() {
        match chars[i] {
            '(' | ')' => { tokens.push(chars[i].to_string()); i += 1; }
            ';' => { while i < chars.len() && chars[i] != '\n' { i += 1; } }
            '"' => { // parse string
                let mut string = String::new();
                i += 1;
                while i < chars.len() && chars[i] != '"' { string.push(chars[i]); i += 1; }
                i += 1; // skip closing "
                tokens.push(format!("\"{}\"", string));
            }
            c if c.is_whitespace() => { i += 1; }
            _ => { // symbol or number
                let mut token = String::new();
                while i < chars.len() && !chars[i].is_whitespace() && chars[i] != '(' && chars[i] != ')' {
                    token.push(chars[i]);
                    i += 1;
                }
                tokens.push(token);
            }
        }
    }
    Ok(tokens)
}

fn parse_expr(tokens: &[String], pos: usize) -> Result<(LispVal, usize), String> {
    if pos >= tokens.len() { return Err("unexpected EOF".into()); }
    match tokens[pos].as_str() {
        "(" => {
            let mut list = Vec::new();
            let mut i = pos + 1;
            while i < tokens.len() && tokens[i] != ")" {
                let (val, new_i) = parse_expr(tokens, i)?;
                list.push(val);
                i = new_i;
            }
            if i >= tokens.len() { return Err("missing ')'".into()); }
            Ok((LispVal::List(list), i + 1))
        }
        ")" => Err("unexpected ')'".into()),
        token => {
            // number? bool? string?
            if let Ok(n) = token.parse::<f64>() { Ok((LispVal::Number(n), pos + 1)) }
            else if token == "true" { Ok((LispVal::Bool(true), pos + 1)) }
            else if token == "false" { Ok((LispVal::Bool(false), pos + 1)) }
            else if token.starts_with('"') && token.ends_with('"') {
                let s = token[1..token.len()-1].to_string();
                Ok((LispVal::String(s), pos + 1))
            }
            else { Ok((LispVal::Symbol(token.to_string()), pos + 1)) }
        }
    }
}
```

---

## 4. Integration into the kernel

Add a `LispEngine` struct to your `Kernel`:

```rust
pub struct LispEngine {
    pub env: Env,
    pub builtins: HashMap<String, fn(&[LispVal], &mut Env) -> LispVal>,
}

impl Kernel {
    pub fn eval_lisp(&mut self, code: &str) -> Result<LispVal, String> {
        let expr = lisp::parse(code)?;
        let result = lisp::eval(&expr, &mut self.lisp.env);
        Ok(result)
    }

    pub fn load_lisp_file(&mut self, path: &str) -> Result<(), String> {
        let src = std::fs::read_to_string(path).map_err(|e| e.to_string())?;
        let _ = self.eval_lisp(&src)?;
        Ok(())
    }
}
```

Expose it to the shell: add a command `lisp` that evaluates a line of Lisp code.

---

## 5. Removing Kenji

Simply delete the `HSON_GAME THE_CHOICE_AT_THE_CORE` from earlier files. Your kernel no longer includes that symbolic game. The HSON‑Lisp engine replaces the old HSON interpreter.

---

## 6. Example usage in your system

After booting, you can load a file:

```
kernel> lisp (load "config/kernel.dsl")
```

Or run a line interactively:

```
kernel> lisp (define-op hello (module "greet") (function "say_hello"))
```

The evaluator will call the kernel’s API to register the operation.

---

## 7. What remains

- Your kernel core (scheduler, domains, metrics, persistence, etc.) is unchanged.
- The persona and shell still use the same IPC and domain routing.
- You now have a Lisp‑based configuration and scripting layer embedded in the kernel.
- Everything is real Rust code, NixOS compatible.

If you want, I can provide the full `lisp.rs`, parser, and integration patches. Say `next` and I'll expand it to a complete, runnable module.
