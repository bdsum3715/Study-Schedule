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

  /* Header */
  .header{background:linear-gradient(135deg,#5C54D4,#0369A1);color:white;padding:20px 16px 18px;margin-bottom:12px;}
  .header-top{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:14px;}
  .header-label{font-size:10px;font-weight:700;letter-spacing:2px;opacity:0.7;text-transform:uppercase;margin-bottom:3px;}
  .header h1{font-size:20px;font-weight:800;margin-bottom:3px;}
  .header p{font-size:12px;opacity:0.85;}
  .streak-badge{background:rgba(255,255,255,0.18);border-radius:14px;padding:8px 12px;text-align:center;min-width:56px;}
  .streak-flame{font-size:16px;line-height:1;}
  .streak-num{font-size:15px;font-weight:800;line-height:1.3;}
  .streak-label{font-size:8px;opacity:0.75;text-transform:uppercase;letter-spacing:0.5px;}
  .progress-bar{background:rgba(255,255,255,0.25);border-radius:20px;height:9px;margin-bottom:6px;}
  .progress-fill{background:white;border-radius:20px;height:9px;transition:width 0.3s;}
  .progress-label{font-size:11px;opacity:0.8;}

  /* Today banner */
  .today-banner{margin:0 14px 14px;background:white;border-radius:16px;padding:16px;box-shadow:0 2px 10px rgba(15,23,42,0.08);border:1.5px solid #E0E7FF;cursor:pointer;position:relative;overflow:hidden;}
  .today-banner::before{content:'';position:absolute;top:0;left:0;bottom:0;width:4px;background:linear-gradient(180deg,#5C54D4,#0369A1);}
  .today-banner-label{font-size:10px;font-weight:700;color:#5C54D4;text-transform:uppercase;letter-spacing:1px;margin-bottom:4px;}
  .today-banner-title{font-size:15px;font-weight:800;color:#0F172A;margin-bottom:6px;}
  .today-banner-sub{font-size:12px;color:#64748B;display:flex;align-items:center;gap:6px;}
  .today-banner-arrow{margin-left:auto;color:#5C54D4;font-size:16px;}
  .today-banner-progress{display:flex;gap:3px;margin-top:10px;}
  .today-banner-dot{flex:1;height:5px;border-radius:3px;background:#E2E8F0;}
  .today-banner-dot.done{background:#5C54D4;}
  .today-banner-empty{color:#94A3B8;font-size:13px;text-align:center;padding:8px 0;}
  .today-banner-vacation{background:#FFFBEB;border-color:#FDE68A;}
  .today-banner-vacation .today-banner-label{color:#B45309;}
  .today-banner-vacation::before{background:#B45309;}

  /* Nav */
  .nav{display:flex;gap:8px;padding:0 14px;margin-bottom:14px;flex-wrap:wrap;}
  .nav button{padding:9px 16px;border-radius:10px;border:none;cursor:pointer;font-weight:600;font-size:12px;transition:all 0.15s;}
  .nav button.active{background:#5C54D4;color:white;box-shadow:0 3px 10px rgba(92,84,212,0.3);}
  .nav button.inactive{background:white;color:#64748B;box-shadow:0 1px 3px rgba(0,0,0,0.08);}
  .nav button.reset{padding:9px 12px;border:1.5px solid #E2E8F0;background:white;color:#94A3B8;}
  .nav button.rebalance{padding:9px 12px;border:1.5px solid #5C54D4;background:white;color:#5C54D4;font-weight:700;}
  .nav-spacer{margin-left:auto;}

  .content{padding:0 14px;}

  /* Phase card */
  .phase{margin-bottom:9px;border-radius:12px;overflow:hidden;}
  .phase-header{padding:12px 14px;cursor:pointer;border-left:4px solid;border:1.5px solid;border-radius:12px;user-select:none;}
  .phase-header.open{border-radius:12px 12px 0 0;}
  .phase-header.is-today-phase{box-shadow:0 0 0 2px rgba(92,84,212,0.25);}
  .phase-dates{font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:0.8px;margin-bottom:2px;}
  .phase-label{font-weight:700;color:#0F172A;font-size:14px;margin-bottom:2px;}
  .phase-note{font-size:11px;color:#64748B;}
  .phase-meta{display:flex;align-items:center;gap:10px;margin-left:10px;flex-shrink:0;}
  .phase-pct{font-weight:800;font-size:15px;}
  .phase-count{font-size:10px;color:#94A3B8;}
  .phase-row{display:flex;justify-content:space-between;align-items:flex-start;}
  .phase-progress{margin-top:8px;border-radius:10px;height:4px;}
  .phase-progress-fill{border-radius:10px;height:4px;transition:width 0.3s;}
  .rebalanced-tag{display:inline-block;font-size:9px;font-weight:700;background:#EEF2FF;color:#5C54D4;padding:2px 7px;border-radius:6px;margin-left:6px;vertical-align:middle;}

  .days{background:white;border:1.5px solid;border-top:none;border-radius:0 0 12px 12px;overflow:hidden;}
  .day{border-bottom:1px solid #F1F5F9;}
  .day:last-child{border-bottom:none;}
  .day.is-today{background:linear-gradient(90deg,rgba(92,84,212,0.06),transparent);}
  .day-header{padding:10px 15px;cursor:pointer;display:flex;justify-content:space-between;align-items:center;user-select:none;}
  .day-label{font-weight:600;color:#0F172A;font-size:12.5px;}
  .today-pill{display:inline-block;background:#5C54D4;color:white;font-size:9px;font-weight:700;padding:2px 7px;border-radius:6px;margin-left:6px;letter-spacing:0.3px;}
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

  /* Weakness log */
  .weakness-btn{width:100%;text-align:left;padding:9px 12px;background:#FFF5F5;border:1px dashed #FCA5A5;border-radius:9px;color:#B91C1C;font-size:11.5px;font-weight:600;cursor:pointer;margin-top:6px;}
  .weakness-entries{margin-top:6px;}
  .weakness-entry{background:#FFF5F5;border-radius:9px;padding:9px 11px;margin-bottom:6px;font-size:12px;color:#7F1D1D;position:relative;}
  .weakness-entry-del{position:absolute;top:6px;right:8px;color:#B91C1C;font-size:11px;cursor:pointer;font-weight:700;opacity:0.6;}
  .weakness-textarea{width:100%;border:1.5px solid #FCA5A5;border-radius:9px;padding:9px 11px;font-size:12.5px;font-family:inherit;resize:vertical;min-height:50px;color:#334155;}
  .weakness-save{background:#B91C1C;color:white;border:none;padding:7px 14px;border-radius:8px;font-size:11.5px;font-weight:700;cursor:pointer;margin-top:6px;}

  /* Cards / lists */
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
  .overview-label{font-weight:700;font-size:13px;display:flex;align-items:center;gap:6px;}
  .overview-dates{font-size:11px;color:#94A3B8;margin-bottom:4px;}
  .overview-desc{color:#475569;font-size:13px;}
  .principle-box{background:#EEF2FF;border-radius:14px;padding:14px 16px;margin-top:6px;font-size:13px;color:#334155;line-height:1.7;border:1px solid #C7D2FE;}

  /* Modal */
  .modal-overlay{position:fixed;inset:0;background:rgba(15,23,42,0.6);z-index:100;display:flex;align-items:flex-end;justify-content:center;padding-bottom:env(safe-area-inset-bottom,0px);}
  .modal{background:white;border-radius:24px 24px 0 0;width:100%;max-width:540px;padding:24px 20px 36px;max-height:88vh;overflow-y:auto;}
  .modal-handle{width:40px;height:4px;background:#E2E8F0;border-radius:4px;margin:0 auto 20px;}
  .modal-title{font-size:18px;font-weight:800;color:#0F172A;margin-bottom:4px;}
  .modal-sub{font-size:13px;color:#64748B;margin-bottom:20px;}
  .modal-section{margin-bottom:18px;}
  .modal-section-title{font-size:11px;font-weight:700;color:#94A3B8;text-transform:uppercase;letter-spacing:1px;margin-bottom:10px;}
  .rebalance-stat{display:flex;justify-content:space-between;align-items:center;padding:12px 14px;background:#F8FAFC;border-radius:12px;margin-bottom:8px;}
  .rebalance-stat-label{font-size:13px;color:#475569;}
  .rebalance-stat-val{font-size:15px;font-weight:800;color:#5C54D4;}
  .rebalance-day{display:flex;gap:12px;padding:14px;background:#F0F4FF;border-radius:12px;margin-bottom:8px;border-left:4px solid #5C54D4;}
  .rebalance-day-date{font-size:12px;font-weight:700;color:#5C54D4;min-width:90px;}
  .rebalance-day-tasks{font-size:12.5px;color:#334155;line-height:1.6;}
  .rebalance-warn{background:#FFF9F0;border:1px solid #FDE68A;border-radius:12px;padding:12px 14px;font-size:12.5px;color:#92400E;margin-bottom:16px;}
  .rebalance-ok{background:#F0FFF8;border:1px solid #6EE7B7;border-radius:12px;padding:12px 14px;font-size:12.5px;color:#065F46;margin-bottom:16px;}
  .modal-btn{width:100%;padding:14px;border-radius:14px;border:none;font-size:15px;font-weight:700;cursor:pointer;margin-bottom:10px;}
  .modal-btn-primary{background:#5C54D4;color:white;}
  .modal-btn-secondary{background:#F1F5F9;color:#475569;}
  .modal-btn-danger{background:#FEE2E2;color:#B91C1C;}

  .toast{position:fixed;bottom:30px;left:50%;transform:translateX(-50%);background:#0F172A;color:white;padding:12px 22px;border-radius:14px;font-size:13px;font-weight:600;z-index:200;box-shadow:0 4px 20px rgba(0,0,0,0.35);max-width:90vw;text-align:center;}

  /* Calendar */
  .cal-month{background:white;border-radius:14px;padding:16px;margin-bottom:14px;box-shadow:0 1px 4px rgba(0,0,0,0.06);}
  .cal-month-title{font-size:15px;font-weight:800;color:#0F172A;margin-bottom:12px;text-align:center;}
  .cal-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:4px;}
  .cal-dow{font-size:9px;font-weight:700;color:#94A3B8;text-align:center;padding:4px 0;text-transform:uppercase;}
  .cal-cell{aspect-ratio:1;border-radius:8px;display:flex;flex-direction:column;align-items:center;justify-content:center;font-size:11px;position:relative;cursor:pointer;padding:2px;}
  .cal-cell.empty{visibility:hidden;}
  .cal-cell-num{font-weight:700;font-size:11px;}
  .cal-cell-dot{width:5px;height:5px;border-radius:50%;margin-top:2px;}
  .cal-cell.today{box-shadow:0 0 0 2px #5C54D4;}
  .cal-cell-mins{font-size:7.5px;margin-top:1px;opacity:0.85;}
  .cal-legend{display:flex;flex-wrap:wrap;gap:8px;margin-top:14px;padding-top:12px;border-top:1px solid #F1F5F9;}
  .cal-legend-item{display:flex;align-items:center;gap:5px;font-size:10.5px;color:#475569;}
  .cal-legend-dot{width:9px;height:9px;border-radius:3px;flex-shrink:0;}
  .cal-day-popup{background:white;border-radius:14px;padding:16px;margin-bottom:14px;box-shadow:0 2px 10px rgba(0,0,0,0.1);border-left:4px solid #5C54D4;}
  .cal-day-popup-date{font-size:11px;font-weight:700;color:#5C54D4;text-transform:uppercase;letter-spacing:0.5px;margin-bottom:4px;}
  .cal-day-popup-title{font-size:15px;font-weight:800;color:#0F172A;margin-bottom:6px;}
  .cal-day-popup-time{display:inline-block;background:#EEF2FF;color:#5C54D4;font-size:11px;font-weight:700;padding:3px 10px;border-radius:8px;margin-bottom:8px;}
  .cal-week-summary{display:flex;justify-content:space-between;padding:10px 14px;background:#F8FAFC;border-radius:10px;margin-bottom:8px;font-size:11.5px;color:#475569;}
</style>
</head>

<body>
<div class="safe-top">
<div class="header">
  <div class="header-top">
    <div>
      <div class="header-label">Step 1 + Year 3 Foundation</div>
      <h1>Ultimate Summer Study Plan</h1>
      <p>Jul 4 – Sep 27 · Year 3 starts Sep 28</p>
    </div>
    <div class="streak-badge" id="streak-badge">
      <div class="streak-flame">🔥</div>
      <div class="streak-num" id="streak-num">0</div>
      <div class="streak-label">day streak</div>
    </div>
  </div>
  <div class="progress-bar"><div class="progress-fill" id="main-bar" style="width:0%"></div></div>
  <div class="progress-label" id="main-label">0 of 0 tasks · 0% complete</div>
</div>

<div class="today-banner" id="today-banner" onclick="jumpToToday()">
  <!-- populated by renderTodayBanner() -->
</div>

<div class="nav">
  <button class="active" id="btn-tracker" onclick="showView('tracker')">📋 Tracker</button>
  <button class="inactive" id="btn-calendar" onclick="showView('calendar')">🗓️ Calendar</button>
  <button class="inactive" id="btn-order" onclick="showView('order')">📐 Daily Order</button>
  <button class="inactive" id="btn-overview" onclick="showView('overview')">📅 Overview</button>
  <button class="rebalance inactive" onclick="openRebalance()">⚖️ Rebalance</button>
  <button class="reset inactive nav-spacer" onclick="resetAll()">Reset</button>
</div>

<div class="content">
  <div id="view-tracker"></div>
  <div id="view-calendar" style="display:none"></div>
  <div id="view-order" style="display:none"></div>
  <div id="view-overview" style="display:none"></div>
</div>

<!-- Rebalance Modal -->
<div class="modal-overlay" id="modal-rebalance" style="display:none" onclick="closeModalOutside(event,'modal-rebalance')">
  <div class="modal">
    <div class="modal-handle"></div>
    <div class="modal-title">⚖️ Rebalance Plan</div>
    <div class="modal-sub" id="modal-date"></div>
    <div id="modal-body"></div>
    <button class="modal-btn modal-btn-secondary" onclick="closeModal('modal-rebalance')">Close</button>
  </div>
</div>

<!-- Weakness Log Modal -->
<div class="modal-overlay" id="modal-weakness" style="display:none" onclick="closeModalOutside(event,'modal-weakness')">
  <div class="modal">
    <div class="modal-handle"></div>
    <div class="modal-title">📝 Weakness Log</div>
    <div class="modal-sub" id="weakness-modal-sub"></div>
    <div id="weakness-modal-body"></div>
    <button class="modal-btn modal-btn-secondary" onclick="closeModal('modal-weakness')">Close</button>
  </div>
</div>

<!-- Undo Schedule Confirm Modal -->
<div class="modal-overlay" id="modal-undo" style="display:none" onclick="closeModalOutside(event,'modal-undo')">
  <div class="modal">
    <div class="modal-handle"></div>
    <div class="modal-title">↩️ Reset Schedule?</div>
    <div class="modal-sub">This restores all phase and day dates to the original plan. Your checked-off progress is NOT affected — only dates reset.</div>
    <button class="modal-btn modal-btn-danger" onclick="confirmUndoSchedule()">Reset Dates to Original</button>
    <button class="modal-btn modal-btn-secondary" onclick="closeModal('modal-undo')">Cancel</button>
  </div>
</div>

</div>

<script>
const PHASES = [
  {id:"p1",color:"#5C54D4",priority:true,type:"study",label:"Phase 1 — General Pathology, Immunology + Pharm Foundations",dates:"Jul 4 – Jul 13",note:"⭐ Year 3 Priority · Foundational pathology + immunology + pharm basics",days:[
    {id:"d1start",mins:135,label:"Jul 4 Sat — Setup + Cell injury + Inflammation",tasks:[
      "1. AnKing: set up tag system — Pathology · Immunology · Micro · Pharm · Cardio · Pulm · Renal (10 min, once)",
      "2. AnKing: due reviews (60 min)",
      "3. First Aid Pathology: cellular adaptations · reversible/irreversible injury · necrosis vs apoptosis · free radicals · ischemia-reperfusion (this is your primary source — no dedicated Bootcamp Pathology subject exists)",
      "4. Bootcamp Immunology: Ch.3 Inflammatory Response",
      "5. First Aid Pathology: acute/chronic inflammation · granulomas · chemical mediators · wound healing (25 min checklist)",
      "6. AnKing: new cards — Pathology + Inflammation tags (40–60 new)",
      "7. Qbank: 15 questions — pathology only",
      "8. Weakness log: every wrong answer → topic + why + correct rule",
    ]},
    {id:"d1a",mins:120,label:"Jul 5 Sun — Innate immunity",tasks:[
      "1. AnKing: due reviews (60 min)",
      "2. Bootcamp Immunology: Ch.1 Lymphoid Tissue + Ch.2 Innate Immunity",
      "3. First Aid Immunology: innate immunity pages (20 min checklist)",
      "4. AnKing: new cards — Immunology tag",
      "5. Qbank: 10–20 path/immuno questions + weakness log",
    ]},
    {id:"d1b",mins:120,label:"Jul 6 Mon — Hemodynamics + vascular physiology",tasks:[
      "1. AnKing: due reviews (60 min)",
      "2. Bootcamp Cardiology: Ch.3 Vascular System and Cardiac Parameters + Ch.4 (same chapter group)",
      "3. First Aid Pathology: edema · hyperemia/congestion · hemorrhage (20 min checklist)",
      "4. AnKing: new cards",
      "5. Qbank: 10–20 questions + weakness log",
    ]},
    {id:"d1c",mins:120,label:"Jul 7 Tue — Thrombosis, embolism, infarction",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Cardiology: Ch.7 Vasodilation and Vasoconstriction + Ch.8 Pressure Flow Physiology",
      "3. First Aid Pathology: thrombosis · embolism · infarction mechanisms (20 min checklist)",
      "4. AnKing: new cards",
      "5. Qbank: 10–20 questions + weakness log",
    ]},
    {id:"d1d",mins:120,label:"Jul 8 Wed — Shock",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Cardiology: Ch.27 Pericardial Disease + Ch.28 Shock",
      "3. First Aid Pathology: shock — all types + hemodynamic parameters (20 min checklist)",
      "4. Make comparison table: septic vs cardiogenic vs hypovolemic vs obstructive (CO · SVR · PCWP)",
      "5. AnKing: new cards",
      "6. Qbank: 15–20 questions + weakness log",
    ]},
    {id:"d1e",mins:170,label:"Jul 9 Thu — Neoplasia + hemostasis + Pathology consolidation",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Hematology/Oncology: Ch.8 Oncology and Therapeutics (conceptual portions only)",
      "3. Bootcamp Hematology/Oncology: Ch.6 Platelets + Ch.7 Coagulation and Fibrinolysis",
      "4. First Aid Pathology: benign vs malignant · dysplasia · carcinoma in situ · invasion · metastasis · grading/staging (20 min checklist)",
      "5. First Aid Pathology: oncogenes · tumor suppressors · cancer hallmarks · paraneoplastic syndromes (20 min checklist)",
      "6. Know cold: p53 · RB · APC · BCL2 — mechanism + associated cancer",
      "7. AnKing: new cards",
      "8. Qbank: 20–30 questions + weakness log",
      "9. ⭐ Consolidation: build mechanism map from memory — cell injury → inflammation → repair · thrombosis → ischemia → infarction · mutation → neoplasia",
      "10. ⭐ Weakness log: review all General Pathology entries so far — can you answer each without looking?",
    ]},
    {id:"d1h",mins:170,label:"Jul 10 Fri — Immunology 1+2: adaptive immunity, T cells, B cells, antibodies, complement",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Immunology: Ch.4 Cytokines + Ch.5 T cells",
      "3. Bootcamp Immunology: Ch.6 B cells + Ch.7 Antibodies + Ch.8 Complement",
      "4. First Aid Immunology: T cell section (20 min checklist)",
      "5. First Aid Immunology: complement deficiency table (20 min checklist)",
      "6. Make table: C1/C2/C4 vs C3 vs C5-C9 defects + infection risks",
      "7. Know cold: C3 deficiency = pyogenic · C5-C9 deficiency = Neisseria ONLY",
      "8. AnKing: new cards — Immunology tag",
      "9. Qbank: 20–30 questions + weakness log",
    ]},
    {id:"d1i",mins:120,label:"Jul 11 Sat — Immunology 3: vaccines + immunodeficiency",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Immunology: Ch.9 Vaccinations + Ch.10 Immunodeficiency Syndromes",
      "3. First Aid Immunology: immunodeficiency tables (20 min checklist)",
      "4. Tie every defect: inheritance + mechanism + infection risk + lab finding",
      "5. AnKing: new cards",
      "6. Qbank: 10–20 questions + weakness log",
    ]},
    {id:"d1j",mins:120,label:"Jul 12 Sun — Immunology 3: vaccines + immunodeficiency",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Immunology: Ch.9 Vaccinations + Ch.10 Immunodeficiency Syndromes",
      "3. First Aid Immunology: immunodeficiency tables (20 min checklist)",
      "4. Tie every defect: inheritance + mechanism + infection risk + lab finding",
      "5. AnKing: new cards",
      "6. Qbank: 10–20 questions + weakness log",
    ]},
    {id:"d1k",mins:120,label:"Jul 13 Mon — Immunology 4: hypersensitivity + transplant",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Immunology: Ch.11 Hypersensitivity Syndromes + Ch.12 Transfusion Reactions + Ch.13 Transplant Rejection",
      "3. First Aid Immunology: hypersensitivity + transplant sections (20 min checklist)",
      "4. Make Type I–IV table: type → mediator → example → treatment",
      "5. Make transplant rejection timeline: hyperacute / acute / chronic — timing + mechanism",
      "6. AnKing: new cards",
      "7. Qbank: 10–20 questions + weakness log",
    ]},
  ]},
  {id:"vactravel",color:"#0891B2",type:"vacation",label:"✈️ Travel",dates:"Jul 14–26",note:"AnKing reviews only, if you have a spare moment · No new cards · No Bootcamp · No Sketchy · No Qbank — enjoy the trip",days:[
    {id:"vactravela",label:"Jul 14–26 — Travel (13 days)",tasks:[
      "AnKing: due reviews only, if you get a spare moment — no pressure",
      "No new cards. No Bootcamp. No Sketchy. No Qbank.",
      "This is a real break — the plan picks back up automatically when you return on Jul 27",
    ]},
  ]},
  {id:"p1cont",color:"#5C54D4",priority:true,type:"study",label:"Phase 1 (continued) — Pharmacology Foundations",dates:"Jul 27–28",note:"⭐ Year 3 Priority · Finishing Pharm foundations before Microbiology begins",days:[
    {id:"d1l",mins:195,label:"Jul 27 Mon — Pharm Foundations 1+2: Pharmacodynamics + Pharmacokinetics",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Pharmacology: Ch.1 Pharmacodynamics",
      "3. Bootcamp Pharmacology: Ch.2 Pharmacokinetics + Ch.4 Side Effects and Toxins",
      "4. Sketchy Pharmacology: Pharmacology Foundations group — open the Pharmacology Foundations module and watch all videos in order (watch TWICE — story then active recall) · 23 videos, 4 hrs at 1.25x",
      "5. First Aid Pharmacology: PD + PK sections (30 min checklist)",
      "6. Know cold: potency vs efficacy · EC50 · ED50 · therapeutic index · agonist/antagonist/partial agonist curves",
      "7. Know: Vd = dose/plasma conc · CL = Vd × ke · t½ = 0.7/ke · loading dose · maintenance dose · CYP basics",
      "8. AnKing: new cards — Pharmacology tag",
      "9. Qbank: 20–30 pharm questions + weakness log",
    ]},
    {id:"d1n",mins:180,label:"Jul 28 Tue — Autonomics + Phase 1 consolidation",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Pharmacology: Ch.3 Autonomic System",
      "3. Sketchy Pharmacology: Autonomic Drugs group — open the Autonomic Drugs module and watch all videos in order (watch TWICE — story then active recall) · 21 videos, 6 hrs at 1.25x",
      "4. First Aid Pharmacology: autonomics section (20 min checklist)",
      "5. Make receptor table: alpha-1/2 · beta-1/2 · M1-M3 · nicotinic — receptor + location + effect",
      "6. Quiz: cover 'effect' column and reproduce from memory",
      "7. Qbank: 30–40 mixed path/immuno/pharm questions",
      "9. ⭐ Saturday rule: go through all weakness log entries from this week",
    ]},
  ]},
  {id:"p2",color:"#B91C1C",priority:true,type:"study",label:"Phase 2 — Medical Microbiology + Antimicrobial Pharmacology",dates:"Jul 27 – Aug 9",note:"⭐ Sketchy-first for every organism · Watch TWICE · Bootcamp confirms · STOP large cards Aug 9",days:[
    {id:"d2a",mins:210,label:"Jul 29 Wed — Micro framework: fundamentals + bacterial genetics + toxins",tasks:[
      "1. AnKing: due reviews (60–75 min)",
      "2. Bootcamp Microbiology: Ch.1 Fundamentals of Bacteriology",
      "3. Bootcamp Microbiology: Ch.2 Bacterial Genetics",
      "4. Bootcamp Microbiology: Ch.3 Bacterial Toxins",
      "5. Sketchy Micro: Bacteria group — open the Bacteria module · watch the intro/framework videos in order (watch TWICE each — story then active recall) · full module: 53 videos, 4 hrs at 1.25x, spread across this week",
      "6. First Aid Microbiology: bacteria intro tables — virulence factors · toxins (20 min checklist)",
      "7. Know: transformation · transduction · conjugation · exotoxin vs endotoxin mechanisms",
      "8. AnKing: new cards — Micro tag",
      "9. Draw gram stain decision tree from memory at end of day",
      "10. Qbank: 15–20 questions + weakness log",
    ]},
    {id:"d2b",mins:195,label:"Jul 30 Thu — Gram-positive cocci: Staph + Strep",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.4 Staphylococcus",
      "3. Bootcamp Microbiology: Ch.5 Streptococcus",
      "4. Sketchy Micro: Bacteria group — watch Staph aureus · Staph epidermidis · Strep pyogenes · Strep pneumoniae · Strep agalactiae · Strep viridans videos in order (watch TWICE each)",
      "5. First Aid Microbiology: Staph + Strep tables (20 min checklist)",
      "6. Pharm tie-in: beta-lactams (mechanism + resistance) · vancomycin (Red Man syndrome + nephrotoxicity)",
      "7. AnKing: new cards",
      "8. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2c",mins:210,label:"Jul 31 Fri — Enterococcus, Bacillus, Clostridium, Mycobacteria",tasks:[
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
    {id:"d2d",mins:210,label:"Aug 1 Sat — Non-spore G+ rods + spirochetes + atypical bacteria",tasks:[
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
    {id:"d2e",mins:195,label:"Aug 2 Sun — Gram-negative rods I: lactose + non-lactose fermenting",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.10 Lactose Fermenting Gram Negative Bacilli",
      "3. Bootcamp Microbiology: Ch.11 Non-lactose Fermenting Gram Negative Bacilli",
      "4. Sketchy Micro: Bacteria group — watch E. coli · Klebsiella · Enterobacter · Serratia · Proteus · Salmonella · Shigella · Pseudomonas · Burkholderia videos in order (watch TWICE each)",
      "5. First Aid Microbiology: gram-negative rod tables (20 min checklist)",
      "6. Pharm tie-in: aminoglycosides (30S · nephro/ototoxicity) · fluoroquinolones (DNA gyrase) · cephalosporins by generation",
      "7. AnKing: new cards",
      "8. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2f",mins:210,label:"Aug 3 Mon — Gram-negative curved bacilli + diplococci + coccobacilli + Bacteria consolidation",tasks:[
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
      "11. ⭐ Consolidation: focus toxin → mechanism · organism → immune defect association · organism → syndrome → drug class",
      "12. ⭐ Build missed-organism list from Ch.1–14 for targeted re-review",
    ]},
    {id:"d2h",mins:210,label:"Aug 4 Tue — Virology basics + positive-sense + negative-sense RNA viruses",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.26+27 Approach/Basics of Virology",
      "3. Bootcamp Microbiology: Ch.28 Positive Sense RNA Viruses",
      "4. Bootcamp Microbiology: Ch.29 Negative Sense RNA Viruses",
      "5. Sketchy Micro: Viruses – RNA Viruses group — open the RNA Viruses module and watch all videos in order (watch TWICE each) · 21 videos, 2.5 hrs at 1.25x",
      "6. First Aid Microbiology: viral genome chart (20 min checklist)",
      "7. Know: +sense RNA = directly translated · −sense RNA = needs RNA-dependent RNA polymerase first",
      "8. AnKing: new cards — Virology tag",
      "9. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2i",mins:165,label:"Aug 5 Wed — Double-stranded RNA viruses + DNA viruses",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.30+31 Double Stranded RNA Viruses / DNA Viruses",
      "4. Sketchy Micro: Viruses – DNA Viruses group — open the DNA Viruses module and watch all videos in order (watch TWICE each) · 13 videos, 1.5 hrs at 1.25x",
      "5. First Aid Microbiology: DNA virus tables (20 min checklist)",
      "6. Pharm tie-in: acyclovir (HSV/VZV · TK activation) · ganciclovir (CMV) · foscarnet (CMV resistance) · oseltamivir (influenza NA inhibitor)",
      "7. AnKing: new cards",
      "8. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2j",mins:210,label:"Aug 6 Thu — Mycology: dimorphic + opportunistic + tinea",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.17 Dimorphic Mycosis",
      "3. Bootcamp Microbiology: Ch.18 Opportunistic Mycosis",
      "4. Bootcamp Microbiology: Ch.19 Tinea",
      "5. Sketchy Micro: Fungi group — open the Fungi module and watch all videos in order (watch TWICE each) · Fungi + Parasites combined: 29 videos, 3.5 hrs at 1.25x total",
      "6. First Aid Microbiology: fungi section (20 min checklist)",
      "7. Dimorphic rule: mold in cold · yeast in heat (except Coccidioides = spherules in tissue)",
      "8. Pharm tie-in: amphotericin B (ergosterol membrane) · azoles (ergosterol synthesis) · echinocandins (beta-glucan) · flucytosine · terbinafine",
      "9. AnKing: new cards — Fungi tag",
      "10. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2k",mins:240,label:"Aug 7 Fri — Parasitology: protozoa, nematodes, cestodes, trematodes, ectoparasites",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.20 Gastrointestinal Protozoa",
      "3. Bootcamp Microbiology: Ch.21 Systemic Protozoa",
      "4. Bootcamp Microbiology: Ch.22 Nematodes",
      "5. Bootcamp Microbiology: Ch.23 Cestodes",
      "6. Bootcamp Microbiology: Ch.24 Trematodes + Ch.25 Ectoparasites",
      "7. Sketchy Micro: Parasites group — open the Parasites module and watch all videos in order (watch TWICE each) · part of the 29-video, 3.5 hr Fungi + Parasites block",
      "8. First Aid Microbiology: parasite tables (20 min checklist)",
      "9. Pharm tie-in: metronidazole · albendazole/mebendazole · praziquantel · ivermectin — mechanisms each",
      "10. AnKing: new cards — Parasites tag",
      "11. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2l",mins:165,label:"Aug 8 Sat — Antibiotics",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.36 Antibiotics",
      "3. Sketchy Pharmacology: Antimicrobials group — open the Antimicrobials module and watch all videos in order (watch TWICE each) · 28 videos, 4 hrs at 1.25x",
      "4. First Aid Pharmacology: antibiotic tables (20 min checklist)",
      "5. Know by category: cell wall (beta-lactams · vancomycin · bacitracin) · 30S (aminoglycosides · tetracyclines) · 50S (macrolides · linezolid · clindamycin · chloramphenicol) · DNA/RNA (fluoroquinolones · rifampin · metronidazole) · folate (sulfonamides · trimethoprim)",
      "6. For every class: mechanism + major toxicity + resistance mechanism",
      "7. AnKing: new cards — antibiotic tag",
      "8. Qbank: 20 questions + weakness log",
    ]},
    {id:"d2m",mins:225,label:"Aug 9 Sun — Antifungals + antiparasitics + antivirals + Micro/Pharm consolidation",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Microbiology: Ch.37 Antifungals",
      "3. Bootcamp Microbiology: Ch.38 Antiparasitics",
      "4. Bootcamp Microbiology: Ch.39 Antivirals",
      "5. Sketchy Pharmacology: Antimicrobials group — continue with antifungal · antiviral · antiparasitic videos in order (watch TWICE each)",
      "6. First Aid Pharmacology: antifungal · antiviral · antiparasitic sections (20 min checklist)",
      "7. For every class: mechanism + major toxicity + contraindication + resistance",
      "8. LIMIT new cards today — internship starts in 2 days",
      "9. Qbank: 30 mixed micro/pharm questions + weakness log",
      "10. ⭐ Saturday rule: go through all weakness log entries from this week",
      "11. ⭐ Consolidation: quiz yourself — cover treatment column → reproduce from organism name only, across all of Ch.1–39",
      "12. ⭐ Build final missed-organism list + drug-class toxicity list before internship starts",
    ]},
  ]},
  {id:"vac3",color:"#7C3AED",type:"vacation",label:"🏥 Orthopedic Surgery Internship 1",dates:"Aug 10–24",note:"AnKing reviews only for Micro/Pharm · Self-paced MSK anatomy + ortho pathology checklist below — no fixed daily quota, fit around internship hours",days:[
    {id:"vac3a",label:"Aug 10–24 — Internship + self-paced MSK review (15 days)",tasks:[
      "AnKing: due reviews only, every day — Micro + Antimicrobial Pharm decks",
      "No new Micro/Pharm cards. Goal: no backlog explosion for Phase 3.",
      "— MSK ANATOMY + PATHOLOGY CHECKLIST (work through whenever you have time) —",
      "☐ Bootcamp MSK/Rheum Ch.1 Skeletal Muscle — fiber types, contraction mechanism",
      "☐ Bootcamp MSK/Rheum Ch.7 Spine — vertebral levels, spinal cord relationships, disc herniation patterns",
      "☐ Bootcamp MSK/Rheum Ch.8 Brachial Plexus — roots/trunks/divisions/cords/branches, common injury patterns (Erb's, Klumpke's, wrist drop)",
      "☐ Bootcamp MSK/Rheum Ch.9 Shoulder and Elbow — rotator cuff, common fractures/dislocations, nerve at risk with each",
      "☐ Bootcamp MSK/Rheum Ch.10 Wrist and Hand — carpal bones, carpal tunnel, scaphoid fracture risk (AVN), tendon zones",
      "☐ Bootcamp MSK/Rheum Ch.11 Lower Extremity Nerves — sciatic, femoral, obturator, peroneal — motor/sensory + injury patterns (foot drop)",
      "☐ Bootcamp MSK/Rheum Ch.12 Hip & Knee — hip fracture types + blood supply/AVN risk, knee ligaments (ACL/PCL/MCL/LCL), meniscus",
      "☐ Bootcamp MSK/Rheum Ch.13 Foot & Ankle — ankle ligaments, common fracture patterns (Weber classification), compartments",
      "☐ Bootcamp MSK/Rheum Ch.5 Primary Bone Tumors — benign vs malignant, age groups, classic locations/imaging",
      "☐ Bootcamp MSK/Rheum Ch.14 Childhood MSK Pathology — SCFE, Legg-Calve-Perthes, developmental dysplasia of hip",
      "☐ Know cold: compartment syndrome — 6 P's, which compartments, fasciotomy urgency",
      "☐ Know cold: open fracture classification (Gustilo-Anderson) and why timing to OR matters",
      "☐ Know cold: nerve injury classification — neurapraxia vs axonotmesis vs neurotmesis",
      "☐ For every joint: review common surgical approach landmarks (what structures are at risk)",
      "Goal: walk into rounds/cases able to name the structure, the injury pattern, and the nerve/vessel at risk.",
    ]},
  ]},
  {id:"p3",color:"#047857",priority:true,type:"study",label:"Phase 3 — Physiology → Pathophysiology → Pharm: Cardio, Pulm, Renal",dates:"Aug 25 – Sep 5",note:"⭐ Physiology ALWAYS before pathology · Formula: normal → disease → compensation → drug · STOP cards Sep 5",days:[
    {id:"d3a",mins:165,label:"Aug 25 Tue — Cardio physiology 1: embryology, anatomy, vascular system, PV loops",tasks:[
      "1. AnKing: due reviews (60–75 min) — clear any vacation backlog first",
      "2. Bootcamp Cardiology: Ch.1 Embryology and Anatomy + Ch.2 (same chapter group)",
      "3. Bootcamp Cardiology: Ch.3 Vascular System and Cardiac Parameters + Ch.4 (same chapter group)",
      "4. Bootcamp Cardiology: Ch.5 + 6 Cardiac Function Curves, Pressure Volume Loops + Ch.6 (same chapter group)",
      "5. First Aid Cardiology: cardiac physiology section (20 min checklist)",
      "6. Know: preload · afterload · contractility · Frank-Starling curve · PV loop shifts",
      "7. Draw: normal PV loop from memory — then add effect of increased afterload",
      "8. AnKing: new cards — Cardiology physiology tag",
      "9. Qbank: 15–20 questions + weakness log",
    ]},
    {id:"d3b",mins:240,label:"Aug 26 Wed — Cardio physiology 2: vasodilation, cardiac cycle, RAAS, conduction",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Cardiology: Ch.7 Vasodilation and Vasoconstriction + Ch.8 Pressure Flow Physiology",
      "3. Bootcamp Cardiology: Ch.9 Cardiac Cycle",
      "4. Bootcamp Cardiology: Ch.10 RAAS",
      "5. Bootcamp Cardiology: Ch.11 Exercise and Cardiac Conductive Physiology + Ch.12 (same chapter group)",
      "6. Sketchy Pharmacology: Cardiovascular and Renal group — open the Cardiovascular and Renal module and watch all videos in order (watch TWICE each) · 21 videos, 6 hrs at 1.25x (combined with Autonomic Drugs day total)",
      "7. First Aid Cardiology: RAAS + cardiac cycle (20 min checklist)",
      "8. Know RAAS step by step: renin → Ang I → ACE → Ang II → aldosterone → effect",
      "9. AnKing: new cards",
      "10. Qbank: 15–20 questions + weakness log",
    ]},
    {id:"d3c",mins:165,label:"Aug 27 Thu — Cardio pathophysiology 1: antiarrhythmics + arrhythmias + conduction block",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Cardiology: Ch.13 Antiarrhythmics",
      "3. Bootcamp Cardiology: Ch.14 Atrial and Ventricular Arrhythmias + Ch.15 (same chapter group)",
      "4. Bootcamp Cardiology: Ch.16 Conduction Block",
      "5. First Aid Cardiology: arrhythmias + antiarrhythmics sections (20 min checklist)",
      "6. Know antiarrhythmics by Vaughan-Williams class I–IV: mechanism + prototype + toxicity",
      "7. AnKing: new cards",
      "8. Qbank: 20 questions + weakness log",
    ]},
    {id:"d3d",mins:195,label:"Aug 28 Fri — Cardio pathophysiology 2: HF, cardiomyopathy, HTN, shock",tasks:[
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
    {id:"d3e",mins:240,label:"Aug 29 Sat — Cardio pathophysiology 3: ischemia, aortic, valvular, congenital",tasks:[
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
    {id:"d3f",mins:165,label:"Aug 30 Sun — Pulmonary physiology: introduction, air, blood",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Pulmonology: Ch.1 Introduction",
      "3. Bootcamp Pulmonology: Ch.2 Air Physiology",
      "4. Bootcamp Pulmonology: Ch.3 Blood Physiology",
      "5. First Aid Pulmonology: physiology section (20 min checklist)",
      "6. Know: TLC · FRC · RV · ERV · IRV · TV · V/Q mismatch · A-a gradient · oxygenation vs ventilation",
      "7. Draw: V/Q lung unit from memory",
      "8. AnKing: new cards — Pulm tag",
      "9. Qbank: 15–20 questions + weakness log",
    ]},
    {id:"d3g",mins:195,label:"Aug 31 Mon — Pulmonary pathophysiology: obstructive + restrictive + lung cancer",tasks:[
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
    {id:"d3h",mins:135,label:"Sep 1 Tue — Pulmonary special topics + review",tasks:[
      "1. AnKing: due reviews",
      "2. Bootcamp Pulmonology: Ch.8 Lung Pathology Special Topics",
      "3. First Aid Pulmonology: PE · ARDS · pulmonary HTN · pleural effusions (20 min checklist)",
      "4. Review: PE (saddle embolus → right heart strain) · ARDS (diffuse alveolar damage · non-cardiogenic · low PCWP)",
      "5. Make: PE diagnosis flowchart — Wells criteria → CT-PA → anticoagulation decision",
      "6. AnKing: new cards",
      "7. Qbank: 30 mixed pulm questions + weakness log",
    ]},
    {id:"d3i",mins:195,label:"Sep 2 Wed — Renal physiology: anatomy, filtration, nephron transporters, RAAS",tasks:[
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
    {id:"d3j",mins:150,label:"Sep 3 Thu — Renal physiology 2: electrolytes + acid-base",tasks:[
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
    {id:"d3k",mins:165,label:"Sep 4 Fri — Renal pathophysiology: nephrotic + nephritic + kidney injury",tasks:[
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
    {id:"d3l",mins:240,label:"Sep 5 Sat — Renal pharm + stones + integrated review",tasks:[
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
  {id:"vac4",color:"#7C3AED",type:"vacation",label:"🏥 Orthopedic Surgery Internship 2",dates:"Sep 6–24",note:"AnKing reviews only for Cardio/Pulm/Renal/Pharm · Self-paced MSK checklist continues — no fixed daily quota",days:[
    {id:"vac4a",label:"Sep 6–24 — Internship + self-paced MSK review (19 days)",tasks:[
      "AnKing: due reviews only, every day — Cardio/Pulm/Renal/Pharm decks",
      "No new cards. Goal: preserve foundation before Year 3 starts September 28.",
      "— MSK ANATOMY + PATHOLOGY CHECKLIST CONTINUED (whatever wasn't finished in Internship 1) —",
      "☐ Bootcamp MSK/Rheum Ch.2 Non-Rheumatologic Diseases",
      "☐ Bootcamp MSK/Rheum Ch.3 Rheumatologic Diseases — key for peri-op medical clearance discussions",
      "☐ Bootcamp MSK/Rheum Ch.4 Seronegative Spondyloarthritis",
      "☐ Bootcamp MSK/Rheum Ch.6 Vasculitides",
      "☐ Bootcamp MSK/Rheum Ch.15 Pharmacology — NSAIDs, perioperative anticoagulation holds, bone-related drugs",
      "☐ Review: common ortho emergencies — septic joint, compartment syndrome, open fracture, cauda equina",
      "☐ Review: classic imaging findings — Salter-Harris classification (pediatric), Ottawa ankle/knee rules",
      "☐ Review: post-op complications — DVT/PE risk, fat embolism syndrome, infection",
      "☐ Make a one-page cheat sheet: for each major joint — approach, structures at risk, most common fracture pattern",
      "☐ Final self-check: can you describe the nerve/vessel at risk for the 5 most common ortho procedures you saw?",
      "Goal: leave the second internship able to confidently discuss anatomy and management on rounds.",
    ]},
  ]},
  {id:"p4",color:"#0F766E",type:"study",label:"Phase 4 — Pre-Year 3 Launch",dates:"Sep 25–27 · Year 3 begins Sep 28",note:"Light review + system setup only — NOT for new content",days:[
    {id:"d4a",mins:240,label:"Sep 25 Fri — Pathology + heme/coag review",tasks:[
      "1. AnKing: due reviews (clear any backlog first)",
      "2. Bootcamp Hematology/Oncology: Ch.2 Blood Cells",
      "3. Bootcamp Hematology/Oncology: Ch.6 Platelets",
      "4. Bootcamp Hematology/Oncology: Ch.7 Coagulation and Fibrinolysis",
      "5. Sketchy Pharmacology: Blood and Inflammation group + Smooth Muscle group — open each module and watch all videos in order (consolidation pass) · 17 videos, 4.75 hrs at 1.25x combined",
      "6. First Aid Hematology: heme/coag tables (20 min checklist)",
      "7. Review General Pathology: cell injury · inflammation · hemodynamics · thrombosis · shock · neoplasia",
      "8. Build coagulation cascade from memory: intrinsic vs extrinsic vs common pathway",
      "9. Qbank: 30–40 mixed path/heme questions",
    ]},
    {id:"d4b",mins:180,label:"Sep 26 Sat — Pharmacology master review",tasks:[
      "1. AnKing: due reviews",
      "2. Sketchy Pharmacology: Pharmacology Foundations group + Autonomic Drugs group + Antimicrobials group + Cardiovascular and Renal group — re-watch consolidation pass (select weak videos only)",
      "3. Review Bootcamp Pharmacology: Ch.1 Pharmacodynamics · Ch.2 Pharmacokinetics · Ch.3 Autonomic System · Ch.4 Side Effects and Toxins",
      "4. First Aid Pharmacology: general principles sections (20 min checklist)",
      "5. Make drug-class weakness list — which classes feel shakiest going into Year 3?",
      "6. Qbank: 30–40 pharm questions",
      "7. ⭐ Saturday rule: final summer-wide weakness log sweep",
    ]},
    {id:"d4c",mins:165,label:"Sep 27 Sun — Year 3 readiness",tasks:[
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

</script>
<script>
// ═══════════════════════════════════════════════════════════
// STATE
// ═══════════════════════════════════════════════════════════
let checked = {};        // { taskId: true }
let schedule = {};        // { dayId: 'YYYY-MM-DD' }
let weaknessLog = {};     // { phaseId: [ {text, date} ] }
let openPhase = null;
let openDay = null;
let currentView = 'tracker';
let selectedCalDate = null;
let originalPhasesSnapshot = null; // deep copy for undo

const DAILY_ORDER=[
  {n:1,t:"AnKing: due reviews",note:"Always first — before Bootcamp, before everything. 60 min."},
  {n:2,t:"Bootcamp or Sketchy",note:"Bootcamp for physiology/path/immuno/pharm foundations. Sketchy for Micro + Pharm ONLY. 90–120 min."},
  {n:3,t:"First Aid — same topic",note:"Checklist read after Bootcamp/Sketchy. Annotate gaps. 20–30 min max."},
  {n:4,t:"AnKing: new cards",note:"Today's topic ONLY. 40–80 normal / max 100 heavy / 0–30 review day / 0 vacation."},
  {n:5,t:"Qbank questions",note:"10–20 early phases → 30–40 later. Every wrong answer → weakness log immediately."},
  {n:6,t:"Weakness log",note:"Topic + why I missed it + correct rule in one line + fix resource."},
];

const OVERVIEW_TEMPLATE=[
  {c:"#5C54D4",id:"p1",l:"Phase 1 ⭐"},
  {c:"#0891B2",id:"vactravel",l:"✈️ Travel"},
  {c:"#5C54D4",id:"p1cont",l:"Phase 1 (cont.) ⭐"},
  {c:"#B91C1C",id:"p2",l:"Phase 2 ⭐"},
  {c:"#7C3AED",id:"vac3",l:"🏥 Ortho Internship 1"},
  {c:"#047857",id:"p3",l:"Phase 3 ⭐"},
  {c:"#7C3AED",id:"vac4",l:"🏥 Ortho Internship 2"},
  {c:"#0F766E",id:"p4",l:"Phase 4"},
];
const OVERVIEW_DESC={
  p1:"Setup + General pathology + Immunology. Cell injury through neoplasia. Immunology Ch.1–13.",
  vactravel:"Real travel break. AnKing reviews only if you have a spare moment — no pressure, no new content expected.",
  p1cont:"Finishing Pharm foundations (PD, PK, Autonomics) before Microbiology begins. Light re-entry after travel.",
  p2:"Bootcamp Micro Ch.1–39 in order. Sketchy Micro: Bacteria · RNA Viruses · DNA Viruses · Fungi · Parasites modules. Sketchy Pharm: Antimicrobials module.",
  vac3:"Orthopedic Surgery internship. AnKing reviews only for Micro/Pharm. Self-paced MSK anatomy + ortho pathology checklist — no fixed quota, fit around internship hours.",
  p3:"Bootcamp Cardiology Ch.1–28 (5 days) → Pulmonology Ch.1–8 (3 days) → Nephrology Ch.1–15 (3 days). Physiology always before pathology. Sketchy Pharm: Cardiovascular and Renal module.",
  vac4:"Orthopedic Surgery internship. AnKing reviews only for Cardio/Pulm/Renal/Pharm. MSK checklist continues from Internship 1.",
  p4:"Light review: Bootcamp Heme/Onc Ch.2·6·7 + Sketchy Pharm consolidation. Pharm master review. Year 3 workflow setup. Year 3 starts Sep 28.",
};

// ═══════════════════════════════════════════════════════════
// STORAGE
// ═══════════════════════════════════════════════════════════
function load(){ try{const s=localStorage.getItem('sp_v5'); if(s) checked=JSON.parse(s);}catch(e){} }
function save(){ try{localStorage.setItem('sp_v5',JSON.stringify(checked));}catch(e){} }
function saveSchedule(){ try{localStorage.setItem('sp_sched_v3',JSON.stringify(schedule));}catch(e){} }
function loadSchedule(){ try{const s=localStorage.getItem('sp_sched_v3'); if(s) schedule=JSON.parse(s);}catch(e){} }
function saveWeakness(){ try{localStorage.setItem('sp_weakness_v1',JSON.stringify(weaknessLog));}catch(e){} }
function loadWeakness(){ try{const s=localStorage.getItem('sp_weakness_v1'); if(s) weaknessLog=JSON.parse(s);}catch(e){} }
function savePhasesMeta(){
  // Persist only the mutable date/note/label fields, not the whole tree
  const meta={};
  PHASES.forEach(p=>{
    meta[p.id]={dates:p.dates,note:p.note,days:p.days.map(d=>({id:d.id,label:d.label}))};
  });
  try{localStorage.setItem('sp_phasemeta_v3',JSON.stringify(meta));}catch(e){}
}
function loadPhasesMeta(){
  try{
    const s=localStorage.getItem('sp_phasemeta_v3');
    if(!s) return;
    const meta=JSON.parse(s);
    PHASES.forEach(p=>{
      if(meta[p.id]){
        p.dates=meta[p.id].dates;
        p.note=meta[p.id].note;
        meta[p.id].days.forEach(md=>{
          const day=p.days.find(d=>d.id===md.id);
          if(day) day.label=md.label;
        });
      }
    });
  }catch(e){}
}

// ═══════════════════════════════════════════════════════════
// TASK / DAY / PHASE HELPERS
// ═══════════════════════════════════════════════════════════
function allIds(){ return PHASES.flatMap(p=>p.days.flatMap(d=>d.tasks.map((_,i)=>`${d.id}_${i}`))); }
function phaseDone(ph){ return ph.days.flatMap(d=>d.tasks.map((_,i)=>`${d.id}_${i}`)).filter(id=>checked[id]).length; }
function phaseTotal(ph){ return ph.days.flatMap(d=>d.tasks).length; }
function dayDone(d){ return d.tasks.filter((_,i)=>checked[`${d.id}_${i}`]).length; }
function todayISO(){
  const t=new Date();
  const y=t.getFullYear();
  const m=String(t.getMonth()+1).padStart(2,'0');
  const d=String(t.getDate()).padStart(2,'0');
  return `${y}-${m}-${d}`;
}

function fmtDate(dateStr){
  const d=new Date(dateStr+'T12:00:00');
  return ['Sun','Mon','Tue','Wed','Thu','Fri','Sat'][d.getDay()]+' '+
    ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'][d.getMonth()]+' '+d.getDate();
}
function fmtDateLong(dateStr){
  const d=new Date(dateStr+'T12:00:00');
  return ['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'][d.getDay()]+', '+
    ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'][d.getMonth()]+' '+d.getDate();
}

// ═══════════════════════════════════════════════════════════
// STREAK CALCULATION
// ═══════════════════════════════════════════════════════════
// A "streak day" = a scheduled study day where the AnKing review task (task index 0) is checked.
// We walk backward from today through scheduled days until we hit a day that isn't done.
function computeStreak(){
  const today=todayISO();
  // Build list of {date, day} for all study days using current schedule, sorted ascending
  const allStudyDays=PHASES.filter(p=>p.type==='study').flatMap(p=>p.days);
  const withDates=allStudyDays
    .map(d=>({ day:d, date:schedule[d.id] }))
    .filter(x=>x.date && x.date<=today)
    .sort((a,b)=>b.date.localeCompare(a.date)); // descending, most recent first

  let streak=0;
  for(const {day,date} of withDates){
    // "Done" for streak purposes = AnKing review task (index 0) checked
    const ankingDone = checked[`${day.id}_0`];
    if(ankingDone){
      streak++;
    } else if(date===today){
      // Today not done yet doesn't break the streak — just doesn't count yet
      continue;
    } else {
      break;
    }
  }
  return streak;
}

// ═══════════════════════════════════════════════════════════
// WEAKNESS LOG
// ═══════════════════════════════════════════════════════════
function openWeaknessLog(phaseId){
  const phase=PHASES.find(p=>p.id===phaseId);
  if(!phase) return;
  document.getElementById('weakness-modal-sub').textContent=phase.label;
  renderWeaknessBody(phaseId);
  document.getElementById('modal-weakness').style.display='flex';
  document.body.style.overflow='hidden';
}

function renderWeaknessBody(phaseId){
  const entries=weaknessLog[phaseId]||[];
  let html='';
  if(entries.length>0){
    html+='<div class="weakness-entries">';
    entries.forEach((e,i)=>{
      html+=`<div class="weakness-entry">${escapeHtml(e.text)}<span class="weakness-entry-del" onclick="deleteWeaknessEntry('${phaseId}',${i})">✕ remove</span></div>`;
    });
    html+='</div>';
  } else {
    html+='<div style="text-align:center;color:#94A3B8;font-size:12.5px;padding:16px 0">No entries yet. Add one below after each wrong Qbank answer.</div>';
  }
  html+=`<textarea class="weakness-textarea" id="weakness-input" placeholder="Topic: ... | Why I missed it: ... | Correct rule: ..."></textarea>`;
  html+=`<button class="weakness-save" onclick="addWeaknessEntry('${phaseId}')">+ Add entry</button>`;
  document.getElementById('weakness-modal-body').innerHTML=html;
}

function addWeaknessEntry(phaseId){
  const input=document.getElementById('weakness-input');
  const text=input.value.trim();
  if(!text) return;
  if(!weaknessLog[phaseId]) weaknessLog[phaseId]=[];
  weaknessLog[phaseId].push({ text, date: todayISO() });
  saveWeakness();
  renderWeaknessBody(phaseId);
  renderTracker(); // update entry count shown inline
}

function deleteWeaknessEntry(phaseId,idx){
  if(!weaknessLog[phaseId]) return;
  weaknessLog[phaseId].splice(idx,1);
  saveWeakness();
  renderWeaknessBody(phaseId);
  renderTracker();
}

function weaknessCount(phaseId){
  return (weaknessLog[phaseId]||[]).length;
}

function escapeHtml(s){
  const d=document.createElement('div');
  d.textContent=s;
  return d.innerHTML;
}
</script>
<script>
// ═══════════════════════════════════════════════════════════
// HEADER / STREAK
// ═══════════════════════════════════════════════════════════
function updateHeader(){
  const ids=allIds(), done=ids.filter(id=>checked[id]).length, pct=ids.length?Math.round(done/ids.length*100):0;
  document.getElementById('main-bar').style.width=pct+'%';
  document.getElementById('main-label').textContent=`${done} of ${ids.length} tasks · ${pct}% complete`;

  const streak=computeStreak();
  document.getElementById('streak-num').textContent=streak;
  const badge=document.getElementById('streak-badge');
  const flame=badge.querySelector('.streak-flame');
  if(streak===0){ flame.textContent='💤'; badge.style.opacity='0.6'; }
  else if(streak<3){ flame.textContent='🔥'; badge.style.opacity='1'; }
  else if(streak<7){ flame.textContent='🔥🔥'; badge.style.opacity='1'; }
  else { flame.textContent='🔥🔥🔥'; badge.style.opacity='1'; }
}

// ═══════════════════════════════════════════════════════════
// TODAY BANNER
// ═══════════════════════════════════════════════════════════
function findTodayDay(){
  const today=todayISO();
  for(const phase of PHASES){
    for(const day of phase.days){
      if(schedule[day.id]===today) return { phase, day };
    }
  }
  return null;
}

function isVacationToday(){
  const today=todayISO();
  return VACATION_RANGES.some(([s,e])=>today>=s&&today<=e);
}

function isInternshipToday(){
  const today=todayISO();
  const internshipRanges=[['2026-08-10','2026-08-24'],['2026-09-06','2026-09-24']];
  return internshipRanges.some(([s,e])=>today>=s&&today<=e);
}

function renderTodayBanner(){
  const el=document.getElementById('today-banner');
  const today=todayISO();

  if(isInternshipToday()){
    el.className='today-banner today-banner-vacation';
    el.style.setProperty('--pc','#7C3AED');
    el.innerHTML=`
      <div class="today-banner-label" style="color:#7C3AED">Today · ${fmtDate(today)}</div>
      <div class="today-banner-title">🏥 Orthopedic Surgery Internship</div>
      <div class="today-banner-sub">AnKing due reviews only for content decks · self-paced MSK checklist — fit around your hours today</div>`;
    return;
  }

  if(isVacationToday()){
    el.className='today-banner today-banner-vacation';
    el.innerHTML=`
      <div class="today-banner-label">Today · ${fmtDate(today)}</div>
      <div class="today-banner-title">🌴 Vacation day</div>
      <div class="today-banner-sub">AnKing due reviews only — no new content today</div>`;
    return;
  }

  const found=findTodayDay();
  el.className='today-banner';

  if(!found){
    const beforeStart=today<'2026-06-24';
    const afterEnd=today>'2026-09-27';
    el.innerHTML=`
      <div class="today-banner-label">Today · ${fmtDate(today)}</div>
      <div class="today-banner-empty">${
        beforeStart ? 'Plan starts July 4 — nothing scheduled yet.' :
        afterEnd ? '🎓 Plan period complete — Year 3 is underway.' :
        'No day scheduled for today. Tap ⚖️ Rebalance to fix the schedule.'
      }</div>`;
    return;
  }

  const { phase, day } = found;
  const done=dayDone(day), total=day.tasks.length;
  const titlePart=day.label.replace(/^\S+ \d+ \S+(\s\(S\d+\/\d+\))? — /,'');
  const dots=Array.from({length:total},(_,i)=>{
    const isDone=!!checked[`${day.id}_${i}`];
    return `<div class="today-banner-dot${isDone?' done':''}"></div>`;
  }).join('');

  el.innerHTML=`
    <div class="today-banner-label">Today · ${fmtDate(today)}</div>
    <div class="today-banner-title">${titlePart}</div>
    <div class="today-banner-sub">
      <span>${done}/${total} tasks complete</span>
      ${day.mins?`<span class="cal-day-popup-time" style="margin-left:8px;padding:2px 8px">⏱ ~${day.mins} min</span>`:''}
      <span class="today-banner-arrow">→</span>
    </div>
    <div class="today-banner-progress">${dots}</div>`;

  // stash for click handler
  el.dataset.phaseId=phase.id;
  el.dataset.dayId=day.id;
}

function jumpToToday(){
  const found=findTodayDay();
  if(!found) return;
  showView('tracker');
  openPhase=found.phase.id;
  openDay=found.day.id;
  renderTracker();
  // scroll into view after render
  setTimeout(()=>{
    const el=document.getElementById('day-'+found.day.id);
    if(el) el.scrollIntoView({behavior:'smooth',block:'center'});
  },50);
}

// ═══════════════════════════════════════════════════════════
// NAV
// ═══════════════════════════════════════════════════════════
function showView(v){
  currentView=v;
  ['tracker','calendar','order','overview'].forEach(n=>{
    document.getElementById('view-'+n).style.display=n===v?'block':'none';
    const b=document.getElementById('btn-'+n);
    if(b) b.className=n===v?'active':'inactive';
  });
  if(v==='calendar') renderCalendar();
}

function resetAll(){
  if(!confirm('Reset all checked-off progress? (Schedule and weakness log stay intact)')) return;
  checked={};
  save();
  renderAll();
}

// ═══════════════════════════════════════════════════════════
// TASK TOGGLE
// ═══════════════════════════════════════════════════════════
function toggleTask(tid){
  checked[tid]=!checked[tid];
  save();
  updateHeader();
  renderTodayBanner();

  const box=document.getElementById('box-'+tid), txt=document.getElementById('txt-'+tid);
  const pc=document.getElementById('pc-'+tid.split('_')[0]);
  const col=pc?pc.value:'#5C54D4';
  if(box){ box.className='task-box'+(checked[tid]?' done':''); box.style.setProperty('--pc',col); box.innerHTML=checked[tid]?'<span>✓</span>':''; }
  if(txt){ txt.className='task-text'+(checked[tid]?' done':''); }

  const dayId=tid.split('_').slice(0,-1).join('_');
  updateDayCircle(dayId);
  updatePhaseProgress(dayId);
}

function updateDayCircle(dayId){
  for(const p of PHASES){
    const d=p.days.find(d=>d.id===dayId);
    if(d){
      const done=dayDone(d), circ=document.getElementById('circ-'+dayId), cnt=document.getElementById('cnt-'+dayId);
      if(circ){
        if(done===d.tasks.length){ circ.className='day-circle done'; circ.style.setProperty('--pc',p.color); circ.innerHTML='<span>✓</span>'; }
        else{ circ.className='day-circle'; circ.innerHTML=''; }
      }
      if(cnt) cnt.textContent=`${done}/${d.tasks.length}`;
      break;
    }
  }
}

function updatePhaseProgress(dayId){
  for(const p of PHASES){
    if(p.days.find(d=>d.id===dayId)){
      const done=phaseDone(p), total=phaseTotal(p), pct=total?Math.round(done/total*100):0;
      const pe=document.getElementById('ppct-'+p.id), ce=document.getElementById('pcnt-'+p.id), be=document.getElementById('pbar-'+p.id);
      if(pe) pe.textContent=pct+'%'; if(ce) ce.textContent=`${done}/${total}`; if(be) be.style.width=pct+'%';
      break;
    }
  }
}

function togglePhase(id){ openPhase=openPhase===id?null:id; renderTracker(); }
function toggleDay(id){ openDay=openDay===id?null:id; renderTracker(); }

function rgba(hex,a){ const r=parseInt(hex.slice(1,3),16),g=parseInt(hex.slice(3,5),16),b=parseInt(hex.slice(5,7),16); return `rgba(${r},${g},${b},${a})`; }

// ═══════════════════════════════════════════════════════════
// TRACKER RENDER
// ═══════════════════════════════════════════════════════════
function renderTracker(){
  const today=todayISO();
  let html='';
  for(const phase of PHASES){
    const isOpen=openPhase===phase.id, isVac=phase.type==='vacation';
    const done=phaseDone(phase), total=phaseTotal(phase), pct=total?Math.round(done/total*100):0;
    const bg=isVac?'#FFFBEB':rgba(phase.color,0.07), bc=rgba(phase.color,0.2);
    const isTodayPhase=!isVac && phase.days.some(d=>schedule[d.id]===today);
    const wCount=weaknessCount(phase.id);
    const rebalanced=phase.note.includes('Rebalanced');

    html+=`<input type="hidden" id="pc-${phase.id}" value="${phase.color}">
    <div class="phase">
      <div class="phase-header${isOpen?' open':''}${isTodayPhase?' is-today-phase':''}" style="background:${bg};border-color:${bc};border-left-color:${phase.color};opacity:${isVac?0.8:1}" onclick="togglePhase('${phase.id}')">
        <div class="phase-row">
          <div style="flex:1">
            <div class="phase-dates" style="color:${phase.color}">${phase.dates}</div>
            <div class="phase-label">${phase.label}</div>
            <div class="phase-note">${phase.note.replace(' · Rebalanced ⚖️','')}${rebalanced?'<span class="rebalanced-tag">⚖️ rebalanced</span>':''}</div>
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
        const dd=dayDone(day), dt=day.tasks.length, isDayOpen=openDay===day.id, allDone=dd===dt;
        const isToday=schedule[day.id]===today;
        html+=`<div class="day${isToday?' is-today':''}" id="day-${day.id}">
          <div class="day-header" style="background:${allDone?rgba(phase.color,0.05):'white'}" onclick="toggleDay('${day.id}')">
            <div class="day-info">
              <div class="day-circle${allDone?' done':''}" id="circ-${day.id}" style="--pc:${phase.color};${allDone?`background:${phase.color};border-color:${phase.color}`:''}">
                ${allDone?'<span>✓</span>':''}
              </div>
              <span class="day-label">${day.label}${isToday?'<span class="today-pill">TODAY</span>':''}</span>
            </div>
            <div class="day-meta">
              <span class="day-count" id="cnt-${day.id}" style="color:${phase.color}">${dd}/${dt}</span>
              <span style="color:#94A3B8;font-size:12px">${isDayOpen?'▲':'▼'}</span>
            </div>
          </div>`;
        if(isDayOpen){
          html+=`<div class="tasks">`;
          day.tasks.forEach((task,i)=>{
            const tid=`${day.id}_${i}`, done=!!checked[tid];
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
      // Weakness log button for study phases
      if(!isVac){
        html+=`<div style="padding:4px 15px 14px">
          <button class="weakness-btn" onclick="event.stopPropagation();openWeaknessLog('${phase.id}')">
            📝 Weakness log ${wCount>0?`(${wCount} ${wCount===1?'entry':'entries'})`:'— add entry'}
          </button>
        </div>`;
      }
      html+=`</div>`;
    }
    html+=`</div>`;
  }
  document.getElementById('view-tracker').innerHTML=html;
}

// ═══════════════════════════════════════════════════════════
// DAILY ORDER RENDER
// ═══════════════════════════════════════════════════════════
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
  [{r:"Bootcamp",c:"#5C54D4",d:"Main teaching spine. Watch at 1.25–1.5×. Pause before answers. Used for physiology, pathophysiology, immunology, pharm foundations."},
   {r:"Sketchy",c:"#B91C1C",d:"Micro + Pharm ONLY. Watch every video TWICE — story first, then active recall. Close and write everything you remember after."},
   {r:"First Aid",c:"#047857",d:"Annotation hub. Read matching pages AFTER Bootcamp/Sketchy. Annotate gaps. 20–30 min max."},
   {r:"AnKing",c:"#0369A1",d:"Reviews always first. Unsuspend only cards from today's studied topic. Never unsuspend entire decks."},
   {r:"Qbank",c:"#334155",d:"10–20/day early phases → 30–40 later. Every wrong answer → weakness log immediately."}].forEach(({r,c,d})=>{
    html+=`<div class="resource-item" style="border-left:3px solid ${c}"><div class="resource-name" style="color:${c}">${r}</div><div class="resource-desc">${d}</div></div>`;
  });
  html+=`</div>`;
  document.getElementById('view-order').innerHTML=html;
}

// ═══════════════════════════════════════════════════════════
// CALENDAR RENDER
// ═══════════════════════════════════════════════════════════
function getDayById(dayId){
  for(const phase of PHASES){
    const d=phase.days.find(d=>d.id===dayId);
    if(d) return {day:d, phase};
  }
  return null;
}

function getScheduleForDate(dateStr){
  // Return {dayId, phase} for this date, or null
  for(const [id,date] of Object.entries(schedule)){
    if(date===dateStr){
      const found=getDayById(id);
      if(found) return found;
    }
  }
  // Check fixed vacation-type blocks (travel + both internships) by their own explicit dates
  const vacationMap=[
    {id:'vactravel', start:'2026-07-14', end:'2026-07-26'},
    {id:'vac3', start:'2026-08-10', end:'2026-08-24'},
    {id:'vac4', start:'2026-09-06', end:'2026-09-24'},
  ];
  for(const {id,start,end} of vacationMap){
    if(dateStr>=start && dateStr<=end){
      const phase=PHASES.find(p=>p.id===id);
      if(phase) return {day:null, phase, isVacation:true};
    }
  }
  return null;
}

function renderCalendar(){
  const today=todayISO();
  const months=[
    {y:2026,m:7,name:'July 2026'},
    {y:2026,m:8,name:'August 2026'},
    {y:2026,m:9,name:'September 2026'},
  ];

  let html='';
  months.forEach(({y,m,name})=>{
    const firstDay=new Date(y,m-1,1);
    const daysInMonth=new Date(y,m,0).getDate();
    const startWeekday=firstDay.getDay(); // 0=Sun

    html+=`<div class="cal-month"><div class="cal-month-title">${name}</div><div class="cal-grid">`;
    ['S','M','T','W','T','F','S'].forEach(d=>{ html+=`<div class="cal-dow">${d}</div>`; });

    for(let i=0;i<startWeekday;i++){ html+=`<div class="cal-cell empty"></div>`; }

    for(let day=1;day<=daysInMonth;day++){
      const dateStr=`${y}-${String(m).padStart(2,'0')}-${String(day).padStart(2,'0')}`;
      const isToday=dateStr===today;
      const info=getScheduleForDate(dateStr);

      let bg='#F8FAFC', textColor='#94A3B8', mins='', dotColor='';
      if(info){
        if(info.isVacation){
          bg=rgba(info.phase.color,0.18); textColor=info.phase.color; dotColor=info.phase.color;
        } else if(info.day){
          const color=info.phase.color;
          const dayComplete=dayDone(info.day)===info.day.tasks.length;
          bg=dayComplete?rgba(color,0.35):rgba(color,0.15);
          textColor=color;
          dotColor=color;
          if(info.day.mins) mins=info.day.mins+'m';
        }
      }

      html+=`<div class="cal-cell${isToday?' today':''}" style="background:${bg};color:${textColor}"
        onclick="goToCalendarDay('${dateStr}')">
        <div class="cal-cell-num">${day}</div>
        ${dotColor?`<div class="cal-cell-dot" style="background:${dotColor}"></div>`:''}
        ${mins?`<div class="cal-cell-mins">${mins}</div>`:''}
      </div>`;
    }
    html+=`</div></div>`;
  });

  // Legend
  html+=`<div class="cal-month"><div class="cal-legend">`;
  const legendItems=[
    {c:'#5C54D4',l:'Phase 1 — Path/Immuno/Pharm'},
    {c:'#0891B2',l:'✈️ Travel'},
    {c:'#B91C1C',l:'Phase 2 — Microbiology'},
    {c:'#7C3AED',l:'🏥 Ortho Internships'},
    {c:'#047857',l:'Phase 3 — Cardio/Pulm/Renal'},
    {c:'#0F766E',l:'Phase 4 — Launch'},
  ];
  legendItems.forEach(({c,l})=>{
    html+=`<div class="cal-legend-item"><div class="cal-legend-dot" style="background:${c}"></div>${l}</div>`;
  });
  html+=`</div></div>`;

  // Selected day detail (default: today)
  html+=`<div id="cal-day-detail"></div>`;

  document.getElementById('view-calendar').innerHTML=html;
  showCalDayDetail(selectedCalDate || today);
}

function showCalDayDetail(dateStr){
  selectedCalDate=dateStr;
  const el=document.getElementById('cal-day-detail');
  if(!el) return;
  const info=getScheduleForDate(dateStr);
  const dateLabel=fmtDateLong(dateStr);

  if(!info){
    el.innerHTML=`<div class="cal-day-popup"><div class="cal-day-popup-date">${dateLabel}</div><div style="color:#94A3B8;font-size:13px">Outside the study plan window.</div></div>`;
    return;
  }

  if(info.isVacation){
    el.innerHTML=`<div class="cal-day-popup" style="border-left-color:${info.phase.color}">
      <div class="cal-day-popup-date" style="color:${info.phase.color}">${dateLabel}</div>
      <div class="cal-day-popup-title">${info.phase.label}</div>
      <div style="font-size:13px;color:#475569;margin-bottom:10px">${info.phase.note}</div>
      <div style="font-size:12px;color:${info.phase.color};font-weight:600;cursor:pointer" onclick="showView('tracker');togglePhaseAndDay('${info.phase.id}','${info.phase.days[0].id}')">View full checklist in Tracker →</div>
    </div>`;
    return;
  }

  if(info.day){
    const day=info.day, phase=info.phase;
    const done=dayDone(day), total=day.tasks.length;
    const titlePart=day.label.replace(/^\S+ \d+ \S+(\s\(S\d+\/\d+\))? — /,'');
    const color=phase.color;

    const taskRows=day.tasks.map((task,i)=>{
      const tid=`${day.id}_${i}`;
      const isDone=!!checked[tid];
      return `<div class="task" onclick="toggleCalTask('${tid}','${dateStr}')">
        <div class="task-box${isDone?' done':''}" id="calbox-${tid}" style="--pc:${color};${isDone?`background:${color};border-color:${color}`:''}">
          ${isDone?'<span>✓</span>':''}
        </div>
        <span class="task-text${isDone?' done':''}" id="caltxt-${tid}">${task}</span>
      </div>`;
    }).join('');

    el.innerHTML=`<div class="cal-day-popup" style="border-left-color:${color}">
      <div class="cal-day-popup-date" style="color:${color}">${dateLabel} · ${phase.label.replace(/⭐|🏥/g,'').trim()}</div>
      <div class="cal-day-popup-title">${titlePart}</div>
      <div style="display:flex;align-items:center;gap:8px;margin-bottom:10px">
        ${day.mins?`<span class="cal-day-popup-time">⏱ ~${day.mins} min</span>`:''}
        <span id="caldone-${day.id}" style="font-size:12px;color:#64748B;font-weight:600">${done}/${total} complete</span>
      </div>
      <div style="background:#F8FAFC;border-radius:12px;padding:6px 8px">${taskRows}</div>
    </div>`;
  }
}

function toggleCalTask(tid,dateStr){
  toggleTask(tid); // reuses existing logic — updates checked{}, saves, updates tracker elements if open
  // Update the calendar's own copy of this task row
  const box=document.getElementById('calbox-'+tid), txt=document.getElementById('caltxt-'+tid);
  const dayId=tid.split('_').slice(0,-1).join('_');
  const found=getDayById(dayId);
  if(box && found){
    const color=found.phase.color;
    box.className='task-box'+(checked[tid]?' done':'');
    box.style.setProperty('--pc',color);
    if(checked[tid]){ box.style.background=color; box.style.borderColor=color; box.innerHTML='<span>✓</span>'; }
    else { box.style.background='white'; box.style.borderColor='#CBD5E1'; box.innerHTML=''; }
  }
  if(txt){ txt.className='task-text'+(checked[tid]?' done':''); }
  // Update the completion count shown in the popup
  if(found){
    const doneEl=document.getElementById('caldone-'+dayId);
    if(doneEl) doneEl.textContent=`${dayDone(found.day)}/${found.day.tasks.length} complete`;
  }
  // Refresh the calendar grid cell coloring (day may now be fully complete)
  renderCalendar();
  showCalDayDetail(dateStr);
}

function togglePhaseAndDay(phaseId,dayId){
  openPhase=phaseId;
  openDay=dayId;
  renderTracker();
  setTimeout(()=>{
    const el=document.getElementById('day-'+dayId);
    if(el) el.scrollIntoView({behavior:'smooth',block:'center'});
  },50);
}

function goToCalendarDay(dateStr){
  const info=getScheduleForDate(dateStr);
  if(!info){ return; } // outside plan window, nothing to open

  if(info.isVacation){
    // Internship/vacation block — open that phase (first day) in the Tracker
    showView('tracker');
    togglePhaseAndDay(info.phase.id, info.phase.days[0].id);
    return;
  }

  if(info.day){
    showView('tracker');
    togglePhaseAndDay(info.phase.id, info.day.id);
  }
}

// ═══════════════════════════════════════════════════════════
// OVERVIEW RENDER — now dynamic, synced with actual PHASES data
// ═══════════════════════════════════════════════════════════
function renderOverview(){
  let html='';
  OVERVIEW_TEMPLATE.forEach(({c,id,l})=>{
    const phase=PHASES.find(p=>p.id===id);
    if(!phase) return;
    const rebalanced=phase.note && phase.note.includes('Rebalanced');
    html+=`<div class="overview-item" style="border-left-color:${c}">
      <div class="overview-label" style="color:${c}">${l}${rebalanced?'<span class="rebalanced-tag">⚖️ rebalanced</span>':''}</div>
      <div class="overview-dates">${phase.dates}</div>
      <div class="overview-desc">${OVERVIEW_DESC[id]}</div>
    </div>`;
  });
  html+=`<div class="principle-box"><strong style="color:#5C54D4">Guiding principle: </strong>Physiology first → pathophysiology second → pharmacology layered in. Sketchy for Micro and Pharm only. Bootcamp is the teaching spine. First Aid annotates. AnKing retains. Questions prove understanding.</div>`;
  document.getElementById('view-overview').innerHTML=html;
}

function renderAll(){
  updateHeader();
  renderTodayBanner();
  renderTracker();
  renderOrder();
  renderOverview();
}
</script>
<script>
// ═══════════════════════════════════════════════════════════
// REBALANCE
// ═══════════════════════════════════════════════════════════
const ALL_STUDY_DAYS = PHASES.filter(p=>p.type==='study').flatMap(p=>p.days);

const VACATION_RANGES = [
  ['2026-07-14','2026-07-26'],
  ['2026-08-10','2026-08-24'],
  ['2026-09-06','2026-09-24'],
];

const ORIGINAL_DATES = [
  '2026-07-04','2026-07-05','2026-07-06','2026-07-07','2026-07-08','2026-07-09',
  '2026-07-10','2026-07-11','2026-07-12','2026-07-13','2026-07-27','2026-07-28',
  '2026-07-29','2026-07-30','2026-07-31','2026-08-01','2026-08-02','2026-08-03',
  '2026-08-04','2026-08-05','2026-08-06','2026-08-07','2026-08-08','2026-08-09',
  '2026-08-25','2026-08-26','2026-08-27','2026-08-28','2026-08-29','2026-08-30',
  '2026-08-31','2026-09-01','2026-09-02','2026-09-03','2026-09-04','2026-09-05',
  '2026-09-25','2026-09-26','2026-09-27',
];

const ORIGINAL_PHASE_META = {}; // filled once at load, before any mutation

function captureOriginalPhaseMeta(){
  PHASES.forEach(p=>{
    ORIGINAL_PHASE_META[p.id]={
      dates:p.dates,
      note:p.note,
      days:p.days.map(d=>({id:d.id,label:d.label}))
    };
  });
}

function buildDefaultSchedule(){
  ALL_STUDY_DAYS.forEach((day,i)=>{ schedule[day.id]=ORIGINAL_DATES[i]||'2026-09-27'; });
}

function addDays(dateStr,n){
  const d=new Date(dateStr+'T12:00:00');
  d.setDate(d.getDate()+n);
  return d.toISOString().split('T')[0];
}
function isVacation(dateStr){
  return VACATION_RANGES.some(([s,e])=>dateStr>=s&&dateStr<=e);
}
function getAvailableDates(fromStr){
  const dates=[];
  let d=fromStr;
  const end='2026-09-27';
  while(d<=end){
    if(!isVacation(d)) dates.push(d);
    d=addDays(d,1);
  }
  return dates;
}

// Core compression: spread N content days across M calendar dates evenly
function buildCompressedSchedule(remainingDays, availableDates){
  const N=remainingDays.length, M=availableDates.length;
  if(M===0) return remainingDays.map(day=>({ date:'2026-09-27', days:[day] }));
  const slots=[];
  let ci=0;
  availableDates.forEach((date,si)=>{
    const target=Math.round(N*(si+1)/M);
    const prev=Math.round(N*si/M);
    const count=target-prev;
    const group=[];
    for(let g=0;g<count&&ci<N;g++,ci++) group.push(remainingDays[ci]);
    if(group.length>0) slots.push({date,days:group});
  });
  while(ci<N){ slots[slots.length-1].days.push(remainingDays[ci++]); }
  return slots;
}

function openRebalance(){
  const todayStr=todayISO();
  const remaining=ALL_STUDY_DAYS.filter(d=>dayDone(d)<d.tasks.length);
  const completed=ALL_STUDY_DAYS.length-remaining.length;
  const available=getAvailableDates(todayStr);
  const slots=buildCompressedSchedule(remaining,available);
  const maxPerDay=slots.length>0?Math.max(...slots.map(s=>s.days.length)):0;

  document.getElementById('modal-date').textContent='Today is '+fmtDateLong(todayStr);
  let html='';

  html+='<div class="modal-section"><div class="modal-section-title">Where you stand</div>';
  html+='<div class="rebalance-stat"><span class="rebalance-stat-label">✅ Days completed</span><span class="rebalance-stat-val" style="color:#047857">'+completed+' of '+ALL_STUDY_DAYS.length+'</span></div>';
  html+='<div class="rebalance-stat"><span class="rebalance-stat-label">📋 Content days remaining</span><span class="rebalance-stat-val" style="color:#5C54D4">'+remaining.length+'</span></div>';
  html+='<div class="rebalance-stat"><span class="rebalance-stat-label">📅 Available study dates</span><span class="rebalance-stat-val" style="color:#0369A1">'+available.length+'</span></div>';
  if(remaining.length>0&&available.length>0){
    const avg=(remaining.length/available.length).toFixed(1);
    html+='<div class="rebalance-stat"><span class="rebalance-stat-label">📊 Avg sessions per day</span><span class="rebalance-stat-val" style="color:'+(parseFloat(avg)>1.5?'#B91C1C':'#047857')+'">'+avg+'x</span></div>';
  }
  html+='</div>';

  if(remaining.length===0){
    html+='<div class="rebalance-ok">🎉 Every study day is complete. Summer done.</div>';
  } else if(available.length===0){
    html+='<div class="rebalance-warn">⚠️ No study dates remaining before Sep 27. Focus on AnKing reviews only.</div>';
  } else {
    if(maxPerDay<=1){
      html+='<div class="rebalance-ok">✅ You are on track — one content day per calendar day.</div>';
    } else if(maxPerDay===2){
      html+='<div class="rebalance-warn" style="background:#FFF9F0;border-color:#FDE68A;color:#92400E">⚠️ You are behind. The plan below doubles up on '+slots.filter(s=>s.days.length>1).length+' days — longer sessions on those days but fully doable.</div>';
    } else {
      html+='<div class="rebalance-warn">⚠️ You are significantly behind. Some days have '+maxPerDay+' sessions. If you need to cut anything, cut review days before content days.</div>';
    }

    html+='<div class="modal-section"><div class="modal-section-title">Load by period</div>';
    [
      {label:'Jul 4–13',s:'2026-07-04',e:'2026-07-13'},
      {label:'Jul 27–Aug 9',s:'2026-07-27',e:'2026-08-09'},
      {label:'Aug 25–Sep 5',s:'2026-08-25',e:'2026-09-05'},
      {label:'Sep 25–27',s:'2026-09-25',e:'2026-09-27'},
    ].forEach(({label,s,e})=>{
      const bSlots=slots.filter(sl=>sl.date>=s&&sl.date<=e);
      const total=bSlots.reduce((sum,sl)=>sum+sl.days.length,0);
      if(!total) return;
      const avg=(total/bSlots.length).toFixed(1);
      html+='<div class="rebalance-stat"><span class="rebalance-stat-label">'+label+'</span><span class="rebalance-stat-val" style="color:'+(parseFloat(avg)>1.5?'#B91C1C':'#047857')+'">'+total+' sessions · '+bSlots.length+' days · '+avg+'x/day</span></div>';
    });
    html+='</div>';

    html+='<div class="modal-section"><div class="modal-section-title">New schedule preview (first 14 study dates)</div>';
    slots.slice(0,14).forEach(({date,days})=>{
      const isToday=date===todayStr;
      const multi=days.length>1;
      const borderStyle=isToday?'border-left-color:#047857;background:#F0FFF8;':multi?'border-left-color:#B91C1C;background:#FFF5F5;':'';
      const dateColor=isToday?'color:#047857':multi?'color:#B91C1C':'';
      const prefix=isToday?'TODAY &middot; ':'';
      const sessionCount=multi?'<div style="font-size:10px;font-weight:700;color:#B91C1C;margin-top:2px">'+days.length+' sessions</div>':'';
      const divider='<div style="border-top:1px dashed #E2E8F0;margin:6px 0"></div>';
      const taskHtml=days.map((d,i)=>{
        const sessionLabel=multi?'<span style="font-size:10px;font-weight:700;color:#94A3B8;display:block;margin-bottom:2px">SESSION '+(i+1)+'</span>':'';
        const cleanLabel=d.label.replace(/^\S+ \d+ \S+(\s\(S\d+\/\d+\))? — /,'');
        return sessionLabel+cleanLabel;
      }).join(divider);
      html+='<div class="rebalance-day" style="'+borderStyle+'">'
        +'<div style="min-width:110px">'
          +'<div class="rebalance-day-date" style="'+dateColor+'">'+prefix+fmtDate(date)+'</div>'
          +sessionCount
        +'</div>'
        +'<div class="rebalance-day-tasks">'+taskHtml+'</div>'
        +'</div>';
    });
    if(slots.length>14){
      html+='<div style="text-align:center;font-size:12px;color:#94A3B8;padding:10px 0">+ '+(slots.length-14)+' more study dates</div>';
    }
    html+='</div>';
    html+='<button class="modal-btn modal-btn-primary" onclick="applyRebalance()">⚖️ Apply — Lock In This Schedule</button>';
  }

  // Undo option — only show if schedule differs from original
  const isModified=ALL_STUDY_DAYS.some((d,i)=>schedule[d.id]!==ORIGINAL_DATES[i]);
  if(isModified){
    html+='<button class="modal-btn modal-btn-secondary" id="undo-schedule-btn">↩️ Reset to Original Schedule</button>';
  }

  document.getElementById('modal-body').innerHTML=html;
  document.getElementById('modal-rebalance').style.display='flex';
  document.body.style.overflow='hidden';

  const undoBtn=document.getElementById('undo-schedule-btn');
  if(undoBtn){
    undoBtn.onclick=function(){ closeModal('modal-rebalance'); openUndoConfirm(); };
  }
}

function applyRebalance(){
  const todayStr=todayISO();
  const remaining=ALL_STUDY_DAYS.filter(d=>dayDone(d)<d.tasks.length);
  const available=getAvailableDates(todayStr);
  const slots=buildCompressedSchedule(remaining,available);
  const M=['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
  const D=['Sun','Mon','Tue','Wed','Thu','Fri','Sat'];

  // 1. Update day labels + save schedule
  slots.forEach(({date,days})=>{
    days.forEach((day,si)=>{
      schedule[day.id]=date;
      for(const phase of PHASES){
        const found=phase.days.find(d=>d.id===day.id);
        if(found){
          const d=new Date(date+'T12:00:00');
          const multi=days.length>1;
          const prefix=M[d.getMonth()]+' '+d.getDate()+' '+D[d.getDay()]+(multi?' (S'+(si+1)+'/'+days.length+')':'')+' — ';
          found.label=found.label.replace(/^\S+ \d+ \S+(\s\(S\d+\/\d+\))? — /,prefix);
          break;
        }
      }
    });
  });

  // 2. Update phase dates + notes based on new day schedule
  for(const phase of PHASES){
    if(phase.type==='vacation') continue;
    const studyDays=phase.days;
    if(!studyDays.length) continue;
    const assignedDates=studyDays.map(d=>schedule[d.id]).filter(Boolean).sort();
    if(!assignedDates.length) continue;
    const firstDate=assignedDates[0], lastDate=assignedDates[assignedDates.length-1];
    function fmtShort(ds){ const d=new Date(ds+'T12:00:00'); return M[d.getMonth()]+' '+d.getDate(); }
    phase.dates = firstDate===lastDate ? fmtShort(firstDate) : fmtShort(firstDate)+' – '+fmtShort(lastDate);

    const dateCounts={};
    assignedDates.forEach(d=>{ dateCounts[d]=(dateCounts[d]||0)+1; });
    const doubledDays=Object.values(dateCounts).filter(c=>c>1).length;
    const totalDays=Object.keys(dateCounts).length;

    let baseNote=phase.note;
    baseNote=baseNote.replace(/^\d+ days\s*·\s*/,'');
    baseNote=baseNote.replace(/\s*·\s*\d+ days[^·]*/g,'');
    baseNote=baseNote.replace(/\s*·\s*Rebalanced[^·]*/g,'');
    baseNote=baseNote.replace(/\s*·\s*STOP large[^·]*/g,'');
    baseNote=baseNote.replace(/\s*·\s*Reduce[^·]*/g,'');
    baseNote=baseNote.trimEnd().replace(/\s*·\s*$/,'');

    phase.note=baseNote+(doubledDays>0?' · '+totalDays+' days ('+doubledDays+' doubled up) · Rebalanced ⚖️':' · '+totalDays+' days · Rebalanced ⚖️');
  }

  saveSchedule();
  savePhasesMeta();
  closeModal('modal-rebalance');
  renderAll();
  const multi=slots.filter(s=>s.days.length>1).length;
  showToast(multi>0?'⚖️ Rebalanced · '+multi+' days have 2+ sessions':'✅ On track · 1 session per day');
}

// ═══════════════════════════════════════════════════════════
// UNDO SCHEDULE
// ═══════════════════════════════════════════════════════════
function openUndoConfirm(){
  document.getElementById('modal-undo').style.display='flex';
  document.body.style.overflow='hidden';
}

function confirmUndoSchedule(){
  // Restore original schedule dates
  ALL_STUDY_DAYS.forEach((day,i)=>{ schedule[day.id]=ORIGINAL_DATES[i]||'2026-09-27'; });

  // Restore original phase meta (dates, notes, day labels)
  PHASES.forEach(p=>{
    const orig=ORIGINAL_PHASE_META[p.id];
    if(!orig) return;
    p.dates=orig.dates;
    p.note=orig.note;
    orig.days.forEach(od=>{
      const day=p.days.find(d=>d.id===od.id);
      if(day) day.label=od.label;
    });
  });

  saveSchedule();
  savePhasesMeta();
  closeModal('modal-undo');
  renderAll();
  showToast('↩️ Schedule reset to original dates');
}

// ═══════════════════════════════════════════════════════════
// MODAL / TOAST UTILITIES
// ═══════════════════════════════════════════════════════════
function showToast(msg){
  const t=document.createElement('div');
  t.className='toast';
  t.textContent=msg;
  document.body.appendChild(t);
  setTimeout(()=>t.remove(),3500);
}
function closeModal(id){
  document.getElementById(id).style.display='none';
  document.body.style.overflow='';
}
function closeModalOutside(e,id){
  if(e.target===document.getElementById(id)) closeModal(id);
}

// ═══════════════════════════════════════════════════════════
// INIT
// ═══════════════════════════════════════════════════════════
captureOriginalPhaseMeta();
load();
loadWeakness();
loadSchedule();

// Self-healing check: if the cached schedule references day-ids that no longer
// exist in the current PHASES structure (e.g. after a plan restructure), the
// cache is stale and must be discarded rather than silently producing gaps.
(function validateSchedule(){
  const validIds=new Set(ALL_STUDY_DAYS.map(d=>d.id));
  const cachedIds=Object.keys(schedule);
  const isStale = cachedIds.length!==validIds.size || cachedIds.some(id=>!validIds.has(id));
  if(isStale){
    schedule={};
    buildDefaultSchedule();
    saveSchedule();
  }
})();

if(Object.keys(schedule).length===0) buildDefaultSchedule();
loadPhasesMeta();
renderAll();
</script>
</body>
</html>
