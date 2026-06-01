<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>SHARAN // DEV</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Bebas+Neue&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet"/>
<style>
  :root {
    --void: #000000;
    --abyss: #040404;
    --surface: #0a0a0a;
    --panel: #0f0f0f;
    --border: #1a1a1a;
    --muted: #2a2a2a;
    --dim: #444;
    --text: #c8c8c8;
    --bright: #e8e8e8;
    --pure: #ffffff;
    --acid: #00ff88;
    --acid-dim: rgba(0,255,136,0.08);
    --acid-glow: rgba(0,255,136,0.25);
    --red: #ff2244;
    --amber: #ffaa00;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--void);
    color: var(--text);
    font-family: 'Share Tech Mono', monospace;
    font-size: 14px;
    line-height: 1.7;
    overflow-x: hidden;
    cursor: crosshair;
  }

  /* Scanlines overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.18) 2px,
      rgba(0,0,0,0.18) 4px
    );
    pointer-events: none;
    z-index: 9999;
  }

  /* Noise grain */
  body::after {
    content: '';
    position: fixed;
    inset: -50%;
    width: 200%;
    height: 200%;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    opacity: 0.06;
    pointer-events: none;
    z-index: 9998;
    animation: grain 0.4s steps(1) infinite;
  }

  @keyframes grain {
    0%  { transform: translate(0,0); }
    20% { transform: translate(-3%,-4%); }
    40% { transform: translate(3%, 2%); }
    60% { transform: translate(-2%, 5%); }
    80% { transform: translate(4%,-2%); }
   100% { transform: translate(-1%, 3%); }
  }

  /* ──── LAYOUT ──── */
  .wrapper {
    max-width: 860px;
    margin: 0 auto;
    padding: 0 24px 80px;
  }

  /* ──── TOP BAR ──── */
  .topbar {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 18px 0 18px;
    border-bottom: 1px solid var(--border);
    animation: fadeDown 0.6s ease both;
  }
  .topbar-dot { width:10px; height:10px; border-radius:50%; }
  .dot-r { background: var(--red); }
  .dot-a { background: var(--amber); }
  .dot-g { background: var(--acid); }
  .topbar-path {
    margin-left: 12px;
    color: var(--dim);
    font-size: 11px;
    letter-spacing: 0.08em;
  }
  .topbar-path span { color: var(--acid); }

  /* ──── HERO ──── */
  .hero {
    padding: 72px 0 48px;
    position: relative;
    animation: fadeUp 0.8s ease 0.2s both;
  }

  .hero-label {
    font-size: 11px;
    letter-spacing: 0.3em;
    color: var(--acid);
    text-transform: uppercase;
    margin-bottom: 16px;
    opacity: 0.8;
  }

  .hero h1 {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(72px, 14vw, 160px);
    line-height: 0.88;
    color: var(--pure);
    letter-spacing: -0.02em;
    position: relative;
  }

  .hero h1 .glitch {
    position: relative;
    display: inline-block;
  }
  .hero h1 .glitch::before,
  .hero h1 .glitch::after {
    content: attr(data-text);
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 100%;
  }
  .hero h1 .glitch::before {
    color: var(--red);
    clip-path: polygon(0 0, 100% 0, 100% 35%, 0 35%);
    animation: glitch-top 3s infinite steps(1);
    opacity: 0.7;
  }
  .hero h1 .glitch::after {
    color: var(--acid);
    clip-path: polygon(0 65%, 100% 65%, 100% 100%, 0 100%);
    animation: glitch-bot 3s infinite steps(1) 0.3s;
    opacity: 0.5;
  }

  @keyframes glitch-top {
    0%,90%,100% { transform: translate(0,0); opacity:0; }
    91% { transform: translate(-4px, -2px); opacity:0.7; }
    93% { transform: translate(4px, 0); opacity:0.5; }
    95% { transform: translate(-2px, 2px); opacity:0.7; }
  }
  @keyframes glitch-bot {
    0%,85%,100% { transform: translate(0,0); opacity:0; }
    86% { transform: translate(4px, 2px); opacity:0.5; }
    88% { transform: translate(-3px, -1px); opacity:0.6; }
    90% { transform: translate(2px, 0); opacity:0.4; }
  }

  .hero-roles {
    margin-top: 24px;
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }

  .role-tag {
    font-size: 11px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    padding: 5px 14px;
    border: 1px solid var(--border);
    color: var(--dim);
    position: relative;
    overflow: hidden;
    transition: all 0.3s;
  }
  .role-tag::before {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--acid);
    transform: translateX(-100%);
    transition: transform 0.3s;
    z-index: -1;
  }
  .role-tag:hover {
    color: var(--void);
    border-color: var(--acid);
  }
  .role-tag:hover::before { transform: translateX(0); }

  .hero-motto {
    margin-top: 32px;
    padding-left: 16px;
    border-left: 2px solid var(--acid);
    color: var(--dim);
    font-style: italic;
    font-size: 13px;
  }
  .hero-motto strong { color: var(--acid); font-style: normal; }

  /* ──── SECTION ──── */
  section {
    margin-top: 64px;
    animation: fadeUp 0.7s ease both;
  }

  .sec-header {
    display: flex;
    align-items: center;
    gap: 14px;
    margin-bottom: 32px;
  }
  .sec-num {
    font-size: 10px;
    color: var(--acid);
    letter-spacing: 0.2em;
    opacity: 0.6;
  }
  .sec-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 28px;
    letter-spacing: 0.12em;
    color: var(--bright);
  }
  .sec-line {
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, var(--border), transparent);
  }

  /* ──── ABOUT ──── */
  .about-grid {
    display: grid;
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
  }
  .about-item {
    background: var(--abyss);
    padding: 18px 22px;
    display: flex;
    gap: 16px;
    align-items: flex-start;
    transition: background 0.2s;
    position: relative;
  }
  .about-item::before {
    content: '';
    position: absolute;
    left: 0; top: 0; bottom: 0;
    width: 2px;
    background: var(--acid);
    transform: scaleY(0);
    transition: transform 0.25s;
    transform-origin: bottom;
  }
  .about-item:hover { background: var(--surface); }
  .about-item:hover::before { transform: scaleY(1); }
  .about-icon { font-size: 16px; flex-shrink: 0; margin-top: 2px; }
  .about-text { color: var(--text); font-size: 13px; }
  .about-text .hl { color: var(--acid); }

  /* ──── CONNECT ──── */
  .connect-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
  }
  .connect-item {
    background: var(--abyss);
    padding: 20px 16px;
    text-align: center;
    text-decoration: none;
    color: var(--dim);
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    transition: all 0.25s;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
  }
  .connect-icon { font-size: 20px; }
  .connect-item:hover {
    background: var(--acid-dim);
    color: var(--acid);
    border-color: var(--acid);
  }

  /* ──── TECH STACK ──── */
  .stack-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
    gap: 8px;
  }
  .stack-item {
    background: var(--abyss);
    border: 1px solid var(--border);
    padding: 16px 12px;
    text-align: center;
    font-size: 11px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--dim);
    transition: all 0.25s;
    position: relative;
    overflow: hidden;
  }
  .stack-item::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0;
    height: 2px;
    width: 0;
    background: var(--acid);
    transition: width 0.3s;
  }
  .stack-item:hover {
    background: var(--surface);
    color: var(--bright);
    border-color: var(--muted);
  }
  .stack-item:hover::after { width: 100%; }
  .stack-dot {
    display: block;
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--acid);
    margin: 0 auto 10px;
    opacity: 0.5;
    transition: opacity 0.25s;
  }
  .stack-item:hover .stack-dot { opacity: 1; }

  /* ──── PROJECTS ──── */
  .project-list { display: flex; flex-direction: column; gap: 1px; background: var(--border); border: 1px solid var(--border); }

  .project-item {
    background: var(--abyss);
    padding: 24px 22px;
    display: grid;
    grid-template-columns: auto 1fr auto;
    gap: 16px;
    align-items: start;
    transition: background 0.2s;
    position: relative;
    overflow: hidden;
  }
  .project-item::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(90deg, var(--acid-dim), transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }
  .project-item:hover { background: var(--surface); }
  .project-item:hover::before { opacity: 1; }

  .project-id {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 36px;
    color: var(--border);
    line-height: 1;
    width: 44px;
    transition: color 0.3s;
  }
  .project-item:hover .project-id { color: var(--acid); }

  .project-name {
    font-family: 'Space Mono', monospace;
    font-size: 15px;
    font-weight: 700;
    color: var(--bright);
    letter-spacing: 0.05em;
    margin-bottom: 4px;
  }
  .project-desc {
    font-size: 12px;
    color: var(--dim);
    line-height: 1.6;
  }
  .project-arrow {
    font-size: 18px;
    color: var(--border);
    transition: all 0.3s;
    align-self: center;
  }
  .project-item:hover .project-arrow {
    color: var(--acid);
    transform: translateX(4px);
  }

  /* ──── QUOTE ──── */
  .quote-block {
    margin-top: 64px;
    padding: 40px 32px;
    border: 1px solid var(--border);
    background: var(--abyss);
    position: relative;
    text-align: center;
    animation: fadeUp 0.7s ease both;
  }
  .quote-block::before {
    content: '"';
    position: absolute;
    top: -28px; left: 24px;
    font-family: 'Bebas Neue', sans-serif;
    font-size: 100px;
    color: var(--acid);
    opacity: 0.08;
    line-height: 1;
  }
  .quote-text {
    font-family: 'Space Mono', monospace;
    font-size: 16px;
    color: var(--bright);
    line-height: 1.8;
    letter-spacing: 0.02em;
    font-style: italic;
  }
  .quote-text em { color: var(--acid); font-style: normal; }

  /* ──── FOOTER ──── */
  footer {
    margin-top: 64px;
    padding-top: 24px;
    border-top: 1px solid var(--border);
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 11px;
    color: var(--muted);
    animation: fadeUp 0.6s ease 0.4s both;
  }
  .footer-status {
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .pulse-dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: var(--acid);
    animation: pulse 2s infinite;
  }
  @keyframes pulse {
    0%,100% { box-shadow: 0 0 0 0 var(--acid-glow); }
    50%      { box-shadow: 0 0 0 6px transparent; }
  }

  /* ──── ANIMATIONS ──── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeDown {
    from { opacity: 0; transform: translateY(-12px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* staggered sections */
  section:nth-child(2) { animation-delay: 0.1s; }
  section:nth-child(3) { animation-delay: 0.2s; }
  section:nth-child(4) { animation-delay: 0.3s; }
  section:nth-child(5) { animation-delay: 0.4s; }

  /* ──── CURSOR TRAIL (JS driven) ──── */
  .cursor-ring {
    position: fixed;
    width: 32px; height: 32px;
    border: 1px solid var(--acid);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9997;
    transform: translate(-50%, -50%);
    transition: transform 0.06s linear, width 0.2s, height 0.2s, opacity 0.2s;
    mix-blend-mode: screen;
    opacity: 0.6;
  }
</style>
</head>
<body>

<div class="cursor-ring" id="cursor"></div>

<div class="wrapper">

  <!-- TOP BAR -->
  <div class="topbar">
    <div class="topbar-dot dot-r"></div>
    <div class="topbar-dot dot-a"></div>
    <div class="topbar-dot dot-g"></div>
    <div class="topbar-path">~/dev/<span>sharan</span>/README.md</div>
  </div>

  <!-- HERO -->
  <header class="hero">
    <div class="hero-label">// init profile</div>
    <h1>
      <span class="glitch" data-text="SHARAN">SHARAN</span>
    </h1>
    <div class="hero-roles">
      <span class="role-tag">Full-Stack Dev</span>
      <span class="role-tag">AI / ML Explorer</span>
      <span class="role-tag">Digital Experience</span>
      <span class="role-tag">Creative Builder</span>
    </div>
    <p class="hero-motto">
      Building immersive web experiences, intelligent applications,<br>
      and ideas that leave an impact.<br>
      <strong>"Create. Learn. Build. Repeat."</strong>
    </p>
  </header>

  <!-- ABOUT -->
  <section>
    <div class="sec-header">
      <span class="sec-num">01</span>
      <span class="sec-title">About</span>
      <div class="sec-line"></div>
    </div>
    <div class="about-grid">
      <div class="about-item">
        <span class="about-icon">🕷️</span>
        <span class="about-text">Passionate about <span class="hl">Web Development</span>, Artificial Intelligence, and Machine Learning</span>
      </div>
      <div class="about-item">
        <span class="about-icon">🎓</span>
        <span class="about-text"><span class="hl">Computer Science Graduate</span> exploring modern software engineering</span>
      </div>
      <div class="about-item">
        <span class="about-icon">🚀</span>
        <span class="about-text">Building interactive websites, <span class="hl">AI-powered solutions</span>, and creative digital experiences</span>
      </div>
      <div class="about-item">
        <span class="about-icon">🧠</span>
        <span class="about-text">Currently learning <span class="hl">Deep Learning</span>, AI Engineering &amp; Advanced Full-Stack</span>
      </div>
      <div class="about-item">
        <span class="about-icon">🎬</span>
        <span class="about-text">Built <span class="hl">cinematic horror experiences</span>, portfolio platforms &amp; client-focused web apps</span>
      </div>
    </div>
  </section>

  <!-- CONNECT -->
  <section>
    <div class="sec-header">
      <span class="sec-num">02</span>
      <span class="sec-title">Connect</span>
      <div class="sec-line"></div>
    </div>
    <div class="connect-grid">
      <a href="https://sharan-codes.vercel.app" class="connect-item" target="_blank">
        <span class="connect-icon">◈</span>Portfolio
      </a>
      <a href="#" class="connect-item">
        <span class="connect-icon">in</span>LinkedIn
      </a>
      <a href="#" class="connect-item">
        <span class="connect-icon">◻</span>Instagram
      </a>
      <a href="#" class="connect-item">
        <span class="connect-icon">f</span>Facebook
      </a>
      <a href="#" class="connect-item">
        <span class="connect-icon">✕</span>X / Twitter
      </a>
    </div>
  </section>

  <!-- TECH STACK -->
  <section>
    <div class="sec-header">
      <span class="sec-num">03</span>
      <span class="sec-title">Tech Stack</span>
      <div class="sec-line"></div>
    </div>
    <div class="stack-grid">
      <div class="stack-item"><span class="stack-dot"></span>React</div>
      <div class="stack-item"><span class="stack-dot"></span>TypeScript</div>
      <div class="stack-item"><span class="stack-dot"></span>Next.js</div>
      <div class="stack-item"><span class="stack-dot"></span>Tailwind</div>
      <div class="stack-item"><span class="stack-dot"></span>Node.js</div>
      <div class="stack-item"><span class="stack-dot"></span>Python</div>
      <div class="stack-item"><span class="stack-dot"></span>Machine Learning</div>
    </div>
  </section>

  <!-- PROJECTS -->
  <section>
    <div class="sec-header">
      <span class="sec-num">04</span>
      <span class="sec-title">Featured Projects</span>
      <div class="sec-line"></div>
    </div>
    <div class="project-list">
      <div class="project-item">
        <div class="project-id">01</div>
        <div>
          <div class="project-name">ARCHIVE-7</div>
          <div class="project-desc">Analog horror &amp; found-footage web experience — cinematic, immersive, unsettling.</div>
        </div>
        <div class="project-arrow">→</div>
      </div>
      <div class="project-item">
        <div class="project-id">02</div>
        <div>
          <div class="project-name">HORROR FILM WEBSITE</div>
          <div class="project-desc">Interactive client project built for a short film — atmosphere-first design.</div>
        </div>
        <div class="project-arrow">→</div>
      </div>
      <div class="project-item">
        <div class="project-id">03</div>
        <div>
          <div class="project-name">AI &amp; ML PROJECTS</div>
          <div class="project-desc">Intelligent systems, automation pipelines &amp; predictive solutions.</div>
        </div>
        <div class="project-arrow">→</div>
      </div>
    </div>
  </section>

  <!-- QUOTE -->
  <div class="quote-block">
    <p class="quote-text">
      "The best experiences are built where <em>creativity</em> meets <em>technology</em>."
    </p>
  </div>

  <!-- FOOTER -->
  <footer>
    <div class="footer-status">
      <div class="pulse-dot"></div>
      <span>AVAILABLE FOR WORK</span>
    </div>
    <span>SHARAN © 2025</span>
  </footer>

</div>

<script>
  // Cursor ring
  const ring = document.getElementById('cursor');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
  function animCursor() {
    rx += (mx - rx) * 0.15;
    ry += (my - ry) * 0.15;
    ring.style.left = rx + 'px';
    ring.style.top  = ry + 'px';
    requestAnimationFrame(animCursor);
  }
  animCursor();

  // Expand ring on hover
  document.querySelectorAll('a, .about-item, .stack-item, .project-item, .role-tag').forEach(el => {
    el.addEventListener('mouseenter', () => {
      ring.style.width  = '52px';
      ring.style.height = '52px';
      ring.style.opacity = '1';
    });
    el.addEventListener('mouseleave', () => {
      ring.style.width  = '32px';
      ring.style.height = '32px';
      ring.style.opacity = '0.6';
    });
  });

  // Intersection observer for stagger reveal
  const obs = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.style.opacity = '1';
        e.target.style.transform = 'translateY(0)';
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('section, .quote-block, footer').forEach(el => {
    el.style.opacity = '0';
    el.style.transform = 'translateY(24px)';
    el.style.transition = 'opacity 0.6s ease, transform 0.6s ease';
    obs.observe(el);
  });
</script>
</body>
</html>
