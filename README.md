<html ....>
<html lang="th">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>School Weekly Planner — Prototype</title>

<!-- Font: Mali -->
<link href="https://fonts.googleapis.com/css2?family=Mali:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>
  :root{
    --bg-from: #EBD9FF; /* pastel purple */
    --bg-to:   #DFFBEA; /* pastel green */
    --card-bg: #FFFFFF;
    --muted:   #6B6A76;
    --accent:  #8F7BFF;
    --success: #4FC08D;
    --danger:  #FF8A8A;
    --radius: 18px;
    font-family: "Mali", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    -webkit-font-smoothing:antialiased;
    -moz-osx-font-smoothing:grayscale;
    color: #2F2B3A;
  }

  /* Page layout (mobile-first) */
  html,body{height:100%;margin:0;background:linear-gradient(160deg,var(--bg-from),var(--bg-to));}
  body{display:flex;align-items:stretch;justify-content:center;padding:18px;box-sizing:border-box;}
  .app {
    width:100%;
    max-width:420px;
    height:100vh;
    background: linear-gradient(180deg, rgba(255,255,255,0.9), rgba(255,255,255,0.96));
    border-radius:22px;
    box-shadow: 0 8px 30px rgba(48,40,78,0.08);
    overflow:hidden;
    position:relative;
    display:flex;
    flex-direction:column;
  }

  /* subtle dot-grid background to evoke notebook (very light) */
  .app::before{
    content:"";
    position:absolute;inset:0;
    background-image: radial-gradient(circle at 1px 1px, rgba(0,0,0,0.02) 0.5px, transparent 2px);
    background-size: 20px 20px;
    opacity:0.45;
    pointer-events:none;
    mix-blend-mode:multiply;
  }

  header{
    padding:16px 16px 8px 16px;
    display:flex;
    align-items:center;
    justify-content:space-between;
  }
  .brand{display:flex;flex-direction:column}
  .brand .title{font-weight:700;font-size:18px;color:#31283F}
  .brand .subtitle{font-size:12px;color:var(--muted);margin-top:2px}

  main{flex:1;overflow:auto;padding:8px 16px 100px 16px}

  /* Cards */
  .card{
    background:var(--card-bg);
    border-radius:var(--radius);
    box-shadow: 0 4px 10px rgba(60,50,90,0.04);
    padding:12px;
    margin-bottom:12px;
  }
  .muted{color:var(--muted);font-size:13px}
  .small{font-size:13px;color:#2F2B3A}

  /* Dashboard layout */
  .dashboard-grid{display:grid;grid-template-columns:1fr;gap:10px}
  .chip{padding:6px 10px;border-radius:12px;font-size:13px;background:linear-gradient(90deg, rgba(143,123,255,0.08), rgba(143,123,255,0.04));border:1px solid rgba(143,123,255,0.06);}

  /* Weekly calendar */
  .week{
    display:flex;gap:10px;overflow-x:auto;padding-bottom:6px;
  }
  .day{
    min-width:128px;
    padding:10px;border-radius:14px;background:linear-gradient(180deg, rgba(255,255,255,0.95), rgba(255,255,255,0.98));
    border:1px solid rgba(0,0,0,0.04);
  }
  .day-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:8px}
  .day-name{font-weight:700;color:#2F2B3A}
  .day-date{font-size:13px;color:var(--muted)}

  .activity{
    display:flex;align-items:flex-start;gap:8px;padding:8px;border-radius:12px;margin-bottom:8px;
    background:rgba(143,123,255,0.04);
    border-left:6px solid rgba(143,123,255,0.26);
  }
  .tag{
    padding:4px 8px;border-radius:10px;font-size:12px;color:#ffffff;
    min-width:58px;text-align:center;font-weight:600;
  }
  .tag.meeting{background:#8F7BFF}
  .tag.sport{background:#62C08E}
  .tag.academic{background:#6F92FF}
  .tag.ceremony{background:#FFB86B}

  /* Duties list */
  .duty{
    padding:10px;border-radius:12px;border:1px dashed rgba(0,0,0,0.06);display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;
  }
  .duty .meta{display:flex;flex-direction:column}
  .btn{
    padding:8px 10px;border-radius:12px;background:var(--accent);color:white;border:none;font-weight:700;cursor:pointer;
  }
  .btn.ghost{background:transparent;color:var(--accent);border:1px solid rgba(143,123,255,0.14)}
  .btn.small{padding:6px 8px;font-size:13px}

  /* Announcements */
  .announcement{padding:10px;border-radius:12px;background:linear-gradient(180deg, rgba(255,255,255,0.95), rgba(255,255,255,0.98));border-left:4px solid rgba(143,123,255,0.12);margin-bottom:8px}

  /* Floating bottom nav */
  nav.bottom-nav{
    position:fixed;bottom:20px;left:50%;transform:translateX(-50%);
    width:calc(100% - 48px);max-width:396px;height:64px;border-radius:34px;background:rgba(255,255,255,0.85);
    display:flex;align-items:center;justify-content:space-around;padding:8px 12px;backdrop-filter: blur(6px);box-shadow:0 8px 20px rgba(48,40,78,0.06)
  }
  .nav-item{flex:1;text-align:center;font-weight:700;color:#4a4460;font-size:13px;cursor:pointer;padding:8px;border-radius:14px}
  .nav-item.active{background:linear-gradient(90deg,var(--bg-from),var(--bg-to));color:white}

  /* Login */
  .login-screen{display:flex;flex-direction:column;gap:12px;align-items:stretch;padding:20px}
  .input{padding:12px;border-radius:12px;border:1px solid rgba(0,0,0,0.06);background:transparent;font-size:14px}
  .login-note{font-size:13px;color:var(--muted)}

  /* Toast */
  .toast{
    position:fixed;left:50%;transform:translateX(-50%);bottom:100px;background:#31283F;color:white;padding:10px 14px;border-radius:12px;box-shadow:0 6px 18px rgba(0,0,0,0.12);
    display:none;font-weight:700
  }

  /* small helper */
  .muted-block{color:var(--muted);font-size:13px;margin-top:6px}

  @media(min-width:800px){
    body{background:linear-gradient(160deg,var(--bg-from),var(--bg-to));align-items:center}
  }
</style>
</head>
<body>
<div class="app" id="app">
  <!-- Header -->
  <header>
    <div class="brand">
      <div class="title">School Weekly Planner</div>
      <div class="subtitle">สรุปกิจกรรมและหน้าที่ประจำสัปดาห์</div>
    </div>
    <div id="header-actions" class="muted"></div>
  </header>

  <!-- Main content: multiple screens -->
  <main id="main">
    <!-- Login Screen -->
    <section id="screen-login">
      <div class="login-screen card" style="margin-top:8px">
        <div style="font-weight:700;font-size:16px;color:#2F2B3A">เข้าสู่ระบบ</div>

        <label class="muted" for="inp-username">ชื่อผู้ใช้</label>
        <input id="inp-username" class="input" placeholder="ตัวอย่าง: teacher1 หรือ admin" aria-label="ชื่อผู้ใช้" />

        <label class="muted" for="inp-role">บทบาท</label>
        <select id="inp-role" class="input" aria-label="บทบาท">
          <option value="teacher">ครู</option>
          <option value="admin">ผู้บริหาร</option>
        </select>

        <div class="login-note">โปรโตไทป์นี้เก็บข้อมูลเฉพาะเครื่อง (localStorage) เพื่อทดลองใช้งาน</div>
        <button id="btn-login" class="btn" aria-label="เข้าสู่ระบบ">เข้าสู่ระบบ</button>
      </div>
    </section>

    <!-- Dashboard -->
    <section id="screen-dashboard" style="display:none">
      <div class="dashboard-grid">
        <div class="card">
          <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px">
            <div style="font-weight:700">กิจกรรมสัปดาห์นี้</div>
            <div class="muted">สรุปรายวัน</div>
          </div>
          <div class="week" id="week-list" aria-label="ปฏิทินสรุปสัปดาห์"></div>
        </div>

        <div class="card">
          <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px">
            <div style="font-weight:700">หน้าที่ของคุณ (วันนี้)</div>
            <div class="muted" id="duty-count">0 งาน</div>
          </div>
          <div id="duty-list" aria-live="polite"></div>
        </div>

        <div class="card">
          <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px">
            <div style="font-weight:700">แต่งกายวันนี้</div>
            <div class="muted" id="dress-today-date"></div>
          </div>
          <div style="display:flex;align-items:center;justify-content:space-between">
            <div>
              <div id="dress-role" style="font-weight:700;font-size:15px">ชุดปกติ</div>
              <div class="muted-block" id="dress-desc">อ้างอิงประกาศโรงเรียน</div>
            </div>
            <div id="dress-chip" class="chip" style="border-radius:12px">ทั่วไป</div>
          </div>
        </div>

        <div class="card">
          <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px">
            <div style="font-weight:700">ประกาศสำคัญ</div>
            <div class="muted">ล่าสุด</div>
          </div>
          <div id="announcements"></div>
        </div>
      </div>
    </section>

    <!-- Calendar Screen -->
    <section id="screen-calendar" style="display:none">
      <div class="card" style="margin-top:8px">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px">
          <div style="font-weight:700">ปฏิทินกิจกรรม (สัปดาห์)</div>
          <div class="muted" id="week-range"></div>
        </div>
        <div id="calendar-list"></div>
      </div>
    </section>

    <!-- Notifications -->
    <section id="screen-notifications" style="display:none">
      <div class="card" style="margin-top:8px">
        <div style="font-weight:700;margin-bottom:8px">การแจ้งเตือน</div>
        <div id="reminder-list"></div>
      </div>
    </section>

    <!-- Profile -->
    <section id="screen-profile" style="display:none">
      <div class="card" style="margin-top:8px">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px">
          <div>
            <div style="font-weight:700" id="profile-name">ชื่อครู</div>
            <div class="muted" id="profile-role">ตำแหน่ง</div>
          </div>
          <div class="muted">ID: <span id="profile-id">---</span></div>
        </div>

        <div style="margin-bottom:8px">
          <div style="font-weight:700">หน้าที่ประจำ</div>
          <div class="muted" id="profile-regular">-</div>
        </div>

        <div style="margin-bottom:8px">
          <div style="font-weight:700">หน้าที่พิเศษประจำฝ่าย</div>
          <div id="profile-special" class="muted">-</div>
        </div>

        <div>
          <div style="font-weight:700">ประวัติการยืนยันงาน</div>
          <div id="history-list" class="muted">ยังไม่มีประวัติ</div>
        </div>
      </div>
    </section>
  </main>

  <!-- Floating nav -->
  <nav class="bottom-nav" id="bottom-nav" role="navigation" aria-label="เมนูหลัก">
    <div class="nav-item active" data-screen="screen-dashboard" tabindex="0">Dashboard</div>
    <div class="nav-item" data-screen="screen-calendar" tabindex="0">Calendar</div>
    <div class="nav-item" data-screen="screen-notifications" tabindex="0">Notifications</div>
    <div class="nav-item" data-screen="screen-profile" tabindex="0">Profile</div>
  </nav>

  <div id="toast" class="toast" role="status" aria-live="polite"></div>
</div>

<script>
/* ------------------------------------------
   Prototype single-file app (mobile-first)
   - Login -> Dashboard
   - Weekly calendar
   - Duties (including 3 special duties)
   - Announcements
   - Dress code
   - Notifications (simulated)
   - Duty confirmation saved in localStorage
   ------------------------------------------ */

/* Utilities */
const today = new Date();
function addDays(d, offset){ const n=new Date(d); n.setDate(n.getDate()+offset); return n; }
function fmtDateShort(d){ return d.toLocaleDateString('th-TH', {weekday:'short', day:'numeric', month:'short'}); }
function startOfWeek(d){
  const copy=new Date(d);
  const day = copy.getDay(); // 0 Sun .. 6 Sat
  const diff = (day + 6)%7; // make Monday=0
  copy.setDate(copy.getDate() - diff);
  copy.setHours(0,0,0,0);
  return copy;
}
function showToast(msg, ms=2200){
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.style.display = 'block';
  clearTimeout(t._h);
  t._h = setTimeout(()=> t.style.display = 'none', ms);
}

/* Sample / initial data (client-side demo)
   In production this data comes from backend APIs.
*/
const sampleUser = {
  id: "teacher1",
  name: "ครูสมชาย ใจดี",
  role: "teacher",
  regularDuty: "ครูประจำชั้น ป.4/2",
  specialDuties: [
    "ตรวจและส่งแผนการสอน (Academic)",
    "กรอกคะแนนเก็บลงระบบ SGS (Registration/Measurement)",
    "เวรรับฝากเงินนักเรียนตอนเช้า (School Bank)"
  ]
};

const weekStart = startOfWeek(today);

const activities = [
  {id:1,title:"ประชุมครูประจำสัปดาห์", dateOffset:0, time:"08:30", place:"ห้องประชุม", owner:"ฝ่ายบริหาร", type:"meeting"},
  {id:2,title:"แข่งฟุตบอลชุมชน", dateOffset:1, time:"15:00", place:"สนามกีฬา", owner:"ครูพลศึกษา", type:"sport"},
  {id:3,title:"สัมมนาวิชาการ", dateOffset:2, time:"09:00", place:"ห้องบรรยาย", owner:"ฝ่ายวิชาการ", type:"academic"},
  {id:4,title:"พิธีเปิดกิจกรรมพิเศษ", dateOffset:4, time:"07:30", place:"สนามหน้าเสาธง", owner:"ฝ่ายกิจการ", type:"ceremony"},
  {id:5,title:"ตรวจระบบคะแนน SGS", dateOffset:3, time:"10:00", place:"ห้องคอม", owner:"ครูพัช", type:"academic"}
];

/* Duties including the three special duties requested */
const duties = [
  {id:101, title:"เวรเช้ารับฝากเงิน (School Bank)", dateOffset:0, assignedTo:"teacher1", time:"07:15", tag:"School Bank"},
  {id:102, title:"ตรวจและส่งแผนการสอน (Academic)", dateOffset:1, assignedTo:"teacher1", time:"12:00", tag:"Academic"},
  {id:103, title:"กรอกคะแนนใน SGS (Registration/Measurement)", dateOffset:2, assignedTo:"teacher1", time:"16:00", tag:"Registration"}
];

const announcements = [
  {id:201, title:"แจ้งเตือนการประชุมผู้ปกครอง", dateOffset:-1, body:"การประชุมผู้ปกครองจะจัดวันที่ศุกร์นี้ เวลา 18:00 โปรดเตรียมเอกสารที่เกี่ยวข้อง"},
  {id:202, title:"กำหนดการวันกีฬา", dateOffset:3, body:"วันพฤหัสบดีจัดกิจกรรมกีฬาสี นักเรียนแต่งชุดกีฬา"}
];

const dressCodes = [
  {id:401, dateOffset:0, role:"ชุดทางการ", desc:"เชิ้ตหรือชุดทางการของโรงเรียน", chip:"ชุดทางการ"},
  {id:402, dateOffset:1, role:"ชุดกีฬา", desc:"ชุดกีฬา (เสื้อกีฬาและกางเกงกีฬา)", chip:"ชุดกีฬา"},
  {id:403, dateOffset:3, role:"ชุดพิธี", desc:"ชุดพิธีตามที่ประกาศ", chip:"ชุดพิธี"}
];

const reminders = [
  {id:301, title:"เตรียมเอกสารการประชุม", whenOffsetSec:8, note:"สไลด์และสำเนาประกาศ"},
  {id:302, title:"เตรียมชุดพิธี", whenOffsetSec:18, note:"ครูที่รับผิดชอบเตรียมเครื่องแต่งกาย"}
];

/* App state */
const appState = { user: null };

/* --- Rendering functions --- */
function renderHeader(){
  const headerActions = document.getElementById('header-actions');
  if(appState.user){
    headerActions.innerHTML = '<div style="text-align:right"><div style="font-weight:700">'+escapeHtml(appState.user.name)+'</div><div class="muted">'+escapeHtml(appState.user.role)+'</div></div>';
  } else headerActions.innerHTML = '';
}

function renderWeek(){
  const container = document.getElementById('week-list');
  container.innerHTML = '';
  for(let i=0;i<7;i++){
    const d = addDays(weekStart,i);
    const dayEl = document.createElement('div');
    dayEl.className='day';
    const dayHeader = document.createElement('div');
    dayHeader.className='day-header';
    const name = document.createElement('div'); name.className='day-name'; name.textContent = d.toLocaleDateString('th-TH', {weekday:'short'});
    const date = document.createElement('div'); date.className='day-date'; date.textContent = d.getDate();
    dayHeader.appendChild(name); dayHeader.appendChild(date);
    dayEl.appendChild(dayHeader);

    activities.filter(a => a.dateOffset === i).forEach(a=>{
      const act = document.createElement('div'); act.className='activity';
      const left = document.createElement('div'); left.style.flex='1';
      const title = document.createElement('div'); title.className='small'; title.textContent = a.title;
      const meta = document.createElement('div'); meta.className='muted'; meta.textContent = `${a.time} • ${a.place} • ${a.owner}`;
      left.appendChild(title); left.appendChild(meta);
      const tag = document.createElement('div'); tag.className='tag ' + (a.type || '');
      tag.textContent = a.type === 'meeting' ? 'ประชุม' : a.type==='sport' ? 'กีฬา' : a.type==='academic' ? 'วิชาการ' : 'พิธี';
      act.appendChild(left); act.appendChild(tag);
      dayEl.appendChild(act);
    });

    container.appendChild(dayEl);
  }
}

function renderDuties(){
  const list = document.getElementById('duty-list');
  const userId = appState.user ? appState.user.id : null;
  if(!userId){ list.innerHTML = '<div class="muted">เข้าสู่ระบบเพื่อดูหน้าที่ของคุณ</div>'; return; }
  const my = duties.filter(d=>d.assignedTo===userId);
  document.getElementById('duty-count').textContent = my.length + ' งาน';
  list.innerHTML = '';
  if(my.length===0){
    list.innerHTML = '<div class="muted">ไม่มีหน้าที่วันนี้</div>';
    return;
  }
  my.forEach(d=>{
    const el = document.createElement('div'); el.className='duty';
    const meta = document.createElement('div'); meta.className='meta';
    const title = document.createElement('div'); title.style.fontWeight='700'; title.textContent = d.title;
    const sub = document.createElement('div'); sub.className='muted'; sub.textContent = (d.time ? d.time + ' • ' : '') + 'Tag: ' + d.tag;
    meta.appendChild(title); meta.appendChild(sub);
    const btn = document.createElement('button'); btn.className='btn small'; btn.textContent='ยืนยันแล้ว';
    btn.onclick = ()=>{
      markDutyDone(d.id);
    };
    el.appendChild(meta); el.appendChild(btn);
    list.appendChild(el);
  });
}

function renderAnnouncements(){
  const el = document.getElementById('announcements');
  el.innerHTML='';
  announcements.forEach(a=>{
    const dom = document.createElement('div'); dom.className='announcement';
    const title = document.createElement('div'); title.style.fontWeight='700'; title.textContent = a.title;
    const body = document.createElement('div'); body.className='muted'; body.style.marginTop='6px'; body.textContent = a.body;
    dom.appendChild(title); dom.appendChild(body);
    el.appendChild(dom);
  });
}

function renderCalendarList(){
  const el = document.getElementById('calendar-list');
  el.innerHTML = '';
  activities.sort((a,b)=>a.dateOffset-b.dateOffset).forEach(a=>{
    const d = addDays(weekStart, a.dateOffset);
    const card = document.createElement('div'); card.className='card';
    const h = document.createElement('div'); h.style.display='flex'; h.style.justifyContent='space-between'; h.style.alignItems='center';
    const left = document.createElement('div'); left.style.display='flex'; left.style.flexDirection='column';
    const title = document.createElement('div'); title.style.fontWeight='700'; title.textContent = a.title;
    const meta = document.createElement('div'); meta.className='muted'; meta.textContent = `${fmtDateShort(d)} • ${a.time} • ${a.place}`;
    left.appendChild(title); left.appendChild(meta);
    const right = document.createElement('div'); right.className='tag ' + (a.type || ''); right.style.marginLeft='10px';
    right.textContent = a.type === 'meeting' ? 'ประชุม' : a.type==='sport' ? 'กีฬา' : a.type==='academic' ? 'วิชาการ' : 'พิธี';
    h.appendChild(left); h.appendChild(right);
    card.appendChild(h);
    el.appendChild(card);
  });
  document.getElementById('week-range').textContent = fmtDateShort(weekStart) + " — " + fmtDateShort(addDays(weekStart,6));
}

function renderReminders(){
  const el = document.getElementById('reminder-list');
  el.innerHTML = '';
  if(reminders.length===0){ el.innerHTML='<div class="muted">ไม่มีการแจ้งเตือน</div>'; return; }
  reminders.forEach(r=>{
    const dom = document.createElement('div'); dom.className='announcement';
    const title = document.createElement('div'); title.style.fontWeight='700'; title.textContent = r.title;
    const body = document.createElement('div'); body.className='muted'; body.style.marginTop='6px'; body.textContent = r.note || '';
    dom.appendChild(title); dom.appendChild(body);
    el.appendChild(dom);
  });
}

function renderDressToday(){
  const match = dressCodes.find(dc => dc.dateOffset===0);
  const dChip = document.getElementById('dress-chip');
  const role = document.getElementById('dress-role');
  const desc = document.getElementById('dress-desc');
  document.getElementById('dress-today-date').textContent = fmtDateShort(today);
  if(match){
    dChip.textContent = match.chip;
    role.textContent = match.role;
    desc.textContent = match.desc;
  } else {
    dChip.textContent = 'ทั่วไป';
    role.textContent = 'ชุดปกติ';
    desc.textContent = 'อ้างอิงประกาศโรงเรียน';
  }
}

/* ---- History (localStorage) ---- */
function markDutyDone(dutyId){
  if(!appState.user){ showToast('กรุณาเข้าสู่ระบบก่อน'); return; }
  const hist = JSON.parse(localStorage.getItem('swp_done_history')||'[]');
  hist.push({dutyId, userId: appState.user.id, at: new Date().toISOString()});
  localStorage.setItem('swp_done_history', JSON.stringify(hist));
  showToast('บันทึกการทำงานเรียบร้อย');
  renderHistory();
}
function renderHistory(){
  const histAll = JSON.parse(localStorage.getItem('swp_done_history')||'[]');
  const hist = histAll.filter(h=>h.userId===appState.user.id);
  const el = document.getElementById('history-list');
  if(hist.length===0) el.textContent='ยังไม่มีประวัติ';
  else{
    el.innerHTML = '';
    hist.slice().reverse().forEach(h=>{
      const d = new Date(h.at);
      const row = document.createElement('div'); row.textContent = d.toLocaleString('th-TH');
      el.appendChild(row);
    });
  }
}

/* ---- Auth & navigation ---- */
function setScreen(id){
  document.querySelectorAll('main section').forEach(s=>s.style.display='none');
  const target = document.getElementById(id);
  if(target) target.style.display='block';
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  document.querySelectorAll(`.nav-item[data-screen="${id}"]`).forEach(n=>n.classList.add('active'));
}

function escapeHtml(str){
  if(!str) return '';
  return str.replace(/[&<>"']/g, (m)=> ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[m]));
}

function bootApp(){
  const user = JSON.parse(localStorage.getItem('swp_user')||'null');
  if(user){ appState.user = user; }
  renderHeader();
  if(!appState.user){
    setScreen('screen-login');
    document.getElementById('screen-login').style.display='block';
  } else {
    setScreen('screen-dashboard');
    document.getElementById('screen-login').style.display='none';
    renderHeader();
    renderWeek(); renderDuties(); renderAnnouncements(); renderDressToday(); renderCalendarList(); renderReminders(); renderProfile(); renderHistory();
    scheduleReminders();
  }
}

/* Render user profile */
function renderProfile(){
  const p = appState.user;
  if(!p) return;
  document.getElementById('profile-name').textContent = p.name;
  document.getElementById('profile-role').textContent = p.role;
  document.getElementById('profile-id').textContent = p.id;
  document.getElementById('profile-regular').textContent = p.regularDuty || '-';
  document.getElementById('profile-special').textContent = (p.specialDuties || []).join(' • ');
}

/* Simulate server-side scheduled reminders (prototype only) */
function scheduleReminders(){
  reminders.forEach(r=>{
    const ms = (r.whenOffsetSec||12)*1000;
    setTimeout(()=> {
      showToast('การแจ้งเตือน: ' + r.title, 3800);
    }, ms);
  });
}

/* --- Event handlers --- */
document.getElementById('btn-login').addEventListener('click', ()=>{
  const name = document.getElementById('inp-username').value.trim();
  const role = document.getElementById('inp-role').value;
  if(!name){ alert('กรุณากรอกชื่อผู้ใช้'); return; }
  const userObj = {
    id: name,
    name: name === 'admin' ? 'ผู้บริหารโรงเรียน' : sampleUser.name,
    role,
    regularDuty: sampleUser.regularDuty,
    specialDuties: sampleUser.specialDuties
  };
  appState.user = userObj;
  localStorage.setItem('swp_user', JSON.stringify(userObj));
  bootApp();
});

/* Bottom nav click */
document.querySelectorAll('.nav-item').forEach(n=>{
  n.addEventListener('click', e=>{
    const screen = e.currentTarget.getAttribute('data-screen');
    setScreen(screen);
    if(screen==='screen-dashboard') {
      renderDuties(); renderAnnouncements(); renderDressToday(); renderWeek();
    } else if(screen==='screen-calendar') renderCalendarList();
    else if(screen==='screen-notifications') renderReminders();
    else if(screen==='screen-profile') { renderProfile(); renderHistory(); }
  });
});

/* Initialize */
bootApp();

</script>
</body>
</html>
