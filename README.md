<html ....>
<html lang="th">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>School Weekly Planner - Cute Mockup</title>

  <!-- Google Font Mali -->
  <link href="https://fonts.googleapis.com/css2?family=Mali:wght@300;400;600&display=swap" rel="stylesheet">

  <style>
    :root{
      --purple-1:#EED9FF;
      --purple-2:#D2B3FF;
      --green-1:#E6FFE8;
      --green-2:#BFFFD7;
      --accent:#B192FF;
      --paper:#FFFDF9;
      --muted:#7B7B7B;
      --text:#2F2F2F;
      --card-radius:28px; /* rounded-3xl feel */
      --glass-shadow: 0 8px 20px rgba(127,90,255,0.08);
      --dot-size:2px;
    }

    html,body{
      height:100%;
      margin:0;
      font-family: 'Mali', sans-serif;
      background: linear-gradient(160deg, var(--purple-1) 0%, var(--green-1) 100%);
      color:var(--text);
      -webkit-font-smoothing:antialiased;
    }

    /* Dot grid paper effect */
    body::before{
      content:"";
      position:fixed;
      inset:0;
      background-image:
        radial-gradient(var(--muted) 0.6px, transparent 0.7px);
      background-size: 24px 24px;
      opacity:0.06;
      pointer-events:none;
    }

    .app {
      max-width:1100px;
      margin:32px auto;
      padding:28px;
      background: linear-gradient(180deg, rgba(255,255,255,0.92), rgba(255,255,255,0.96));
      border-radius:34px;
      box-shadow: var(--glass-shadow);
      border: 1px solid rgba(160,140,255,0.08);
    }

    header{
      display:flex;
      align-items:center;
      gap:14px;
      margin-bottom:18px;
    }

    .logo {
      width:56px;height:56px;
      background: linear-gradient(135deg,var(--purple-2),var(--green-2));
      border-radius:14px;
      display:flex;align-items:center;justify-content:center;
      color:white;font-weight:700;font-size:20px;
      box-shadow: 0 6px 14px rgba(110,80,255,0.12);
    }

    .title {
      font-size:20px;
      line-height:1;
    }
    .subtitle { font-size:12px;color:var(--muted);margin-top:4px; }

    .top-cards{
      display:grid;
      grid-template-columns: repeat(3, 1fr);
      gap:16px;
      margin-top:12px;
    }

    .card{
      background: white;
      padding:14px;
      border-radius:var(--card-radius);
      box-shadow: 0 6px 18px rgba(120,100,200,0.06);
      border: 1px dashed rgba(180,160,255,0.08);
      position:relative;
      overflow:visible;
    }

    .washi {
      position:absolute;
      left:12px;top:-8px;
      width:80px;height:26px;
      background: linear-gradient(90deg,#FFEFDB,#FFF4F8);
      transform: rotate(-6deg);
      border-radius:8px;
      box-shadow: 0 3px 6px rgba(0,0,0,0.06);
      display:flex;align-items:center;justify-content:center;
      font-size:12px;
    }

    .card h3{ margin:0;font-size:15px; }
    .muted { color:var(--muted); font-size:13px; margin-top:6px; }

    /* week strip */
    .week-strip{
      margin-top:18px;
      display:flex;gap:10px;align-items:center;
      overflow:auto;padding-bottom:8px;
    }
    .day-pill{
      min-width:92px;
      padding:10px;border-radius:18px;
      background: linear-gradient(180deg, #fff, #fafafa);
      border:1px solid rgba(200,190,255,0.06);
      display:flex;flex-direction:column;align-items:flex-start;gap:6px;
    }
    .day-pill .date { font-weight:600; font-size:14px; }
    .dot{width:10px;height:10px;border-radius:50%;}
    .tag { font-size:12px;padding:6px 8px;border-radius:999px;background:var(--purple-1); color:var(--text); }

    /* activity cards within calendar */
    .activity {
      display:flex;gap:10px;align-items:center;
      background: linear-gradient(90deg, rgba(210,179,255,0.18), rgba(191,255,215,0.1));
      padding:8px;border-radius:14px;
      border:1px solid rgba(180,150,255,0.08);
    }
    .activity .time { font-size:12px;color:var(--muted);min-width:56px; }
    .activity .meta { font-size:13px;font-weight:600; }

    .list {
      margin-top:18px; display:grid; gap:12px;
    }

    /* floating nav */
    .floating-nav {
      position:fixed;
      left:50%;
      transform:translateX(-50%);
      bottom:22px;
      background: linear-gradient(180deg, rgba(255,255,255,0.96), rgba(255,255,255,0.98));
      padding:8px 18px;
      border-radius:40px;
      box-shadow: 0 12px 30px rgba(120,90,200,0.12);
      display:flex;gap:14px;align-items:center;
      border:1px solid rgba(160,140,255,0.06);
    }
    .nav-item{ font-size:18px; padding:8px; border-radius:999px; cursor:pointer; color:var(--muted); }
    .nav-item.active{ background: linear-gradient(90deg,var(--purple-2),var(--green-2)); color:white; box-shadow:0 6px 16px rgba(120,90,255,0.18); }

    /* small modal style */
    .modal {
      position:fixed; left:50%; top:50%; transform:translate(-50%,-50%);
      background:white; padding:18px; border-radius:20px; width:90%; max-width:720px;
      box-shadow: 0 20px 60px rgba(80,60,140,0.18);
      display:none; z-index:120;
    }
    .modal.open{ display:block; }
    .modal .close { float:right; cursor:pointer; color:var(--muted) }

    /* list styles */
    .duties .done { opacity:0.6; text-decoration:line-through; }

    /* profile card */
    .profile {
      display:flex; gap:14px; align-items:center;
    }
    .avatar{
      width:76px;height:76px;border-radius:18px;background:linear-gradient(135deg,var(--green-2),var(--purple-2));
      color:white;display:flex;align-items:center;justify-content:center;font-weight:700;
      box-shadow: 0 8px 20px rgba(110,80,255,0.08);
    }

    /* responsive */
    @media (max-width:900px){
      .top-cards { grid-template-columns: 1fr; }
      .app{ margin:12px; padding:18px; border-radius:20px; }
      .floating-nav{ bottom:12px; padding:8px 12px; }
    }
  </style>
</head>
<body>
  <div class="app" role="application" aria-label="School Weekly Planner">
    <header>
      <div class="logo">SWP</div>
      <div>
        <div class="title">School Weekly Planner ✨</div>
        <div class="subtitle">สรุปกิจกรรมและหน้าที่ประจำสัปดาห์ของโรงเรียน</div>
      </div>
      <div style="margin-left:auto;display:flex;gap:10px;align-items:center">
        <button id="announceBtn" style="background:transparent;border:0;cursor:pointer;font-size:20px">📣</button>
        <button id="notifBtn" style="background:transparent;border:0;cursor:pointer;font-size:20px">🔔</button>
      </div>
    </header>

    <!-- Top cards -->
    <div class="top-cards" aria-hidden="false">
      <div class="card" id="todayCard">
        <div class="washi">สรุปวันนี้</div>
        <h3>กิจกรรมวันนี้ 🎉</h3>
        <div class="muted">3 กิจกรรมสำคัญ</div>
        <div style="margin-top:10px">
          <div class="activity" style="margin-top:8px">
            <div class="time">09:00</div>
            <div class="meta">ประชุมครู <span style="margin-left:8px;font-size:12px;color:var(--muted)">ห้องประชุม</span></div>
          </div>
          <div class="activity" style="margin-top:8px">
            <div class="time">13:30</div>
            <div class="meta">ค่ายวิทยาศาสตร์ 🧪</div>
          </div>
        </div>
      </div>

      <div class="card" style="background: linear-gradient(180deg,var(--green-1),#ffffff);">
        <div class="washi">หน้าที่</div>
        <h3>หน้าที่วันนี้ ✅</h3>
        <div class="muted">คุณครู A มี 2 หน้าที่</div>
        <div class="duties list" style="margin-top:10px">
          <div class="activity" style="justify-content:space-between">
            <div><div style="font-weight:700">เวรรับฝากเงิน (School Bank)</div><div style="font-size:12px;color:var(--muted)">07:30 - 08:15</div></div>
            <div><button class="confirmBtn" data-id="d1">ยืนยัน ✓</button></div>
          </div>

          <div class="activity" style="justify-content:space-between">
            <div><div style="font-weight:700">ตรวจแผนการสอน (Academic)</div><div style="font-size:12px;color:var(--muted)">ก่อน 12:00</div></div>
            <div><button class="confirmBtn" data-id="d2">ยืนยัน ✓</button></div>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="washi">แต่งกาย</div>
        <h3>การแต่งกายวันนี้ 👗</h3>
        <div class="muted">ชุดนักเรียน — เสื้อเชิ้ตขาว / กระโปรงกรมท่า</div>
        <div style="margin-top:10px; display:flex;gap:10px;align-items:center;">
          <div style="width:56px;height:56px;border-radius:12px;background:linear-gradient(135deg,#FFF5F0,#FFE7F6);display:flex;align-items:center;justify-content:center;font-size:26px">👔</div>
          <div style="font-size:13px;">ตรวจเครื่องแบบตามประกาศโรงเรียน</div>
        </div>
      </div>
    </div>

    <!-- Week strip -->
    <div class="week-strip" aria-hidden="false" style="margin-top:18px">
      <!-- Example day pills -->
      <div class="day-pill">
        <div class="date">จ. 8 ธ.ค.</div>
        <div class="muted">2 กิจกรรม</div>
        <div style="display:flex;gap:6px;margin-top:6px">
          <div class="dot" style="background:var(--purple-2)"></div>
          <div class="dot" style="background:var(--green-2)"></div>
        </div>
      </div>

      <div class="day-pill">
        <div class="date">อ. 9 ธ.ค.</div>
        <div class="muted">1 กิจกรรม</div>
        <div style="display:flex;gap:6px;margin-top:6px">
          <div class="dot" style="background:#FFD1EA"></div>
        </div>
      </div>

      <div class="day-pill">
        <div class="date">พ. 10 ธ.ค.</div>
        <div class="muted">ไม่มี</div>
        <div style="height:18px"></div>
      </div>
    </div>

    <!-- Main list: announcements & calendar -->
    <div style="display:grid;grid-template-columns:1fr 360px;gap:18px;margin-top:18px">
      <section>
        <h3 style="margin:0 0 10px 0">ปฏิทินสัปดาห์นี้ 📆</h3>

        <div style="background:white;padding:12px;border-radius:20px;border:1px solid rgba(180,160,255,0.05)">
          <div style="display:flex;flex-direction:column;gap:10px">
            <div class="activity">
              <div class="time">09:00</div>
              <div class="meta">ประชุมครูประจำสัปดาห์</div>
            </div>
            <div class="activity">
              <div class="time">11:00</div>
              <div class="meta">คณะกรรมการทางวิชาการ</div>
            </div>
            <div class="activity">
              <div class="time">13:30</div>
              <div class="meta">ค่ายวิทยาศาสตร์ (Lab)</div>
            </div>
          </div>
        </div>

        <h3 style="margin:18px 0 8px 0">ประกาศล่าสุด 📣</h3>
        <div style="display:flex;flex-direction:column;gap:10px">
          <div class="card" style="padding:12px">
            <div style="display:flex;align-items:center;gap:10px">
              <div style="width:44px;height:44px;border-radius:12px;background:linear-gradient(90deg,#FFF2F9,#F2FFF7);display:flex;align-items:center;justify-content:center;">📌</div>
              <div>
                <div style="font-weight:700">แจ้งกำหนดการชุมนุมพิเศษ</div>
                <div class="muted">ประกาศโดย ผู้บริหาร • 1 วันก่อนหน้า</div>
              </div>
            </div>
            <div class="muted" style="margin-top:8px">กรุณาเตรียมเอกสารและแบบฟอร์มการอนุญาตนักเรียนก่อนวันที่ 12 ธ.ค.</div>
          </div>

          <div class="card" style="padding:12px">
            <div style="display:flex;align-items:center;gap:10px">
              <div style="width:44px;height:44px;border-radius:12px;background:linear-gradient(90deg,#FFF7E6,#E8F8FF);display:flex;align-items:center;justify-content:center;">📎</div>
              <div>
                <div style="font-weight:700">อัปเดตแบบฟอร์ม SGS</div>
                <div class="muted">ประกาศโดย เจ้าหน้าที่ทะเบียน • 3 วันก่อนหน้า</div>
              </div>
            </div>
            <div class="muted" style="margin-top:8px">ครูผู้สอนโปรดอัปโหลดผลคะแนนลง SGS ภายในสิ้นเดือน</div>
          </div>
        </div>

      </section>

      <aside>
        <div class="card" style="padding:12px">
          <h4 style="margin-top:0">โปรไฟล์ครู 👩‍🏫</h4>
          <div class="profile">
            <div class="avatar">KA</div>
            <div>
              <div style="font-weight:700">คุณครู กาญจนา</div>
              <div class="muted">ครูวิทยาศาสตร์ • ห้อง 304</div>
              <div style="margin-top:8px;font-size:13px">หน้าที่ประจำ: สอนวิทยาศาสตร์ ม.2</div>
            </div>
          </div>
          <div style="margin-top:12px">
            <button id="viewProfile" style="background:var(--accent);border:0;padding:8px 12px;border-radius:12px;color:white;cursor:pointer">ดูโปรไฟล์</button>
          </div>
        </div>

        <div class="card" style="margin-top:12px;padding:12px">
          <h4 style="margin:0 0 8px 0">แจ้งเตือนล่วงหน้า 🔔</h4>
          <div class="muted">ไม่มีการแจ้งเตือนใหม่</div>
          <div style="margin-top:12px">
            <button id="testNotif" style="background:linear-gradient(90deg,var(--purple-2),var(--green-2));border:0;padding:8px 12px;border-radius:12px;color:white;cursor:pointer">ทดสอบแจ้งเตือน</button>
          </div>
        </div>
      </aside>
    </div>

    <!-- modal: activity detail -->
    <div id="modal" class="modal" role="dialog" aria-modal="true" aria-hidden="true">
      <div style="display:flex;align-items:center;justify-content:space-between">
        <div style="font-weight:700">รายละเอียดกิจกรรม</div>
        <div class="close" onclick="closeModal()">✖️</div>
      </div>
      <div style="margin-top:10px">
        <div class="muted">ประชุมครู — ห้องประชุมใหญ่ • 09:00 - 10:30</div>
        <div style="margin-top:8px">รายละเอียด: ประชุมเตรียมงานกิจกรรมปลายภาค และสรุปผลการเรียน</div>

        <h4 style="margin-top:12px">Checklist เตรียมของ</h4>
        <ul>
          <li><input type="checkbox" id="c1"> เอกสารวาระประชุม</li>
          <li><input type="checkbox"> โปรเจคเตอร์</li>
          <li><input type="checkbox"> แบบประเมิน</li>
        </ul>

        <h4 style="margin-top:8px">การแต่งกาย</h4>
        <div>👔 ชุดสูท/เชิ้ต หรือชุดข้าราชการครูตามประกาศ</div>
        <div style="margin-top:10px">
          <button style="background:var(--green-2);border:0;padding:8px 12px;border-radius:12px;cursor:pointer" onclick="confirmActivity()">ยืนยันทำแล้ว</button>
        </div>
      </div>
    </div>

  </div>

  <div class="floating-nav" role="navigation" aria-label="เมนูหลัก">
    <div class="nav-item active" title="Home">🏠</div>
    <div class="nav-item" title="Calendar">📆</div>
    <div class="nav-item" title="Duties">✅</div>
    <div class="nav-item" title="Dress">👗</div>
    <div class="nav-item" title="Announce">📣</div>
    <div class="nav-item" title="Profile">👩‍🏫</div>
  </div>

  <script>
    // Sample interactive behaviors for mockup
    document.querySelectorAll('.confirmBtn').forEach(btn=>{
      btn.addEventListener('click', (e)=>{
        const id = e.target.dataset.id;
        e.target.textContent = '✔️ ยืนยันแล้ว';
        e.target.disabled = true;
        e.target.style.opacity = 0.7;
        // Save locally (demo)
        localStorage.setItem('duty-'+id, JSON.stringify({done:true, at:Date.now()}));
        alert('บันทึกการยืนยันหน้าที่เรียบร้อย 🎉');
      });
    });

    // Modal open (simulate clicking activity)
    document.querySelectorAll('.activity').forEach((el, idx)=>{
      el.addEventListener('click', (ev)=>{
        // ignore clicks on confirm buttons
        if(ev.target.tagName.toLowerCase() === 'button') return;
        openModal();
      });
    });

    function openModal(){
      const m = document.getElementById('modal');
      m.classList.add('open');
      m.setAttribute('aria-hidden','false');
    }
    function closeModal(){
      const m = document.getElementById('modal');
      m.classList.remove('open');
      m.setAttribute('aria-hidden','true');
    }

    function confirmActivity(){
      alert('ยืนยันการทำกิจกรรมแล้ว ✅ (ตัวอย่าง mockup)');
      closeModal();
    }

    // Floating nav click demo
    document.querySelectorAll('.nav-item').forEach((n,i)=>{
      n.addEventListener('click', ()=>{
        document.querySelectorAll('.nav-item').forEach(x=>x.classList.remove('active'));
        n.classList.add('active');
        // Could route to different views; here show alert for demo
        const labels = ['หน้าแรก','ปฏิทิน','หน้าที่','การแต่งกาย','ประกาศ','โปรไฟล์'];
        alert('ไปยัง: ' + labels[i] + ' (ตัวอย่าง)');
      });
    });

    // Notification demo (Browser)
    document.getElementById('testNotif').addEventListener('click', async ()=>{
      if(!("Notification" in window)){
        alert('เบราว์เซอร์ไม่รองรับ Notifications API');
        return;
      }
      if(Notification.permission === 'default') {
        await Notification.requestPermission();
      }
      if(Notification.permission === 'granted'){
        new Notification('เตือนความจำจาก School Planner', {
          body: 'เตือน: ประชุมครู 09:00 วันนี้ 🎉',
          icon: ''
        });
      } else {
        alert('อนุญาตการแจ้งเตือนในเบราว์เซอร์เพื่อรับ notifications จริง');
      }
    });

    // Announcement btn opens modal with simple message
    document.getElementById('announceBtn').addEventListener('click', ()=>{
      alert('ประกาศล่าสุด: โปรดเตรียมเอกสารสำหรับค่ายวิทย์ 📎');
    });

    document.getElementById('notifBtn').addEventListener('click', ()=>{
      alert('ไม่มีแจ้งเตือนใหม่ 🎈');
    });

    document.getElementById('viewProfile').addEventListener('click', ()=>{
      alert('เปิดหน้าโปรไฟล์ (ตัวอย่าง mockup) 👩‍🏫');
    });

    // small accessibility: escape closes modal
    document.addEventListener('keydown', (e)=>{
      if(e.key === 'Escape') closeModal();
    });
  </script>
</body>
</html>
