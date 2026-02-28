<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>omjha-git — GitHub</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;500;600;700&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
* { margin: 0; padding: 0; box-sizing: border-box; }
:root {
  --bg: #0d1117; --bg2: #161b22; --bg3: #1c2128; --bg4: #21262d;
  --border: #30363d; --border2: #21262d;
  --text: #e6edf3; --text2: #8b949e; --text3: #6e7681;
  --accent: #58a6ff; --green: #3fb950; --purple: #bc8cff;
  --orange: #ffa657; --yellow: #f0c27f; --red: #f85149;
  --glow: rgba(88,166,255,0.15);
}
body { background:var(--bg); color:var(--text); font-family:'JetBrains Mono',monospace; min-height:100vh; cursor:none; overflow-x:hidden; }

/* ROBOT CURSOR */
#robot-cursor { position:fixed; pointer-events:none; z-index:99999; top:0; left:0; transform:translate(-50%,-50%); }
.robot-body { width:42px; height:48px; position:relative; filter:drop-shadow(0 0 10px rgba(88,166,255,0.9)); animation:robotBob 1.4s ease-in-out infinite; }
@keyframes robotBob { 0%,100%{transform:translateY(0) rotate(-2deg)} 50%{transform:translateY(-5px) rotate(2deg)} }
.r-head { width:30px; height:24px; background:linear-gradient(135deg,#1e3a5f,#2d5a9e); border:2px solid var(--accent); border-radius:6px 6px 4px 4px; position:absolute; top:0; left:6px; box-shadow:0 0 12px rgba(88,166,255,0.5); }
.r-antenna { width:3px; height:9px; background:var(--accent); position:absolute; top:-9px; left:50%; transform:translateX(-50%); border-radius:2px; }
.r-antenna::after { content:''; width:7px; height:7px; background:var(--accent); border-radius:50%; position:absolute; top:-6px; left:-2px; box-shadow:0 0 10px var(--accent); animation:antPulse 1s ease-in-out infinite; }
@keyframes antPulse { 0%,100%{opacity:1;transform:scale(1)} 50%{opacity:0.3;transform:scale(0.6)} }
.r-eye { width:7px; height:7px; background:var(--accent); border-radius:50%; position:absolute; top:7px; box-shadow:0 0 8px var(--accent); animation:blink 3.5s ease-in-out infinite; }
.r-eye.l{left:5px} .r-eye.r{right:5px}
@keyframes blink { 0%,88%,100%{transform:scaleY(1)} 93%{transform:scaleY(0.1)} }
.r-mouth { width:16px; height:5px; background:var(--bg); border:1.5px solid var(--accent); border-radius:3px; position:absolute; bottom:3px; left:50%; transform:translateX(-50%); }
.r-mouth.talk { animation:talk 0.25s ease-in-out infinite alternate; }
@keyframes talk { 0%{height:2px} 100%{height:7px} }
.r-torso { width:34px; height:22px; background:linear-gradient(135deg,#1a2f4a,#1e3a5f); border:2px solid #2d5a9e; border-radius:3px; position:absolute; top:24px; left:4px; display:flex; align-items:center; justify-content:center; }
.r-light { width:9px; height:9px; background:var(--green); border-radius:50%; box-shadow:0 0 10px var(--green); animation:lightPulse 1.8s ease-in-out infinite; }
@keyframes lightPulse { 0%,100%{opacity:1} 50%{opacity:0.2} }
.r-leg { width:11px; height:12px; background:linear-gradient(135deg,#1e3a5f,#2d5a9e); border:1.5px solid #2d5a9e; border-radius:2px; position:absolute; top:46px; }
.r-leg.l{left:7px; animation:legL 1.4s ease-in-out infinite;}
.r-leg.r{right:7px; animation:legR 1.4s ease-in-out infinite;}
@keyframes legL { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-3px)} }
@keyframes legR { 0%,100%{transform:translateY(-3px)} 50%{transform:translateY(0)} }
.trail { position:fixed; pointer-events:none; z-index:99998; width:5px; height:5px; background:var(--accent); border-radius:50%; transform:translate(-50%,-50%); animation:trailFade 0.6s forwards; }
@keyframes trailFade { 0%{opacity:0.7;transform:translate(-50%,-50%) scale(1)} 100%{opacity:0;transform:translate(-50%,-50%) scale(0)} }

/* SCANLINES */
body::after { content:''; position:fixed; inset:0; background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,0.025) 2px,rgba(0,0,0,0.025) 4px); pointer-events:none; z-index:99990; }

/* GLOW ORBS */
.orb { position:fixed; border-radius:50%; filter:blur(90px); pointer-events:none; z-index:0; animation:orbDrift 10s ease-in-out infinite; }
.orb1 { width:500px; height:500px; background:rgba(88,166,255,0.05); top:-150px; right:-150px; }
.orb2 { width:400px; height:400px; background:rgba(63,185,80,0.04); bottom:100px; left:-100px; animation-delay:-4s; }
.orb3 { width:350px; height:350px; background:rgba(188,140,255,0.035); bottom:-80px; right:20%; animation-delay:-7s; }
@keyframes orbDrift { 0%,100%{transform:translate(0,0)} 33%{transform:translate(40px,-40px)} 66%{transform:translate(-25px,25px)} }

/* NAV */
nav { background:rgba(22,27,34,0.95); border-bottom:1px solid var(--border); height:64px; display:flex; align-items:center; padding:0 24px; gap:16px; position:sticky; top:0; z-index:1000; backdrop-filter:blur(20px); }
.nav-logo svg { fill:var(--text); width:34px; height:34px; }
.nav-search { flex:1; max-width:300px; background:var(--bg); border:1px solid var(--border); border-radius:8px; display:flex; align-items:center; padding:7px 12px; gap:8px; color:var(--text3); font-size:13px; transition:all 0.2s; }
.nav-search:hover,.nav-search:focus-within { border-color:var(--accent); box-shadow:0 0 0 3px var(--glow); }
.nav-search input { background:none; border:none; outline:none; color:var(--text2); font-family:'JetBrains Mono',monospace; font-size:13px; width:100%; }
.kbd { background:var(--bg3); border:1px solid var(--border); border-radius:4px; padding:1px 6px; font-size:11px; color:var(--text3); }
.nav-right { display:flex; gap:6px; margin-left:auto; align-items:center; }
.nbtn { background:none; border:1px solid transparent; color:var(--text2); padding:6px 12px; border-radius:6px; font-family:'JetBrains Mono',monospace; font-size:13px; cursor:none; transition:all 0.2s; display:flex; align-items:center; gap:6px; }
.nbtn:hover { border-color:var(--border); background:var(--bg3); color:var(--text); }
.nbtn svg { width:15px; height:15px; fill:currentColor; }
.nav-av { width:32px; height:32px; border-radius:50%; background:linear-gradient(135deg,#1e3a5f,#4a7fb5); border:2px solid var(--accent); display:flex; align-items:center; justify-content:center; font-size:12px; font-weight:700; color:var(--accent); cursor:none; box-shadow:0 0 12px var(--glow); }

/* PROFILE TABS */
.ptabs { background:rgba(22,27,34,0.9); border-bottom:1px solid var(--border); padding:0 24px; display:flex; align-items:center; backdrop-filter:blur(12px); }
.ptab { padding:14px 16px; color:var(--text2); font-size:13px; border-bottom:2px solid transparent; cursor:none; display:flex; align-items:center; gap:8px; transition:all 0.2s; text-decoration:none; }
.ptab:hover { color:var(--text); }
.ptab.active { color:var(--text); border-bottom-color:var(--orange); }
.ptab svg { width:14px; height:14px; fill:currentColor; }
.tab-ct { background:var(--bg4); border:1px solid var(--border); border-radius:20px; padding:1px 8px; font-size:11px; color:var(--text2); }

/* LAYOUT */
.main { max-width:1280px; margin:0 auto; padding:28px 24px; display:grid; grid-template-columns:300px 1fr; gap:28px; position:relative; z-index:1; }

/* SIDEBAR */
.sidebar { display:flex; flex-direction:column; gap:22px; }
.av-wrap { position:relative; border-radius:50%; overflow:hidden; border:3px solid var(--border); box-shadow:0 0 35px rgba(88,166,255,0.12); transition:box-shadow 0.3s; aspect-ratio:1; }
.av-wrap:hover { box-shadow:0 0 50px rgba(88,166,255,0.3); }
.av-svg { width:100%; height:100%; display:block; }
.av-status { position:absolute; bottom:10px; right:10px; width:26px; height:26px; background:var(--bg); border-radius:50%; display:flex; align-items:center; justify-content:center; border:2px solid var(--bg); }
.sdot { width:17px; height:17px; background:var(--green); border-radius:50%; box-shadow:0 0 10px var(--green); animation:sPulse 2s ease-in-out infinite; }
@keyframes sPulse { 0%,100%{box-shadow:0 0 4px var(--green)} 50%{box-shadow:0 0 16px var(--green)} }
.pname { font-family:'Syne',sans-serif; font-size:23px; font-weight:800; color:var(--text); letter-spacing:-0.5px; }
.phandle { font-size:16px; color:var(--text2); font-weight:300; margin-top:3px; }
.pbio { font-size:13px; color:var(--text2); line-height:1.65; padding:12px 14px; background:var(--bg3); border-radius:8px; border-left:3px solid var(--accent); }
.ebtn { width:100%; padding:9px; background:var(--bg3); border:1px solid var(--border); border-radius:6px; color:var(--text); font-family:'JetBrains Mono',monospace; font-size:13px; cursor:none; transition:all 0.2s; display:flex; align-items:center; justify-content:center; gap:8px; }
.ebtn:hover { background:var(--bg4); border-color:var(--accent); box-shadow:0 0 12px var(--glow); }
.ebtn svg { width:14px; height:14px; fill:currentColor; }
.fstats { display:flex; gap:16px; font-size:13px; color:var(--text2); align-items:center; }
.fstats svg { width:14px; height:14px; fill:var(--text3); }
.fstats a { color:var(--text); text-decoration:none; font-weight:600; }
.fstats a:hover { color:var(--accent); }
.slabel { font-size:11px; font-weight:600; color:var(--text2); text-transform:uppercase; letter-spacing:0.8px; margin-bottom:10px; display:flex; align-items:center; gap:8px; }
.slabel::after { content:''; flex:1; height:1px; background:var(--border); }
.slinks { display:flex; flex-direction:column; gap:6px; }
.slink { display:flex; align-items:center; gap:10px; color:var(--text2); text-decoration:none; font-size:13px; padding:7px 9px; border-radius:6px; transition:all 0.2s; }
.slink:hover { color:var(--accent); background:var(--bg3); }
.slink svg { width:14px; height:14px; fill:currentColor; flex-shrink:0; }
.tstack { display:flex; flex-wrap:wrap; gap:6px; }
.tb { font-size:11px; padding:3px 8px; border-radius:20px; border:1px solid; font-family:'JetBrains Mono',monospace; letter-spacing:0.3px; transition:all 0.2s; cursor:none; }
.tb:hover { transform:translateY(-2px); box-shadow:0 4px 14px rgba(0,0,0,0.3); }
.js{color:#f0c27f;border-color:#f0c27f33;background:#f0c27f10} .nd{color:#3fb950;border-color:#3fb95033;background:#3fb95010}
.re{color:#58a6ff;border-color:#58a6ff33;background:#58a6ff10} .mg{color:#4ea94b;border-color:#4ea94b33;background:#4ea94b10}
.ht{color:#ffa657;border-color:#ffa65733;background:#ffa65710} .cs{color:#bc8cff;border-color:#bc8cff33;background:#bc8cff10}
.dk{color:#0db7ed;border-color:#0db7ed33;background:#0db7ed10} .cp{color:#7cb9e8;border-color:#7cb9e833;background:#7cb9e810}
.jv{color:#ED8B00;border-color:#ED8B0033;background:#ED8B0010} .nx{color:#e6edf3;border-color:#30363d;background:#161b22}
.ex{color:#61DAFB;border-color:#61DAFB33;background:#61DAFB10} .py{color:#FFE873;border-color:#FFE87333;background:#FFE87310}

/* CONTENT */
.content { display:flex; flex-direction:column; gap:20px; }
.toolbar { display:flex; gap:10px; align-items:center; }
.rsearch { flex:1; background:var(--bg2); border:1px solid var(--border); border-radius:6px; padding:9px 14px; color:var(--text); font-family:'JetBrains Mono',monospace; font-size:13px; outline:none; transition:all 0.2s; }
.rsearch:focus { border-color:var(--accent); box-shadow:0 0 0 3px var(--glow); }
.rsearch::placeholder { color:var(--text3); }
.tbtn { background:var(--bg2); border:1px solid var(--border); border-radius:6px; padding:9px 14px; color:var(--text2); font-family:'JetBrains Mono',monospace; font-size:13px; cursor:none; transition:all 0.2s; display:flex; align-items:center; gap:6px; white-space:nowrap; }
.tbtn:hover { border-color:var(--accent); color:var(--text); background:var(--bg3); }
.tbtn svg { width:12px; height:12px; fill:currentColor; }
.newbtn { background:#238636; border-color:rgba(240,246,252,0.1); color:#fff; }
.newbtn:hover { background:#2ea043; }

/* REPO GRID */
.rgrid { border:1px solid var(--border); border-radius:10px; overflow:hidden; background:var(--bg2); }
.rcard { padding:20px 24px; border-bottom:1px solid var(--border2); position:relative; transition:background 0.2s; display:grid; grid-template-columns:1fr auto; gap:12px; align-items:start; }
.rcard:last-child { border-bottom:none; }
.rcard:hover { background:var(--bg3); }
.rcard::before { content:''; position:absolute; left:0; top:0; bottom:0; width:3px; background:transparent; transition:background 0.2s; border-radius:0; }
.rcard:hover::before { background:var(--accent); }
.rnamerow { display:flex; align-items:center; gap:10px; margin-bottom:7px; flex-wrap:wrap; }
.rname { color:var(--accent); font-size:15px; font-weight:600; font-family:'Syne',sans-serif; text-decoration:none; transition:color 0.2s; }
.rname:hover { color:#79b8ff; text-decoration:underline; }
.rbadge { font-size:11px; padding:2px 8px; border-radius:20px; border:1px solid var(--border); color:var(--text3); }
.rdesc { font-size:13px; color:var(--text2); margin-bottom:10px; line-height:1.55; }
.rmeta { display:flex; align-items:center; gap:16px; flex-wrap:wrap; }
.rlang { display:flex; align-items:center; gap:6px; font-size:12px; color:var(--text2); }
.ldot { width:11px; height:11px; border-radius:50%; flex-shrink:0; }
.ljs{background:#f1e05a;box-shadow:0 0 5px #f1e05a66} .lhtml{background:#e34c26;box-shadow:0 0 5px #e34c2666} .lcss{background:#563d7c;box-shadow:0 0 5px #563d7c66}
.rtime { font-size:12px; color:var(--text3); }
.sbtn { display:flex; align-items:center; gap:6px; background:var(--bg3); border:1px solid var(--border); border-radius:6px; padding:6px 12px; color:var(--text2); font-family:'JetBrains Mono',monospace; font-size:12px; cursor:none; transition:all 0.2s; white-space:nowrap; align-self:start; }
.sbtn:hover { background:var(--bg4); border-color:var(--yellow); color:var(--yellow); box-shadow:0 0 12px rgba(240,194,127,0.2); }
.sbtn svg { width:14px; height:14px; fill:currentColor; transition:transform 0.2s; }
.sbtn:hover svg { transform:scale(1.2) rotate(15deg); }
.sbtn.starred { background:rgba(240,194,127,0.12); border-color:var(--yellow); color:var(--yellow); }
.sbtn.starred svg { fill:var(--yellow); }

/* CONTRIB GRAPH */
.cgraph-wrap { background:var(--bg2); border:1px solid var(--border); border-radius:10px; padding:22px; }
.cg-title { font-size:13px; color:var(--text2); margin-bottom:16px; font-family:'Syne',sans-serif; font-weight:600; }
.cgraph { display:flex; gap:3px; overflow-x:auto; padding-bottom:4px; }
.cweek { display:flex; flex-direction:column; gap:3px; }
.cday { width:12px; height:12px; border-radius:2px; background:var(--bg4); cursor:none; transition:transform 0.1s; }
.cday:hover { transform:scale(1.4); }
.cday.l1{background:#0e4429} .cday.l2{background:#006d32} .cday.l3{background:#26a641} .cday.l4{background:#39d353}
.cg-legend { display:flex; align-items:center; gap:6px; margin-top:12px; font-size:11px; color:var(--text3); justify-content:flex-end; }
.cg-legend div { width:11px; height:11px; border-radius:2px; }

/* STATS */
.sgrid { display:grid; grid-template-columns:repeat(3,1fr); gap:14px; }
.scard { background:var(--bg2); border:1px solid var(--border); border-radius:10px; padding:16px; overflow:hidden; transition:all 0.3s; position:relative; }
.scard::before { content:''; position:absolute; inset:0; background:linear-gradient(135deg,transparent,rgba(88,166,255,0.03)); opacity:0; transition:opacity 0.3s; }
.scard:hover { border-color:var(--accent); box-shadow:0 0 24px var(--glow); transform:translateY(-2px); }
.scard:hover::before { opacity:1; }
.scard img { width:100%; border-radius:6px; display:block; }

/* PINNED */
.pgrid { display:grid; grid-template-columns:repeat(2,1fr); gap:14px; }
.pcard { background:var(--bg2); border:1px solid var(--border); border-radius:10px; padding:18px; transition:all 0.3s; position:relative; overflow:hidden; }
.pcard::after { content:''; position:absolute; top:0; left:0; right:0; height:2px; background:linear-gradient(90deg,var(--accent),var(--purple)); opacity:0; transition:opacity 0.3s; }
.pcard:hover { border-color:var(--accent); box-shadow:0 8px 32px rgba(0,0,0,0.35); transform:translateY(-2px); }
.pcard:hover::after { opacity:1; }
.plabel { font-size:11px; color:var(--text3); display:flex; align-items:center; gap:5px; margin-bottom:8px; }
.plabel svg { width:12px; height:12px; fill:currentColor; }
.pn { color:var(--accent); font-size:15px; font-weight:700; font-family:'Syne',sans-serif; margin-bottom:6px; }
.pd { font-size:12px; color:var(--text2); margin-bottom:10px; line-height:1.5; }

/* QUOTE */
.qcard { background:var(--bg2); border:1px solid var(--border); border-radius:10px; overflow:hidden; }
.qcard img { width:100%; display:block; }

/* FADE ANIM */
.fu { opacity:0; transform:translateY(18px); transition:opacity 0.5s, transform 0.5s; }
.fu.vis { opacity:1; transform:translateY(0); }

/* FOOTER */
footer { background:var(--bg2); border-top:1px solid var(--border); padding:36px 24px; text-align:center; color:var(--text3); font-size:12px; line-height:2.2; margin-top:40px; }
footer a { color:var(--accent); text-decoration:none; }
footer a:hover { text-decoration:underline; }
</style>
</head>
<body>

<div class="orb orb1"></div>
<div class="orb orb2"></div>
<div class="orb orb3"></div>

<!-- ROBOT CURSOR -->
<div id="robot-cursor">
  <div class="robot-body">
    <div class="r-head">
      <div class="r-antenna"></div>
      <div class="r-eye l"></div>
      <div class="r-eye r"></div>
      <div class="r-mouth" id="rmount"></div>
    </div>
    <div class="r-torso"><div class="r-light"></div></div>
    <div class="r-leg l"></div>
    <div class="r-leg r"></div>
  </div>
</div>

<!-- NAV -->
<nav>
  <svg height="34" viewBox="0 0 16 16" width="34" fill="var(--text)"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg>
  <div class="nav-search">
    <svg width="14" height="14" fill="currentColor" viewBox="0 0 16 16"><path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.099zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/></svg>
    <input type="text" placeholder="Type / to search">
    <span class="kbd">/</span>
  </div>
  <div class="nav-right">
    <button class="nbtn">
      <svg viewBox="0 0 16 16"><path d="M8 9.5a1.5 1.5 0 1 0 0-3 1.5 1.5 0 0 0 0 3z"/><path fill-rule="evenodd" d="M8 0a8 8 0 1 1 0 16A8 8 0 0 1 8 0zM1.5 8a6.5 6.5 0 1 0 13 0 6.5 6.5 0 0 0-13 0z"/></svg>
      Pull requests
    </button>
    <button class="nbtn">
      <svg viewBox="0 0 16 16"><path d="M8 1.5a6.5 6.5 0 1 0 0 13 6.5 6.5 0 0 0 0-13zM0 8a8 8 0 1 1 16 0A8 8 0 0 1 0 8zm9 3a1 1 0 1 1-2 0 1 1 0 0 1 2 0zm-.25-6.25a.75.75 0 0 0-1.5 0v3.5a.75.75 0 0 0 1.5 0v-3.5z"/></svg>
      Issues
    </button>
    <div class="nav-av">OJ</div>
  </div>
</nav>

<!-- TABS -->
<div class="ptabs">
  <a href="#" class="ptab"><svg viewBox="0 0 16 16"><path d="M2 2.5A2.5 2.5 0 0 1 4.5 0h8.75a.75.75 0 0 1 .75.75v12.5a.75.75 0 0 1-.75.75h-2.5a.75.75 0 0 1 0-1.5h1.75v-2h-8a1 1 0 0 0-.714 1.7.75.75 0 1 1-1.072 1.05A2.495 2.495 0 0 1 2 11.5Zm10.5-1h-8a1 1 0 0 0-1 1v6.708A2.486 2.486 0 0 1 4.5 9h8V1.5Z"/></svg>Overview</a>
  <a href="#" class="ptab active"><svg viewBox="0 0 16 16"><path d="M2 2.5A2.5 2.5 0 0 1 4.5 0h8.75a.75.75 0 0 1 .75.75v12.5a.75.75 0 0 1-.75.75h-2.5a.75.75 0 0 1 0-1.5h1.75v-2h-8a1 1 0 0 0-.714 1.7.75.75 0 1 1-1.072 1.05A2.495 2.495 0 0 1 2 11.5Zm10.5-1h-8a1 1 0 0 0-1 1v6.708A2.486 2.486 0 0 1 4.5 9h8V1.5Z"/></svg>Repositories<span class="tab-ct">7</span></a>
  <a href="#" class="ptab"><svg viewBox="0 0 16 16"><path fill-rule="evenodd" d="M1.5 1.75V13.5h13.75a.75.75 0 0 1 0 1.5H.75a.75.75 0 0 1-.75-.75V1.75a.75.75 0 0 1 1.5 0z"/></svg>Projects</a>
  <a href="#" class="ptab"><svg viewBox="0 0 16 16"><path d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.75.75 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25z"/></svg>Stars<span class="tab-ct">1</span></a>
</div>

<!-- MAIN -->
<div class="main">

  <!-- SIDEBAR -->
  <aside class="sidebar">
    <div class="av-wrap">
      <svg class="av-svg" viewBox="0 0 300 300" xmlns="http://www.w3.org/2000/svg">
        <defs>
          <linearGradient id="bg" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#1e2d40"/><stop offset="100%" style="stop-color:#2d4a6e"/></linearGradient>
          <linearGradient id="bl" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#4a7fb5"/><stop offset="100%" style="stop-color:#2d5a9e"/></linearGradient>
          <filter id="glow"><feGaussianBlur stdDeviation="3" result="coloredBlur"/><feMerge><feMergeNode in="coloredBlur"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
        </defs>
        <rect width="300" height="300" fill="url(#bg)"/>
        <!-- Grid lines -->
        <line x1="0" y1="100" x2="300" y2="100" stroke="#58a6ff" stroke-width="0.4" opacity="0.2"/>
        <line x1="0" y1="150" x2="300" y2="150" stroke="#58a6ff" stroke-width="0.4" opacity="0.2"/>
        <line x1="0" y1="200" x2="300" y2="200" stroke="#58a6ff" stroke-width="0.4" opacity="0.2"/>
        <line x1="100" y1="0" x2="100" y2="300" stroke="#58a6ff" stroke-width="0.4" opacity="0.2"/>
        <line x1="200" y1="0" x2="200" y2="300" stroke="#58a6ff" stroke-width="0.4" opacity="0.2"/>
        <!-- O -->
        <rect x="30" y="55" width="95" height="190" rx="14" fill="url(#bl)" filter="url(#glow)"/>
        <rect x="62" y="87" width="31" height="126" rx="6" fill="#1a2a3f"/>
        <!-- J -->
        <rect x="175" y="55" width="95" height="190" rx="14" fill="url(#bl)" filter="url(#glow)"/>
        <rect x="175" y="55" width="95" height="55" rx="14" fill="#1a2a3f" opacity="0.6"/>
        <!-- Glitch lines -->
        <rect x="0" y="147" width="300" height="2" fill="#58a6ff" opacity="0.4"/>
        <rect x="0" y="153" width="220" height="1" fill="#58a6ff" opacity="0.2"/>
        <rect x="80" y="160" width="140" height="1" fill="#3fb950" opacity="0.15"/>
      </svg>
      <div class="av-status"><div class="sdot"></div></div>
    </div>

    <div>
      <div class="pname">Om Jha</div>
      <div class="phandle">omjha-git</div>
    </div>

    <div class="pbio">⚡ MERN Stack Developer<br>Full-stack web development enthusiast.<br>Building the web, one commit at a time.</div>

    <button class="ebtn">
      <svg viewBox="0 0 16 16"><path d="M11.013 1.427a1.75 1.75 0 0 1 2.474 0l1.086 1.086a1.75 1.75 0 0 1 0 2.474l-8.61 8.61c-.21.21-.47.364-.756.445l-3.251.93a.75.75 0 0 1-.927-.928l.929-3.25c.081-.286.235-.547.445-.758l8.61-8.61Zm1.414 1.06a.25.25 0 0 0-.354 0L10.811 3.75l1.439 1.44 1.263-1.263a.25.25 0 0 0 0-.354l-1.086-1.086ZM11.189 6.25 9.75 4.81 4.275 10.286l-.598 2.092 2.092-.598L11.19 6.25Z"/></svg>
      Edit profile
    </button>

    <div class="fstats">
      <svg viewBox="0 0 16 16"><path d="M7 14s-1 0-1-1 1-4 5-4 5 3 5 4-1 1-1 1H7zm4-6a3 3 0 1 0 0-6 3 3 0 0 0 0 6z"/><path fill-rule="evenodd" d="M5.216 14A2.238 2.238 0 0 1 5 13c0-1.355.68-2.75 1.936-3.72A6.325 6.325 0 0 0 5 9c-4 0-5 3-5 4s1 1 1 1h4.216z"/><path d="M4.5 8a2.5 2.5 0 1 0 0-5 2.5 2.5 0 0 0 0 5z"/></svg>
      <a href="#">1 follower</a> &nbsp;·&nbsp; <a href="#">1 following</a>
    </div>

    <div>
      <div class="slabel">Socials</div>
      <div class="slinks">
        <a href="https://instagram.com/_om.jha__" class="slink" target="_blank">
          <svg viewBox="0 0 16 16"><path d="M8 0C5.829 0 5.556.01 4.703.048 3.85.088 3.269.222 2.76.42a3.917 3.917 0 0 0-1.417.923A3.927 3.927 0 0 0 .42 2.76C.222 3.268.087 3.85.048 4.7.01 5.555 0 5.827 0 8.001c0 2.172.01 2.444.048 3.297.04.852.174 1.433.372 1.942.205.526.478.972.923 1.417.444.445.89.719 1.416.923.51.198 1.09.333 1.942.372C5.555 15.99 5.827 16 8 16s2.444-.01 3.298-.048c.851-.04 1.434-.174 1.943-.372a3.916 3.916 0 0 0 1.416-.923c.445-.445.718-.891.923-1.417.197-.509.332-1.09.372-1.942C15.99 10.445 16 10.173 16 8s-.01-2.445-.048-3.299c-.04-.851-.175-1.433-.372-1.941a3.926 3.926 0 0 0-.923-1.417A3.911 3.911 0 0 0 13.24.42c-.51-.198-1.092-.333-1.943-.372C10.443.01 10.172 0 7.998 0h.003zm-.717 1.442h.718c2.136 0 2.389.007 3.232.046.78.035 1.204.166 1.486.275.373.145.64.319.92.599.28.28.453.546.598.92.11.281.24.705.275 1.485.039.843.047 1.096.047 3.231s-.008 2.389-.047 3.232c-.035.78-.166 1.203-.275 1.485a2.47 2.47 0 0 1-.599.919c-.28.28-.546.453-.92.598-.28.11-.704.24-1.485.276-.843.038-1.096.047-3.232.047s-2.39-.009-3.233-.047c-.78-.036-1.203-.166-1.485-.276a2.478 2.478 0 0 1-.92-.598 2.48 2.48 0 0 1-.6-.92c-.109-.281-.24-.705-.275-1.485-.038-.843-.046-1.096-.046-3.233 0-2.136.008-2.388.046-3.231.036-.78.166-1.204.276-1.486.145-.373.319-.64.599-.92.28-.28.546-.453.92-.598.282-.11.705-.24 1.485-.276.738-.034 1.024-.044 2.515-.045v.002zm4.988 1.328a.96.96 0 1 0 0 1.92.96.96 0 0 0 0-1.92zm-4.27 1.122a4.109 4.109 0 1 0 0 8.217 4.109 4.109 0 0 0 0-8.217zm0 1.441a2.667 2.667 0 1 1 0 5.334 2.667 2.667 0 0 1 0-5.334z"/></svg>
          _om.jha__
        </a>
        <a href="https://linkedin.com/in/om-jha--" class="slink" target="_blank">
          <svg viewBox="0 0 16 16"><path d="M0 1.146C0 .513.526 0 1.175 0h13.65C15.474 0 16 .513 16 1.146v13.708c0 .633-.526 1.146-1.175 1.146H1.175C.526 16 0 15.487 0 14.854V1.146zm4.943 12.248V6.169H2.542v7.225h2.401zm-1.2-8.212c.837 0 1.358-.554 1.358-1.248-.015-.709-.52-1.248-1.342-1.248-.822 0-1.359.54-1.359 1.248 0 .694.521 1.248 1.327 1.248h.016zm4.908 8.212V9.359c0-.216.016-.432.08-.586.173-.431.568-.878 1.232-.878.869 0 1.216.662 1.216 1.634v3.865h2.401V9.25c0-2.22-1.184-3.252-2.764-3.252-1.274 0-1.845.7-2.165 1.193v.025h-.016a5.54 5.54 0 0 1 .016-.025V6.169h-2.4c.03.678 0 7.225 0 7.225h2.4z"/></svg>
          om-jha
        </a>
        <a href="mailto:jhaom1085@gmail.com" class="slink">
          <svg viewBox="0 0 16 16"><path d="M0 4a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v8a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V4Zm2-1a1 1 0 0 0-1 1v.217l7 4.2 7-4.2V4a1 1 0 0 0-1-1H2Zm13 2.383-4.708 2.825L15 11.105V5.383Zm-.034 6.876-5.64-3.471L8 9.583l-1.326-.795-5.64 3.47A1 1 0 0 0 2 13h12a1 1 0 0 0 .966-.741ZM1 11.105l4.708-2.897L1 5.383v5.722Z"/></svg>
          jhaom1085@gmail.com
        </a>
      </div>
    </div>

    <div>
      <div class="slabel">Tech Stack</div>
      <div class="tstack">
        <span class="tb js">JavaScript</span><span class="tb nd">Node.js</span><span class="tb re">React</span>
        <span class="tb mg">MongoDB</span><span class="tb ht">HTML5</span><span class="tb cs">CSS3</span>
        <span class="tb ex">Express.js</span><span class="tb nx">Next.js</span><span class="tb dk">Docker</span>
        <span class="tb cp">C++</span><span class="tb jv">Java</span><span class="tb py">Pandas</span>
        <span class="tb cs" style="color:#8D6748;border-color:#8D674833;background:#8D674810">Mocha</span>
        <span class="tb re" style="color:#40B5A4;border-color:#40B5A433;background:#40B5A410">Puppeteer</span>
      </div>
    </div>
  </aside>

  <!-- CONTENT -->
  <main class="content">

    <!-- Toolbar -->
    <div class="toolbar fu">
      <input class="rsearch" type="text" placeholder="Find a repository..." id="repoSearch">
      <button class="tbtn">Type <svg viewBox="0 0 16 16"><path d="m4.427 7.427 3.396 3.396a.25.25 0 0 0 .354 0l3.396-3.396A.25.25 0 0 0 11.396 7H4.604a.25.25 0 0 0-.177.427z"/></svg></button>
      <button class="tbtn">Language <svg viewBox="0 0 16 16"><path d="m4.427 7.427 3.396 3.396a.25.25 0 0 0 .354 0l3.396-3.396A.25.25 0 0 0 11.396 7H4.604a.25.25 0 0 0-.177.427z"/></svg></button>
      <button class="tbtn">Sort <svg viewBox="0 0 16 16"><path d="m4.427 7.427 3.396 3.396a.25.25 0 0 0 .354 0l3.396-3.396A.25.25 0 0 0 11.396 7H4.604a.25.25 0 0 0-.177.427z"/></svg></button>
      <button class="tbtn newbtn">
        <svg viewBox="0 0 16 16" fill="white" width="13" height="13"><path d="M2 2.5A2.5 2.5 0 0 1 4.5 0h8.75a.75.75 0 0 1 .75.75v12.5a.75.75 0 0 1-.75.75h-2.5a.75.75 0 0 1 0-1.5h1.75v-2h-8a1 1 0 0 0-.714 1.7.75.75 0 1 1-1.072 1.05A2.495 2.495 0 0 1 2 11.5Zm10.5-1h-8a1 1 0 0 0-1 1v6.708A2.486 2.486 0 0 1 4.5 9h8V1.5Z"/></svg>
        New
      </button>
    </div>

    <!-- Repo Cards -->
    <div class="rgrid fu" id="repoGrid">
      <!-- omjha_git -->
      <div class="rcard" data-name="omjha_git">
        <div>
          <div class="rnamerow"><a href="https://github.com/omjha-git/omjha_git" class="rname" target="_blank">omjha_git</a><span class="rbadge">Public</span></div>
          <div class="rmeta"><span class="rtime">Updated 1 minute ago</span></div>
        </div>
        <button class="sbtn"><svg viewBox="0 0 16 16"><path d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.75.75 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25z"/></svg>Star</button>
      </div>
      <!-- airbnb -->
      <div class="rcard" data-name="airbnb">
        <div>
          <div class="rnamerow"><a href="https://github.com/omjha-git/airbnb" class="rname" target="_blank">airbnb</a><span class="rbadge">Public</span></div>
          <div class="rdesc">Airbnb clone project built with JavaScript</div>
          <div class="rmeta"><span class="rlang"><span class="ldot ljs"></span>JavaScript</span><span class="rtime">Updated last week</span></div>
        </div>
        <button class="sbtn"><svg viewBox="0 0 16 16"><path d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.75.75 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25z"/></svg>Star</button>
      </div>
      <!-- spotify -->
      <div class="rcard" data-name="spotify">
        <div>
          <div class="rnamerow"><a href="https://github.com/omjha-git/spotify" class="rname" target="_blank">spotify</a><span class="rbadge">Public</span></div>
          <div class="rdesc">Spotify clone using HTML &amp; CSS</div>
          <div class="rmeta"><span class="rlang"><span class="ldot lhtml"></span>HTML</span><span class="rtime">Updated on Jan 12</span></div>
        </div>
        <button class="sbtn"><svg viewBox="0 0 16 16"><path d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.75.75 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25z"/></svg>Star</button>
      </div>
      <!-- simon-says -->
      <div class="rcard" data-name="simon-says">
        <div>
          <div class="rnamerow"><a href="https://github.com/omjha-git/simon-says" class="rname" target="_blank">simon-says</a><span class="rbadge">Public</span></div>
          <div class="rdesc">Classic Simon Says memory game in JavaScript</div>
          <div class="rmeta"><span class="rlang"><span class="ldot ljs"></span>JavaScript</span><span class="rtime">Updated on Dec 29, 2025</span></div>
        </div>
        <button class="sbtn"><svg viewBox="0 0 16 16"><path d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.75.75 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25z"/></svg>Star</button>
      </div>
      <!-- project2 -->
      <div class="rcard" data-name="project2">
        <div>
          <div class="rnamerow"><a href="https://github.com/omjha-git/project2" class="rname" target="_blank">project2</a><span class="rbadge">Public</span></div>
          <div class="rmeta"><span class="rtime">Updated on Dec 29, 2025</span></div>
        </div>
        <button class="sbtn"><svg viewBox="0 0 16 16"><path d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.75.75 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25z"/></svg>Star</button>
      </div>
      <!-- boat -->
      <div class="rcard" data-name="boat">
        <div>
          <div class="rnamerow"><a href="https://github.com/omjha-git/boat" class="rname" target="_blank">boat</a><span class="rbadge">Public</span></div>
          <div class="rdesc">Boat landing page clone with HTML</div>
          <div class="rmeta"><span class="rlang"><span class="ldot lhtml"></span>HTML</span><span class="rtime">Updated on Jul 5, 2025</span></div>
        </div>
        <button class="sbtn"><svg viewBox="0 0 16 16"><path d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.75.75 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25z"/></svg>Star</button>
      </div>
      <!-- amazon -->
      <div class="rcard" data-name="amazon">
        <div>
          <div class="rnamerow"><a href="https://github.com/omjha-git/amazon" class="rname" target="_blank">amazon</a><span class="rbadge">Public</span></div>
          <div class="rdesc">Amazon homepage clone using CSS</div>
          <div class="rmeta"><span class="rlang"><span class="ldot lcss"></span>CSS</span><span class="rtime">Updated on Jun 30, 2025</span></div>
        </div>
        <button class="sbtn"><svg viewBox="0 0 16 16"><path d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.75.75 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25z"/></svg>Star</button>
      </div>
    </div>

    <!-- CONTRIBUTION GRAPH -->
    <div class="cgraph-wrap fu">
      <div class="cg-title" id="cgTitle">382 contributions in the last year</div>
      <div class="cgraph" id="cgraph"></div>
      <div class="cg-legend">
        Less
        <div style="background:var(--bg4)"></div>
        <div style="background:#0e4429"></div>
        <div style="background:#006d32"></div>
        <div style="background:#26a641"></div>
        <div style="background:#39d353"></div>
        More
      </div>
    </div>

    <!-- STATS -->
    <div class="sgrid fu">
      <div class="scard"><img src="https://github-readme-stats.vercel.app/api?username=omjha-git&theme=github_dark&hide_border=true&include_all_commits=false&count_private=false" alt="GitHub Stats"></div>
      <div class="scard"><img src="https://nirzak-streak-stats.vercel.app/?user=omjha-git&theme=github_dark_dimmed&hide_border=true" alt="Streak Stats"></div>
      <div class="scard"><img src="https://github-readme-stats.vercel.app/api/top-langs/?username=omjha-git&theme=github_dark&hide_border=true&layout=compact" alt="Top Languages"></div>
    </div>

    <!-- PINNED -->
    <div class="fu">
      <div class="slabel" style="margin-bottom:14px;">Pinned</div>
      <div class="pgrid">
        <div class="pcard"><div class="plabel"><svg viewBox="0 0 16 16"><path d="M4.456.734a1.75 1.75 0 0 1 2.826.504l.613 1.327a3.081 3.081 0 0 0 2.084 1.707l2.454.584c.564.135.846.76.57 1.273l-1.365 2.527a3.081 3.081 0 0 0-.17 2.638l.903 2.405c.206.547-.176 1.14-.759 1.158l-2.551.07a3.081 3.081 0 0 0-2.19 1.018l-1.713 1.957a.75.75 0 0 1-1.275-.254l-.757-2.448a3.081 3.081 0 0 0-1.814-1.929l-2.403-.908a.75.75 0 0 1-.246-1.275l1.953-1.719a3.081 3.081 0 0 0 1.011-2.195l.07-2.551c.018-.583.611-.965 1.158-.759l2.406.903A3.081 3.081 0 0 0 7.68 5.87l.584-2.454a3.081 3.081 0 0 0-1.707-2.084L5.23 2.719A1.75 1.75 0 0 1 4.456.734z"/></svg>Pinned</div><div class="pn">airbnb</div><div class="pd">Airbnb clone — JavaScript, React components</div><div class="rmeta"><span class="rlang"><span class="ldot ljs"></span>JavaScript</span></div></div>
        <div class="pcard"><div class="plabel"><svg viewBox="0 0 16 16"><path d="M4.456.734a1.75 1.75 0 0 1 2.826.504l.613 1.327a3.081 3.081 0 0 0 2.084 1.707l2.454.584c.564.135.846.76.57 1.273l-1.365 2.527a3.081 3.081 0 0 0-.17 2.638l.903 2.405c.206.547-.176 1.14-.759 1.158l-2.551.07a3.081 3.081 0 0 0-2.19 1.018l-1.713 1.957a.75.75 0 0 1-1.275-.254l-.757-2.448a3.081 3.081 0 0 0-1.814-1.929l-2.403-.908a.75.75 0 0 1-.246-1.275l1.953-1.719a3.081 3.081 0 0 0 1.011-2.195l.07-2.551c.018-.583.611-.965 1.158-.759l2.406.903A3.081 3.081 0 0 0 7.68 5.87l.584-2.454a3.081 3.081 0 0 0-1.707-2.084L5.23 2.719A1.75 1.75 0 0 1 4.456.734z"/></svg>Pinned</div><div class="pn">spotify</div><div class="pd">Spotify clone — HTML &amp; CSS</div><div class="rmeta"><span class="rlang"><span class="ldot lhtml"></span>HTML</span></div></div>
        <div class="pcard"><div class="plabel"><svg viewBox="0 0 16 16"><path d="M4.456.734a1.75 1.75 0 0 1 2.826.504l.613 1.327a3.081 3.081 0 0 0 2.084 1.707l2.454.584c.564.135.846.76.57 1.273l-1.365 2.527a3.081 3.081 0 0 0-.17 2.638l.903 2.405c.206.547-.176 1.14-.759 1.158l-2.551.07a3.081 3.081 0 0 0-2.19 1.018l-1.713 1.957a.75.75 0 0 1-1.275-.254l-.757-2.448a3.081 3.081 0 0 0-1.814-1.929l-2.403-.908a.75.75 0 0 1-.246-1.275l1.953-1.719a3.081 3.081 0 0 0 1.011-2.195l.07-2.551c.018-.583.611-.965 1.158-.759l2.406.903A3.081 3.081 0 0 0 7.68 5.87l.584-2.454a3.081 3.081 0 0 0-1.707-2.084L5.23 2.719A1.75 1.75 0 0 1 4.456.734z"/></svg>Pinned</div><div class="pn">simon-says</div><div class="pd">Classic memory game built with JavaScript</div><div class="rmeta"><span class="rlang"><span class="ldot ljs"></span>JavaScript</span></div></div>
        <div class="pcard"><div class="plabel"><svg viewBox="0 0 16 16"><path d="M4.456.734a1.75 1.75 0 0 1 2.826.504l.613 1.327a3.081 3.081 0 0 0 2.084 1.707l2.454.584c.564.135.846.76.57 1.273l-1.365 2.527a3.081 3.081 0 0 0-.17 2.638l.903 2.405c.206.547-.176 1.14-.759 1.158l-2.551.07a3.081 3.081 0 0 0-2.19 1.018l-1.713 1.957a.75.75 0 0 1-1.275-.254l-.757-2.448a3.081 3.081 0 0 0-1.814-1.929l-2.403-.908a.75.75 0 0 1-.246-1.275l1.953-1.719a3.081 3.081 0 0 0 1.011-2.195l.07-2.551c.018-.583.611-.965 1.158-.759l2.406.903A3.081 3.081 0 0 0 7.68 5.87l.584-2.454a3.081 3.081 0 0 0-1.707-2.084L5.23 2.719A1.75 1.75 0 0 1 4.456.734z"/></svg>Pinned</div><div class="pn">amazon</div><div class="pd">Amazon homepage clone — CSS</div><div class="rmeta"><span class="rlang"><span class="ldot lcss"></span>CSS</span></div></div>
      </div>
    </div>

    <!-- QUOTE -->
    <div class="qcard fu">
      <img src="https://quotes-github-readme.vercel.app/api?type=horizontal&theme=dark" alt="Dev Quote" style="border-radius:10px;">
    </div>

  </main>
</div>

<footer>
  <div>© 2025 GitHub, Inc. · <a href="#">Terms</a> · <a href="#">Privacy</a> · <a href="#">Security</a> · <a href="#">Status</a> · <a href="#">Docs</a> · <a href="#">Contact</a></div>
  <div style="margin-top:6px; color:var(--text3);">Profile of <a href="https://github.com/omjha-git" target="_blank">omjha-git</a> · MERN Stack Developer 🤖</div>
</footer>

<script>
// ── ROBOT CURSOR ──
const rc = document.getElementById('robot-cursor');
const rm = document.getElementById('rmount');
let mx=window.innerWidth/2, my=window.innerHeight/2, rx=mx, ry=my;
let mt;

document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  rm.classList.add('talk');
  clearTimeout(mt);
  mt = setTimeout(() => rm.classList.remove('talk'), 250);
  // trail
  const d = document.createElement('div');
  d.className = 'trail';
  d.style.left = mx+'px'; d.style.top = my+'px';
  document.body.appendChild(d);
  setTimeout(() => d.remove(), 600);
});

(function anim() {
  rx += (mx-rx)*0.13; ry += (my-ry)*0.13;
  rc.style.left = rx+'px'; rc.style.top = ry+'px';
  requestAnimationFrame(anim);
})();

// ── CONTRIBUTION GRAPH ──
const cg = document.getElementById('cgraph');
let totalContribs = 0;
for (let w=0; w<52; w++) {
  const wk = document.createElement('div');
  wk.className = 'cweek';
  for (let d=0; d<7; d++) {
    const day = document.createElement('div');
    const r = Math.random();
    let l = 0;
    if (r > 0.55) l = Math.floor(Math.random()*4)+1;
    totalContribs += l * 2;
    day.className = 'cday' + (l ? ' l'+l : '');
    day.title = l ? `${l*2} contributions` : 'No contributions';
    wk.appendChild(day);
  }
  cg.appendChild(wk);
}
document.getElementById('cgTitle').textContent = `${totalContribs} contributions in the last year`;

// ── SCROLL FADE ──
const obs = new IntersectionObserver(entries => {
  entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('vis'); });
}, { threshold: 0.08 });
document.querySelectorAll('.fu').forEach((el, i) => {
  el.style.transitionDelay = (i * 0.07)+'s';
  obs.observe(el);
});

// ── STAR TOGGLE ──
document.querySelectorAll('.sbtn').forEach(btn => {
  btn.addEventListener('click', () => btn.classList.toggle('starred'));
});

// ── REPO SEARCH ──
document.getElementById('repoSearch').addEventListener('input', e => {
  const q = e.target.value.toLowerCase();
  document.querySelectorAll('.rcard').forEach(c => {
    c.style.display = c.dataset.name.includes(q) ? '' : 'none';
  });
});
</script>
</body>
</html>
