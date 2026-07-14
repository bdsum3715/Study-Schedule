<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover"/>
<title>Foundations Tracker</title>
<style>
  *{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
  body{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif;background:#F7F4EE;min-height:100vh;padding-bottom:56px;color:#2A2825;}
  h1,.serif{font-family:ui-serif,Georgia,"Times New Roman",serif;}

  .header{background:linear-gradient(160deg,#1F3A32 0%,#16281F 100%);color:#F7F4EE;padding:26px 20px 24px;border-radius:0 0 22px 22px;}
  .eyebrow{font-size:10px;font-weight:700;letter-spacing:2.2px;text-transform:uppercase;opacity:0.6;margin-bottom:6px;}
  .header h1{font-size:23px;font-weight:600;margin-bottom:8px;letter-spacing:.2px;}
  .header p{font-size:12.5px;opacity:0.82;line-height:1.55;}
  .stat-row{display:flex;gap:10px;margin-top:18px;}
  .stat{flex:1;background:rgba(255,255,255,0.08);border:1px solid rgba(255,255,255,0.08);border-radius:13px;padding:11px 12px;}
  .stat-num{font-size:19px;font-weight:700;font-family:ui-serif,Georgia,serif;}
  .stat-label{font-size:9.5px;opacity:0.7;text-transform:uppercase;letter-spacing:0.6px;margin-top:2px;}
  .progress-track{background:rgba(255,255,255,0.15);border-radius:20px;height:6px;margin-top:16px;overflow:hidden;}
  .progress-fill{background:linear-gradient(90deg,#D4A537,#E8C468);border-radius:20px;height:6px;transition:width .3s;}

  .banner{margin:18px 16px 14px;background:white;border-radius:16px;padding:17px 18px;box-shadow:0 4px 18px rgba(31,58,50,0.07);border-left:4px solid #1F3A32;}
  .banner.rest{border-left-color:#B8B4A9;background:#FBFAF7;}
  .banner.light{border-left-color:#D4A537;background:#FEFAF0;}
  .banner-eyebrow{font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:1.2px;color:#1F3A32;margin-bottom:5px;}
  .banner.rest .banner-eyebrow{color:#8B8778;}
  .banner.light .banner-eyebrow{color:#A8791F;}
  .banner-title{font-size:15.5px;font-weight:700;margin-bottom:9px;font-family:ui-serif,Georgia,serif;}
  .banner-time{display:inline-block;font-size:11px;font-weight:700;background:#EDF2EE;color:#1F3A32;padding:4px 10px;border-radius:8px;margin-bottom:10px;}
  .banner.light .banner-time{background:#FBF0D6;color:#A8791F;}

  .rules{margin:0 16px 18px;background:white;border-radius:16px;padding:16px 18px;box-shadow:0 2px 10px rgba(31,58,50,0.05);}
  .rules-title{font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:1.2px;color:#A39E8F;margin-bottom:10px;}
  .rule{display:flex;gap:9px;font-size:12.5px;color:#48453F;line-height:1.55;padding:4px 0;}
  .rule b{color:#1F3A32;}

  .week{margin:0 16px 16px;}
  .week-head{display:flex;justify-content:space-between;align-items:baseline;padding:0 3px 9px;}
  .week-title{font-size:13.5px;font-weight:700;color:#2A2825;font-family:ui-serif,Georgia,serif;}
  .week-sub{font-size:11px;color:#A39E8F;}

  .day-card{background:white;border-radius:13px;margin-bottom:9px;box-shadow:0 2px 8px rgba(31,58,50,0.06);overflow:hidden;border:1.5px solid transparent;transition:box-shadow .15s;}
  .day-card.is-today{border-color:#1F3A32;box-shadow:0 4px 14px rgba(31,58,50,0.14);}
  .day-card.rest-day{opacity:0.65;}
  .day-top{display:flex;align-items:center;padding:13px 15px;cursor:pointer;gap:11px;}
  .day-circle{width:23px;height:23px;border-radius:50%;border:2px solid #E1DDD2;flex-shrink:0;display:flex;align-items:center;justify-content:center;transition:all .15s;}
  .day-circle.done{background:#1F3A32;border-color:#1F3A32;}
  .day-circle.done span{color:white;font-size:11px;font-weight:700;}
  .day-info{flex:1;min-width:0;}
  .day-date{font-size:10.5px;font-weight:700;color:#A39E8F;text-transform:uppercase;letter-spacing:0.5px;}
  .day-topic{font-size:13px;font-weight:600;color:#2A2825;margin-top:2px;}
  .today-tag{display:inline-block;background:#D4A537;color:#1F3A32;font-size:8.5px;font-weight:800;padding:2px 7px;border-radius:5px;margin-left:6px;letter-spacing:.3px;vertical-align:middle;}
  .day-count{font-size:11px;font-weight:700;color:#1F3A32;flex-shrink:0;}
  .day-arrow{color:#D2CDBF;font-size:12px;flex-shrink:0;}

  .tasks{padding:2px 15px 14px 48px;}
  .task{display:flex;gap:10px;align-items:flex-start;padding:7px 0;cursor:pointer;}
  .task-box{width:19px;height:19px;border-radius:6px;border:2px solid #E1DDD2;flex-shrink:0;margin-top:1px;display:flex;align-items:center;justify-content:center;transition:all .15s;}
  .task-box.done{background:#1F3A32;border-color:#1F3A32;}
  .task-box.done span{color:white;font-size:10px;font-weight:700;}
  .task-text{font-size:12.5px;color:#48453F;line-height:1.5;}
  .task-text.done{color:#C2BEB1;text-decoration:line-through;}

  .footer-note{margin:22px 16px 0;text-align:center;font-size:11.5px;color:#A39E8F;line-height:1.65;padding:0 12px;}
</style>
</head>
<body>

<div class="header">
  <div class="eyebrow">Jul 27 → Sep 27 · Starts After Vacation · Uni Starts Sep 28</div>
  <h1>Foundations — Microbiology &amp; Pharmacology</h1>
  <p>Starts right after your travel — no pre-vacation days to worry about. Microbiology is one-shot (semester 5 only, no repeat) so it's fully in the must-finish set, alongside the Pharm modules confirmed or likely tied to semester 5 (Antimicrobials, Autonomic/CV/Renal, Blood/Inflammation, GI/Endocrine, Neuro/Psych). Antineoplastics & Pharmacology Foundations is held as <b>stretch</b> content — assumed semester 6, correct me if that's wrong too. Must-finish pace: ~1 hr 44 min/day across 25 real study days. Anki first (capped ~20 new/day), internship days stay fully protected.</p>
  <div class="stat-row">
    <div class="stat"><div class="stat-num" id="streak-num">0</div><div class="stat-label">Day streak</div></div>
    <div class="stat"><div class="stat-num" id="done-num">0</div><div class="stat-label">Days done</div></div>
    <div class="stat"><div class="stat-num" id="pct-num">0%</div><div class="stat-label">Complete</div></div>
  </div>
  <div class="progress-track"><div class="progress-fill" id="progress-fill" style="width:0%"></div></div>
</div>

<div class="banner" id="today-banner"></div>

<div class="rules">
  <div class="rules-title">The only rules</div>
  <div class="rule">✅ <span><b>Anki reviews always first</b>, before anything new.</span></div>
  <div class="rule">✅ <span><b>New cards capped at ~20/day</b> — only from what you actually watched today.</span></div>
  <div class="rule">✅ <span><b>Missed a day? Skip it.</b> No make-up sessions, no guilt.</span></div>
  <div class="rule">✅ <span>During internship weeks: <b>Anki reviews only</b>, nothing new expected.</span></div>
  <div class="rule">✅ <span>1 rest day built in every week — reviews only, if you feel like it.</span></div>
</div>

<div id="weeks-container"></div>

<div class="footer-note">Must-finish set (Micro + semester-5 Pharm, including Neuro/Psych) ≈ 43.5 hours ÷ 25 real study days (starting Jul 27, after travel) ≈ 1 hr 44 min/day. Antineoplastics & Pharmacology Foundations stays queued as bonus-only, assumed semester 6 — flag it if that's wrong. Internship days stay fully protected at reviews-only.</div>


<script>
// ═══════════════════════════════════════════════════════════
// CONFIG — edit these date ranges if your actual dates differ
// ═══════════════════════════════════════════════════════════
const START_DATE = '2026-07-27'; // starts right after travel — no pre-vacation days
const END_DATE   = '2026-09-27'; // Uni starts Sep 28 — hard boundary for solo pre-study

// Light-mode windows (internships): Anki reviews only, no new content — protected, never touched
const LIGHT_WINDOWS = [
  { start:'2026-08-10', end:'2026-08-24', label:'🏥 Internship 1' },
  { start:'2026-09-06', end:'2026-09-24', label:'🏥 Internship 2' },
];

// ── Date helpers (defined early — needed before pacing math) ──
function addDays(dateStr,n){ const d=new Date(dateStr+'T12:00:00'); d.setDate(d.getDate()+n); return d.toISOString().split('T')[0]; }
function dowIndex(dateStr){ return new Date(dateStr+'T12:00:00').getDay(); } // 0=Sun
function fmtShort(dateStr){ const d=new Date(dateStr+'T12:00:00'); return ['Sun','Mon','Tue','Wed','Thu','Fri','Sat'][d.getDay()]+' '+['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'][d.getMonth()]+' '+d.getDate(); }
function fmtLong(dateStr){ const d=new Date(dateStr+'T12:00:00'); return ['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'][d.getDay()]+', '+['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'][d.getMonth()]+' '+d.getDate(); }
function isLight(dateStr){ return LIGHT_WINDOWS.find(w=>dateStr>=w.start&&dateStr<=w.end); }
function todayISO(){ const t=new Date(); return t.getFullYear()+'-'+String(t.getMonth()+1).padStart(2,'0')+'-'+String(t.getDate()).padStart(2,'0'); }

// Count real active study days (not light, not Sunday) between START_DATE and END_DATE.
// This is the actual number of days available to get through all the content.
let ACTIVE_STUDY_DAYS = 0;
(function countActiveDays(){
  let d=START_DATE;
  while(d<=END_DATE){
    if(!isLight(d) && dowIndex(d)!==0) ACTIVE_STUDY_DAYS++;
    d=addDays(d,1);
  }
})();

// Real Sketchy modules — official names, video counts, and total runtimes,
// pulled directly from Sketchy's own 6-week guide, converted to 1x speed.
// Reprioritized based on curriculum structure: Microbiology is one-shot
// (semester 5 only, no repeat) so it's fully in the must-finish set. Pharm
// spans semesters 5 AND 6 — meaning the curriculum itself already gives you
// two passes and natural spacing — so Neuro/Psych Pharm and Antineoplastics
// (assumed semester 6 content; correct this if wrong) are marked as stretch:
// worth covering if there's time, but not something to force this summer.
const SKETCHY_MODULES = [
  { name:"Sketchy Micro — Bacteria (Part 1)",                          videos:19, totalMins:75,  stretch:false },
  { name:"Sketchy Micro — Bacteria (Part 2)",                          videos:34, totalMins:225, stretch:false },
  { name:"Sketchy Pharm — Antimicrobials",                             videos:28, totalMins:300, stretch:false },
  { name:"Sketchy Micro — Viruses: RNA Viruses",                       videos:21, totalMins:188, stretch:false },
  { name:"Sketchy Micro — Viruses: DNA Viruses",                       videos:13, totalMins:113, stretch:false },
  { name:"Sketchy Micro — Fungi & Parasites",                          videos:29, totalMins:263, stretch:false },
  { name:"Sketchy Pharm — Autonomic Drugs, Cardio & Renal",            videos:21, totalMins:450, stretch:false },
  { name:"Sketchy Pharm — Blood & Inflammation, Smooth Muscle",        videos:17, totalMins:356, stretch:false },
  { name:"Sketchy Pharm — GI & Endocrine",                             videos:15, totalMins:263, stretch:false },
  { name:"Sketchy Pharm — Neuro/Psych",                                videos:25, totalMins:375, stretch:false },
  // — Stretch: assumed semester 6 Pharm, gets natural repetition later —
  { name:"Sketchy Pharm — Antineoplastics & Pharmacology Foundations", videos:23, totalMins:300, stretch:true  },
];
const PRIORITY_MODULES = SKETCHY_MODULES.filter(m=>!m.stretch);
const STRETCH_MODULES = SKETCHY_MODULES.filter(m=>m.stretch);
const TOTAL_CONTENT_MINS = SKETCHY_MODULES.reduce((s,m)=>s+m.totalMins,0);
const TOTAL_CONTENT_VIDEOS = SKETCHY_MODULES.reduce((s,m)=>s+m.videos,0);
const PRIORITY_MINS = PRIORITY_MODULES.reduce((s,m)=>s+m.totalMins,0);

// Required daily pace to finish the MUST-FINISH set (Micro + semester-5
// Pharm) by Sep 27 — this is the number that matters, not the pace for
// everything including stretch content.
const REQUIRED_MINS_PER_DAY = Math.round(PRIORITY_MINS / ACTIVE_STUDY_DAYS);

// ── Build the ordered video list: priority modules first, stretch modules
// appended after. Days are filled at REQUIRED_MINS_PER_DAY (fixed rate) —
// this naturally exhausts the priority set right around Sep 27, so stretch
// content only gets scheduled if there's real slack, never forced.
let FLAT_VIDEOS = [];
SKETCHY_MODULES.forEach(mod=>{
  const mpv = mod.totalMins / mod.videos;
  for(let i=1;i<=mod.videos;i++){
    FLAT_VIDEOS.push({ module:mod.name, videoNum:i, totalVideos:mod.videos, mins:mpv, stretch:mod.stretch });
  }
});

function buildDayBins(items, M, ratePerDay){
  const bins=[]; let idx=0;
  for(let b=0; b<M; b++){
    const bin=[]; let cum=0;
    while(idx<items.length && (cum+items[idx].mins <= ratePerDay || bin.length===0)){
      cum += items[idx].mins;
      bin.push(items[idx]);
      idx++;
    }
    bins.push(bin);
  }
  return bins; // any leftover stretch items past the last bin simply aren't scheduled — by design
}
const DAY_BINS = buildDayBins(FLAT_VIDEOS, ACTIVE_STUDY_DAYS, REQUIRED_MINS_PER_DAY);

// Turn a day's bin of individual videos into readable "Watch:" lines — one
// line per contiguous module range (a bin usually spans 1, occasionally 2
// modules right at a transition point).
function binToTopic(bin){
  if(!bin || bin.length===0) return null;
  const segments=[];
  let cur={ module:bin[0].module, start:bin[0].videoNum, end:bin[0].videoNum, totalVideos:bin[0].totalVideos };
  for(let i=1;i<bin.length;i++){
    const v=bin[i];
    if(v.module===cur.module && v.videoNum===cur.end+1){ cur.end=v.videoNum; }
    else{ segments.push(cur); cur={ module:v.module, start:v.videoNum, end:v.videoNum, totalVideos:v.totalVideos }; }
  }
  segments.push(cur);
  const mins = Math.round(bin.reduce((s,v)=>s+v.mins,0));
  const lines = segments.map(s=>{
    const range = s.start===s.end ? `video ${s.start} of ${s.totalVideos}` : `videos ${s.start}–${s.end} of ${s.totalVideos}`;
    return `${s.module} — ${range}`;
  });
  return { lines, mins, segments };
}
const TOPIC_POOL = DAY_BINS.map(binToTopic);

// Builds a searchable keyword from a module name (strips the
// "Sketchy Micro/Pharm —" prefix) so each day's Anki step is copy-pasteable.
function searchKeyword(moduleName){
  return moduleName.replace(/^Sketchy (Micro|Pharm) — /,'').replace(/\(Part \d\)/,'').trim();
}

function buildTasks(topic){
  const tasks=["Anki: clear all due reviews first — new cards wait until this is done"];
  topic.lines.forEach(line=>tasks.push(`Watch: ${line}`));
  topic.segments.forEach(seg=>{
    const kw=searchKeyword(seg.module);
    tasks.push(`Anki Browse: search  tag:*Sketchy* ${kw} is:suspended  — select all, right-click → Toggle Suspend`);
  });
  tasks.push("If a search returns nothing, drop the tag: prefix and search just the keyword with is:suspended");
  tasks.push("Anki: review the newly unsuspended cards once — if it's a lot, use Custom Study to cap today's new cards");
  return tasks;
}

const LIGHT_TASKS = ["Anki: due reviews only — no new cards today"];

// ═══════════════════════════════════════════════════════════
// BUILD DAY LIST
// ═══════════════════════════════════════════════════════════
let DAYS=[];
(function build(){
  let d=START_DATE, topicIdx=0;
  while(d<=END_DATE){
    const light=isLight(d);
    const isSunday=dowIndex(d)===0;
    let type='study', tasks=[], label='';
    if(light){ type='light'; label=light.label; tasks=LIGHT_TASKS.slice(); }
    else if(isSunday){ type='rest'; label='Rest day'; tasks=["Anki: quick review only, if you feel like it — otherwise fully off"]; }
    else{
      const topic=TOPIC_POOL[topicIdx];
      topicIdx++;
      if(topic){ type='study'; label=topic.lines[0]+(topic.lines.length>1?` (+${topic.lines.length-1} more)`:''); tasks=buildTasks(topic); }
      else{ type='study'; label='Content complete — bonus review day'; tasks=["Anki: due reviews","Free choice: rewatch a weak module, or get ahead if you want"]; }
    }
    DAYS.push({ id:'d_'+d, date:d, type, label, tasks, mins: type==='study'?(TOPIC_POOL[topicIdx-1]?.mins||0):(type==='light'?10:5) });
    d=addDays(d,1);
  }
})();

// ═══════════════════════════════════════════════════════════
// STATE + PERSISTENCE (window.storage, falls back to memory)
// ═══════════════════════════════════════════════════════════
let checked={};
async function loadState(){
  try{
    const res = await window.storage.get('light-tracker-checked', false);
    if(res && res.value) checked = JSON.parse(res.value);
  }catch(e){ /* no saved state yet */ }
}
async function saveState(){
  try{ await window.storage.set('light-tracker-checked', JSON.stringify(checked), false); }catch(e){}
}

function dayDone(day){ return day.tasks.filter((_,i)=>checked[day.id+'_'+i]).length; }
function allTaskIds(){ return DAYS.flatMap(d=>d.tasks.map((_,i)=>d.id+'_'+i)); }

function computeStreak(){
  const today=todayISO();
  const past=DAYS.filter(d=>d.date<=today).sort((a,b)=>b.date.localeCompare(a.date));
  let streak=0;
  for(const day of past){
    const ankingDone = checked[day.id+'_0'];
    if(ankingDone) streak++;
    else if(day.date===today) continue;
    else break;
  }
  return streak;
}

// ═══════════════════════════════════════════════════════════
// RENDER
// ═══════════════════════════════════════════════════════════
function renderHeader(){
  const ids=allTaskIds(); const done=ids.filter(id=>checked[id]).length;
  const pct = ids.length ? Math.round(done/ids.length*100) : 0;
  document.getElementById('progress-fill').style.width=pct+'%';
  document.getElementById('pct-num').textContent=pct+'%';
  document.getElementById('streak-num').textContent=computeStreak();
  const doneDays=DAYS.filter(d=>dayDone(d)===d.tasks.length && d.tasks.length>0).length;
  document.getElementById('done-num').textContent=doneDays;
}

function renderBanner(){
  const today=todayISO();
  const day=DAYS.find(d=>d.date===today);
  const el=document.getElementById('today-banner');
  if(!day){
    el.className='banner';
    el.innerHTML=`<div class="banner-eyebrow">Today</div><div class="banner-title">Outside the plan window</div>`;
    return;
  }
  const cls = day.type==='light' ? 'light' : (day.type==='rest' ? 'rest' : '');
  el.className='banner '+cls;
  const eyebrowText = day.type==='light' ? light_eyebrow(day) : day.type==='rest' ? 'Today · Rest day' : 'Today';
  el.innerHTML=`
    <div class="banner-eyebrow">${eyebrowText}</div>
    <div class="banner-title">${day.label}</div>
    ${day.mins?`<div class="banner-time">⏱ ~${day.mins} min video (est.) + Anki</div>`:''}
    <div style="font-size:12px;color:#64748B">${dayDone(day)}/${day.tasks.length} done today</div>`;
}
function light_eyebrow(day){ return 'Today · '+day.label; }

function renderWeeks(){
  const today=todayISO();
  const container=document.getElementById('weeks-container');
  let html='';
  // group by week (Sun–Sat)
  let weekStart=null, weekDays=[], weekNum=1, out=[];
  DAYS.forEach(day=>{
    if(dowIndex(day.date)===0 || weekDays.length===0 && !weekStart){
      if(weekDays.length){ out.push(weekDays); weekDays=[]; }
    }
    weekDays.push(day);
  });
  if(weekDays.length) out.push(weekDays);
  // simpler: just chunk every 7 starting from START_DATE's week
  out=[]; let chunk=[];
  DAYS.forEach((day,i)=>{
    chunk.push(day);
    if(dowIndex(day.date)===6 || i===DAYS.length-1){ out.push(chunk); chunk=[]; }
  });

  out.forEach((week,wi)=>{
    const rangeLabel = fmtShort(week[0].date)+' – '+fmtShort(week[week.length-1].date);
    html+=`<div class="week"><div class="week-head"><div class="week-title">Week ${wi+1}</div><div class="week-sub">${rangeLabel}</div></div>`;
    week.forEach(day=>{
      const isToday=day.date===today;
      const dd=dayDone(day), dt=day.tasks.length, complete=dd===dt&&dt>0;
      html+=`<div class="day-card${isToday?' is-today':''}${day.type==='rest'?' rest-day':''}" id="card-${day.id}">
        <div class="day-top" onclick="toggleOpen('${day.id}')">
          <div class="day-circle${complete?' done':''}" id="circ-${day.id}">${complete?'<span>✓</span>':''}</div>
          <div class="day-info">
            <div class="day-date">${fmtShort(day.date)}${isToday?'<span class="today-tag">TODAY</span>':''}</div>
            <div class="day-topic">${day.label}</div>
          </div>
          <div class="day-count" id="cnt-${day.id}">${dd}/${dt}</div>
          <div class="day-arrow" id="arrow-${day.id}">▼</div>
        </div>
        <div class="tasks" id="tasks-${day.id}" style="display:none">
          ${day.tasks.map((task,i)=>{
            const tid=day.id+'_'+i, done=!!checked[tid];
            return `<div class="task" onclick="toggleTask('${tid}','${day.id}')">
              <div class="task-box${done?' done':''}" id="box-${tid}">${done?'<span>✓</span>':''}</div>
              <span class="task-text${done?' done':''}" id="txt-${tid}">${task}</span>
            </div>`;
          }).join('')}
        </div>
      </div>`;
    });
    html+=`</div>`;
  });
  container.innerHTML=html;
}

let openDayId=null;
function toggleOpen(dayId){
  const wasOpen = openDayId===dayId;
  if(openDayId){
    const prevTasks=document.getElementById('tasks-'+openDayId);
    const prevArrow=document.getElementById('arrow-'+openDayId);
    if(prevTasks) prevTasks.style.display='none';
    if(prevArrow) prevArrow.textContent='▼';
  }
  openDayId = wasOpen ? null : dayId;
  if(openDayId){
    const t=document.getElementById('tasks-'+openDayId), a=document.getElementById('arrow-'+openDayId);
    if(t) t.style.display='block';
    if(a) a.textContent='▲';
    setTimeout(()=>{ document.getElementById('card-'+openDayId)?.scrollIntoView({behavior:'smooth',block:'center'}); },50);
  }
}

async function toggleTask(tid,dayId){
  checked[tid]=!checked[tid];
  await saveState();
  const box=document.getElementById('box-'+tid), txt=document.getElementById('txt-'+tid);
  if(box){ box.className='task-box'+(checked[tid]?' done':''); box.innerHTML=checked[tid]?'<span>✓</span>':''; }
  if(txt){ txt.className='task-text'+(checked[tid]?' done':''); }

  const day=DAYS.find(d=>d.id===dayId);
  if(day){
    const dd=dayDone(day), dt=day.tasks.length, complete=dd===dt&&dt>0;
    const circ=document.getElementById('circ-'+dayId), cnt=document.getElementById('cnt-'+dayId);
    if(circ){ circ.className='day-circle'+(complete?' done':''); circ.innerHTML=complete?'<span>✓</span>':''; }
    if(cnt) cnt.textContent=dd+'/'+dt;
  }
  renderHeader();
  renderBanner();
}

// ═══════════════════════════════════════════════════════════
// INIT
// ═══════════════════════════════════════════════════════════
(async function init(){
  await loadState();
  renderHeader();
  renderBanner();
  renderWeeks();
  // auto-open today
  const today=todayISO();
  const todayDay=DAYS.find(d=>d.date===today);
  if(todayDay) toggleOpen(todayDay.id);
})();
</script>
</body>
</html>
