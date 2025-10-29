# Proposal-kavitha
<!doctype html>

<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Kavitha — Will You Be Mine?</title>
  <style>
    :root{--bg:#0f1724;--card:#0b1220;--accent:#ff3b6b}
    *{box-sizing:border-box}
    html,body{height:100%;margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,'Helvetica Neue',Arial}
    body{background: radial-gradient(circle at 10% 10%, #10213a 0%, #061022 40%, var(--bg) 100%);display:flex;align-items:center;justify-content:center;color:#e6eef8}
    .card{width:min(920px,95vw);background:linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.01));border-radius:20px;padding:36px;box-shadow:0 10px 40px rgba(2,6,23,0.7);position:relative;overflow:hidden;text-align:center}
    h1{font-size:clamp(28px,6vw,56px);margin:0 0 8px 0;letter-spacing:1px}
    .name{color:var(--accent);font-weight:700}
    p.lead{margin:0 0 22px 0;font-size:18px;color:#cfe6ff}
    .btn{background:linear-gradient(90deg,#ff6a90,#ff3b6b);border:none;padding:14px 20px;border-radius:12px;color:white;font-weight:700;cursor:pointer;box-shadow:0 6px 18px rgba(255,59,107,0.25);transition:transform .18s ease}
    .btn:active{transform:translateY(2px)}
    .small{background:transparent;border:1px solid rgba(255,255,255,0.06);padding:10px 14px;border-radius:10px;color:#dcecff}
    .hearts{position:absolute;right:-40px;top:-40px;pointer-events:none}
    .heart{width:160px;height:160px;background:conic-gradient(from 200deg, var(--accent), #ff9db0);transform:rotate(45deg);border-radius:24px 24px 24px 0;opacity:.09;filter:blur(6px)}
    footer{position:absolute;left:20px;bottom:14px;color:#9fb1d6;font-size:13px}
    .message{background:rgba(255,255,255,0.02);padding:18px;border-radius:14px;border:1px solid rgba(255,255,255,0.02)}/* Heart-shaped photo */
.photo-heart {
  position: relative;
  width: 250px;
  height: 230px;
  margin: 0 auto 24px;
  clip-path: path('M12 21s-6.5-4.35-9-7.1C-0.2 10.05 3.2 4.5 7.8 7.3 9.4 8.4 10.1 9.7 12 11c1.9-1.3 2.6-2.6 4.2-3.7C20.8 4.5 24.2 10 21 13.9 18.5 16.65 12 21 12 21z');
  background: radial-gradient(circle at center, #ffb6c1, #ff3b6b);
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  animation: pulse 1.8s infinite ease-in-out;
  border-radius: 20px;
}
.photo-heart img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: brightness(1.1);
}
@keyframes pulse {
  0%, 100% { transform: scale(1); box-shadow: 0 0 15px #ff3b6b; }
  50% { transform: scale(1.05); box-shadow: 0 0 30px #ff7fa5; }
}

/* overlay */
.overlay{position:fixed;inset:0;background:rgba(2,6,23,0.6);backdrop-filter:blur(4px);display:flex;align-items:center;justify-content:center;z-index:30;opacity:0;pointer-events:none;transition:opacity .25s}
.overlay.show{opacity:1;pointer-events:auto}
.popup{background:linear-gradient(180deg,#071022,#082036);padding:28px;border-radius:16px;box-shadow:0 20px 50px rgba(2,6,23,0.6);text-align:center;color:#eaf6ff;width:min(720px,92vw)}
.ring{width:120px;height:120px;border-radius:50%;margin:18px auto 10px;border:6px solid rgba(255,255,255,0.06);display:flex;align-items:center;justify-content:center}
.ring .inner{width:70px;height:70px;border-radius:50%;background:linear-gradient(180deg,#ff6a90,#ff3b6b);display:flex;align-items:center;justify-content:center;color:white;font-weight:900;font-size:22px}
canvas#confetti{position:fixed;inset:0;pointer-events:none;z-index:25}

  </style>
</head>
<body>
  <div class="card" role="main">
    <div class="hearts" aria-hidden>
      <div class="heart"></div>
    </div><div class="photo-heart">
  <img src="yourphoto.jpg" alt="Kavitha" />
</div>

<h1>Hey <span class="name">Kavitha</span> —</h1>
<p class="lead">There are a thousand little reasons I smile every day. Today I want to tell you the biggest one: <strong>I love you</strong>.</p>

<div class="message">
  <p style="margin:0 0 8px 0;font-size:16px">From silly jokes to quiet hugs, you make everything brighter. Will you be my girlfriend? 💖</p>
  <div style="display:flex;gap:10px;justify-content:center;margin-top:14px">
    <button class="btn" id="yesBtn">Yes — I love you too</button>
    <button class="small" id="noBtn">Surprise me later</button>
  </div>
</div>

<footer>Made with ❤️ — a little website for Kavitha</footer>

  </div><canvas id="confetti"></canvas>

  <div class="overlay" id="overlay" role="dialog" aria-modal="true">
    <div class="popup">
      <div class="ring"><div class="inner">💍</div></div>
      <h2 style="margin:6px 0 8px 0">It's a yes!</h2>
      <p style="margin:0 0 14px 0">Kavitha, I promise to hold your hand through all of it — laughs, adventures, and lazy Sundays.</p>
      <div style="display:flex;gap:10px;justify-content:center;margin-top:12px">
        <button class="btn" id="closePopup">Celebrate 🎉</button>
        <button class="small" id="downloadBtn">Download page</button>
      </div>
    </div>
  </div>  <script>
    const canvas = document.getElementById('confetti');
    const ctx = canvas.getContext('2d');
    let W = canvas.width = innerWidth;
    let H = canvas.height = innerHeight;
    window.addEventListener('resize', ()=>{W=canvas.width=innerWidth;H=canvas.height=innerHeight});

    function rand(min,max){return Math.random()*(max-min)+min}
    function makeConfetti(count=120){
      const pieces = [];
      for(let i=0;i<count;i++){
        pieces.push({x:rand(0,W),y:rand(-H,0),vx:rand(-2,2),vy:rand(2,6),w:rand(6,12),h:rand(8,18),rot:rand(0,360),vr:rand(-6,6),color:`hsl(${rand(330,360)},80%,60%)`} );
      }
      return pieces;
    }
    let confetti = [];
    function startConfetti(){confetti = makeConfetti(180); requestAnimationFrame(loop)}
    function loop(){ctx.clearRect(0,0,W,H); for(let p of confetti){p.x+=p.vx;p.y+=p.vy;p.rot+=p.vr;ctx.save();ctx.translate(p.x,p.y);ctx.rotate(p.rot*Math.PI/180);ctx.fillStyle=p.color;ctx.fillRect(-p.w/2,-p.h/2,p.w,p.h);ctx.restore(); if(p.y>H+40)p.y=-20; } if(confetti.length) raf = requestAnimationFrame(loop)}

    document.getElementById('yesBtn').addEventListener('click',()=>{
      document.getElementById('overlay').classList.add('show');
      startConfetti();
    });
    document.getElementById('closePopup').addEventListener('click',()=>{
      confetti = [];
      document.getElementById('overlay').classList.remove('show');
      ctx.clearRect(0,0,W,H);
    });
    document.getElementById('noBtn').addEventListener('click',()=>{
      const card = document.querySelector('.card');
      card.animate([{transform:'translateX(0)'},{transform:'translateX(-8px)'},{transform:'translateX(8px)'},{transform:'translateX(0)'}],{duration:420});
    });

    document.getElementById('downloadBtn').addEventListener('click',()=>{
      const html = '<!doctype html>\n' + document.documentElement.outerHTML;
      const blob = new Blob([html],{type:'text/html'});
      const a = document.createElement('a');
      a.href = URL.createObjectURL(blob);
      a.download = 'proposal_kavitha.html';
      document.body.appendChild(a);a.click();a.remove();
    });
  </script></body>
</html>
