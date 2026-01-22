
<html lang="de">
<head>
<meta charset="UTF-8">
<title>AstroPlays ©</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}

body {
  background: linear-gradient(135deg, #0f172a, #020617);
  color: #e5e7eb;
}

/* TOP BAR */
.topbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 14px 22px;
  border-bottom: 1px solid rgba(255,255,255,0.08);
}

.brand {
  font-size: 1.3rem;
  font-weight: bold;
}

.actions {
  display: flex;
  gap: 10px;
  align-items: center;
}

.lang {
  cursor: pointer;
  font-size: 0.85rem;
  color: #94a3b8;
}

/* BUTTONS */
.btn {
  padding: 8px 16px;
  border-radius: 6px;
  text-decoration: none;
  font-weight: bold;
  font-size: 0.85rem;
  color: white;
  transition: 0.2s;
}

.btn.login {
  background: #5865F2;
}
.btn.login:hover {
  background: #4752c4;
}

.btn.server {
  background: #22c55e;
}
.btn.server:hover {
  background: #16a34a;
}

/* HERO */
.hero {
  padding: 32px 22px 18px;
  max-width: 1200px;
  margin: auto;
}

.hero h1 {
  font-size: 2.1rem;
}

.hero p {
  color: #94a3b8;
  margin-top: 6px;
  font-size: 0.95rem;
}

/* GRID */
.grid {
  max-width: 1200px;
  margin: 18px auto 0;
  padding: 0 22px;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 14px;
}

/* CARD */
.card {
  background: rgba(255,255,255,0.03);
  border: 1px solid rgba(255,255,255,0.06);
  border-radius: 10px;
  padding: 14px;
  transition: 0.2s;
}

.card:hover {
  border-color: rgba(122,162,255,0.6);
  box-shadow: 0 0 0 1px rgba(122,162,255,0.3);
  transform: translateY(-2px);
}

.card h3 {
  margin-bottom: 8px;
  color: #7aa2ff;
  font-size: 1rem;
}

.card ul {
  padding-left: 18px;
}

.card li {
  margin-bottom: 6px;
  font-size: 0.88rem;
  color: #cbd5f5;
}

/* COMING */
.coming {
  text-align: center;
  padding: 12px;
  border-radius: 8px;
  background: rgba(122,162,255,0.1);
  font-weight: bold;
  font-size: 0.9rem;
  color: #a5b4fc;
}

/* FOOTER */
footer {
  text-align: center;
  padding: 18px;
  color: #64748b;
  font-size: 0.8rem;
}
</style>
</head>

<body>

<!-- TOP BAR -->
<div class="topbar">
  <div class="brand">AstroPlays ©</div>

  <div class="actions">
    <div class="lang" onclick="toggleLang()" id="langBtn">EN</div>
    <a href="#" class="btn login" id="loginBtn">Login</a>
    <a href="https://discord.gg/9FwvXmRF3H" target="_blank" class="btn server" id="serverBtn">
      Discord
    </a>
  </div>
</div>

<!-- HERO -->
<div class="hero">
  <h1 id="headline">Play. Manage. Level Up.</h1>
  <p id="subline">Ein modularer Discord Bot für moderne Communities.</p>
</div>

<!-- GRID -->
<div class="grid">

  <div class="card">
    <h3 id="coreTitle">Core Features</h3>
    <ul id="coreList">
      <li>Modulares System</li>
      <li>Server-spezifische Konfiguration</li>
      <li>Skalierbar & stabil</li>
    </ul>
  </div>

  <div class="card">
    <h3 id="activeTitle">Aktive Module</h3>
    <ul>
      <li>AstroBoost</li>
      <li>AstroGreeting</li>
      <li>AstroModeration</li>
      <li>AstroModlogs</li>
      <li>AstroShield</li>
    </ul>
  </div>

  <div class="card">
    <h3 id="devTitle">In Entwicklung</h3>
    <ul>
      <li>AstroRoles</li>
      <li>AstroTickets</li>
      <li>AstroSupport</li>
      <li>AstroLogs</li>
    </ul>
  </div>

  <div class="card">
    <h3>Dashboard</h3>
    <div class="coming" id="comingText">Coming Soon</div>
  </div>

</div>

<footer>
  © AstroPlays – Play, Manage, Level Up.
</footer>

<script>
let lang = "de";

function toggleLang() {
  lang = lang === "de" ? "en" : "de";
  document.getElementById("langBtn").innerText = lang === "de" ? "EN" : "DE";

  if (lang === "en") {
    document.getElementById("headline").innerText = "Play. Manage. Level Up.";
    document.getElementById("subline").innerText = "A modular Discord bot for modern communities.";
    document.getElementById("coreTitle").innerText = "Core Features";
    document.getElementById("coreList").innerHTML = `
      <li>Modular system</li>
      <li>Per-server configuration</li>
      <li>Scalable & stable</li>
    `;
    document.getElementById("activeTitle").innerText = "Active Modules";
    document.getElementById("devTitle").innerText = "In Development";
    document.getElementById("comingText").innerText = "Coming Soon";
  } else {
    document.getElementById("headline").innerText = "Play. Manage. Level Up.";
    document.getElementById("subline").innerText = "Ein modularer Discord Bot für moderne Communities.";
    document.getElementById("coreTitle").innerText = "Core Features";
    document.getElementById("coreList").innerHTML = `
      <li>Modulares System</li>
      <li>Server-spezifische Konfiguration</li>
      <li>Skalierbar & stabil</li>
    `;
    document.getElementById("activeTitle").innerText = "Aktive Module";
    document.getElementById("devTitle").innerText = "In Entwicklung";
    document.getElementById("comingText").innerText = "Coming Soon";
  }
}
</script>

</body>
</html>
