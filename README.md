<!DOCTYPE html>

<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>BikeFit</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

:root {
–bg:       #0f1117;
–surface:  #181c26;
–surface2: #1e2333;
–border:   #272e42;
–yellow:   #f4ff00;
–yellow2:  #e0f500;
–text:     #ffffff;
–muted:    #8892a4;
–card-bg:  #161b28;
–mtb:      #eeff41;
–renn:     #ff5252;
–trek:     #40c4ff;
–city:     #ff9800;
}

html, body {
height: 100%;
background: #0f1117 !important;
background-color: #0f1117 !important;
color: #ffffff !important;
font-family: ‘DM Sans’, sans-serif;
overflow: hidden;
}

/* Force dark everywhere */

- { color: inherit; }

/* Grid texture like screenshot */
body::before {
content: ‘’;
position: fixed; inset: 0;
background-image:
linear-gradient(rgba(255,255,255,0.025) 1px, transparent 1px),
linear-gradient(90deg, rgba(255,255,255,0.025) 1px, transparent 1px);
background-size: 36px 36px;
pointer-events: none; z-index: 0;
}

/* ── APP SHELL ── */
.app {
max-width: 430px;
margin: 0 auto;
height: 100dvh;
display: flex; flex-direction: column;
position: relative; z-index: 1;
overflow: hidden;
background: #0f1117 !important;
color: #ffffff !important;
}

/* ── TOP BAR (like screenshot nav) ── */
.topbar {
padding: 14px 18px 10px;
display: flex; align-items: flex-start; justify-content: space-between;
flex-shrink: 0;
background: #0f1117 !important;
}

.logo-block {}
.logo-text {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 2rem; letter-spacing: 3px; line-height: 1;
}
.logo-text .y { color: var(–yellow); }
.logo-text .w { color: var(–text); }
.logo-tagline {
font-size: 0.6rem; letter-spacing: 2px;
text-transform: uppercase; color: #8892a4 !important;
margin-top: 2px;
}

.shop-badge {
background: var(–surface2);
border: 1px solid var(–border);
border-radius: 10px;
padding: 8px 13px;
text-align: right;
font-size: 0.72rem; color: var(–muted);
max-width: 160px;
}
.shop-badge strong { color: var(–text); display: block; font-size: 0.8rem; font-weight: 600; }

/* ── PROGRESS BAR (3 segments like screenshot) ── */
.seg-bar {
display: flex; gap: 6px;
padding: 10px 18px 14px;
flex-shrink: 0;
background: #0f1117 !important;
}
.seg {
flex: 1; height: 4px; border-radius: 2px;
background: var(–border);
transition: background 0.4s;
}
.seg.done   { background: var(–yellow); opacity: 0.5; }
.seg.active { background: var(–yellow); }

/* ── SCROLL BODY ── */
.scroll-body {
flex: 1; overflow-y: auto; overflow-x: hidden;
-webkit-overflow-scrolling: touch;
padding: 0 18px 100px;
background: #0f1117 !important;
color: #ffffff !important;
}

/* ── BOTTOM BAR ── */
.bottom-bar {
position: absolute; bottom: 0; left: 0; right: 0;
padding: 12px 18px calc(12px + env(safe-area-inset-bottom));
background: #0f1117 !important;
border-top: 1px solid #272e42;
z-index: 50;
}

.btn-main {
width: 100%;
background: var(–yellow);
color: #0f1117;
border: none; border-radius: 14px;
padding: 17px;
font-family: ‘Bebas Neue’, sans-serif;
font-size: 1.2rem; letter-spacing: 2px;
cursor: pointer; display: flex; align-items: center; justify-content: center; gap: 8px;
transition: all 0.2s;
}
.btn-main:active { transform: scale(0.97); }
.btn-main:disabled { background: #3a4020; color: #6b7040; cursor: not-allowed; transform: none; }
.btn-main.dim { background: #4a5225; color: #8b9040; }

.btn-ghost {
width: 100%; background: transparent;
border: none; color: var(–muted);
font-size: 0.84rem; padding: 9px;
cursor: pointer; font-family: ‘DM Sans’, sans-serif;
}

/* ── SCREENS ── */
.screen { display: none; }
.screen.active { display: block; animation: fadeUp 0.3s ease both; }
@keyframes fadeUp { from { opacity:0; transform:translateY(14px); } to { opacity:1; transform:none; } }

/* ══════════════════════
SCREEN 0 — MODE
══════════════════════ */
.page-title {
font-family: ‘Bebas Neue’, sans-serif;
font-size: 2.6rem; letter-spacing: 2px; line-height: 1.05;
margin-bottom: 8px;
color: #ffffff !important;
}
.page-title .y { color: var(–yellow); }

.page-sub { font-size: 0.88rem; color: #8892a4 !important; line-height: 1.6; margin-bottom: 26px; }

.mode-cards { display: flex; flex-direction: column; gap: 12px; }
.mode-card {
background: var(–card-bg);
border: 1px solid var(–border);
border-radius: 16px;
padding: 18px 16px;
display: flex; align-items: center; gap: 14px;
cursor: pointer; transition: all 0.2s;
}
.mode-card:active { border-color: var(–yellow); background: #1e2a10; }
.mode-ico {
width: 50px; height: 50px; flex-shrink: 0;
background: var(–surface2); border-radius: 13px;
display: flex; align-items: center; justify-content: center; font-size: 1.6rem;
}
.mode-info { flex: 1; }
.mode-title { font-size: 0.98rem; font-weight: 700; margin-bottom: 3px; color: #ffffff !important; }
.mode-desc  { font-size: 0.76rem; color: #8892a4 !important; line-height: 1.4; }
.mode-arrow { color: var(–yellow); font-size: 1.3rem; }

/* ══════════════════════
SCREEN 1 — GENDER (exact screenshot)
══════════════════════ */
.gender-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-bottom: 20px; }

.gender-card {
background: var(–card-bg);
border: 2px solid var(–border);
border-radius: 16px;
padding: 32px 14px 24px;
text-align: center; cursor: pointer;
transition: all 0.2s;
}
.gender-card.sel {
border-color: var(–yellow);
background: #1c2610;
}
.gender-card .g-em  { font-size: 2.6rem; margin-bottom: 12px; }
.gender-card .g-lbl { font-size: 1rem; font-weight: 600; }

/* ══════════════════════
SCREEN 2 — INPUTS (exact screenshot style)
══════════════════════ */
.hint-card {
background: var(–card-bg);
border: 1px solid var(–border);
border-radius: 14px;
padding: 14px 16px;
margin-bottom: 16px;
display: flex; gap: 12px; align-items: flex-start;
}
.hint-card .h-ico { font-size: 1.2rem; flex-shrink: 0; color: var(–muted); margin-top: 1px; }
.hint-card .h-txt { font-size: 0.78rem; color: var(–muted); line-height: 1.65; }
.hint-card .h-txt strong { color: var(–text); }

.inp-field {
background: var(–card-bg);
border: 1px solid var(–border);
border-radius: 14px;
padding: 16px 18px 14px;
margin-bottom: 10px;
transition: border-color 0.2s;
}
.inp-field:focus-within { border-color: var(–yellow); }

.inp-top {
display: flex; align-items: center; gap: 8px;
margin-bottom: 6px;
}
.inp-code-badge {
width: 20px; height: 20px; border-radius: 5px;
display: flex; align-items: center; justify-content: center;
font-size: 0.7rem; font-weight: 800; letter-spacing: 0;
}
.inp-code-badge.L { background: #eeff41; color: #0f1117; }
.inp-code-badge.I { background: #40c4ff; color: #0f1117; }
.inp-code-badge.A { background: #eeff41; color: #0f1117; }
.inp-code-badge.R { background: #ff9800; color: #0f1117; }

.inp-lbl-text {
font-size: 0.65rem; letter-spacing: 2px;
text-transform: uppercase; color: var(–muted); font-weight: 600;
}

.inp-row { display: flex; align-items: baseline; justify-content: space-between; }
.inp-row input {
background: transparent; border: none; outline: none;
color: var(–text);
font-family: ‘Bebas Neue’, sans-serif;
font-size: 2.2rem; letter-spacing: 1px;
width: 100%;
}
.inp-row input::placeholder { color: var(–border); }
.inp-unit { font-size: 0.78rem; color: var(–muted); font-weight: 500; }

/* ══════════════════════
SCREEN 3 — PHOTO UPLOAD
══════════════════════ */
.upload-card {
background: var(–card-bg);
border: 1px solid var(–border);
border-radius: 18px; padding: 24px 18px 20px;
text-align: center; margin-bottom: 14px;
}
.upload-card .u-ico {
width: 68px; height: 68px; border-radius: 18px;
background: var(–surface2); margin: 0 auto 16px;
display: flex; align-items: center; justify-content: center;
font-size: 2rem;
}
.upload-card h3 { font-size: 1.1rem; font-weight: 700; margin-bottom: 6px; }
.upload-card p  { font-size: 0.8rem; color: var(–muted); line-height: 1.5; margin-bottom: 16px; }

.drop-zone {
border: 2px dashed var(–border);
border-radius: 12px; padding: 28px 14px;
cursor: pointer; transition: all 0.2s;
}
.drop-zone:active { border-color: var(–yellow); background: #1c2610; }
#previewImg { width: 100%; max-height: 200px; object-fit: cover; border-radius: 8px; display: none; }
.dp-ico  { font-size: 1.8rem; margin-bottom: 6px; }
.dp-txt  { font-size: 0.8rem; color: var(–muted); }
.dp-txt strong { color: var(–yellow); font-weight: 600; }

.tips-row { display: grid; grid-template-columns: repeat(3,1fr); gap: 8px; }
.tip-c { background: var(–card-bg); border: 1px solid var(–border); border-radius: 12px; padding: 12px 8px; text-align: center; }
.tip-c .t-e { font-size: 1.2rem; margin-bottom: 4px; }
.tip-c .t-t { font-size: 0.68rem; font-weight: 700; margin-bottom: 2px; }
.tip-c .t-d { font-size: 0.6rem; color: var(–muted); line-height: 1.4; }

/* ══════════════════════
SCREEN 4 — SCANNING
══════════════════════ */
.scan-card {
background: var(–card-bg); border: 1px solid var(–border);
border-radius: 18px; overflow: hidden; margin-bottom: 14px;
}
.scan-photo-box {
position: relative; background: #080c10;
min-height: 240px; display: flex; align-items: center; justify-content: center;
overflow: hidden;
}
#scanPhoto { width: 100%; max-height: 280px; object-fit: contain; display: block; }
.scan-ui { position: absolute; inset: 0; pointer-events: none; }
.corner { position: absolute; width: 20px; height: 20px; border-color: var(–yellow); border-style: solid; }
.corner.tl { top:10px; left:10px;  border-width:2px 0 0 2px; }
.corner.tr { top:10px; right:10px; border-width:2px 2px 0 0; }
.corner.bl { bottom:10px; left:10px;  border-width:0 0 2px 2px; }
.corner.br { bottom:10px; right:10px; border-width:0 2px 2px 0; }
.sweep {
position: absolute; left:0; right:0; height:2px;
background: linear-gradient(90deg,transparent,var(–yellow),transparent);
box-shadow: 0 0 12px var(–yellow);
animation: swp 2.2s ease-in-out infinite;
}
@keyframes swp { 0%{top:3%;opacity:0} 8%{opacity:1} 92%{opacity:1} 100%{top:97%;opacity:0} }
.ldot {
position: absolute; width:10px; height:10px; border-radius:50%;
background: var(–yellow); border:2px solid rgba(255,255,255,.8);
transform: translate(-50%,-50%) scale(0);
transition: transform .3s cubic-bezier(.34,1.56,.64,1);
box-shadow: 0 0 8px var(–yellow);
}
.ldot.show { transform: translate(-50%,-50%) scale(1); }
.ldot-lbl { position:absolute; left:13px; top:50%; transform:translateY(-50%); font-size:8px; font-weight:800; color:var(–yellow); white-space:nowrap; text-shadow:0 1px 4px #000; letter-spacing:.5px; }

.scan-steps { padding: 14px 16px 12px; }
.ss { display:flex; align-items:center; gap:12px; padding:9px 0; border-bottom:1px solid var(–surface2); opacity:.28; transition:opacity .3s; }
.ss:last-child { border-bottom:none; }
.ss.active { opacity:1; }
.ss.done   { opacity:.6; }
.ss-ico { width:32px; height:32px; border-radius:9px; background:var(–surface2); display:flex; align-items:center; justify-content:center; font-size:.95rem; flex-shrink:0; }
.ss.active .ss-ico { background:#1e2a10; }
.ss-txt { flex:1; }
.ss-name { font-size:.82rem; font-weight:600; }
.ss-det  { font-size:.68rem; color:var(–muted); margin-top:1px; }
.ss-bar  { height:3px; background:var(–border); border-radius:2px; margin-top:4px; overflow:hidden; }
.ss-fill { height:100%; background:var(–yellow); border-radius:2px; width:0%; transition:width .8s ease; }
.ss-chk  { font-size:.95rem; opacity:0; transition:opacity .3s; flex-shrink:0; }
.ss.done .ss-chk { opacity:1; }

/* ══════════════════════
SCREEN 5 — RESULTS
══════════════════════ */
.res-hero {
background: linear-gradient(135deg, #1e3012 0%, #162008 100%);
border: 1px solid #4a6a28;
border-radius: 18px; padding: 20px 18px;
display: flex; align-items: center; gap: 14px;
margin-bottom: 16px;
}
.res-av {
width:48px; height:48px; flex-shrink:0;
background:rgba(238,255,65,.12); border-radius:13px;
display:flex; align-items:center; justify-content:center; font-size:1.5rem;
}
.res-info { flex:1; }
.res-info h2 { font-family:‘Bebas Neue’,sans-serif; font-size:1.2rem; letter-spacing:1px; margin-bottom:3px; }
.res-info p  { font-size:.74rem; color:var(–muted); }
.konf-badge {
background:var(–yellow); color:#0f1117;
font-size:.68rem; font-weight:800; padding:4px 10px; border-radius:20px; flex-shrink:0;
}

.sec-lbl {
font-size:.62rem; font-weight:700; letter-spacing:2px;
text-transform:uppercase; color:var(–muted); margin:18px 0 9px;
}

/* Measurement chips */
.meas-row { display:flex; gap:9px; overflow-x:auto; -webkit-overflow-scrolling:touch; scrollbar-width:none; padding-bottom:2px; }
.meas-row::-webkit-scrollbar { display:none; }
.mchip {
background:var(–card-bg); border:1px solid var(–border);
border-radius:13px; padding:12px 14px; flex-shrink:0; min-width:78px; text-align:center;
}
.mc-badge { display:inline-block; font-size:.68rem; font-weight:800; padding:2px 7px; border-radius:5px; margin-bottom:5px; }
.mc-badge.L { background:var(–yellow); color:#0f1117; }
.mc-badge.I { background:#40c4ff; color:#0f1117; }
.mc-badge.A { background:var(–yellow); color:#0f1117; }
.mc-badge.R { background:#ff9800; color:#0f1117; }
.mc-badge.S { background:#ff5252; color:#fff; }
.mc-val  { font-family:‘Bebas Neue’,sans-serif; font-size:1.3rem; letter-spacing:1px; display:block; margin-bottom:2px; }
.mc-name { font-size:.6rem; color:var(–muted); line-height:1.3; }

/* Bike cards */
.bike-col { display:flex; flex-direction:column; gap:10px; }
.bcard {
background:var(–card-bg); border:1.5px solid var(–border);
border-radius:14px; padding:13px 14px;
display:flex; align-items:center; gap:13px;
position:relative; transition:all .2s;
}
.bcard.best { border-color:var(–yellow); background:#161c08; }
.best-tag {
position:absolute; top:-1px; right:12px;
background:var(–yellow); color:#0f1117;
font-size:.56rem; font-weight:800; letter-spacing:.5px;
text-transform:uppercase; padding:3px 8px; border-radius:0 0 7px 7px;
}
.bcard-em   { font-size:1.9rem; flex-shrink:0; }
.bcard-info { flex:1; min-width:0; }
.bcard-name { font-size:.9rem; font-weight:700; margin-bottom:2px; }
.bcard-frame {
display:inline-block; font-size:.74rem; font-weight:700;
padding:2px 9px; border-radius:20px; color:#0f1117; margin-bottom:5px;
}
.bcard-frame.mtb  { background:var(–yellow); }
.bcard-frame.renn { background:var(–renn); color:#fff; }
.bcard-frame.trek { background:var(–trek); }
.bcard-frame.city { background:var(–city); color:#0f1117; }
.bcard-bar  { height:3px; background:var(–border); border-radius:2px; overflow:hidden; }
.bcard-fill { height:100%; border-radius:2px; transition:width 1.2s cubic-bezier(.4,0,.2,1); width:0%; }
.bcard-fill.mtb  { background:var(–yellow); }
.bcard-fill.renn { background:var(–renn); }
.bcard-fill.trek { background:var(–trek); }
.bcard-fill.city { background:var(–city); }
.bcard-pct { font-family:‘Bebas Neue’,sans-serif; font-size:1.1rem; letter-spacing:1px; flex-shrink:0; }
.bcard-pct.mtb  { color:var(–yellow); }
.bcard-pct.renn { color:var(–renn); }
.bcard-pct.trek { color:var(–trek); }
.bcard-pct.city { color:var(–city); }

/* Sitzposition */
.sitz-block { background:var(–card-bg); border:1px solid var(–border); border-radius:14px; overflow:hidden; }
.sitz-row { display:flex; align-items:center; padding:11px 14px; border-bottom:1px solid var(–surface2); }
.sitz-row:last-child { border-bottom:none; }
.sitz-num {
width:22px; height:22px; border-radius:50%;
background:var(–yellow); color:#0f1117;
font-size:.68rem; font-weight:800;
display:flex; align-items:center; justify-content:center; flex-shrink:0; margin-right:10px;
}
.sitz-name { flex:1; font-size:.8rem; }
.sitz-val  { font-family:‘Bebas Neue’,sans-serif; font-size:1rem; letter-spacing:1px; color:var(–yellow); margin-right:5px; }
.sitz-unit { font-size:.68rem; color:var(–muted); }

.hint-res {
background:var(–surface2); border:1px solid var(–border);
border-radius:12px; padding:11px 13px;
font-size:.75rem; color:var(–muted); line-height:1.5; margin-top:4px;
}
.hint-res strong { color:var(–text); }

.spacer { height:20px; }

#fileInput { display:none; }
@keyframes spin { to { transform:rotate(360deg); } }
.spin { display:inline-block; animation:spin .7s linear infinite; }
</style>

</head>
<body>
<div class="app">

  <!-- TOP BAR -->

  <div class="topbar">
    <div class="logo-block">
      <div class="logo-text"><span class="y">BIKE</span><span class="w">FIT</span></div>
      <div class="logo-tagline">Fahrrad · Vermessung · Beratung</div>
    </div>
    <div class="shop-badge">
      🚲 Ihr<br>
      <strong>Fahrradgeschäft</strong>
      Ergonomie-Beratung
    </div>
  </div>

  <!-- SEGMENT PROGRESS -->

  <div class="seg-bar">
    <div class="seg" id="seg0"></div>
    <div class="seg" id="seg1"></div>
    <div class="seg" id="seg2"></div>
  </div>

  <!-- SCROLL -->

  <div class="scroll-body" id="scrollBody">

```
<!-- ── S0: MODE SELECT ── -->
<div class="screen active" id="s0">
  <div class="page-title">WILLKOMMEN BEI<br><span class="y">BIKEFIT</span></div>
  <div class="page-sub">Wählen Sie Ihre Methode für die optimale Fahrradberatung.</div>
  <div class="mode-cards">
    <div class="mode-card" onclick="selectMode('photo')">
      <div class="mode-ico">📸</div>
      <div class="mode-info">
        <div class="mode-title">Foto-Scan (KI)</div>
        <div class="mode-desc">Foto aufnehmen → KI analysiert Körpermaße automatisch</div>
      </div>
      <div class="mode-arrow">›</div>
    </div>
    <div class="mode-card" onclick="selectMode('manual')">
      <div class="mode-ico">📐</div>
      <div class="mode-info">
        <div class="mode-title">Manuelle Eingabe</div>
        <div class="mode-desc">Körpermaße nach Messblatt Fahrer (Seite 365) eingeben</div>
      </div>
      <div class="mode-arrow">›</div>
    </div>
  </div>
</div>

<!-- ── S1: GENDER (exact screenshot) ── -->
<div class="screen" id="s1">
  <div class="page-title">WILLKOMMEN BEI<br><span class="y">BIKEFIT</span></div>
  <div class="page-sub">Wählen Sie zunächst Ihr Geschlecht für die korrekte Körpermaßtabelle.</div>
  <div class="gender-grid">
    <div class="gender-card" id="gm" onclick="selGender('männlich',this)">
      <div class="g-em">🧑</div>
      <div class="g-lbl">Männlich</div>
    </div>
    <div class="gender-card" id="gw" onclick="selGender('weiblich',this)">
      <div class="g-em">👩</div>
      <div class="g-lbl">Weiblich</div>
    </div>
  </div>
</div>

<!-- ── S2: MANUAL INPUT (exact screenshot) ── -->
<div class="screen" id="s2">
  <div class="page-title">KÖRPER<span class="y">MASSE</span></div>
  <div class="page-sub">Geben Sie Ihre Maße ein — wir berechnen die optimale Rahmengröße.</div>

  <div class="hint-card">
    <div class="h-ico">▲</div>
    <div class="h-txt">
      <strong>Messblatt Fahrer (Seite 365):</strong><br>
      L = Körperlänge · I = Innenbeinlänge (Schrittlänge) · A = Armlänge · R = Rumpflänge<br>
      Alle Maße in <strong>Millimeter (mm)</strong> eingeben.
    </div>
  </div>

  <div class="inp-field">
    <div class="inp-top">
      <span class="inp-code-badge L">L</span>
      <span class="inp-lbl-text">Körperlänge</span>
    </div>
    <div class="inp-row">
      <input type="number" id="mL" placeholder="1750" min="1400" max="2200" oninput="checkManual()">
      <span class="inp-unit">mm</span>
    </div>
  </div>

  <div class="inp-field">
    <div class="inp-top">
      <span class="inp-code-badge I">I</span>
      <span class="inp-lbl-text">Innenbeinlänge</span>
    </div>
    <div class="inp-row">
      <input type="number" id="mI" placeholder="830" min="600" max="1100" oninput="checkManual()">
      <span class="inp-unit">mm</span>
    </div>
  </div>

  <div class="inp-field">
    <div class="inp-top">
      <span class="inp-code-badge A">A</span>
      <span class="inp-lbl-text">Armlänge</span>
    </div>
    <div class="inp-row">
      <input type="number" id="mA" placeholder="651" min="400" max="900" oninput="checkManual()">
      <span class="inp-unit">mm</span>
    </div>
  </div>

  <div class="inp-field">
    <div class="inp-top">
      <span class="inp-code-badge R">R</span>
      <span class="inp-lbl-text">Rumpflänge</span>
    </div>
    <div class="inp-row">
      <input type="number" id="mR" placeholder="563" min="300" max="800" oninput="checkManual()">
      <span class="inp-unit">mm</span>
    </div>
  </div>
</div>

<!-- ── S3: PHOTO UPLOAD ── -->
<div class="screen" id="s3">
  <div class="upload-card">
    <div class="u-ico">📸</div>
    <h3>Foto aufnehmen</h3>
    <p>KI erkennt Körperpunkte und berechnet Rahmengröße für MTB, Rennrad, Trekking & City.</p>
    <div class="drop-zone" id="dropZone" onclick="document.getElementById('fileInput').click()">
      <img id="previewImg" alt="">
      <div id="dropPH">
        <div class="dp-ico">🖼️</div>
        <div class="dp-txt">Tippen zum <strong>Foto auswählen</strong></div>
      </div>
    </div>
  </div>
  <div class="tips-row">
    <div class="tip-c"><div class="t-e">🧍</div><div class="t-t">Ganzkörper</div><div class="t-d">Kopf bis Fuß</div></div>
    <div class="tip-c"><div class="t-e">💡</div><div class="t-t">Heller BG</div><div class="t-d">Gleichm. Licht</div></div>
    <div class="tip-c"><div class="t-e">👕</div><div class="t-t">Enganliegend</div><div class="t-d">Sportkleidung</div></div>
  </div>
  <input type="file" id="fileInput" accept="image/*">
</div>

<!-- ── S3b: HEIGHT INPUT after photo ── -->
<div class="screen" id="s3b">
  <div style="margin-bottom:16px;">
    <div style="background:#181c26;border:1px solid #272e42;border-radius:16px;overflow:hidden;">
      <img id="heightPreviewImg" src="" alt="" style="width:100%;max-height:220px;object-fit:cover;display:block;">
    </div>
  </div>

  <div style="background:#181c26;border:1px solid #272e42;border-radius:16px;padding:20px 18px;">
    <div style="font-family:'Bebas Neue',sans-serif;font-size:1.4rem;letter-spacing:2px;color:#ffffff;margin-bottom:6px;">
      KÖRPERGRÖSSE <span style="color:#f4ff00;">EINGEBEN</span>
    </div>
    <div style="font-size:0.82rem;color:#8892a4;margin-bottom:20px;line-height:1.5;">
      Geben Sie die Körpergröße ein — damit werden die Körperpunkte präzise berechnet.
    </div>

    <div style="background:#0f1117;border:1.5px solid #272e42;border-radius:12px;padding:16px 18px;margin-bottom:8px;" id="heightInputField">
      <div style="display:flex;align-items:center;gap:8px;margin-bottom:6px;">
        <span style="background:#f4ff00;color:#0f1117;font-size:0.7rem;font-weight:800;padding:2px 8px;border-radius:5px;">L</span>
        <span style="font-size:0.65rem;letter-spacing:2px;text-transform:uppercase;color:#8892a4;font-weight:600;">Körpergröße</span>
      </div>
      <div style="display:flex;align-items:baseline;gap:8px;">
        <input type="number" id="heightInput" placeholder="175"
          min="140" max="220"
          oninput="checkHeightInput()"
          style="background:transparent;border:none;outline:none;color:#ffffff;font-family:'Bebas Neue',sans-serif;font-size:3rem;letter-spacing:2px;width:100%;">
        <span style="color:#8892a4;font-size:0.9rem;font-weight:500;">cm</span>
      </div>
    </div>

    <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-top:14px;">
      <div onclick="setHeight(160)" style="background:#1e2333;border:1px solid #272e42;border-radius:10px;padding:10px 6px;text-align:center;cursor:pointer;font-size:0.82rem;font-weight:600;color:#8892a4;" class="h-preset">160</div>
      <div onclick="setHeight(170)" style="background:#1e2333;border:1px solid #272e42;border-radius:10px;padding:10px 6px;text-align:center;cursor:pointer;font-size:0.82rem;font-weight:600;color:#8892a4;" class="h-preset">170</div>
      <div onclick="setHeight(180)" style="background:#1e2333;border:1px solid #272e42;border-radius:10px;padding:10px 6px;text-align:center;cursor:pointer;font-size:0.82rem;font-weight:600;color:#8892a4;" class="h-preset">180</div>
      <div onclick="setHeight(190)" style="background:#1e2333;border:1px solid #272e42;border-radius:10px;padding:10px 6px;text-align:center;cursor:pointer;font-size:0.82rem;font-weight:600;color:#8892a4;" class="h-preset">190</div>
    </div>
  </div>
</div>

<!-- ── S4: SCANNING ── -->
<div class="screen" id="s4">
  <div class="scan-card">
    <div class="scan-photo-box" id="scanBox">
      <img id="scanPhoto" src="" alt="">
      <div class="scan-ui" id="scanUi">
        <div class="corner tl"></div><div class="corner tr"></div>
        <div class="corner bl"></div><div class="corner br"></div>
        <div class="sweep"></div>
      </div>
    </div>
    <div class="scan-steps">
      <div class="ss" id="ss0"><div class="ss-ico">🧍</div><div class="ss-txt"><div class="ss-name">Person erkennen</div><div class="ss-det">Körperkontur analysieren</div><div class="ss-bar"><div class="ss-fill" id="sf0"></div></div></div><div class="ss-chk">✅</div></div>
      <div class="ss" id="ss1"><div class="ss-ico">📍</div><div class="ss-txt"><div class="ss-name">Körperpunkte markieren</div><div class="ss-det">Gelenke & Messpunkte</div><div class="ss-bar"><div class="ss-fill" id="sf1"></div></div></div><div class="ss-chk">✅</div></div>
      <div class="ss" id="ss2"><div class="ss-ico">📐</div><div class="ss-txt"><div class="ss-name">Körpermaße berechnen</div><div class="ss-det">L · I · A · R · S</div><div class="ss-bar"><div class="ss-fill" id="sf2"></div></div></div><div class="ss-chk">✅</div></div>
      <div class="ss" id="ss3"><div class="ss-ico">🚲</div><div class="ss-txt"><div class="ss-name">Rahmengröße ermitteln</div><div class="ss-det">MTB · Rennrad · Trekking · City</div><div class="ss-bar"><div class="ss-fill" id="sf3"></div></div></div><div class="ss-chk">✅</div></div>
    </div>
  </div>
</div>

<!-- ── S5: RESULTS ── -->
<div class="screen" id="s5">
  <!-- Kunde photo thumbnail -->
  <div id="kundePhotoWrap" style="display:none; margin-bottom:12px;">
    <div style="position:relative; border-radius:16px; overflow:hidden; background:#0f1117; border:1px solid #272e42;">
      <img id="kundePhoto" src="" alt="Kunde" style="width:100%; max-height:200px; object-fit:cover; display:block;">
      <div style="position:absolute; top:10px; left:10px; background:rgba(0,0,0,0.6); border:1px solid #272e42; border-radius:8px; padding:5px 10px; font-size:0.72rem; color:#eeff41; font-weight:700; letter-spacing:1px;">📸 KUNDE</div>
    </div>
  </div>

  <div class="res-hero">
    <div class="res-av" id="resAv">👤</div>
    <div class="res-info">
      <h2 id="resTitle">Analyse fertig</h2>
      <p id="resSub">—</p>
    </div>
    <div class="konf-badge" id="konfB">—</div>
  </div>

  <div class="sec-lbl">📐 Körpermaße</div>
  <div class="meas-row" id="measRow"></div>

  <div class="sec-lbl">🚲 Fahrrad-Empfehlung</div>
  <div class="bike-col" id="bikeCol"></div>

  <div class="sec-lbl">🪑 Sitzposition</div>
  <div class="sitz-block" id="sitzBlock"></div>

  <div id="hintResWrap"></div>
  <div class="spacer"></div>
</div>
```

  </div><!-- /scroll-body -->

  <!-- BOTTOM BAR -->

  <div class="bottom-bar">
    <button class="btn-main" id="btnMain" onclick="handleBtn()">Methode wählen</button>
    <button class="btn-ghost" id="btnBack" style="display:none" onclick="handleBack()">← Zurück</button>
  </div>
</div>

<script>
/* ══ STATE ══ */
let mode = '', gender = '', photoData = null, cur = 's0', bodyHeightCm = 175;

/* ══ SEG BAR ══ */
function setSeg(step) {
  // step 0=none, 1=first done, 2=two done, 3=all
  [0,1,2].forEach(i => {
    const el = document.getElementById('seg'+i);
    el.className = 'seg';
    if (i < step)      el.classList.add('done');
    else if (i===step) el.classList.add('active');
  });
}

/* ══ SCREEN NAV ══ */
const btnConf = {
  s0: { txt: null,                           back: null },
  s1: { txt: 'WEITER →',                     back: '← Zurück', dis: true },
  s2: { txt: 'FAHRRAD BERECHNEN →',          back: '← Zurück', dis: true },
  s3: { txt: '📸 Foto / Kamera öffnen',      back: '← Zurück' },
  s3b:{ txt: '🔍 Scan starten',              back: '← Zurück', dis: true },
  s4: { txt: null,                           back: null },
  s5: { txt: null,                           back: '↺ Neue Messung' },
};

function goScreen(sid) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.getElementById(sid).classList.add('active');
  cur = sid;
  document.getElementById('scrollBody').scrollTop = 0;

  const c = btnConf[sid] || {};
  const btn = document.getElementById('btnMain');
  const bck = document.getElementById('btnBack');

  if (!c.txt) { btn.style.display='none'; } else {
    btn.style.display='flex';
    btn.textContent = c.txt;
    btn.disabled = !!c.dis;
    btn.onclick = handleBtn;
  }
  bck.style.display = c.back ? 'block' : 'none';
  if (c.back) bck.textContent = c.back;

  const segMap = {s0:0,s1:0,s2:1,s3:1,s3b:1,s4:2,s5:3};
  setSeg(segMap[sid]||0);
}

function handleBtn() {
  if (cur==='s1') {
    if (!gender) return;
    if (mode==='manual') goScreen('s2');
    else goScreen('s3');
  } else if (cur==='s2') {
    startManual();
  } else if (cur==='s3') {
    const fi=document.getElementById('fileInput');
    if(fi){ fi.value=''; fi.click(); }
  } else if (cur==='s3b') {
    startPhotoScan();
  }
}

function handleBack() {
  const map = {s1:'s0',s2:'s1',s3:'s1',s3b:'s3',s5:'s0'};
  if (cur==='s5') { resetAll(); return; }
  goScreen(map[cur]||'s0');
}

/* ══ MODE ══ */
function selectMode(m) {
  mode = m;
  goScreen('s1');
}

/* ══ GENDER ══ */
function selGender(g, el) {
  gender = g;
  document.getElementById('gm').classList.remove('sel');
  document.getElementById('gw').classList.remove('sel');
  el.classList.add('sel');
  document.getElementById('btnMain').disabled = false;
}

/* ══ MANUAL ══ */
function checkManual() {
  const ok = document.getElementById('mL').value &&
             document.getElementById('mI').value &&
             document.getElementById('mA').value &&
             document.getElementById('mR').value;
  document.getElementById('btnMain').disabled = !ok;
}

function startManual() {
  const inputH = +document.getElementById('mL').value;
  bodyHeightCm = Math.round(inputH / 10); // sync state
  const r = {
    geschlecht: gender,
    koerper:   inputH,
    innenbein: +document.getElementById('mI').value,
    arm:       +document.getElementById('mA').value,
    rumpf:     +document.getElementById('mR').value,
  };
  r.schulter   = Math.round(r.innenbein * 0.49);
  r.mtb_zoll   = Math.round(r.innenbein * 0.226);
  r.renn_cm    = Math.round(r.innenbein * 0.665 / 10);
  r.trek_cm    = Math.round(r.innenbein * 0.66  / 10);
  r.city_cm    = Math.round(r.innenbein * 0.64  / 10);
  r.sattel     = Math.round(r.innenbein * 0.885);
  r.sitzlaenge = r.rumpf + r.arm;
  r.lenker     = Math.round(r.koerper  * 0.55);
  r.konfidenz  = 0.98;
  r.hinweis    = 'Direkt aus Messblatt Fahrer (Seite 364–365) berechnet.';

  // Show scan screen (no photo)
  document.getElementById('scanPhoto').src='';
  document.getElementById('scanBox').style.minHeight='0';
  document.querySelector('.sweep').style.display='none';
  document.querySelectorAll('.corner').forEach(c=>c.style.display='none');
  goScreen('s4');
  animateSteps([550,650,750,450]).then(()=>showResults(r));
}

/* ══ FILE INPUT ══ */
function initFileListeners(){
  const fi=document.getElementById('fileInput');
  const dz=document.getElementById('dropZone');
  if(fi) fi.addEventListener('change',function(){ if(this.files[0]) loadPhoto(this.files[0]); });
  if(dz) dz.addEventListener('click',()=>{ const fi2=document.getElementById('fileInput'); if(fi2) fi2.click(); });
}
// Call after DOM ready
if(document.readyState==='loading'){ document.addEventListener('DOMContentLoaded',initFileListeners); }
else { initFileListeners(); }

function loadPhoto(file){
  if(!file||!file.type.startsWith('image/')) return;
  const r=new FileReader();
  r.onload=e=>{
    photoData=e.target.result;
    // Update s3 preview
    const img=document.getElementById('previewImg');
    if(img){ img.src=photoData; img.style.display='block'; }
    const dp=document.getElementById('dropPH');
    if(dp) dp.style.display='none';
    // Show photo in height screen
    const hpimg=document.getElementById('heightPreviewImg');
    if(hpimg) hpimg.src=photoData;
    // Go to height input screen
    goScreen('s3b');
  };
  r.readAsDataURL(file);
}

/* ══ PHOTO SCAN ══ */
async function startPhotoScan(){
  document.getElementById('scanPhoto').src=photoData;
  document.getElementById('scanBox').style.minHeight='';
  document.querySelector('.sweep').style.display='';
  document.querySelectorAll('.corner').forEach(c=>c.style.display='');
  document.getElementById('btnMain').style.display='none';
  goScreen('s4');
  setTimeout(()=>spawnDots(bodyHeightCm),700);
  const steps=animateSteps([750,950,1100,650]);
  try{
    const result=await callClaude(photoData);
    await steps; showResults(result);
  }catch(e){ await steps; showResults(fallback()); }
}

function spawnDots(heightCm){
  heightCm = heightCm || 175;
  const ui = document.getElementById('scanUi');
  const box = document.getElementById('scanBox');
  const W = box.offsetWidth  || 320;
  const H = box.offsetHeight || 280;

  /* ── 1. GRID OVERLAY ── */
  const gridSvg = document.createElementNS('http://www.w3.org/2000/svg','svg');
  gridSvg.setAttribute('viewBox',`0 0 ${W} ${H}`);
  gridSvg.style.cssText='position:absolute;inset:0;width:100%;height:100%;pointer-events:none;';

  const COLS=6, ROWS=8;
  const cw=W/COLS, rh=H/ROWS;

  // Vertical grid lines
  for(let i=1;i<COLS;i++){
    const l=document.createElementNS('http://www.w3.org/2000/svg','line');
    l.setAttribute('x1',i*cw); l.setAttribute('y1',0);
    l.setAttribute('x2',i*cw); l.setAttribute('y2',H);
    l.setAttribute('stroke','rgba(255,255,255,0.07)');
    l.setAttribute('stroke-width','0.5');
    gridSvg.appendChild(l);
  }
  // Horizontal grid lines
  for(let j=1;j<ROWS;j++){
    const l=document.createElementNS('http://www.w3.org/2000/svg','line');
    l.setAttribute('x1',0);   l.setAttribute('y1',j*rh);
    l.setAttribute('x2',W);   l.setAttribute('y2',j*rh);
    l.setAttribute('stroke','rgba(255,255,255,0.07)');
    l.setAttribute('stroke-width','0.5');
    gridSvg.appendChild(l);
  }

  // Grid intersection dots (tiny)
  for(let i=1;i<COLS;i++){
    for(let j=1;j<ROWS;j++){
      const c=document.createElementNS('http://www.w3.org/2000/svg','circle');
      c.setAttribute('cx',i*cw); c.setAttribute('cy',j*rh); c.setAttribute('r','0.8');
      c.setAttribute('fill','rgba(255,255,255,0.12)');
      gridSvg.appendChild(c);
    }
  }

  // Outer measurement rectangle (elegant border inside corners)
  const pad=12;
  const rect=document.createElementNS('http://www.w3.org/2000/svg','rect');
  rect.setAttribute('x',pad); rect.setAttribute('y',pad);
  rect.setAttribute('width',W-pad*2); rect.setAttribute('height',H-pad*2);
  rect.setAttribute('fill','none');
  rect.setAttribute('stroke','rgba(255,255,255,0.15)');
  rect.setAttribute('stroke-width','0.6');
  rect.setAttribute('rx','2');
  gridSvg.appendChild(rect);

  // Center vertical dashed line (measurement reference - red like Smartfit)
  const cLine=document.createElementNS('http://www.w3.org/2000/svg','line');
  cLine.setAttribute('x1',W/2); cLine.setAttribute('y1',pad);
  cLine.setAttribute('x2',W/2); cLine.setAttribute('y2',H-pad);
  cLine.setAttribute('stroke','rgba(220,60,60,0.7)');
  cLine.setAttribute('stroke-width','0.7');
  cLine.setAttribute('stroke-dasharray','3,3');
  gridSvg.appendChild(cLine);

  gridSvg.style.opacity='0';
  gridSvg.style.transition='opacity 0.6s ease';
  ui.appendChild(gridSvg);
  setTimeout(()=>{ gridSvg.style.opacity='1'; }, 150);

  /* ── 2. SKELETON OVERLAY ── */
  const pts = {
    head:  {x:50, y:8,  lb:'Kopf'},
    neck:  {x:50, y:15, lb:''},
    lSho:  {x:39, y:19, lb:'Schulter L'},
    rSho:  {x:61, y:19, lb:'Schulter R'},
    lElb:  {x:36, y:33, lb:''},
    rElb:  {x:64, y:33, lb:''},
    lWri:  {x:35, y:46, lb:''},
    rWri:  {x:65, y:46, lb:''},
    lHip:  {x:43, y:48, lb:''},
    rHip:  {x:57, y:48, lb:'Hüfte'},
    lKne:  {x:43, y:64, lb:'Knie L'},
    rKne:  {x:57, y:64, lb:'Knie R'},
    lAnk:  {x:43, y:79, lb:''},
    rAnk:  {x:57, y:79, lb:'Sprunggelenk'},
    lFoot: {x:43, y:88, lb:''},
    rFoot: {x:57, y:88, lb:'Fuß'},
  };

  const bones = [
    ['neck','lSho'],['neck','rSho'],
    ['lSho','rSho'],
    ['lSho','lElb'],['lElb','lWri'],
    ['rSho','rElb'],['rElb','rWri'],
    ['lSho','lHip'],['rSho','rHip'],
    ['lHip','rHip'],
    ['lHip','lKne'],['rHip','rKne'],
    ['lKne','rKne'],
    ['lKne','lAnk'],['rKne','rAnk'],
    ['lAnk','rAnk'],
    ['lAnk','lFoot'],['rAnk','rFoot'],
  ];

  const skelSvg = document.createElementNS('http://www.w3.org/2000/svg','svg');
  skelSvg.setAttribute('viewBox','0 0 100 100');
  skelSvg.setAttribute('preserveAspectRatio','none');
  skelSvg.style.cssText='position:absolute;inset:0;width:100%;height:100%;pointer-events:none;';

  // Measurement lines (horizontal dashed - body width markers)
  const measLines=[
    {y:19, label:'Schulterbreite', color:'rgba(255,255,255,0.25)'},
    {y:48, label:'Hüftbreite',     color:'rgba(255,255,255,0.20)'},
    {y:64, label:'Kniebreite',     color:'rgba(255,255,255,0.15)'},
  ];
  measLines.forEach(m=>{
    const l=document.createElementNS('http://www.w3.org/2000/svg','line');
    l.setAttribute('x1','5'); l.setAttribute('y1',m.y);
    l.setAttribute('x2','95'); l.setAttribute('y2',m.y);
    l.setAttribute('stroke',m.color); l.setAttribute('stroke-width','0.3');
    l.setAttribute('stroke-dasharray','1,2');
    skelSvg.appendChild(l);
  });

  // Bones
  bones.forEach(([a,b],i)=>{
    const pa=pts[a], pb=pts[b];
    const line=document.createElementNS('http://www.w3.org/2000/svg','line');
    line.setAttribute('x1',pa.x); line.setAttribute('y1',pa.y);
    line.setAttribute('x2',pb.x); line.setAttribute('y2',pb.y);
    line.setAttribute('stroke','rgba(230,245,230,0.80)');
    line.setAttribute('stroke-width','0.55');
    line.setAttribute('stroke-linecap','round');
    line.style.opacity='0';
    skelSvg.appendChild(line);
    setTimeout(()=>{ line.style.transition='opacity 0.3s'; line.style.opacity='1'; }, 400+i*45);
  });

  // Dots + labels
  Object.entries(pts).forEach(([key,p],i)=>{
    // Glow
    const glow=document.createElementNS('http://www.w3.org/2000/svg','circle');
    glow.setAttribute('cx',p.x); glow.setAttribute('cy',p.y); glow.setAttribute('r','2.0');
    glow.setAttribute('fill','rgba(255,255,255,0.08)');
    glow.style.opacity='0';
    skelSvg.appendChild(glow);

    // Main dot — white/light gray
    const dot=document.createElementNS('http://www.w3.org/2000/svg','circle');
    dot.setAttribute('cx',p.x); dot.setAttribute('cy',p.y); dot.setAttribute('r','1.1');
    dot.setAttribute('fill','rgba(240,248,240,0.95)');
    dot.setAttribute('stroke','rgba(255,255,255,0.4)');
    dot.setAttribute('stroke-width','0.3');
    dot.style.opacity='0';
    skelSvg.appendChild(dot);

    // Label — elegant small white text
    if(p.lb && ['head','lSho','rSho','rHip','lKne','rKne','rAnk','rFoot'].includes(key)){
      const txt=document.createElementNS('http://www.w3.org/2000/svg','text');
      const right=p.x>=50;
      txt.setAttribute('x', right ? p.x+2.5 : p.x-2.5);
      txt.setAttribute('y', p.y+1.0);
      txt.setAttribute('font-size','2.5');
      txt.setAttribute('fill','rgba(255,255,255,0.90)');
      txt.setAttribute('font-family','system-ui,sans-serif');
      txt.setAttribute('font-weight','600');
      txt.setAttribute('letter-spacing','0.1');
      txt.setAttribute('text-anchor', right ? 'start' : 'end');
      txt.style.opacity='0';
      txt.textContent=p.lb;
      skelSvg.appendChild(txt);
      setTimeout(()=>{ txt.style.transition='opacity 0.4s'; txt.style.opacity='1'; }, 650+i*40);
    }

    setTimeout(()=>{
      glow.style.transition='opacity 0.3s'; dot.style.transition='opacity 0.3s';
      glow.style.opacity='1'; dot.style.opacity='1';
    }, 280+i*65);
  });

  ui.appendChild(skelSvg);
}

async function animateSteps(durs){
  for(let i=0;i<4;i++){
    document.getElementById('ss'+i).classList.add('active');
    fillBar('sf'+i,durs[i]);
    await sleep(durs[i]+180);
    document.getElementById('ss'+i).classList.remove('active');
    document.getElementById('ss'+i).classList.add('done');
  }
}

async function callClaude(base64){
  const b64=base64.split(',')[1];
  const mime=(base64.match(/data:(image\/[^;]+);/)||[])[1]||'image/jpeg';

  // Build prompt with exact height values
  const hCm  = bodyHeightCm;          // e.g. 167
  const hMm  = hCm * 10;             // e.g. 1670
  // Proportional estimates based on height
  const ibMm = Math.round(hMm * 0.475);  // Innenbein ~47.5%
  const aMm  = Math.round(hMm * 0.365);  // Arm ~36.5%
  const rMm  = Math.round(hMm * 0.32);   // Rumpf ~32%
  const sMm  = Math.round(hMm * 0.235);  // Schulter ~23.5%

  const promptText = 'Du bist Fahrrad-Ergonomie-Experte. Analysiere dieses Foto einer Person.'
    + ' Die exakte Körpergröße ist ' + hCm + ' cm (' + hMm + ' mm) — nutze diesen Wert EXAKT als "koerper".'
    + ' Schätze die anderen Maße anhand des Fotos (Proportionen, Körperbau).'
    + ' Startschätzungen (kannst du anpassen): innenbein=' + ibMm + ', arm=' + aMm + ', rumpf=' + rMm + ', schulter=' + sMm + '.'
    + ' Antworte NUR mit JSON ohne Backticks oder Markdown:'
    + ' {"geschlecht":"männlich oder weiblich"'
    + ',"koerper":' + hMm
    + ',"innenbein":Zahl,"arm":Zahl,"rumpf":Zahl,"schulter":Zahl'
    + ',"mtb_zoll":Zahl,"renn_cm":Zahl,"trek_cm":Zahl,"city_cm":Zahl'
    + ',"sattel":Zahl,"sitzlaenge":Zahl,"lenker":Zahl'
    + ',"konfidenz":0.93,"hinweis":"kurzer Hinweis auf Deutsch"}';

  const res=await fetch('https://api.anthropic.com/v1/messages',{
    method:'POST', headers:{'Content-Type':'application/json'},
    body:JSON.stringify({
      model:'claude-sonnet-4-20250514', max_tokens:1000,
      messages:[{role:'user',content:[
        {type:'image',source:{type:'base64',media_type:mime,data:b64}},
        {type:'text',text:promptText}
      ]}]
    })
  });
  const data=await res.json();
  const raw=data.content.map(c=>c.text||'').join('').replace(/```json|```/g,'').trim();
  const result=JSON.parse(raw);
  // Always enforce exact height
  result.koerper = hMm;
  return result;
}

function fallback(){
  const hMm = bodyHeightCm * 10;
  const ib  = Math.round(hMm * 0.475);
  const arm = Math.round(hMm * 0.365);
  const rum = Math.round(hMm * 0.320);
  const sch = Math.round(hMm * 0.235);
  return{
    geschlecht: gender || 'männlich',
    koerper:    hMm,
    innenbein:  ib,
    arm:        arm,
    rumpf:      rum,
    schulter:   sch,
    mtb_zoll:   Math.round(ib * 0.226),
    renn_cm:    Math.round(ib * 0.665 / 10),
    trek_cm:    Math.round(ib * 0.660 / 10),
    city_cm:    Math.round(ib * 0.640 / 10),
    sattel:     Math.round(ib * 0.885),
    sitzlaenge: rum + arm,
    lenker:     Math.round(hMm * 0.55),
    konfidenz:  0.88,
    hinweis:    'Proportionale Schätzung basierend auf eingegebener Körpergröße (' + bodyHeightCm + ' cm).'
  };
}

/* ══ SHOW RESULTS ══ */
function showResults(r){
  // Show kunde photo in results if available
  const kpw = document.getElementById('kundePhotoWrap');
  const kph = document.getElementById('kundePhoto');
  if(photoData && kpw && kph){ kph.src=photoData; kpw.style.display='block'; }
  else if(kpw){ kpw.style.display='none'; }

  document.getElementById('resAv').textContent    = r.geschlecht==='weiblich'?'👩':'👨';
  document.getElementById('resTitle').textContent = r.geschlecht==='weiblich'?'♀ Kundin':'♂ Kunde';
  document.getElementById('resSub').textContent   = `${r.koerper} mm · Innenbein ${r.innenbein} mm`;
  document.getElementById('konfB').textContent    = Math.round(r.konfidenz*100)+'%';

  const meas=[
    {c:'L',name:'Körperlänge',val:r.koerper},
    {c:'I',name:'Innenbein',  val:r.innenbein},
    {c:'A',name:'Armlänge',   val:r.arm},
    {c:'R',name:'Rumpflänge', val:r.rumpf},
    {c:'S',name:'Schulter',   val:r.schulter},
  ];
  document.getElementById('measRow').innerHTML=meas.map(m=>`
    <div class="mchip">
      <span class="mc-badge ${m.c}">${m.c}</span>
      <span class="mc-val">${m.val}</span>
      <span class="mc-name">${m.name}<br>mm</span>
    </div>`).join('');

  const reach=r.arm+r.rumpf, ratio=r.innenbein/r.koerper;
  const bikes=[
    {type:'trek',em:'🛤️',name:'Trekking Rad', frame:r.trek_cm+' cm',
     score:Math.min(77+(reach>=1100&&reach<=1280?10:0)+5,99)},
    {type:'mtb', em:'🏔️',name:'Mountain Bike',frame:r.mtb_zoll+'"',
     score:Math.min(75+(ratio>.47&&ratio<.52?10:0)+(reach>1150&&reach<1350?8:0),99)},
    {type:'renn',em:'🏁',name:'Rennrad',       frame:r.renn_cm+' cm',
     score:Math.min(68+(reach>1200?12:0)+(ratio>.49?8:0),99)},
    {type:'city',em:'🏙️',name:'City Bike',     frame:r.city_cm+' cm',
     score:Math.min(65+(reach<1180?10:0),99)},
  ].sort((a,b)=>b.score-a.score);

  document.getElementById('bikeCol').innerHTML=bikes.map((b,i)=>`
    <div class="bcard ${b.type}${i===0?' best':''}">
      ${i===0?'<div class="best-tag">⭐ EMPFOHLEN</div>':''}
      <div class="bcard-em">${b.em}</div>
      <div class="bcard-info">
        <div class="bcard-name">${b.name}</div>
        <span class="bcard-frame ${b.type}">${b.frame}</span>
        <div class="bcard-bar"><div class="bcard-fill ${b.type}" data-w="${b.score}"></div></div>
      </div>
      <div class="bcard-pct ${b.type}">${b.score}%</div>
    </div>`).join('');

  document.getElementById('sitzBlock').innerHTML=[
    {n:1,name:'Sitzhöhe (SaH)',val:r.sattel,unit:'mm'},
    {n:2,name:'Sitzlänge',     val:r.sitzlaenge,unit:'mm'},
    {n:3,name:'Lenkerhöhe (LH)',val:Math.round(r.lenker),unit:'mm'},
    {n:4,name:'Sattelposition', val:22,unit:'cm'},
  ].map(s=>`
    <div class="sitz-row">
      <div class="sitz-num">${s.n}</div>
      <div class="sitz-name">${s.name}</div>
      <span class="sitz-val">${s.val}</span>
      <span class="sitz-unit">${s.unit}</span>
    </div>`).join('');

  if(r.hinweis){
    document.getElementById('hintResWrap').innerHTML=
      `<div class="hint-res">ℹ️ <strong>Hinweis:</strong> ${r.hinweis}</div>`;
  }

  goScreen('s5');
  setTimeout(()=>{
    document.querySelectorAll('.bcard-fill').forEach(el=>el.style.width=el.dataset.w+'%');
  },350);
}

/* ══ RESET ══ */
function checkHeightInput(){
  const val = parseInt(document.getElementById('heightInput').value);
  const btn = document.getElementById('btnMain');
  const field = document.getElementById('heightInputField');
  if(val >= 140 && val <= 220){
    bodyHeightCm = val;
    if(btn){ btn.disabled = false; }
    if(field) field.style.borderColor = '#2db84f';
    // Highlight matching preset
    document.querySelectorAll('.h-preset').forEach(el=>{
      el.style.borderColor = parseInt(el.textContent)===val ? '#f4ff00' : '#272e42';
      el.style.color       = parseInt(el.textContent)===val ? '#f4ff00' : '#8892a4';
    });
  } else {
    if(btn){ btn.disabled = true; }
    if(field) field.style.borderColor = '#272e42';
  }
}

function setHeight(h){
  bodyHeightCm = h;
  const inp = document.getElementById('heightInput');
  if(inp){ inp.value = h; }
  checkHeightInput();
}

function resetAll(){
  mode=''; gender=''; photoData=null;
  document.getElementById('fileInput').value='';
  bodyHeightCm = 175;
  const hi=document.getElementById('heightInput'); if(hi) hi.value='';
  const hf=document.getElementById('heightInputField'); if(hf) hf.style.borderColor='#272e42';
  document.querySelectorAll('.h-preset').forEach(el=>{ el.style.borderColor='#272e42'; el.style.color='#8892a4'; });
  document.getElementById('previewImg').style.display='none';
  document.getElementById('previewImg').src='';
  document.getElementById('dropPH').style.display='block';
  document.getElementById('gm').classList.remove('sel');
  document.getElementById('gw').classList.remove('sel');
  ['mL','mI','mA','mR'].forEach(id=>document.getElementById(id).value='');
  document.querySelectorAll('.ss').forEach(el=>el.className='ss');
  document.querySelectorAll('.ss-fill').forEach(el=>el.style.width='0%');
  document.querySelectorAll('.ldot').forEach(el=>el.remove());
  document.getElementById('hintResWrap').innerHTML='';
  const kpw2=document.getElementById('kundePhotoWrap'); if(kpw2) kpw2.style.display='none';
  const kph2=document.getElementById('kundePhoto'); if(kph2) kph2.src='';
  document.getElementById('btnMain').onclick=handleBtn;
  goScreen('s0');
}

function fillBar(id,dur){ const el=document.getElementById(id); if(!el)return; el.style.transition=`width ${dur}ms ease`; setTimeout(()=>el.style.width='100%',30); }
function sleep(ms){ return new Promise(r=>setTimeout(r,ms)); }
</script>

</body>
</html>