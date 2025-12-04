<html ....>
<html lang="th">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>School Weekly Planner — Mockup</title>
  <style>
    :root{
      --bg:#f6f8fb; --card:#ffffff; --muted:#6b7280;
      --primary:#0b74de; --tag-meeting:#ffb86b; --tag-sports:#6bd3ff; --tag-acad:#9b8cff;
      font-family: Inter, Roboto, "Noto Sans Thai", Helvetica, Arial;
    }
    body{background:var(--bg); margin:0; color:#111; font-size:14px}
    .app{display:flex; min-height:100vh}
    .sidebar{width:220px; background:#fff; border-right:1px solid #e6e6ef; padding:20px; box-sizing:border-box}
    .sidebar h2{margin:0 0 12px 0; font-size:16px}
    .nav{list-style:none; padding:0; margin:12px 0}
    .nav li{padding:8px 10px; border-radius:6px; color:var(--muted)}
    .nav li.active{background:#f0f7ff; color:var(--primary)}
    .content{flex:1; padding:20px}
    .header{display:flex; justify-content:space-between; align-items:center; margin-bottom:18px}
    .header .left h1{margin:0; font-size:18px}
    .header .right{display:flex; gap:12px; align-items:center}
    .notif{position:relative}
    .notif .badge{position:absolute; top:-6px; right:-6px; background:#ff4d6d; color:white; font-size:12px; padding:3px 6px; border-radius:12px}
    .grid{display:grid; grid-template-columns: repeat(3, 1fr); gap:16px; margin-bottom:18px}
    .card{background:var(--card); padding:14px; border-radius:10px; box-shadow:0 1px 2px rgba(15,20,30,0.04)}
    .card h3{margin:0 0 10px 0; font-size:15px}
    .event-item{display:flex; justify-content:space-between; gap:10px; padding:8px 0; border-top:1px dashed #f0f0f3}
    .event-item:first-child{border-top:0}
    .tag{padding:4px 8px; border-radius:6px; font-size:12px; color:#fff}
    .tag.meeting{background:var(--tag-meeting)}
    .tag.sports{background:var(--tag-sports)}
    .mini-week{display:flex; gap:6px; margin-top:12px}
    .day{flex:1; background:#fbfcff; padding:8px; border-radius:6px; text-align:center}
    .day .dot{width:8px; height:8px; background:var(--primary); border-radius:50%; margin:6px auto 0}
    .calendar{margin-top:10px; background:var(--card); padding:12px; border-radius:10px}
    .week-grid{display:grid; grid-template-columns: repeat(7, 1fr); gap:8px}
    .day-cell{background:#fff; border-radius:8px; padding:8px; min-height:80px; box-shadow:inset 0 0 0 1px #f3f4f6}
    .evt{background:#eef6ff; padding:6px 8px; border-radius:6px; font-size:13px; margin-bottom:6px; display:flex; justify-content:space-between; align-items:center}
    .evt .who{font-size:12px; color:var(--muted)}
    .right-col{width:300px; margin-left:18px}
    .ann{background:#fff; padding:12px; border-radius:10px; margin-bottom:12px}
    .profile{background:#fff; padding:12px; border-radius:10px}
    /* responsive */
    @media (max-width:900px){
      .grid{grid-template-columns:1fr}
      .app{flex-direction:column}
      .sidebar{display:none}
      .right-col{display:none}
    }
  </style>
</head>
<body>
  <div class="app">
    <aside class="sidebar">
      <h2>School Weekly Planner</h2>
      <div class="muted">โรงเรียนตัวอย่าง</div>
      <ul class="nav">
        <li class="active">Dashboard</li>
        <li>Calendar</li>
        <li>Assignments</li>
        <li>Dress Code</li>
        <li>Announcements</li>
        <li>Notifications</li>
        <li>Profile</li>
      </ul>
    </aside>

    <main class="content">
      <div class="header">
        <div class="left">
          <h1>Dashboard — สัปดาห์ 1 ธ.ค. 2025</h1>
          <div style="color:var(--muted); font-size:13px">สวัสดี, ครูสมชาย — คุณมี 2 งานที่ยังไม่ยืนยัน</div>
        </div>
        <div class="right">
          <div class="notif">
            <button>🔔</button>
            <div class="badge">2</div>
          </div>
          <div><img src="" alt="avatar" style="width:36px;height:36px;border-radius:50%;background:#ddd"></div>
        </div>
      </div>

      <section class="grid">
        <div class="card">
          <h3>กิจกรรมวันนี้</h3>
          <div class="event-item">
            <div>
              <div style="font-weight:600">ประชุมคณะครู</div>
              <div style="color:var(--muted); font-size:13px">09:00 • ห้องประชุมใหญ่</div>
            </div>
            <div style="text-align:right">
              <div class="tag meeting">ประชุม</div>
              <div style="font-size:12px; color:var(--muted); margin-top:6px">ผู้รับผิดชอบ: ผอ.</div>
            </div>
          </div>
          <div class="event-item">
            <div>
              <div style="font-weight:600">คัดเลือกนักกีฬาระดับโรงเรียน</div>
              <div style="color:var(--muted); font-size:13px">13:00 • สนามกีฬา</div>
            </div>
            <div style="text-align:right">
              <div class="tag sports">กีฬา</div>
              <div style="font-size:12px; color:var(--muted); margin-top:6px">ผู้รับผิดชอบ: ครูอ้อย</div>
            </div>
          </div>
        </div>

        <div class="card">
          <h3>หน้าที่วันนี้</h3>
          <div style="padding:6px 0">
            <div style="display:flex; justify-content:space-between; align-items:center; padding:6px 0">
              <div>
                <div style="font-weight:600">ดูแลแถวหน้าเสาธง</div>
                <div style="font-size:12px; color:var(--muted)">06:45 • สนามหน้าอาคาร</div>
              </div>
              <div>
                <button style="background:#e6f7ee;border:1px solid #c5edd3;padding:6px 10px;border-radius:6px">ยืนยัน</button>
              </div>
            </div>
            <div style="display:flex; justify-content:space-between; align-items:center; padding:6px 0">
              <div>
                <div style="font-weight:600">จุดคัดกรองผู้ปกครอง</div>
                <div style="font-size:12px; color:var(--muted)">08:00 • ทางเข้า</div>
              </div>
              <div>
                <button style="background:#fff3cd;border:1px solid #ffeeba;padding:6px 10px;border-radius:6px">ขอเปลี่ยน</button>
              </div>
            </div>
          </div>
        </div>

        <div class="card">
          <h3>การแต่งกายวันนี้</h3>
          <div style="display:flex; gap:8px; align-items:center;">
            <div style="width:56px;height:56px;border-radius:8px;background:#fff;display:flex;align-items:center;justify-content:center">
              🎩
            </div>
            <div>
              <div style="font-weight:600">ชุดพิธี</div>
              <div style="color:var(--muted); font-size:13px">โปรดสวมเสื้อเชิ้ตสีขาว กระโปรง/กางเกงสีดำ</div>
            </div>
          </div>
        </div>
      </section>

      <div style="display:flex; gap:18px">
        <div style="flex:1">
          <div class="calendar card">
            <h3 style="margin-top:0">ปฏิทินสัปดาห์</h3>
            <div class="week-grid" aria-hidden="true">
              <div class="day-cell">
                <div style="font-weight:600">จันทร์<br><span style="color:var(--muted);font-size:12px">1 ธ.ค.</span></div>
                <div class="evt"><div>ประชุมคณะครู</div><div class="who">ผอ.</div></div>
                <div class="evt" style="background:#fff4e6"><div>อบรม ICT</div><div class="who">ครูเอ</div></div>
              </div>
              <div class="day-cell">
                <div style="font-weight:600">อังคาร<br><span style="color:var(--muted);font-size:12px">2 ธ.ค.</span></div>
              </div>
              <div class="day-cell">
                <div style="font-weight:600">พุธ<br><span style="color:var(--muted);font-size:12px">3 ธ.ค.</span></div>
                <div class="evt"><div>คัดเลือกนักกีฬา</div><div class="who">ครูอ้อย</div></div>
              </div>
              <div class="day-cell">
                <div style="font-weight:600">พฤหัส<br><span style="color:var(--muted);font-size:12px">4 ธ.ค.</span></div>
              </div>
              <div class="day-cell">
                <div style="font-weight:600">ศุกร์<br><span style="color:var(--muted);font-size:12px">5 ธ.ค.</span></div>
              </div>
              <div class="day-cell">
                <div style="font-weight:600">เสาร์<br><span style="color:var(--muted);font-size:12px">6 ธ.ค.</span></div>
              </div>
              <div class="day-cell">
                <div style="font-weight:600">อาทิตย์<br><span style="color:var(--muted);font-size:12px">7 ธ.ค.</span></div>
              </div>
            </div>
          </div>
        </div>

        <aside class="right-col">
          <div class="ann card">
            <h4 style="margin:0 0 8px 0">ประกาศล่าสุด</h4>
            <div style="font-size:13px; color:var(--muted)">- ปิดรับสมัครค่ายวิชาการ 4 ธ.ค. 10:00</div>
            <div style="font-size:13px; color:var(--muted); margin-top:8px">- แจ้งปรับตารางสอนชั่วคราว</div>
          </div>

          <div class="profile card">
            <div style="display:flex; gap:10px; align-items:center">
              <div style="width:56px;height:56px;border-radius:50%;background:#ddd"></div>
              <div>
                <div style="font-weight:600">ครูสมชาย ใจดี</div>
                <div style="font-size:13px;color:var(--muted)">ครูประจำชั้น ม.2/3</div>
                <div style="margin-top:8px"><button style="padding:6px 10px;border-radius:6px;background:#f0f7ff;border:1px solid #d6ecff">ดูโปรไฟล์</button></div>
              </div>
            </div>
          </div>
        </aside>
      </div>
    </main>
  </div>
</body>
</html>
