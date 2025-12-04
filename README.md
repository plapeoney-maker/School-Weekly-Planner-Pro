<html ....>
<html lang="th">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>School Weekly Planner — โมบาย (Demo)</title>

  <!-- Mali Font -->
  <link href="https://fonts.googleapis.com/css2?family=Mali:wght@300;400;600&display=swap" rel="stylesheet">

  <style>
    :root{
      --bg:#fffafc;
      --accent-grad: linear-gradient(135deg,#d6c8ff 0%, #c8f0d6 100%);
      --purple-pastel:#cfc0ff;
      --green-pastel:#c8f0d6;
      --primary:#8b5cf6;
      --secondary:#34d399;
      --muted:#9ca3af;
      --card:#ffffff;
      --note:#fff6f9;
      --shadow: 0 8px 20px rgba(139,92,246,0.12);
      --rounded: 18px;
      font-family: "Mali", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    }

    /* Dot-grid background like notebook */
    body{
      margin:0;
      background: radial-gradient(circle at 10px 10px, rgba(0,0,0,0.02) 1px, transparent 1px);
      background-size: 24px 24px;
      background-color: var(--bg);
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      color:#222;
      min-height:100vh;
      display:flex;
      align-items:center;
      justify-content:center;
      padding:16px;
    }

    /* App frame (mobile) */
    .app {
      width: 390px;
      max-width: calc(100% - 32px);
      height: 812px;
      max-height: calc(100vh - 32px);
      background: var(--card);
      border-radius: 28px;
      box-shadow: 0 16px 36px rgba(16,24,40,0.15);
      overflow: hidden;
      position:relative;
      display:flex;
      flex-direction:column;
    }

    /* Header with washi tape */
    .app-header{
      padding:18px 18px 8px 18px;
      background: var(--accent-grad);
      display:flex;
      gap:12px;
      align-items:center;
      border-bottom-left-radius:18px;
      border-bottom-right-radius:18px;
      position:relative;
    }
    .washi{
      position:absolute;
      left:18px;
      top:-8px;
      width:120px;
      height:30px;
      background: linear-gradient(90deg,#ffd7e8,#fff4f8);
      border-radius:10px;
      transform: rotate(-6deg);
      box-shadow: 0 6px 14px rgba(0,0,0,0.06);
      display:flex;
      align-items:center;
      justify-content:center;
      font-size:12px;
      color:#7c3aed;
      font-weight:600;
      z-index:2;
      opacity:0.95;
    }
    .header-title{
      display:flex;
      flex-direction:column;
      gap:2px;
    }
    .header-title h1{ margin:0; font-size:20px; }
    .header-title p{ margin:0; font-size:12px; color:var(--muted); }

    /* Floating search / quick actions */
    .quick-actions{
      margin-left:auto;
      display:flex;
      gap:8px;
    }
    .qa-btn{
      background:rgba(255,255,255,0.7);
      padding:8px;
      border-radius:12px;
      box-shadow: var(--shadow);
      cursor:pointer;
      font-size:18px;
    }

    /* Content (scrollable) */
    .app-content{
      padding:14px;
      overflow:auto;
      flex:1;
    }

    /* Cards */
    .cards{
      display:grid;
      grid-template-columns: 1fr 1fr;
      gap:12px;
      margin-bottom:12px;
    }
    .card{
      background: linear-gradient(180deg, rgba(255,255,255,0.9), rgba(255,255,255,0.95));
      border-radius: 14px;
      padding:12px;
      box-shadow: 0 6px 18px rgba(16,24,40,0.06);
      border:1px solid rgba(139,92,246,0.06);
      min-height:74px;
    }
    .card h3{ margin:0 0 6px 0; font-size:13px; }
    .card p{ margin:0; font-size:12px; color:var(--muted); }

    /* Weekly list (simpler calendar) */
    .week-list{
      margin-top:8px;
    }
    .day-row{
      display:flex;
      gap:8px;
      align-items:flex-start;
      padding:8px;
      border-radius:12px;
      margin-bottom:8px;
      background: linear-gradient(90deg, rgba(255,255,255,0.7), rgba(255,255,255,0.8));
      border:1px dashed rgba(0,0,0,0.03);
    }
    .day-date{
      width:68px;
      font-size:13px;
      text-align:center;
      padding:6px;
      border-radius:10px;
      background:rgba(139,92,246,0.06);
    }
    .events{
      flex:1;
      display:flex;
      flex-direction:column;
      gap:6px;
    }
    .event{
      display:flex;
      align-items:center;
      gap:8px;
      background:#fff;
      padding:8px;
      border-radius:12px;
      border:1px solid rgba(0,0,0,0.04);
      box-shadow: 0 6px 12px rgba(16,24,40,0.04);
      cursor:pointer;
    }
    .tag{
      width:10px;height:10px;border-radius:4px;
      flex-shrink:0;
    }
    .event .meta{ font-size:12px; color:var(--muted); }

    /* Floating nav bottom */
    .floating-nav{
      position:absolute;
      left:50%;
      transform:translateX(-50%);
      bottom:18px;
      width:92%;
      max-width:720px;
      height:64px;
      background:linear-gradient(180deg,rgba(255,255,255,0.9),#fff);
      border-radius: 999px;
      display:flex;
      align-items:center;
      justify-content:space-around;
      box-shadow: 0 12px 26px rgba(16,24,40,0.12);
      border:1px solid rgba(139,92,246,0.06);
      padding:8px 18px;
      z-index:5;
    }
    .nav-item{
      display:flex;
      flex-direction:column;
      align-items:center;
      gap:4px;
      font-size:12px;
      color:var(--muted);
      cursor:pointer;
      user-select:none;
    }
    .nav-item.active{ color:var(--primary); font-weight:600; }

    /* Modal / panels */
    .panel{
      position:fixed;
      inset:0;
      display:none;
      align-items:flex-end;
      justify-content:center;
      z-index:50;
      background:linear-gradient(180deg, rgba(0,0,0,0.18), rgba(0,0,0,0.24));
    }
    .panel.open{ display:flex; }
    .sheet{
      width:100%;
      max-width:420px;
      background:#fff;
      border-top-left-radius:20px;
      border-top-right-radius:20px;
      padding:14px;
      max-height:82%;
      overflow:auto;
      box-shadow: 0 -12px 30px rgba(16,24,40,0.12);
    }

    /* Login screen */
    .login{
      height:100%;
      display:flex;
      flex-direction:column;
      align-items:center;
      justify-content:center;
      gap:18px;
      padding:24px;
    }
    .login-card{
      width:320px;
      max-width: calc(100% - 48px);
      padding:18px;
      background:linear-gradient(180deg,#fff,#fff);
      border-radius:20px;
      box-shadow: var(--shadow);
      border:1px solid rgba(139,92,246,0.06);
    }
    .input{
      display:flex;
      flex-direction:column;
      gap:8px;
      margin-bottom:12px;
    }
    .input input{
      padding:10px 12px;
      border-radius:12px;
      border:1px solid rgba(0,0,0,0.06);
      font-size:14px;
      outline:none;
    }
    .btn{
      padding:10px;
      border-radius:12px;
      background:linear-gradient(90deg,var(--purple-pastel),var(--green-pastel));
      border:none;
      cursor:pointer;
      font-weight:700;
      color:#3a076b;
      box-shadow: 0 8px 18px rgba(139,92,246,0.12);
    }

    /* Tiny elements for list */
    .small{ font-size:12px; color:var(--muted); }

    /* badges for dress code */
    .dress-badge{
      padding:8px 10px;
      border-radius:999px;
      background:linear-gradient(90deg,#fff,#fff);
      border:1px solid rgba(0,0,0,0.04);
      display:inline-flex;
      gap:8px;
      align-items:center;
      font-size:13px;
      box-shadow: 0 8px 18px rgba(0,0,0,0.04);
    }

    /* Responsive for small screens */
    @media (max-width:420px){
      .app{ width:100%; height:100vh; border-radius:0; }
      .washi{ left:8px; width:96px; }
      .login-card{ width:92%; }
    }

  </style>
</head>
<body>

  <div class="app" id="app">
    <!-- Login Screen -->
    <div id="screen-login" style="height:100%; display:flex; flex-direction:column;">
      <div style="padding:32px 18px 0 18px;">
        <div style="font-size:28px; font-weight:700; color:var(--primary);">School Weekly Planner ✨</div>
        <div style="margin-top:6px; font-size:13px; color:var(--muted);">แอปสำหรับครู — วางแผนงานประจำสัปดาห์</div>
      </div>

      <div class="login" style="flex:1;">
        <div class="login-card">
          <div style="display:flex; gap:10px; align-items:center; margin-bottom:12px;">
            <div style="width:56px; height:56px; border-radius:12px; background:var(--purple-pastel); display:flex; align-items:center; justify-content:center; font-size:28px;">📒</div>
            <div>
              <div style="font-weight:700;">เข้าสู่ระบบครู</div>
              <div style="font-size:12px; color:var(--muted);">กรุณาใส่อีเมลและรหัสผ่านเพื่อเข้าใช้งาน</div>
            </div>
          </div>

          <div class="input">
            <label class="small">อีเมล</label>
            <input id="login-email" placeholder="you@school.edu" />
            <label class="small">รหัสผ่าน</label>
            <input id="login-pass" type="password" placeholder="••••••••" />
          </div>
          <button class="btn" id="btn-login">เข้าสู่ระบบ</button>

          <div style="margin-top:10px; font-size:12px; color:var(--muted); text-align:center;">
            ทดลองใช้งานด้วยบัญชีตัวอย่าง: demo@school / demo123
          </div>
        </div>

        <div style="font-size:12px; color:var(--muted); margin-top:12px; text-align:center;">
          ดีไซน์: สมุดจดน่ารัก (Mali, ดอกจุด, washi tape) 🧾💜
        </div>
      </div>
    </div>

    <!-- Main App (hidden until login) -->
    <div id="screen-main" style="display:none; height:100%; flex-direction:column;">
      <div class="app-header">
        <div class="washi">Weekly Notes</div>
        <div style="width:48px; height:48px; border-radius:12px; background:linear-gradient(90deg,var(--purple-pastel),#fff); display:flex; align-items:center; justify-content:center; font-size:22px;">🏫</div>
        <div class="header-title">
          <h1 id="welcome-title">สวัสดี ครูสมมติ 😊</h1>
          <p id="week-range" class="small">สัปดาห์: 1 ธ.ค. 2025 - 7 ธ.ค. 2025</p>
        </div>
        <div class="quick-actions">
          <div class="qa-btn" title="ประกาศ" id="open-ann">📣</div>
          <div class="qa-btn" title="แจ้งเตือน" id="open-rem">🔔</div>
        </div>
      </div>

      <div class="app-content">
        <!-- Top cards -->
        <div class="cards">
          <div class="card" id="card-today">
            <h3>กิจกรรมวันนี้ • 2 รายการ</h3>
            <p id="today-events">08:00 - พิธีเช้า (สนาม) • คุณครูใหญ่ 🎉<br/>10:00 - ประชุมคณะครู (ห้องประชุม) • คณะบริหาร</p>
          </div>
          <div class="card" id="card-duty">
            <h3>หน้าที่วันนี้ • เวรเช้า</h3>
            <p id="today-duty">งาน: เวรรับฝากเงินนักเรียน (School Bank) — ยืนยันสถานะ</p>
          </div>
          <div class="card" id="card-dress" style="grid-column: span 2;">
            <h3>การแต่งกายวันนี้</h3>
            <div style="display:flex; gap:10px; align-items:center; margin-top:6px;">
              <div class="dress-badge">🎽 ชุดกีฬา</div>
              <div style="flex:1; font-size:13px; color:var(--muted);">อ้างอิง: ประกาศ โรงเรียน ลงวันที่ 2025-11-25</div>
            </div>
          </div>
        </div>

        <!-- Weekly list -->
        <div>
          <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:8px;">
            <div style="font-weight:700;">ปฏิทินสัปดาห์นี้</div>
            <div style="font-size:12px; color:var(--muted);">แท็ก: 🟣 ประชุม 🟢 กีฬา 🔵 วิชาการ 🟡 พิธี</div>
          </div>

          <div class="week-list" id="week-list">
            <!-- JS will inject day rows -->
          </div>
        </div>

        <!-- Quick sections -->
        <div style="margin-top:10px; display:flex; gap:10px;">
          <div style="flex:1;" class="card">
            <h3>ประกาศล่าสุด</h3>
            <p id="latest-ann" class="small">📢 ระบบทำความสะอาดสนามแข่งขัน วันศุกร์นี้ 14:00 — ลงชื่อได้ที่หน้า "ประกาศ"</p>
          </div>
          <div style="width:120px;" class="card">
            <h3>สถานะงาน</h3>
            <p id="status-summary" class="small">งานที่ยืนยัน: 3/5</p>
          </div>
        </div>

        <!-- Hidden panels triggered by nav -->
        <div id="panel-container"></div>
      </div>

      <!-- Floating nav -->
      <div class="floating-nav" role="navigation" aria-label="Navigation">
        <div class="nav-item active" data-panel="dashboard">🏠<div>Dashboard</div></div>
        <div class="nav-item" data-panel="calendar">📆<div>Calendar</div></div>
        <div class="nav-item" data-panel="duties">📝<div>Duties</div></div>
        <div class="nav-item" data-panel="dress">👔<div>Dress</div></div>
        <div class="nav-item" data-panel="profile">👩‍🏫<div>Profile</div></div>
      </div>
    </div>
  </div>

  <!-- Panels (modals) -->
  <div id="panel-sheet" class="panel" aria-hidden="true">
    <div class="sheet" id="sheet-body">
      <!-- Injected content -->
      <div style="text-align:center; font-weight:700; margin-bottom:8px;">รายละเอียด</div>
      <div id="sheet-content" style="font-size:13px; color:var(--muted);"></div>
      <div style="height:18px;"></div>
      <div style="display:flex; gap:8px; justify-content:flex-end;">
        <button class="btn" id="sheet-close" style="background:linear-gradient(90deg,#ffe7f3,#e9fff2); color:#6b2177;">ปิด</button>
      </div>
    </div>
  </div>

  <script>
    /*******************************
     * Demo data (in-memory / localStorage)
     *******************************/
    const demoUser = {
      id: "tch-001",
      name: "ครูสายฝน",
      role: "teacher",
      email: "demo@school",
      duties: [
        // today's duty sample
      ]
    };

    // Sample week data: array of days with events
    const WEEK = getThisWeekDates();
    const sampleEvents = [
      { id:1, day:WEEK[0], time:"08:00", title:"พิธีเช้า", place:"สนาม", owner:"ผอ.", tag:"ceremony", tagEmoji:"🟡" },
      { id:2, day:WEEK[0], time:"10:00", title:"ประชุมคณะครู", place:"ห้องประชุม", owner:"ฝ่ายบริหาร", tag:"meeting", tagEmoji:"🟣" },
      { id:3, day:WEEK[1], time:"09:00", title:"คัดเลือกนักกีฬา", place:"สนาม", owner:"ครูพลศึกษา", tag:"sports", tagEmoji:"🟢" },
      { id:4, day:WEEK[2], time:"13:00", title:"อบรมวิชาการ", place:"ห้องปฏิบัติการ", owner:"ฝ่ายวิชาการ", tag:"academic", tagEmoji:"🔵" },
      { id:5, day:WEEK[4], time:"07:30", title:"เวรรับฝากเงินนักเรียน", place:"ธนาคารโรงเรียน", owner:"คุณครูสมชาย", tag:"bank", tagEmoji:"🟣" }
    ];

    // Sample duties (including the 3 special tasks)
    const DUTIES = [
      { id:"d1", title:"เวรรับฝากเงินนักเรียน (School Bank)", type:"School Bank", assignedTo:"tch-001", date: WEEK[4], time:"07:30", status:"pending" },
      { id:"d2", title:"ตรวจสอบและส่งแผนการสอน (Academic)", type:"Academic", assignedTo:"tch-001", date: WEEK[2], time:"16:00", status:"submitted" },
      { id:"d3", title:"กรอกคะแนนเก็บลงระบบ SGS (Registration/Measurement)", type:"Registration/Measurement", assignedTo:"tch-002", date: WEEK[3], time:"12:00", status:"pending" }
    ];

    // Announcements
    const ANNS = [
      { id:"a1", title:"ประชาสัมพันธ์: ทำความสะอาดสนาม", date:"2025-11-25", content:"สนามจะปิดทำความสะอาดวันศุกร์ 14:00 - 16:00" },
      { id:"a2", title:"ประกาศ: แต่งกายวันกีฬา", date:"2025-11-24", content:"ครูทุกท่านสวมชุดกีฬาในวันศุกร์นี้" }
    ];

    // Dress code rules
    const DRESS = [
      { id:"dr1", date:WEEK[0], code:"ชุดนักเรียน", icon:"👔", ref:"ประกาศ 2025-11-01" },
      { id:"dr2", date:WEEK[1], code:"ชุดกีฬา", icon:"🎽", ref:"ประกาศ 2025-11-20" },
      { id:"dr3", date:WEEK[2], code:"ชุดทางการ", icon:"🕴️", ref:"ประกาศ 2025-10-15" },
    ];

    // Reminders (in-app)
    const REMINDERS = [
      { id:"r1", when: new Date(Date.now() + 1000*60*60*6).toISOString(), title:"เตรียมเอกสารสำหรับประชุม", note:"เอกสารตารางสอน 3 ชุด" }
    ];

    /*******************************
     * Helper functions
     *******************************/
    function getThisWeekDates(){
      const d = new Date();
      // make Monday as start
      const day = d.getDay() || 7;
      const monday = new Date(d); monday.setDate(d.getDate() - day + 1);
      const days = [];
      for(let i=0;i<7;i++){
        const dd = new Date(monday); dd.setDate(monday.getDate()+i);
        days.push(dd.toISOString().slice(0,10));
      }
      return days;
    }

    function formatDateShort(iso){
      const dt = new Date(iso);
      return dt.getDate()+"/"+(dt.getMonth()+1);
    }

    function tagColor(tag){
      switch(tag){
        case "meeting": return "#c7b3ff";
        case "sports": return "#b9f0d2";
        case "academic": return "#bfdbff";
        case "ceremony": return "#fff1b8";
        case "bank": return "#ffd6e8";
        default: return "#eee";
      }
    }

    /*******************************
     * Render functions
     *******************************/
    function renderWeekList(){
      const container = document.getElementById("week-list");
      container.innerHTML = "";
      WEEK.forEach((isoDate, idx) => {
        const dayEvents = sampleEvents.filter(e => e.day === isoDate);
        const dayDiv = document.createElement("div");
        dayDiv.className = "day-row";
        dayDiv.innerHTML = `
          <div class="day-date">
            <div style="font-weight:700;">${["จ","อ","พ","พฤ","ศ","ส","อา"][idx]}</div>
            <div class="small">${formatDateShort(isoDate)}</div>
          </div>
          <div class="events" id="events-${idx}"></div>
        `;
        container.appendChild(dayDiv);
        const eventsDiv = dayDiv.querySelector(`#events-${idx}`);
        if(dayEvents.length === 0){
          eventsDiv.innerHTML = `<div class="small" style="padding:8px;">ไม่มีเหตุการณ์</div>`;
        } else {
          dayEvents.forEach(ev=>{
            const evEl = document.createElement("div");
            evEl.className = "event";
            evEl.innerHTML = `
              <div class="tag" style="background:${tagColor(ev.tag)}"></div>
              <div style="flex:1">
                <div style="font-weight:700;">${ev.time} — ${ev.title} ${ev.tagEmoji || ""}</div>
                <div class="meta">${ev.place} • ผู้รับผิดชอบ: ${ev.owner}</div>
              </div>
              <div style="font-size:14px; color:var(--muted)">›</div>
            `;
            evEl.addEventListener("click",()=> openEventSheet(ev));
            eventsDiv.appendChild(evEl);
          });
        }
      });
    }

    function openEventSheet(ev){
      const sheet = document.getElementById("panel-sheet");
      const content = document.getElementById("sheet-content");
      content.innerHTML = `
        <div style="font-weight:800; font-size:16px;">${ev.title} ${ev.tagEmoji || ""}</div>
        <div class="small" style="margin-top:6px;">วัน: ${ev.day} • เวลา: ${ev.time}</div>
        <div style="margin-top:8px;">สถานที่: <b>${ev.place}</b></div>
        <div style="margin-top:8px;">ผู้รับผิดชอบ: <b>${ev.owner}</b></div>
        <div style="margin-top:12px;"><button class="btn" id="confirm-duty">ยืนยันการทำงาน/เข้าร่วม</button></div>
      `;
      sheet.classList.add("open");
      document.getElementById("sheet-close").focus();

      document.getElementById("confirm-duty").addEventListener("click",()=>{
        // mark as confirmed in localStorage history
        const hist = JSON.parse(localStorage.getItem("confirmed")||"[]");
        hist.push({eventId:ev.id, timestamp:new Date().toISOString(), user:demoUser.id});
        localStorage.setItem("confirmed", JSON.stringify(hist));
        alert("บันทึกการยืนยันแล้ว ✅");
        sheet.classList.remove("open");
        renderStatusSummary();
      });
    }

    function renderTopCards(){
      // today events
      const today = new Date().toISOString().slice(0,10);
      const todayEvents = sampleEvents.filter(e => e.day === today);
      document.getElementById("today-events").innerHTML = todayEvents.length ? todayEvents.map(e=>`${e.time} - ${e.title} (${e.place}) • ${e.owner}`).join("<br/>") : "วันนี้ไม่มีเหตุการณ์";
      // today's duty - find duties for today
      const todayDuty = DUTIES.find(d=>d.assignedTo===demoUser.id && d.date === today);
      document.getElementById("today-duty").innerText = todayDuty ? `${todayDuty.title} — สถานะ: ${todayDuty.status}` : "ไม่มีหน้าที่ประจำวันนี้";
    }

    function renderAnnouncements(){
      document.getElementById("latest-ann").innerText = (ANNS[0] && `📢 ${ANNS[0].title} — ${ANNS[0].content}`) || "ไม่มีประกาศใหม่";
    }

    function renderStatusSummary(){
      const confirmed = JSON.parse(localStorage.getItem("confirmed")||"[]");
      const total = DUTIES.filter(d=>d.assignedTo===demoUser.id).length;
      const done = confirmed.filter(c=> {
        const d = DUTIES.find(x => x.id == ("e"+c.eventId) || x.id==c.eventId);
        return !!d || true; // for demo count any confirmation
      }).length;
      document.getElementById("status-summary").innerText = `งานที่ยืนยัน: ${done}/${total || 1}`;
    }

    /*******************************
     * Login / Navigation
     *******************************/
    document.getElementById("btn-login").addEventListener("click", ()=>{
      const email = document.getElementById("login-email").value || "";
      const pass = document.getElementById("login-pass").value || "";
      if(!email && !pass){
        // demo login
        startApp(demoUser);
      } else {
        // very basic demo auth
        if(email.includes("@") && pass.length>=4){
          demoUser.email = email;
          startApp(demoUser);
        } else {
          alert("โปรดใส่อีเมลและรหัสผ่านที่ถูกต้อง (ตัวอย่าง demo@school / demo123)");
        }
      }
    });

    function startApp(user){
      document.getElementById("screen-login").style.display = "none";
      document.getElementById("screen-main").style.display = "flex";
      document.getElementById("welcome-title").innerText = `สวัสดี ${user.name} 😊`;
      // set week range
      const weekRange = `${formatDateShort(WEEK[0])} - ${formatDateShort(WEEK[6])}`;
      document.getElementById("week-range").innerText = `สัปดาห์: ${weekRange}`;
      renderWeekList();
      renderTopCards();
      renderAnnouncements();
      renderStatusSummary();
    }

    // nav items
    document.querySelectorAll(".nav-item").forEach(item=>{
      item.addEventListener("click", ()=>{
        document.querySelectorAll(".nav-item").forEach(i=>i.classList.remove("active"));
        item.classList.add("active");
        openPanel(item.dataset.panel);
      });
    });

    // quick actions
    document.getElementById("open-ann").addEventListener("click", ()=> openPanel("announcements"));
    document.getElementById("open-rem").addEventListener("click", ()=> openPanel("reminders"));

    // sheet close
    document.getElementById("sheet-close").addEventListener("click", ()=> {
      document.getElementById("panel-sheet").classList.remove("open");
    });

    function openPanel(name){
      const sheet = document.getElementById("panel-sheet");
      const content = document.getElementById("sheet-content");
      content.innerHTML = ""; // reset
      if(name==="dashboard"){
        sheet.classList.remove("open");
        return;
      }
      if(name==="calendar"){
        content.innerHTML = `<div style="font-weight:800;">ปฏิทินรายสัปดาห์</div>`;
        WEEK.forEach((d,idx)=>{
          const events = sampleEvents.filter(e=>e.day===d);
          content.innerHTML += `<div style="margin-top:8px; font-weight:700;">${["จ","อ","พ","พฤ","ศ","ส","อา"][idx]} ${formatDateShort(d)}</div>`;
          if(events.length===0) content.innerHTML += `<div class="small">ไม่มีเหตุการณ์</div>`;
          events.forEach(ev=>{
            content.innerHTML += `<div style="margin-top:6px; padding:8px; border-radius:12px; background:#fff; border:1px solid #eee;">${ev.time} — <b>${ev.title}</b> • ${ev.place}</div>`;
          });
        });
      } else if(name==="duties"){
        content.innerHTML = `<div style="font-weight:800;">กำหนดหน้าที่</div><div class="small" style="margin-top:6px;">งานประจำ / งานพิเศษ</div>`;
        DUTIES.forEach(d=>{
          content.innerHTML += `
            <div style="margin-top:8px; padding:8px; border-radius:12px; background:#fff; border:1px solid #eee;">
              <div style="font-weight:700;">${d.title}</div>
              <div class="small">${d.date} • ${d.time} • สถานะ: ${d.status}</div>
              <div style="margin-top:6px; display:flex; gap:8px; justify-content:flex-end;">
                ${d.assignedTo === demoUser.id ? `<button class="btn" onclick="confirmDuty('${d.id}')">ยืนยันแล้ว</button>` : ""}
              </div>
            </div>`;
        });
      } else if(name==="dress"){
        content.innerHTML = `<div style="font-weight:800;">การแต่งกายวันนี้</div><div class="small" style="margin-top:6px;">อ้างอิงจากประกาศโรงเรียน</div>`;
        DRESS.forEach(dd=>{
          content.innerHTML += `<div style="margin-top:8px;" class="dress-badge">${dd.icon} ${dd.code} <span class="small" style="margin-left:8px; color:var(--muted);">• ${dd.ref}</span></div>`;
        });
      } else if(name==="profile"){
        content.innerHTML = `<div style="font-weight:800;">โปรไฟล์ครู</div>`;
        content.innerHTML += `<div style="margin-top:8px;"><b>${demoUser.name}</b> • ${demoUser.role}</div>`;
        content.innerHTML += `<div class="small" style="margin-top:8px;">หน้าที่ประจำ: ครูประจำชั้น / งานพิเศษ: เวรธนาคาร, ตรวจแผนการสอน</div>`;
        const confirmed = JSON.parse(localStorage.getItem("confirmed")||"[]");
        content.innerHTML += `<div style="margin-top:10px; font-weight:700;">ประวัติการยืนยันการทำงาน</div>`;
        content.innerHTML += confirmed.length ? confirmed.map(c=>`<div class="small">• ยืนยันเมื่อ ${new Date(c.timestamp).toLocaleString()}</div>`).join("") : `<div class="small">ยังไม่มีประวัติ</div>`;
      } else if(name==="announcements"){
        content.innerHTML = `<div style="font-weight:800;">ประกาศสำคัญ</div>`;
        ANNS.forEach(a=>{
          content.innerHTML += `<div style="margin-top:8px; padding:8px; border-radius:12px; background:#fff; border:1px solid #eee;">
            <div style="font-weight:700;">${a.title}</div>
            <div class="small">${a.date}</div>
            <div style="margin-top:6px;" class="small">${a.content}</div>
          </div>`;
        });
      } else if(name==="reminders"){
        content.innerHTML = `<div style="font-weight:800;">แจ้งเตือน</div>`;
        REMINDERS.forEach(r=>{
          content.innerHTML += `<div style="margin-top:8px; padding:8px; border-radius:12px; background:#fff; border:1px solid #eee;">
            <div style="font-weight:700;">${r.title}</div>
            <div class="small">${new Date(r.when).toLocaleString()}</div>
            <div style="margin-top:6px;" class="small">${r.note}</div>
          </div>`;
        });
      } else {
        content.innerHTML = `<div>ไม่พบหน้าที่เลือก</div>`;
      }
      sheet.classList.add("open");
    }

    function confirmDuty(did){
      const d = DUTIES.find(x=>x.id===did);
      if(!d) return;
      d.status = "completed";
      const hist = JSON.parse(localStorage.getItem("confirmed")||"[]");
      hist.push({eventId:did, timestamp:new Date().toISOString(), user:demoUser.id});
      localStorage.setItem("confirmed", JSON.stringify(hist));
      alert("บันทึกสถานะงานว่า 'ทำแล้ว' ✅");
      renderStatusSummary();
      openPanel("duties");
    }

    // Initialize demo (keep login visible until user clicks)
    // pre-populate some localStorage
    if(!localStorage.getItem("confirmed")){
      localStorage.setItem("confirmed", JSON.stringify([]));
    }

    // Expose some functions to window for inline buttons
    window.confirmDuty = confirmDuty;
    window.openPanel = openPanel;

  </script>
</body>
</html>
