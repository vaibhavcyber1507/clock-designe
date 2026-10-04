# clock-designe
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Copenhagen Cyber Terminal | World Tourism Day</title>
  <link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap" rel="stylesheet" />
  <style>
    :root {
      --bg: #07090e;
      --red: #ff1e42;
      --neon-red: #ff3366;
      --white: #ffffff;
      --cyan: #00e5ff;
      --dim-border: rgba(255, 30, 66, 0.35);
    }

    * {
      box-sizing: border-box;
      user-select: none;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: var(--bg);
      color: #fff;
      font-family: 'Share Tech Mono', monospace;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
      padding: 20px;
    }

    /* Terminal HUD Box */
    .terminal-container {
      width: 100%;
      max-width: 900px;
      background: rgba(10, 13, 20, 0.95);
      border: 2px solid var(--red);
      box-shadow: 0 0 25px rgba(255, 30, 66, 0.4), inset 0 0 15px rgba(255, 30, 66, 0.15);
      padding: 24px;
      display: flex;
      flex-direction: column;
      gap: 20px;
      position: relative;
    }

    /* Scanline Overlay */
    .terminal-container::before {
      content: "";
      position: absolute;
      top: 0; left: 0; right: 0; bottom: 0;
      background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.3) 50%);
      background-size: 100% 4px;
      pointer-events: none;
      z-index: 5;
    }

    /* Upper-Left Cyber Watermark *//* Prominent Cyber Watermark - Bottom Right */
    .terminal-watermark {
      position: fixed;
      bottom: 55px;
      left: 60px;
      font-size: 1.2rem; /* Significantly larger */
      font-weight: bold;
      letter-spacing: 3px;
      color: rgba(255, 255, 255, 0.8); /* Much brighter and more visible */
      text-transform: uppercase;
      z-index: 10;
      pointer-events: none;
      text-shadow: 0 0 10px rgba(255, 30, 66, 0.6); /* Adds a red cyber glow */
    }
   
    /* Header Node Info */
    .hud-header {
      display: flex;
      justify-content: space-between;
      border-bottom: 1px solid var(--dim-border);
      padding-top: 6px;
      padding-bottom: 10px;
      font-size: 0.9rem;
      color: var(--neon-red);
      letter-spacing: 1px;
    }

    /* Mode Navigation */
    .mode-nav {
      display: flex;
      gap: 12px;
    }

    .tab-btn {
      flex: 1;
      padding: 10px;
      background: rgba(255, 30, 66, 0.08);
      border: 1px solid var(--dim-border);
      color: #ccc;
      font-family: inherit;
      font-size: 0.95rem;
      cursor: pointer;
      transition: all 0.2s ease;
      letter-spacing: 1px;
    }

    .tab-btn:hover {
      background: rgba(255, 30, 66, 0.25);
      color: #fff;
    }

    .tab-btn.active {
      background: var(--red);
      border-color: var(--neon-red);
      color: #fff;
      font-weight: bold;
      box-shadow: 0 0 12px var(--red);
    }

    /* Main Digital Readout */
    .display-box {
      border: 1px solid var(--dim-border);
      background: rgba(0, 0, 0, 0.6);
      padding: 30px 20px;
      text-align: center;
      position: relative;
    }

    .display-label {
      font-size: 0.85rem;
      color: #888;
      letter-spacing: 2px;
      margin-bottom: 10px;
    }

    .digital-counter {
      font-size: clamp(2.6rem, 7vw, 5.2rem);
      font-weight: bold;
      letter-spacing: 4px;
      color: var(--white);
      text-shadow: 0 0 12px rgba(255, 255, 255, 0.8), 0 0 24px var(--red);
    }

    .digital-counter span.ms {
      font-size: clamp(1.4rem, 4vw, 2.5rem);
      color: var(--neon-red);
    }

    /* Reflex Arena Box */
    .reflex-arena {
      height: 180px;
      border: 2px dashed var(--dim-border);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      cursor: pointer;
      transition: all 0.15s ease;
      background: rgba(0, 0, 0, 0.4);
    }

    .reflex-arena.standby {
      border-color: #ffaa00;
      color: #ffaa00;
      background: rgba(255, 170, 0, 0.08);
    }

    .reflex-arena.breach {
      background: var(--red) !important;
      border-color: #fff !important;
      color: #fff !important;
      box-shadow: 0 0 40px var(--red);
    }

    .arena-title {
      font-size: 1.4rem;
      letter-spacing: 3px;
      font-weight: bold;
    }

    .arena-subtitle {
      font-size: 0.85rem;
      margin-top: 6px;
      opacity: 0.8;
    }

    /* Button Controls */
    .btn-row {
      display: flex;
      gap: 12px;
    }

    .action-btn {
      flex: 1;
      padding: 12px;
      border: 1px solid var(--dim-border);
      background: transparent;
      color: #fff;
      font-family: inherit;
      font-size: 1rem;
      letter-spacing: 1px;
      cursor: pointer;
      transition: background 0.2s ease;
    }

    .action-btn:hover {
      background: rgba(255, 30, 66, 0.25);
    }

    /* Footer Terminal Log */
    .terminal-log {
      border-top: 1px solid var(--dim-border);
      padding-top: 10px;
      font-size: 0.8rem;
      color: #6d788d;
      display: flex;
      justify-content: space-between;
    }
  </style>
</head>
<body>

  <div class="terminal-container">
    <!-- Small Watermark in Upper Left Corner -->
    <div class="terminal-watermark">// CREATED  VAIBHAV KANOJIYA IoT-2</div>

    <!-- Header -->
    <div class="hud-header">
      <span>&gt; NODE: COPENHAGEN_DK // SECURE</span>
      <span>WORLD TOURISM DAY 2026</span>
    </div>

    <!-- Navigation -->
    <div class="mode-nav">
      <button class="tab-btn active" id="btnClock" onclick="setMode('clock')">[ SYSTEM CLOCK ]</button>
      <button class="tab-btn" id="btnStopwatch" onclick="setMode('stopwatch')">[ STOPWATCH ]</button>
      <button class="tab-btn" id="btnReflex" onclick="setMode('reflex')">[ REFLEX BREACH ]</button>
    </div>

    <!-- Clock / Stopwatch Display -->
    <div id="standardDisplay" class="display-box">
      <div class="display-label" id="displayLabel">SYSTEM REAL-TIME FEED (COPENHAGEN)</div>
      <div class="digital-counter" id="mainTime">00:00:00<span class="ms" id="msSub"></span></div>
    </div>

    <!-- Reflex Mode Display -->
    <div id="reflexDisplay" class="reflex-arena" style="display: none;" onclick="handleArenaClick()">
      <div class="arena-title" id="reflexStatus">PRESS [INITIATE] TO ARM</div>
      <div class="arena-subtitle" id="reflexHint">CLICK THIS BOX OR PRESS SPACE WHEN RED DETECTED</div>
    </div>

    <!-- Action Controls -->
    <div class="btn-row" id="controlRow" style="display: none;">
      <button class="action-btn" id="primaryBtn" onclick="handlePrimaryAction()">START</button>
      <button class="action-btn" id="resetBtn" onclick="handleResetAction()">RESET</button>
    </div>

    <!-- Footer Status -->
    <div class="terminal-log">
      <span id="sysConsole">&gt; STATUS: IDLE. ALL PROTOCOLS NORMAL.</span>
      <span>PROJECT DANNEBROG</span>
    </div>
  </div>

  <script>
    let activeMode = 'clock';

    // Clock Interval
    let clockTimer = null;

    // Stopwatch State
    let swStartTime = 0;
    let swElapsedTime = 0;
    let swTimer = null;
    let swRunning = false;

    // Reflex State
    let reflexPhase = 'idle';
    let breachTimeout = null;
    let breachStartTime = 0;

    // 1. Clock Engine
    function startClock() {
      stopStopwatch();
      clearTimeout(breachTimeout);
      document.getElementById('msSub').textContent = '';
      document.getElementById('displayLabel').textContent = 'SYSTEM REAL-TIME FEED (COPENHAGEN/LOCAL)';

      function tick() {
        const now = new Date();
        const h = String(now.getHours()).padStart(2, '0');
        const m = String(now.getMinutes()).padStart(2, '0');
        const s = String(now.getSeconds()).padStart(2, '0');
        document.getElementById('mainTime').firstChild.nodeValue = `${h}:${m}:${s}`;
      }
      tick();
      clockTimer = setInterval(tick, 1000);
    }

    // 2. Stopwatch Engine
    function formatStopwatch(ms) {
      const minutes = Math.floor(ms / 60000);
      const seconds = Math.floor((ms % 60000) / 1000);
      const centis = Math.floor((ms % 1000) / 10);
      return {
        main: `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`,
        sub: `.${String(centis).padStart(2, '0')}`
      };
    }

    function updateStopwatch() {
      const current = Date.now() - swStartTime + swElapsedTime;
      const formatted = formatStopwatch(current);
      document.getElementById('mainTime').firstChild.nodeValue = formatted.main;
      document.getElementById('msSub').textContent = formatted.sub;
    }

    function toggleStopwatch() {
      if (!swRunning) {
        swStartTime = Date.now();
        swTimer = setInterval(updateStopwatch, 10);
        swRunning = true;
        document.getElementById('primaryBtn').textContent = 'STOP';
        document.getElementById('sysConsole').textContent = '> TIMER ACTIVE... SCANNING DURATION';
      } else {
        clearInterval(swTimer);
        swElapsedTime += Date.now() - swStartTime;
        swRunning = false;
        document.getElementById('primaryBtn').textContent = 'START';
        document.getElementById('sysConsole').textContent = '> TIMER PAUSED';
      }
    }

    function resetStopwatch() {
      clearInterval(swTimer);
      swRunning = false;
      swStartTime = 0;
      swElapsedTime = 0;
      document.getElementById('mainTime').firstChild.nodeValue = '00:00';
      document.getElementById('msSub').textContent = '.00';
      document.getElementById('primaryBtn').textContent = 'START';
      document.getElementById('sysConsole').textContent = '> TIMER CLEARED';
    }

    function stopStopwatch() {
      clearInterval(swTimer);
      swRunning = false;
    }

    // 3. Reflex Breach Engine
    function armReflexTest() {
      if (reflexPhase === 'waiting' || reflexPhase === 'active') return;

      const arena = document.getElementById('reflexDisplay');
      arena.className = 'reflex-arena standby';
      document.getElementById('reflexStatus').textContent = '> SCANNING FOR INTRUSION...';
      document.getElementById('reflexHint').textContent = 'WAIT FOR FULL RED BREACH ALERT';
      document.getElementById('sysConsole').textContent = '> PROTOCOL ARMED. STAND BY...';
      reflexPhase = 'waiting';

      const randomDelay = Math.floor(Math.random() * 3000) + 2000;

      breachTimeout = setTimeout(() => {
        arena.className = 'reflex-arena breach';
        document.getElementById('reflexStatus').textContent = '🚨 BREACH DETECTED! HIT NOW! 🚨';
        document.getElementById('sysConsole').textContent = '> ALERT: SYSTEM FIREWALL COMPROMISED!';
        breachStartTime = performance.now();
        reflexPhase = 'active';
      }, randomDelay);
    }

    function handleArenaClick() {
      const arena = document.getElementById('reflexDisplay');

      if (reflexPhase === 'waiting') {
        clearTimeout(breachTimeout);
        arena.className = 'reflex-arena';
        document.getElementById('reflexStatus').textContent = 'FALSE ALARM / EARLY TRIGGER';
        document.getElementById('reflexHint').textContent = 'PENALTY: RETRY BREACH CHECK';
        document.getElementById('sysConsole').textContent = '> PROTOCOL VOID: PRE-EMPTIVE INPUT DETECTED';
        reflexPhase = 'idle';
      } else if (reflexPhase === 'active') {
        const reactionTime = Math.round(performance.now() - breachStartTime);
        arena.className = 'reflex-arena';
        document.getElementById('reflexStatus').textContent = `LOCKDOWN TIME: ${reactionTime} ms`;

        let rating = reactionTime < 200 ? 'GOD' : reactionTime < 220 ? 'FANTASTIC' : reactionTime < 320 ? 'NORMAL OPERATOR' : 'LATENCY DETECTED';
        document.getElementById('reflexHint').textContent = `RATING: ${rating} // CLICK INITIATE TO RETRY`;
        document.getElementById('sysConsole').textContent = `> LOCKDOWN CONFIRMED: ${reactionTime}ms`;
        reflexPhase = 'complete';
      }
    }

    // Mode Selector
    function setMode(mode) {
      activeMode = mode;
      clearInterval(clockTimer);
      stopStopwatch();
      clearTimeout(breachTimeout);

      document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
      document.getElementById('standardDisplay').style.display = 'block';
      document.getElementById('reflexDisplay').style.display = 'none';
      document.getElementById('controlRow').style.display = 'none';

      if (mode === 'clock') {
        document.getElementById('btnClock').classList.add('active');
        startClock();
      } else if (mode === 'stopwatch') {
        document.getElementById('btnStopwatch').classList.add('active');
        document.getElementById('displayLabel').textContent = 'TACTICAL STOPWATCH';
        document.getElementById('controlRow').style.display = 'flex';
        resetStopwatch();
      } else if (mode === 'reflex') {
        document.getElementById('btnReflex').classList.add('active');
        document.getElementById('standardDisplay').style.display = 'none';
        document.getElementById('reflexDisplay').style.display = 'flex';
        document.getElementById('controlRow').style.display = 'flex';
        document.getElementById('primaryBtn').textContent = 'INITIATE';
        document.getElementById('resetBtn').textContent = 'CANCEL';

        const arena = document.getElementById('reflexDisplay');
        arena.className = 'reflex-arena';
        document.getElementById('reflexStatus').textContent = 'PRESS [INITIATE] TO ARM';
        document.getElementById('reflexHint').textContent = 'CLICK BOX OR SPACEBAR ON RED ALERT';
        reflexPhase = 'idle';
      }
    }

    function handlePrimaryAction() {
      if (activeMode === 'stopwatch') toggleStopwatch();
      if (activeMode === 'reflex') armReflexTest();
    }

    function handleResetAction() {
      if (activeMode === 'stopwatch') resetStopwatch();
      if (activeMode === 'reflex') {
        clearTimeout(breachTimeout);
        reflexPhase = 'idle';
        const arena = document.getElementById('reflexDisplay');
        arena.className = 'reflex-arena';
        document.getElementById('reflexStatus').textContent = 'PRESS [INITIATE] TO ARM';
        document.getElementById('reflexHint').textContent = 'READY';
      }
    }

    // Spacebar control
    window.addEventListener('keydown', (e) => {
      if (e.code === 'Space') {
        e.preventDefault();
        if (activeMode === 'reflex') {
          if (reflexPhase === 'idle' || reflexPhase === 'complete') armReflexTest();
          else handleArenaClick();
        } else if (activeMode === 'stopwatch') {
          toggleStopwatch();
        }
      }
    });

    // Boot
    startClock();
  </script>
</body>
</html>
