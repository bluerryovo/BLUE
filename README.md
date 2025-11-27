# BLUE
A chemistry AI game --
:root {
  --bg: #0f172a;
  --card: #111827;
  --text: #e5e7eb;
  --accent: #22d3ee;
  --orbit: #374151;
  --bonding: #10b981;
  --antibonding: #ef4444;
  --degenerate: #60a5fa;
  --unpaired: #f59e0b;
}

* { box-sizing: border-box; }
body {
  margin: 0;
  background: linear-gradient(180deg, #0b1220 0%, var(--bg) 100%);
  color: var(--text);
  font-family: system-ui, Segoe UI, Roboto, Arial, sans-serif;
  line-height: 1.5;
}

header, footer {
  text-align: center;
  padding: 1.5rem 1rem;
}

main {
  max-width: 1000px;
  margin: 0 auto;
  padding: 1rem;
}

section {
  background: var(--card);
  border: 1px solid #1f2937;
  border-radius: 12px;
  padding: 1rem;
  margin-bottom: 1rem;
  box-shadow: 0 10px 30px rgba(0,0,0,0.25);
}

h1, h2 { margin: 0 0 0.75rem; }

.controls .row, .quiz .row {
  display: flex;
  gap: 0.75rem;
  align-items: center;
  margin: 0.5rem 0;
  flex-wrap: wrap;
}

label { min-width: 180px; }

select, input[type="number"] {
  padding: 0.5rem;
  border-radius: 8px;
  border: 1px solid #334155;
  background: #0b1324;
  color: var(--text);
}

button {
  padding: 0.6rem 1rem;
  border-radius: 8px;
  border: 1px solid #334155;
  background: #0b1324;
  color: var(--text);
  cursor: pointer;
  transition: transform 0.02s ease-in, background 0.2s ease;
}

button:hover { background: #0f1a33; }
button:active { transform: scale(0.98); }

.diagram .hint {
  color: #9ca3af;
  font-size: 0.9rem;
  margin-top: 0.5rem;
}

#moDiagram {
  display: grid;
  grid-template-columns: 1fr;
  gap: 0.75rem;
}

.orbital-row {
  display: grid;
  grid-template-columns: 160px 1fr;
  gap: 1rem;
  align-items: center;
}

.orbital-label {
  font-weight: 600;
  color: #a1a1aa;
}

.orbital-set {
  display: flex;
  gap: 0.75rem;
}

.orbital {
  width: 120px;
  min-height: 52px;
  border: 2px dashed var(--orbit);
  border-radius: 10px;
  position: relative;
  padding: 6px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #0b1324;
}

.orbital.bonding { border-color: var(--bonding); }
.orbital.antibonding { border-color: var(--antibonding); }
.orbital.degenerate { border-color: var(--degenerate); }

.orbital .name {
  position: absolute;
  top: 4px;
  left: 6px;
  font-size: 0.85rem;
  color: #94a3b8;
}

.electron {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  margin: 2px;
  background: #e5e7eb;
  box-shadow: 0 2px 8px rgba(255,255,255,0.2);
  border: 1px solid #93c5fd;
}

.electron.unpaired { background: var(--unpaired); }

#results {
  margin-top: 0.75rem;
  padding: 0.75rem;
  border-radius: 8px;
  border: 1px solid #334155;
  background: #0b1324;
}

details summary {
  cursor: pointer;
  padding: 0.5rem;
  border-radius: 8px;
  background: #0f1a33;
}
details ul { margin: 0.5rem 0 0; }
