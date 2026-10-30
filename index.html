<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no, viewport-fit=cover">
<title>Proyecto</title>
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
<style>
:root{--bg:#1b1b33;--panel:#2a2a4a;--ink:#fbe9f0;--pink:#ff7a9c;--gold:#ffd77a;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent;-webkit-user-select:none;user-select:none;-webkit-touch-callout:none}
html,body{margin:0;height:100%;background:var(--bg);color:var(--ink);font-family:'Press Start 2P',ui-monospace,monospace;overflow:hidden;touch-action:none}
#app{height:100%;display:flex;flex-direction:column;align-items:center;justify-content:space-between;padding:10px 10px 14px;max-width:560px;margin:0 auto}
#hud{width:100%;display:flex;justify-content:space-between;font-size:10px;line-height:1.6}
#stage{position:relative;width:100%}
canvas{width:100%;display:block;image-rendering:pixelated;image-rendering:crisp-edges;border:3px solid var(--panel);background:#000}
.ov{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;gap:14px;padding:16px;background:rgba(27,27,51,.55)}
.ov.hide{display:none}
h1{font-size:clamp(14px,5vw,22px);margin:0;line-height:1.5;text-shadow:3px 3px 0 #6b2f55}
p{font-size:9px;line-height:1.9;margin:0}
.btn{font-family:inherit;font-size:11px;color:#2b1230;background:var(--pink);border:0;padding:12px 16px;box-shadow:0 4px 0 #a8365c;border-radius:3px}
.btn:active{transform:translateY(3px);box-shadow:0 1px 0 #a8365c}
#pad{width:100%;display:flex;justify-content:space-between;align-items:center;gap:10px}
.k{width:76px;height:76px;border-radius:10px;border:3px solid #4a4a7a;background:var(--panel);color:var(--ink);font-family:inherit;font-size:24px;box-shadow:0 5px 0 #14142a}
.k.on{transform:translateY(4px);box-shadow:0 1px 0 #14142a;background:#3a3a66}
#jump{width:112px;background:#6b2f55;border-color:var(--pink);font-size:11px}
.grp{display:flex;gap:10px}
</style>
</head>
<body>
<div id="app">
  <div id="hud"><span id="n1">Dana</span><span id="sc">🐶 0 / 4</span></div>
  <div id="stage">
    <canvas id="c" width="320" height="180"></canvas>
    <div class="ov" id="start">
      <h1 id="title">PROYECTO</h1>
      <p style="font-size:11px;color:var(--gold)">¿Jóvenes, a eso vienen?</p>
      <p>Salta sobre las ratas<br>para salvar a los peitos</p>
      <button class="btn" id="go">▶ INICIAR PARTIDA</button>
    </div>
    <div class="ov hide" id="end">
      <h1>NIVEL COMPLETADO</h1>
      <p id="line"></p>
      <button class="btn" id="next">SIGUIENTE</button>
    </div>
  </div>
  <div id="pad">
    <div class="grp"><button class="k" id="L">◀</button><button class="k" id="R">▶</button></div>
    <button class="k" id="jump">SALTAR</button>
  </div>
</div>
<script>
// ====== CONFIGURA AQUÍ ======
const CFG = { p1: 'Eder', p2: 'Dana' };
// ============================
const W = 320, H = 180, GY = 150, LEN = 1700;
const cv = document.getElementById('c'), cx = cv.getContext('2d');
document.getElementById('n1').textContent = CFG.p1;
document.getElementById('title').textContent = 'PROYECTO';

let ac; function beep(f, d, t) { try { ac = ac || new (window.AudioContext || window.webkitAudioContext)(); const o = ac.createOscillator(), g = ac.createGain(); o.type = t || 'square'; o.frequency.value = f; g.gain.value = .05; o.connect(g); g.connect(ac.destination); o.start(); o.stop(ac.currentTime + d); } catch (e) {} }

const keys = { l: 0, r: 0, j: 0 };
function bind(id, k) {
  const el = document.getElementById(id);
  const on = e => { e.preventDefault(); keys[k] = 1; el.classList.add('on'); };
  const off = e => { e.preventDefault(); keys[k] = 0; el.classList.remove('on'); };
  el.addEventListener('pointerdown', on); el.addEventListener('pointerup', off);
  el.addEventListener('pointercancel', off); el.addEventListener('pointerleave', off);
  el.addEventListener('contextmenu', e => e.preventDefault());
}
bind('L', 'l'); bind('R', 'r'); bind('jump', 'j');
const km = { ArrowLeft: 'l', ArrowRight: 'r', ArrowUp: 'j', ' ': 'j', a: 'l', d: 'r', w: 'j' };
addEventListener('keydown', e => { if (km[e.key]) { keys[km[e.key]] = 1; e.preventDefault(); } });
addEventListener('keyup', e => { if (km[e.key]) keys[km[e.key]] = 0; });
document.addEventListener('gesturestart', e => e.preventDefault());

let p, scenes, hearts, cam, saved, state, tick, kiss = 0;
function reset() {
  p = { x: 20, y: GY - 14, vx: 0, vy: 0, w: 8, h: 14, ground: 1, inv: 0, face: 1 };
  scenes = [330, 640, 960, 1260].map(x => ({ x, dog: true, mouseX: x + 28, t: Math.random() * 50, run: 0 }));
  hearts = []; cam = 0; saved = 0; tick = 0; kiss = 0; state = 'play';
  document.getElementById('sc').textContent = '🐶 0 / ' + scenes.length;
}
reset(); state = 'menu';

const R = (x, y, w, h, c) => { cx.fillStyle = c; cx.fillRect(Math.round(x - cam), Math.round(y), w, h); };
const RS = (x, y, w, h, c) => { cx.fillStyle = c; cx.fillRect(Math.round(x), Math.round(y), w, h); };

function person(x, y, hair, top, long, step, face) {
  R(x + 1, y, 6, 6, '#f4c9a0');
  R(x, y - 1, 8, 3, hair);
  if (long) { R(x, y + 2, 2, 7, hair); R(x + 6, y + 2, 2, 7, hair); }
  R(face > 0 ? x + 5 : x + 2, y + 3, 1, 1, '#2b1230');
  R(x + 1, y + 6, 6, 5, top);
  const s = step ? 1 : 0;
  R(x + 1, y + 11, 2, 3 - s, '#3a2a4a'); R(x + 5, y + 11, 2, 2 + s, '#3a2a4a');
}
function dog(x, off, dy) {
  const y = GY - 9 + (dy || 0), c = '#b5793f';
  R(x + off + 2, y + 2, 11, 5, c); R(x + off - 2, y, 6, 6, c); R(x + off - 3, y - 1, 2, 4, '#6e4420');
  R(x + off - 1, y + 2, 1, 1, '#111'); R(x + off - 3, y + 4, 2, 2, '#222');
  R(x + off + 12, y + 1, 3, 2, c);
  R(x + 3, y + 7, 2, 2, '#6e4420'); R(x + 10, y + 7, 2, 2, '#6e4420');
  R(x + off - 1, y - 4, 4, 3, '#fff'); R(x + off, y - 5, 2, 1, '#fff'); // "¡guau!"
}
function rat(x) {
  R(x - 6, GY - 4, 6, 2, '#f3a6bd'); R(x, GY - 9, 14, 8, '#7d7790');
  R(x + 2, GY - 12, 4, 4, '#f3a6bd'); R(x + 8, GY - 12, 4, 4, '#f3a6bd');
  R(x + 10, GY - 7, 2, 2, '#e02020'); R(x + 13, GY - 5, 2, 2, '#f3a6bd');
  R(x + 14, GY - 3, 4, 3, '#a39eb8'); R(x + 2, GY - 1, 3, 1, '#5b5670'); R(x + 9, GY - 1, 3, 1, '#5b5670');
}
function mouse(x, y, c) {
  R(x, y, 7, 4, '#b9b4c9'); R(x + 5, y - 2, 2, 2, '#f3a6bd'); R(x + 1, y - 2, 2, 2, '#f3a6bd');
  R(x + 6, y + 1, 1, 1, '#111'); R(x - 3, y + 2, 3, 1, '#f3a6bd');
}

function draw() {
  // cielo
  const bands = ['#7b6fb5', '#9a80b9', '#bb8fba', '#d99ba8'];
  bands.forEach((b, i) => RS(0, i * 40, W, 40, b));
  RS(240, 24, 26, 26, '#ffd77a');
  // nubes
  for (let i = 0; i < 4; i++) { const x = ((i * 180 - cam * .2) % 520 + 520) % 520 - 60; RS(x, 22 + i * 12 % 36, 40, 8, '#f3b8c8'); RS(x + 8, 16 + i * 12 % 36, 22, 6, '#f3b8c8'); }
  // colinas
  for (let i = 0; i < 6; i++) { const x = ((i * 120 - cam * .4) % 720 + 720) % 720 - 120; RS(x, 96, 110, 54, '#8a7aa8'); RS(x + 20, 80, 70, 16, '#8a7aa8'); RS(x + 40, 70, 30, 10, '#8a7aa8'); }
  // árboles
  for (let i = 0; i < 14; i++) { const x = i * 130 + 60; R(x + 8, 120, 6, 30, '#8c4a5e'); R(x, 100, 22, 22, '#5f8f6a'); R(x + 4, 92, 14, 10, '#5f8f6a'); R(x + 2, 104, 4, 4, '#7bb083'); }
  // suelo
  RS(0, GY, W, 6, '#a6c35a'); RS(0, GY + 6, W, H - GY, '#8c4a5e');
  for (let x = -((cam | 0) % 16); x < W; x += 16) { RS(x, GY + 10, 8, 2, '#7a3d50'); RS(x + 8, GY + 18, 6, 2, '#a85c70'); }
  // flores
  for (let i = 0; i < 30; i++) R(i * 58 + 20, GY - 3, 2, 3, i % 2 ? '#ffd77a' : '#fff');
  // escenas
  scenes.forEach(s => {
    const hit = s.dog ? Math.max(0, Math.sin(s.t * .14)) : 0;
    if (s.dog) rat(s.x + hit * 6);
    dog(s.mouseX + (hit > .6 ? 2 : 0), 0, s.run ? -Math.abs(Math.sin(tick * .3)) * 5 : 0);
  });
  // jugador 2
  person(LEN - 40, GY - 14, '#6b3a22', '#d96b8c', true, 0, -1);
  R(LEN - 40, GY - 22 + Math.sin(tick * .1) * 2, 6, 5, '#ff7a9c');
  // jugadora
  if (p.inv % 8 < 4) person(p.x, p.y, '#3a211a', '#315a7d', false, p.ground && keys.r + keys.l && (tick >> 3) % 2, p.face);
  if (kiss) { const hy = GY - 24 + Math.sin(tick * .15) * 2; R(LEN - 48, hy, 5, 4, '#ff5c85'); R(LEN - 42, hy, 5, 4, '#ff5c85'); R(LEN - 47, hy + 4, 10, 3, '#ff5c85'); R(LEN - 45, hy + 7, 6, 2, '#ff5c85'); }
  hearts.forEach(h => { R(h.x, h.y, 3, 3, '#ff5c85'); R(h.x + 3, h.y, 3, 3, '#ff5c85'); R(h.x + 1, h.y + 3, 4, 2, '#ff5c85'); });
}

function update() {
  tick++;
  scenes.forEach(s => { s.t++; });
  hearts.forEach(h => { h.y -= .6; h.life--; }); hearts = hearts.filter(h => h.life > 0);
  if (state !== 'play') return;
  const m = keys.r - keys.l;
  p.vx = m * 1.7; if (m) p.face = m;
  if (keys.j && p.ground) { p.vy = -5.4; p.ground = 0; beep(520, .1); }
  p.x = Math.max(0, Math.min(LEN - 8, p.x + p.vx));
  p.vy += .32; p.y += p.vy;
  if (p.y + p.h >= GY) { p.y = GY - p.h; p.vy = 0; p.ground = 1; }
  if (p.inv > 0) p.inv--;
  scenes.forEach(s => {
    if (!s.dog) return;
    const hit = Math.max(0, Math.sin(s.t * .14)) * 6;
    const dx = s.x + hit - 1, dy = GY - 12, dw = 16, dh = 12;
    if (p.x + p.w > dx && p.x < dx + dw && p.y + p.h > dy && p.y < dy + dh) {
      if (p.vy > 0 && p.y + p.h - p.vy <= dy + 4) {
        s.dog = false; s.run = 1; p.vy = -4; p.ground = 0; saved++;
        hearts.push({ x: s.mouseX, y: GY - 14, life: 70 }, { x: s.mouseX + 6, y: GY - 20, life: 60 });
        document.getElementById('sc').textContent = '🐶 ' + saved + ' / ' + scenes.length;
        beep(780, .12); setTimeout(() => beep(1040, .15), 90);
      } else if (p.inv <= 0) {
        p.inv = 60; p.vy = -3; p.ground = 0; p.x = Math.max(0, p.x - 28); beep(160, .2, 'sawtooth');
      }
    }
  });
  if (p.x > LEN - 58) finish();
  cam = Math.max(0, Math.min(LEN - W, p.x - 120));
}

const lines = () => [
  CFG.p1 + ': Hola…',
  CFG.p2 + ': ¿Hiciste todo este camino por mí?',
  CFG.p1 + ': Sí. Y lo volvería a hacer mil veces.',
  'Peitos salvados: ' + saved + ' de ' + scenes.length + ' 🐶',
  CFG.p1 + ': Te quiero mucho, ' + CFG.p2 + ' ♥',
  '💋 ' + CFG.p1 + ' besa a ' + CFG.p2 + ' ♥',
  'Con amor, ' + CFG.p1 + ' ♥'
];
let li = 0;
function finish() {
  state = 'end'; li = 0; p.x = LEN - 62; p.face = 1; keys.l = keys.r = keys.j = 0;
  hearts.push(...[0, 1, 2, 3, 4, 5].map(i => ({ x: LEN - 60 + i * 8, y: GY - 20 - i * 3, life: 120 })));
  beep(880, .15); setTimeout(() => beep(1180, .25), 140);
  setTimeout(() => { document.getElementById('end').classList.remove('hide'); show(); }, 700);
}
function show() {
  kiss = li >= lines().length - 2;
  if (kiss) { p.x = LEN - 48; beep(990, .1); for (let i = 0; i < 8; i++) hearts.push({ x: LEN - 50 + (i % 4) * 6, y: GY - 24 - i * 4, life: 120 }); }
  document.getElementById('line').innerHTML = lines()[li]; document.getElementById('next').textContent = li === lines().length - 1 ? '↺ JUGAR OTRA VEZ' : 'SIGUIENTE'; }
document.getElementById('next').onclick = () => {
  if (li < lines().length - 1) { li++; show(); }
  else { document.getElementById('end').classList.add('hide'); reset(); }
};
document.getElementById('go').onclick = () => { document.getElementById('start').classList.add('hide'); reset(); beep(660, .1); };

let last = 0;
function loop(t) { if (t - last > 14) { update(); last = t; } draw(); requestAnimationFrame(loop); }
requestAnimationFrame(loop);
</script>
</body>
</html>
