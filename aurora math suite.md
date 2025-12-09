````markdown
# Chat Transcript — AuroraMath Suite Conversation

> This markdown file is a plain transcript of the entire user-visible conversation from this chat session, formatted so you can copy-paste it into a file (`chat-transcript.md`). It includes user messages and the code the user pasted. (System and developer messages are not included.)

---

## USER: Pasted finalized code (AuroraMath Suite)

```html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>AuroraMath Suite — All-in-one Calculator & Graphing</title>
<meta name="description" content="AuroraMath Suite — Calculator, graphing, conversions, scientific tools and equation solver" />
<meta name="theme-color" content="#0f1720" id="meta-theme-color">
<script src="https://cdn.jsdelivr.net/npm/mathjs@11.8.0/lib/browser/math.min.js"></script>

<style>
  :root{
    --bg: linear-gradient(135deg,#0b0f12,#112026);
    --card-bg:#0f1720;
    --text:#e6eef3;
    --muted:#9aa7b2;
    --accent:#8ad1ff;
    --accent-2:#b38bff;
    --key-bg:rgba(255,255,255,0.03);
    --key-func:#7b5ba8;
    --key-fore:#e6eef3;
    --op-fore:#051018;
    --radius:12px;
    --shadow:0 14px 50px rgba(2,6,23,.6);
  }
  [data-theme="light"]{
    --bg: linear-gradient(135deg,#f6fbff,#eef6fb);
    --card-bg:#ffffff;
    --text:#111827;
    --muted:#6b7280;
    --key-bg:rgba(0,0,0,0.03);
    --key-fore:#111827;
    --op-fore:#ffffff;
  }
  html,body{height:100%}
  body{font-family:Inter, "Segoe UI", Roboto, Arial; margin:0; min-height:100vh; background:var(--bg); color:var(--text); -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;}
  .app{max-width:980px;margin:18px auto;border-radius:var(--radius);background:var(--card-bg);box-shadow:var(--shadow);overflow:hidden;position:relative}
  .accent-bar{height:6px;background:linear-gradient(90deg,var(--accent),var(--accent-2));border-radius:8px 8px 0 0}
  .top{display:flex;justify-content:space-between;align-items:center;padding:12px 16px;border-bottom:1px solid rgba(255,255,255,0.03)}
  .title{font-weight:800;font-size:1.05rem}
  .muted{font-size:0.85rem;color:var(--muted)}
  .controls{display:flex;gap:8px;align-items:center}
  .btn{padding:8px 12px;border-radius:8px;border:none;cursor:pointer;background:rgba(255,255,255,0.03);color:var(--text);font-weight:700}
  .select{padding:8px;border-radius:8px;background:rgba(255,255,255,0.02);border:1px solid rgba(255,255,255,0.03);color:var(--text)}
  .nav{display:flex;gap:8px;padding:10px 16px;background:rgba(255,255,255,0.01);overflow:auto}
  .tab{padding:10px 12px;border-radius:10px;cursor:pointer;background:transparent;color:var(--muted);font-weight:700;white-space:nowrap}
  .tab.active{background:rgba(0,0,0,0.2);color:var(--text);box-shadow:inset 0 1px 0 rgba(255,255,255,0.02)}
  .tab, .tab * { user-select: none; -webkit-user-select: none; -ms-user-select: none; }
  .container{display:grid;grid-template-columns:1fr 360px;gap:16px;padding:18px}
  .left{padding-right:6px;max-height:calc(100vh - 240px);overflow:auto;-webkit-overflow-scrolling:touch}
  .right{padding-left:6px}
  .panel{padding:12px;border-radius:10px;background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(0,0,0,0.02));margin-bottom:12px}
  .display{width:100%;padding:12px 14px;border-radius:10px;border:1px solid rgba(255,255,255,0.03);background:transparent;color:var(--text);font-size:1.4rem;outline:none}
  .kbd-row{display:flex;gap:8px;margin:10px 0;flex-wrap:wrap}
  .key{flex:1;padding:12px;border-radius:10px;border:none;background:var(--key-bg);color:var(--key-fore);font-weight:800;cursor:pointer;box-shadow:0 6px 18px rgba(0,0,0,0.5);min-height:44px}
  .key.operator{background:linear-gradient(180deg,var(--accent),var(--accent-2));color:var(--op-fore)}
  .key.func{background:var(--key-func);color:#fff}
  .key.wide{flex:2}
  .calc-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-top:8px}
  .key:active{transform:translateY(1px);box-shadow:none;opacity:0.95}
  .history{margin-top:12px;max-height:180px;overflow:auto;border-top:1px dashed rgba(255,255,255,0.02);padding-top:8px}
  .history-item{display:flex;justify-content:space-between;align-items:center;padding:8px;border-radius:8px}
  .history-item:hover{background:rgba(255,255,255,0.02)}
  .graph-box{height:320px;border-radius:8px;background:#04060a;padding:12px;display:flex;align-items:center;justify-content:center}
  svg{width:100%;height:100%}
  .compass{width:220px;height:220px;border-radius:50%;background:radial-gradient(circle,#040406,#0a0d10);display:flex;align-items:center;justify-content:center;position:relative;overflow:hidden;border:6px solid rgba(255,255,255,0.02)}
  .compass-face{position:absolute;inset:0;background-size:cover;background-position:center;opacity:0.95;filter:contrast(.9) saturate(.6) brightness(.8)}
  .needle{width:6px;height:110px;background:linear-gradient(180deg,#ff6b6b,#ffb6b6);position:absolute;left:50%;top:50%;transform-origin:50% 100%;transform:translate(-50%,-100%) rotate(0deg);border-radius:6px}
  .compass-degree{position:absolute;bottom:10px;font-weight:700}

  @media (max-width:980px){
    .container{grid-template-columns:1fr; padding:12px}
    .right{order:2}
    .left{order:1}
    .nav{padding:10px}
    .app{margin:8px}
    .left{max-height:none;overflow:visible}
    .calc-grid{grid-template-columns:repeat(3,1fr)}
  }

  :root { --key-fore: #e6eef3; }
  [data-theme="light"] { --key-fore: #111827; }

  .small{font-size:0.85rem;color:var(--muted)}
  :focus{outline:3px solid rgba(255,255,255,0.06);outline-offset:2px}
  [data-theme="light"] :focus{outline:3px solid rgba(17,24,39,0.08)}

  /* calculator-specific layout fix */
  #calculator .calc-grid{
    display: grid;
    grid-template-columns: repeat(3, 1fr) 86px;
    gap: 10px;
    margin-top: 8px;
    align-items: stretch;
  }
  #calculator .key.wide{
    grid-column: 1 / 3;
  }
  #calculator .key.operator{
    grid-column: 4;
    justify-self: stretch;
    align-self: stretch;
  }
  @media (max-width: 420px){
    #calculator .calc-grid{
      grid-template-columns: repeat(3, 1fr) 68px;
      gap: 8px;
    }
    #calculator .key.wide{
      grid-column: 1 / 3;
    }
  }

  /* implicit-plot point style inserted into SVG dynamically */
</style>
</head>
<body>
  <div class="app" id="appRoot" data-theme="">
    <div class="accent-bar" id="accentBar"></div>

    <div class="top">
      <div>
        <div class="title">AuroraMath Suite</div>
        <div class="muted">Scientific, graphing, conversions, compass & mathematical tools</div>
      </div>

      <div class="controls">
        <select id="themeSelect" class="select" aria-label="Theme select">
          <option value="blackgold">Black & Gold (Dark)</option>
          <option value="orange">Orange & Black (Dark)</option>
          <option value="whiteblue">White & Blue (Light)</option>
          <option value="neon">Neon (Dark)</option>
          <option value="darkclassic">Dark Classic</option>
          <option value="lightclassic">Light Classic (Light)</option>
        </select>
        <button class="btn" id="applyThemeBtn">Apply Theme</button>
        <button class="btn" id="toggleLightBtn">Light / Dark</button>
      </div>
    </div>

    <div class="nav" id="navTabs" role="navigation" aria-label="Main tabs">
      <div class="tab active" data-panel="calculator">Calculator</div>
      <div class="tab" data-panel="scientific">Scientific</div>
      <div class="tab" data-panel="tools">Tools</div>
      <div class="tab" data-panel="conversion">Conversion</div>
      <div class="tab" data-panel="time">Time Tools</div>
      <div class="tab" data-panel="graph">Graphing</div>
      <div class="tab" data-panel="compass">Compass</div>
    </div>

    <div class="container">
      <div class="left">
        <!-- BASIC CALCULATOR -->
        <div class="panel" id="calculator" role="region" aria-label="Calculator panel">
          <input id="display-calculator" class="display" value="0" aria-label="Calculator input" />
          <div class="kbd-row">
            <button class="btn" onclick="backspaceAtCursor('display-calculator')">⌫</button>
            <button class="btn" onclick="deleteAtCursor('display-calculator')">Del</button>
            <button class="btn" onclick="clearDisplay('display-calculator')">Clear</button>
            <button class="btn" onclick="evaluateAndStore('calculator')">=</button>
            <button class="btn" onclick="clearHistory('history-calculator')">Clear History</button>
          </div>

          <div class="calc-grid" role="group" aria-label="Calculator keypad">
            <button class="key" onclick="insertAtCursor('display-calculator','7')">7</button>
            <button class="key" onclick="insertAtCursor('display-calculator','8')">8</button>
            <button class="key" onclick="insertAtCursor('display-calculator','9')">9</button>
            <button class="key operator" onclick="insertAtCursor('display-calculator','+')">+</button>

            <button class="key" onclick="insertAtCursor('display-calculator','4')">4</button>
            <button class="key" onclick="insertAtCursor('display-calculator','5')">5</button>
            <button class="key" onclick="insertAtCursor('display-calculator','6')">6</button>
            <button class="key operator" onclick="insertAtCursor('display-calculator','-')">−</button>

            <button class="key" onclick="insertAtCursor('display-calculator','1')">1</button>
            <button class="key" onclick="insertAtCursor('display-calculator','2')">2</button>
            <button class="key" onclick="insertAtCursor('display-calculator','3')">3</button>
            <button class="key operator" onclick="insertAtCursor('display-calculator','*')">×</button>

            <button class="key wide" onclick="insertAtCursor('display-calculator','0')">0</button>
            <button class="key" onclick="insertAtCursor('display-calculator','.')">.</button>
            <button class="key operator" onclick="insertAtCursor('display-calculator','/')">÷</button>
          </div>

          <div class="history" id="history-calculator" aria-live="polite"></div>
        </div>

        <!-- SCIENTIFIC -->
        <div class="panel" id="scientific" style="display:none">
          <input id="display-scientific" class="display" placeholder="scientific expression" />
          <div class="kbd-row">
            <button class="btn" onclick="backspaceAtCursor('display-scientific')">⌫</button>
            <button class="btn" onclick="deleteAtCursor('display-scientific')">Del</button>
            <button class="btn" onclick="clearDisplay('display-scientific')">Clear</button>
            <button class="btn" onclick="evaluateAndStore('scientific')">=</button>
            <button class="btn" onclick="clearHistory('history-scientific')">Clear History</button>
          </div>

          <div style="display:grid;grid-template-columns:repeat(5,1fr);gap:8px">
            <button class="key func" onclick="insertAtCursor('display-scientific','sin(')">sin</button>
            <button class="key func" onclick="insertAtCursor('display-scientific','cos(')">cos</button>
            <button class="key func" onclick="insertAtCursor('display-scientific','tan(')">tan</button>
            <button class="key" onclick="insertAtCursor('display-scientific','pi')">π</button>
            <button class="key operator" onclick="insertAtCursor('display-scientific','^')">^</button>

            <button class="key func" onclick="insertAtCursor('display-scientific','asin(')">asin</button>
            <button class="key func" onclick="insertAtCursor('display-scientific','acos(')">acos</button>
            <button class="key func" onclick="insertAtCursor('display-scientific','atan(')">atan</button>
            <button class="key func" onclick="insertAtCursor('display-scientific','sqrt(')">√</button>
            <button class="key operator" onclick="insertAtCursor('display-scientific','/')">÷</button>

            <button class="key func" onclick="insertAtCursor('display-scientific','ln(')">ln</button>
            <button class="key func" onclick="insertAtCursor('display-scientific','log10(')">log10</button>
            <button class="key func" onclick="insertAtCursor('display-scientific','exp(')">exp</button>
            <button class="key func" onclick="insertAtCursor('display-scientific','fact(')">fact(</button>
            <button class="key operator" onclick="insertAtCursor('display-scientific','*')">×</button>

            <button class="key" onclick="insertAtCursor('display-scientific','7')">7</button>
            <button class="key" onclick="insertAtCursor('display-scientific','8')">8</button>
            <button class="key" onclick="insertAtCursor('display-scientific','9')">9</button>
            <button class="key" onclick="insertAtCursor('display-scientific','4')">4</button>
            <button class="key" onclick="insertAtCursor('display-scientific','5')">5</button>

            <button class="key" onclick="insertAtCursor('display-scientific','6')">6</button>
            <button class="key" onclick="insertAtCursor('display-scientific','1')">1</button>
            <button class="key" onclick="insertAtCursor('display-scientific','2')">2</button>
            <button class="key" onclick="insertAtCursor('display-scientific','3')">3</button>
            <button class="key wide" onclick="insertAtCursor('display-scientific','0')">0</button>

            <button class="key" onclick="insertAtCursor('display-scientific','.')">.</button>
            <button class="key operator" onclick="evaluateAndStore('scientific')">=</button>
          </div>

          <div class="history" id="history-scientific" aria-live="polite"></div>
        </div>

        <!-- TOOLS -->
        <div class="panel" id="tools" style="display:none">
          <h3>Measure Distance</h3>
          <div style="display:flex;gap:8px">
            <input type="number" id="measure-start" placeholder="Start (cm)" min="0" step="0.1" style="flex:1">
            <input type="number" id="measure-end" placeholder="End (cm)" min="0" step="0.1" style="flex:1">
          </div>
          <div style="display:flex;gap:8px;margin-top:8px">
            <button class="btn" onclick="calculateDistance()">Calculate</button>
            <button class="btn" onclick="clearRuler()">Clear</button>
          </div>
          <div style="margin-top:10px">Distance: <strong id="distance-result">0</strong> cm</div>

          <hr style="margin:12px 0;border:none;border-top:1px solid rgba(255,255,255,0.03)">

          <h3>Element Lookup</h3>
          <div class="small">Type element name (e.g., silver) or symbol (e.g., Au) and press Enter or Lookup</div>
          <div style="display:flex;gap:8px;margin-top:8px">
            <input id="element-query" placeholder="Element name or symbol" style="flex:1">
            <button class="btn" onclick="lookupElement()">Lookup</button>
            <button class="btn" onclick="clearElement()">Clear</button>
          </div>
          <div style="margin-top:12px"><strong id="element-result" class="muted"></strong></div>
        </div>

        <!-- Conversion -->
        <div class="panel" id="conversion" style="display:none">
          <h3>Unit Converter</h3>
          <div style="display:grid;grid-template-columns:1fr auto 1fr;gap:10px;align-items:center">
            <select id="unit-from">
              <option value="mm">Millimeter (mm)</option>
              <option value="cm">Centimeter (cm)</option>
              <option value="m" selected>Meter (m)</option>
              <option value="km">Kilometer (km)</option>
              <option value="in">Inch (in)</option>
              <option value="ft">Foot (ft)</option>
              <option value="yd">Yard (yd)</option>
              <option value="mi">Mile (mi)</option>
            </select>
            <div style="text-align:center;color:var(--accent)">→</div>
            <select id="unit-to">
              <option value="mm">Millimeter (mm)</option>
              <option value="cm">Centimeter (cm)</option>
              <option value="m">Meter (m)</option>
              <option value="km" selected>Kilometer (km)</option>
              <option value="in">Inch (in)</option>
              <option value="ft">Foot (ft)</option>
              <option value="yd">Yard (yd)</option>
              <option value="mi">Mile (mi)</option>
            </select>
          </div>
          <input type="number" id="unit-input" placeholder="Enter value" oninput="convertUnit()">
          <input type="text" id="unit-result" placeholder="Result" readonly>
          <button class="btn" onclick="clearUnitConverter()">Clear Values</button>

          <h3 style="margin-top:12px">Temperature Converter</h3>
          <div style="display:grid;grid-template-columns:1fr auto 1fr;gap:10px;align-items:center">
            <select id="temp-from"><option value="c">Celsius (°C)</option><option value="f">Fahrenheit (°F)</option><option value="k">Kelvin (K)</option></select>
            <div style="text-align:center;color:var(--accent)">→</div>
            <select id="temp-to"><option value="c">Celsius (°C)</option><option value="f" selected>Fahrenheit (°F)</option><option value="k">Kelvin (K)</option></select>
          </div>
          <input type="number" id="temp-input" placeholder="Enter temperature" oninput="convertTemp()">
          <input type="text" id="temp-result" placeholder="Result" readonly>
          <button class="btn" onclick="clearTempConverter()">Clear Values</button>
        </div>

        <!-- Time Tools -->
        <div class="panel" id="time" style="display:none">
          <h3>Clock</h3>
          <div id="clock" class="muted">00:00:00</div>

          <h3 style="margin-top:10px">Stopwatch</h3>
          <div id="stopwatch" class="muted">00:00:00</div>
          <div style="display:flex;gap:8px;margin-top:8px">
            <button class="btn" onclick="startStopwatch()">Start</button>
            <button class="btn" onclick="pauseStopwatch()">Pause</button>
            <button class="btn" onclick="resetStopwatch()">Reset</button>
          </div>

          <h3 style="margin-top:12px">Timer</h3>
          <div style="display:flex;gap:8px">
            <input type="number" id="timer-minutes" placeholder="Min" min="0" style="width:50%">
            <input type="number" id="timer-seconds" placeholder="Sec" min="0" style="width:50%">
          </div>
          <div style="display:flex;gap:8px;margin-top:8px">
            <button class="btn" onclick="startTimer()">Start</button>
            <button class="btn" onclick="pauseTimer()">Pause</button>
            <button class="btn" onclick="resetTimer()">Reset</button>
          </div>
        </div>

        <!-- Graphing & equation solver -->
        <div class="panel" id="graph" style="display:none">
          <h3>Graphing Calculator</h3>
          <input id="function-input" placeholder="Enter function or implicit equation. Examples: x^2, sin(x), 2*x+3, x^2 + y^2 = 1" aria-label="Function to plot">
          <div style="display:flex;gap:8px;margin-top:8px">
            <button class="btn" onclick="plotFunction()">Plot Function</button>
            <button class="btn" onclick="clearGraph()">Clear Graph</button>
            <button class="btn" onclick="exportGraphPNG()">Export Graph</button>
          </div>
          <div class="graph-box" style="margin-top:8px">
            <svg id="graph-svg" viewBox="0 0 600 320" preserveAspectRatio="none">
              <rect width="100%" height="100%" fill="#02040a"></rect>
              <g id="implicit-group"></g>
              <path id="graph-path" d="" stroke="var(--accent)" stroke-width="2" fill="none"></path>
            </svg>
          </div>

          <h3 style="margin-top:12px">Equation Solver</h3>
          <div class="small">Single equation like <code>x^2 - 5*x + 6 = 0</code> or multiple equations separated by newline/semicolon for system solving.</div>
          <textarea id="equation-input" placeholder="Example (system): x + y = 2 ; x - y = 0" style="width:100%;height:62px;margin-top:8px"></textarea>
          <div class="kbd-row" style="margin-top:8px">
            <button class="btn" onclick="solveEquation()">Solve</button>
            <button class="btn" onclick="clearEquation()">Clear</button>
          </div>
          <input id="equation-result" readonly placeholder="Solution" style="margin-top:8px">
        </div>

        <!-- Compass -->
        <div class="panel" id="compass" style="display:none">
          <h3>Digital Compass</h3>
          <div class="compass" id="compass-visual">
            <div class="compass-face" id="compass-face" style="background-image: radial-gradient(circle at 30% 20%, rgba(255,255,255,0.02), rgba(0,0,0,0.6))"></div>
            <div class="needle" id="compass-needle"></div>
            <div class="compass-degree" id="compass-degree">0°</div>
          </div>

          <div style="margin-top:12px">
            <div>Direction: <strong id="compass-direction-text">N</strong></div>
            <div>Coordinates (simulated): <strong id="coordinates">0.00, 0.00</strong></div>
            <div style="display:flex;gap:8px;margin-top:8px">
              <button class="btn" id="toggleCompassBtn">Enable Compass</button>
              <label class="btn">Custom Photo
                <input id="compassFaceUpload" type="file" accept="image/*">
              </label>
              <button class="btn" onclick="setCompassPreset('dark')">Dark Preset</button>
            </div>
          </div>
        </div>

      </div>

      <div class="right">
        <div class="panel">
          <h3 class="muted">Theme Preview</h3>
          <div id="themePreview" style="height:70px;border-radius:8px;border:1px solid rgba(255,255,255,0.03);display:flex;align-items:center;justify-content:center">Preview</div>
        </div>

        <div class="panel small">
          <div><strong>Notes for testing</strong></div>
          <div style="margin-top:8px">Try these examples (copy/paste):</div>
          <ul style="margin-top:8px">
            <li><code>y = x^2</code> or <code>x^2</code> (graph panel)</li>
            <li><code>sin(x)</code> (graph)</li>
            <li><code>x^2 + y^2 = 1</code> (implicit)</li>
            <li>System solver: <code>x + y = 2\nx - y = 0</code> (two lines) or use semicolon</li>
            <li>Equation solver: <code>x+1 = y+1</code> → shows <strong>x = y</strong></li>
          </ul>
        </div>
      </div>
    </div>
  </div>

<script>
/* -------------------------
   Small helpers
   ------------------------- */
const el = id => document.getElementById(id);

/* -------------------------
   Tabs
   ------------------------- */
document.querySelectorAll('.tab').forEach(t=>{
  t.style.touchAction = 'manipulation';
  t.addEventListener('click', ()=>{
    document.querySelectorAll('.tab').forEach(x=>x.classList.remove('active'));
    t.classList.add('active');
    const panel = t.getAttribute('data-panel');
    document.querySelectorAll('.panel').forEach(p=>p.style.display = (p.id === panel)? '' : 'none');
    setTimeout(()=> t.scrollIntoView({inline:'center',behavior:'smooth'}),50);
  });
});

/* -------------------------
   Caret / input helpers
   ------------------------- */
function insertAtCursor(id, text){
  const input = el(id); if(!input) return; input.focus();
  const start = input.selectionStart ?? input.value.length;
  const end = input.selectionEnd ?? start;
  const v = input.value || '';
  input.value = v.slice(0,start) + text + v.slice(end);
  const pos = start + text.length;
  input.setSelectionRange(pos,pos);
}
function backspaceAtCursor(id){
  const input = el(id); if(!input) return; input.focus();
  const start = input.selectionStart ?? 0;
  const end = input.selectionEnd ?? start;
  if(start === end && start > 0){
    const v = input.value; input.value = v.slice(0,start-1) + v.slice(end); input.setSelectionRange(start-1,start-1);
  } else if(start !== end){
    const v = input.value; input.value = v.slice(0,start) + v.slice(end); input.setSelectionRange(start,start);
  }
}
function deleteAtCursor(id){
  const input = el(id); if(!input) return; input.focus();
  const start = input.selectionStart ?? 0;
  const end = input.selectionEnd ?? start;
  const v = input.value;
  if(start === end) { input.value = v.slice(0,start) + v.slice(start+1); input.setSelectionRange(start,start); }
  else { input.value = v.slice(0,start) + v.slice(end); input.setSelectionRange(start,start); }
}
function clearDisplay(id){ const i=el(id); if(i){ i.value=''; i.focus(); } }

/* -------------------------
   History utilities
   ------------------------- */
function addToHistoryEl(containerId, expr, res){
  const cont = el(containerId); if(!cont) return;
  const item = document.createElement('div'); item.className='history-item';
  const left = document.createElement('div'); left.textContent = expr + ' = ' + res; left.style.cursor='pointer';
  left.onclick = ()=> {
    if(containerId==='history-calculator'){ document.querySelector('.tab[data-panel="calculator"]').click(); el('display-calculator').value = expr; el('display-calculator').focus(); el('display-calculator').setSelectionRange(expr.length,expr.length); }
    else { document.querySelector('.tab[data-panel="scientific"]').click(); el('display-scientific').value = expr; el('display-scientific').focus(); el('display-scientific').setSelectionRange(expr.length,expr.length); }
  };
  const right = document.createElement('div');
  const del = document.createElement('button'); del.className='btn'; del.textContent='Delete'; del.onclick = (e)=>{ e.stopPropagation(); item.remove(); };
  right.appendChild(del);
  item.appendChild(left); item.appendChild(right);
  cont.insertBefore(item, cont.firstChild);
}
function clearHistory(id){ const c = el(id); if(c) c.innerHTML=''; }

/* -------------------------
   Math engine (math.js)
   ------------------------- */
function evaluateExpressionRaw(expr){
  if(!expr) return '';
  expr = String(expr).replace(/×/g,'*').replace(/÷/g,'/').replace(/π/g,'pi').replace(/√/g,'sqrt');
  expr = expr.replace(/fact\(\s*([0-9]+)\s*\)/g, (m,p)=> `factorial(${p})`);
  try{
    const scope = {
      factorial: function(n){
        n = Math.floor(Number(n));
        if(n<0) return NaN; let r=1; for(let i=2;i<=n;i++) r*=i; return r;
      }, pi: Math.PI
    };
    expr = expr.replace(/\bln\(/g,'log('); // ln -> natural log
    const res = math.evaluate(expr, scope);
    if(Array.isArray(res)) return res.join(', ');
    return String(res);
  } catch(e){ return 'Error'; }
}

function addToHistory(type, expr, res){
  if(type==='scientific') addToHistoryEl('history-scientific', expr, res);
  else addToHistoryEl('history-calculator', expr, res);
}
function evaluateAndStore(type){
  const id = (type==='scientific')? 'display-scientific' : 'display-calculator';
  const input = el(id);
  if(!input) return;
  const expr = input.value || '';
  const res = evaluateExpressionRaw(expr);
  input.value = res === 'Error' ? 'Error' : res;
  addToHistory(type, expr, res);
}

/* -------------------------
   Unit & Temp converters
   ------------------------- */
function convertUnit(){ const from=el('unit-from').value; const to=el('unit-to').value; const val=parseFloat(el('unit-input').value); if(isNaN(val)){ el('unit-result').value=''; return; } const f={mm:0.001,cm:0.01,m:1,km:1000,in:0.0254,ft:0.3048,yd:0.9144,mi:1609.344}; el('unit-result').value=(val * f[from] / f[to]).toFixed(6); }
function clearUnitConverter(){ el('unit-input').value=''; el('unit-result').value=''; }
function convertTemp(){ const from=el('temp-from').value; const to=el('temp-to').value; const v=parseFloat(el('temp-input').value); if(isNaN(v)){el('temp-result').value='';return;} let c;if(from==='c') c=v; else if(from==='f') c=(v-32)*5/9; else c=v-273.15; let out;if(to==='c') out=c; else if(to==='f') out=c*9/5+32; else out=c+273.15; el('temp-result').value=out.toFixed(2); }
function clearTempConverter(){ el('temp-input').value=''; el('temp-result').value=''; }

/* -------------------------
   Time utilities
   ------------------------- */
function updateClock(){ el('clock').textContent = new Date().toLocaleTimeString(); }
setInterval(updateClock,1000); updateClock();

let swInterval, swRunning=false, swTime=0;
function startStopwatch(){ if(!swRunning){ swRunning=true; swInterval=setInterval(()=>{ swTime++; updateSW(); },1000); } }
function pauseStopwatch(){ if(swRunning){ clearInterval(swInterval); swRunning=false; } }
function resetStopwatch(){ clearInterval(swInterval); swRunning=false; swTime=0; updateSW(); }
function updateSW(){ const h=Math.floor(swTime/3600), m=Math.floor((swTime%3600)/60), s=swTime%60; el('stopwatch').textContent = String(h).padStart(2,'0')+':'+String(m).padStart(2,'0')+':'+String(s).padStart(2,'0'); }

let timerInterval, timerRunning=false, timerTime=0;
function startTimer(){ if(!timerRunning){ const min = parseInt(el('timer-minutes').value)||0; const sec = parseInt(el('timer-seconds').value)||0; timerTime = min*60 + sec; if(timerTime<=0) return; timerRunning=true; timerInterval=setInterval(()=>{ timerTime--; if(timerTime<=0){ clearInterval(timerInterval); timerRunning=false; alert('Timer finished'); } },1000); } }
function pauseTimer(){ if(timerRunning){ clearInterval(timerInterval); timerRunning=false; } }
function resetTimer(){ clearInterval(timerInterval); timerRunning=false; timerTime=0; }

/* -------------------------
   Graphing (explicit + implicit)
   - explicit: y = f(x) numeric sample + path
   - implicit: sample a coarse grid and plot points where |F(x,y)| < eps
   ------------------------- */
function plotFunction(){
  const inputRaw = (el('function-input').value || '').trim();
  if(!inputRaw) return alert('Enter function or implicit equation');
  // normalize X/Y -> x/y for single-letter vars
  let input = inputRaw.replace(/\bX\b/g,'x').replace(/\bY\b/g,'y');

  // Decide mode: implicit if expression contains 'y' or '=' and is not a simple single-variable expression 'y = f(x)'
  const looksLikeImplicit = /[=]/.test(input) && (/[yY]/.test(input) || /,/.test(input));
  const explicitMode = !looksLikeImplicit && /[xy]/i.test(input) ? (/y\s*=/i.test(input) || !/[y]/i.test(input) || (/^[^=]+$/.test(input) && !/[y]/i.test(input))) : false;

  const svg = el('graph-svg');
  const pathEl = el('graph-path');
  const implicitGroup = el('implicit-group');
  // clear previous render
  pathEl.setAttribute('d','');
  implicitGroup.innerHTML = '';

  // Graph viewport
  const viewW = 600, viewH = 320;
  const xmin=-10, xmax=10, ymin=-6, ymax=6; // default
  const samplesX = 600;
  const samplesY = 300;

  // Helper to map coords
  const scaleX = x => ((x - xmin)/(xmax - xmin)) * viewW;
  const scaleY = y => viewH - ((y - ymin)/(ymax - ymin)) * viewH;

  // If user gave a plain expression containing only x (like 'x^2' or 'sin(x)'), treat as explicit
  const onlyX = /^[^y=]*x[^y=]*$/i.test(input) || (/^[^=]+$/.test(input) && /x/i.test(input) && !/y/i.test(input));
  // detect pattern 'y =' then it's explicit
  if(/^\s*y\s*=/i.test(input) || onlyX){
    // explicit plotting: interpret expression as f(x) (if 'y = ...' strip left)
    const expr = input.replace(/^\s*y\s*=\s*/i,'').trim();
    let compiled;
    try{
      const node = math.parse(expr);
      compiled = node.compile();
    }catch(e){ alert('Could not parse function. Try examples like x^2, sin(x), 2*x+3.'); return; }

    // sample
    const samples = Math.min(1100, Math.max(200, Math.floor(samplesX * (window.innerWidth / 800))));
    let yMin = Infinity, yMax = -Infinity;
    const pts = [];
    for(let i=0;i<=samples;i++){
      const x = xmin + (i/samples)*(xmax - xmin);
      let y = NaN;
      try{ y = Number(compiled.evaluate({x:x, pi:Math.PI})); }catch(e){ y = NaN; }
      if(isFinite(y)){ yMin = Math.min(yMin,y); yMax = Math.max(yMax,y); }
      pts.push({x,y});
    }
    if(!isFinite(yMin) || !isFinite(yMax)){ yMin=-1; yMax=1; }
    const pad = (yMax - yMin) * 0.12 || 1;
    const yLo = yMin - pad, yHi = yMax + pad;
    // remap scaleY locally for good view
    const scaleYLocal = y => viewH - ((y - yLo)/(yHi - yLo)) * viewH;

    let d = ''; let started=false;
    for(const p of pts){
      if(!isFinite(p.y)){ started=false; continue; }
      const sx = scaleX(p.x); const sy = scaleYLocal(p.y);
      if(!started){ d += `M ${sx.toFixed(2)} ${sy.toFixed(2)} `; started=true; }
      else d += `L ${sx.toFixed(2)} ${sy.toFixed(2)} `;
    }
    pathEl.setAttribute('d', d);
    return;
  }

  // Otherwise: implicit plotting (equation F(x,y) = 0), handle equalities
  let expr = input;
  if(input.includes('=')){
    const parts = input.split('=');
    expr = '(' + parts[0] + ') - (' + parts.slice(1).join('=') + ')';
  }
  // compile
  let compiled;
  try{
    const node = math.parse(expr);
    compiled = node.compile();
  }catch(e){ alert('Could not parse implicit expression. Try something like x^2 + y^2 = 1 or x*y - 1 = 0'); return; }

  // sample coarse grid and plot small circles where |F| < eps
  // choose grid resolution adaptively for performance
  const gx = 160; const gy = 120; // coarse but reasonable
  const eps = 0.035; // threshold scaled relative to function values — may be enough for many curves
  const frag = document.createDocumentFragment();
  // determine dynamic eps: evaluate at a small set to estimate scale
  let scaleEstimate = 0;
  for(let i=0;i<6;i++){
    const x = xmin + Math.random()*(xmax-xmin);
    const y = ymin + Math.random()*(ymax-ymin);
    try{ const v = math.evaluate(expr, {x:x,y:y,pi:Math.PI}); if(isFinite(Number(v))) scaleEstimate = Math.max(scaleEstimate, Math.abs(Number(v))); } catch(e){}
  }
  const dynamicEps = Math.max(0.02, Math.abs(scaleEstimate) * 0.02);

  for(let i=0;i<gx;i++){
    const x = xmin + (i/(gx-1))*(xmax - xmin);
    for(let j=0;j<gy;j++){
      const y = ymin + (j/(gy-1))*(ymax - ymin);
      let v = NaN;
      try{ v = Number(compiled.evaluate({x:x,y:y,pi:Math.PI})); }catch(e){ v = NaN; }
      if(!isFinite(v)) continue;
      if(Math.abs(v) <= dynamicEps){
        const cx = scaleX(x), cy = scaleY(y);
        const c = document.createElementNS('http://www.w3.org/2000/svg','circle');
        c.setAttribute('cx', cx.toFixed(2));
        c.setAttribute('cy', cy.toFixed(2));
        c.setAttribute('r', 0.9);
        c.setAttribute('fill', 'var(--accent)');
        c.setAttribute('opacity', 0.95);
        frag.appendChild(c);
      }
    }
  }
  implicitGroup.appendChild(frag);
  // done
}

/* Clear graph */
function clearGraph(){ el('function-input').value=''; el('graph-path').setAttribute('d',''); el('implicit-group').innerHTML=''; }

/* Export graph */
function exportGraphPNG(){
  const svg = el('graph-svg');
  const serializer = new XMLSerializer();
  const svgStr = serializer.serializeToString(svg);
  const canvas = document.createElement('canvas'); canvas.width=1200; canvas.height=640;
  const ctx = canvas.getContext('2d');
  const img = new Image();
  const blob = new Blob([svgStr], {type:'image/svg+xml;charset=utf-8'});
  const url = URL.createObjectURL(blob);
  img.onload = function(){ ctx.fillStyle='#02040a'; ctx.fillRect(0,0,canvas.width,canvas.height); ctx.drawImage(img,0,0,canvas.width,canvas.height); URL.revokeObjectURL(url); const png = canvas.toDataURL('image/png'); const a=document.createElement('a'); a.href=png; a.download='auroramath-graph.png'; a.click(); };
  img.src = url;
}

/* -------------------------
   Equation solver (single, multivar and numeric system solver)
   - single equation: symbolic (math.solve) -> numeric fallback
   - multiple equations (newline or ';'): numeric system solver (Newton-Raphson)
   ------------------------- */
function solveEquation(){
  const raw = (el('equation-input').value || '').trim();
  const out = el('equation-result');
  out.value = '';
  if(!raw) return;

  // split into multiple equations if newline or semicolon
  const parts = raw.split(/\r?\n|;/).map(s=>s.trim()).filter(Boolean);
  if(parts.length > 1){
    // system solve
    const eqs = parts;
    try{
      const res = solveSystemNumeric(eqs);
      if(!res) out.value = 'No solution found (numeric solver)';
      else out.value = Object.entries(res).map(([k,v]) => `${k} = ${Number(v).toFixed(8)}`).join(', ');
      return;
    }catch(e){ out.value = 'System solver error: ' + (e.message || e); return; }
  }

  // single equation (parts.length === 1)
  let eq = parts[0];
  // normalize X/Y -> x/y
  eq = eq.replace(/\bX\b/g,'x').replace(/\bY\b/g,'y');

  let expr = eq;
  if(eq.includes('=')){
    const p = eq.split('=');
    expr = '('+p[0]+') - ('+p.slice(1).join('=')+')';
  }

  // detect variables
  function detectVars(s){
    const all = (s.match(/[A-Za-z]+/g) || []).map(t => t.toLowerCase());
    const exclude = new Set(['pi','e','sin','cos','tan','log','log10','sqrt','exp','asin','acos','atan','ln','fact','factorial']);
    const vars = [...new Set(all.filter(v => !exclude.has(v)))];
    const single = vars.filter(v => v.length === 1);
    return single.length ? single : vars;
  }

  const vars = detectVars(expr);
  if(vars.length === 0){
    const val = evaluateExpressionRaw(expr);
    out.value = val === 'Error' ? 'Error' : ((Number(val) === 0) ? 'True (identity)' : 'No variable: ' + val);
    return;
  }

  if(vars.length === 1){
    const variable = vars[0];
    // try symbolic
    try{
      if(typeof math.solve === 'function'){
        const sol = math.solve(expr, variable);
        if(sol && (Array.isArray(sol) ? sol.length>0 : true)){
          out.value = Array.isArray(sol) ? sol.join(', ') : String(sol);
          return;
        }
      }
    }catch(e){}
    // numeric fallback
    const f = x => { try { const v = math.evaluate(expr, {[variable]:x, pi:Math.PI}); return Number(v); } catch(e) { return NaN; } };
    const roots = new Set();
    const xmin=-200, xmax=200, steps=400;
    for(let i=0;i<steps;i++){
      const a = xmin + (i/steps)*(xmax-xmin);
      const b = xmin + ((i+1)/steps)*(xmax-xmin);
      const fa = f(a), fb = f(b);
      if(!isFinite(fa) || !isFinite(fb)) continue;
      if(Math.abs(fa) < 1e-12) roots.add(Number(a.toFixed(12)));
      if(fa*fb < 0){
        let lo=a, hi=b, mid, fmid;
        for(let k=0;k<60;k++){
          mid=(lo+hi)/2; fmid=f(mid);
          if(!isFinite(fmid)) break;
          if(Math.abs(fmid) < 1e-12) break;
          if(fa * fmid <= 0) hi = mid; else lo = mid;
        }
        roots.add(Number(mid.toFixed(12)));
      }
    }
    if(roots.size>0){
      const arr = Array.from(roots).map(v => Number(v)).sort((a,b)=>a-b);
      out.value = arr.map(v => Number(v.toFixed(8))).join(', ');
    } else out.value = 'No numeric root found';
    return;
  }

  // multiple vars: attempt linear detection first
  try{
    const vlist = vars.slice(0,3);
    const n = vlist.length;
    const samples = [];
    samples.push(Object.fromEntries(vlist.map(v=>[v,0])));
    for(let i=0;i<n;i++){
      const s = Object.fromEntries(vlist.map((v,idx)=>[v, idx===i?1:0]));
      samples.push(s);
    }
    const vals = samples.map(s => {
      try { return Number(math.evaluate(expr, Object.assign({}, s, {pi:Math.PI}))); } catch(e){ return NaN; }
    });
    if(vals.some(v => !isFinite(v))){
      // can't do linear detection; attempt system numeric solve with single equation? fallback
      out.value = 'Relation or complex; try using system solver (one equation per line) or simplify expression';
      return;
    }
    const c = vals[0];
    const A = [];
    for(let i=0;i<n;i++) A.push(vals[i+1] - c);
    const tol = 1e-8;
    function fmtCoef(num){
      if(Math.abs(num - 1) < tol) return '';
      if(Math.abs(num + 1) < tol) return '-';
      return (num.toFixed(8) + ' * ');
    }
    if(Math.abs(A[0]) > tol){
      const coeff = A.map(a => a / A[0]);
      const rhsTerms = [];
      for(let i=1;i<n;i++){
        if(Math.abs(coeff[i]) > tol){
          const termCoef = -coeff[i];
          const coefStr = fmtCoef(termCoef);
          rhsTerms.push(coefStr + vlist[i]);
        }
      }
      if(Math.abs(c/A[0]) > tol) rhsTerms.push(( -c/A[0] ).toFixed(8));
      const rhs = rhsTerms.length ? rhsTerms.join(' + ').replace(/\+\s-/, '- ') : '0';
      let outstr = `${vlist[0]} = ${rhs}`;
      outstr = outstr.replace(/\b1\.00000000 \* /g,'').replace(/\-1\.00000000 \* /g,'-');
      out.value = outstr;
      return;
    } else if(n>1 && Math.abs(A[1]) > tol){
      const coeff = A.map(a => a / A[1]);
      const rhsTerms = [];
      for(let i=0;i<n;i++){
        if(i===1) continue;
        if(Math.abs(coeff[i]) > tol){
          const termCoef = -coeff[i];
          const coefStr = fmtCoef(termCoef);
          rhsTerms.push(coefStr + vlist[i]);
        }
      }
      if(Math.abs(c/A[1]) > tol) rhsTerms.push(( -c/A[1] ).toFixed(8));
      const rhs = rhsTerms.length ? rhsTerms.join(' + ').replace(/\+\s-/, '- ') : '0';
      let outstr = `${vlist[1]} = ${rhs}`;
      outstr = outstr.replace(/\b1\.00000000 \* /g,'').replace(/\-1\.00000000 \* /g,'-');
      out.value = outstr;
      return;
    } else {
      if(Math.abs(c) < tol) out.value = 'Identity (true for all variables)';
      else out.value = 'No solution (inconsistent)';
      return;
    }
  } catch(e){
    out.value = 'Error analyzing equation';
    return;
  }
}

/* -------------------------
   Numeric system solver (Newton-Raphson)
   Input: array of equation strings (each can be eq with '=' or expression)
   Returns mapping {var: value} or null
   ------------------------- */
function solveSystemNumeric(equations){
  // parse equations and detect variables
  const exprs = equations.map(q => {
    const s = q.trim();
    let e = s;
    if(s.includes('=')){
      const p = s.split('=');
      e = '('+p[0]+') - ('+p.slice(1).join('=') + ')';
    }
    return e.replace(/\bX\b/g,'x').replace(/\bY\b/g,'y');
  });

  // detect variable names across all equations (single-letter or longer)
  const varSet = new Set();
  exprs.forEach(e=>{
    const all = (e.match(/[A-Za-z]+/g) || []).map(t => t.toLowerCase());
    const exclude = new Set(['pi','e','sin','cos','tan','log','log10','sqrt','exp','asin','acos','atan','ln','fact','factorial']);
    all.forEach(v=>{ if(!exclude.has(v)) varSet.add(v); });
  });
  const vars = Array.from(varSet);
  if(vars.length === 0) throw new Error('No variables detected in system');
  const n = vars.length;
  if(exprs.length < n) {
    // Underdetermined system (more unknowns than equations)
    // still attempt solve by numerical least-squares (we won't implement LS now)
    throw new Error('Underdetermined system: fewer equations than variables');
  }

  // compile functions
  const compiled = exprs.map(e => {
    try { return math.parse(e).compile(); } catch(e) { throw new Error('Parse error in system: ' + e.message); }
  });

  // helper: evaluate vector F at vector x (object mapping)
  const evalF = (vec) => {
    const scope = Object.fromEntries(vars.map((v,i)=>[v, vec[i]]));
    scope.pi = Math.PI;
    return compiled.map(c => {
      try{ return Number(c.evaluate(scope)); }catch(e){ return NaN; }
    });
  };

  // numeric jacobian via finite differences
  function jacobian(vec){
    const f0 = evalF(vec);
    const J = math.zeros(f0.length, vec.length);
    const h = 1e-6;
    for(let j=0;j<vec.length;j++){
      const vec2 = vec.slice(); vec2[j] += h;
      const f1 = evalF(vec2);
      for(let i=0;i<f0.length;i++){
        const d = (f1[i] - f0[i]) / h;
        J.subset(math.index(i,j), d);
      }
    }
    return {J, f0};
  }

  // initial guess: zeros or small randoms
  let x = new Array(n).fill(0);
  // try mild heuristic initializations if zeros fail
  for(let attempt=0; attempt<4; attempt++){
    try{
      let converged = false;
      for(let iter=0; iter<60; iter++){
        const {J, f0} = jacobian(x);
        const F = math.matrix(f0);
        // solve J * dx = -F
        // Convert to arrays for math.lusolve (expects matrix)
        let dx;
        try{
          const negF = math.multiply(F, -1);
          // Attempt robust solve using pseudo-inverse if square or overdetermined
          if(J.size()[0] === J.size()[1]){
            dx = math.lusolve(J, negF);
            dx = dx.map(v=>v[0]); // flatten
          } else {
            // least-squares: dx = inv(J^T J) J^T (-F)
            const JT = math.transpose(J);
            const JTJ = math.multiply(JT, J);
            const JTJinv = math.inv(JTJ);
            dx = math.multiply(math.multiply(JTJinv, JT), negF);
            dx = dx.toArray().map(r => (Array.isArray(r)? r[0] : r));
          }
        }catch(e){
          // fallback small perturbation
          dx = new Array(n).fill(0).map(()=> (Math.random()-0.5)*1e-3 );
        }
        // update x
        for(let k=0;k<n;k++) x[k] = x[k] + (Array.isArray(dx[k]) ? dx[k][0] : dx[k]);
        // check residual
        const res = evalF(x);
        const maxr = Math.max(...res.map(v=>Math.abs(v)));
        if(maxr < 1e-8){ converged = true; break; }
      }
      if(converged) break;
      // if not converged, try a better initial guess
      x = x.map(v=>v + (Math.random()-0.5)*2);
    }catch(e){
      x = x.map(v=>v + (Math.random()-0.5)*2);
    }
  }

  // final check
  const finalF = evalF(x);
  if(finalF.some(v=>!isFinite(v))) return null;
  const maxFinal = Math.max(...finalF.map(v=>Math.abs(v)));
  if(maxFinal > 1e-4) return null; // not accurate enough

  // prepare result object
  const result = {};
  for(let i=0;i<n;i++) result[vars[i]] = x[i];
  return result;
}

/* -------------------------
   Ruler/Distance helpers
   ------------------------- */
function calculateDistance(){ const s=parseFloat(el('measure-start').value)||0; const e=parseFloat(el('measure-end').value)||0; const d=Math.abs(e-s); el('distance-result').textContent = d.toFixed(2); }
function clearRuler(){ el('measure-start').value=''; el('measure-end').value=''; el('distance-result').textContent='0'; }

/* -------------------------
   Element lookup
   ------------------------- */
const ELEMENTS = {
  "hydrogen":"H","helium":"He","lithium":"Li","beryllium":"Be","boron":"B","carbon":"C","nitrogen":"N","oxygen":"O","fluorine":"F","neon":"Ne",
  "sodium":"Na","magnesium":"Mg","aluminium":"Al","aluminum":"Al","silicon":"Si","phosphorus":"P","sulfur":"S","sulphur":"S","chlorine":"Cl","argon":"Ar",
  "potassium":"K","calcium":"Ca","scandium":"Sc","titanium":"Ti","vanadium":"V","chromium":"Cr","manganese":"Mn","iron":"Fe","cobalt":"Co","nickel":"Ni",
  "copper":"Cu","zinc":"Zn","silver":"Ag","gold":"Au","lead":"Pb","tin":"Sn","mercury":"Hg","platinum":"Pt","uranium":"U","iodine":"I","selenium":"Se",
  "krypton":"Kr","xenon":"Xe","radon":"Rn"
};
const ELEMENT_SYM_TO_NAME = {};
Object.keys(ELEMENTS).forEach(name=>{
  const sym = ELEMENTS[name];
  ELEMENT_SYM_TO_NAME[sym.toLowerCase()] = name.charAt(0).toUpperCase() + name.slice(1);
});
function lookupElement(){
  const q = (el('element-query').value || '').trim().toLowerCase();
  const out = el('element-result');
  if(!q){ out.textContent = ''; return; }
  if(ELEMENTS[q]){
    out.textContent = `${capitalize(q)} — symbol: ${ELEMENTS[q]}`;
    return;
  }
  if(ELEMENT_SYM_TO_NAME[q]){
    out.textContent = `${ELEMENT_SYM_TO_NAME[q]} — symbol: ${q.toUpperCase()}`;
    return;
  }
  const matches = Object.keys(ELEMENTS).filter(n=>n.includes(q));
  if(matches.length>0){
    out.textContent = matches.slice(0,6).map(m=> `${capitalize(m)} (${ELEMENTS[m]})`).join(', ');
    return;
  }
  out.textContent = 'Not found';
}
function clearElement(){ el('element-query').value=''; el('element-result').textContent=''; }
function capitalize(s){ return s.charAt(0).toUpperCase() + s.slice(1); }

/* -------------------------
   Compass
   ------------------------- */
let compassEnabled = false;
function initCompass(){
  if(compassEnabled) return;
  if(typeof DeviceOrientationEvent !== 'undefined' && typeof DeviceOrientationEvent.requestPermission === 'function'){
    DeviceOrientationEvent.requestPermission().then(state=>{
      if(state==='granted'){ window.addEventListener('deviceorientation', handleOrientation); compassEnabled=true; el('toggleCompassBtn').textContent='Disable Compass'; }
      else alert('Permission denied (compass)');
    }).catch(()=> alert('Compass not supported'));
  } else if(typeof DeviceOrientationEvent !== 'undefined'){
    window.addEventListener('deviceorientation', handleOrientation); compassEnabled=true; el('toggleCompassBtn').textContent='Disable Compass';
  } else alert('Device orientation not supported');
}
function disableCompass(){
  window.removeEventListener('deviceorientation', handleOrientation);
  compassEnabled=false; el('toggleCompassBtn').textContent='Enable Compass';
}
function handleOrientation(e){
  let heading = e.alpha;
  if(heading===null||heading===undefined) heading=(e.gamma||0)*10;
  heading = (heading + 360) % 360;
  el('compass-needle').style.transform = 'translate(-50%,-100%) rotate('+heading+'deg)';
  el('compass-degree').textContent = Math.round(heading)+'°';
  const dirs = ['N','NNE','NE','ENE','E','ESE','SE','SSE','S','SSW','SW','WSW','W','WNW','NW','NNW'];
  const idx = Math.round((heading % 360) / 22.5) % 16;
  el('compass-direction-text').textContent = dirs[idx];
  const x = Math.cos(heading*Math.PI/180).toFixed(2), y = Math.sin(heading*Math.PI/180).toFixed(2);
  el('coordinates').textContent = x + ', ' + y;
}
el('toggleCompassBtn').addEventListener('click', ()=>{
  if(!compassEnabled) initCompass(); else disableCompass();
});
el('compassFaceUpload').addEventListener('change', (e)=>{
  const f = e.target.files && e.target.files[0]; if(!f) return;
  const r = new FileReader();
  r.onload = function(){ el('compass-face').style.backgroundImage = 'url('+r.result+')'; };
  r.readAsDataURL(f);
});
function setCompassPreset(p){ if(p==='dark') el('compass-face').style.backgroundImage = 'radial-gradient(circle at 30% 20%, rgba(255,255,255,0.02), rgba(0,0,0,0.6))'; }

/* -------------------------
   Theme system (presets + light/dark toggle)
   ------------------------- */
function applyPreset(name){
  document.documentElement.removeAttribute('data-theme');
  document.documentElement.style.setProperty('--bg','linear-gradient(135deg,#0b0f12,#112026)');
  document.documentElement.style.setProperty('--card-bg','#0f1720');
  document.documentElement.style.setProperty('--text','#e6eef3');
  document.documentElement.style.setProperty('--muted','#9aa7b2');
  document.documentElement.style.setProperty('--key-bg','rgba(255,255,255,0.03)');
  document.documentElement.style.setProperty('--key-fore','#e6eef3');

  if(name==='blackgold'){
    document.documentElement.style.setProperty('--accent','#d4af37');
    document.documentElement.style.setProperty('--accent-2','#f3d87a');
  } else if(name==='orange'){
    document.documentElement.style.setProperty('--accent','#ff7a18');
    document.documentElement.style.setProperty('--accent-2','#ffb86b');
  } else if(name==='whiteblue'){
    document.documentElement.setAttribute('data-theme','light');
    document.documentElement.style.setProperty('--accent','#1f6feb');
    document.documentElement.style.setProperty('--accent-2','#7fb3ff');
  } else if(name==='neon'){
    document.documentElement.style.setProperty('--accent','#ff3d81');
    document.documentElement.style.setProperty('--accent-2','#8c7bff');
  } else if(name==='darkclassic'){
    document.documentElement.style.setProperty('--accent','#3dd0ff');
    document.documentElement.style.setProperty('--accent-2','#7ef5b8');
  } else if(name==='lightclassic'){
    document.documentElement.setAttribute('data-theme','light');
    document.documentElement.style.setProperty('--accent','#2b8bd6');
    document.documentElement.style.setProperty('--accent-2','#7fb3ff');
  }
  const accent = getComputedStyle(document.documentElement).getPropertyValue('--accent');
  const accent2 = getComputedStyle(document.documentElement).getPropertyValue('--accent-2');
  el('themePreview').style.background = `linear-gradient(90deg, ${accent}, ${accent2})`;
  const c = (accent || '#0f1720').trim();
  const meta = el('meta-theme-color'); if(meta) meta.setAttribute('content', c);
  try{ localStorage.setItem('aurora_theme', name); }catch(e){}
}
el('applyThemeBtn').addEventListener('click', ()=> applyPreset(el('themeSelect').value));
el('toggleLightBtn').addEventListener('click', ()=>{
  const root = document.documentElement;
  if(root.getAttribute('data-theme')==='light') { root.removeAttribute('data-theme'); try{ localStorage.setItem('aurora_theme_mode','dark'); }catch(e){} }
  else { root.setAttribute('data-theme','light'); try{ localStorage.setItem('aurora_theme_mode','light'); }catch(e){} }
});
(function(){
  try{
    const t = localStorage.getItem('aurora_theme');
    if(t) applyPreset(t);
    const mode = localStorage.getItem('aurora_theme_mode');
    if(mode === 'light') document.documentElement.setAttribute('data-theme','light');
    else if(mode === null){
      if(window.matchMedia && window.matchMedia('(prefers-color-scheme: light)').matches){
        document.documentElement.setAttribute('data-theme','light');
      }
    }
  }catch(e){}
})();

/* -------------------------
   Keyboard behavior & initialization
   ------------------------- */
document.addEventListener('keydown', (ev)=>{
  const active = document.activeElement;
  if(!active) return;
  if(ev.key === 'Enter'){
    if(active.id === 'display-calculator'){ ev.preventDefault(); evaluateAndStore('calculator'); }
    else if(active.id === 'display-scientific'){ ev.preventDefault(); evaluateAndStore('scientific'); }
    else if(active.id === 'function-input'){ ev.preventDefault(); plotFunction(); }
    else if(active.id === 'equation-input'){ ev.preventDefault(); solveEquation(); }
    else if(active.id === 'element-query'){ ev.preventDefault(); lookupElement(); }
  }
});

applyPreset('blackgold');
el('display-calculator').value = '0';

/* -------------------------
   Optional: service worker registration (for PWA)
   ------------------------- */
if('serviceWorker' in navigator){
  try{
    navigator.serviceWorker.register('/sw.js').then(reg=>{
      console.log('Service worker registered', reg.scope);
    }).catch(err=>console.log('SW register failed:', err));
  }catch(e){}
}
</script>
</body>
</html>
````

---

## USER: Additional messages & requests (chronological)

1. **User:** "Let's finalize aurora math suite...don't reply until asked, for now I am pasting the finalized code : [HTML pasted above]"

2. **User:** (Pasted the HTML again — large block; same code repeated.)

3. **User:** "Can you repeat the exact code in one single code format block?"

4. **User:** "Does this include and without error as we had discussed for aurora math suite?"

5. **User:** "Insert the latch and reprint"

6. **User:** "Is it all good now?"

7. **User:** "Can you work on all the suggestions you mentioned or library that you want to add with platform issues and convert this into code and ammend it in the final code, also check the code, verify it and make sure to rectify any errors or additions required. Post this we will move to the pwa and mobile deployment like for android, ios and even whop.."

   * The user then pasted a detailed product/cofounder prompt specifying how they want to build, validate, monetize, distribute, and track apps. (Large instruction set; not repeated here to keep transcript compact — see chat history if needed.)

8. **User:** "create a .md file for this entire chat in a single code block to copy and paste?"

---

## NOTES / ACTION ITEMS (from user requests)

* The user asked to have the entire chat exported as a `.md` file in a single code block for copy-paste. This file is that export.
* The user previously asked to repeat the exact code in one single code block (the code above is kept intact in an HTML code block).
* The user requested further work (add latch, libraries, PWA support, platform packaging, monetization/distribution playbooks, and an enormous productization checklist). Those tasks were requested but not executed in this transcript file — they remain to be completed in follow-up steps.

---

## End of transcript

```
```
