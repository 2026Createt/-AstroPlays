<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<title>AstroPlays ©</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
/* RESET */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}

/* BACKGROUND */
body {
  color: #fff;
  min-height: 100vh;
  background: radial-gradient(circle at bottom, #1b2735 0%, #090a0f 100%);
  overflow-x: hidden;
  scroll-behavior: smooth;
}

/* STARFIELD */
.stars, .stars2, .stars3 {
  position: fixed;
  width: 1px;
  height: 1px;
  background: transparent;
  box-shadow: 1000px 2000px white;
  animation: animStars 50s linear infinite;
  z-index: -1;
}
.stars2 {
  width: 2px;
  height: 2px;
  animation-duration: 100s;
  opacity: 0.6;
}
.stars3 {
  width: 3px;
  height: 3px;
  animation-duration: 150s;
  opacity: 0.3;
}

@keyframes animStars {
  from { transform: translateY(0); }
  to { transform: translateY(-2000px); }
}

/* HEADER */
header {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 20px;
}

h1 {
  font-size: 3.4rem;
  text-shadow: 0 0 15px #7aa2ff;
}

.subtitle {
  color: #9db5ff;
  font-size: 1.3rem;
  margin: 15px 0 40px;
}

/* BUTTONS */
.buttons {
  display: flex;
  gap: 15px;
  flex-wrap: wrap;
  justify-content: center;
}

.btn {
  padding: 14px 30px;
  border-radius: 10px;
  text-decoration: none;
  font-weight: bold;
  color: #fff;
  transition: 0.25s;
  box-shadow: 0 0 15px rgba(0,0,0,0.5);
}

.btn.login {
  background: #5865F2;
}
.btn.login:hover {
  box-shadow: 0 0 20px #5865F2;
}

.btn.server {
  background: #2ecc71;
}
.btn.server:hover {
  box-shadow: 0 0 20px #2ecc71;
}

/* GEAR MENU */
.gear {
  position: fixed;
  top: 20px;
  right: 20px;
  font-size: 28px;
  cursor: pointer;
  z-index: 10;
}

.menu {
  position: fixed;
  top: 60px;
  right: 20px;
  background: rgba(15, 25, 50, 0.95);
  border-radius: 12px;
  padding: 15px;
  display: none;
  width: 230px;
  z-index: 10;
}

.menu a {
  display: block;
  color: #fff;
  text-decoration: none;
  padding: 8px 0;
  border-bottom: 1px solid rgba(255,255,255,0.1);
}
.menu a:last-child { border-bottom: none; }
.menu a:hover { color: #7aa2ff; }

/* SECTIONS */
section {
  max-width: 900px;
  margin: auto;
  padding: 90px 20px;
}

h2 {
  color: #7aa2ff;
  margin-bottom: 20px;
  text-shadow: 0 0 10px rgba(122,162,255,0.4);
}

ul {
  padding-left: 20px;
}
li {
  margin-bottom: 10px;
}

/* COMING SOON */
.coming {
  text-align: center;
  padding: 60px 20px;
  border: 1px dashed rgba(122,162,255,0.4);
  border-radius: 15px;
  box-shadow: 0 0 20px rgba(122,162,255,0.1);
}

.coming span {
  font-size: 1.5rem;
  color: #9db5ff;
}

/* LANGUAGE SWITCH */
.lang {
  position: fixed;
  bottom: 20px;
  right: 20px;
  cursor: pointer;
  background: rgba(20,30,60,0.9);
  padding: 10px 15px;
  border-radius: 10px;
  font-weight: bold;
}

/* FOOTER */
footer {
  text-align: center;
  padding: 40px;
  color: #aaa;
  font-size: 0.9rem;
}
</style>
</head>

<body>

<div class="stars"></div>
<div class="stars2"></div>
<div class="stars3"></div>

<div class="gear" onclick="toggleMenu()">⚙️</div>

<div class="menu" id="menu">
  <a href="#about">Über</a>
  <a href="#features">Features</a>
  <a href="#modules">Module</a>
  <a href="#dashboard">Dashboard</a>
</div>

<div class="lang" onclick="toggleLang()">DE / EN</div>

<header>
  <h1>AstroPlays ©</h1>
  <div class="subtitle" id="subtitle">Play, Manage, Level Up.</div>

  <div class="buttons">
    <a href="#" class="btn login">Mit Discord anmelden</a>
    <a href="https://discord.gg/9FwvXmRF3H" target="_blank" class="btn server">
      Discord beitreten
    </a>
  </div>
</header>

<section id="about">
  <h2>Über AstroPlays</h2>
  <ul>
    <li>Modularer Discord Bot</li>
    <li>Individuelle Server-Einstellungen</li>
    <li>Skalierbar & leistungsstark</li>
  </ul>
</section>

<section id="features">
  <h2>Core Features</h2>
  <ul>
    <li>Automatisierung & Moderation</li>
    <li>Hohe Anpassbarkeit</li>
    <li>Dashboard-ready Architektur</li>
  </ul>
</section>

<section id="modules">
  <h2>Module</h2>
  <ul>
    <li>AstroBoost</li>
    <li>AstroGreeting</li>
    <li>AstroModeration</li>
    <li>AstroModlogs</li>
    <li>AstroShield</li>
  </ul>
</section>

<section id="dashboard">
  <div class="coming">
    <span>🚧 Dashboard – Coming Soon 🚧</span>
  </div>
</section>

<footer>
  © AstroPlays – Play, Manage, Level Up.
</footer>

<script>
function toggleMenu() {
  const m = document.getElementById("menu");
  m.style.display = m.style.display === "block" ? "none" : "block";
}

let lang = "de";
function toggleLang() {
  lang = lang === "de" ? "en" : "de";
  document.getElementById("subtitle").innerText =
    lang === "de" ? "Play, Manage, Level Up." : "Play. Manage. Level up your server.";
}
</script>

</body>
</html>
