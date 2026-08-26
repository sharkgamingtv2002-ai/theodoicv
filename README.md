<!doctype html>
<html lang="vi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta name="theme-color" content="#0b1020" />
  <title>Nhật ký hằng ngày</title>
  <style>
    :root {
      --ink: #edf3ff;
      --muted: #99a6bd;
      --line: rgba(174, 193, 226, .14);
      --surface: rgba(17, 25, 47, .82);
      --surface-2: rgba(28, 39, 67, .82);
      --navy: #0b1020;
      --blue: #7198ff;
      --blue-strong: #517df6;
      --mint: #4dd6b8;
      --amber: #f4bd58;
      --rose: #fb8293;
      --shadow: 0 18px 50px rgba(0, 0, 0, .24);
    }
    * { box-sizing: border-box; }
    html { color-scheme: dark; }
    body {
      margin: 0;
      min-width: 320px;
      color: var(--ink);
      background: var(--navy);
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      letter-spacing: -.01em;
    }
    body::before {
      position: fixed;
      z-index: -1;
      inset: 0;
      background: radial-gradient(circle at 14% 5%, rgba(89, 119, 244, .23), transparent 28rem),
                  radial-gradient(circle at 92% 30%, rgba(49, 198, 170, .13), transparent 25rem),
                  linear-gradient(135deg, #0b1020 0%, #111a34 100%);
      content: "";
    }
    button, input, textarea, select { font: inherit; }
    button { cursor: pointer; }
    .app { max-width: 1320px; margin: 0 auto; padding: 28px 28px 48px; }
    .topbar { display: flex; justify-content: space-between; align-items: center; gap: 20px; margin-bottom: 28px; }
    .brand { display: flex; align-items: center; gap: 12px; }
    .brand-mark { width: 39px; height: 39px; display: grid; place-items: center; border-radius: 13px; background: linear-gradient(145deg, #8ba8ff, #496ff0); box-shadow: 0 12px 30px rgba(80, 120, 245, .32); color: white; }
    .brand-mark svg { width: 22px; height: 22px; }
    .brand-name { margin: 0; font-size: 16px; font-weight: 760; letter-spacing: -.025em; }
    .brand-subtitle { margin: 2px 0 0; color: var(--muted); font-size: 12px; }
    .topbar-actions { display: flex; align-items: center; gap: 10px; }
    .today { display: inline-flex; align-items: center; gap: 8px; color: var(--muted); font-size: 13px; }
    .today::before { width: 7px; height: 7px; border-radius: 50%; background: var(--mint); box-shadow: 0 0 0 5px rgba(77, 214, 184, .12); content: ""; }
    .button { min-height: 42px; padding: 0 15px; display: inline-flex; align-items: center; justify-content: center; gap: 8px; border: 1px solid transparent; border-radius: 12px; color: var(--ink); background: transparent; font-weight: 680; font-size: 13px; transition: transform .15s, background .15s, border-color .15s; }
    .button:hover { transform: translateY(-1px); }
    .button-primary { background: var(--blue-strong); box-shadow: 0 8px 18px rgba(81, 125, 246, .26); }
    .button-primary:hover { background: #6389f8; }
    .button-quiet { border-color: var(--line); background: rgba(255,255,255,.025); color: #c6d1e8; }
    .button-quiet:hover { background: rgba(255,255,255,.075); }
    .button svg { width: 17px; height: 17px; }
    .hero { display: flex; justify-content: space-between; align-items: end; gap: 30px; padding: 26px 0 24px; }
    .eyebrow { margin: 0 0 7px; color: #aebfff; font-size: 12px; font-weight: 760; letter-spacing: .09em; text-transform: uppercase; }
    h1 { max-width: 650px; margin: 0; font-size: clamp(28px, 4vw, 42px); line-height: 1.08; letter-spacing: -.045em; }
    .intro { max-width: 460px; margin: 0 0 3px; color: var(--muted); font-size: 14px; line-height: 1.6; }
    .stat-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 14px; margin-bottom: 28px; }
    .stat { min-height: 126px; padding: 18px; border: 1px solid var(--line); border-radius: 17px; background: linear-gradient(145deg, rgba(31, 44, 77, .83), rgba(17, 25, 47, .76)); box-shadow: var(--shadow); }
    .stat-header { display: flex; justify-content: space-between; align-items: center; gap: 8px; color: var(--muted); font-size: 12px; }
    .stat-icon { width: 28px; height: 28px; display: grid; place-items: center; border-radius: 9px; background: rgba(119, 150, 255, .12); color: #a8bcff; }
    .stat-icon svg { width: 15px; height: 15px; }
    .stat-value { margin: 14px 0 3px; font-size: 31px; font-weight: 760; letter-spacing: -.045em; }
    .stat-detail { color: var(--muted); font-size: 12px; }
    .content-grid { display: grid; grid-template-columns: minmax(0, 1.8fr) minmax(290px, .8fr); align-items: start; gap: 18px; }
    .panel { overflow: hidden; border: 1px solid var(--line); border-radius: 18px; background: var(--surface); box-shadow: var(--shadow); }
    .panel-heading { padding: 19px 20px 16px; display: flex; justify-content: space-between; align-items: center; gap: 12px; border-bottom: 1px solid var(--line); }
    .panel-heading h2 { margin: 0; font-size: 16px; letter-spacing: -.025em; }
    .panel-heading p { margin: 4px 0 0; color: var(--muted); font-size: 12px; }
    .count { min-width: 27px; padding: 4px 8px; border-radius: 20px; color: #c9d5ee; background: rgba(118, 149, 255, .13); text-align: center; font-size: 12px; font-weight: 700; }
    .filters { padding: 14px 20px; display: flex; flex-wrap: wrap; gap: 9px; border-bottom: 1px solid var(--line); }
    .search { position: relative; flex: 1 1 185px; }
    .search svg { position: absolute; left: 12px; top: 11px; width: 16px; height: 16px; color: var(--muted); }
    input, textarea, select { width: 100%; outline: none; border: 1px solid rgba(170, 190, 226, .16); border-radius: 10px; color: var(--ink); background: rgba(255,255,255,.045); }
    input:focus, textarea:focus, select:focus { border-color: rgba(129, 157, 255, .75); box-shadow: 0 0 0 3px rgba(113, 152, 255, .15); }
    .search input { height: 39px; padding: 0 12px 0 36px; font-size: 13px; }
    select { min-width: 122px; height: 39px; padding: 0 30px 0 11px; color: #cad5e9; font-size: 13px; }
    option { color: #0b1020; }
    .report-list { min-height: 430px; }
    .report { padding: 16px 20px; display: grid; grid-template-columns: 12px minmax(0, 1fr) auto; gap: 13px; align-items: start; border-bottom: 1px solid var(--line); transition: background .15s; }
    .report:last-child { border-bottom: 0; }
    .report:hover { background: rgba(255,255,255,.028); }
    .status-dot { width: 9px; height: 9px; margin-top: 5px; border-radius: 50%; }
    .status-doing { background: var(--blue); box-shadow: 0 0 0 4px rgba(113, 152, 255, .11); }
    .status-done { background: var(--mint); box-shadow: 0 0 0 4px rgba(77, 214, 184, .11); }
    .status-blocked { background: var(--rose); box-shadow: 0 0 0 4px rgba(251, 130, 147, .11); }
    .report-title { margin: 0; color: #f0f5ff; font-size: 14px; font-weight: 700; line-height: 1.35; }
    .report-note { margin: 5px 0 0; color: var(--muted); font-size: 12px; line-height: 1.48; }
    .report-meta { margin-top: 10px; display: flex; flex-wrap: wrap; align-items: center; gap: 7px; color: #8997af; font-size: 11px; }
    .tag { padding: 3px 7px; border: 1px solid transparent; border-radius: 6px; font-weight: 700; font-size: 10px; letter-spacing: .015em; }
    .priority-high { color: #ffb1bc; border-color: rgba(251,130,147,.19); background: rgba(251,130,147,.1); }
    .priority-medium { color: #f6d18a; border-color: rgba(244,189,88,.18); background: rgba(244,189,88,.09); }
    .priority-low { color: #a8bcff; border-color: rgba(113,152,255,.17); background: rgba(113,152,255,.09); }
    .status-label { min-width: 78px; padding: 5px 8px; border: 0; border-radius: 7px; text-align: center; font-size: 10px; font-weight: 760; }
    .label-doing { color: #b8c8ff; background: rgba(113, 152, 255, .12); }
    .label-done { color: #8cedd8; background: rgba(77, 214, 184, .12); }
    .label-blocked { color: #ffb3bd; background: rgba(251, 130, 147, .12); }
    .empty { min-height: 300px; padding: 40px; display: grid; place-items: center; color: var(--muted); text-align: center; font-size: 13px; }
    .empty strong { display: block; margin-bottom: 5px; color: var(--ink); font-size: 15px; }
    .side-stack { display: grid; gap: 18px; }
    .progress-panel { padding: 20px; }
    .progress-panel h2 { margin: 0; font-size: 16px; }
    .progress-panel > p { margin: 5px 0 20px; color: var(--muted); font-size: 12px; }
    .progress-ring { --percent: 0; width: 148px; height: 148px; margin: 7px auto 20px; display: grid; place-items: center; border-radius: 50%; background: conic-gradient(var(--mint) calc(var(--percent) * 1%), rgba(255,255,255,.075) 0); }
    .progress-ring::before { width: 118px; height: 118px; border-radius: 50%; background: #151e3a; box-shadow: inset 0 0 18px rgba(0,0,0,.22); content: ""; grid-area: 1 / 1; }
    .progress-content { z-index: 1; grid-area: 1 / 1; text-align: center; }
    .progress-content strong { display: block; font-size: 27px; letter-spacing: -.04em; }
    .progress-content span { color: var(--muted); font-size: 11px; }
    .legend { display: grid; gap: 10px; }
    .legend-row { display: flex; align-items: center; justify-content: space-between; color: var(--muted); font-size: 12px; }
    .legend-name { display: flex; align-items: center; gap: 8px; }
    .legend-name i { width: 8px; height: 8px; display: inline-block; border-radius: 50%; }
    .legend-row b { color: #ced9ed; font-size: 12px; }
    .prompt-panel { padding: 20px; background: linear-gradient(150deg, rgba(92, 118, 237, .25), rgba(28, 39, 67, .77)); }
    .prompt-icon { width: 32px; height: 32px; margin-bottom: 13px; display: grid; place-items: center; border-radius: 10px; background: rgba(193,207,255,.13); color: #d8e1ff; }
    .prompt-icon svg { width: 18px; height: 18px; }
    .prompt-panel h2 { margin: 0; font-size: 15px; }
    .prompt-panel p { margin: 6px 0 16px; color: #becaeb; font-size: 12px; line-height: 1.5; }
    .small-button { min-height: 35px; padding: 0 11px; border-radius: 9px; font-size: 12px; }
    .modal-backdrop { position: fixed; z-index: 10; inset: 0; display: none; align-items: center; justify-content: center; padding: 20px; background: rgba(4, 7, 17, .7); backdrop-filter: blur(5px); }
    .modal-backdrop.open { display: flex; }
    .modal { width: min(560px, 100%); max-height: min(760px, 100%); overflow: auto; padding: 24px; border: 1px solid rgba(183, 199, 235, .2); border-radius: 19px; background: #151e3a; box-shadow: 0 30px 80px rgba(0,0,0,.48); }
    .modal-head { display: flex; align-items: flex-start; justify-content: space-between; gap: 16px; margin-bottom: 21px; }
    .modal h2 { margin: 0; font-size: 20px; letter-spacing: -.03em; }
    .modal-head p { margin: 4px 0 0; color: var(--muted); font-size: 12px; }
    .close { width: 32px; height: 32px; display: grid; place-items: center; border: 0; border-radius: 9px; color: var(--muted); background: rgba(255,255,255,.055); }
    .close:hover { color: white; background: rgba(255,255,255,.1); }
    .close svg { width: 18px; height: 18px; }
    .field { display: grid; gap: 7px; margin-bottom: 15px; }
    .field label { color: #c9d5ea; font-size: 12px; font-weight: 680; }
    .field input, .field textarea, .field select { padding: 10px 11px; font-size: 13px; }
    .field textarea { min-height: 92px; resize: vertical; line-height: 1.45; }
    .two-fields { display: grid; grid-template-columns: 1fr 1fr; gap: 13px; }
    .modal-actions { margin-top: 22px; display: flex; justify-content: flex-end; gap: 9px; }
    .toast { position: fixed; z-index: 20; right: 22px; bottom: 22px; transform: translateY(16px); padding: 11px 14px; border: 1px solid rgba(108, 232, 196, .26); border-radius: 11px; opacity: 0; color: #d5fff4; background: #173a36; box-shadow: var(--shadow); font-size: 13px; transition: opacity .2s, transform .2s; pointer-events: none; }
    .toast.show { transform: translateY(0); opacity: 1; }
    .auth-button { max-width: 185px; overflow: hidden; border-color: var(--line); background: rgba(255,255,255,.045); color: #d9e3f5; white-space: nowrap; text-overflow: ellipsis; }
    .auth-button.signed-in { border-color: rgba(77, 214, 184, .25); color: #a8f3e2; }
    @media (max-width: 920px) { .content-grid { grid-template-columns: 1fr; } .side-stack { grid-template-columns: 1fr 1fr; } }
    @media (max-width: 690px) { .app { padding: 20px 16px 36px; } .topbar { align-items: flex-start; } .today { display: none; } .hero { display: block; padding-top: 15px; } .intro { margin-top: 12px; } .stat-grid { grid-template-columns: 1fr 1fr; } .side-stack { grid-template-columns: 1fr; } .report { padding: 15px; grid-template-columns: 10px minmax(0,1fr); } .status-label { grid-column: 2; justify-self: start; } .panel-heading { padding: 17px 15px 14px; } .filters { padding: 12px 15px; } .topbar-actions .button-quiet { display: none; } .two-fields { grid-template-columns: 1fr; gap: 0; } }
  </style>
</head>
<body>
  <main class="app">
    <header class="topbar">
      <div class="brand">
        <div class="brand-mark" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M7 3v3M17 3v3M4 10h16M5 5h14a1 1 0 0 1 1 1v13a1 1 0 0 1-1 1H5a1 1 0 0 1-1-1V6a1 1 0 0 1 1-1Z"/><path d="M8 14h3M8 17h6"/></svg></div>
        <div><p class="brand-name">Nhật ký hằng ngày</p><p class="brand-subtitle">Theo dõi công việc, rõ tiến độ</p></div>
      </div>
      <div class="topbar-actions"><span class="today" id="todayLabel"></span><button class="button button-quiet" id="exportButton" title="Tải dữ liệu dạng CSV"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3v12M7 10l5 5 5-5M5 21h14"/></svg><span>Xuất CSV</span></button><button class="button auth-button" id="authButton" type="button">Đăng nhập Google</button><button class="button button-primary" id="openModal"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.3" stroke-linecap="round"><path d="M12 5v14M5 12h14"/></svg><span>Thêm báo cáo</span></button></div>
    </header>

    <section class="hero">
      <div><p class="eyebrow">Tổng quan hôm nay</p><h1>Công việc nào đang cần bạn chú ý?</h1></div>
      <p class="intro">Ghi nhanh việc đã làm, việc đang xử lý và các trở ngại để cả ngày làm việc luôn rõ ràng.</p>
    </section>

    <section class="stat-grid" aria-label="Tóm tắt báo cáo">
      <article class="stat"><div class="stat-header"><span>Tổng báo cáo</span><span class="stat-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M8 6h13M8 12h13M8 18h13M3 6h.01M3 12h.01M3 18h.01"/></svg></span></div><div class="stat-value" id="totalCount">0</div><div class="stat-detail">bản ghi trong nhật ký</div></article>
      <article class="stat"><div class="stat-header"><span>Đã hoàn thành</span><span class="stat-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="m5 12 4 4L19 6"/></svg></span></div><div class="stat-value" id="doneCount">0</div><div class="stat-detail" id="doneDetail">chưa có dữ liệu</div></article>
      <article class="stat"><div class="stat-header"><span>Đang thực hiện</span><span class="stat-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 6v6l4 2"/><circle cx="12" cy="12" r="9"/></svg></span></div><div class="stat-value" id="doingCount">0</div><div class="stat-detail">cần theo dõi tiếp</div></article>
      <article class="stat"><div class="stat-header"><span>Đang bị chặn</span><span class="stat-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 9v4M12 17h.01"/><path d="m10.3 3.2-8 14A2 2 0 0 0 4 20h16a2 2 0 0 0 1.7-2.8l-8-14a2 2 0 0 0-3.4 0Z"/></svg></span></div><div class="stat-value" id="blockedCount">0</div><div class="stat-detail">việc cần gỡ vướng</div></article>
    </section>

    <section class="content-grid">
      <section class="panel">
        <div class="panel-heading"><div><h2>Báo cáo gần đây</h2><p>Những cập nhật mới nhất của bạn</p></div><span class="count" id="visibleCount">0</span></div>
        <div class="filters"><div class="search"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="6"/><path d="m20 20-4.2-4.2"/></svg><input type="search" id="searchInput" placeholder="Tìm theo nội dung..." aria-label="Tìm báo cáo" /></div><select id="statusFilter" aria-label="Lọc theo trạng thái"><option value="all">Mọi trạng thái</option><option value="doing">Đang thực hiện</option><option value="done">Hoàn thành</option><option value="blocked">Bị chặn</option></select><select id="dateFilter" aria-label="Lọc theo thời gian"><option value="all">Mọi ngày</option><option value="today">Hôm nay</option><option value="week">7 ngày gần đây</option></select></div>
        <div class="report-list" id="reportList"></div>
      </section>

      <aside class="side-stack">
        <section class="panel progress-panel"><h2>Tiến độ hôm nay</h2><p>Dựa trên các báo cáo được tạo hôm nay</p><div class="progress-ring" id="progressRing"><div class="progress-content"><strong id="progressPercent">0%</strong><span>hoàn thành</span></div></div><div class="legend"><div class="legend-row"><span class="legend-name"><i style="background:var(--mint)"></i>Hoàn thành</span><b id="legendDone">0</b></div><div class="legend-row"><span class="legend-name"><i style="background:var(--blue)"></i>Đang thực hiện</span><b id="legendDoing">0</b></div><div class="legend-row"><span class="legend-name"><i style="background:var(--rose)"></i>Bị chặn</span><b id="legendBlocked">0</b></div></div></section>
        <section class="panel prompt-panel"><div class="prompt-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2a7 7 0 0 0-4 12.74V17a2 2 0 0 0 2 2h4a2 2 0 0 0 2-2v-2.26A7 7 0 0 0 12 2Z"/><path d="M9 22h6M9 14h6"/></svg></div><h2>Gợi ý báo cáo</h2><p>Viết ngắn theo công thức: Việc gì — kết quả — bước tiếp theo hoặc trở ngại.</p><button class="button button-quiet small-button" id="quickAdd">Ghi báo cáo hôm nay</button></section>
      </aside>
    </section>
  </main>

  <div class="modal-backdrop" id="modalBackdrop" role="presentation">
    <form class="modal" id="reportForm" aria-labelledby="formTitle">
      <div class="modal-head"><div><h2 id="formTitle">Báo cáo mới</h2><p>Thêm một cập nhật để theo dõi tiến độ.</p></div><button type="button" class="close" id="closeModal" aria-label="Đóng biểu mẫu"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="m6 6 12 12M18 6 6 18"/></svg></button></div>
      <div class="field"><label for="title">Bạn đã / đang làm gì?</label><input id="title" name="title" maxlength="120" placeholder="Ví dụ: Hoàn thiện bản đề xuất tháng 9" required autocomplete="off" /></div>
      <div class="field"><label for="note">Kết quả, bước tiếp theo hoặc trở ngại</label><textarea id="note" name="note" maxlength="500" placeholder="Ví dụ: Đã nhận phản hồi từ đội thiết kế; cần cập nhật số liệu trước 16:00."></textarea></div>
      <div class="two-fields"><div class="field"><label for="status">Trạng thái</label><select id="status" name="status"><option value="doing">Đang thực hiện</option><option value="done">Hoàn thành</option><option value="blocked">Bị chặn</option></select></div><div class="field"><label for="priority">Mức ưu tiên</label><select id="priority" name="priority"><option value="high">Cao</option><option value="medium" selected>Trung bình</option><option value="low">Thấp</option></select></div></div>
      <div class="field"><label for="date">Ngày báo cáo</label><input id="date" name="date" type="date" required /></div>
      <div class="modal-actions"><button class="button button-quiet" type="button" id="cancelModal">Hủy</button><button class="button button-primary" type="submit">Lưu báo cáo</button></div>
    </form>
  </div>
  <div class="toast" id="toast" role="status" aria-live="polite">Đã lưu báo cáo.</div>

  <script type="module">
    import { initializeApp } from 'https://www.gstatic.com/firebasejs/12.17.1/firebase-app.js';
    import { getAuth, GoogleAuthProvider, onAuthStateChanged, signInWithPopup, signOut } from 'https://www.gstatic.com/firebasejs/12.17.1/firebase-auth.js';
    import { getFirestore, addDoc, collection, onSnapshot, orderBy, query, serverTimestamp } from 'https://www.gstatic.com/firebasejs/12.17.1/firebase-firestore.js';

    const firebaseConfig = {
      apiKey: 'AIzaSyAmTqlscC6ZuXbp6-5il2lX09RDOjr_1O8',
      authDomain: 'tdcv-484ca.firebaseapp.com',
      projectId: 'tdcv-484ca',
      storageBucket: 'tdcv-484ca.firebasestorage.app',
      messagingSenderId: '811188902231',
      appId: '1:811188902231:web:dbe5f3378cc8877f988612',
      measurementId: 'G-8MH7QSRKXX'
    };

    const statusInfo = {
      doing: { label: 'Đang thực hiện', dot: 'status-doing', badge: 'label-doing' },
      done: { label: 'Hoàn thành', dot: 'status-done', badge: 'label-done' },
      blocked: { label: 'Bị chặn', dot: 'status-blocked', badge: 'label-blocked' }
    };
    const priorityInfo = {
      high: { label: 'Ưu tiên cao', className: 'priority-high' },
      medium: { label: 'Trung bình', className: 'priority-medium' },
      low: { label: 'Ưu tiên thấp', className: 'priority-low' }
    };
    const dateKey = (date = new Date()) => new Date(date).toLocaleDateString('en-CA');
    const now = new Date();
    const todayKey = dateKey(now);
    let reports = [];
    let currentUser = null;
    let auth;
    let db;

    const els = {
      list: document.getElementById('reportList'), search: document.getElementById('searchInput'), statusFilter: document.getElementById('statusFilter'), dateFilter: document.getElementById('dateFilter'), visibleCount: document.getElementById('visibleCount'), total: document.getElementById('totalCount'), done: document.getElementById('doneCount'), doing: document.getElementById('doingCount'), blocked: document.getElementById('blockedCount'), doneDetail: document.getElementById('doneDetail'), ring: document.getElementById('progressRing'), percent: document.getElementById('progressPercent'), legendDone: document.getElementById('legendDone'), legendDoing: document.getElementById('legendDoing'), legendBlocked: document.getElementById('legendBlocked'), modal: document.getElementById('modalBackdrop'), form: document.getElementById('reportForm'), date: document.getElementById('date'), toast: document.getElementById('toast'), authButton: document.getElementById('authButton')
    };
    document.getElementById('todayLabel').textContent = new Intl.DateTimeFormat('vi-VN', { weekday: 'long', day: 'numeric', month: 'long' }).format(now);
    els.date.value = todayKey;

    const escapeHtml = (text = '') => String(text).replace(/[&<>'"]/g, char => ({ '&':'&amp;', '<':'&lt;', '>':'&gt;', "'":'&#39;', '"':'&quot;' })[char]);
    const formatDate = (value) => new Intl.DateTimeFormat('vi-VN', { day: '2-digit', month: '2-digit', year: 'numeric' }).format(new Date(`${value}T12:00:00`));
    function showToast(message) { els.toast.textContent = message; els.toast.classList.add('show'); setTimeout(() => els.toast.classList.remove('show'), 3000); }
    function closeModal() { els.modal.classList.remove('open'); }
    function updateAuthUI() {
      if (currentUser) {
        const name = currentUser.displayName || currentUser.email || 'Đã đăng nhập';
        els.authButton.textContent = `${name} · Đăng xuất`;
        els.authButton.classList.add('signed-in');
        els.authButton.title = 'Đăng xuất';
      } else {
        els.authButton.textContent = 'Đăng nhập Google';
        els.authButton.classList.remove('signed-in');
        els.authButton.title = 'Đăng nhập để thêm báo cáo';
      }
    }
    async function signIn() {
      try { await signInWithPopup(auth, new GoogleAuthProvider()); }
      catch (error) { showToast(error.code === 'auth/popup-closed-by-user' ? 'Bạn đã đóng cửa sổ đăng nhập.' : 'Không thể đăng nhập. Hãy thử lại sau.'); }
    }
    function getVisibleReports() {
      const search = els.search.value.trim().toLocaleLowerCase('vi');
      const range = els.dateFilter.value;
      const weekAgo = new Date(now); weekAgo.setDate(now.getDate() - 6);
      const weekKey = dateKey(weekAgo);
      return reports.filter(report => {
        const textMatch = !search || `${report.title} ${report.note}`.toLocaleLowerCase('vi').includes(search);
        const statusMatch = els.statusFilter.value === 'all' || report.status === els.statusFilter.value;
        const dateMatch = range === 'all' || (range === 'today' && report.date === todayKey) || (range === 'week' && report.date >= weekKey && report.date <= todayKey);
        return textMatch && statusMatch && dateMatch;
      });
    }
    function renderReports() {
      const visible = getVisibleReports();
      els.visibleCount.textContent = visible.length;
      if (!visible.length) {
        els.list.innerHTML = '<div class="empty"><div><strong>Chưa có báo cáo</strong>Đăng nhập Google để thêm báo cáo đầu tiên cho cả nhóm.</div></div>';
        return;
      }
      els.list.innerHTML = visible.map(report => {
        const state = statusInfo[report.status];
        const priority = priorityInfo[report.priority];
        return `<article class="report"><span class="status-dot ${state.dot}" aria-hidden="true"></span><div><h3 class="report-title">${escapeHtml(report.title)}</h3>${report.note ? `<p class="report-note">${escapeHtml(report.note)}</p>` : ''}<div class="report-meta"><span class="tag ${priority.className}">${priority.label}</span><span>${formatDate(report.date)}</span><span>${escapeHtml(report.ownerName || 'Thành viên')}</span></div></div><span class="status-label ${state.badge}">${state.label}</span></article>`;
      }).join('');
    }
    function updateSummary() {
      const counts = { total: reports.length, done: reports.filter(r => r.status === 'done').length, doing: reports.filter(r => r.status === 'doing').length, blocked: reports.filter(r => r.status === 'blocked').length };
      els.total.textContent = counts.total; els.done.textContent = counts.done; els.doing.textContent = counts.doing; els.blocked.textContent = counts.blocked;
      els.doneDetail.textContent = counts.total ? `${Math.round(counts.done / counts.total * 100)}% tổng báo cáo` : 'chưa có dữ liệu';
      const today = reports.filter(r => r.date === todayKey);
      const todayCounts = { done: today.filter(r => r.status === 'done').length, doing: today.filter(r => r.status === 'doing').length, blocked: today.filter(r => r.status === 'blocked').length };
      const percent = today.length ? Math.round(todayCounts.done / today.length * 100) : 0;
      els.ring.style.setProperty('--percent', percent); els.percent.textContent = `${percent}%`;
      els.legendDone.textContent = todayCounts.done; els.legendDoing.textContent = todayCounts.doing; els.legendBlocked.textContent = todayCounts.blocked;
    }
    const render = () => { updateSummary(); renderReports(); };
    function openModal() {
      if (!currentUser) { showToast('Hãy đăng nhập Google trước khi thêm báo cáo.'); signIn(); return; }
      els.form.reset(); els.date.value = todayKey; els.modal.classList.add('open');
      setTimeout(() => document.getElementById('title').focus(), 30);
    }
    function listenForReports() {
      const reportsQuery = query(collection(db, 'reports'), orderBy('createdAt', 'desc'));
      onSnapshot(reportsQuery, snapshot => {
        reports = snapshot.docs.map(document => ({ id: document.id, ...document.data() }));
        render();
      }, () => showToast('Chưa tải được dữ liệu chung. Kiểm tra lại quy tắc Firestore.'));
    }
    document.getElementById('openModal').addEventListener('click', openModal);
    document.getElementById('quickAdd').addEventListener('click', openModal);
    document.getElementById('closeModal').addEventListener('click', closeModal);
    document.getElementById('cancelModal').addEventListener('click', closeModal);
    els.modal.addEventListener('click', event => { if (event.target === els.modal) closeModal(); });
    document.addEventListener('keydown', event => { if (event.key === 'Escape') closeModal(); });
    [els.search, els.statusFilter, els.dateFilter].forEach(input => input.addEventListener('input', renderReports));
    els.authButton.addEventListener('click', async () => { if (currentUser) await signOut(auth); else await signIn(); });
    els.form.addEventListener('submit', async event => {
      event.preventDefault();
      if (!currentUser) { closeModal(); await signIn(); return; }
      const data = new FormData(els.form);
      try {
        await addDoc(collection(db, 'reports'), { title: data.get('title').trim(), note: data.get('note').trim(), status: data.get('status'), priority: data.get('priority'), date: data.get('date'), ownerId: currentUser.uid, ownerName: currentUser.displayName || currentUser.email || 'Thành viên', createdAt: serverTimestamp() });
        closeModal(); showToast('Đã lưu báo cáo cho cả nhóm.');
      } catch { showToast('Không thể lưu báo cáo. Kiểm tra quyền Firestore.'); }
    });
    document.getElementById('exportButton').addEventListener('click', () => {
      const rows = [['Ngày', 'Công việc', 'Nội dung', 'Trạng thái', 'Ưu tiên', 'Người tạo'], ...reports.map(r => [r.date, r.title, r.note, statusInfo[r.status].label, priorityInfo[r.priority].label, r.ownerName || ''])];
      const csv = '\uFEFF' + rows.map(row => row.map(cell => `"${String(cell).replaceAll('"', '""')}"`).join(',')).join('\n');
      const url = URL.createObjectURL(new Blob([csv], { type: 'text/csv;charset=utf-8' }));
      const link = document.createElement('a'); link.href = url; link.download = `bao-cao-hang-ngay-${todayKey}.csv`; link.click(); URL.revokeObjectURL(url); showToast('Đã xuất tệp CSV.');
    });
    try {
      const app = initializeApp(firebaseConfig);
      auth = getAuth(app); db = getFirestore(app);
      onAuthStateChanged(auth, user => { currentUser = user; updateAuthUI(); });
      listenForReports(); render();
    } catch { render(); showToast('Không thể khởi tạo Firebase.'); }
  </script>
</body>
</html>
