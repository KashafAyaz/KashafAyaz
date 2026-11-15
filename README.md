<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Kashaf Ayaz · Interactive README</title>
<style>
  :root {
    --bg: #1c1220;
    --bg-2: #2a1a30;
    --card: #271a2d;
    --stroke: #43294b;
    --text: #fbeef2;
    --muted: #c9aebb;
    --accent: #f28cb1;
    --accent-2: #ffb3cf;
    --ok: #9fe0b8;
    --code-bg: #150c19;
    --radius: 16px;
  }
  :root[data-theme="light"] {
    --bg: #fff5f8;
    --bg-2: #ffe8ef;
    --card: #ffffff;
    --stroke: #f3c9d8;
    --text: #3a1f2d;
    --muted: #8a6575;
    --accent: #d6527f;
    --accent-2: #b53a65;
    --ok: #2f7a4b;
    --code-bg: #2a1a30;
  }
  * { box-sizing: border-box; }
  html { scroll-behavior: smooth; }
  body {
    margin: 0;
    background: var(--bg);
    color: var(--text);
    font-family: system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
    line-height: 1.6;
    transition: background .3s, color .3s;
  }
  a { color: var(--accent-2); text-decoration: none; }
  a:hover { text-decoration: underline; }
  .mono { font-family: ui-monospace, "Fira Code", Menlo, Consolas, monospace; }

  /* top nav */
  nav {
    position: sticky; top: 0; z-index: 10;
    display: flex; align-items: center; gap: 6px;
    padding: 10px 20px;
    background: color-mix(in srgb, var(--bg) 88%, transparent);
    backdrop-filter: blur(8px);
    border-bottom: 1px solid var(--stroke);
    overflow-x: auto;
  }
  nav .brand { font-weight: 700; margin-right: auto; white-space: nowrap; }
  nav a.link {
    color: var(--muted); padding: 6px 12px; border-radius: 999px;
    font-size: 14px; white-space: nowrap;
  }
  nav a.link:hover, nav a.link.active { background: var(--stroke); color: var(--text); text-decoration: none; }
  #themeBtn {
    background: var(--stroke); color: var(--text); border: 0; border-radius: 999px;
    padding: 6px 12px; cursor: pointer; font-size: 14px;
  }

  /* hero */
  header.hero {
    text-align: center;
    padding: 90px 20px 70px;
    background:
      radial-gradient(900px 300px at 50% 0%, color-mix(in srgb, var(--accent) 35%, transparent), transparent 70%),
      var(--bg);
  }
  .hero h1 { font-size: clamp(36px, 7vw, 64px); margin: 0 0 6px; letter-spacing: -1px; }
  .hero .sub { color: var(--muted); font-size: clamp(16px, 2.4vw, 22px); margin: 0 0 18px; }
  .typing {
    font-size: clamp(18px, 3vw, 26px); font-weight: 600; color: var(--accent);
    min-height: 40px;
  }
  .caret { display: inline-block; width: 2px; height: 1.1em; background: var(--accent); margin-left: 3px; vertical-align: text-bottom; animation: blink 1s steps(1) infinite; }
  @keyframes blink { 50% { opacity: 0; } }
  .badges { display: flex; flex-wrap: wrap; gap: 10px; justify-content: center; margin-top: 26px; }
  .badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: var(--card); border: 1px solid var(--stroke);
    padding: 8px 16px; border-radius: 10px; font-weight: 600; font-size: 14px;
    color: var(--text); transition: transform .15s, border-color .15s;
  }
  .badge:hover { transform: translateY(-2px); border-color: var(--accent); text-decoration: none; }

  main { max-width: 920px; margin: 0 auto; padding: 0 20px 80px; }
  section { padding-top: 56px; }
  h2 { font-size: 28px; margin: 0 0 6px; }
  h2 span.tag { color: var(--accent); font-weight: 400; margin-right: 6px; }
  .lead { color: var(--muted); margin: 0 0 22px; }

  .card {
    background: var(--card); border: 1px solid var(--stroke);
    border-radius: var(--radius); padding: 22px;
  }

  /* about */
  .about-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 14px; }
  .fact { display: flex; gap: 14px; align-items: flex-start; }
  .fact .ico { font-size: 28px; }
  .fact h3 { margin: 0; font-size: 16px; }
  .fact p { margin: 2px 0 0; color: var(--muted); font-size: 14px; }

  details.card { margin-top: 14px; }
  summary { cursor: pointer; font-weight: 700; list-style: none; display: flex; align-items: center; gap: 10px; }
  summary::-webkit-details-marker { display: none; }
  summary::before { content: "▸"; color: var(--accent); transition: transform .2s; }
  details[open] summary::before { transform: rotate(90deg); }
  details ul { margin: 12px 0 0; padding-left: 22px; color: var(--muted); }

  /* tools */
  .chips { display: flex; flex-wrap: wrap; gap: 10px; }
  .chip {
    background: var(--card); border: 1px solid var(--stroke); color: var(--text);
    padding: 10px 18px; border-radius: 10px; cursor: pointer; font-weight: 700; font-size: 15px;
    font-family: inherit; transition: all .15s;
  }
  .chip:hover { border-color: var(--accent); }
  .chip.active { background: var(--accent); color: #fff; border-color: var(--accent); }
  #toolInfo { margin-top: 14px; min-height: 64px; }
  #toolInfo b { color: var(--accent-2); }

  /* repos */
  .repos { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 14px; }
  a.repo {
    display: block; color: var(--text); background: var(--card);
    border: 1px solid var(--stroke); border-radius: var(--radius); padding: 20px;
    transition: transform .15s, border-color .15s;
  }
  a.repo:hover { transform: translateY(-3px); border-color: var(--accent); text-decoration: none; }
  a.repo h3 { margin: 0 0 4px; font-size: 17px; }
  a.repo p { margin: 0 0 14px; color: var(--muted); font-size: 14px; }
  .lang { display: inline-flex; align-items: center; gap: 6px; font-size: 13px; color: var(--muted); }
  .dot { width: 10px; height: 10px; border-radius: 50%; display: inline-block; }

  /* connect */
  .connect { text-align: center; }
  .connect .badges { margin-top: 18px; }
  footer { text-align: center; color: var(--muted); padding: 30px 20px 50px; border-top: 1px solid var(--stroke); }
  .paw { display: inline-block; cursor: pointer; user-select: none; transition: transform .2s; }
  .paw:active { transform: scale(1.5) rotate(-12deg); }

  #toast {
    position: fixed; bottom: 24px; left: 50%; transform: translateX(-50%) translateY(20px);
    background: var(--accent); color: #fff; padding: 10px 18px; border-radius: 10px;
    opacity: 0; pointer-events: none; transition: all .25s; font-size: 14px; z-index: 20;
  }
  #toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }

  .reveal { opacity: 0; transform: translateY(18px); transition: opacity .6s, transform .6s; }
  .reveal.in { opacity: 1; transform: none; }
  @media (prefers-reduced-motion: reduce) {
    .reveal { opacity: 1; transform: none; transition: none; }
    .caret { animation: none; }
    html { scroll-behavior: auto; }
  }
</style>
</head>
<body>

<nav>
  <span class="brand mono">~/kashaf</span>
  <a class="link" href="#about">About</a>
  <a class="link" href="#tools">Tools</a>
  <a class="link" href="#projects">Projects</a>
  <a class="link" href="#connect">Connect</a>
  <button id="themeBtn" aria-label="Toggle theme">🌙 / ☀️</button>
</nav>

<header class="hero">
  <h1>Hi, I'm Kashaf</h1>
  <p class="sub">CIS student at NED University</p>
  <div class="typing mono"><span id="typed"></span><span class="caret"></span></div>
  <div class="badges">
    <a class="badge" href="https://github.com/KashafAyaz?tab=repositories" target="_blank" rel="noopener">💻 Learning C</a>
    <a class="badge" href="https://code.visualstudio.com/" target="_blank" rel="noopener">📝 VS Code</a>
    <a class="badge" href="https://www.linkedin.com/in/kashaf-ayaz-157821422" target="_blank" rel="noopener">🔗 LinkedIn</a>
  </div>
</header>

<main>

  <section id="about" class="reveal">
    <h2><span class="tag mono">01.</span>About me</h2>
    <p class="lead">A quick intro, one program at a time.</p>
    <div class="about-grid">
      <div class="card fact"><div class="ico">🎓</div><div><h3>Student</h3><p>CIS student at NED University</p></div></div>
      <div class="card fact"><div class="ico">💻</div><div><h3>Currently learning</h3><p>C programming</p></div></div>
      <div class="card fact"><div class="ico">📘</div><div><h3>My approach</h3><p>Building my skills one program at a time</p></div></div>
    </div>
    <details class="card">
      <summary>Click to see what I'm working on</summary>
      <ul>
        <li>Practicing C basics: loops, arrays, functions</li>
        <li>Getting comfortable with Git and GitHub</li>
        <li>Goal: build a small project in C</li>
      </ul>
    </details>
  </section>

  <section id="tools" class="reveal">
    <h2><span class="tag mono">02.</span>My tools</h2>
    <p class="lead">Tap a tool to see how I use it.</p>
    <div class="chips" id="chips"></div>
    <div class="card" id="toolInfo"></div>
  </section>

  <section id="projects" class="reveal">
    <h2><span class="tag mono">03.</span>Projects</h2>
    <p class="lead">Pinned on my GitHub.</p>
    <div class="repos">
      <a class="repo" href="https://github.com/KashafAyaz/C-LEARNING" target="_blank" rel="noopener">
        <h3 class="mono">📁 C-LEARNING</h3>
        <p>My C practice repo: programs I write while learning.</p>
        <span class="lang"><span class="dot" style="background:#f28cb1"></span>C</span>
      </a>
      <a class="repo" href="https://github.com/Iamfaizan-prog/blood-bank-manager" target="_blank" rel="noopener">
        <h3 class="mono">📁 blood-bank-manager</h3>
        <p>A project pinned on my profile (hosted under Iamfaizan-prog).</p>
        <span class="lang"><span class="dot" style="background:#c7a6ff"></span>CSS</span>
      </a>
      <a class="repo" href="https://github.com/KashafAyaz/KashafAyaz" target="_blank" rel="noopener">
        <h3 class="mono">📁 KashafAyaz</h3>
        <p>My profile README repo, where this all started.</p>
        <span class="lang"><span class="dot" style="background:#fbeef2"></span>Markdown</span>
      </a>
    </div>
  </section>

  <section id="connect" class="reveal connect">
    <h2><span class="tag mono">04.</span>Let's connect</h2>
    <p class="lead">Always happy to chat about code, C, or Git.</p>
    <div class="badges">
      <a class="badge" href="https://www.linkedin.com/in/kashaf-ayaz-157821422" target="_blank" rel="noopener">🔗 LinkedIn · Kashaf Ayaz</a>
      <a class="badge" href="https://github.com/KashafAyaz" target="_blank" rel="noopener">🐙 GitHub · KashafAyaz</a>
    </div>
  </section>

</main>

<footer>
  Thanks for stopping by <span class="paw" id="paw" title="Click me!">🐾</span>
</footer>

<div id="toast"></div>

<script>
(function () {
  var $ = function (s) { return document.querySelector(s); };

  function toast(msg) {
    var t = $('#toast'); t.textContent = msg; t.classList.add('show');
    clearTimeout(toast._t); toast._t = setTimeout(function () { t.classList.remove('show'); }, 1800);
  }

  /* ---------- theme ---------- */
  var root = document.documentElement;
  try { var saved = localStorage.getItem('kashaf-theme'); if (saved) root.setAttribute('data-theme', saved); } catch (e) {}
  $('#themeBtn').addEventListener('click', function () {
    var next = root.getAttribute('data-theme') === 'light' ? 'dark' : 'light';
    root.setAttribute('data-theme', next);
    try { localStorage.setItem('kashaf-theme', next); } catch (e) {}
  });

  /* ---------- typing effect ---------- */
  var lines = ['Learning C programming', 'One program at a time', 'Always building something new'];
  var li = 0, ci = 0, del = false, typed = $('#typed');
  var reduce = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  function tick() {
    var line = lines[li];
    if (reduce) { typed.textContent = line; li = (li + 1) % lines.length; return setTimeout(tick, 2500); }
    if (!del) {
      ci++; typed.textContent = line.slice(0, ci);
      if (ci === line.length) { del = true; return setTimeout(tick, 1400); }
      return setTimeout(tick, 70);
    }
    ci--; typed.textContent = line.slice(0, ci);
    if (ci === 0) { del = false; li = (li + 1) % lines.length; return setTimeout(tick, 350); }
    setTimeout(tick, 35);
  }
  tick();

  /* ---------- reveal on scroll ---------- */
  var io = new IntersectionObserver(function (es) {
    es.forEach(function (e) { if (e.isIntersecting) { e.target.classList.add('in'); io.unobserve(e.target); } });
  }, { threshold: 0.08 });
  document.querySelectorAll('.reveal').forEach(function (el) { io.observe(el); });

  /* ---------- active nav link ---------- */
  var links = document.querySelectorAll('nav a.link');
  var spy = new IntersectionObserver(function (es) {
    es.forEach(function (e) {
      if (e.isIntersecting) {
        links.forEach(function (a) { a.classList.toggle('active', a.getAttribute('href') === '#' + e.target.id); });
      }
    });
  }, { rootMargin: '-40% 0px -55% 0px' });
  document.querySelectorAll('main section').forEach(function (s) { spy.observe(s); });

  /* ---------- tools ---------- */
  var tools = {
    'C': 'My main language right now. I use it to practice <b>loops, arrays and functions</b> and to learn how programs really work.',
    'Git': 'Version control. I\'m getting comfortable with <b>commits, branches and history</b> so I never lose my work.',
    'GitHub': 'Where my code lives. My practice programs are in <b>C-LEARNING</b>, and this page is my profile README.',
    'VS Code': 'My editor for writing and running programs, with syntax highlighting and an integrated terminal.'
  };
  var chips = $('#chips'), info = $('#toolInfo');
  Object.keys(tools).forEach(function (name, i) {
    var b = document.createElement('button'); b.className = 'chip'; b.textContent = name;
    b.addEventListener('click', function () {
      chips.querySelectorAll('.chip').forEach(function (c) { c.classList.remove('active'); });
      b.classList.add('active');
      info.innerHTML = '<b>' + name + '</b><br>' + tools[name];
    });
    chips.appendChild(b);
    if (i === 0) b.click();
  });

  /* ---------- paw easter egg ---------- */
  var pawCount = 0;
  $('#paw').addEventListener('click', function () {
    pawCount++;
    toast(pawCount < 5 ? '🐾 Meow!' : '🐾 You found the secret paw (' + pawCount + ' clicks)');
  });
})();
</script>
</body>
</html>
