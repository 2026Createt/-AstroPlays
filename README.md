
<html lang="de">
<head>
<meta charset="UTF-8">
<title>ASTROPLAYS</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Segoe UI',Roboto,Arial,sans-serif}
body{color:#e5e7eb;overflow-x:hidden;background:#0b0c17;scroll-behavior:smooth}

/* CANVAS */
#spaceCanvas,#nebulaCanvas{
  position:fixed;top:0;left:0;width:100%;height:100%;z-index:-2
}
#spaceCanvas{background:linear-gradient(160deg,#0b0c17,#05060b)}
#nebulaCanvas{z-index:-1}

/* TOPBAR */
.topbar{
  display:flex;justify-content:space-between;align-items:center;
  padding:16px 40px;position:fixed;width:100%;top:0;
  background:rgba(11,12,23,.75);backdrop-filter:blur(8px);z-index:10
}
.brand{font-size:2rem;font-weight:900;letter-spacing:3px;color:#7aa2ff}
.nav-links a{
  color:#e5e7eb;text-decoration:none;font-weight:600;margin-left:20px;
  position:relative
}
.nav-links a::after{
  content:"";position:absolute;left:0;bottom:-4px;width:0;height:2px;
  background:#7aa2ff;transition:.3s
}
.nav-links a:hover::after,.nav-links a.active::after{width:100%}
.nav-links a:hover{color:#7aa2ff}

/* HERO */
.hero{
  min-height:100vh;padding:160px 20px 80px;
  display:flex;flex-direction:column;align-items:center;
  text-align:center;position:relative;z-index:2
}
.hero h1{
  font-size:4rem;font-weight:900;color:#7aa2ff;
  text-shadow:0 0 25px rgba(122,162,255,.6)
}
.hero p{
  margin-top:14px;font-size:1.2rem;color:#94a3b8;
  max-width:700px
}
.hero-buttons{
  margin-top:32px;display:flex;gap:16px;flex-wrap:wrap;justify-content:center
}

/* BUTTONS */
.btn{
  padding:10px 22px;border-radius:10px;
  text-decoration:none;font-weight:700;font-size:.95rem;
  color:#fff;transition:.3s
}
.btn.login{background:#5865F2}
.btn.login:hover{background:#4752c4}
.btn.server{background:#22c55e}
.btn.server:hover{background:#16a34a}

/* SECTIONS */
section{
  max-width:900px;margin:80px auto;padding:0 24px;
  position:relative;z-index:2
}
section h2{
  font-size:2rem;font-weight:700;color:#7aa2ff;
  margin-bottom:24px;text-align:center
}

/* ACCORDION */
.accordion{display:flex;flex-direction:column;gap:16px}
.accordion-item{
  background:rgba(255,255,255,.03);
  border:1px solid rgba(255,255,255,.08);
  border-radius:14px;overflow:hidden
}
.accordion-header{
  padding:18px 22px;font-weight:700;
  font-size:1.05rem;color:#7aa2ff;
  cursor:pointer;background:rgba(255,255,255,.02)
}
.accordion-header:hover{
  background:rgba(122,162,255,.08)
}
.accordion-content{
  display:none;padding:18px 26px
}
.accordion-content ul{padding-left:18px}
.accordion-content li{
  margin-bottom:8px;color:#cbd5f5;font-size:.95rem
}

/* FOOTER */
footer{
  text-align:center;padding:24px;
  color:#64748b;font-size:.85rem
}

/* RESPONSIVE */
@media(max-width:768px){
  .hero h1{font-size:3rem}
  .nav-links{display:none}
}
</style>
</head>
<body>

<canvas id="spaceCanvas"></canvas>
<canvas id="nebulaCanvas"></canvas>

<!-- TOPBAR -->
<div class="topbar">
  <div class="brand">ASTROPLAYS</div>
  <div class="nav-links">
    <a href="#infos">Infos</a>
  </div>
</div>

<!-- HERO -->
<div class="hero">
  <h1>ASTROPLAYS</h1>
  <p>Play, Manage, Level Up – das ultimative Discord-Bot-System.</p>

  <div class="hero-buttons">
    <a href="#" class="btn login">Login (Demo)</a>
    <a href="https://discord.gg/9FwvXmRF3H" target="_blank" class="btn server">Discord</a>
    <a href="https://2026createt.github.io/Dashboard-AstroBot/" target="_blank" class="btn server">Dashboard</a>
  </div>
</div>

<!-- INFOS -->
<section id="infos">
  <h2>Funktionen & Module</h2>
  <div class="accordion">

    <div class="accordion-item">
      <div class="accordion-header">Aktive Module</div>
      <div class="accordion-content">
        <ul>
          <li>AstroBoost</li>
          <li>AstroGreeting</li>
          <li>AstroModeration</li>
          <li>AstroModlogs</li>
          <li>AstroShield</li>
        </ul>
      </div>
    </div>

    <div class="accordion-item">
      <div class="accordion-header">Core Features</div>
      <div class="accordion-content">
        <ul>
          <li>Modular & skalierbar</li>
          <li>Server-individuelle Einstellungen</li>
          <li>Dashboard-Steuerung</li>
        </ul>
      </div>
    </div>

    <div class="accordion-item">
      <div class="accordion-header">In Entwicklung</div>
      <div class="accordion-content">
        <ul>
          <li>AstroRoles</li>
          <li>AstroTickets</li>
          <li>AstroSupport</li>
          <li>AstroLogs</li>
        </ul>
      </div>
    </div>

  </div>
</section>

<footer>© ASTROPLAYS – Play, Manage, Level Up.</footer>

<script>
// NAV SCROLL
$(".nav-links a").click(function(e){
  e.preventDefault();
  $("html,body").animate({
    scrollTop:$($(this).attr("href")).offset().top-90
  },500);
});

// ACCORDION
$(".accordion-header").click(function(){
  const c=$(this).next();
  $(".accordion-content").not(c).slideUp(250);
  c.slideToggle(250);
});

// STARFIELD
const c=document.getElementById("spaceCanvas"),x=c.getContext("2d");
let w=c.width=innerWidth,h=c.height=innerHeight;
let s=[...Array(500)].map(()=>({x:Math.random()*w,y:Math.random()*h,z:Math.random()*2+0.5}));
(function d(){
  x.clearRect(0,0,w,h);
  s.forEach(a=>{
    a.x-=0.3*a.z;if(a.x<0){a.x=w;a.y=Math.random()*h}
    x.fillStyle="white";x.fillRect(a.x,a.y,1.2,1.2)
  });
  requestAnimationFrame(d)
})();
onresize=()=>{w=c.width=innerWidth;h=c.height=innerHeight};
</script>

</body>
</html>
