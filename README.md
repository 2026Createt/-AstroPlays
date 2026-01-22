<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<title>ASTROPLAYS</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

<style>
* { margin:0; padding:0; box-sizing:border-box; font-family:Arial, Helvetica, sans-serif; }
body { color:#e5e7eb; overflow-x:hidden; scroll-behavior:smooth; }

/* CANVAS BACKGROUND */
#spaceCanvas, #nebulaCanvas {
  position: fixed; top:0; left:0; width:100%; height:100%; z-index:-2;
}
#spaceCanvas{ background: linear-gradient(135deg, #0f172a, #020617); }
#nebulaCanvas{ z-index:-1; }

/* TOPBAR */
.topbar {
  display:flex; justify-content:space-between; align-items:center;
  padding:12px 22px; position:fixed; width:100%; background:rgba(15,23,42,0.7); backdrop-filter:blur(6px); z-index:3;
}
.brand-nav { display:flex; align-items:center; gap:18px; }
.brand{ font-size:2rem; font-weight:bold; letter-spacing:2px; cursor:pointer; }
.nav-links a{ color:#e5e7eb; text-decoration:none; font-weight:500; margin-left:12px; transition:0.2s; }
.nav-links a:hover, .nav-links a.active{ color:#7aa2ff; }

/* RIGHT BUTTONS */
.right-buttons { display:flex; gap:10px; align-items:center; }
.btn{ padding:6px 14px; border-radius:6px; text-decoration:none; font-weight:bold; font-size:0.85rem; color:white; transition:0.2s; }
.btn.login{ background:#5865F2; } .btn.login:hover{ background:#4752c4; }
.btn.server{ background:#22c55e; } .btn.server:hover{ background:#16a34a; }

/* HERO */
.hero{ padding:100px 22px 20px; max-width:1200px; margin:auto; position:relative; z-index:2; text-align:center; }
.hero h1{ font-size:3rem; text-shadow:0 0 20px rgba(122,162,255,0.7);}
.hero p{ color:#94a3b8; margin-top:8px; font-size:1rem; text-shadow:0 0 5px rgba(0,0,0,0.2); }

/* SECTIONS */
section{ max-width:1200px; margin:40px auto 0; padding:0 22px; position:relative; z-index:2; }

/* GRID CARDS */
.grid{ display:grid; grid-template-columns:repeat(auto-fit,minmax(200px,1fr)); gap:12px; }
.card{
  background: rgba(255,255,255,0.03); 
  border:1px solid rgba(255,255,255,0.06); 
  border-radius:10px; 
  padding:14px; 
  transition:0.3s;
  cursor:pointer;
  transform-style: preserve-3d;
}
.card:hover{
  border-color: rgba(122,162,255,0.6); 
  box-shadow:0 0 15px rgba(122,162,255,0.4); 
  transform:translateY(-4px) scale(1.03) rotateX(1deg) rotateY(1deg);
}
.card h3{ margin-bottom:6px; color:#7aa2ff; font-size:1rem;}
.card ul{ padding-left:16px; }
.card li{ margin-bottom:4px; font-size:0.85rem; color:#cbd5f5;}

/* COMING */
.coming{ text-align:center; padding:10px; border-radius:8px; background:rgba(122,162,255,0.1); font-weight:bold; font-size:0.85rem; color:#a5b4fc; }

/* FOOTER */
footer{ text-align:center; padding:16px; color:#64748b; font-size:0.8rem; position:relative; z-index:2; }
</style>
</head>
<body>

<canvas id="spaceCanvas"></canvas>
<canvas id="nebulaCanvas"></canvas>

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

<section id="infos">
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

<section id="dashboard">
  <div class="card">
    <div class="coming">Dashboard Coming Soon</div>
  </div>
</section>

<section id="links">
  <div class="card">
    <ul>
      <li><a href="https://discord.gg/9FwvXmRF3H" target="_blank" style="color:#22c55e; text-decoration:none;">Join Discord</a></li>
      <li><a href="#" style="color:#5865F2; text-decoration:none;">Login (Demo)</a></li>
    </ul>
  </div>
</section>

<footer>© ASTROPLAYS – Play, Manage, Level Up.</footer>

<script>
// ACTIVE LINK + SCROLL
$(".nav-links a").click(function(e){
  e.preventDefault();
  let target = $(this).attr("href");
  $("html, body").animate({scrollTop: $(target).offset().top - 70}, 500);
});
$(window).scroll(function(){
  let scrollPos = $(document).scrollTop();
  $(".nav-links a").each(function(){
    let currLink = $(this);
    let refElem = $(currLink.attr("href"));
    if(refElem.position().top - 80 <= scrollPos && refElem.position().top + refElem.height() > scrollPos){
      $(".nav-links a").removeClass("active");
      currLink.addClass("active");
    }
  });
});

// STARFIELD PARALLAX
const canvas=document.getElementById("spaceCanvas");
const ctx=canvas.getContext("2d");
let w=canvas.width=window.innerWidth;
let h=canvas.height=window.innerHeight;
let stars=[];
for(let i=0;i<400;i++){ 
  stars.push({
    x:Math.random()*w, 
    y:Math.random()*h, 
    z:Math.random()*3+0.5, 
    r:Math.random()*1.2+0.2,
    dx:Math.random()*0.05, dy:Math.random()*0.05
  }); 
}
function drawStars(){
  ctx.clearRect(0,0,w,h);
  for(let s of stars){
    s.x += Math.sin(Date.now()*0.0001)*s.z*0.1;
    s.y += Math.cos(Date.now()*0.0001)*s.z*0.1;
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

$(window).resize(function(){ w=canvas.width=nebula.width=window.innerWidth; h=canvas.height=nebula.height=window.innerHeight; });
</script>

</body>
</html>
