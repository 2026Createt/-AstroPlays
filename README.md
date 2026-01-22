<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<title>ASTROPLAYS</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

<style>
/* ===== BASIC RESET ===== */
* { margin:0; padding:0; box-sizing:border-box; font-family: 'Segoe UI', Roboto, Arial, sans-serif; }
body { color:#e5e7eb; overflow-x:hidden; scroll-behavior:smooth; background:#0b0c17; }

/* ===== CANVAS BACKGROUND ===== */
#spaceCanvas, #nebulaCanvas {
  position: fixed; top:0; left:0; width:100%; height:100%; z-index:-2;
}
#spaceCanvas { background: linear-gradient(160deg, #0b0c17, #05060b); }
#nebulaCanvas { z-index:-1; }

/* ===== TOPBAR ===== */
.topbar {
  display:flex; justify-content:space-between; align-items:center;
  padding:16px 40px; position:fixed; width:100%; top:0;
  background:rgba(11,12,23,0.75); backdrop-filter:blur(8px); z-index:10;
}
.brand-nav { display:flex; align-items:center; gap:28px; }
.brand { font-size:2rem; font-weight:900; letter-spacing:3px; color:#7aa2ff; cursor:pointer; }
.nav-links a {
  color:#e5e7eb; text-decoration:none; font-weight:600; margin-left:20px;
  position:relative; transition:0.3s;
}
.nav-links a::after {
  content:""; position:absolute; left:0; bottom:-4px; width:0; height:2px; background:#7aa2ff; transition:0.3s;
}
.nav-links a:hover::after, .nav-links a.active::after { width:100%; }
.nav-links a:hover, .nav-links a.active { color:#7aa2ff; }

/* RIGHT BUTTONS */
.right-buttons { display:flex; gap:14px; align-items:center; }
.btn {
  padding:8px 18px; border-radius:8px; text-decoration:none; font-weight:600; font-size:0.9rem; color:white; transition:0.3s;
}
.btn.login { background:#5865F2; } .btn.login:hover { background:#4752c4; }
.btn.server { background:#22c55e; } .btn.server:hover { background:#16a34a; }

/* ===== HERO ===== */
.hero {
  display:flex; flex-direction:column; justify-content:center; align-items:center;
  text-align:center; padding:160px 20px 80px; min-height:100vh; position:relative; z-index:2;
}
.hero h1 { font-size:4rem; font-weight:900; color:#7aa2ff; text-shadow:0 0 20px rgba(122,162,255,0.5); }
.hero p { margin-top:14px; font-size:1.2rem; color:#94a3b8; max-width:700px; line-height:1.5; }

/* ===== SECTIONS ===== */
section { max-width:1200px; margin:80px auto; padding:0 40px; position:relative; z-index:2; }

/* SECTION TITLES */
section h2 {
  font-size:2rem; font-weight:700; color:#7aa2ff; margin-bottom:24px; text-align:center;
}

/* ===== GRID CARDS ===== */
.grid {
  display:grid; grid-template-columns:repeat(auto-fit,minmax(260px,1fr)); gap:24px;
}
.card {
  background: rgba(255,255,255,0.03); border:1px solid rgba(255,255,255,0.06); border-radius:12px;
  padding:22px; transition:0.4s, box-shadow 0.5s, transform 0.5s; cursor:pointer; backdrop-filter:blur(6px);
  transform-style: preserve-3d;
  will-change: transform, box-shadow;
}
.card:hover {
  transform:translateY(-8px) rotateX(2deg) rotateY(2deg);
  box-shadow:0 12px 35px rgba(122,162,255,0.35);
  border-color: rgba(122,162,255,0.5);
}
.card h3 { margin-bottom:12px; color:#7aa2ff; font-size:1.2rem; }
.card ul { padding-left:16px; }
.card li { margin-bottom:6px; font-size:0.9rem; color:#cbd5f5; }

/* GLOW ON SCROLL */
.card.scroll-glow { box-shadow:0 12px 45px rgba(122,162,255,0.45); transform:translateY(-6px) rotateX(1deg) rotateY(1deg); }

/* COMING */
.coming {
  text-align:center; padding:12px; border-radius:8px; background:rgba(122,162,255,0.1);
  font-weight:600; font-size:0.9rem; color:#a5b4fc;
}

/* ===== FOOTER ===== */
footer {
  text-align:center; padding:24px; color:#64748b; font-size:0.85rem; position:relative; z-index:2;
}

/* ===== RESPONSIVE ===== */
@media(max-width:768px){
  .hero h1 { font-size:3rem; }
  .nav-links { display:none; }
  .topbar { padding:12px 20px; }
}
</style>
</head>

<body>

<canvas id="spaceCanvas"></canvas>
<canvas id="nebulaCanvas"></canvas>

<!-- TOPBAR -->
<div class="topbar">
  <div class="brand-nav">
    <div class="brand">ASTROPLAYS</div>
    <div class="nav-links">
      <a href="#infos">Infos</a>
      <a href="#dashboard">Dashboard</a>
      <a href="#links">Links</a>
    </div>
  </div>
  <div class="right-buttons">
    <a href="#" class="btn login">Login</a>
    <a href="https://discord.gg/9FwvXmRF3H" target="_blank" class="btn server">Discord</a>
  </div>
</div>

<!-- HERO -->
<div class="hero">
  <h1>ASTROPLAYS</h1>
  <p>Play, Manage, Level Up – das ultimative Discord-Bot Dashboard für alle Server, modular und individuell anpassbar.</p>
</div>

<!-- INFOS SECTION -->
<section id="infos">
  <h2>Funktionen & Module</h2>
  <div class="grid">
    <div class="card">
      <h3>Core Features</h3>
      <ul>
        <li>Modulares System</li>
        <li>Server-spezifische Konfiguration</li>
        <li>Skalierbar & stabil</li>
      </ul>
    </div>
    <div class="card">
      <h3>Aktive Module</h3>
      <ul>
        <li>AstroBoost</li>
        <li>AstroGreeting</li>
        <li>AstroModeration</li>
        <li>AstroModlogs</li>
        <li>AstroShield</li>
      </ul>
    </div>
    <div class="card">
      <h3>In Entwicklung</h3>
      <ul>
        <li>AstroRoles</li>
        <li>AstroTickets</li>
        <li>AstroSupport</li>
        <li>AstroLogs</li>
      </ul>
    </div>
  </div>
</section>

<!-- DASHBOARD SECTION -->
<section id="dashboard">
  <h2>Dashboard</h2>
  <div class="card"><div class="coming">Coming Soon</div></div>
</section>

<!-- LINKS SECTION -->
<section id="links">
  <h2>Links</h2>
  <div class="grid">
    <div class="card">
      <ul>
        <li><a href="https://discord.gg/9FwvXmRF3H" target="_blank" style="color:#22c55e; text-decoration:none;">Join Discord</a></li>
        <li><a href="#" style="color:#5865F2; text-decoration:none;">Login (Demo)</a></li>
      </ul>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>© ASTROPLAYS – Play, Manage, Level Up.</footer>

<script>
// NAV ACTIVE LINK
$(".nav-links a").click(function(e){
  e.preventDefault();
  let target = $(this).attr("href");
  $("html, body").animate({scrollTop: $(target).offset().top - 90}, 500);
});
$(window).scroll(function(){
  let scrollPos = $(document).scrollTop();
  $(".nav-links a").each(function(){
    let currLink = $(this);
    let refElem = $(currLink.attr("href"));
    if(refElem.position().top - 100 <= scrollPos && refElem.position().top + refElem.height() > scrollPos){
      $(".nav-links a").removeClass("active");
      currLink.addClass("active");
    }
  });
});

// STARFIELD BACKGROUND
const canvas=document.getElementById("spaceCanvas");
const ctx=canvas.getContext("2d");
let w=canvas.width=window.innerWidth;
let h=canvas.height=window.innerHeight;
let stars=[];
for(let i=0;i<500;i++){ 
  stars.push({x:Math.random()*w, y:Math.random()*h, z:Math.random()*2+0.5, r:Math.random()*1.2+0.2});
}
function drawStars(){
  ctx.clearRect(0,0,w,h);
  for(let s of stars){
    s.x -= 0.3*s.z;
    if(s.x<0){ s.x=w; s.y=Math.random()*h; }
    ctx.beginPath(); ctx.arc(s.x,s.y,s.r,0,Math.PI*2);
    ctx.fillStyle="rgba(255,255,255,0.8)"; ctx.fill();
  }
  requestAnimationFrame(drawStars);
}
drawStars();

// NEBULA LAYER
const nebula=document.getElementById("nebulaCanvas");
const nctx=nebula.getContext("2d");
function drawNebula(){
  nctx.clearRect(0,0,w,h);
  let gradient=nctx.createRadialGradient(w*0.3,h*0.3,0,w*0.3,h*0.3,w*0.6);
  gradient.addColorStop(0,'rgba(122,162,255,0.08)');
  gradient.addColorStop(0.5,'rgba(122,162,255,0.02)');
  gradient.addColorStop(1,'rgba(0,0,0,0)');
  nctx.fillStyle=gradient;
  nctx.fillRect(0,0,w,h);
  requestAnimationFrame(drawNebula);
}
drawNebula();

// CARD SCROLL GLOW
function scrollGlow(){
  $('.card').each(function(){
    let top = $(this).offset().top;
    let bottom = top + $(this).outerHeight();
    let scroll = $(window).scrollTop();
    let windowHeight = $(window).height();
    if(scroll + windowHeight > top + 50 && scroll < bottom){
      $(this).addClass('scroll-glow');
    } else { $(this).removeClass('scroll-glow'); }
  });
}
$(window).on('scroll resize', scrollGlow);
scrollGlow();

// RESIZE
$(window).resize(function(){ w=canvas.width=nebula.width=window.innerWidth; h=canvas.height=nebula.height=window.innerHeight; });
</script>

</body>
</html>
