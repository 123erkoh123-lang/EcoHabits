<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>EcoHabit</title>

  <style>
    :root{
      --bg:#0b0f0c;
      --card:#111827;
      --card2:#0f172a;
      --border:#1f2937;
      --text:#e5e7eb;
      --muted:#9ca3af;
      --green:#22c55e;
      --green2:#16a34a;
      --danger:#ef4444;
      --shadow: 0 18px 40px rgba(0,0,0,.55);
      --r: 18px;
    }

    *{ box-sizing:border-box; }

    body{
      margin:0;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      background: radial-gradient(1200px 600px at 20% 0%, rgba(34,197,94,.15), transparent 60%),
                  radial-gradient(900px 500px at 90% 10%, rgba(34,197,94,.10), transparent 55%),
                  var(--bg);
      color:var(--text);
      min-height:100vh;
    }

    .wrap{
      max-width: 980px;
      margin: 0 auto;
      padding: 18px 14px 36px;
    }

    /* ===== NAV ===== */
    .topbar{
      display:flex;
      align-items:center;
      gap:12px;
      padding:14px 16px;
      background: rgba(17,24,39,.7);
      border:1px solid var(--border);
      border-radius: var(--r);
      box-shadow: var(--shadow);
      backdrop-filter: blur(10px);
      position: sticky;
      top: 10px;
      z-index: 20;
    }
    .brand{
      display:flex;
      align-items:center;
      gap:10px;
      font-weight: 800;
      letter-spacing: .3px;
      white-space: nowrap;
    }
    .brand .dot{
      width:10px;height:10px;border-radius:999px;background:var(--green);
      box-shadow: 0 0 0 4px rgba(34,197,94,.15);
    }
    .spacer{ flex:1; }
    .pill{
      font-size:12px;
      color:var(--muted);
      border:1px solid var(--border);
      padding:6px 10px;
      border-radius:999px;
      background: rgba(2,6,23,.45);
      max-width: 48vw;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
    .btn{
      border:none;
      background: linear-gradient(135deg, var(--green), var(--green2));
      color:#052e16;
      font-weight: 800;
      padding:10px 14px;
      border-radius: 12px;
      cursor:pointer;
      transition: transform .05s ease, filter .15s ease;
    }
    .btn:hover{ filter: brightness(1.05); }
    .btn:active{ transform: translateY(1px); }
    .btn.ghost{
      background: transparent;
      color: var(--text);
      border: 1px solid var(--border);
      font-weight: 700;
    }
    .btn.danger{
      background: #7f1d1d;
      color:#fecaca;
      border: 1px solid #991b1b;
    }

    /* ===== LAYOUT ===== */
    .grid{
      display:grid;
      grid-template-columns: 1.12fr .88fr;
      gap: 16px;
      margin-top: 16px;
      align-items: start;
    }
    @media (max-width: 920px){
      .grid{ grid-template-columns: 1fr; }
    }

    .card{
      background: rgba(17,24,39,.78);
      border:1px solid var(--border);
      border-radius: var(--r);
      box-shadow: var(--shadow);
      padding: 16px;
      backdrop-filter: blur(10px);
    }

    h1,h2,h3{ margin:0; }
    .title{
      font-size: 22px;
      line-height: 1.2;
      margin-bottom: 6px;
    }
    .sub{
      color: var(--muted);
      font-size: 14px;
      margin-bottom: 10px;
    }

    /* ===== AUTH ===== */
    .field{
      display:grid;
      gap:8px;
      margin-top: 10px;
    }
    .label{
      font-size: 12px;
      color: var(--muted);
    }
    .input{
      width:100%;
      padding: 12px 12px;
      border-radius: 14px;
      border: 1px solid var(--border);
      background: rgba(2,6,23,.7);
      color: var(--text);
      outline: none;
    }
    .input:focus{
      border-color: rgba(34,197,94,.9);
      box-shadow: 0 0 0 4px rgba(34,197,94,.12);
    }

    .msg{
      margin-top: 10px;
      font-size: 13px;
      color: var(--danger);
      min-height: 18px;
    }

    /* ===== HABITS ===== */
    .row{
      display:flex;
      gap: 10px;
      flex-wrap: wrap;
      align-items: end;
      margin-top: 10px;
    }
    .dateBox{
      flex: 1;
      min-width: 220px;
    }
    .dateBox .input{ padding: 10px 12px; }
    .hintline{
      font-size: 12px;
      color: var(--muted);
      margin-top: 6px;
    }

    .habit{
      display:flex;
      align-items:center;
      gap:12px;
      padding: 12px;
      border-radius: 16px;
      border: 1px solid var(--border);
      background: rgba(2,6,23,.45);
      cursor:pointer;
      user-select:none;
      transition: border-color .15s ease, transform .05s ease;
      margin-top: 10px;
    }
    .habit:hover{ border-color: rgba(34,197,94,.7); }
    .habit:active{ transform: translateY(1px); }
    .habit input{
      width: 20px;
      height: 20px;
      accent-color: var(--green);
      cursor:pointer;
    }
    .habit .t{
      display:flex;
      flex-direction:column;
      gap:2px;
    }
    .habit .t b{ font-size: 14px; }
    .habit .t span{ font-size: 12px; color: var(--muted); }

    .actions{
      display:flex;
      gap:10px;
      margin-top: 14px;
      flex-wrap:wrap;
    }
    .actions .btn{ flex:1; }

    /* ===== RESULT ===== */
    .result{
      margin-top: 14px;
      padding: 14px;
      border-radius: 16px;
      border: 1px solid rgba(34,197,94,.35);
      background: rgba(2,44,34,.65);
      display:none;
    }
    .result ul{ margin: 8px 0 0; padding-left: 18px; }
    .result li{ margin: 6px 0; }
    .ok{
      color: #86efac;
      font-weight: 700;
    }

    /* ===== RIGHT PANEL ===== */
    .mini{
      display:grid;
      gap:10px;
    }
    .stat{
      border:1px solid var(--border);
      background: rgba(2,6,23,.45);
      border-radius: 16px;
      padding: 12px;
    }
    .stat .k{ color: var(--muted); font-size: 12px; }
    .stat .v{ font-size: 18px; font-weight: 900; margin-top: 2px; }

    .hint{
      color: var(--muted);
      font-size: 13px;
      line-height: 1.35;
    }

    /* ===== 7 DAYS TABLE ===== */
    .tableWrap{
      margin-top: 12px;
      border:1px solid var(--border);
      border-radius: 16px;
      overflow:hidden;
      background: rgba(2,6,23,.35);
    }
    .trow{
      display:grid;
      grid-template-columns: 120px 1fr 1fr 1fr 1fr;
      gap: 8px;
      padding: 10px 12px;
      align-items:center;
      border-top: 1px solid rgba(31,41,55,.7);
      font-size: 13px;
    }
    .trow.head{
      background: rgba(17,24,39,.65);
      border-top: none;
      font-weight: 800;
      color: var(--muted);
      font-size: 12px;
    }
    .badge{
      display:inline-flex;
      align-items:center;
      justify-content:center;
      min-width: 34px;
      padding: 4px 8px;
      border-radius: 999px;
      border:1px solid var(--border);
      background: rgba(2,6,23,.55);
      font-weight: 800;
    }
    .yes{ border-color: rgba(34,197,94,.55); }
    .no{ opacity:.7; }

    /* ===== MOBILE UX ===== */
    @media (max-width: 520px){
      .wrap{ padding: 14px 12px 90px; }
      .topbar{ padding: 12px 12px; gap:10px; }
      .btn{ padding: 10px 12px; border-radius: 12px; }
      .title{ font-size: 20px; }
      .trow{ grid-template-columns: 92px 1fr 1fr 1fr 1fr; font-size: 12px; padding: 10px; }
      .dateBox{ min-width: 100%; }
    }

    /* Sticky actions bar for mobile */
    .mobileBar{
      display:none;
      position: fixed;
      left: 0; right: 0; bottom: 0;
      padding: 10px 12px;
      background: rgba(2,6,23,.85);
      border-top: 1px solid var(--border);
      backdrop-filter: blur(10px);
      z-index: 50;
    }
    .mobileBar .actions{ margin:0; }
    @media (max-width: 520px){
      .mobileBar{ display:block; }
      .desktopActions{ display:none; }
    }
  </style>
</head>

<body>
  <div class="wrap">

    <div class="topbar">
      <div class="brand">
        <span class="dot"></span>
        <span>EcoHabit</span>
      </div>
      <div class="spacer"></div>
      <div class="pill" id="userPill">Гость</div>
      <button class="btn danger" id="logoutBtn" style="display:none;">Выйти</button>
    </div>

    <!-- AUTH CARD -->
    <div class="card" id="authCard">
      <div class="title">Вход / Регистрация</div>
      <div class="sub">Для хакатона: демо-авторизация в браузере</div>

      <div class="field">
        <div class="label">Email</div>
        <input class="input" id="email" placeholder="example@mail.com" />
      </div>

      <div class="field">
        <div class="label">Пароль</div>
        <input class="input" id="password" type="password" placeholder="минимум 4 символа" />
      </div>

      <div class="actions">
        <button class="btn" id="loginBtn">Войти / Зарегистрироваться</button>
        <button class="btn ghost" id="demoBtn">Демо-вход</button>
      </div>

      <div class="msg" id="authMsg"></div>
    </div>

    <!-- APP -->
    <div class="grid" id="appGrid" style="display:none;">
      <div class="card">
        <div class="title">Привычки и эффект</div>
        <div class="sub">Отметь действия — сохраним их на выбранную дату и покажем статистику за 7 дней</div>

        <div class="row">
          <div class="dateBox">
            <div class="label">Дата</div>
            <input class="input" id="dayInput" type="date" />
            <div class="hintline">Можно выбрать прошлый день и отметить задним числом</div>
          </div>
          <button class="btn ghost" id="todayBtn">Сегодня</button>
        </div>

        <label class="habit" for="water">
          <input type="checkbox" id="water" />
          <div class="t">
            <b>💧 Сэкономил воду</b>
            <span>закрывал кран, короткий душ</span>
          </div>
        </label>

        <label class="habit" for="plastic">
          <input type="checkbox" id="plastic" />
          <div class="t">
            <b>🧴 Отказался от пластика</b>
            <span>многоразовая бутылка/сумка</span>
          </div>
        </label>

        <label class="habit" for="recycle">
          <input type="checkbox" id="recycle" />
          <div class="t">
            <b>♻️ Сортировал мусор</b>
            <span>бумага/пластик/стекло отдельно</span>
          </div>
        </label>

        <label class="habit" for="energy">
          <input type="checkbox" id="energy" />
          <div class="t">
            <b>⚡ Экономил электроэнергию</b>
            <span>выключал свет, заряжал рационально</span>
          </div>
        </label>

        <!-- desktop actions (hidden on mobile) -->
        <div class="actions desktopActions">
          <button class="btn" id="calcBtn">Сохранить и показать эффект</button>
          <button class="btn ghost" id="resetBtn">Сбросить</button>
        </div>

        <div class="msg" id="appMsg"></div>
        <div class="result" id="result"></div>
      </div>

      <div class="card mini">
        <div class="stat">
          <div class="k">Сегодня: вода (оценка)</div>
          <div class="v" id="statWater">0 л</div>
        </div>
        <div class="stat">
          <div class="k">Сегодня: пластик</div>
          <div class="v" id="statPlastic">0 шт</div>
        </div>
        <div class="stat">
          <div class="k">Сегодня: энергия</div>
          <div class="v" id="statEnergy">0 кВт⋅ч</div>
        </div>
        <div class="stat">
          <div class="k">Сегодня: сортировка</div>
          <div class="v" id="statRecycle">Нет</div>
        </div>

        <div class="stat">
          <div class="k">Итоги за 7 дней</div>
          <div class="v" id="weekSummary">—</div>
          <div class="hint" id="weekHint" style="margin-top:6px;"></div>
        </div>

        <div class="card" style="padding:12px; background: rgba(2,6,23,.35); border-radius: 16px;">
          <div class="k" style="color:var(--muted); font-size:12px; font-weight:800;">Последние 7 дней</div>

          <div class="tableWrap" id="weekTable">
            <div class="trow head">
              <div>Дата</div>
              <div>💧</div>
              <div>🧴</div>
              <div>♻️</div>
              <div>⚡</div>
            </div>
            <!-- rows injected -->
          </div>

          <div class="hint" style="margin-top:10px;">
            Подсказка: отметь привычки на “Сегодня”, потом посмотри как растёт статистика недели.
          </div>
        </div>
      </div>
    </div>

  </div>

  <!-- mobile bottom bar -->
  <div class="mobileBar" id="mobileBar" style="display:none;">
    <div class="actions">
      <button class="btn" id="calcBtnM">Сохранить</button>
      <button class="btn ghost" id="resetBtnM">Сброс</button>
    </div>
  </div>

  <script>
    // --- helpers ---
    const $ = (id) => document.getElementById(id);

    const safeParse = (s, fallback) => {
      try { return JSON.parse(s); } catch { return fallback; }
    };

    const setText = (id, text) => { const el = $(id); if (el) el.textContent = text || ""; };
    const show = (el, on) => { if (el) el.style.display = on ? "" : "none"; };

    function todayISO() {
      const d = new Date();
      const pad = (n) => String(n).padStart(2, "0");
      return `${d.getFullYear()}-${pad(d.getMonth()+1)}-${pad(d.getDate())}`;
    }

    function addDaysISO(iso, delta) {
      const d = new Date(iso + "T00:00:00");
      d.setDate(d.getDate() + delta);
      const pad = (n) => String(n).padStart(2, "0");
      return `${d.getFullYear()}-${pad(d.getMonth()+1)}-${pad(d.getDate())}`;
    }

    // --- auth storage ---
    const USERS_KEY = "ecohabit_users";
    const CUR_KEY = "ecohabit_current_user";

    function getUsers() {
      return safeParse(localStorage.getItem(USERS_KEY) || "{}", {});
    }
    function saveUsers(users) {
      localStorage.setItem(USERS_KEY, JSON.stringify(users));
    }
    function getCurrentUser() {
      return localStorage.getItem(CUR_KEY) || "";
    }
    function setCurrentUser(email) {
      localStorage.setItem(CUR_KEY, email);
    }
    function clearCurrentUser() {
      localStorage.removeItem(CUR_KEY);
    }

    // --- entries per user ---
    function entriesKey(email){
      return `ecohabit_entries__${email}`;
    }

    function getEntries(email){
      return safeParse(localStorage.getItem(entriesKey(email)) || "{}", {});
    }

    function saveEntries(email, entries){
      localStorage.setItem(entriesKey(email), JSON.stringify(entries));
    }

    function getSelectedDay(){
      return ($("dayInput")?.value || todayISO());
    }

    function setSelectedDay(iso){
      const inp = $("dayInput");
      if (inp) inp.value = iso;
    }

    function readChecks(){
      return {
        water: Boolean($("water")?.checked),
        plastic: Boolean($("plastic")?.checked),
        recycle: Boolean($("recycle")?.checked),
        energy: Boolean($("energy")?.checked),
      };
    }

    function writeChecks(data){
      if ($("water")) $("water").checked = Boolean(data?.water);
      if ($("plastic")) $("plastic").checked = Boolean(data?.plastic);
      if ($("recycle")) $("recycle").checked = Boolean(data?.recycle);
      if ($("energy")) $("energy").checked = Boolean(data?.energy);
    }

    function loadDayToUI(){
      const email = getCurrentUser();
      if (!email) return;

      const day = getSelectedDay();
      const entries = getEntries(email);
      const dayEntry = entries[day] || null;

      writeChecks(dayEntry);
      updateStats();         // today stats (based on current UI)
      hideResult();
      setText("appMsg", "");
    }

    function persistSelectedDay(){
      const email = getCurrentUser();
      if (!email) return;

      const day = getSelectedDay();
      const entries = getEntries(email);

      entries[day] = {
        ...readChecks(),
        savedAt: new Date().toISOString(),
      };

      // Можно чистить всё старше 30 дней, чтобы локальное хранилище не разрасталось
      // (не обязательно, но полезно)
      const cutoff = addDaysISO(todayISO(), -30);
      Object.keys(entries).forEach(k => { if (k < cutoff) delete entries[k]; });

      saveEntries(email, entries);
    }

    // --- UI states ---
    function renderAuthState() {
      const email = getCurrentUser();
      const loggedIn = Boolean(email);

      show($("authCard"), !loggedIn);
      show($("appGrid"), loggedIn);
      show($("logoutBtn"), loggedIn);
      show($("mobileBar"), loggedIn); // на мобиле
      $("userPill").textContent = loggedIn ? email : "Гость";

      setText("authMsg", "");
      setText("appMsg", "");
      hideResult();

      if (loggedIn) {
        // дата по умолчанию = сегодня
        setSelectedDay(todayISO());
        loadDayToUI();
        render7Days();
      }
    }

    function hideResult() {
      const r = $("result");
      if (r) { r.style.display = "none"; r.innerHTML = ""; }
    }

    function resetChecksOnlyUI() {
      ["water","plastic","recycle","energy"].forEach(id => {
        const el = $(id);
        if (el) el.checked = false;
      });
      updateStats();
      hideResult();
      setText("appMsg", "");
    }

    // --- logic ---
    function loginOrSignup() {
      setText("authMsg", "");

      const email = ($("email").value || "").trim().toLowerCase();
      const pass  = ($("password").value || "").trim();

      if (!email || !pass) { setText("authMsg", "Введите email и пароль"); return; }
      if (pass.length < 4) { setText("authMsg", "Пароль слишком короткий (мин. 4)"); return; }
      if (!email.includes("@")) { setText("authMsg", "Email выглядит неверно"); return; }

      const users = getUsers();

      if (!users[email]) {
        users[email] = pass;
        saveUsers(users);
      }

      if (users[email] !== pass) {
        setText("authMsg", "Неверный пароль");
        return;
      }

      setCurrentUser(email);
      renderAuthState();
    }

    function demoLogin() {
      const users = getUsers();
      const email = "demo@ecohabit.kz";
      if (!users[email]) { users[email] = "demo"; saveUsers(users); }
      setCurrentUser(email);
      renderAuthState();
    }

    function logout() {
      clearCurrentUser();
      renderAuthState();
    }

    function updateStats() {
      const c = readChecks();
      $("statWater").textContent = (c.water ? 6 : 0) + " л";
      $("statPlastic").textContent = (c.plastic ? 1 : 0) + " шт";
      $("statEnergy").textContent = (c.energy ? 0.5 : 0) + " кВт⋅ч";
      $("statRecycle").textContent = c.recycle ? "Да" : "Нет";
    }

    function calculateAndSave() {
      setText("appMsg", "");

      const day = getSelectedDay();
      const c = readChecks();

      // сохраняем всегда (даже если всё false — чтобы “сброс” фиксировался)
      persistSelectedDay();
      render7Days();

      if (!c.water && !c.plastic && !c.recycle && !c.energy) {
        setText("appMsg", "Отмечено: 0 привычек. Можно выбрать другую дату и заполнить 🙂");
        hideResult();
        return;
      }

      let html = `<h3>🌍 Эффект за ${day}</h3><ul>`;
      if (c.water) html += "<li>💧 −6 литров воды</li>";
      if (c.plastic) html += "<li>🧴 −1 пластиковая бутылка</li>";
      if (c.recycle) html += "<li>♻️ Сортировка — меньше отходов на свалках</li>";
      if (c.energy) html += "<li>⚡ −0.5 кВт⋅ч энергии</li>";
      html += "</ul><p><b class='ok'>Отлично! Продолжай 💚</b></p>";

      const res = $("result");
      res.innerHTML = html;
      res.style.display = "block";
    }

    function resetForDay() {
      // сброс = очистка чекбоксов + сохранение пустого дня
      resetChecksOnlyUI();
      persistSelectedDay();
      render7Days();
      setText("appMsg", "Сброшено и сохранено для выбранной даты.");
    }

    // --- 7 days rendering ---
    function getLast7DaysList(baseDayISO){
      // baseDay = сегодня, показываем 7 дней включая сегодня: [today-6 ... today]
      const out = [];
      for (let i = 6; i >= 0; i--) out.push(addDaysISO(baseDayISO, -i));
      return out;
    }

    function render7Days(){
      const email = getCurrentUser();
      if (!email) return;

      const entries = getEntries(email);
      const list = getLast7DaysList(todayISO());

      // table rows
      const table = $("weekTable");
      if (table) {
        // remove old rows (everything except header)
        const old = Array.from(table.querySelectorAll(".trow.data"));
        old.forEach(n => n.remove());

        list.forEach(day => {
          const d = entries[day] || null;
          const w = Boolean(d?.water);
          const p = Boolean(d?.plastic);
          const r = Boolean(d?.recycle);
          const e = Boolean(d?.energy);

          const row = document.createElement("div");
          row.className = "trow data";

          const cellDate = document.createElement("div");
          cellDate.textContent = day.slice(5); // MM-DD (короче)
          cellDate.style.fontWeight = "900";

          const c1 = document.createElement("div");
          c1.innerHTML = `<span class="badge ${w ? "yes" : "no"}">${w ? "Да" : "—"}</span>`;

          const c2 = document.createElement("div");
          c2.innerHTML = `<span class="badge ${p ? "yes" : "no"}">${p ? "Да" : "—"}</span>`;

          const c3 = document.createElement("div");
          c3.innerHTML = `<span class="badge ${r ? "yes" : "no"}">${r ? "Да" : "—"}</span>`;

          const c4 = document.createElement("div");
          c4.innerHTML = `<span class="badge ${e ? "yes" : "no"}">${e ? "Да" : "—"}</span>`;

          row.appendChild(cellDate);
          row.appendChild(c1);
          row.appendChild(c2);
          row.appendChild(c3);
          row.appendChild(c4);

          table.appendChild(row);
        });
      }

      // weekly totals
      let totalWaterL = 0;
      let totalPlastic = 0;
      let totalEnergy = 0;
      let recycleDays = 0;
      let habitMarks = 0;

      list.forEach(day => {
        const d = entries[day] || null;
        const w = Boolean(d?.water);
        const p = Boolean(d?.plastic);
        const r = Boolean(d?.recycle);
        const e = Boolean(d?.energy);

        if (w) { totalWaterL += 6; habitMarks++; }
        if (p) { totalPlastic += 1; habitMarks++; }
        if (e) { totalEnergy += 0.5; habitMarks++; }
        if (r) { recycleDays += 1; habitMarks++; }
      });

      $("weekSummary").textContent = `${habitMarks} отметок`;
      $("weekHint").innerHTML =
        `💧 ${totalWaterL} л • 🧴 ${totalPlastic} шт • ⚡ ${totalEnergy.toFixed(1)} кВт⋅ч<br/>♻️ сортировка: ${recycleDays} из 7 дней`;
    }

    // --- init safely after DOM loaded ---
    window.addEventListener("DOMContentLoaded", () => {
      // wire buttons
      $("loginBtn").addEventListener("click", loginOrSignup);
      $("demoBtn").addEventListener("click", demoLogin);
      $("logoutBtn").addEventListener("click", logout);

      $("calcBtn").addEventListener("click", calculateAndSave);
      $("resetBtn").addEventListener("click", resetForDay);

      // mobile bar buttons
      $("calcBtnM").addEventListener("click", calculateAndSave);
      $("resetBtnM").addEventListener("click", resetForDay);

      // date handlers
      $("todayBtn").addEventListener("click", () => {
        setSelectedDay(todayISO());
        loadDayToUI();
      });
      $("dayInput").addEventListener("change", () => {
        loadDayToUI();
      });

      // update stats & autosave on changes
      ["water","plastic","recycle","energy"].forEach(id => {
        $(id).addEventListener("change", () => {
          updateStats();
          // автосохранение, чтобы не потерять отметки
          persistSelectedDay();
          render7Days();
        });
      });

      // initial render
      renderAuthState();
      updateStats();
      render7Days();
    });
  </script>
</body>
</html>
