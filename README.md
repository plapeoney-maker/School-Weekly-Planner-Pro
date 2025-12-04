<html ....>
<html lang="th">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
  <title>School Weekly Planner — Demo</title>
  <!-- Mali font -->
  <link href="https://fonts.googleapis.com/css2?family=Mali:wght@300;400;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg:#FFFDF9;
      --accent1:#C7B7FF; /* pastel purple */
      --accent2:#BFF3CC; /* pastel green */
      --accent-grad: linear-gradient(135deg,var(--accent1),var(--accent2));
      --card:#FFFFFF;
      --muted:#8F8F9A;
      --danger:#FF6B6B;
      --radius:18px; /* rounded-3xl-ish */
      --nav-height:70px;
    }
    html,body{height:100%;margin:0;font-family:"Mali",system-ui,-apple-system,Segoe UI,Roboto,"Helvetica Neue",Arial;
      background:
        radial-gradient(circle at 10% 10%, rgba(199,183,255,0.06) 0 10%, transparent 10%),
        radial-gradient(circle at 90% 90%, rgba(191,243,204,0.06) 0 10%, transparent 10%),
        var(--bg);
      color:#2b2b2b;
      -webkit-font-smoothing:antialiased;
    }
    /* dot-grid background like notebook */
    .dot-grid{
      background-image:
        radial-gradient(#EDE7FF 0.8px, transparent 0.8px);
      background-size:14px 14px;
      padding:18px;
    }
    /* App container */
    .app{
      max-width:480px;
      margin:12px auto;
      box-shadow: 0 8px 30px rgba(50,50,70,0.07);
      border-radius:26px;
      overflow:hidden;
      background:linear-gradient(180deg, rgba(255,255,255,0.98), rgba(255,255,255,0.9));
      min-height:calc(100vh - 24px);
      position:relative;
    }
    header.app-header{
      padding:18px;
      position:relative;
    }
    .app-top{
      display:flex;align-items:center;gap:12px;
    }
    .logo{
      width:56px;height:56px;border-radius:14px;
      background:var(--accent-grad);
      display:flex;align-items:center;justify-content:center;font-size:26px;
      color:white;box-shadow:0 6px 18px rgba(143,121,255,0.18);
      flex-shrink:0;
    }
    .title{
      font-size:18px;font-weight:700;margin:0;
    }
    .subtitle{font-size:12px;color:var(--muted);margin:2px 0 0;}
    main{padding:0 16px 96px;}
    /* Cards */
    .card{
      background:var(--card);
      border-radius:16px;
      padding:12px;
      margin:12px 0;
      box-shadow:0 6px 14px rgba(60,60,80,0.04);
      border:1px solid rgba(40,40,60,0.04);
    }
    .card-row{display:flex;gap:12px;align-items:center;}
    .small{
      font-size:12px;color:var(--muted);
    }
    /* Weekly calendar */
    .week{
      display:flex;gap:8px;overflow-x:auto;padding-bottom:6px;
    }
    .day{
      min-width:112px;background:linear-gradient(180deg,#FFF,#FBF9FF);
      border-radius:14px;padding:8px;border:1px dashed rgba(160,140,255,0.12);
    }
    .day .day-name{font-size:12px;color:var(--muted)}
    .day .date{font-weight:700;margin-top:6px}
    .activity{
      margin-top:8px;padding:8px;border-radius:12px;color:#fff;font-weight:600;font-size:12px;
      display:flex;flex-direction:column;gap:6px;
    }
    /* color tags */
    .tag-meeting{background:#9B8BFF}
    .tag-sport{background:#63D28B}
    .tag-academic{background:#FFB86B}
    .tag-ceremony{background:#6EC6FF}
    .tag-other{background:#C8C8D1}
    .small-muted{font-size:11px;color:#FAFAFA;opacity:0.85}
    /* Floating nav */
    nav.floating-nav{
      position:fixed;left:50%;transform:translateX(-50%);
      bottom:18px;height:var(--nav-height);width:92%;max-width:460px;
      display:flex;align-items:center;justify-content:space-around;
      background:linear-gradient(180deg, rgba(255,255,255,0.98), rgba(255,255,255,0.95));
      border-radius:34px;padding:10px 12px;
      box-shadow:0 18px 40px rgba(60,60,100,0.12);
      border:1px solid rgba(160,140,255,0.09);
      z-index:50;
      backdrop-filter: blur(6px);
    }
    .nav-btn{display:flex;flex-direction:column;align-items:center;font-size:12px;color:var(--muted);gap:4px}
    .nav-btn .ico{width:28px;height:28px;border-radius:10px;display:flex;align-items:center;justify-content:center;background:linear-gradient(180deg,rgba(255,255,255,0.6),transparent)}
    /* Login */
    .login-screen{padding:28px;display:flex;flex-direction:column;gap:12px;align-items:center;justify-content:center;height:60vh}
    .input{
      width:100%;padding:10px 12px;border-radius:14px;border:1px solid rgba(40,40,60,0.06);background:linear-gradient(180deg,#fff,#fffaf6);
      font-size:15px;box-shadow:inset 0 2px 6px rgba(0,0,0,0.02);
    }
    .btn{
      padding:10px 14px;border-radius:14px;border:none;background:var(--accent1);color:white;font-weight:700;
      box-shadow:0 8px 20px rgba(167,140,255,0.18);
    }
    /* modal / panel */
    .panel{
      position:fixed;inset:0;background:rgba(20,20,40,0.35);display:flex;align-items:flex-end;justify-content:center;padding:18px;
      z-index:60;backdrop-filter:blur(4px);
    }
    .sheet{width:100%;max-width:460px;background:var(--card);border-radius:18px;padding:16px;box-shadow:0 12px 28px rgba(0,0,0,0.18)}
    .close{float:right;border:none;background:none;font-size:18px;color:var(--muted)}
    /* washi tape */
    .washi{
      display:inline-block;padding:6px 12px;border-radius:8px;background:linear-gradient(90deg,#FFDEE9,#B5FFFC);
      transform:rotate(-6deg);box-shadow:0 6px 12px rgba(0,0,0,0.06);font-weight:700;font-size:12px;color:#3b3b3b;
    }
    /* tiny helpers */
    .muted{color:var(--muted)}
    .pill{padding:6px 8px;border-radius:999px;background:rgba(0,0,0,0.03);font-size:12px}
    .split{display:flex;gap:10px;align-items:center;justify-content:space-between}
    /* responsive for very small screens */
    @media (max-width:360px){
      .day{min-width:92px}
      .logo{width:48px;height:48px}
    }
    /* history badge */
    .badge{background:linear-gradient(90deg,#FFF2F5,#FFF);padding:6px 8px;border-radius:12px;font-size:12px;border:1px dashed rgba(200,120,255,0.08)}
    /* simple form styles inside sheet */
    label{font-size:13px;color:#444;margin-top:8px;display:block}
    textarea,input[type="text"],select{width:100%;padding:8px;border-radius:10px;border:1px solid rgba(30,30,40,0.06);margin-top:6px;font-size:14px}
    .list{display:flex;flex-direction:column;gap:8px}
    .small-note{font-size:12px;color:var(--muted);margin-top:6px}
  </style>
</head>
<body>
  <div class="app dot-grid" id="app">
    <!-- Header / Login area -->
    <header class="app-header">
      <div class="app-top">
        <div class="logo">📒</div>
        <div>
          <h1 class="title" id="appTitle">School Weekly Planner</h1>
          <div class="subtitle" id="welcomeSub">ยินดีต้อนรับ — กรุณาเข้าสู่ระบบ</div>
        </div>
      </div>
    </header>

    <main id="mainContent">
      <!-- Login Screen -->
      <section id="loginScreen" class="card login-screen" aria-hidden="false">
        <div style="text-align:center">
          <div class="washi">♪ สมุดจดโรงเรียน</div>
          <h2 style="margin:10px 0 0">เข้าสู่ระบบ</h2>
          <p class="small-muted small">ลองใช้ demo account: teacher1 / admin1</p>
        </div>
        <input class="input" id="inputUser" placeholder="ชื่อผู้ใช้ (teacher1 / admin1)" />
        <select id="roleSelect" class="input">
          <option value="teacher">ครู</option>
          <option value="admin">ผู้บริหาร</option>
        </select>
        <button class="btn" id="btnLogin">เข้าสู่ระบบ</button>
        <p class="small-muted small">แอปตัวอย่างเก็บข้อมูลโดย localStorage — ในระบบจริงใช้ API/DB</p>
      </section>

      <!-- Main Dashboard -->
      <section id="dashboard" style="display:none">
        <!-- Announcements top -->
        <div class="card split">
          <div>
            <div style="font-size:13px;color:#6F42C1;font-weight:800">📢 ประกาศโรงเรียน</div>
            <div id="topAnnouncement" class="small-muted small">ยังไม่มีประกาศล่าสุด</div>
          </div>
          <div class="pill" id="annCount">0</div>
        </div>

        <!-- Three cards row -->
        <div class="card">
          <div class="split">
            <div><strong>กิจกรรมวันนี้</strong><div class="small muted" id="todaySummary">-</div></div>
            <div><div class="badge" id="todayDate"></div></div>
          </div>
          <div style="margin-top:10px">
            <div class="week" id="weekView"></div>
          </div>
        </div>

        <div class="card">
          <div class="split"><div><strong>หน้าที่วันนี้</strong><div class="small muted">กดเพื่อยืนยันเมื่อเสร็จ ✨</div></div><div class="pill" id="todayDutiesCount">0</div></div>
          <div id="todayDuties" style="margin-top:10px"></div>
        </div>

        <div class="card">
          <div class="split"><div><strong>การแต่งกายวันนี้</strong><div class="small muted">อ้างอิงประกาศ</div></div><div class="pill" id="dressTag">—</div></div>
          <div style="margin-top:10px" id="dressGuide"></div>
        </div>

        <!-- Other quick actions -->
        <div class="card">
          <div style="display:flex;gap:10px;flex-wrap:wrap">
            <button class="btn" onclick="openPanel('assign')">มอบหมายหน้าที่</button>
            <button class="btn" style="background:var(--accent2);color:#134e2b" onclick="openPanel('announce')">ประกาศใหม่</button>
            <button class="btn" style="background:#FFD3B6;color:#6b3700" onclick="openPanel('reminder')">ตั้งเตือน</button>
          </div>
          <p class="small-note">คุณสามารถเปลี่ยนเป็นผู้บริหารโดยเลือก role เมื่อ login</p>
        </div>

        <!-- Recent activity & history -->
        <div class="card">
          <div class="split"><div><strong>ประวัติการยืนยันงาน</strong><div class="small muted">ล่าสุด 5 รายการ</div></div><div class="pill" id="historyCount">0</div></div>
          <div id="historyList" style="margin-top:8px"></div>
        </div>
      </section>

    </main>

    <!-- Floating nav -->
    <nav class="floating-nav" id="navBar" style="display:none">
      <div class="nav-btn" onclick="goTo('dashboardView')">
        <div class="ico">🏠</div>หน้าหลัก
      </div>
      <div class="nav-btn" onclick="goTo('calendarView')">
        <div class="ico">🗓️</div>ปฏิทิน
      </div>
      <div class="nav-btn" onclick="goTo('dutiesView')">
        <div class="ico">📝</div>หน้าที่
      </div>
      <div class="nav-btn" onclick="goTo('profileView')">
        <div class="ico">👩‍🏫</div>โปรไฟล์
      </div>
    </nav>

    <!-- Panels (modals) -->
    <div id="panelContainer"></div>

  </div>

<script>
/*
  Simple demo app logic
  Data model (simulated DB tables in localStorage):
  - users: [{id, username, name, role, avatar}]
  - activities: [{id,title,type,description,start, end, location,responsible}]
  - duties: [{id,title,type,assignedTo,userType,repeat,notes}]
  - reminders: [{id, userId, refType, refId, when, note}]
  - dressCodes: [{id,date,type,label,icon,color,notes}]
  - announcements: [{id, title, body, author, createdAt}]
  - dutyHistory: [{id,dutyId,userId,doneAt,notes}]
  - teachingSchedule: [{id, teacherId, subject, day, start, end, class}]
*/

const demoNow = new Date();
const state = {
  me: null,
  users: [],
  activities: [],
  duties: [],
  reminders: [],
  dressCodes: [],
  announcements: [],
  dutyHistory: [],
  teachingSchedule: []
};

function saveAll(){ localStorage.setItem('swp_state', JSON.stringify(state)); }
function loadAll(){
  const raw = localStorage.getItem('swp_state');
  if(raw){ Object.assign(state, JSON.parse(raw)); }
  else{ seedDemo(); saveAll(); }
}
function seedDemo(){
  // users
  state.users = [
    {id:'u1',username:'teacher1',name:'ครูสายฝน',role:'teacher',avatar:'👩‍🏫'},
    {id:'u2',username:'teacher2',name:'ครูภูมิ',role:'teacher',avatar:'👨‍🏫'},
    {id:'admin1',username:'admin1',name:'ผู้บริหารแจ่ม',role:'admin',avatar:'🧑‍💼'}
  ];
  // activities (weekly)
  const base = new Date(); base.setHours(0,0,0,0);
  const monday = getStartOfWeek(base);
  state.activities = [
    {id:'a1',title:'ประชุมผู้บริหาร',type:'meeting',description:'ประเมินแผนงานสัปดาห์',start:isoDate(addDays(monday,0),9,0),end:isoDate(addDays(monday,0),10,30),location:'ห้องประชุม',responsible:'admin1'},
    {id:'a2',title:'แข่งขันกีฬาภายใน',type:'sport',description:'เชียร์ทีมโรงเรียน',start:isoDate(addDays(monday,2),8,30),end:isoDate(addDays(monday,2),15,0),location:'สนามกีฬา',responsible:'u2'},
    {id:'a3',title:'อบรมเชิงปฏิบัติการวิชาการ',type:'academic',description:'แผนการสอนและนวัตกรรม',start:isoDate(addDays(monday,4),13,0),end:isoDate(addDays(monday,4),16,0),location:'อาคาร 2 ห้อง 201',responsible:'u1'},
    {id:'a4',title:'พิธีเชิญธง',type:'ceremony',description:'พิธีเช้า',start:isoDate(addDays(monday,0),7,30),end:isoDate(addDays(monday,0),8,0),location:'ลานหน้าเสาธง',responsible:'u1'}
  ];
  // duties (including 3 special requested)
  state.duties = [
    {id:'d1',title:'เวรป้ายหน้าเสาธง',type:'morningDuty',assignedTo:'u1',userType:'teacher',repeat:'daily',notes:'เช็คความเรียบร้อยก่อน 07:20'},
    {id:'d2',title:'ตรวจสอบและส่งแผนการสอน',type:'academic',assignedTo:'u2',userType:'teacher',repeat:'weekly',notes:'ส่งก่อนวันศุกร์'},
    {id:'d3',title:'กรอกคะแนนเก็บลง SGS',type:'registration',assignedTo:'u1',userType:'teacher',repeat:'weekly',notes:'กรอกครบภายใน 3 วันหลังสอบ'},
    {id:'d4',title:'เวรรับฝากเงินนักเรียน (ธนาคารโรงเรียน)',type:'schoolbank',assignedTo:'u2',userType:'teacher',repeat:'daily',notes:'เช็คสมุดฝาก-ถอน'},
  ];
  // dress codes
  state.dressCodes = [
    {id:'dc1', date:formatYMD(addDays(monday,0)), type:'uniform', label:'ชุดนักเรียน',icon:'🎓',color:'#B19BFF',notes:'ชุดนักเรียนเต็มรูปแบบ'},
    {id:'dc2', date:formatYMD(addDays(monday,2)), type:'sport', label:'ชุดกีฬา',icon:'🏃‍♀️',color:'#99EFBF',notes:'รองเท้ากีฬาต้องปิดเท้า'}
  ];
  // announcements
  state.announcements = [
    {id:'an1',title:'ขอความร่วมมือ',body:'วันพรุ่งนี้ให้ครูทุกท่านสวมเครื่องหมายชื่อ',author:'admin1',createdAt:new Date().toISOString()},
    {id:'an2',title:'ตารางสอบกลางภาค',body:'ตารางประกาศแล้วที่ห้องทะเบียน',author:'admin1',createdAt:new Date().toISOString()}
  ];
  // reminders
  state.reminders = [
    {id:'r1',userId:'u1',refType:'activity',refId:'a3',when:new Date(new Date().setHours(new Date().getHours()+1)).toISOString(),note:'เตรียมสไลด์'},
  ];
  // teaching schedule
  state.teachingSchedule = [
    {id:'s1',teacherId:'u1',subject:'คณิตศาสตร์',day:1,start:'09:00',end:'10:30',class:'ม.1/2'},
    {id:'s2',teacherId:'u1',subject:'คณิตศาสตร์',day:3,start:'09:00',end:'10:30',class:'ม.2/1'}
  ];
  state.dutyHistory = [];
}

function isoDate(date, hour=9, min=0){
  const d = new Date(date);
  d.setHours(hour,min,0,0);
  return d.toISOString();
}
function addDays(d, n){ const x=new Date(d); x.setDate(x.getDate()+n); return x; }
function getStartOfWeek(date){
  const d = new Date(date);
  const day = (d.getDay()+6)%7; // Monday = 0
  d.setDate(d.getDate()-day);
  d.setHours(0,0,0,0);
  return d;
}
function formatYMD(d){
  const dt = new Date(d);
  return dt.toISOString().slice(0,10);
}
function renderApp(){
  const me = state.me;
  if(!me) return;
  document.getElementById('loginScreen').style.display='none';
  document.getElementById('dashboard').style.display='block';
  document.getElementById('navBar').style.display='flex';
  document.getElementById('welcomeSub').textContent = `${me.name} — ${me.role === 'admin' ? 'ผู้บริหาร' : 'ครู'}`;
  // top announcement
  const top = state.announcements.slice(-1)[0];
  document.getElementById('topAnnouncement').textContent = top ? `${top.title} — ${top.body.slice(0,60)}...` : 'ยังไม่มีประกาศล่าสุด';
  document.getElementById('annCount').textContent = state.announcements.length;
  // Week view
  renderWeek();
  renderTodayDuties();
  renderDressToday();
  renderHistory();
}

function renderWeek(){
  const weekEl = document.getElementById('weekView');
  weekEl.innerHTML='';
  const start = getStartOfWeek(new Date());
  for(let i=0;i<7;i++){
    const dayDate = addDays(start,i);
    const dayBox = document.createElement('div'); dayBox.className='day';
    const dayName = ['จ','อ','พ','พฤ','ศ','ส','อา'][i];
    const dateNum = dayDate.getDate();
    dayBox.innerHTML = `<div class="day-name">${dayName}</div><div class="date">${dateNum}</div>`;
    // activities for the day
    const dayStr = formatYMD(dayDate);
    const acts = state.activities.filter(a => a.start.slice(0,10) === dayStr);
    acts.forEach(a=>{
      const tagClass = ({meeting:'tag-meeting',sport:'tag-sport',academic:'tag-academic',ceremony:'tag-ceremony'})[a.type] || 'tag-other';
      const el = document.createElement('div'); el.className = 'activity '+tagClass;
      el.innerHTML = `<div style="display:flex;justify-content:space-between;align-items:center"><div>${a.title}</div><div style="font-size:11px;opacity:0.95">${a.start.slice(11,16)}</div></div><div class="small-muted">${a.location} • ${getUserName(a.responsible)}</div>`;
      el.onclick = ()=> openActivityDetail(a.id);
      dayBox.appendChild(el);
    });
    weekEl.appendChild(dayBox);
  }
  // today summary
  const todayStr = formatYMD(new Date());
  const todays = state.activities.filter(a => a.start.slice(0,10) === todayStr);
  document.getElementById('todaySummary').textContent = todays.length ? `${todays.length} กิจกรรมวันนี้` : 'ไม่มีรายการ';
  document.getElementById('todayDate').textContent = new Date().toLocaleDateString('th-TH',{weekday:'short',day:'numeric',month:'short'});
}

function getUserName(id){ const u = state.users.find(x=>x.id===id); return u ? u.name : id; }

function openActivityDetail(id){
  const a = state.activities.find(x=>x.id===id); if(!a) return;
  const panel = document.createElement('div'); panel.className='panel';
  panel.innerHTML = `<div class="sheet">
    <button class="close" onclick="this.closest('.panel').remove()">✕</button>
    <h3 style="margin-top:0">${a.title} <span class="small muted">• ${a.start.slice(11,16)}-${a.end.slice(11,16)}</span></h3>
    <div class="small-muted">${a.location} • ผู้รับผิดชอบ: ${getUserName(a.responsible)}</div>
    <p style="margin-top:12px">${a.description}</p>
    <div style="display:flex;gap:8px;margin-top:12px">
      <button class="btn" onclick="scheduleReminderFor('${a.id}','activity')">เตือนฉัน 🔔</button>
      <button class="btn" style="background:#FFB86B;color:#542e00" onclick="assignToMe('${a.id}')">รับผิดชอบ</button>
    </div>
  </div>`;
  document.getElementById('panelContainer').appendChild(panel);
}
function scheduleReminderFor(refId, refType){
  const when = new Date(); when.setMinutes(when.getMinutes()+30); // demo: 30 min later
  const r = {id:'r'+Date.now(),userId:state.me.id,refType,refId,when:when.toISOString(),note:'เตือนจากกิจกรรม'};
  state.reminders.push(r); saveAll(); showToast('ตั้งการเตือนเรียบร้อย (30 นาที)');
  // schedule immediate demo notification
  scheduleNotification(r);
}
function assignToMe(activityId){
  // simple: add a duty record
  const d = {id:'da'+Date.now(),title:'รับผิดชอบกิจกรรม:'+activityId,type:'ad-hoc',assignedTo:state.me.id,userType:'teacher',repeat:'once',notes:'รับผิดชอบจากแอป'};
  state.duties.push(d); saveAll(); renderTodayDuties(); showToast('รับผิดชอบเรียบร้อย');
}

/* Duties page & today duties */
function renderTodayDuties(){
  const el = document.getElementById('todayDuties');
  el.innerHTML='';
  const todayStr = formatYMD(new Date());
  // duties assigned to me that are for today (repeat daily or weekly or once)
  const myD = state.duties.filter(d => d.assignedTo === state.me.id);
  const list = myD; // for demo we show all assigned duties
  document.getElementById('todayDutiesCount').textContent = list.length;
  list.forEach(d=>{
    const div = document.createElement('div'); div.className='split'; div.style.padding='8px 0';
    div.innerHTML = `<div><strong>${d.title}</strong><div class="small muted">${formatDutyType(d.type)} ${d.notes ? '• '+d.notes:''}</div></div>`;
    const btn = document.createElement('button'); btn.className='pill'; btn.textContent='ยืนยัน';
    btn.onclick = ()=> confirmDuty(d.id);
    div.appendChild(btn);
    el.appendChild(div);
  });
}
function formatDutyType(t){
  return ({academic:'งานวิชาการ',registration:'งานทะเบียนวัดผล',schoolbank:'ธนาคารโรงเรียน',morningDuty:'เวรเช้า'})[t] || t;
}
function confirmDuty(dutyId){
  const h = {id:'h'+Date.now(),dutyId,userId:state.me.id,doneAt:new Date().toISOString(),notes:''};
  state.dutyHistory.push(h); saveAll(); renderHistory(); showToast('ยืนยันการทำหน้าที่แล้ว ✅');
}

/* History */
function renderHistory(){
  const list = state.dutyHistory.slice(-5).reverse();
  document.getElementById('historyCount').textContent = state.dutyHistory.length;
  const el = document.getElementById('historyList'); el.innerHTML='';
  if(list.length===0){ el.innerHTML='<div class="small muted">ยังไม่มีประวัติ</div>'; return; }
  list.forEach(h=>{
    const duty = state.duties.find(d=>d.id===h.dutyId) || {title:'(ไม่ทราบชื่อ)'} ;
    const div = document.createElement('div'); div.className='split';
    div.innerHTML = `<div><div style="font-weight:700">${duty.title}</div><div class="small muted">${getUserName(h.userId)} • ${new Date(h.doneAt).toLocaleString('th-TH')}</div></div><div class="badge">เสร็จ</div>`;
    el.appendChild(div);
  });
}

/* Dress guide */
function renderDressToday(){
  const today = formatYMD(new Date());
  const dc = state.dressCodes.find(d=>d.date===today) || null;
  const el = document.getElementById('dressGuide');
  if(!dc){
    document.getElementById('dressTag').textContent='ปกติ';
    el.innerHTML = `<div class="small muted">ไม่มีกำหนดการแต่งกายพิเศษวันนี้ — แต่งชุดข้าราชการ/ชุดครูตามปกติ</div>`;
  } else {
    document.getElementById('dressTag').textContent = dc.label;
    el.innerHTML = `<div style="display:flex;align-items:center;gap:8px"><div style="font-size:24px">${dc.icon}</div><div><div style="font-weight:800">${dc.label}</div><div class="small muted">${dc.notes}</div></div></div>`;
  }
}

/* Panels for assign, announce, reminder */
function openPanel(mode='assign'){
  const panel = document.createElement('div'); panel.className='panel';
  let html = `<div class="sheet"><button class="close" onclick="this.closest('.panel').remove()">✕</button>`;
  if(mode==='assign'){
    html += `<h3>มอบหมายหน้าที่ใหม่</h3>
    <div class="list">
      <label>หัวข้อ</label><input id="paTitle" type="text" placeholder="ชื่อหน้าที่">
      <label>ประเภท</label>
      <select id="paType"><option value="academic">งานวิชาการ</option><option value="registration">ทะเบียนวัดผล</option><option value="schoolbank">ธนาคารโรงเรียน</option><option value="morningDuty">เวรเช้า</option></select>
      <label>มอบหมายให้ (username)</label><input id="paTo" type="text" placeholder="e.g. teacher1">
      <label>หมายเหตุ</label><input id="paNotes" type="text" placeholder="เช่น ส่งก่อนวันศุกร์">
      <div style="display:flex;gap:8px;margin-top:10px"><button class="btn" onclick="saveAssign()">บันทึก</button><button class="btn" style="background:#EEE;color:#333" onclick="this.closest('.panel').remove()">ยกเลิก</button></div>
    </div>`;
  } else if(mode==='announce'){
    html += `<h3>โพสต์ประกาศ</h3>
      <label>หัวข้อ</label><input id="anTitle" type="text">
      <label>เนื้อหา</label><textarea id="anBody" rows="4"></textarea>
      <div style="display:flex;gap:8px;margin-top:10px"><button class="btn" onclick="saveAnnouncement()">โพสต์</button><button class="btn" style="background:#EEE;color:#333" onclick="this.closest('.panel').remove()">ยกเลิก</button></div>`;
  } else if(mode==='reminder'){
    html += `<h3>ตั้งการแจ้งเตือน</h3>
      <label>ข้อความ</label><input id="rNote" type="text" placeholder="เตือนเตรียมเอกสาร">
      <label>เวลา (นาทีจากปัจจุบัน)</label><input id="rMin" type="number" value="10">
      <div style="display:flex;gap:8px;margin-top:10px"><button class="btn" onclick="saveReminder()">ตั้งเตือน</button><button class="btn" style="background:#EEE;color:#333" onclick="this.closest('.panel').remove()">ยกเลิก</button></div>`;
  }
  html += `</div>`;
  panel.innerHTML = html;
  document.getElementById('panelContainer').appendChild(panel);
}
function saveAssign(){
  const t=document.getElementById('paTitle').value.trim();
  const ty=document.getElementById('paType').value;
  const to=document.getElementById('paTo').value.trim();
  const notes=document.getElementById('paNotes').value.trim();
  if(!t || !to){ alert('กรุณากรอกชื่อหน้าที่และผู้รับมอบ'); return; }
  const user = state.users.find(u=>u.username===to);
  if(!user){ alert('ไม่พบผู้ใช้: '+to); return; }
  const d = {id:'d'+Date.now(),title:t,type:ty,assignedTo:user.id,userType:'teacher',repeat:'once',notes};
  state.duties.push(d); saveAll(); renderTodayDuties(); closeAllPanels(); showToast('มอบหมายเรียบร้อย 🎉');
}
function saveAnnouncement(){
  const t=document.getElementById('anTitle').value.trim();
  const b=document.getElementById('anBody').value.trim();
  if(!t||!b){ alert('กรอกข้อมูลไม่ครบ');return; }
  const an = {id:'an'+Date.now(),title:t,body:b,author:state.me.id,createdAt:new Date().toISOString()};
  state.announcements.push(an); saveAll(); closeAllPanels(); renderApp(); showToast('ประกาศถูกโพสต์ 📣');
}
function saveReminder(){
  const note=document.getElementById('rNote').value || 'เตือนจากแอป';
  const min=parseInt(document.getElementById('rMin').value||10,10);
  const when = new Date(); when.setMinutes(when.getMinutes()+min);
  const r = {id:'r'+Date.now(),userId:state.me.id,refType:'manual',refId:null,when:when.toISOString(),note};
  state.reminders.push(r); saveAll(); scheduleNotification(r); closeAllPanels(); showToast('ตั้งเตือนแล้ว 🔔');
}

function closeAllPanels(){ document.getElementById('panelContainer').innerHTML=''; }

/* Notification scheduling (demo using setTimeout and Notification API) */
function scheduleNotification(r){
  const when = new Date(r.when).getTime();
  const now = Date.now();
  const delay = Math.max(0, when - now);
  setTimeout(()=>{
    // show web notification
    const title = 'School Planner — แจ้งเตือน';
    const options = {body: r.note, icon: '', tag: r.id};
    if(Notification.permission === 'granted'){
      new Notification(title, options);
    } else {
      alert('🔔 '+r.note);
    }
  }, delay);
}

/* Simple toast */
function showToast(msg){
  const t = document.createElement('div'); t.style.position='fixed'; t.style.left='50%'; t.style.transform='translateX(-50%)'; t.style.bottom='110px';
  t.style.background='linear-gradient(90deg,#FFFFFF,#F6F0FF)'; t.style.padding='10px 14px'; t.style.borderRadius='12px'; t.style.boxShadow='0 8px 24px rgba(60,60,100,0.12)'; t.innerText=msg;
  document.body.appendChild(t); setTimeout(()=>t.remove(),2500);
}

/* Login flow */
document.getElementById('btnLogin').onclick = function(){
  const username = document.getElementById('inputUser').value.trim() || 'teacher1';
  const roleSel = document.getElementById('roleSelect').value;
  // find user by username, or create simple user
  let user = state.users.find(u=>u.username===username);
  if(!user){
    user = {id:username, username, name:username, role:roleSel, avatar:'👩‍🏫'};
    state.users.push(user); saveAll();
  }
  state.me = user;
  saveAll();
  // request notification permission
  if('Notification' in window){ Notification.requestPermission().then(()=>{/* noop */}); }
  renderApp();
  // schedule existing reminders for this user
  state.reminders.filter(r=>r.userId===state.me.id).forEach(scheduleNotification);
};

function goTo(view){
  // very simple: show relevant panel or view
  if(view==='dashboardView'){ document.getElementById('mainContent').scrollTo({top:0,behavior:'smooth'}); }
  else if(view==='calendarView'){ openCalendarSheet(); }
  else if(view==='dutiesView'){ openDutiesSheet(); }
  else if(view==='profileView'){ openProfileSheet(); }
}

/* Calendar sheet (full week + event list) */
function openCalendarSheet(){
  const panel = document.createElement('div'); panel.className='panel';
  const start = getStartOfWeek(new Date());
  let html = `<div class="sheet"><button class="close" onclick="this.closest('.panel').remove()">✕</button><h3>ปฏิทินประจำสัปดาห์</h3>`;
  for(let i=0;i<7;i++){
    const d = addDays(start,i);
    html += `<div style="margin-top:8px;padding:8px;border-radius:12px;background:linear-gradient(90deg,rgba(255,255,255,0.6),transparent)"><div style="font-weight:700">${d.toLocaleDateString('th-TH',{weekday:'short',day:'numeric',month:'short'})}</div>`;
    const acts = state.activities.filter(a=>a.start.slice(0,10)===formatYMD(d));
    if(acts.length===0) html += `<div class="small muted">ไม่มีรายการ</div>`;
    acts.forEach(a=>{
      html += `<div style="margin-top:6px;padding:8px;border-radius:10px;background:linear-gradient(90deg, #fff,#f7f3ff)"><div style="font-weight:700">${a.title} <span class="small muted" style="font-weight:400">• ${a.start.slice(11,16)}</span></div><div class="small muted">${a.location} • ${getUserName(a.responsible)}</div></div>`;
    });
    html += `</div>`;
  }
  html += `<div style="display:flex;gap:8px;margin-top:12px"><button class="btn" onclick="this.closest('.panel').remove()">ปิด</button></div></div>`;
  panel.innerHTML = html;
  document.getElementById('panelContainer').appendChild(panel);
}

/* Duties sheet */
function openDutiesSheet(){
  const panel = document.createElement('div'); panel.className='panel';
  let html = `<div class="sheet"><button class="close" onclick="this.closest('.panel').remove()">✕</button><h3>ระบบมอบหมายหน้าที่</h3>`;
  html += `<div class="small muted">รายการหน้าที่ทั้งหมด</div>`;
  state.duties.forEach(d=>{
    const who = getUserName(d.assignedTo);
    html += `<div style="display:flex;justify-content:space-between;align-items:center;margin-top:8px;padding:8px;border-radius:10px;background:#fff"><div><div style="font-weight:700">${d.title}</div><div class="small muted">${formatDutyType(d.type)} • ${who}</div></div>`;
    if(d.assignedTo===state.me.id){
      html += `<div><button class="pill" onclick="confirmDuty('${d.id}')">ยืนยัน</button></div></div>`;
    } else {
      html += `<div><div class="small muted">—</div></div></div>`;
    }
  });
  html += `<div style="display:flex;gap:8px;margin-top:12px"><button class="btn" onclick="this.closest('.panel').remove()">ปิด</button></div></div>`;
  panel.innerHTML = html;
  document.getElementById('panelContainer').appendChild(panel);
}

/* Profile sheet */
function openProfileSheet(){
  const panel = document.createElement('div'); panel.className='panel';
  const me = state.me;
  const myDuties = state.duties.filter(d=>d.assignedTo===me.id);
  let html = `<div class="sheet"><button class="close" onclick="this.closest('.panel').remove()">✕</button><h3>${me.avatar} ${me.name}</h3><div class="small muted">ตำแหน่ง: ${me.role==='admin'?'ผู้บริหาร':'ครู'}</div>`;
  html += `<div style="margin-top:10px"><strong>หน้าที่ประจำ</strong><div class="small muted">${myDuties.length} งาน</div>`;
  myDuties.forEach(d=> html += `<div style="margin-top:8px;padding:8px;border-radius:10px;background:#fff"><div style="font-weight:700">${d.title}</div><div class="small muted">${formatDutyType(d.type)} • ${d.notes || ''}</div></div>`);
  html += `</div><div style="margin-top:10px"><strong>ประวัติการเข้าร่วมกิจกรรม</strong><div class="small muted">ล่าสุด ${state.dutyHistory.length} รายการ</div></div>`;
  html += `<div style="display:flex;gap:8px;margin-top:12px"><button class="btn" onclick="this.closest('.panel').remove()">ปิด</button></div></div>`;
  panel.innerHTML = html;
  document.getElementById('panelContainer').appendChild(panel);
}

/* Utilities */
function showInitialDataNotice(){
  const el = document.createElement('div'); el.style.position='fixed'; el.style.top='22px'; el.style.right='18px';
  el.innerHTML = `<div class="badge">Demo: ข้อมูลเก็บใน localStorage</div>`; document.body.appendChild(el); setTimeout(()=>el.remove(),2500);
}

// load and init
loadAll();
showInitialDataNotice();
// schedule any pending reminders (for demo all users)
state.reminders.forEach(r=> scheduleNotification(r));

/* Expose some functions for inline onclick */
window.openPanel = openPanel;
window.scheduleReminderFor = scheduleReminderFor;
window.assignToMe = assignToMe;
window.openActivityDetail = openActivityDetail;
window.openCalendarSheet = openCalendarSheet;
window.openDutiesSheet = openDutiesSheet;
window.openProfileSheet = openProfileSheet;
window.saveAssign = saveAssign;
window.saveAnnouncement = saveAnnouncement;
window.saveReminder = saveReminder;
window.goTo = goTo;
window.closeAllPanels = closeAllPanels;

</script>
</body>
</html>
