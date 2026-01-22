<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<title>AstroPlays ©</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

<style>
* { margin:0; padding:0; box-sizing:border-box; font-family:Arial, Helvetica, sans-serif; }
body { margin:0; overflow-x:hidden; color:#e5e7eb; scroll-behavior:smooth; }

/* CANVAS FULLSCREEN */
#spaceCanvas, #nebulaCanvas {
  position: fixed; top:0; left:0; width:100%; height:100%; z-index:-2;
}
#spaceCanvas{ background: linear-gradient(135deg, #0f172a, #020617); }
#nebulaCanvas{ z-index:-1; }

/* TOP BAR */
.topbar {
  display:flex; justify-content:space-between; align-items:center;
  padding:14px 22px; border-bottom:1px solid rgba(255,255,255,0.08);
  position:fixed; width:100%; background:rgba(15,23,42,0.7); backdrop-filter:blur(6px); z-index:3;
}
.brand{ font-size:1.8rem; font-weight:bold; cursor:pointer; }
.nav-links { display:flex; gap:18px; align-items:center; }
.nav-links a{ color:#e5e7eb; text-decoration:none; font-weight:500; transition:0.2s; padding:4px 6px; border-radius:4px; }
.nav-links a:hover{ color:#7aa2ff; background:rgba(122,162,255,0.1); }
.nav-links a.active{ color:#7aa2ff; background:rgba(122,162,255,0.2); }
.lang{ cursor:pointer; font-size:0.85rem; color:#94a3b8; transition:0.2s;} .lang:hover{ color:#7aa2ff; }
.btn{ padding:6px 14px; border-radius:6px; text-decoration:none; font-weight:bold; font-size:0.85rem; color:white; transition:0.2s; }
.btn.login{ background:#5865F2; } .btn.login:hover{ background:#4752c4; }
.btn.server{ background:#22c55e; } .btn.server:hover{ background:#16a34a; }

/* HERO */
.hero{ padding:120px 22px 40px; max-width:1200px; margin:auto; position:relative; z-index:2; text-align:center; }
.hero h1{ font-size:3rem; text-shadow:0 0 20px rgba(122,162,255,0.7);}
.hero p{ color:#94a3b8; margin-top:12px; font-size:1.1rem; text-shadow:0 0 5px rgba(0,0,0,0.2); }

/* SECTIONS */
section{ max-width:1200px; margin:60px auto 0; padding:0 22px; position:relative; z-index:2; }

/* GRID CARDS */
.grid{ display:grid; grid-template-columns:repeat(auto-fit,minmax(240px,1fr)); gap:14px; }
.card{ background: rgba(255,255,255,0.03); border:1px solid rgba(255,255,255,0.06); border-radius:10px; padding:16px; transition:0.2s; }
.card:hover{ border-color: rgba(122,162,255,0.6); box-shadow:0 0 10px rgba(122,162,255,0.3); transform:translateY(-2px);}
.card h3{ margin-bottom:8px; color:#7aa2ff; font-size:1.05rem;}
.card ul{ padding-left:18px; }
.card li{ margin-bottom:6px; font-size:0.9rem; color:#cbd5f5;}

/* COMING */
.coming{ text-align:center; padding:12px; border-radius:8px; background:rgba(122,162,255,0.1); font-weight:bold; font-size:0.9rem; color:#a5b4fc; }

/* FOOTER */
footer{ text-align:center; padding:22px; color:#64748b; font-size:0.85rem; position:relative; z-index:2; }
</style>
</head>
<body>

<canvas id="spaceCanvas"></canvas>
<canvas id="nebulaCanvas"></canvas>

<div class="topbar">
  <div class="brand" id="brand">AstroPlays ©</div>
  <div class="nav-links">
    <a href="#infos">Infos</a>
    <a href="#dashboard">Dashboard</a>
    <a href="#links">Links</a>
    <div class="lang" id="langBtn">EN</div>
    <a href="#" class="btn login" id="loginBtn">Login</a>
    <a href="https://discord.gg/9FwvXmRF3H" target="_blank" class="btn server">Discord</a>
  </div>
</div>

<div class="hero" id="hero">
  <h1 id="headline">AstroPlays</h1>
  <p id="subline">Ein modularer Discord Bot für moderne Communities.</p>
</div>

<section id="infos">
  <h2 style="color:#7aa2ff; margin-bottom:16px;">Core Features</h2>
  <div class="grid">
    <div class="card" id="coreCard">
      <h3 id="coreTitle">Core Features</h3>
      <ul id="coreList">
        <li>Modulares System</li>
        <li>Server-spezifische Konfiguration</li>
        <li>Skalierbar & stabil</li>
      </ul>
    </div>
    <div class="card" id="activeCard">
      <h3 id="activeTitle">Aktive Module</h3>
      <ul>
        <li>AstroBoost</li>
        <li>AstroGreeting</li>
        <li>AstroModeration</li>
        <li>AstroModlogs</li>
        <li>AstroShield</li>
      </ul>
    </div>
    <div class="card" id="devCard">
      <h3 id="devTitle">In Entwicklung</h3>
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
  <h2 style="color:#7aa2ff; margin-bottom:16px;">Dashboard</h2>
  <div class="card">
    <div class="coming" id="comingText">Coming Soon</div>
  </div>
</section>

<section id="links">
  <h2 style="color:#7aa2ff; margin-bottom:16px;">Links</h2>
  <div class="card">
    <ul>
      <li><a href="https://discord.gg/9FwvXmRF3H" target="_blank" style="color:#22c55e; text-decoration:none;">Join Discord</a></li>
      <li><a href="#" style="color:#5865F2; text-decoration:none;">Login (Demo)</a></li>
    </ul>
  </div>
</section>

<footer>© AstroPlays – Play, Manage, Level Up.</footer>

<script>
// LANGUAGE SWITCH
let lang="de";
$("#langBtn").click(function(){
  lang = lang==="de"?"en":"de";
  $("#langBtn").text(lang==="de"?"EN":"DE");
  if(lang==="en"){
    $("#headline").text("AstroPlays");
    $("#subline").text("A modular Discord bot for modern communities.");
    $("#coreTitle").text("Core Features");
    $("#coreList").html("<li>Modular system</li><li>Per-server configuration</li><li>Scalable & stable</li>");
    $("#activeTitle").text("Active Modules");
    $("#devTitle").text("In Development");
    $("#comingText").text("Coming Soon");
  }else{
    $("#headline").text("AstroPlays");
    $("#subline").text("Ein modularer Discord Bot für moderne Communities.");
    $("#coreTitle").text("Core Features");
    $("#coreList").html("<li>Modulares System</li><li>Server-spezifische Konfiguration</li><li>Skalierbar & stabil</li>");
    $("#activeTitle").text("Aktive Module");
    $("#devTitle").text("In Entwicklung");
    $("#comingText").text("Coming Soon");
  }
});

// SCROLL SMOOTH & ACTIVE LINK
$(".nav-links a").click(function(e){
  e.preventDefault();
  let target = $(this).attr("href");
  $("html, body").animate({scrollTop: $(target).offset().top - 80}, 600);
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

// STARFIELD CANVAS
const canvas=document.getElementById("spaceCanvas");
const ctx=canvas.getContext("2d");
let w=canvas.width=window.innerWidth;
let h=canvas.height=window.innerHeight;
let stars=[];
for(let i=0;i<300;i++){ stars.push({x:Math.random()*w, y:Math.random()*h, z:Math.random()*1.5+0.5, r:Math.random()*1.2+0.2}); }
function drawStars(){
  ctx.clearRect(0,0,w,h);
  for(let s of stars){
    s.x -= s.z;
    if(s.x<0){ s.x=w; s.y=Math.random()*h; s.z=Math.random()*1.5+0.5;}
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
  nctx.clearRect(0,0,nebula.width,nebula.height);
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
