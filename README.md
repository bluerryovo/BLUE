# BLUE
A chemistry AI game --
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Molecular Orbital Matching Game</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    :root {
      --bg: #0f172a;
      --card: #1e293b;
      --accent: #38bdf8;
      --good: #22c55e;
      --warn: #f59e0b;
      --bad: #ef4444;
      --text: #e5e7eb;
      --muted: #94a3b8;
    }

    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Ubuntu, "Helvetica Neue", Arial, "Noto Sans", sans-serif;
      color: var(--text);
      background: radial-gradient(1200px 600px at 20% 0%, #0b1227 0%, var(--bg) 50%, #0b1227 100%);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }

    header {
      padding: 16px 20px;
      border-bottom: 1px solid #0b1a33;
      background: linear-gradient(180deg, rgba(56, 189, 248, 0.08), transparent);
      backdrop-filter: blur(2px);
    }
    header h1 { margin: 0; font-size: 1.4rem; letter-spacing: 0.3px; }
    header p { margin: 6px 0 0; color: var(--muted); font-size: 0.95rem; }

    .toolbar {
      display: grid;
      grid-template-columns: 1fr auto auto auto;
      gap: 12px;
      padding: 12px 20px;
      align-items: center;
    }
    .stat {
      display: flex; gap: 14px; flex-wrap: wrap; align-items: center;
      color: var(--muted);
    }
    .pill {
      display: inline-flex; align-items: center; gap: 8px;
      background: #0b1a33; color: var(--text);
      border: 1px solid #132241;
      padding: 8px 12px; border-radius: 999px; font-size: 0.9rem;
    }
    .btn {
      border: 1px solid #1f3a64;
      background: #0b1a33; color: var(--text);
      padding: 10px 14px; border-radius: 10px;
      font-weight: 600; cursor: pointer;
      transition: 150ms ease;
    }
    .btn:hover { border-color: var(--accent); box-shadow: 0 0 0 2px rgba(56,189,248,0.2) inset; }
    .btn.primary {
      background: linear-gradient(180deg, #0e223f, #0b1a33);
      border-color: #2a4f84;
    }

    main {
      flex: 1;
      display: grid;
      grid-template-columns: 1fr 320px;
      gap: 16px;
      padding: 16px 20px 28px;
    }

    .grid {
      display: grid;
      gap: 12px;
      grid-template-columns: repeat(4, minmax(120px, 1fr));
    }

    .card {
      position: relative;
      background: linear-gradient(180deg, #15243f, #0f1e35);
      border: 1px solid #22385f;
      border-radius: 14px;
      padding: 12px;
      min-height: 120px;
      display: flex; align-items: center; justify-content: center;
      text-align: center; cursor: pointer;
      user-select: none;
      transition: transform 160ms ease, box-shadow 160ms ease, border-color 160ms ease;
    }
    .card:hover { transform: translateY(-2px); border-color: #2a4f84; }
    .card.matched { background: #0d261c; border-color: #195338; box-shadow: 0 0 0 2px rgba(34,197,94,0.2) inset; }
    .card.selected { outline: 2px solid var(--accent); }
    .card .type {
      position: absolute; top: 10px; left: 12px;
      font-size: 0.75rem; color: var(--muted);
    }
    .card .label {
      font-weight: 700; font-size: 1.05rem; letter-spacing: 0.3px;
    }
    .card .sub {
      margin-top: 6px;
      font-size: 0.85rem; color: #cbd5e1;
    }

    .sidebar {
      background: linear-gradient(180deg, #101a2f, #0b1426);
      border: 1px solid #1a2f55; border-radius: 16px;
      padding: 14px;
    }
    .panel { margin-bottom: 14px; padding: 12px; border-radius: 12px; border: 1px dashed #203760; }
    .panel h3 { margin: 0 0 8px; font-size: 1.05rem; }
    .hint { color: #cbd5e1; font-size: 0.92rem; }
    .kbd { font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", monospace; background: #172742; padding: 2px 6px; border-radius: 6px; border: 1px solid #244269; font-size: 0.85rem; }

    .legend { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; font-size: 0.9rem; color: var(--muted); }
    .badge { display: inline-block; padding: 4px 8px; border-radius: 999px; border: 1px solid #233a62; }
    .badge.good { color: #86efac; border-color: #195338; background: rgba(34,197,94,0.08); }
    .badge.warn { color: #fde68a; border-color: #5b460d; background: rgba(245,158,11,0.08); }

    .footer {
      padding: 12px 20px; border-top: 1px solid #0b1a33; color: var(--muted);
      display: flex; justify-content: space-between; flex-wrap: wrap; gap: 10px;
    }

    @media (max-width: 980px) {
      main { grid-template-columns: 1fr; }
      .grid { grid-template-columns: repeat(3, minmax(120px, 1fr)); }
    }
    @media (max-width: 640px) {
      .grid { grid-template-columns: repeat(2, minmax(120px, 1fr)); }
    }
  </style>
</head>
<body>
  <header>
    <h1>Molecular Orbital Matching Game</h1>
    <p>Match each molecule to its MO properties: bond order and magnetism. Practice Chapters 4–6 concepts interactively.</p>
  </header>

  <div class="toolbar">
    <div class="stat">
      <div class="pill">Time: <span id="time">00:00</span></div>
      <div class="pill">Moves: <span id="moves">0</span></div>
      <div class="pill">Matches: <span id="matches">0</span>/<span id="total">0</span></div>
    </div>
    <button class="btn" id="hintBtn">Hint</button>
    <button class="btn" id="peekBtn">Peek</button>
    <button class="btn primary" id="resetBtn">New game</button>
  </div>

  <main>
    <section class="grid" id="grid"></section>

    <aside class="sidebar">
      <div class="panel">
        <h3>How to play</h3>
        <p class="hint">
          Click one molecule card, then click the matching property card (bond order and magnetism).
          A correct match locks both cards. Finish all matches as fast as you can with few moves.
        </p>
      </div>
      <div class="panel">
        <h3>Quick MO reminders</h3>
        <div class="legend">
          <div>
            <span class="badge good">Bond order</span>
            <div>BO = (bonding − antibonding) / 2</div>
          </div>
          <div>
            <span class="badge warn">Magnetism</span>
            <div>Unpaired electrons → paramagnetic; none → diamagnetic</div>
          </div>
        </div>
      </div>
      <div class="panel">
        <h3>Controls</h3>
        <ul style="margin:0; padding-left: 18px;">
          <li><span class="kbd">Hint</span> highlights likely matches.</li>
          <li><span class="kbd">Peek</span> briefly reveals all cards (costs 1 move).</li>
          <li><span class="kbd">New game</span> shuffles pairs and restarts the timer.</li>
        </ul>
      </div>
      <div class="panel">
        <h3>Customize the deck</h3>
        <p class="hint">
          Open the code and edit <span class="kbd">MO_DECK</span> to add molecules, change bond orders,
         
