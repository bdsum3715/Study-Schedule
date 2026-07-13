<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover"/>
<title>Summer Foundations — Light Tracker</title>
<style>
  *{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
  body{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif;background:#F6F5F1;min-height:100vh;padding-bottom:50px;color:#2B2A28;}

  .header{background:#2F5D50;color:#F6F5F1;padding:22px 18px 20px;}
  .eyebrow{font-size:10px;font-weight:700;letter-spacing:2px;text-transform:uppercase;opacity:0.65;margin-bottom:4px;}
  .header h1{font-size:21px;font-weight:800;margin-bottom:4px;}
  .header p{font-size:12.5px;opacity:0.8;line-height:1.5;}
  .stat-row{display:flex;gap:10px;margin-top:16px;}
  .stat{flex:1;background:rgba(255,255,255,0.1);border-radius:12px;padding:10px 12px;}
  .stat-num{font-size:18px;font-weight:800;}
  .stat-label{font-size:9.5px;opacity:0.75;text-transform:uppercase;letter-spacing:0.5px;margin-top:1px;}
  .progress-track{background:rgba(255,255,255,0.2);border-radius:20px;height:7px;margin-top:14px;overflow:hidden;}
  .progress-fill{background:#E8B84B;border-radius:20px;height:7px;transition:width .3s;}

  .banner{margin:16px 16px 14px;background:white;border-radius:14px;padding:16px;box-shadow:0 1px 6px rgba(43,42,40,0.08);border-left:4px solid #2F5D50;}
  .banner.rest{border-left-color:#94A3B8;background:#FAFAF8;}
  .banner.light{border-left-color:#E8B84B;background:#FFFBEF;}
  .banner-eyebrow{font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:1px;color:#2F5D50;margin-bottom:4px;}
  .banner.rest .banner-eyebrow{color:#64748B;}
  .banner.light .banner-eyebrow{color:#A8791F;}
  .banner-title{font-size:15px;font-weight:800;margin-bottom:8px;}
  .banner-time{display:inline-block;font-size:11px;font-weight:700;background:#EAF2EF;color:#2F5D50;padding:3px 9px;border-radius:8px;margin-bottom:10px;}
  .banner.light .banner-time{background:#FBF0D6;color:#A8791F;}

  .rules{margin:0 16px 16px;background:white;border-radius:14px;padding:14px 16px;box-shadow:0 1px 6px rgba(43,42,40,0.06);}
  .rules-title{font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:1px;color:#94A3B8;margin-bottom:8px;}
  .rule{display:flex;gap:8px;font-size:12.5px;color:#43423F;line-height:1.5;padding:3px 0;}
  .rule b{color:#2F5D50;}

  .week{margin:0 16px 14px;}
  .week-head{display:flex;justify-content:space-between;align-items:baseline;padding:0 2px 8px;}
  .week-title{font-size:13px;font-weight:800;color:#2B2A28;}
  .week-sub{font-size:11px;color:#94A3B8;}

  .day-card{background:white;border-radius:12px;margin-bottom:8px;box-shadow:0 1px 4px rgba(43,42,40,0.06);overflow:hidden;border:1.5px solid transparent;}
  .day-card.is-today{border-color:#2F5D50;}
  .day-card.rest-day{opacity:0.7;}
  .day-top{display:flex;align-items:center;padding:12px 14px;cursor:pointer;gap:10px;}
  .day-circle{width:22px;height:22px;border-radius:50%;border:2px solid #D8D6CF;flex-shrink:0;display:flex;align-items:center;justify-content:center;}
  .day-circle.done{background:#2F5D50;border-color:#2F5D50;}
  .day-circle.done span{color:white;font-size:11px;font-weight:800;}
  .day-info{flex:1;min-width:0;}
  .day-date{font-size:10.5px;font-weight:700;color:#94A3B8;text-transform:uppercase;letter-spacing:0.4px;}
  .day-topic{font-size:13px;font-weight:700;color:#2B2A28;margin-top:1px;}
  .today-tag{display:inline-block;background:#2F5D50;color:white;font-size:8.5px;font-weight:700;padding:2px 6px;border-radius:5px;margin-left:6px;letter-spacing:.3px;vertical-align:middle;}
  .day-count{font-size:11px;font-weight:700;color:#2F5D50;flex-shrink:0;}
  .day-arrow{color:#C7C5BE;font-size:12px;flex-shrink:0;}

  .tasks{padding:0 14px 12px 46px;}
  .task{display:flex;gap:9px;align-items:flex-start;padding:6px 0;cursor:pointer;}
  .task-box{width:18px;height:18px;border-radius:5px;border:2px solid #D8D6CF;flex-shrink:0;margin-top:1px;display:flex;align-items:center;justify-content:center;}
  .task-box.done{background:#2F5D50;border-color:#2F5D50;}
  .task-box.done span{color:white;font-size:10px;font-weight:800;}
  .task-text{font-size:12.5px;color:#43423F;line-height:1.45;}
  .task-text.done{color:#B4B2AB;text-decoration:line-through;}

  .footer-note{margin:18px 16px 0;text-align:center;font-size:11.5px;color:#94A3B8;line-height:1.6;padding:0 10px;}
</style>
</head>
<body>

<div class="header">
  <div class="eyebrow">Jul 13 → Sep 27 · Micro + Pharm Only · Uni Starts Sep 28</div>
  <h1>Foundations Tracker — Microbiology & Pharmacology</h1>
  <p>~15–18 min video (est.) + Anki reviews, most days. Anki reviews first (capped 15–20 new/day), one Sketchy chunk, done. Video times are estimates only — Sketchy publishes module totals, not per-video length, and individual videos run roughly 6–12 min each, so some days will run a bit shorter or longer than shown. Physiology and Pathophysiology are left for lecture — a First Aid page or single Bootcamp video is your on-demand backup if a lecture assumes physio you don't have solid, not a summer queue. Built to leave real room for the gym, Spanish, the move, and everything else.</p>
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
  <div class="rule">✅ <span><b>New cards capped at 15–20/day</b> — only from what you actually watched today.</span></div>
  <div class="rule">✅ <span><b>Missed a day? Skip it.</b> No make-up sessions, no guilt.</span></div>
  <div class="rule">✅ <span>During internship weeks: <b>Anki reviews only</b>, nothing new expected.</span></div>
  <div class="rule">✅ <span>1 rest day built in every week — reviews only, if you feel like it.</span></div>
</div>

<div id="weeks-container"></div>

<div class="footer-note">Video times shown are estimates (module average, since Sketchy doesn't publish per-video length) — expect some day-to-day variance since individual videos run ~6–12 min each. Anki review time is separate and additive on top of the video estimate. Micro + Pharm together are ~46 hours of video. Physio/Path/Pathophys are taught properly starting Sep 28 — this tracker isn't trying to cover them.</div>

<script>
// ═══════════════════════════════════════════════════════════
// CONFIG — edit these date ranges if your actual dates differ
// ═══════════════════════════════════════════════════════════
const START_DATE = '2026-07-13';
const END_DATE   = '2026-09-27'; // Uni starts Sep 28 — this is the hard boundary for solo pre-study

// Light-mode windows (internships / travel): Anki reviews only, no new content expected
const LIGHT_WINDOWS = [
  { start:'2026-07-14', end:'2026-07-26', label:'✈️ Travel' },
  { start:'2026-08-10', end:'2026-08-24', label:'🏥 Internship 1' },
  { start:'2026-09-06', end:'2026-09-24', label:'🏥 Internship 2' },
];

// Real Sketchy modules — official names, video counts, and total runtimes,
// pulled directly from Sketchy's own 6-week guide, converted to 1x speed.
// Micro + Pharm only — self-contained, fact-based, doesn't need a professor's
// scaffolding, so it's the best fit for solo summer study alongside everything
// else going on (internships, gym/rehab, Spanish, moving).
// Physiology/Pathology/Pathophysiology are left for lecture, where they're
// taught properly — if a specific lecture assumes physio you don't have solid,
// use First Aid or a single Bootcamp physio video as a targeted reference,
// not a full pre-study queue.
const SKETCHY_MODULES = [
  { name:"Sketchy Micro — Bacteria (Part 1)",                          videos:19, totalMins:75  },
  { name:"Sketchy Micro — Bacteria (Part 2)",                          videos:34, totalMins:225 },
  { name:"Sketchy Pharm — Antimicrobials",                             videos:28, totalMins:300 },
  { name:"Sketchy Micro — Viruses: RNA Viruses",                       videos:21, totalMins:188 },
  { name:"Sketchy Micro — Viruses: DNA Viruses",                       videos:13, totalMins:113 },
  { name:"Sketchy Micro — Fungi & Parasites",                          videos:29, totalMins:263 },
  { name:"Sketchy Pharm — Autonomic Drugs, Cardio & Renal",             videos:21, totalMins:450 },
  { name:"Sketchy Pharm — Blood & Inflammation, Smooth Muscle",        videos:17, totalMins:356 },
  { name:"Sketchy Pharm — GI & Endocrine",                             videos:15, totalMins:263 },
  { name:"Sketchy Pharm — Neuro/Psych",                                videos:25, totalMins:375 },
  { name:"Sketchy Pharm — Antineoplastics & Pharmacology Foundations", videos:23, totalMins:300 },
];

// Auto-chunk each module into video portions targeting ~18 min of video/day.
// NOTE: Sketchy only publishes each module's total runtime and video count,
// not each individual video's length — and individual videos commonly run
// 6–12 min each. So chunk size is an ESTIMATE based on the module average,
// not a guarantee — some days will run a bit shorter, some longer, depending
// which specific videos land in that chunk. Sizing is floored (rounded down,
// minimum 1) rather than rounded up, to bias toward the shorter side instead
// of risking overshoot on a run of longer videos.
const TARGET_MINS_PER_DAY = 18;
function chunkModules(modules){
  const chunks=[];
  modules.forEach(mod=>{
    const minsPerVideo = mod.totalMins / mod.videos;
    const videosPerChunk = Math.max(1, Math.floor(TARGET_MINS_PER_DAY / minsPerVideo));
    let start=1;
    while(start<=mod.videos){
      const end=Math.min(mod.videos, start+videosPerChunk-1);
      const mins=Math.round((end-start+1)*minsPerVideo);
      const rangeLabel = start===end ? `video ${start} of ${mod.videos}` : `videos ${start}–${end} of ${mod.videos}`;
      chunks.push({ t:`${mod.name} — ${rangeLabel}`, mins });
      start=end+1;
    }
  });
  return chunks;
}
const TOPIC_POOL = chunkModules(SKETCHY_MODULES);

// Builds a searchable keyword from the module name (strips the
// "Sketchy Micro/Pharm —" prefix) so each day's Anki step is copy-pasteable.
function searchKeyword(moduleName){
  return moduleName.replace(/^Sketchy (Micro|Pharm) — /,'').replace(/\(Part \d\)/,'').trim();
}

function buildTasks(topic){
  const keyword = searchKeyword(topic.t.split(' — videos')[0].split(' — video ')[0]);
  return [
    "Anki: clear all due reviews first — new cards wait until this is done",
    `Watch: ${topic.t}`,
    `Anki Browse: search  tag:*Sketchy* ${keyword} is:suspended  — select all, right-click → Toggle Suspend`,
    "If that search returns nothing, drop the tag: prefix and search just the keyword with is:suspended",
    "Anki: review the newly unsuspended cards once — if it's more than ~20, use Custom Study to cap today's new cards",
  ];
}

const LIGHT_TASKS = ["Anki: due reviews only — no new cards today"];

// ═══════════════════════════════════════════════════════════
// BUILD DAY LIST
// ═══════════════════════════════════════════════════════════
function addDays(dateStr,n){ const d=new Date(dateStr+'T12:00:00'); d.setDate(d.getDate()+n); return d.toISOString().split('T')[0]; }
function dowIndex(dateStr){ return new Date(dateStr+'T12:00:00').getDay(); } // 0=Sun
function fmtShort(dateStr){ const d=new Date(dateStr+'T12:00:00'); return ['Sun','Mon','Tue','Wed','Thu','Fri','Sat'][d.getDay()]+' '+['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'][d.getMonth()]+' '+d.getDate(); }
function fmtLong(dateStr){ const d=new Date(dateStr+'T12:00:00'); return ['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'][d.getDay()]+', '+['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'][d.getMonth()]+' '+d.getDate(); }
function isLight(dateStr){ return LIGHT_WINDOWS.find(w=>dateStr>=w.start&&dateStr<=w.end); }
function todayISO(){ const t=new Date(); return t.getFullYear()+'-'+String(t.getMonth()+1).padStart(2,'0')+'-'+String(t.getDate()).padStart(2,'0'); }

let DAYS=[];
(function build(){
  let d=START_DATE, topicIdx=0;
  while(d<=END_DATE){
    const light=isLight(d);
    const isSunday=dowIndex(d)===0;
    let type='study', tasks=[], label='';
    if(light){ type='light'; label=light.label; tasks=LIGHT_TASKS.slice(); }
    else if(isSunday){ type='rest'; label='Rest day'; tasks=["Anki: quick review only, if you feel like it — otherwise fully off"]; }
    else{ const topic=TOPIC_POOL[topicIdx % TOPIC_POOL.length]; topicIdx++; type='study'; label=topic.t; tasks=buildTasks(topic); }
    DAYS.push({ id:'d_'+d, date:d, type, label, tasks, mins: type==='study'?(TOPIC_POOL[(topicIdx-1+TOPIC_POOL.length)%TOPIC_POOL.length].mins||30):(type==='light'?10:5) });
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
