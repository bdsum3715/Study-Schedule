# Study-Schedule
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover"/>
<meta name="apple-mobile-web-app-capable" content="yes"/>
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent"/>
<meta name="apple-mobile-web-app-title" content="Study Plan"/>
<meta name="theme-color" content="#5C54D4"/>
<title>Ultimate Study Plan</title>
<style>
  *{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
  body{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif;background:#F8FAFC;min-height:100vh;padding-bottom:40px;}
  .safe-top{padding-top:env(safe-area-inset-top,0px);}
  .header{background:linear-gradient(135deg,#5C54D4,#0369A1);color:white;padding:20px 16px 18px;margin-bottom:14px;}
  .header-label{font-size:10px;font-weight:700;letter-spacing:2px;opacity:0.7;text-transform:uppercase;margin-bottom:3px;}
  .header h1{font-size:20px;font-weight:800;margin-bottom:3px;}
  .header p{font-size:12px;opacity:0.85;margin-bottom:14px;}
  .progress-bar{background:rgba(255,255,255,0.25);border-radius:20px;height:9px;margin-bottom:6px;}
  .progress-fill{background:white;border-radius:20px;height:9px;transition:width 0.3s;}
  .progress-label{font-size:11px;opacity:0.8;}
  .nav{display:flex;gap:8px;padding:0 14px;margin-bottom:14px;flex-wrap:wrap;}
  .nav button{padding:9px 16px;border-radius:10px;border:none;cursor:pointer;font-weight:600;font-size:12px;transition:all 0.15s;}
  .nav button.active{background:#5C54D4;color:white;box-shadow:0 3px 10px rgba(92,84,212,0.3);}
  .nav button.inactive{background:white;color:#64748B;box-shadow:0 1px 3px rgba(0,0,0,0.08);}
  .nav button.reset{padding:9px 12px;border:1.5px solid #E2E8F0;background:white;color:#94A3B8;margin-left:auto;}
  .content{padding:0 14px;}
  .phase{margin-bottom:9px;border-radius:12px;overflow:hidden;}
  .phase-header{padding:12px 14px;cursor:pointer;border-left:4px solid;border:1.5px solid;border-radius:12px;user-select:none;}
  .phase-header.open{border-radius:12px 12px 0 0;}
  .phase-dates{font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:0.8px;margin-bottom:2px;}
  .phase-label{font-weight:700;color:#0F172A;font-size:14px;margin-bottom:2px;}
  .phase-note{font-size:11px;color:#64748B;}
  .phase-meta{display:flex;align-items:center;gap:10px;margin-left:10px;flex-shrink:0;}
  .phase-pct{font-weight:800;font-size:15px;}
  .phase-count{font-size:10px;color:#94A3B8;}
  .phase-row{display:flex;justify-content:space-between;align-items:flex-start;}
  .phase-progress{margin-top:8px;border-radius:10px;height:4px;}
  .phase-progress-fill{border-radius:10px;height:4px;transition:width 0.3s;}
  .days{background:white;border:1.5px solid;border-top:none;border-radius:0 0 12px 12px;overflow:hidden;}
  .day{border-bottom:1px solid #F1F5F9;}
  .day:last-child{border-bottom:none;}
  .day-header{padding:10px 15px;cursor:pointer;display:flex;justify-content:space-between;align-items:center;user-select:none;}
  .day-label{font-weight:600;color:#0F172A;font-size:12.5px;}
  .day-circle{width:18px;height:18px;border-radius:50%;border:2px solid #CBD5E1;background:transparent;display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-right:8px;}
  .day-circle.done{border-color:var(--pc);background:var(--pc);}
  .day-circle span{color:white;font-size:10px;font-weight:700;}
  .day-info{display:flex;align-items:center;}
  .day-meta{display:flex;align-items:center;gap:8px;}
  .day-count{font-size:11px;font-weight:600;}
  .tasks{padding:6px 15px 12px;}
  .task{display:flex;gap:9px;padding:7px 9px;border-radius:8px;cursor:pointer;margin-bottom:3px;align-items:flex-start;user-select:none;}
  .task:active{opacity:0.7;}
  .task-box{width:20px;height:20px;border-radius:5px;border:2px solid #CBD5E1;background:white;display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:1px;transition:all 0.15s;}
  .task-box.done{background:var(--pc);border-color:var(--pc);}
  .task-box span{color:white;font-size:11px;font-weight:700;}
  .task-text{font-size:12.5px;color:#334155;line-height:1.5;}
  .task-text.done{color:#94A3B8;text-decoration:line-through;}
  .card{background:white;border-radius:14px;padding:18px;margin-bottom:12px;box-shadow:0 1px 4px rgba(0,0,0,0.06);}
  .card-title{font-weight:700;color:#0F172A;font-size:15px;margin-bottom:14px;}
  .order-item{display:flex;gap:12px;margin-bottom:10px;align-items:flex-start;padding:11px 13px;background:#F8FAFC;border-radius:10px;border-left:3px solid #5C54D4;}
  .order-num{min-width:26px;height:26px;background:#5C54D4;border-radius:50%;display:flex;align-items:center;justify-content:center;color:white;font-weight:700;font-size:13px;flex-shrink:0;}
  .order-title{font-weight:700;color:#0F172A;font-size:13px;}
  .order-note{color:#64748B;font-size:12px;margin-top:2px;}
  .limit-row{display:flex;justify-content:space-between;padding:9px 12px;background:#F8FAFC;border-radius:9px;margin-bottom:4px;align-items:center;border-left:3px solid #0369A1;}
  .limit-rule{color:#334155;font-size:13px;}
  .limit-cards{color:#0369A1;font-weight:700;font-size:13px;}
  .resource-item{padding:10px 12px;background:#F8FAFC;border-radius:10px;margin-bottom:6px;}
  .resource-name{font-weight:700;font-size:13px;}
  .resource-desc{color:#475569;font-size:12px;margin-top:2px;}
  .overview-item{background:white;border-radius:12px;padding:13px 15px;margin-bottom:8px;box-shadow:0 1px 4px rgba(0,0,0,0.05);border-left:4px solid;}
  .overview-label{font-weight:700;font-size:13px;}
  .overview-dates{font-size:11px;color:#94A3B8;margin-bottom:4px;}
  .overview-desc{color:#475569;font-size:13px;}
  .principle-box{background:#EEF2FF;border-radius:14px;padding:14px 16px;margin-top:6px;font-size:13px;color:#334155;line-height:1.7;border:1px solid #C7D2FE;}
</style>
</head>
<body>
<div class="safe-top">
<div class="header">
  <div class="header-label">Step 1 + Year 3 Foundation</div>
  <h1>Ultimate Summer Study Plan</h1>
  <p>Jun 24 – Sep 27 · Year 3 starts Sep 28</p>
  <div class="progress-bar"><div class="progress-fill" id="main-bar" style="width:0%"></div></div>
  <div class="progress-label" id="main-label">0 of 0 tasks · 0% complete</div>
</div>
<div class="nav">
  <button class="active" id="btn-tracker" onclick="showView('tracker')">📋 Tracker</button>
  <button class="inactive" id="btn-order" onclick="showView('order')">📐 Daily Order</button>
  <button class="inactive" id="btn-overview" onclick="showView('overview')">📅 Overview</button>
  <button class="reset inactive" onclick="resetAll()">Reset</button>
</div>
<div class="content">
  <div id="view-tracker"></div>
  <div id="view-order" style="display:none"></div>
  <div id="view-overview" style="display:none"></div>
</div>
</div>

<script>
// All chapter names verified against both uploaded Bootcamp PDFs
const PHASES = [
  {id:"p0",color:"#334155",type:"study",label:"Phase 0 — Setup + General Pathology",dates:"Jun 24–26",note:"3 days · Set up your full system · Begin the language of disease",days:[
    {id:"d0a",label:"Jun 24 Wed — Setup",tasks:[
      "1. AnKing: due reviews only (no new cards today)",
      "2. Set up First Aid as your annotation hub",
      "3. Create AnKing tag system: Pathology · Immunology · Micro · Pharm · Cardio · Pulm · Renal",
      "4. Make Bootcamp + Sketchy checklists for the summer",
      "5. Skim First Aid: How to Use This Book + Step 1 checklist overview",
    ]},
    {id:"d0b",label:"Jun 25 Thu — Cell injury",tasks:[
      "1. AnKing: due reviews (60 min)",
      "2. Bootcamp Pathology: Ch.1 Cell Injury and Death",
      "3. First Aid Pathology: cellular adaptations · reversible/irreversible injury · necrosis vs apoptosis · free radicals · ischemia-reperfusion (20 min checklist)",
      "4. AnKing: unsuspend + do Pathology tag cards only (40–60 new)",
      "5. Qbank: 10 questions — pathology only",
      "6. Weakness log: every wrong answer → topic + why + correct rule",
    ]},
    {id:"d0c",label:"Jun 26 Fri — Inflammation",tasks:[
      "1. AnKing: due reviews (60 min)",
      "2. Bootcamp Immunology: Ch.3 Inflammatory Response",
      "3. First Aid Pathology: acute inflammation · chronic inflammation · granulomas · chemical mediators · wound healing (20 min checklist)",
      "4. AnKing: new cards — inflammation tag",
      "5. Qbank: 10 questions + weakness log",
      "6. Write 3–5 one-line takeaways in notebook",
    ]},
  ]},
  {id:"vac1",color:"#B45309",type:"vacation",label:"Vacation",dates:"Jun 27–29",note:"AnKing reviews ONLY · No new cards · No Bootcamp · No Qbank",days:[
    {id:"vac1a",label:"Jun 27–29 — Vacation",tasks:[
      "AnKing: due reviews only — keep streak alive",
      "No new cards. No Bootcamp. No Sketchy. No Qbank.",
    ]},
  ]},
  {id:"p1",color:"#5C54D4",priority:true,type:"study",label:"Phase 1 — General Pathology, Immunology + Pharm Foundations",dates:"Jun 30 – Jul 13",note:"⭐ Year 3 Priority · 14 days · Reduce new Anki cards Jul 12–13 before vacation",days:[
    {id:"d1a",label:"Jun 30 Tue — Inflammation consolidation + innate immunity",tasks:[
      "1. AnKing: due reviews (60 min)",
      "2. Bootcamp Immunology: Ch.1 Lymphoid Tissue + Ch.2 Innate Immunity",
      "3. First Aid Pathology: inflammation/wound healing consolidation · First Aid Immunology: innate immunity pages (20 min checklist)",
      "4. AnKing: new cards — Immunology tag",
      "5. Qbank: 10–20 path/immuno questions + weakness log",
    ]},
    {id:"d1b",label:"Jul 1 Wed — Hemodynamics + vascular physiology",tasks:[
      "1. AnKing: due reviews (60 min)",
      "2. Bootcamp Cardiology: Ch.3 Vascular System and Cardiac Parameters + Ch.4 (same chapter group)",
      "3. First Aid Pathology: edema · hyperemia/congestion · hemorrhage (20 min checklist)",
      "4. AnKing: new cards",
      "5. Qbank: 10–20 questions + weakness log",
    ]},
    {id:"d1c",label:"Jul 2 Thu — Thrombosis, embolism, infarction",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Cardiology: Ch.7 Vasodilation and Vasoconstriction + Ch.8 Pressure Flow Physiology",
      "3. First Aid Pathology: thrombosis · embolism · infarction mechanisms (20 min checklist)",
      "4. AnKing: new cards",
      "5. Qbank: 10–20 questions + weakness log",
    ]},
    {id:"d1d",label:"Jul 3 Fri — Shock",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Cardiology: Ch.27 Pericardial Disease + Ch.28 Shock",
      "3. First Aid Pathology: shock — all types + hemodynamic parameters (20 min checklist)",
      "4. Make comparison table: septic vs cardiogenic vs hypovolemic vs obstructive (CO · SVR · PCWP)",
      "5. AnKing: new cards",
      "6. Qbank: 15–20 questions + weakness log",
    ]},
    {id:"d1e",label:"Jul 4 Sat — Neoplasia 1",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Hematology/Oncology: Ch.8 Oncology and Therapeutics (conceptual portions only)",
      "3. First Aid Pathology: benign vs malignant · dysplasia · carcinoma in situ · invasion · metastasis · grading/staging (20 min checklist)",
      "4. AnKing: new cards",
      "5. Qbank: 10–20 questions + weakness log",
    ]},
    {id:"d1f",label:"Jul 5 Sun — Neoplasia 2 + hemostasis bridge",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Hematology/Oncology: Ch.6 Platelets + Ch.7 Coagulation and Fibrinolysis",
      "3. First Aid Pathology: oncogenes · tumor suppressors · cancer hallmarks · paraneoplastic syndromes (20 min checklist)",
      "4. Know cold: p53 · RB · APC · BCL2 — mechanism + associated cancer",
      "5. AnKing: new cards",
      "6. Qbank: 15–25 questions + weakness log",
    ]},
    {id:"d1g",label:"Jul 6 Mon — ⭐ Pathology REVIEW DAY",tasks:[
      "1. AnKing: due reviews",
      "2. Review all Bootcamp Pathology chapters studied so far — no new videos",
      "3. First Aid Pathology: full section sweep (checklist)",
      "4. Build mechanism map from memory: cell injury → inflammation → repair · thrombosis → ischemia → infarction · mutation → neoplasia",
      "5. Qbank: 30–40 mixed pathology questions",
      "6. Weakness log: review all entries from this week",
    ]},
    {id:"d1h",label:"Jul 7 Tue — Immunology 1: adaptive immunity + T cells",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Immunology: Ch.4 Cytokines + Ch.5 T cells",
      "3. First Aid Immunology: T cell section (20 min checklist)",
      "4. AnKing: new cards — Immunology tag",
      "5. Qbank: 10–20 questions + weakness log",
    ]},
    {id:"d1i",label:"Jul 8 Wed — Immunology 2: B cells, antibodies, complement",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Immunology: Ch.6 B cells + Ch.7 Antibodies + Ch.8 Complement",
      "3. First Aid Immunology: complement deficiency table (20 min checklist)",
      "4. Make table: C1/C2/C4 vs C3 vs C5-C9 defects + infection risks",
      "5. Know cold: C3 deficiency = pyogenic · C5-C9 deficiency = Neisseria ONLY",
      "6. AnKing: new cards",
      "7. Qbank: 10–20 questions + weakness log",
    ]},
    {id:"d1j",label:"Jul 9 Thu — Immunology 3: vaccines + immunodeficiency",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Immunology: Ch.9 Vaccinations + Ch.10 Immunodeficiency Syndromes",
      "3. First Aid Immunology: immunodeficiency tables (20 min checklist)",
      "4. Tie every defect: inheritance + mechanism + infection risk + lab finding",
      "5. AnKing: new cards",
      "6. Qbank: 10–20 questions + weakness log",
    ]},
    {id:"d1k",label:"Jul 10 Fri — Immunology 4: hypersensitivity + transplant",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Immunology: Ch.11 Hypersensitivity Syndromes + Ch.12 Transfusion Reactions + Ch.13 Transplant Rejection",
      "3. First Aid Immunology: hypersensitivity + transplant sections (20 min checklist)",
      "4. Make Type I–IV table: type → mediator → example → treatment",
      "5. Make transplant rejection timeline: hyperacute / acute / chronic — timing + mechanism",
      "6. AnKing: new cards",
      "7. Qbank: 10–20 questions + weakness log",
    ]},
    {id:"d1l",label:"Jul 11 Sat — Pharm Foundations 1: Pharmacodynamics",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Pharmacology: Ch.1 Pharmacodynamics",
      "3. Sketchy Pharmacology: Pharmacology Foundations group — open the Pharmacology Foundations module and watch all videos in order (watch TWICE — story then active recall)",
      "4. First Aid Pharmacology: PD section (20 min checklist)",
      "5. Know cold: potency vs efficacy · EC50 · ED50 · therapeutic index · agonist/antagonist/partial agonist curves",
      "6. AnKing: new cards — Pharmacology tag",
      "7. Qbank: 10–20 pharm questions + weakness log",
    ]},
    {id:"d1m",label:"Jul 12 Sun — Pharm Foundations 2: Pharmacokinetics",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Pharmacology: Ch.2 Pharmacokinetics + Ch.4 Side Effects and Toxins",
      "3. First Aid Pharmacology: PK section (20 min checklist)",
      "4. Know: Vd = dose/plasma conc · CL = Vd × ke · t½ = 0.7/ke · loading dose · maintenance dose · CYP basics",
      "5. LIMIT new AnKing cards today — vacation in 2 days",
      "6. Qbank: 10–20 questions + weakness log",
    ]},
    {id:"d1n",label:"Jul 13 Mon — Autonomics + pre-vacation consolidation",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Pharmacology: Ch.3 Autonomic System",
      "3. Sketchy Pharmacology: Autonomic Drugs group — open the Autonomic Drugs module and watch all videos in order (watch TWICE — story then active recall)",
      "4. First Aid Pharmacology: autonomics section (20 min checklist)",
      "5. Make receptor table: alpha-1/2 · beta-1/2 · M1-M3 · nicotinic — receptor + location + effect",
      "6. Quiz: cover 'effect' column and reproduce from memory",
      "7. STOP large new card batches today",
      "8. Qbank: 30–40 mixed path/immuno/pharm questions",
      "9. ⭐ Saturday rule: go through all weakness log entries from this week",
    ]},
  ]},
  {id:"vac2",color:"#B45309",type:"vacation",label:"Vacation",dates:"Jul 14–26",note:"AnKing reviews ONLY · Prioritize Path · Immuno · Pharm reviews · No new cards",days:[
    {id:"vac2a",label:"Jul 14–26 — Vacation (13 days)",tasks:[
      "AnKing: due reviews only, every day",
      "No new cards. Prioritize: Pathology · Immunology · Pharm foundation reviews",
      "Goal: return without backlog",
    ]},
  ]},
  {id:"p2",color:"#B91C1C",priority:true,type:"study",label:"Phase 2 — Medical Microbiology + Antimicrobial Pharmacology",dates:"Jul 27 – Aug 9",note:"⭐ Sketchy-first for every organism · Watch TWICE · Bootcamp confirms · STOP large cards Aug 9",days:[
    {id:"d2a",label:"Jul 27 Mon — Micro framework: fundamentals + bacterial genetics + toxins",tasks:[
      "1. AnKing: due reviews (60–75 min)",
      "2. Bootcamp Microbiology: Ch.1 Fundamentals of Bacteriology",
      "3. Bootcamp Microbiology: Ch.2 Bacterial Genetics",
      "4. Bootcamp Microbiology: Ch.3 Bacterial Toxins",
      "5. Sketchy Micro: Bacteria group — open the Bacteria module · watch the intro/framework videos in order (watch TWICE each — story then active recall)",
      "6. First Aid Microbiology: bacteria intro tables — virulence factors · toxins (20 min checklist)",
      "7. Know: transformation · transduction · conjugation · exotoxin vs endotoxin mechanisms",
      "8. AnKing: new cards — Micro tag",
      "9. Draw gram stain decision tree from memory at end of day",
      "10. Qbank: 15–20 questions + weakness log",
    ]},
    {id:"d2b",label:"Jul 28 Tue — Gram-positive cocci: Staph + Strep",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.4 Staphylococcus",
      "3. Bootcamp Microbiology: Ch.5 Streptococcus",
      "4. Sketchy Micro: Bacteria group — watch Staph aureus · Staph epidermidis · Strep pyogenes · Strep pneumoniae · Strep agalactiae · Strep viridans videos in order (watch TWICE each)",
      "5. First Aid Microbiology: Staph + Strep tables (20 min checklist)",
      "6. Pharm tie-in: beta-lactams (mechanism + resistance) · vancomycin (Red Man syndrome + nephrotoxicity)",
      "7. AnKing: new cards",
      "8. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2c",label:"Jul 29 Wed — Enterococcus, Bacillus, Clostridium, Mycobacteria",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.6 Enterococcus and Bacillus",
      "3. Bootcamp Microbiology: Ch.7 Clostridium",
      "4. Bootcamp Microbiology: Ch.8 Mycobacteria",
      "5. Sketchy Micro: Bacteria group — watch Enterococcus · Bacillus anthracis · Bacillus cereus · C. difficile · C. tetani · C. botulinum · C. perfringens · M. tuberculosis · M. leprae videos in order (watch TWICE each)",
      "6. First Aid Microbiology: Clostridium + Mycobacteria sections (20 min checklist)",
      "7. Know C. diff/tetani/botulinum toxin mechanisms cold",
      "8. Pharm tie-in: TB drugs RIPE — rifampin · isoniazid · pyrazinamide · ethambutol (mechanism + toxicity each)",
      "9. AnKing: new cards",
      "10. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2d",label:"Jul 30 Thu — Non-spore G+ rods + spirochetes + atypical bacteria",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.9 Non-Spore Forming Gram Positive Bacilli",
      "3. Bootcamp Microbiology: Ch.15 Spirochetes",
      "4. Bootcamp Microbiology: Ch.16 Atypical Bacteria",
      "5. Sketchy Micro: Bacteria group — watch Listeria · Corynebacterium · Actinomyces · Nocardia · Treponema pallidum · Borrelia · Leptospira · Chlamydia · Mycoplasma · Rickettsia videos in order (watch TWICE each)",
      "6. First Aid Microbiology: spirochetes + atypicals sections (20 min checklist)",
      "7. Know: Lyme disease stages · syphilis stages · Chlamydia vs Mycoplasma differences",
      "8. AnKing: new cards",
      "9. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2e",label:"Jul 31 Fri — Gram-negative rods I: lactose + non-lactose fermenting",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.10 Lactose Fermenting Gram Negative Bacilli",
      "3. Bootcamp Microbiology: Ch.11 Non-Lactose Fermenting Gram Negative Bacilli",
      "4. Sketchy Micro: Bacteria group — watch E. coli · Klebsiella · Enterobacter · Serratia · Proteus · Salmonella · Shigella · Pseudomonas · Burkholderia videos in order (watch TWICE each)",
      "5. First Aid Microbiology: gram-negative rod tables (20 min checklist)",
      "6. Pharm tie-in: aminoglycosides (30S · nephro/ototoxicity) · fluoroquinolones (DNA gyrase) · cephalosporins by generation",
      "7. AnKing: new cards",
      "8. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2f",label:"Aug 1 Sat — Gram-negative curved bacilli + diplococci + coccobacilli",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.12 Gram Negative Curved Bacilli",
      "3. Bootcamp Microbiology: Ch.13 Gram Negative Diplococci",
      "4. Bootcamp Microbiology: Ch.14 Gram Negative Coccobacilli",
      "5. Sketchy Micro: Bacteria group — watch H. pylori · Campylobacter · Vibrio cholerae · N. meningitidis · N. gonorrhoeae · H. influenzae · Bordetella · Pasteurella · Brucella · Francisella videos in order (watch TWICE each)",
      "6. First Aid Microbiology: Neisseria + coccobacilli tables (20 min checklist)",
      "7. Know: N. meningitidis vs N. gonorrhoeae differences · H. pylori triple/quadruple therapy",
      "8. AnKing: new cards",
      "9. Qbank: 20 questions + weakness log",
      "10. ⭐ Saturday rule: go through all weakness log entries from this week",
    ]},
    {id:"d2g",label:"Aug 2 Sun — ⭐ Bacteria REVIEW DAY",tasks:[
      "1. AnKing: due reviews",
      "2. Review Bootcamp Microbiology Ch.1–16 — no new videos, consolidation only",
      "3. First Aid Microbiology: full bacteriology tables sweep (checklist)",
      "4. Focus: toxin → mechanism · organism → immune defect association · organism → syndrome → drug class",
      "5. Build missed-organism list for targeted re-review",
      "6. Qbank: 40 mixed bacteria questions + weakness log review",
    ]},
    {id:"d2h",label:"Aug 3 Mon — Virology basics + positive-sense + negative-sense RNA viruses",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.26 Approach to Virology + Ch.27 Basics of Virology",
      "3. Bootcamp Microbiology: Ch.28 Positive Sense RNA Viruses",
      "4. Bootcamp Microbiology: Ch.29 Negative Sense RNA Viruses",
      "5. Sketchy Micro: Viruses – RNA Viruses group — open the RNA Viruses module and watch all videos in order (watch TWICE each)",
      "6. First Aid Microbiology: viral genome chart (20 min checklist)",
      "7. Know: +sense RNA = directly translated · −sense RNA = needs RNA-dependent RNA polymerase first",
      "8. AnKing: new cards — Virology tag",
      "9. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2i",label:"Aug 4 Tue — Double-stranded RNA viruses + DNA viruses",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.30 Double Stranded RNA Viruses",
      "3. Bootcamp Microbiology: Ch.31 DNA Viruses",
      "4. Sketchy Micro: Viruses – DNA Viruses group — open the DNA Viruses module and watch all videos in order (watch TWICE each)",
      "5. First Aid Microbiology: DNA virus tables (20 min checklist)",
      "6. Pharm tie-in: acyclovir (HSV/VZV · TK activation) · ganciclovir (CMV) · foscarnet (CMV resistance) · oseltamivir (influenza NA inhibitor)",
      "7. AnKing: new cards",
      "8. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2j",label:"Aug 5 Wed — Mycology: dimorphic + opportunistic + tinea",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.17 Dimorphic Mycosis",
      "3. Bootcamp Microbiology: Ch.18 Opportunistic Mycosis",
      "4. Bootcamp Microbiology: Ch.19 Tinea",
      "5. Sketchy Micro: Fungi group — open the Fungi module and watch all videos in order (watch TWICE each)",
      "6. First Aid Microbiology: fungi section (20 min checklist)",
      "7. Dimorphic rule: mold in cold · yeast in heat (except Coccidioides = spherules in tissue)",
      "8. Pharm tie-in: amphotericin B (ergosterol membrane) · azoles (ergosterol synthesis) · echinocandins (beta-glucan) · flucytosine · terbinafine",
      "9. AnKing: new cards — Fungi tag",
      "10. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2k",label:"Aug 6 Thu — Parasitology: protozoa, nematodes, cestodes, trematodes, ectoparasites",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.20 Gastrointestinal Protozoa",
      "3. Bootcamp Microbiology: Ch.21 Systemic Protozoa",
      "4. Bootcamp Microbiology: Ch.22 Nematodes",
      "5. Bootcamp Microbiology: Ch.23 Cestodes",
      "6. Bootcamp Microbiology: Ch.24 Trematodes + Ch.25 Ectoparasites",
      "7. Sketchy Micro: Parasites group — open the Parasites module and watch all videos in order (watch TWICE each)",
      "8. First Aid Microbiology: parasite tables (20 min checklist)",
      "9. Pharm tie-in: metronidazole · albendazole/mebendazole · praziquantel · ivermectin — mechanisms each",
      "10. AnKing: new cards — Parasites tag",
      "11. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2l",label:"Aug 7 Fri — Antibiotics",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.36 Antibiotics",
      "3. Sketchy Pharmacology: Antimicrobials group — open the Antimicrobials module and watch all videos in order (watch TWICE each)",
      "4. First Aid Pharmacology: antibiotic tables (20 min checklist)",
      "5. Know by category: cell wall (beta-lactams · vancomycin · bacitracin) · 30S (aminoglycosides · tetracyclines) · 50S (macrolides · linezolid · clindamycin · chloramphenicol) · DNA/RNA (fluoroquinolones · rifampin · metronidazole) · folate (sulfonamides · trimethoprim)",
      "6. For every class: mechanism + major toxicity + resistance mechanism",
      "7. AnKing: new cards — antibiotic tag",
      "8. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2m",label:"Aug 8 Sat — Antifungals + antiparasitics + antivirals",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.37 Antifungals",
      "3. Bootcamp Microbiology: Ch.38 Antiparasitics",
      "4. Bootcamp Microbiology: Ch.39 Antivirals",
      "5. Sketchy Pharmacology: Antimicrobials group — continue with antifungal · antiviral · antiparasitic videos in order (watch TWICE each)",
      "6. First Aid Pharmacology: antifungal · antiviral · antiparasitic sections (20 min checklist)",
      "7. For every class: mechanism + major toxicity + contraindication + resistance",
      "8. LIMIT new cards today — vacation in 2 days",
      "9. Qbank: 20 questions + weakness log",
      "10. ⭐ Saturday rule: go through all weakness log entries from this week",
    ]},
    {id:"d2n",label:"Aug 9 Sun — ⭐ Micro/Pharm REVIEW DAY",tasks:[
      "1. AnKing: due reviews",
      "2. Review Bootcamp Microbiology Ch.1–39 + all antimicrobials — no new videos",
      "3. First Aid Microbiology + Pharmacology: full tables sweep (checklist)",
      "4. Quiz: cover treatment column → reproduce from organism name only",
      "5. Build: missed-organism list + drug-class toxicity list",
      "6. STOP large new card batches — vacation starts tomorrow",
      "7. Qbank: 40 mixed micro/pharm questions + weakness log review",
    ]},
  ]},
  {id:"vac3",color:"#B45309",type:"vacation",label:"Vacation",dates:"Aug 10–24",note:"AnKing reviews ONLY · Prioritize Microbiology + Antimicrobial Pharm reviews · No new cards",days:[
    {id:"vac3a",label:"Aug 10–24 — Vacation (15 days)",tasks:[
      "AnKing: due reviews only, every day",
      "No new cards. Prioritize: Microbiology + Antimicrobial Pharm reviews",
      "Goal: no backlog explosion. Return ready for Cardio/Pulm/Renal.",
    ]},
  ]},
  {id:"p3",color:"#047857",priority:true,type:"study",label:"Phase 3 — Physiology → Pathophysiology → Pharm: Cardio, Pulm, Renal",dates:"Aug 25 – Sep 5",note:"⭐ Physiology ALWAYS before pathology · Formula: normal → disease → compensation → drug · STOP cards Sep 5",days:[
    {id:"d3a",label:"Aug 25 Tue — Cardio physiology 1: embryology, anatomy, vascular system, PV loops",tasks:[
      "1. AnKing: due reviews (60–75 min) — clear any vacation backlog first",
      "2. Bootcamp Cardiology: Ch.1 Embryology and Anatomy + Ch.2 (same chapter group)",
      "3. Bootcamp Cardiology: Ch.3 Vascular System and Cardiac Parameters + Ch.4 (same chapter group)",
      "4. Bootcamp Cardiology: Ch.5 Cardiac Function and PV Loops + Ch.6 (same chapter group)",
      "5. First Aid Cardiology: cardiac physiology section (20 min checklist)",
      "6. Know: preload · afterload · contractility · Frank-Starling curve · PV loop shifts",
      "7. Draw: normal PV loop from memory — then add effect of increased afterload",
      "8. AnKing: new cards — Cardiology physiology tag",
      "9. Qbank: 15–20 questions + weakness log",
    ]},
    {id:"d3b",label:"Aug 26 Wed — Cardio physiology 2: vasodilation, cardiac cycle, RAAS, conduction",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Cardiology: Ch.7 Vasodilation and Vasoconstriction + Ch.8 Pressure Flow Physiology",
      "3. Bootcamp Cardiology: Ch.9 Cardiac Cycle",
      "4. Bootcamp Cardiology: Ch.10 RAAS",
      "5. Bootcamp Cardiology: Ch.11 Exercise and Cardiac Conductive Physiology + Ch.12 (same chapter group)",
      "6. Sketchy Pharmacology: Cardiovascular and Renal group — open the Cardiovascular and Renal module and watch all videos in order (watch TWICE each)",
      "7. First Aid Cardiology: RAAS + cardiac cycle (20 min checklist)",
      "8. Know RAAS step by step: renin → Ang I → ACE → Ang II → aldosterone → effect",
      "9. AnKing: new cards",
      "10. Qbank: 15–20 questions + weakness log",
    ]},
    {id:"d3c",label:"Aug 27 Thu — Cardio pathophysiology 1: antiarrhythmics + arrhythmias + conduction block",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Cardiology: Ch.13 Antiarrhythmics",
      "3. Bootcamp Cardiology: Ch.14 Atrial and Ventricular Arrhythmias + Ch.15 (same chapter group)",
      "4. Bootcamp Cardiology: Ch.16 Conduction Block",
      "5. First Aid Cardiology: arrhythmias + antiarrhythmics sections (20 min checklist)",
      "6. Know antiarrhythmics by Vaughan-Williams class I–IV: mechanism + prototype + toxicity",
      "7. AnKing: new cards",
      "8. Qbank: 20 questions + weakness log",
    ]},
    {id:"d3d",label:"Aug 28 Fri — Cardio pathophysiology 2: HF, cardiomyopathy, HTN, shock",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Cardiology: Ch.17 Heart Failure",
      "3. Bootcamp Cardiology: Ch.18 Cardiomyopathy",
      "4. Bootcamp Cardiology: Ch.26 Hypertension",
      "5. Bootcamp Cardiology: Ch.27 Pericardial Disease + Ch.28 Shock",
      "6. First Aid Cardiology: heart failure + shock sections (20 min checklist)",
      "7. Know: systolic vs diastolic HF on PV loop · shock types: CO/SVR/PCWP for each",
      "8. Pharm tie-in: ACEi/ARB · beta-blockers · diuretics · nitrates · digoxin · vasodilators",
      "9. AnKing: new cards",
      "10. Qbank: 20 questions + weakness log",
    ]},
    {id:"d3e",label:"Aug 29 Sat — Cardio pathophysiology 3: ischemia, aortic, valvular, congenital",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Cardiology: Ch.23 Stable Angina and Atherosclerosis",
      "3. Bootcamp Cardiology: Ch.24 Myocardial Infarction",
      "4. Bootcamp Cardiology: Ch.19 Aortic Disease",
      "5. Bootcamp Cardiology: Ch.20 Valvular Disease",
      "6. Bootcamp Cardiology: Ch.21 Acyanotic and Cyanotic Congenital Heart Defects + Ch.22 (same chapter group)",
      "7. Bootcamp Cardiology: Ch.25 Peripheral Venous and Arterial Disease",
      "8. First Aid Cardiology: MI · valvular · congenital sections (20 min checklist)",
      "9. Know: STEMI vs NSTEMI vs UA management · murmur table (systolic/diastolic · location · Valsalva/squat effect)",
      "10. Pharm tie-in: antiplatelets · thrombolytics (tPA) · statins (HMG-CoA reductase)",
      "11. AnKing: new cards",
      "12. Qbank: 30–40 mixed cardio questions",
      "13. ⭐ Saturday rule: go through all weakness log entries from this week",
    ]},
    {id:"d3f",label:"Aug 30 Sun — Pulmonary physiology: introduction, air, blood",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Pulmonology: Ch.1 Introduction",
      "3. Bootcamp Pulmonology: Ch.2 Air",
      "4. Bootcamp Pulmonology: Ch.3 Blood Physiology",
      "5. First Aid Pulmonology: physiology section (20 min checklist)",
      "6. Know: TLC · FRC · RV · ERV · IRV · TV · V/Q mismatch · A-a gradient · oxygenation vs ventilation",
      "7. Draw: V/Q lung unit from memory",
      "8. AnKing: new cards — Pulm tag",
      "9. Qbank: 15–20 questions + weakness log",
    ]},
    {id:"d3g",label:"Aug 31 Mon — Pulmonary pathophysiology: obstructive + restrictive + lung cancer",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Pulmonology: Ch.4 Lung Pathology Fundamentals",
      "3. Bootcamp Pulmonology: Ch.5 Obstructive Lung Disease",
      "4. Bootcamp Pulmonology: Ch.6 Restrictive Lung Disease",
      "5. Bootcamp Pulmonology: Ch.7 Lung Cancer",
      "6. First Aid Pulmonology: obstructive + restrictive + lung cancer sections (20 min checklist)",
      "7. Know: FEV1/FVC <70% = obstructive · normal/elevated FEV1/FVC + low TLC = restrictive",
      "8. Know lung cancer: small cell (SIADH/ACTH · central) · squamous (PTHrP · central) · adenocarcinoma (peripheral · most common)",
      "9. Pharm tie-in: SABA/LABA · anticholinergics (M3 block) · ICS · leukotriene modifiers · theophylline (PDE inhibitor)",
      "10. AnKing: new cards",
      "11. Qbank: 20 questions + weakness log",
    ]},
    {id:"d3h",label:"Sep 1 Tue — Pulmonary special topics + review",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Pulmonology: Ch.8 Lung Pathology Special Topics",
      "3. First Aid Pulmonology: PE · ARDS · pulmonary HTN · pleural effusions (20 min checklist)",
      "4. Review: PE (saddle embolus → right heart strain) · ARDS (diffuse alveolar damage · non-cardiogenic · low PCWP)",
      "5. Make: PE diagnosis flowchart — Wells criteria → CT-PA → anticoagulation decision",
      "6. AnKing: new cards",
      "7. Qbank: 30 mixed pulm questions + weakness log",
    ]},
    {id:"d3i",label:"Sep 2 Wed — Renal physiology: anatomy, filtration, nephron transporters, RAAS",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Nephrology: Ch.1 Anatomy and Embryology",
      "3. Bootcamp Nephrology: Ch.2 Fluid and Filtration",
      "4. Bootcamp Nephrology: Ch.3 Nephron Transporters",
      "5. Bootcamp Nephrology: Ch.4 RAAS",
      "6. First Aid Nephrology: nephron physiology section (20 min checklist)",
      "7. Know: GFR equation · Starling forces across glomerulus",
      "8. Know every nephron segment: transporter + what it moves + what drug targets it",
      "9. Draw nephron from PCT → loop of Henle → DCT → collecting duct with all transporters from memory",
      "10. AnKing: new cards — Renal tag",
      "11. Qbank: 15–20 questions + weakness log",
    ]},
    {id:"d3j",label:"Sep 3 Thu — Renal physiology 2: electrolytes + acid-base",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Nephrology: Ch.5 Electrolytes",
      "3. Bootcamp Nephrology: Ch.6 Acid Base Physiology",
      "4. First Aid Nephrology: electrolytes + acid-base (20 min checklist)",
      "5. Know all 4 primary acid-base disorders + compensation rules",
      "6. Know Winter's formula: expected pCO2 = 1.5(HCO3) + 8 ± 2",
      "7. Make diuretic table: drug → nephron site → transporter targeted → electrolyte effect",
      "8. Pharm: acetazolamide (PCT) · loop diuretics (TALH) · thiazides (DCT) · spironolactone/eplerenone (CD · aldosterone antagonist) · amiloride (CD · ENaC)",
      "9. AnKing: new cards",
      "10. Qbank: 20 questions + weakness log",
      "11. ⭐ Saturday rule: go through all weakness log entries from this week",
    ]},
    {id:"d3k",label:"Sep 4 Fri — Renal pathophysiology: nephrotic + nephritic + kidney injury",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Nephrology: Ch.7 Pathology Diagnostics + Ch.8 Nephrotic Syndromes",
      "3. Bootcamp Nephrology: Ch.9 Nephritic Syndromes",
      "4. Bootcamp Nephrology: Ch.12 Kidney Injury",
      "5. First Aid Nephrology: nephrotic + nephritic + AKI sections (20 min checklist)",
      "6. Nephrotic: minimal change (kids · selective albuminuria) · membranous nephropathy (adults · spike-and-dome) · FSGS",
      "7. Nephritic: IgA nephropathy (post-URI) · post-streptococcal GN (weeks after) · RPGN (crescents on biopsy)",
      "8. Make comparison table: nephrotic vs nephritic — mechanism · UA · complement · treatment",
      "9. AnKing: new cards",
      "10. Qbank: 20 questions + weakness log",
    ]},
    {id:"d3l",label:"Sep 5 Sat — Renal pharm + stones + integrated review",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Nephrology: Ch.10 Nephrolithiasis",
      "3. Bootcamp Nephrology: Ch.11 Urinary Incontinence",
      "4. Bootcamp Nephrology: Ch.13 Inflammatory Conditions and Malignancy",
      "5. Bootcamp Nephrology: Ch.14 Cystic Kidney Disease",
      "6. Bootcamp Nephrology: Ch.15 Pharmacology",
      "7. Sketchy Pharmacology: Cardiovascular and Renal group — re-watch renal pharm videos for consolidation",
      "8. First Aid Nephrology: pharmacology + kidney stone sections (20 min checklist)",
      "9. Know stone types: calcium oxalate (acidic urine) · uric acid (gout · allopurinol) · struvite (urease+ bacteria) · cystine (alkalinize urine)",
      "10. STOP large new card batches — long vacation starts tomorrow",
      "11. Qbank: 40 mixed Cardio/Pulm/Renal questions",
      "12. ⭐ Saturday rule: go through all weakness log entries — final Phase 3 sweep",
    ]},
  ]},
  {id:"vac4",color:"#B45309",type:"vacation",label:"Vacation",dates:"Sep 6–24",note:"AnKing reviews ONLY · Prioritize physiology/pathophysiology + pharm reviews · No new cards",days:[
    {id:"vac4a",label:"Sep 6–24 — Vacation (19 days)",tasks:[
      "AnKing: due reviews only, every day",
      "No new cards. Prioritize: physiology/pathophys and pharmacology reviews",
      "Goal: preserve foundation before Year 3 starts September 28",
    ]},
  ]},
  {id:"p4",color:"#0F766E",type:"study",label:"Phase 4 — Pre-Year 3 Launch",dates:"Sep 25–27 · Year 3 begins Sep 28",note:"Light review + system setup only — NOT for new content",days:[
    {id:"d4a",label:"Sep 25 Fri — Pathology + heme/coag review",tasks:[
      "1. AnKing: due reviews (clear any backlog first)",
      "2. Bootcamp Hematology/Oncology: Ch.2 Blood Cells",
      "3. Bootcamp Hematology/Oncology: Ch.6 Platelets",
      "4. Bootcamp Hematology/Oncology: Ch.7 Coagulation and Fibrinolysis",
      "5. Sketchy Pharmacology: Blood and Inflammation group + Smooth Muscle group — open each module and watch all videos in order (consolidation pass)",
      "6. First Aid Hematology: heme/coag tables (20 min checklist)",
      "7. Review General Pathology: cell injury · inflammation · hemodynamics · thrombosis · shock · neoplasia",
      "8. Build coagulation cascade from memory: intrinsic vs extrinsic vs common pathway",
      "9. Qbank: 30–40 mixed path/heme questions",
    ]},
    {id:"d4b",label:"Sep 26 Sat — Pharmacology master review",tasks:[
      "1. AnKing: due reviews",
      "2. Sketchy Pharmacology: Pharmacology Foundations group + Autonomic Drugs group + Antimicrobials group + Cardiovascular and Renal group — re-watch consolidation pass (select weak videos only)",
      "3. Review Bootcamp Pharmacology: Ch.1 Pharmacodynamics · Ch.2 Pharmacokinetics · Ch.3 Autonomic System · Ch.4 Side Effects and Toxins",
      "4. First Aid Pharmacology: general principles sections (20 min checklist)",
      "5. Make drug-class weakness list — which classes feel shakiest going into Year 3?",
      "6. Qbank: 30–40 pharm questions",
      "7. ⭐ Saturday rule: final summer-wide weakness log sweep",
    ]},
    {id:"d4c",label:"Sep 27 Sun — Year 3 readiness",tasks:[
      "1. AnKing: light reviews only",
      "2. Rapid review: Microbiology Ch.1–39 weak list",
      "3. Rapid review: Cardio/Pulm/Renal physio-pathophys maps",
      "4. Rapid review: Immunology Ch.1–13 weak list",
      "5. Set up Year 3 workflow: (a) FA preview 10–15 min before lecture · (b) Bootcamp or Sketchy after lecture · (c) unsuspend AnKing same day · (d) 10–20 Qbank questions within 48h · (e) weekend: mixed review + weakness log",
      "6. Write top 10 weaknesses — this is your Year 3 Week 1 priority list",
      "7. Sleep well. Year 3 starts tomorrow.",
      "8. ✅ SUMMER COMPLETE — Path · Immuno · Pharm · Micro · Cardio · Pulm · Renal all covered",
    ]},
  ]},
];

const DAILY_ORDER=[
  {n:1,t:"AnKing: due reviews",note:"Always first — before Bootcamp, before everything. 60 min."},
  {n:2,t:"Bootcamp or Sketchy",note:"Bootcamp for physiology/path/immuno/pharm foundations. Sketchy for Micro + Pharm ONLY. 90–120 min."},
  {n:3,t:"First Aid — same topic",note:"Checklist read after Bootcamp/Sketchy. Annotate gaps. 20–30 min max."},
  {n:4,t:"AnKing: new cards",note:"Today's topic ONLY. 40–80 normal / max 100 heavy / 0–30 review day / 0 vacation."},
  {n:5,t:"Qbank questions",note:"10–20 early phases → 30–40 later. Every wrong answer → weakness log immediately."},
  {n:6,t:"Weakness log",note:"Topic + why I missed it + correct rule in one line + fix resource."},
];

const OVERVIEW=[
  {c:"#334155",l:"Phase 0",d:"Jun 24–26",desc:"Setup. Cell injury, necrosis, apoptosis. Bootcamp Pathology Ch.1 + Immunology Ch.3 Inflammatory Response."},
  {c:"#B45309",l:"Vacation",d:"Jun 27–29",desc:"AnKing reviews only."},
  {c:"#5C54D4",l:"Phase 1 ⭐",d:"Jun 30 – Jul 13",desc:"General pathology: hemodynamics, thrombosis, shock, neoplasia. Immunology Ch.1–13. Pharm Ch.1–3 + Sketchy Autonomic Drugs module."},
  {c:"#B45309",l:"Vacation",d:"Jul 14–26",desc:"AnKing reviews only."},
  {c:"#B91C1C",l:"Phase 2 ⭐",d:"Jul 27 – Aug 9",desc:"Bootcamp Micro Ch.1–39 in order. Sketchy Micro: Bacteria · RNA Viruses · DNA Viruses · Fungi · Parasites modules. Sketchy Pharm: Antimicrobials module."},
  {c:"#B45309",l:"Vacation",d:"Aug 10–24",desc:"AnKing reviews only."},
  {c:"#047857",l:"Phase 3 ⭐",d:"Aug 25 – Sep 5",desc:"Bootcamp Cardiology Ch.1–28 (5 days) → Pulmonology Ch.1–8 (3 days) → Nephrology Ch.1–15 (3 days). Physiology always before pathology. Sketchy Pharm: Cardiovascular and Renal module."},
  {c:"#B45309",l:"Vacation",d:"Sep 6–24",desc:"AnKing reviews only."},
  {c:"#0F766E",l:"Phase 4",d:"Sep 25–27",desc:"Light review: Bootcamp Heme/Onc Ch.2·6·7 + Sketchy Pharm consolidation. Pharm master review. Year 3 workflow setup. Year 3 starts Sep 28."},
];

let checked={},openPhase=null,openDay=null,currentView='tracker';

function load(){try{const s=localStorage.getItem('sp_v5');if(s)checked=JSON.parse(s);}catch(e){}}
function save(){try{localStorage.setItem('sp_v5',JSON.stringify(checked));}catch(e){}}
function allIds(){return PHASES.flatMap(p=>p.days.flatMap(d=>d.tasks.map((_,i)=>`${d.id}_${i}`)));}
function phaseDone(ph){return ph.days.flatMap(d=>d.tasks.map((_,i)=>`${d.id}_${i}`)).filter(id=>checked[id]).length;}
function phaseTotal(ph){return ph.days.flatMap(d=>d.tasks).length;}
function dayDone(d){return d.tasks.filter((_,i)=>checked[`${d.id}_${i}`]).length;}

function updateHeader(){
  const ids=allIds(),done=ids.filter(id=>checked[id]).length,pct=ids.length?Math.round(done/ids.length*100):0;
  document.getElementById('main-bar').style.width=pct+'%';
  document.getElementById('main-label').textContent=`${done} of ${ids.length} tasks · ${pct}% complete`;
}

function showView(v){
  currentView=v;
  ['tracker','order','overview'].forEach(n=>{
    document.getElementById('view-'+n).style.display=n===v?'block':'none';
    const b=document.getElementById('btn-'+n);
    if(b)b.className=n===v?'active':'inactive';
  });
}

function resetAll(){
  if(!confirm('Reset all progress?'))return;
  checked={};save();renderAll();
}

function toggleTask(tid){
  checked[tid]=!checked[tid];save();updateHeader();
  const box=document.getElementById('box-'+tid),txt=document.getElementById('txt-'+tid);
  const pc=document.getElementById('pc-'+tid.split('_')[0]);
  const col=pc?pc.value:'#5C54D4';
  if(box){box.className='task-box'+(checked[tid]?' done':'');box.style.setProperty('--pc',col);box.innerHTML=checked[tid]?'<span>✓</span>':'';}
  if(txt){txt.className='task-text'+(checked[tid]?' done':'');}
  const dayId=tid.split('_').slice(0,-1).join('_');
  updateDayCircle(dayId);updatePhaseProgress(dayId);
}

function updateDayCircle(dayId){
  for(const p of PHASES){
    const d=p.days.find(d=>d.id===dayId);
    if(d){
      const done=dayDone(d),circ=document.getElementById('circ-'+dayId),cnt=document.getElementById('cnt-'+dayId);
      if(circ){
        if(done===d.tasks.length){circ.className='day-circle done';circ.style.setProperty('--pc',p.color);circ.innerHTML='<span>✓</span>';}
        else{circ.className='day-circle';circ.innerHTML='';}
      }
      if(cnt)cnt.textContent=`${done}/${d.tasks.length}`;
      break;
    }
  }
}

function updatePhaseProgress(dayId){
  for(const p of PHASES){
    if(p.days.find(d=>d.id===dayId)){
      const done=phaseDone(p),total=phaseTotal(p),pct=total?Math.round(done/total*100):0;
      const pe=document.getElementById('ppct-'+p.id),ce=document.getElementById('pcnt-'+p.id),be=document.getElementById('pbar-'+p.id);
      if(pe)pe.textContent=pct+'%';if(ce)ce.textContent=`${done}/${total}`;if(be)be.style.width=pct+'%';
      break;
    }
  }
}

function togglePhase(id){openPhase=openPhase===id?null:id;renderTracker();}
function toggleDay(id){openDay=openDay===id?null:id;renderTracker();}

function rgba(hex,a){const r=parseInt(hex.slice(1,3),16),g=parseInt(hex.slice(3,5),16),b=parseInt(hex.slice(5,7),16);return`rgba(${r},${g},${b},${a})`;}

function renderTracker(){
  let html='';
  for(const phase of PHASES){
    const isOpen=openPhase===phase.id,isVac=phase.type==='vacation';
    const done=phaseDone(phase),total=phaseTotal(phase),pct=total?Math.round(done/total*100):0;
    const bg=isVac?'#FFFBEB':rgba(phase.color,0.07),bc=rgba(phase.color,0.2);
    html+=`<input type="hidden" id="pc-${phase.id}" value="${phase.color}">
    <div class="phase">
      <div class="phase-header${isOpen?' open':''}" style="background:${bg};border-color:${bc};border-left-color:${phase.color};opacity:${isVac?0.8:1}" onclick="togglePhase('${phase.id}')">
        <div class="phase-row">
          <div style="flex:1">
            <div class="phase-dates" style="color:${phase.color}">${phase.dates}</div>
            <div class="phase-label">${phase.label}</div>
            <div class="phase-note">${phase.note}</div>
          </div>
          <div class="phase-meta">
            ${!isVac?`<div style="text-align:right"><div class="phase-pct" id="ppct-${phase.id}" style="color:${phase.color}">${pct}%</div><div class="phase-count" id="pcnt-${phase.id}">${done}/${total}</div></div>`:''}
            <div style="color:${phase.color};font-size:13px">${isOpen?'▲':'▼'}</div>
          </div>
        </div>
        ${!isVac&&total>0?`<div class="phase-progress" style="background:${rgba(phase.color,0.2)}"><div class="phase-progress-fill" id="pbar-${phase.id}" style="background:${phase.color};width:${pct}%"></div></div>`:''}
      </div>`;
    if(isOpen){
      html+=`<div class="days" style="border-color:${rgba(phase.color,0.15)}">`;
      for(const day of phase.days){
        const dd=dayDone(day),dt=day.tasks.length,isDayOpen=openDay===day.id,allDone=dd===dt;
        html+=`<div class="day">
          <div class="day-header" style="background:${allDone?rgba(phase.color,0.05):'white'}" onclick="toggleDay('${day.id}')">
            <div class="day-info">
              <div class="day-circle${allDone?' done':''}" id="circ-${day.id}" style="--pc:${phase.color};${allDone?`background:${phase.color};border-color:${phase.color}`:''}">
                ${allDone?'<span>✓</span>':''}
              </div>
              <span class="day-label">${day.label}</span>
            </div>
            <div class="day-meta">
              <span class="day-count" id="cnt-${day.id}" style="color:${phase.color}">${dd}/${dt}</span>
              <span style="color:#94A3B8;font-size:12px">${isDayOpen?'▲':'▼'}</span>
            </div>
          </div>`;
        if(isDayOpen){
          html+=`<div class="tasks">`;
          day.tasks.forEach((task,i)=>{
            const tid=`${day.id}_${i}`,done=!!checked[tid];
            html+=`<div class="task" onclick="toggleTask('${tid}')">
              <div class="task-box${done?' done':''}" id="box-${tid}" style="--pc:${phase.color};${done?`background:${phase.color};border-color:${phase.color}`:''}">
                ${done?'<span>✓</span>':''}
              </div>
              <span class="task-text${done?' done':''}" id="txt-${tid}">${task}</span>
            </div>`;
          });
          html+=`</div>`;
        }
        html+=`</div>`;
      }
      html+=`</div>`;
    }
    html+=`</div>`;
  }
  document.getElementById('view-tracker').innerHTML=html;
}

function renderOrder(){
  let html=`<div class="card"><div class="card-title">📐 Every study day — always in this order</div>`;
  DAILY_ORDER.forEach(s=>{
    html+=`<div class="order-item"><div class="order-num">${s.n}</div><div><div class="order-title">${s.t}</div><div class="order-note">${s.note}</div></div></div>`;
  });
  html+=`</div><div class="card"><div class="card-title">🃏 AnKing card limits</div>`;
  [["Normal content day","40–80"],["Heavy content day","Max 100"],["Review / catch-up day","0–30"],["Day before vacation","0–20"],["Vacation day","0 — reviews only"],["Reviews exceed 2 hrs","STOP new cards. Clear backlog first."]].forEach(([r,c])=>{
    html+=`<div class="limit-row"><span class="limit-rule">${r}</span><span class="limit-cards">${c}</span></div>`;
  });
  html+=`</div><div class="card"><div class="card-title">📚 Resource roles</div>`;
  [{r:"Bootcamp",c:"#5C54D4",d:"Main teaching spine. Watch at 1.25–1.5×. Pause before answers. Used for physiology, pathophysiology, immunology, pharm foundations."},{r:"Sketchy",c:"#B91C1C",d:"Micro + Pharm ONLY. Watch every video TWICE — story first, then active recall. Close and write everything you remember after."},{r:"First Aid",c:"#047857",d:"Annotation hub. Read matching pages AFTER Bootcamp/Sketchy. Annotate gaps. 20–30 min max."},{r:"AnKing",c:"#0369A1",d:"Reviews always first. Unsuspend only cards from today's studied topic. Never unsuspend entire decks."},{r:"Qbank",c:"#334155",d:"10–20/day early phases → 30–40 later. Every wrong answer → weakness log immediately."}].forEach(({r,c,d})=>{
    html+=`<div class="resource-item" style="border-left:3px solid ${c}"><div class="resource-name" style="color:${c}">${r}</div><div class="resource-desc">${d}</div></div>`;
  });
  html+=`</div>`;
  document.getElementById('view-order').innerHTML=html;
}

function renderOverview(){
  let html='';
  OVERVIEW.forEach(({c,l,d,desc})=>{
    html+=`<div class="overview-item" style="border-left-color:${c}"><div class="overview-label" style="color:${c}">${l}</div><div class="overview-dates">${d}</div><div class="overview-desc">${desc}</div></div>`;
  });
  html+=`<div class="principle-box"><strong style="color:#5C54D4">Guiding principle: </strong>Physiology first → pathophysiology second → pharmacology layered in. Sketchy for Micro and Pharm only. Bootcamp is the teaching spine. First Aid annotates. AnKing retains. Questions prove understanding.</div>`;
  document.getElementById('view-overview').innerHTML=html;
}

function renderAll(){updateHeader();renderTracker();renderOrder();renderOverview();}
load();renderAll();
</script>
</body>
</html>
