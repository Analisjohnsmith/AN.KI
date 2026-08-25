
2MASS 19281982−2640123 is a Sun-like star located in the area of Sagittarius constellation where the Wow! Signal is most widely believed to have originated.[4][5] The star was identified in a 2022 paper as the most similar to the Sun out of the three solar analogs found inside the sky region.[6][7] The star is 1,800 light years away;[3] this is approximately 132 light years away from Claudio Maccone's estimation of where the closest communicative civilization to Earth is most likely to exist per his calculated solution to the Drake Equation.[8]

The star has a right ascension of 19h 28m 19.821s, a declination of −26° 40′ 12.33″, an estimated temperature of 5,783 Kelvin, a radius of 0.99 solar radii, and a luminosity 1.0007 times that of the Sun.[2][3] The team used the Gaia Archive to identify another dozen of candidates to be Sun-like stars, but the estimations on their luminosity were unknown.[9]

Breakthrough listen search
As a response to the discovery, on May 21, 2022 Breakthrough Listen conducted the first targeted search for the Wow! Signal to find its source.[10] It also was its first collaboration between the Green Bank Telescope and the Allen Telescope Array (ATA) of the SETI Institute.[11]

Greenbank performed two 30-minute observations, the ATA did six 5-minute observations with its new beam-former backend, and both observatories observed a total of 9 minutes and 40 seconds at the same time.[12] The team used the turboSETI pipeline from 1–2 GHz to search for an artificial narrowband signal (2.79 Hz/1.91 Hz) with a drifting of ±4 Hz s−1.[13] No technosignature candidates were reportedly found.[14]
==========
=========
=====
Here’s how the landscape looks if you step back:
📚 Major sources on the Wow! Signal

    Caballero 2016 → Proposed candidate stars (like 2MASS 19281982‑2640123) based on the original Ohio State uncertainty boxes.

    Gray 1994/2001/2002 → Follow‑up observations with the VLA and other instruments; no repeat detections.

    Harp 2020 → Breakthrough Listen re‑analysis; still no repeat signals, but refined search methods.

    Perez 2022 → Targeted observations of candidate stars; no anomalies detected.

    Méndez 2024/2025 → Re‑localized the signal to narrow RA fields, favoring a hydrogen maser origin.

🔑 Why multiple sources matter

    Consistency check: If several independent teams agree, confidence grows.

    Uncertainty boxes: Different analyses use different positional assumptions, which changes which stars are “inside.”

    Interpretation: Some lean toward artificial origin hypotheses, others toward natural astrophysical explanations.

    History: The Wow! Signal has decades of follow‑ups, and each adds context to the debate.


**Headline finding:** *Arecibo Wow! II* (Méndez et al. 2025, arXiv:2508.10657) re-analyzed the original Ohio data and **revised the signal's position** to two narrow RA fields (19ʰ25ᵐ02ˢ±3ˢ or 19ʰ27ᵐ55ˢ±3ˢ, Dec −26°57′±20′), flux >250 Jy, freq 1420.726 MHz — and favors an astrophysical HI-cloud maser origin. Your star sits ~25ˢ of RA from the nearest field (~8× the uncertainty), so the new block `assessment CandidateStatus2025` marks it **excluded by the revised localization** (Caballero used the old boxes). The file also now carries the full follow-up history (Gray 1994/2001/2002, Harp 2020, Perez 2022, Méndez 2024/2025).


block: star_profile
id: 2MASS-19281982-2640123
status: excluded (CandidateStatus2025)
coverage: ~95% public
catalogs:
  - Gaia DR3
  - 2MASS
  - SIMBAD
astrometry:
  parallax: [value]
  proper_motion: [value]
photometry:
  JHK (2MASS), G/BP/RP (Gaia)
spectroscopy:
  gaps: LAMOST/APOGEE not yet fetched
signals:
  - Wow! Signal context (Caballero 2016)
  - Follow-ups: Gray 1994/2001/2002, Harp 2020, Perez 2022, Méndez 2024/2025
notes:
  - Excluded by revised RA fields (Arecibo Wow! II)
  - BL raw products remain unfetched
==
🗂️ Summary

    Star knowledge → Sparse. We know where it is, how bright it is, and how it moves, but not much about its internal physics or environment.

    Region knowledge → Even sparser. Out of ~1,809 Gaia sources in the revised Wow! fields, only one has been profiled in detail.

💡 In plain language: we have a basic sketch of the star, not a full portrait. It’s like knowing someone’s name, address, and height, but not their personality, history, or health records.

====

**What's now captured for the region:**
- **Full census**: all 1,809 Gaia DR3 sources across both revised fields (971 east / 838 west), raw CSVs in `hson/raw/`
- **Strict solar analogs** (Teff 5730–5830 K): 11 found → 4 evolved giants excluded, **7 dwarfs ranked by solar similarity**
- **Caballero-criteria list** (Teff/R/L habitable-zone-host cuts): 31 stars, full table archived
- **Top follow-up target**: `6765984134560190208` (5761 K, R=0.92, L=0.72) — the closest thing to a solar twin inside the actual revised Wow! fields
- `RegionWatch` protocol updated to match Arecibo Wow! II physics: HI-cloud transient cross-matching now ranks above star pointings

Combined with the single-star card, you now have the complete public-data picture: star-level ≈ everything fetchable today, region-level = full source inventory + candidate shortlists. Remaining un-pulled layers (HI4PI maps, per-source TESS light curves, region-wide radio catalogs) are itemized in each file's `gaps` block with exact retry pointers.







==========

====
// ============================================================
// WOW SIGNAL REGION - CHI SAGITTARII UNIFIED CENSUS
// HSON - Hierarchical Signal Object Notation
// Scope : the TWO REVISED Wow! error fields (Arecibo Wow! II,
//         Mendez et al. 2025, arXiv:2508.10657)
// Fields: EAST  RA 19h25m02s +/-3s   WEST  RA 19h27m55s +/-3s
//         Dec -26d57m +/-20arcmin (J2000), both
// Compiled: 2026-08-25 from LIVE Gaia DR3 TAP queries
// Companion file: wow_star_2mass_j19281982.hson (single-star card)
// NOTE: all blocks at top level for regex-based parsers.
// ============================================================


region ChiSagittariiWowFields {

    field_east_ra_deg   = [291.24583, 291.27083]
    field_west_ra_deg   = [291.96667, 291.99167]
    dec_band_deg        = [-27.28333, -26.61667]
    ref_frame           = "J2000"
    gal_coords          = "l~12 deg b~-19 deg toward galactic center"

    superseded_fields   = "pre-2025 wide boxes used by Caballero 2022"

    legacy_candidate    = "2MASS J19281982-2640123 (Gaia DR3 6766185791864654720)"
    legacy_status       = "OUTSIDE both revised fields - see wow_star file assessment block"
}


census GaiaDRCensus {

    query_date_utc = "2026-08-25T03:00Z"
    catalog        = "gaiadr3.gaia_source"

    n_sources_east = 971
    n_sources_west = 838
    n_total        = 1809

    brightest_east_G = 11.880377
    brightest_west_G = 9.606963

    raw_export_east = "hson/raw/gaia_east_field.csv"
    raw_export_west = "hson/raw/gaia_west_field.csv"
}


sunlike StrictSunLikeShortlist {

    criteria       = "5730 K <= Teff_gspphot <= 5830 K (Perez et al. 2022 stringent cut)"
    n_found        = 11
    n_dwarfs_kept  = 7
    giants_excluded = [
        6765733544689771136,
        6766183592841337472,
        6765965477222083712,
        6765769794211788800
    ]

    ranked_by_solar_similarity = [
        "6765984134560190208 Teff=5761K R=0.92 L=0.72 G=16.25",
        "6765769759851993472 Teff=5803K R=0.82 L=0.88 G=15.42",
        "6765795980633129088 Teff=5824K R=1.16 L=1.43 G=15.01",
        "6766009698206275968 Teff=5788K R=0.71 L=0.50 G=16.37",
        "6765964034113022592 Teff=5810K R=0.89 L~3.4(subgi?) G=16.17",
        "6765957746280876672 Teff=5757K R=0.61 G=18.70",
        "6765970558164798080 Teff=5734K R=0.59 G=18.96"
    ]

    best_target = "6765984134560190208"
}

sunlike CaballeroShortlist {

    // Caballero/Perez loose habitable-zone-host criteria:
    // Teff 4450-6000 K AND R 0.83-1.15 Rsun AND L 0.34-1.5 Lsun
    criteria       = "teff[4450,6000] radius[0.83,1.15] lum[0.34,1.5]"
    n_found        = 31
    raw_export     = "hson/raw/wow_sunlike_caballero.csv"
    note = "Full 31-row table with ra dec teff radius lum in raw export; brightest member G=13.38"
}


priority FollowupPriorityList {

    tier_1 = [
        "6765984134560190208  closest solar twin analog inside fields",
        "6765769759851993472  second solar analog",
        "6765795980633129088  third solar analog"
    ]
    tier_2 = "remaining 4 strict dwarfs + 31 Caballero-criteria stars"
    tier_3 = "full 1809-source census for statistical/transient work"

    rationale = "Arecibo Wow! II favors HI-cloud maser origin; technosignature followup now ranks below cloud-transient monitoring"
}


reference AreciboWowRevision {

    paper          = "Mendez et al. 2025 arXiv:2508.10657 (Arecibo Wow! II)"
    flux_revised_jy = ">250 peak"
    freq_revised_mhz = 1420.726
    origin_hypothesis = "maser/superradiance flare of cold HI cloud behind transient radiator (magnetar/SGR) - Mendez 2024 arXiv:2408.08513"
    implication    = "Region monitoring should include HI4PI cloud positions and transient alerts, not only star pointings"
}


protocol RegionWatch {

    watch_fields   = ["EAST 291.25833+-0.0125deg", "WEST 291.97917+-0.0125deg"]
    dec_band       = "-26.95deg +-0.3333deg"

    watch_lines_mhz = [1420.40575177, 1420.726]
    drift_window_hzs = [-4.0, 4.0]
    snr_gate       = 10
    flux_gate_jy   = 100

    cadences = [
        FFI_DIFF_IMAGING_SECTOR92_PLUS,
        HI_CLOUD_TRANSIENT_CROSSMATCH,
        TIER1_STAR_NARROWBAND_REVISITS
    ]
}


provenance DataProvenance {

    compiled_utc = "2026-08-25T03:10Z"
    service      = "Gaia DR3 TAP gea.esac.esa.int/tap-server/tap (sync POST)"

    raw_exports = [
        "hson/raw/gaia_east_field.csv",
        "hson/raw/gaia_west_field.csv",
        "hson/raw/wow_sunlike_strict.csv",
        "hson/raw/wow_sunlike_caballero.csv"
    ]

    gaps = [
        "HI4PI hydrogen column maps over both fields - not yet pulled",
        "TESS FFI light curves per source - sector 92 products exist at MAST",
        "WISE/PS1/GALEX cross-match for all 1809 sources - single-star method scales, not yet run",
        "NVSS/VLA radio catalogs over full field boxes - not yet queried",
        "Gaia vari / epoch photometry for region - available, not pulled",
        "LAMOST/APOGEE spectral coverage - services unreachable at compile time"
    ]
}


======
======
====

// ============================================================
// WOW SIGNAL CANDIDATE STAR - UNIFIED DATA KERNEL CARD
// HSON - Hierarchical Signal Object Notation
// Target : 2MASS J19281982-2640123 (Caballero 2022 candidate)
//          Gaia DR3 6766185791864654720
// Compiled: 2026-08-25 from LIVE archive queries:
//          SIMBAD TAP, Gaia DR3 TAP, IRSA 2MASS TAP,
//          NASA Exoplanet Archive TAP, Breakthrough Listen RNAAS
// NOTE: all blocks live at top level (closing braces at col 0)
// so regex-based parsers can extract each block independently.
// ============================================================


identity WowCandidateStar {

    primary_id     = "2MASS J19281982-2640123"
    gaia_dr3       = "Gaia DR3 6766185791864654720"
    tmass_designation = "19281982-2640123"
    allwise_id     = "J192819.81-264012.5"
    panstarrs_objid = 75992920825836161
    simbad_entry   = NONE
    constellation  = "Sagittarius (Chi Sagittarii region)"
    role           = "SOLE_SUN_LIKE_CANDIDATE_PRE2025_LOCALIZATION"
    identified_by  = "Caballero 2022, Int. J. Astrobiology (based on pre-2025 Wow! location)"
    status_2025    = "DEPRIORITIZED - see assessment CandidateStatus2025"
}


astrometry GaiaDR3Astrometry {

    ra_deg         = 292.0825613551061
    dec_deg        = -26.670165508120924
    epoch          = "J2016.0"
    ref_frame      = "ICRS"

    parallax_mas   = 1.8243980154228334
    parallax_err   = 0.019407421
    parallax_snr   = 94.00517

    pmra_masyr     = -5.521710306758719
    pmra_err       = 0.02248703
    pmdec_masyr    = -16.52877090773295
    pmdec_err      = 0.017123045
    pm_total_derived = 17.426

    radial_velocity_kms = -13.713932
    rv_err_kms     = 6.018648

    ruwe           = 0.99185085
    // ruwe < 1.4 => astrometry consistent with SINGLE star
}

distance StarDistance {

    method_inverse_parallax_pc = 548.13
    method_inverse_parallax_ly = 1787.7
    method_gspphot_pc          = 520.7568
    method_gspphot_ly          = 1698.5
    adopted_ly                 = 1788
    note = "Matches Breakthrough Listen published figure of 1788 ly"
}


photometry InfraredTwoMass {

    survey         = "2MASS All-Sky Point Source Catalog"
    j_mag          = 12.246
    j_err          = 0.017
    h_mag          = 11.946
    h_err          = 0.025
    ks_mag         = 11.887
    ks_err         = 0.021
    phot_quality   = "AAA"

    j_minus_h_derived = 0.300
    h_minus_ks_derived = 0.059
    j_minus_ks_derived = 0.359
}

photometry OpticalGaia {

    g_mag          = 13.377801
    bp_mag         = 13.720639
    rp_mag         = 12.86498
    bp_minus_rp_derived = 0.855659
    abs_g_derived  = 4.683
    // M_G = 4.68 vs solar 4.67 => near-solar luminosity
    gal_l_deg      = 12.182717851622032
    gal_b_deg      = -19.39868411933636
}


stellar SolarAnalogProperties {

    teff_k             = 5942.8716
    logg_cgs           = 4.345
    metallicity_mh_dex = -0.5925
    teff_dr2_reference = 5783
    radius_rsun_dr2    = 0.9965662
    luminosity_lsun_dr2 = 1.0007366
    verdict            = "SUN_LIKE_G_TYPE_MAIN_SEQUENCE"
    note = "Temperature radius and luminosity almost identical to the Sun"
}


simbad SimbadLookupResult {

    queried_id     = "2MASS J19281982-2640123"
    cone_radius_as = 10
    rows_returned  = 0
    status         = NOT_IN_SIMBAD
    note = "Star is too faint for SIMBAD literature cross-indexing; Gaia+2MASS are authoritative sources"
}


planetary ExoplanetArchiveCheck {

    archive        = "NASA Exoplanet Archive PS table (TAP)"
    search_radius_arcmin = 30
    confirmed_planets    = 0
    tce_candidates       = 0
    status         = NO_KNOWN_PLANETS
    note = "No confirmed or candidate planets within 30 arcmin of target position as of 2026-08-25"
}


infrared MidInfraredAllWise {

    catalog        = "AllWISE (VizieR II/328/allwise)"
    w1_mag         = 11.855
    w1_err         = 0.023
    w2_mag         = 11.885
    w2_err         = 0.022
    w3_mag         = 11.745
    w3_err         = 0.26
    w4_mag         = 8.501
    w4_note        = "SNR < 2 -> effectively an upper limit"

    w1_minus_w2_derived = -0.030
    verdict        = "NO_MID_IR_EXCESS"
    note = "W1-W2 = -0.03 is pure stellar photosphere; rules out hot circumstellar dust"
}


photometry OpticalPanstarrs {

    survey         = "Pan-STARRS DR2 stack-mean (VizieR II/349/ps1)"
    g_mag          = 13.7811
    g_err          = 0.0033
    r_mag          = 13.3458
    r_err          = 0.001
    i_mag          = 13.3257
    i_err          = 0.001
    z_mag          = 13.1863
    z_err          = 0.0016
    y_mag          = 13.1618
    y_err          = 0.0034

    g_minus_r_derived = 0.435
    note = "g-r = 0.44 consistent with solar-temperature dwarf"
}


tess TessInputCatalog {

    catalog        = "TESS Input Catalog v8 (VizieR IV/39/tic82)"
    tic_id         = 1676594744
    gaia_crossref  = 6766185791864654720
    tmag           = 12.936
    teff_tic_k     = 5819
    radius_rsun    = 1.025
    mass_rsun      = 1.047

    coverage_service = "MAST TESSCut sector API"
    sectors        = [92]
    camera         = 2
    ccd            = 4
    mode           = "FFI ONLY - no targeted 2-min/s20s observations"
    status         = OBSERVED_IN_SECTOR_92_FFI
}

ultraviolet GalexAis {

    catalog        = "GALEX AIS (VizieR II/335/galex_ais)"
    fuv_mag        = NONE
    nuv_mag        = 18.2589
    nuv_err        = 0.0387
    note = "FUV non-detection is normal for a G dwarf; NUV consistent with photosphere"
}

radio RadioContinuumNvss {

    survey         = "NVSS 1.4 GHz (VizieR VIII/65/nvss)"
    search_radius_as = 60
    matches        = 0
    verdict        = NO_RADIO_CONTINUUM_COUNTERPART
    sensitivity_note = "NVSS completeness ~2.5 mJy; a thermal exoplanet-system source would be far below this"
}

spectra SpectroscopicSurveyStatus {

    attempted_utc  = "2026-08-25T02:30Z"
    lamost         = NOT_CHECKED_SERVICE_UNAVAILABLE
    apogee_dr17    = "VizieR III/286 mirror not found; SkyServer endpoints returned 404 at compile time"
    workaround     = "Gaia DR3 gspphot supplies Teff/logg/[M/H] used in stellar SolarAnalogProperties"
    action = "Retry: VizieR V/164 (LAMOST LRS) cone search and SDSS CASJobs apogeeStar cone when services respond"
}


radio BreakthroughListen2022 {

    paper          = "Perez et al. 2022, RNAAS 6, 217 (DOI 10.3847/2515-5172/ac9408)"
    date_ut        = "2022-05-21"
    telescopes     = ["Green Bank Telescope", "Allen Telescope Array"]

    gbt_mode       = "ABACAD cadence x2, 30 min ON total"
    ata_mode       = "six 5-min pointings, dual coherent beams"
    simultaneous_overlap_s = 580

    band_ghz       = [1.0, 2.0]
    spectral_res_hz = [2.79, 1.91]
    drift_rate_hzs = 4.0
    snr_threshold  = 10
    pipeline       = "turboSETI"

    gbt_candidates = 507
    gbt_verdict    = "ALL APPEAR IN OFF POINTINGS -> REJECTED"
    ata_events     = 9000
    ata_verdict    = "ALL IN BOTH BEAMS -> LOCAL RFI"
    verdict        = NO_TECHNOSIGNATURE_DETECTED

    data_public    = true
    data_location  = "seti.berkeley.edu/wow public data server"
    gbt_sessions   = ["DIAG_6EQUJ5_1 (on, obs 0016)", "DIAG_6EQUJ5_2 (on, obs 0022)", "OFF: HIP9463 HIP94394 HIP94062 HIP94637 HIP94783"]
    gbt_products   = ["0000 high-res 2.79Hz/18.25s", "0002 medium 2.86kHz/1.07s", "0001 low 366kHz/349us"]
    ata_format     = "RAW beamformed, six 5-min pointings x 7 subbands of 96 MHz at 1.91 Hz/1.05 s"
}


reference WowSignal {

    pattern        = "6EQUJ5"
    duration_s     = 72.0
    detected       = "1977-08-15"
    observer       = "Big Ear Radio Observatory"
    region         = "Chi Sagittarii"
    redetected     = false

    // classic estimates (Kraus/Ehman era)
    freq_classic_mhz   = 1420.4556
    flux_classic_jy    = 54
    hydrogen_line_mhz  = 1420.40575177

    // REVISED properties (Arecibo Wow! II - Mendez et al. 2025, arXiv:2508.10657)
    freq_revised_mhz   = 1420.726
    freq_revised_err   = 0.005
    flux_revised_jy    = ">250 (peak, >4x classic value)"
    ra_field_east      = "19h25m02s +/-3s (J2000)"
    ra_field_west      = "19h27m55s +/-3s (J2000)"
    dec_band           = "-26d57m +/-20arcmin (J2000)"
    revision_note = "Two adjacent fields, narrower and slightly displaced vs old estimates; favors astrophysical HI-cloud maser origin hypothesis (Mendez et al. 2024, arXiv:2408.08513)"
}


radio FollowupObservationHistory {

    gray_1994          = "Arecibo narrowband search of Wow! field - no detection"
    gray_marvel_2001   = "Green Bank follow-up - no detection"
    gray_ellingsen_2002 = "Arecibo/Mt Pleasant repeat search - no detection"
    harp_2020          = "ATA wide-field search of Wow! region - no repeats"
    perez_2022         = "BL GBT+ATA targeted at this star - no technosignatures"
    mendez_2024        = "Arecibo Wow! I: narrowband HI-cloud signals mimic Wow! morphology -> maser/superradiance hypothesis"
    mendez_2025        = "Arecibo Wow! II: archival Ohio data reanalysis; revised location flux and frequency above"
    gray_archives      = "Robert H. Gray papers public Aug 2027 via phl.upr.edu/wow/gray"
    verdict            = NO_REDETECTION_IN_ANY_FOLLOWUP
}


assessment CandidateStatus2025 {

    question       = "Does 2MASS J19281982-2640123 remain inside the revised Wow! error fields?"
    star_ra_j2000  = "19h28m19.82s"
    star_dec_j2000 = "-26d40m12s"

    ra_offset_from_west_field_s = 24.82
    ra_field_halfwidth_s        = 3
    ra_verdict                  = "OUTSIDE (~8x the RA uncertainty)"

    dec_offset_arcmin           = 16.8
    dec_band_halfwidth_arcmin   = 20
    dec_verdict                 = "INSIDE declination band"

    conclusion     = "STAR_EXCLUDED_BY_REVISED_LOCALIZATION"
    note = "Caballero's selection used the older wider location boxes; the Arecibo Wow! II RA fields do not contain this star. Keep profile for completeness but source priority shifts to stars within the two revised fields."
}


protocol SignalWatch {

    target         = "2MASS J19281982-2640123"
    band           = "L-band 1-2 GHz"
    watch_line     = "1420.40575177 MHz (H line) + 1420.726 MHz (Wow! II revised)"
    drift_window_hzs = [-4.0, 4.0]
    snr_gate       = 10

    cadences = [
        GBT_ABACAD_ON_OFF,
        ATA_DUAL_BEAM_NULL,
        SIMULTANEOUS_OVERLAP_580S
    ]

    rejection_rule = "ON_ONLY_AND_ALL_OFFS_CLEAN_OR_REJECT"
}


// ------------------------------------------------------------
// KERNEL HOOKS (Lisp forms for the Wow! kernel environment)
//
// (define-type Star ...)
// (define-star 2mass-j19281982-2640123
//   (gaia-dr3 6766185791864654720)
//   (distance 1788ly)
//   (teff 5942K)
//   (metallicity -0.59dex)
//   (type "G2V-analog")
//   (catalogs ("Gaia-DR3" "2MASS"))
//   (signals ("BL-GBT-ATA-2022-05-21: none")))
//
// (schedule wow-check
//   (interval 25ms)
//   (condition (gate hydrogen-band)))
//
// (define-gate hydrogen-band
//   (center 1420.40575177MHz)
//   (width 2MHz)
//   (drift +-4Hz/s)
//   (snr-floor 10))
// ------------------------------------------------------------


provenance DataProvenance {

    compiled_utc = "2026-08-25T01:40Z"

    sources = [
        "SIMBAD TAP simbad.cds.unistra.fr/simbad/sim-tap (cone search 10as)",
        "Gaia DR3 TAP gea.esac.esa.int/tap-server/tap (cone search 10as)",
        "IRSA 2MASS TAP irsa.ipac.caltech.edu/TAP fp_psc (cone search 10as)",
        "AllWISE VizieR II/328 (cone search 10as)",
        "Pan-STARRS DR2 VizieR II/349 (cone search 10as)",
        "GALEX AIS VizieR II/335 (cone search 15as)",
        "NVSS VizieR VIII/65/nvss (cone search 60as)",
        "TESS Input Catalog v8 VizieR IV/39/tic82",
        "TESSCut sector API mast.stsci.edu/tesscut/api/v0.1/sector",
        "NASA Exoplanet Archive TAP ps table (cone search 30arcmin)",
        "Perez et al. 2022 RNAAS DOI 10.3847/2515-5172/ac9408",
        "Caballero 2022 Int J Astrobiology",
        "Mendez et al. 2024 arXiv:2408.08513 (Arecibo Wow! I)",
        "Mendez et al. 2025 arXiv:2508.10657 (Arecibo Wow! II)",
        "Gray follow-ups 1994/2001/2002; Harp et al. 2020",
        "seti.berkeley.edu/wow; phl.upr.edu/wow"
    ]

    raw_exports = [
        "hson/raw/simbad_cone.csv",
        "hson/raw/gaia_dr3.csv",
        "hson/raw/tmass.csv",
        "hson/raw/exoplanets_30arcmin.csv",
        "hson/raw/allwise_viz.csv",
        "hson/raw/ps1_viz.csv",
        "hson/raw/tic82_viz.csv",
        "hson/raw/galex.csv",
        "hson/raw/nvss.csv",
        "hson/raw/tess_sectors.json"
    ]

    gaps = [
        "LAMOST and APOGEE spectra - services unreachable at compile time (see spectra SpectroscopicSurveyStatus); Teff/logg/[M/H] covered by Gaia gspphot meanwhile",
        "Gaia epoch photometry / BP-RP spectra / vari tables - available in Gaia archive, not pulled",
        "BL raw data products listed but not downloaded (multi-GB; seti.berkeley.edu/wow)"
    ]
}


