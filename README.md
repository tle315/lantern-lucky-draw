<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
  <meta name="theme-color" content="#F6F1E8" />
  <title>PandaGoldenEar Lucky Draw</title>
  <style>
    :root{
      --bg:#F6F1E8;
      --card:#ffffffcc;
      --ink:#141414;
      --muted:#6b6b6b;
      --line:#e6d9c8;
      --gold:#caa35a;
      --red:#9a3b2f;
      --green:#2f7a4a;
      --shadow: 0 10px 30px rgba(20,20,20,.06);
      --radius: 28px;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji","Segoe UI Emoji";
      background: radial-gradient(1200px 600px at 50% -10%, #f5e7cf 0%, var(--bg) 55%);
      color:var(--ink);
      line-height:1.35;
    }
    a{ color: inherit; text-decoration: none; }
    a:hover{ text-decoration: underline; }

    .wrap{ max-width: 980px; margin: 0 auto; padding: 22px 16px 34px; }
    .shell{
      background: linear-gradient(180deg, #fff9f0 0%, #fff8f3 55%, #fff 120%);
      border: 1px solid var(--line);
      border-radius: 36px;
      box-shadow: var(--shadow);
      padding: 18px;
      overflow:hidden;
    }
    .center{ text-align:center; }
    .topTag{
      display:inline-flex; align-items:center; gap:10px;
      padding:10px 16px; border-radius:999px;
      background:#f3e7d3; border:1px solid #e7d2b4;
      color:#6a4f25; font-weight:800;
      margin: 0 auto 12px;
    }
    .titleRow{
      display:flex; align-items:center; justify-content:center;
      gap:14px; margin-top:2px;
    }
    .fu{
      width:56px;height:56px; border-radius:16px;
      background: radial-gradient(circle at 30% 30%, #c84a3b 0%, #8e2f26 70%);
      display:grid; place-items:center;
      box-shadow: 0 8px 18px rgba(154,59,47,.18);
      color:#ffd67a; font-weight:900; font-size:28px;
      transform: translateY(-2px);
      flex: 0 0 auto;
    }
    h1{
      font-size: clamp(34px, 5vw, 62px);
      margin: 10px 0 6px;
      letter-spacing: -1px;
      user-select:none;
      -webkit-user-select:none;
      -webkit-touch-callout:none;
    }
    .sub{
      font-size: clamp(15px, 2.2vw, 20px);
      color: var(--muted);
      margin: 0 0 10px;
      font-weight: 650;
    }

    .hint{
      margin: 10px auto 14px;
      max-width: 820px;
      padding: 12px 14px;
      border-radius: 18px;
      border: 1px dashed #d9c3a4;
      background: #fff7ea;
      color:#6a4f25;
      font-weight:800;
      line-height:1.35;
    }
    .hintSmall{
      display:block;
      font-weight:750;
      color:#6a4f25;
      opacity:.9;
      margin-top:6px;
      font-size: 13px;
    }
    .hintLinks{
      display:inline-flex;
      gap:10px;
      flex-wrap:wrap;
      justify-content:center;
      margin-left: 6px;
    }
    .hintLink{
      display:inline-flex;
      align-items:center;
      gap:6px;
      padding:6px 10px;
      border-radius:999px;
      border:1px solid #e6d9c8;
      background:#fff;
      font-weight:900;
    }

    .playedBadge{
      display:none;
      margin: 12px auto 0;
      max-width: 860px;
      padding: 12px 14px;
      border-radius: 16px;
      border: 1px solid #cfe7d6;
      background: #ecfff0;
      color: var(--green);
      font-weight: 900;
      text-align:center;
    }

    /* Wheel */
    .wheelWrap{
      margin: 12px auto 10px;
      display:flex;
      flex-direction:column;
      align-items:center;
      gap:10px;
    }
    .wheelStage{
      position: relative;
      width: min(340px, 86vw);
      aspect-ratio: 1/1;
      display:grid;
      place-items:center;
      user-select:none;
      -webkit-user-select:none;
    }
    canvas#wheel{
      width: 100%;
      height: 100%;
      border-radius: 999px;
      background: #fff;
      border: 1px solid var(--line);
      box-shadow: 0 14px 30px rgba(20,20,20,.08);
      transform: rotate(0deg);
    }
    .pointer{
      position:absolute;
      top: -6px;
      left: 50%;
      transform: translateX(-50%);
      width: 0; height: 0;
      border-left: 14px solid transparent;
      border-right: 14px solid transparent;
      border-bottom: 22px solid #7a2f27;
      filter: drop-shadow(0 6px 10px rgba(0,0,0,.12));
      z-index: 3;
    }
    .centerBtn{
      position:absolute;
      width: 46%;
      aspect-ratio: 1/1;
      border-radius: 999px;
      border: 0;
      cursor: pointer;
      display:grid;
      place-items:center;
      gap:6px;
      color:#fff;
      background: radial-gradient(circle at 30% 30%, #c07b73 0%, #9a5b54 70%);
      box-shadow: 0 18px 36px rgba(154,91,84,.25);
      z-index: 4;
      font-weight: 1000;
      letter-spacing: .2px;
      transition: transform .08s ease, filter .12s ease;
    }
    .centerBtn:active{ transform: translateY(1px) scale(.995); }
    .centerBtn[disabled]{ opacity:.55; cursor:not-allowed; box-shadow:none; }
    .centerBtn span{ font-size: 22px; }
    .centerBtn small{
      font-size: 12px;
      font-weight: 850;
      opacity: .92;
    }

    /* Result card */
    .card{
      margin: 14px auto 10px;
      border-radius: var(--radius);
      border: 1px solid var(--line);
      background: var(--card);
      box-shadow: 0 12px 26px rgba(20,20,20,.05);
      padding: 18px 16px;
      max-width: 860px;
      transition: transform .18s ease, box-shadow .18s ease;
    }
    .card.winner{
      box-shadow: 0 16px 40px rgba(154,59,47,.10);
      border-color:#e7caa0;
      background: linear-gradient(180deg, #fffdf6 0%, #fff 100%);
    }
    @keyframes pop {
      0% { transform: translateY(6px) scale(.985); }
      55% { transform: translateY(-2px) scale(1.01); }
      100% { transform: translateY(0) scale(1); }
    }
    .card.pop { animation: pop .36s ease-out; }

    @keyframes pulseGlow{
      0% { box-shadow: 0 0 0 0 rgba(47,122,74,.18); }
      70%{ box-shadow: 0 0 0 12px rgba(47,122,74,0); }
      100%{ box-shadow: 0 0 0 0 rgba(47,122,74,0); }
    }
    .claimPulse{ animation: pulseGlow 1.2s ease-out infinite; }

    .resultTag{
      display:flex;
      justify-content:space-between;
      align-items:center;
      gap:12px;
      flex-wrap:wrap;
      margin-bottom: 8px;
    }
    .pill{
      display:inline-flex;
      align-items:center;
      gap:10px;
      padding: 10px 14px;
      border-radius: 999px;
      border: 1px solid #d9c3a4;
      background: #fff;
      font-weight: 900;
      color:#6a4f25;
    }
    .pill.green{
      border-color:#cfe7d6;
      background:#ecfff0;
      color: var(--green);
    }
    .big{
      font-size: clamp(30px, 4.2vw, 52px);
      margin: 10px 0 0;
      font-weight: 1000;
      letter-spacing: -.8px;
      color:#7a2f27;
    }
    .small{
      margin: 10px 0 2px;
      color: var(--muted);
      font-weight: 650;
      font-size: 15px;
    }
    .toast{
      margin: 10px auto 0;
      max-width: 860px;
      text-align:center;
      color:#8a6a3a;
      font-weight:800;
      font-size: 14px;
      min-height: 20px;
    }
    .footerNote{
      margin-top: 14px;
      color:#7a7a7a;
      text-align:center;
      font-weight:800;
      font-size: 18px;
      padding-bottom: 6px;
    }

    /* Staff modal */
    .modalMask{
      position:fixed; inset:0;
      background: rgba(0,0,0,.28);
      display:none;
      align-items:center;
      justify-content:center;
      padding: 18px;
      z-index: 9999;
    }
    .modal{
      width: min(520px, 100%);
      background: #fff;
      border-radius: 20px;
      border: 1px solid #eee;
      box-shadow: 0 18px 60px rgba(0,0,0,.18);
      padding: 16px;
      text-align:left;
    }
    .modal h3{ margin: 0 0 8px; font-size: 18px; letter-spacing: -.2px; }
    .modal p{ margin: 0 0 12px; color:#555; font-weight: 650; font-size: 14px; line-height:1.35; }
    .row{ display:flex; gap:10px; align-items:center; flex-wrap:wrap; }
    .input{
      flex: 1 1 220px;
      padding: 12px 12px;
      border-radius: 14px;
      border: 1px solid #ddd;
      font-size: 16px;
      font-weight: 900;
      letter-spacing: .4px;
      outline:none;
    }
    .miniBtn{
      padding: 12px 14px;
      border-radius: 14px;
      border: 1px solid #ddd;
      background:#fff;
      cursor:pointer;
      font-weight: 900;
      font-size: 14px;
    }
    .miniBtn.danger{ border-color:#f0c7c3; background:#fff2f2; color:#8e2f26; }
    .modalNote{ margin-top:10px; color:#7a7a7a; font-size: 12px; font-weight: 650; }

    @media (max-width: 520px){
      .shell{ padding: 14px; border-radius: 28px; }
      .fu{ width:52px;height:52px; border-radius: 16px; font-size: 26px; }
      .card{ padding: 16px 14px; border-radius: 22px; }
      .footerNote{ font-size: 16px; }
      .titleRow{ gap: 12px; }
      .hint{ font-size: 14px; }
      .hintLink{ font-size: 13px; }
    }
  </style>
</head>

<body>
  <div class="wrap">
    <div class="shell">
      <div class="center">
        <div class="topTag">🏮 Lantern Festival Special</div>

        <div class="titleRow">
          <div class="fu">福</div>
          <div>
            <!-- Long-press this title for staff reset -->
            <h1 id="titleHold">PandaGoldenEar Lucky Draw</h1>
            <p class="sub">Tap <b>Spin</b> to reveal your surprise.</p>
          </div>
        </div>

        <!-- Follow reminder (not gating) -->
        <div class="hint" id="followHint">
          📸 Don’t forget to follow us —
          <span class="hintLinks">
            <a class="hintLink" href="https://www.instagram.com/pandagoldenear/" target="_blank" rel="noopener noreferrer">Instagram</a>
            <a class="hintLink" href="https://www.facebook.com/pandagoldenear" target="_blank" rel="noopener noreferrer">Facebook</a>
            <a class="hintLink" href="https://www.tiktok.com/" target="_blank" rel="noopener noreferrer">TikTok</a>
          </span>
          <span class="hintSmall">Follow any ONE platform to stay updated 😉</span>
        </div>

        <div class="playedBadge" id="playedBadge">✅ Already played on this device</div>

        <!-- Wheel -->
        <div class="wheelWrap">
          <div class="wheelStage" aria-label="Lucky draw wheel">
            <div class="pointer" aria-hidden="true"></div>
            <canvas id="wheel" width="600" height="600"></canvas>
            <button id="spinBtn" class="centerBtn" type="button">
              <span>🎉 Spin</span>
              <small>tap to spin</small>
            </button>
          </div>
          <div class="toast" id="toast"></div>
        </div>

        <!-- Result -->
        <div class="card" id="resultCard" style="display:none;">
          <div class="resultTag">
            <span class="pill" id="resultTypePill">RESULT</span>
            <span class="pill green" id="claimPill" style="display:none;">🎁 Show this screen to claim</span>
          </div>

          <div class="center">
            <div class="small" id="resultLabel">YOU GOT</div>
            <div class="big" id="resultText">...</div>
            <div class="small" id="resultHelp" style="display:none;">If you win a prize, show this screen to our staff to claim.</div>
          </div>
        </div>

        <div class="footerNote">Thanks for joining — see you at our dumpling food truck!</div>
      </div>
    </div>
  </div>

  <!-- Staff modal -->
  <div class="modalMask" id="modalMask" role="dialog" aria-modal="true">
    <div class="modal">
      <h3>Staff Panel</h3>
      <p>To reset this device, type <b>RESET</b> and tap <b>Reset device</b>.</p>
      <div class="row">
        <input class="input" id="resetInput" placeholder="Type RESET" autocapitalize="characters" />
        <button class="miniBtn danger" id="resetBtn">Reset device</button>
        <button class="miniBtn" id="closeModalBtn">Close</button>
      </div>
      <div class="modalNote">Tip: long-press the title for 3 seconds to open this panel.</div>
    </div>
  </div>

  <script>
    // ====== CONFIG: your published CSVs ======
    const POOL_CSV_URL = "https://docs.google.com/spreadsheets/d/e/2PACX-1vR1Of71IvsS43kx9oDtQjWMeQDCNFHBw9FQ83YX6VFA2-iS7hOKYRyvrGkGYfsnCirFyzoO8oWe6vZk/pub?gid=0&single=true&output=csv";
    const BLESSINGS_CSV_URL = "https://docs.google.com/spreadsheets/d/e/2PACX-1vR1Of71IvsS43kx9oDtQjWMeQDCNFHBw9FQ83YX6VFA2-iS7hOKYRyvrGkGYfsnCirFyzoO8oWe6vZk/pub?gid=931297523&single=true&output=csv";

    // Local device limit
    const PLAY_KEY = "pge_lucky_draw_played_v2";

    const el = (id) => document.getElementById(id);

    const spinBtn = el("spinBtn");
    const toast = el("toast");
    const wheelCanvas = el("wheel");
    const ctx = wheelCanvas.getContext("2d");

    const resultCard = el("resultCard");
    const resultText = el("resultText");
    const resultHelp = el("resultHelp");
    const claimPill = el("claimPill");
    const resultTypePill = el("resultTypePill");
    const playedBadge = el("playedBadge");

    // staff modal
    const titleHold = el("titleHold");
    const modalMask = el("modalMask");
    const resetInput = el("resetInput");
    const resetBtn = el("resetBtn");
    const closeModalBtn = el("closeModalBtn");

    let poolRows = null;
    let blessingRows = null;

    // wheel state
    let wheelItems = []; // {label, type}
    let currentRotation = 0; // radians

    function setToast(msg){ toast.textContent = msg || ""; }

    function safeBool(v){
      if (v == null) return false;
      const s = String(v).trim().toLowerCase();
      return s === "true" || s === "1" || s === "yes";
    }

    function toNum(v, fallback = 0){
      const n = Number(String(v).trim());
      return Number.isFinite(n) ? n : fallback;
    }

    // Minimal CSV parser (handles quoted commas/newlines)
    function parseCSV(text){
      const rows = [];
      let row = [];
      let cur = "";
      let inQuotes = false;

      for (let i=0; i<text.length; i++){
        const ch = text[i];
        const next = text[i+1];

        if (inQuotes){
          if (ch === '"' && next === '"'){ cur += '"'; i++; }
          else if (ch === '"'){ inQuotes = false; }
          else { cur += ch; }
        } else {
          if (ch === '"'){ inQuotes = true; }
          else if (ch === ","){ row.push(cur); cur=""; }
          else if (ch === "\n"){
            row.push(cur); cur="";
            if (row.some(x => String(x).trim() !== "")) rows.push(row);
            row = [];
          } else if (ch === "\r"){
            // ignore
          } else {
            cur += ch;
          }
        }
      }
      row.push(cur);
      if (row.some(x => String(x).trim() !== "")) rows.push(row);

      if (rows.length === 0) return [];

      const headers = rows[0].map(h => String(h).trim());
      const data = rows.slice(1).map(r => {
        const obj = {};
        headers.forEach((h, idx) => obj[h] = (r[idx] ?? "").trim());
        return obj;
      });
      return data;
    }

    async function fetchCSV(url){
      const res = await fetch(url, { cache: "no-store" });
      if (!res.ok) throw new Error("Failed to load CSV");
      const txt = await res.text();
      return parseCSV(txt);
    }

    async function ensureDataLoaded(){
      if (!poolRows) poolRows = await fetchCSV(POOL_CSV_URL);
      if (!blessingRows) blessingRows = await fetchCSV(BLESSINGS_CSV_URL);
    }

    function buildWeightedBag(rows){
      // prize, weight, remaining_auto, type, active_auto
      const bag = [];
      for (const r of rows){
        const active = safeBool(r.active_auto ?? r.active);
        const remaining = toNum(r.remaining_auto ?? r.remaining, 0);
        const w = toNum(r.weight, 0);
        const label = (r.prize ?? "").trim();
        const type = (r.type ?? "prize").trim().toLowerCase();

        if (!active) continue;
        if (!label) continue;
        if (remaining <= 0) continue;
        if (w <= 0) continue;

        bag.push({ label, type, weight: w });
      }
      return bag;
    }

    function pickWeighted(items){
      const total = items.reduce((s,x)=>s+x.weight, 0);
      if (total <= 0) return null;
      let r = Math.random() * total;
      for (const it of items){
        r -= it.weight;
        if (r <= 0) return it;
      }
      return items[items.length - 1];
    }

    function pickBlessing(blessRows){
      // blessing, weight, active
      const candidates = [];
      for (const r of blessRows){
        const active = safeBool(r.active);
        const text = (r.blessing ?? "").trim();
        const w = toNum(r.weight, 1);
        if (!active) continue;
        if (!text) continue;
        candidates.push({ text, weight: w > 0 ? w : 1 });
      }
      if (candidates.length === 0) return "Good luck is coming your way :)";
      const picked = pickWeighted(candidates.map(x => ({ label:x.text, type:"blessing", weight:x.weight })));
      return picked?.label ?? "Good luck is coming your way :)";
    }

    function resetResultCardEffects(){
      resultCard.classList.remove("winner","pop");
      claimPill.classList.remove("claimPulse");
    }

    function showResult({ type, text }){
      resultCard.style.display = "";
      resultText.textContent = text;

      resetResultCardEffects();
      void resultCard.offsetWidth;

      if (type === "blessing"){
        resultTypePill.textContent = "BLESSING ✨";
        claimPill.style.display = "none";
        resultHelp.style.display = "none";
        resultText.style.color = "#141414";
      } else {
        resultTypePill.textContent = "YOU WON 🎉";
        claimPill.style.display = "";
        resultHelp.style.display = "";
        resultText.style.color = "#7a2f27";

        resultCard.classList.add("winner","pop");
        claimPill.classList.add("claimPulse");
      }

      setTimeout(() => {
        resultCard.scrollIntoView({ behavior:"smooth", block:"center" });
      }, 80);
    }

    function setPlayedUI(){
      playedBadge.style.display = "";
      spinBtn.disabled = true;
      setToast("Thanks! One play per device.");
    }

    function clearPlayedUI(){
      playedBadge.style.display = "none";
      spinBtn.disabled = false;
      setToast("");
      resultCard.style.display = "none";
      resetResultCardEffects();
    }

    function isPlayed(){ return localStorage.getItem(PLAY_KEY) === "1"; }
    function markPlayed(){ localStorage.setItem(PLAY_KEY, "1"); }
    function unmarkPlayed(){ localStorage.removeItem(PLAY_KEY); }

    // ===== Wheel rendering =====
    function normalizeAngle(rad){
      const twoPI = Math.PI * 2;
      rad = rad % twoPI;
      return rad < 0 ? rad + twoPI : rad;
    }

    function truncateLabel(s, max=14){
      s = String(s || "").trim();
      return s.length > max ? (s.slice(0, max-1) + "…") : s;
    }

    function drawWheel(items, rotationRad){
      const w = wheelCanvas.width, h = wheelCanvas.height;
      const cx = w/2, cy = h/2;
      const r = Math.min(cx, cy) - 12;

      ctx.clearRect(0,0,w,h);

      // background
      ctx.save();
      ctx.beginPath();
      ctx.arc(cx,cy,r+6,0,Math.PI*2);
      ctx.fillStyle = "#fff";
      ctx.fill();
      ctx.restore();

      if (!items || items.length === 0){
        ctx.save();
        ctx.translate(cx, cy);
        ctx.fillStyle = "#888";
        ctx.font = "900 22px system-ui";
        ctx.textAlign = "center";
        ctx.fillText("Loading…", 0, 8);
        ctx.restore();
        return;
      }

      const n = items.length;
      const twoPI = Math.PI * 2;
      const step = twoPI / n;

      // palette (soft)
      const colors = ["#fff2e6","#fff7ea","#f7f7ff","#f2fff4","#fffdf6","#f0fbff","#fff0f6","#f7fff0"];

      ctx.save();
      ctx.translate(cx, cy);
      ctx.rotate(rotationRad);

      for (let i=0; i<n; i++){
        const a0 = i * step;
        const a1 = a0 + step;

        // slice
        ctx.beginPath();
        ctx.moveTo(0,0);
        ctx.arc(0,0,r,a0,a1);
        ctx.closePath();
        ctx.fillStyle = colors[i % colors.length];
        ctx.fill();

        // border line
        ctx.strokeStyle = "#e6d9c8";
        ctx.lineWidth = 2;
        ctx.stroke();

        // text
        const mid = (a0+a1)/2;
        ctx.save();
        ctx.rotate(mid);
        ctx.translate(r*0.62, 0);
        ctx.rotate(Math.PI/2);
        ctx.fillStyle = "#6a4f25";
        ctx.font = "900 18px system-ui";
        ctx.textAlign = "center";
        ctx.fillText(truncateLabel(items[i].label, 16), 0, 6);
        ctx.restore();
      }

      // center ring
      ctx.beginPath();
      ctx.arc(0,0,r*0.18,0,twoPI);
      ctx.fillStyle = "#ffffff";
      ctx.fill();
      ctx.strokeStyle = "#e6d9c8";
      ctx.lineWidth = 2;
      ctx.stroke();

      ctx.restore();
    }

    function buildWheelItemsFromPool(pool){
      // Visual wheel is equal segments (for fun).
      // It shows available prizes + one "Blessing" segment.
      const uniques = [];
      const seen = new Set();
      for (const r of pool){
        const active = safeBool(r.active_auto ?? r.active);
        const remaining = toNum(r.remaining_auto ?? r.remaining, 0);
        const label = (r.prize ?? "").trim();
        const type = (r.type ?? "prize").trim().toLowerCase();

        if (!active) continue;
        if (remaining <= 0) continue;
        if (!label) continue;

        const key = type + "::" + label;
        if (seen.has(key)) continue;
        seen.add(key);
        uniques.push({ label, type });
      }

      // ensure we have a blessing slice (even if pool already has "blessing" row)
      const hasBless = uniques.some(x => x.type === "blessing");
      if (!hasBless){
        uniques.push({ label: "Blessing", type: "blessing" });
      }
      // cap to avoid a crazy wheel (optional)
      return uniques.slice(0, 10); // adjust if you want more
    }

    // ===== Spin animation to land on selected item =====
    let isSpinning = false;

    function spinToIndex(targetIndex, n){
      return new Promise((resolve) => {
        const twoPI = Math.PI * 2;
        const step = twoPI / n;

        // pointer is at "top" (12 o'clock). With our drawing rotation,
        // the segment at angle 0 starts at 3 o'clock; so we align using offset.
        // We want the center of target segment to align at -90deg (top).
        const targetCenter = (targetIndex + 0.5) * step;
        const desired = (-Math.PI/2) - targetCenter; // radians

        const start = currentRotation;
        const extraTurns = twoPI * (5 + Math.floor(Math.random()*2)); // 5-6 turns
        const end = desired + extraTurns;

        const duration = 2400 + Math.random()*500;
        const t0 = performance.now();

        function easeOutCubic(t){ return 1 - Math.pow(1-t, 3); }

        function tick(now){
          const p = Math.min(1, (now - t0) / duration);
          const e = easeOutCubic(p);
          currentRotation = start + (end - start) * e;
          drawWheel(wheelItems, currentRotation);

          if (p < 1) requestAnimationFrame(tick);
          else {
            currentRotation = normalizeAngle(currentRotation);
            drawWheel(wheelItems, currentRotation);
            resolve();
          }
        }
        requestAnimationFrame(tick);
      });
    }

    async function onSpin(){
      if (isSpinning) return;
      isSpinning = true;

      try{
        setToast("Loading prizes…");
        spinBtn.disabled = true;

        await ensureDataLoaded();

        // Build weighted bag for real outcome
        const bag = buildWeightedBag(poolRows);
        if (bag.length === 0){
          setToast("No prizes available right now. Please try later.");
          spinBtn.disabled = false;
          isSpinning = false;
          return;
        }

        // Build wheel visuals (equal segments)
        wheelItems = buildWheelItemsFromPool(poolRows);
        if (wheelItems.length < 2){
          wheelItems = [...wheelItems, { label:"Blessing", type:"blessing" }];
        }
        drawWheel(wheelItems, currentRotation);

        setToast("Spinning…");

        // Pick the real outcome
        const picked = pickWeighted(bag);
        if (!picked){
          setToast("Spin failed. Please try again.");
          spinBtn.disabled = false;
          isSpinning = false;
          return;
        }

        // Map outcome to a wheel index:
        // - If prize: find same label
        // - If blessing: land on "Blessing" slice
        let targetIndex = 0;
        if ((picked.type || "").toLowerCase() === "blessing"){
          targetIndex = Math.max(0, wheelItems.findIndex(x => x.type === "blessing"));
          if (targetIndex < 0) targetIndex = 0;
        } else {
          const idx = wheelItems.findIndex(x => x.label === picked.label);
          targetIndex = idx >= 0 ? idx : 0;
        }

        // Animate wheel to target index
        await spinToIndex(targetIndex, wheelItems.length);

        // Then show result
        if ((picked.type || "").toLowerCase() === "blessing"){
          const msg = pickBlessing(blessingRows);
          showResult({ type: "blessing", text: msg });
        } else {
          showResult({ type: "prize", text: picked.label });
        }

        markPlayed();
        setPlayedUI();
      } catch(err){
        console.error(err);
        setToast("Error loading data. Check your Google Sheet publish settings.");
        spinBtn.disabled = false;
      } finally {
        isSpinning = false;
      }
    }

    // ===== Staff modal (hidden) =====
    function openStaffModal(){
      modalMask.style.display = "flex";
      resetInput.value = "";
      setTimeout(() => resetInput.focus(), 50);
    }
    function closeStaffModal(){
      modalMask.style.display = "none";
      resetInput.value = "";
    }

    closeModalBtn.addEventListener("click", closeStaffModal);
    modalMask.addEventListener("click", (e) => { if (e.target === modalMask) closeStaffModal(); });

    resetBtn.addEventListener("click", () => {
      const v = String(resetInput.value || "").trim().toUpperCase();
      if (v !== "RESET"){
        resetInput.focus();
        resetInput.select?.();
        return;
      }
      unmarkPlayed();
      closeStaffModal();
      clearPlayedUI();
      setToast("Device reset ✅ You can spin again.");
    });

    // Long-press detection (3s)
    let holdTimer = null;
    const HOLD_MS = 3000;

    function startHold(){
      if (holdTimer) return;
      holdTimer = setTimeout(() => {
        holdTimer = null;
        openStaffModal();
      }, HOLD_MS);
    }
    function cancelHold(){
      if (holdTimer){
        clearTimeout(holdTimer);
        holdTimer = null;
      }
    }

    titleHold.addEventListener("touchstart", () => startHold(), { passive:true });
    titleHold.addEventListener("touchend", cancelHold);
    titleHold.addEventListener("touchcancel", cancelHold);
    titleHold.addEventListener("mousedown", startHold);
    titleHold.addEventListener("mouseup", cancelHold);
    titleHold.addEventListener("mouseleave", cancelHold);

    // Init
    (function init(){
      // placeholder wheel
      wheelItems = [{label:"Loading…", type:"info"}];
      drawWheel(wheelItems, currentRotation);

      // preload async (doesn't block)
      ensureDataLoaded().then(() => {
        wheelItems = buildWheelItemsFromPool(poolRows);
        drawWheel(wheelItems, currentRotation);
      }).catch(()=>{});

      if (isPlayed()){
        setPlayedUI();
      } else {
        setToast("");
        spinBtn.disabled = false;
      }

      spinBtn.addEventListener("click", () => {
        if (isPlayed()) return;
        onSpin();
      });
    })();
  </script>
</body>
</html>
