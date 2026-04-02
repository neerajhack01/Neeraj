<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Neeraj Sai Kumar | Cybersecurity Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Rajdhani:wght@300;400;500;600;700&family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg:       #050a0e;
    --bg2:      #0a1520;
    --bg3:      #0d1f2d;
    --green:    #00ff9d;
    --cyan:     #00cfff;
    --red:      #ff3c5a;
    --yellow:   #ffd700;
    --text:     #c8dce8;
    --muted:    #4a6a80;
    --border:   rgba(0,255,157,0.15);
    --glow:     0 0 20px rgba(0,255,157,0.25);
    --glow-c:   0 0 20px rgba(0,207,255,0.25);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Rajdhani', sans-serif;
    font-size: 16px;
    line-height: 1.7;
    overflow-x: hidden;
    cursor: none;
  }

  /* \u2500\u2500 Custom Cursor \u2500\u2500 */
  .cursor {
    width: 12px; height: 12px;
    border-radius: 50%;
    background: var(--green);
    position: fixed; pointer-events: none;
    z-index: 9999;
    transform: translate(-50%,-50%);
    transition: transform .1s;
    box-shadow: 0 0 10px var(--green);
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1px solid var(--green);
    border-radius: 50%;
    position: fixed; pointer-events: none;
    z-index: 9998;
    transform: translate(-50%,-50%);
    transition: transform .15s, width .2s, height .2s;
    opacity: 0.5;
  }

  /* \u2500\u2500 Scanline Overlay \u2500\u2500 */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.03) 2px,
      rgba(0,0,0,0.03) 4px
    );
    pointer-events: none;
    z-index: 1000;
  }

  /* \u2500\u2500 Matrix Canvas \u2500\u2500 */
  #matrix-canvas {
    position: fixed; top: 0; left: 0;
    width: 100%; height: 100%;
    opacity: 0.04;
    pointer-events: none;
    z-index: 0;
  }

  /* \u2500\u2500 Navbar \u2500\u2500 */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 500;
    display: flex; align-items: center; justify-content: space-between;
    padding: 1rem 3rem;
    background: rgba(5,10,14,0.85);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
  }
  .nav-logo {
    font-family: 'Orbitron', monospace;
    font-size: 1.1rem;
    color: var(--green);
    letter-spacing: 3px;
    text-decoration: none;
  }
  .nav-links { display: flex; gap: 2rem; list-style: none; }
  .nav-links a {
    font-family: 'Share Tech Mono', monospace;
    font-size: .82rem;
    color: var(--muted);
    text-decoration: none;
    letter-spacing: 2px;
    text-transform: uppercase;
    transition: color .3s;
  }
  .nav-links a:hover { color: var(--green); text-shadow: 0 0 8px var(--green); }

  /* \u2500\u2500 Hero \u2500\u2500 */
  #hero {
    position: relative; z-index: 1;
    min-height: 100vh;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    text-align: center;
    padding: 2rem;
  }
  .hero-tag {
    font-family: 'Share Tech Mono', monospace;
    font-size: .78rem;
    color: var(--green);
    letter-spacing: 4px;
    margin-bottom: 1.2rem;
    opacity: 0;
    animation: fadeUp .6s .3s forwards;
  }
  .hero-name {
    font-family: 'Orbitron', monospace;
    font-size: clamp(2.5rem, 7vw, 5rem);
    font-weight: 900;
    line-height: 1;
    color: #fff;
    text-shadow: 0 0 40px rgba(0,255,157,0.3);
    opacity: 0;
    animation: fadeUp .7s .5s forwards;
  }
  .hero-name span { color: var(--green); }
  .hero-title {
    font-family: 'Share Tech Mono', monospace;
    font-size: clamp(.9rem, 2.5vw, 1.2rem);
    color: var(--cyan);
    margin-top: 1rem;
    letter-spacing: 2px;
    opacity: 0;
    animation: fadeUp .7s .7s forwards;
  }
  .hero-desc {
    max-width: 680px;
    margin: 1.5rem auto 0;
    font-size: 1.05rem;
    color: var(--muted);
    opacity: 0;
    animation: fadeUp .7s .9s forwards;
  }
  .hero-btns {
    display: flex; gap: 1rem; flex-wrap: wrap;
    justify-content: center;
    margin-top: 2.5rem;
    opacity: 0;
    animation: fadeUp .7s 1.1s forwards;
  }
  .btn {
    display: inline-block;
    padding: .7rem 1.8rem;
    font-family: 'Share Tech Mono', monospace;
    font-size: .85rem;
    letter-spacing: 2px;
    text-transform: uppercase;
    text-decoration: none;
    border-radius: 3px;
    transition: all .3s;
    cursor: none;
  }
  .btn-primary {
    background: var(--green);
    color: #050a0e;
    box-shadow: 0 0 20px rgba(0,255,157,0.35);
  }
  .btn-primary:hover {
    box-shadow: 0 0 35px rgba(0,255,157,0.6);
    transform: translateY(-2px);
  }
  .btn-outline {
    border: 1px solid var(--cyan);
    color: var(--cyan);
  }
  .btn-outline:hover {
    background: rgba(0,207,255,0.1);
    box-shadow: 0 0 20px rgba(0,207,255,0.3);
    transform: translateY(-2px);
  }
  .hero-stats {
    display: flex; gap: 3rem; flex-wrap: wrap;
    justify-content: center;
    margin-top: 3rem;
    opacity: 0;
    animation: fadeUp .7s 1.3s forwards;
  }
  .stat { text-align: center; }
  .stat-num {
    font-family: 'Orbitron', monospace;
    font-size: 1.8rem;
    color: var(--green);
    display: block;
  }
  .stat-label {
    font-family: 'Share Tech Mono', monospace;
    font-size: .72rem;
    color: var(--muted);
    letter-spacing: 2px;
    text-transform: uppercase;
  }
  .scroll-hint {
    position: absolute; bottom: 2rem;
    font-family: 'Share Tech Mono', monospace;
    font-size: .72rem;
    color: var(--muted);
    letter-spacing: 3px;
    animation: blink 2s infinite;
  }

  /* \u2500\u2500 Section Base \u2500\u2500 */
  section {
    position: relative; z-index: 1;
    padding: 6rem 2rem;
    max-width: 1100px;
    margin: 0 auto;
  }
  .section-header {
    display: flex; align-items: center; gap: 1rem;
    margin-bottom: 3rem;
  }
  .section-num {
    font-family: 'Share Tech Mono', monospace;
    font-size: .78rem;
    color: var(--green);
    letter-spacing: 3px;
  }
  .section-title {
    font-family: 'Orbitron', monospace;
    font-size: clamp(1.4rem, 3vw, 2rem);
    font-weight: 700;
    color: #fff;
    letter-spacing: 2px;
  }
  .section-line {
    flex: 1;
    height: 1px;
    background: linear-gradient(to right, var(--border), transparent);
  }

  /* \u2500\u2500 About \u2500\u2500 */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 3rem;
    align-items: start;
  }
  .terminal-box {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 6px;
    overflow: hidden;
    box-shadow: var(--glow);
  }
  .terminal-bar {
    background: var(--bg3);
    padding: .55rem 1rem;
    display: flex; align-items: center; gap: .5rem;
    border-bottom: 1px solid var(--border);
  }
  .dot { width: 10px; height: 10px; border-radius: 50%; }
  .dot-r { background: var(--red); }
  .dot-y { background: var(--yellow); }
  .dot-g { background: var(--green); }
  .terminal-title {
    font-family: 'Share Tech Mono', monospace;
    font-size: .72rem;
    color: var(--muted);
    margin-left: .5rem;
    letter-spacing: 2px;
  }
  .terminal-body {
    padding: 1.5rem;
    font-family: 'Share Tech Mono', monospace;
    font-size: .83rem;
    line-height: 1.9;
  }
  .t-prompt { color: var(--green); }
  .t-cmd    { color: var(--cyan); }
  .t-val    { color: #fff; }
  .t-comment{ color: var(--muted); }
  .about-right { display: flex; flex-direction: column; gap: 1.5rem; }
  .info-card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-left: 3px solid var(--green);
    border-radius: 4px;
    padding: 1.2rem 1.5rem;
    transition: transform .3s, box-shadow .3s;
  }
  .info-card:hover {
    transform: translateX(6px);
    box-shadow: var(--glow);
  }
  .info-card h4 {
    font-family: 'Orbitron', monospace;
    font-size: .78rem;
    color: var(--green);
    letter-spacing: 3px;
    margin-bottom: .4rem;
  }
  .info-card p { color: var(--text); font-size: .95rem; }

  /* \u2500\u2500 Skills \u2500\u2500 */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
  }
  .skill-category {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 1.5rem;
    transition: box-shadow .3s;
  }
  .skill-category:hover { box-shadow: var(--glow); }
  .skill-cat-title {
    font-family: 'Orbitron', monospace;
    font-size: .8rem;
    letter-spacing: 2px;
    margin-bottom: 1rem;
    display: flex; align-items: center; gap: .6rem;
  }
  .cat-icon { font-size: 1rem; }
  .skill-tags { display: flex; flex-wrap: wrap; gap: .5rem; }
  .tag {
    padding: .3rem .8rem;
    border-radius: 3px;
    font-family: 'Share Tech Mono', monospace;
    font-size: .75rem;
    letter-spacing: 1px;
    border: 1px solid;
    transition: all .25s;
  }
  .tag-green  { color: var(--green);  border-color: rgba(0,255,157,0.3);  background: rgba(0,255,157,0.05); }
  .tag-cyan   { color: var(--cyan);   border-color: rgba(0,207,255,0.3);  background: rgba(0,207,255,0.05); }
  .tag-red    { color: var(--red);    border-color: rgba(255,60,90,0.3);   background: rgba(255,60,90,0.05); }
  .tag-yellow { color: var(--yellow); border-color: rgba(255,215,0,0.3);  background: rgba(255,215,0,0.05); }
  .tag:hover  { transform: translateY(-2px); filter: brightness(1.3); }

  /* \u2500\u2500 Projects \u2500\u2500 */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
    gap: 1.5rem;
  }
  .project-card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 1.6rem;
    position: relative;
    overflow: hidden;
    transition: transform .3s, box-shadow .3s;
    text-decoration: none;
    display: block;
    color: inherit;
  }
  .project-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(to right, var(--green), var(--cyan));
    transform: scaleX(0);
    transition: transform .3s;
  }
  .project-card:hover { transform: translateY(-6px); box-shadow: var(--glow); }
  .project-card:hover::before { transform: scaleX(1); }
  .project-type {
    font-family: 'Share Tech Mono', monospace;
    font-size: .7rem;
    letter-spacing: 3px;
    text-transform: uppercase;
    margin-bottom: .6rem;
  }
  .project-card h3 {
    font-family: 'Orbitron', monospace;
    font-size: 1rem;
    color: #fff;
    margin-bottom: .8rem;
    font-weight: 700;
  }
  .project-card p { font-size: .92rem; color: var(--muted); line-height: 1.6; margin-bottom: 1rem; }
  .project-tools { display: flex; flex-wrap: wrap; gap: .4rem; margin-top: auto; }
  .project-link-icon {
    position: absolute; top: 1.2rem; right: 1.2rem;
    font-size: 1rem;
    color: var(--muted);
    transition: color .3s;
  }
  .project-card:hover .project-link-icon { color: var(--green); }

  /* \u2500\u2500 Certifications \u2500\u2500 */
  .certs-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 1.2rem;
  }
  .cert-card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 1.4rem;
    display: flex; align-items: flex-start; gap: 1rem;
    transition: transform .3s, box-shadow .3s;
    text-decoration: none;
    color: inherit;
  }
  .cert-card:hover { transform: translateY(-4px); box-shadow: var(--glow); }
  .cert-icon {
    width: 44px; height: 44px;
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 1.3rem;
    flex-shrink: 0;
  }
  .cert-icon-green { background: rgba(0,255,157,0.1); border: 1px solid rgba(0,255,157,0.3); }
  .cert-icon-cyan  { background: rgba(0,207,255,0.1); border: 1px solid rgba(0,207,255,0.3); }
  .cert-icon-red   { background: rgba(255,60,90,0.1);  border: 1px solid rgba(255,60,90,0.3); }
  .cert-icon-yellow{ background: rgba(255,215,0,0.1);  border: 1px solid rgba(255,215,0,0.3); }
  .cert-info h4 {
    font-family: 'Rajdhani', sans-serif;
    font-size: 1rem;
    font-weight: 600;
    color: #fff;
    line-height: 1.3;
    margin-bottom: .3rem;
  }
  .cert-issuer {
    font-family: 'Share Tech Mono', monospace;
    font-size: .72rem;
    color: var(--green);
    letter-spacing: 1px;
  }
  .cert-date {
    font-size: .8rem;
    color: var(--muted);
    margin-top: .2rem;
  }
  .cert-view {
    font-family: 'Share Tech Mono', monospace;
    font-size: .68rem;
    color: var(--cyan);
    letter-spacing: 1px;
    margin-top: .4rem;
    display: flex; align-items: center; gap: .3rem;
  }

  /* \u2500\u2500 Experience \u2500\u2500 */
  .timeline { position: relative; padding-left: 2rem; }
  .timeline::before {
    content: '';
    position: absolute; left: 0; top: 0; bottom: 0;
    width: 1px;
    background: linear-gradient(to bottom, var(--green), transparent);
  }
  .timeline-item {
    position: relative;
    margin-bottom: 2.5rem;
    padding-left: 1.5rem;
  }
  .timeline-item::before {
    content: '';
    position: absolute; left: -2.4rem; top: .4rem;
    width: 8px; height: 8px;
    border-radius: 50%;
    background: var(--green);
    box-shadow: 0 0 10px var(--green);
  }
  .timeline-date {
    font-family: 'Share Tech Mono', monospace;
    font-size: .75rem;
    color: var(--green);
    letter-spacing: 2px;
    margin-bottom: .4rem;
  }
  .timeline-role {
    font-family: 'Orbitron', monospace;
    font-size: 1.05rem;
    color: #fff;
    margin-bottom: .2rem;
  }
  .timeline-company {
    font-size: .9rem;
    color: var(--cyan);
    margin-bottom: .8rem;
  }
  .timeline-bullets { list-style: none; }
  .timeline-bullets li {
    font-size: .93rem;
    color: var(--text);
    padding-left: 1.2rem;
    position: relative;
    margin-bottom: .4rem;
  }
  .timeline-bullets li::before {
    content: '\u25b8';
    position: absolute; left: 0;
    color: var(--green);
  }

  /* \u2500\u2500 Contact \u2500\u2500 */
  .contact-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 3rem;
    align-items: start;
  }
  .contact-links { display: flex; flex-direction: column; gap: 1rem; }
  .contact-link {
    display: flex; align-items: center; gap: 1rem;
    padding: 1rem 1.2rem;
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 5px;
    text-decoration: none;
    color: var(--text);
    transition: all .3s;
  }
  .contact-link:hover {
    border-color: var(--green);
    transform: translateX(6px);
    box-shadow: var(--glow);
  }
  .contact-link-icon { font-size: 1.2rem; width: 24px; text-align: center; }
  .contact-link-text { font-family: 'Share Tech Mono', monospace; font-size: .82rem; letter-spacing: 1px; }
  .contact-link:hover .contact-link-text { color: var(--green); }

  /* \u2500\u2500 Footer \u2500\u2500 */
  footer {
    position: relative; z-index: 1;
    border-top: 1px solid var(--border);
    padding: 2rem;
    text-align: center;
    font-family: 'Share Tech Mono', monospace;
    font-size: .78rem;
    color: var(--muted);
    letter-spacing: 2px;
  }
  footer span { color: var(--green); }

  /* \u2500\u2500 Animations \u2500\u2500 */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  @keyframes blink {
    0%, 100% { opacity: 1; }
    50%       { opacity: 0; }
  }
  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity .7s, transform .7s;
  }
  .reveal.visible { opacity: 1; transform: none; }

  /* \u2500\u2500 Responsive \u2500\u2500 */
  @media (max-width: 768px) {
    nav { padding: 1rem 1.5rem; }
    .nav-links { display: none; }
    .about-grid, .contact-grid { grid-template-columns: 1fr; }
    section { padding: 4rem 1.2rem; }
  }
</style>
</head>
<body>

<!-- Custom Cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursor-ring"></div>

<!-- Matrix Background -->
<canvas id="matrix-canvas"></canvas>

<!-- Navbar -->
<nav>
  <a class="nav-logo" href="#">NSK_SEC</a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#certs">Certs</a></li>
    <li><a href="#experience">Experience</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- \u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550 HERO \u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550 -->
<section id="hero" style="max-width:100%; padding: 0 2rem;">
  <p class="hero-tag">// INITIALIZING SECURE PROFILE...</p>
  <h1 class="hero-name">Neeraj <span>Sai Kumar</span></h1>
  <p class="hero-title">VAPT Engineer &nbsp;|&nbsp; SOC Analyst &nbsp;|&nbsp; Cloud Security</p>
  <p class="hero-desc">
    Offensive security specialist with expertise in Vulnerability Assessment &amp; Penetration Testing,
    SOC operations, and multi-cloud security. Breaking systems ethically to make them stronger.
  </p>
  <div class="hero-btns">
    <a class="btn btn-primary" href="#projects">View Projects</a>
    <a class="btn btn-outline" href="#contact">Contact Me</a>
    <a class="btn btn-outline" href="./resume/Siripurapu_NeerajSaiKumar_Resume.pdf" target="_blank">Download CV</a>
  </div>
  <div class="hero-stats">
    <div class="stat"><span class="stat-num">3+</span><span class="stat-label">Projects</span></div>
    <div class="stat"><span class="stat-num">4+</span><span class="stat-label">Certifications</span></div>
    <div class="stat"><span class="stat-num">30%</span><span class="stat-label">Risk Reduction</span></div>
    <div class="stat"><span class="stat-num">35%</span><span class="stat-label">Threat Detection \u2191</span></div>
  </div>
  <p class="scroll-hint">\u25bc SCROLL TO EXPLORE</p>
</section>

<!-- \u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550 ABOUT \u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550\u2550 -->
<section id="about">
  <div class="section-header reveal">
    <span class="section-num">01 //</span>
    <h2 class="section-title">ABOUT</h2>
    <div class="section-line"></div>
  </div>
  <div class="about-grid reveal">
    <div class="terminal-box">
      <div class="terminal-bar">
        <div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div>
        <span class="terminal-title">neeraj@kali:~$ whoami</span>
      </div>
      <div class="terminal-body">
        <p><span class="t-prompt">\u250c\u2500\u2500(</span><span class="t-cmd">neeraj</span><span class="t-prompt">\u327fkali)-[~]</span></p>
        <p><span class="t-prompt">\u2514\u2500$ </span><span class="t-cmd">cat profile.json</span></p>
        <br>
        <p><span class="t-prompt">{</span></p>
        <p>&nbsp;&nbsp;<span class="t-cmd">"name"</span>: <span class="t-val">"Siripurapu Neeraj Sai Kumar"</span>,</p>
        <p>&nbsp;&nbsp;<span class="t-cmd">"role"</span>: <span class="t-val">"Cybersecurity Engineer"</span>,</p>
        <p>&nbsp;&nbsp;<span class="t-cmd">"education"</span>: <span class="t-val">"B.Tech, SIMATS"</span>,</p>
        <p>&nbsp;&nbsp;<span class="t-cmd">"location"</span>: <span class="t-val">"Hyderabad, India"</span>,</p>
        <p>&nbsp;&nbsp;<span class="t-cmd">"specialization"</span>: [</p>
        <p>&nbsp;
