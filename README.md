<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Mina Nabil — Flutter Developer</title>
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=JetBrains+Mono:wght@300;400;500&display=swap" rel="stylesheet" />
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #050810;
    --bg2: #0a0f1e;
    --bg3: #0f1628;
    --accent: #4f8cff;
    --accent2: #00e5ff;
    --accent3: #7c3aed;
    --text: #e8eaf6;
    --text2: #8892b0;
    --text3: #4a5568;
    --border: rgba(79,140,255,0.15);
    --border2: rgba(79,140,255,0.08);
    --glow: 0 0 40px rgba(79,140,255,0.12);
    --font: 'Space Grotesk', sans-serif;
    --mono: 'JetBrains Mono', monospace;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font);
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    position: fixed;
    width: 10px; height: 10px;
    background: var(--accent);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s, opacity 0.2s;
    mix-blend-mode: screen;
  }
  .cursor-ring {
    position: fixed;
    width: 36px; height: 36px;
    border: 1px solid rgba(79,140,255,0.5);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%, -50%);
    transition: transform 0.15s ease, width 0.2s, height 0.2s, opacity 0.2s;
  }

  /* Noise overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1000;
    opacity: 0.4;
  }

  /* Grid background */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(79,140,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(79,140,255,0.03) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none;
    z-index: 0;
  }

  /* Glow orbs */
  .orb {
    position: fixed;
    border-radius: 50%;
    filter: blur(120px);
    pointer-events: none;
    z-index: 0;
    animation: drift 20s ease-in-out infinite;
  }
  .orb1 { width: 600px; height: 600px; background: rgba(79,140,255,0.06); top: -200px; right: -200px; animation-delay: 0s; }
  .orb2 { width: 400px; height: 400px; background: rgba(124,58,237,0.05); bottom: 10%; left: -100px; animation-delay: -7s; }
  .orb3 { width: 300px; height: 300px; background: rgba(0,229,255,0.04); top: 40%; right: 10%; animation-delay: -13s; }

  @keyframes drift {
    0%, 100% { transform: translate(0, 0) scale(1); }
    33% { transform: translate(30px, -20px) scale(1.05); }
    66% { transform: translate(-20px, 30px) scale(0.95); }
  }

  /* NAV */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    padding: 20px 48px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid var(--border2);
    backdrop-filter: blur(20px);
    background: rgba(5,8,16,0.6);
  }
  .nav-logo {
    font-family: var(--mono);
    font-size: 13px;
    color: var(--accent);
    letter-spacing: 0.1em;
  }
  .nav-links { display: flex; gap: 32px; }
  .nav-links a {
    font-size: 13px;
    color: var(--text2);
    text-decoration: none;
    letter-spacing: 0.05em;
    transition: color 0.2s;
    font-family: var(--mono);
  }
  .nav-links a:hover { color: var(--accent); }

  /* STATUS DOT */
  .status-pill {
    display: flex;
    align-items: center;
    gap: 8px;
    font-family: var(--mono);
    font-size: 11px;
    color: var(--text2);
    padding: 6px 14px;
    border: 1px solid var(--border);
    border-radius: 100px;
  }
  .status-dot {
    width: 6px; height: 6px;
    background: #22c55e;
    border-radius: 50%;
    animation: pulse-dot 2s ease-in-out infinite;
  }
  @keyframes pulse-dot {
    0%, 100% { box-shadow: 0 0 0 0 rgba(34,197,94,0.5); }
    50% { box-shadow: 0 0 0 6px rgba(34,197,94,0); }
  }

  /* MAIN */
  main { position: relative; z-index: 1; }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 120px 48px 80px;
    max-width: 1100px;
    margin: 0 auto;
  }

  .hero-tag {
    font-family: var(--mono);
    font-size: 12px;
    color: var(--accent);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 24px;
    opacity: 0;
    animation: fadeUp 0.8s 0.2s forwards;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .hero-tag::before {
    content: '';
    width: 32px; height: 1px;
    background: var(--accent);
  }

  .hero-name {
    font-size: clamp(64px, 10vw, 120px);
    font-weight: 700;
    line-height: 0.9;
    letter-spacing: -0.03em;
    margin-bottom: 8px;
    opacity: 0;
    animation: fadeUp 0.8s 0.35s forwards;
  }
  .hero-name span {
    display: block;
    background: linear-gradient(135deg, #fff 0%, var(--accent) 60%, var(--accent2) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-role {
    font-size: clamp(16px, 2.5vw, 22px);
    color: var(--text2);
    font-weight: 300;
    margin-bottom: 32px;
    opacity: 0;
    animation: fadeUp 0.8s 0.5s forwards;
  }
  .hero-role strong { color: var(--accent); font-weight: 500; }

  .hero-desc {
    font-size: 16px;
    color: var(--text2);
    max-width: 480px;
    line-height: 1.7;
    margin-bottom: 48px;
    opacity: 0;
    animation: fadeUp 0.8s 0.65s forwards;
    border-left: 2px solid var(--accent);
    padding-left: 20px;
  }

  .hero-actions {
    display: flex;
    gap: 16px;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.8s 0.8s forwards;
  }

  .btn-primary {
    padding: 14px 32px;
    background: var(--accent);
    color: var(--bg);
    border: none;
    border-radius: 4px;
    font-family: var(--font);
    font-size: 14px;
    font-weight: 600;
    letter-spacing: 0.05em;
    cursor: none;
    text-decoration: none;
    transition: transform 0.2s, box-shadow 0.2s;
    display: inline-flex;
    align-items: center;
    gap: 8px;
  }
  .btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 12px 40px rgba(79,140,255,0.4);
  }

  .btn-ghost {
    padding: 14px 32px;
    background: transparent;
    color: var(--text);
    border: 1px solid var(--border);
    border-radius: 4px;
    font-family: var(--font);
    font-size: 14px;
    font-weight: 500;
    letter-spacing: 0.05em;
    cursor: none;
    text-decoration: none;
    transition: border-color 0.2s, background 0.2s, transform 0.2s;
    display: inline-flex;
    align-items: center;
    gap: 8px;
  }
  .btn-ghost:hover {
    border-color: var(--accent);
    background: rgba(79,140,255,0.06);
    transform: translateY(-2px);
  }

  /* HERO STATS */
  .hero-stats {
    position: absolute;
    right: 48px;
    top: 50%;
    transform: translateY(-50%);
    display: flex;
    flex-direction: column;
    gap: 24px;
    opacity: 0;
    animation: fadeLeft 0.8s 1s forwards;
  }
  .stat-item {
    text-align: right;
    padding: 20px 24px;
    border: 1px solid var(--border);
    border-radius: 8px;
    background: rgba(10,15,30,0.6);
    backdrop-filter: blur(10px);
    transition: border-color 0.2s, transform 0.2s;
  }
  .stat-item:hover {
    border-color: rgba(79,140,255,0.4);
    transform: translateX(-4px);
  }
  .stat-num {
    font-size: 36px;
    font-weight: 700;
    color: var(--accent);
    font-family: var(--mono);
    line-height: 1;
  }
  .stat-label {
    font-size: 11px;
    color: var(--text2);
    letter-spacing: 0.1em;
    text-transform: uppercase;
    margin-top: 4px;
  }

  /* SECTIONS */
  section {
    padding: 100px 48px;
    max-width: 1100px;
    margin: 0 auto;
  }

  .section-tag {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--accent);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .section-tag::before { content: '//'; opacity: 0.5; }

  .section-title {
    font-size: clamp(32px, 5vw, 52px);
    font-weight: 700;
    line-height: 1;
    letter-spacing: -0.02em;
    margin-bottom: 60px;
    color: var(--text);
  }
  .section-title span { color: var(--accent); }

  /* TECH STACK */
  .tech-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
    gap: 12px;
  }

  .tech-card {
    padding: 24px 20px;
    border: 1px solid var(--border2);
    border-radius: 8px;
    background: var(--bg2);
    transition: border-color 0.3s, transform 0.3s, box-shadow 0.3s;
    cursor: none;
    position: relative;
    overflow: hidden;
  }
  .tech-card::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, var(--accent), transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }
  .tech-card:hover {
    border-color: rgba(79,140,255,0.5);
    transform: translateY(-4px);
    box-shadow: 0 16px 48px rgba(79,140,255,0.1);
  }
  .tech-card:hover::before { opacity: 0.05; }

  .tech-icon {
    font-size: 28px;
    margin-bottom: 12px;
    display: block;
    filter: grayscale(0.3);
    transition: filter 0.3s, transform 0.3s;
  }
  .tech-card:hover .tech-icon { filter: grayscale(0); transform: scale(1.1); }

  .tech-name {
    font-size: 14px;
    font-weight: 600;
    color: var(--text);
    display: block;
  }
  .tech-level {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--text3);
    margin-top: 4px;
    display: block;
  }

  /* ZEXO PROJECT */
  .zexo-card {
    border: 1px solid var(--border);
    border-radius: 12px;
    background: var(--bg2);
    overflow: hidden;
    position: relative;
  }
  .zexo-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2), var(--accent3));
  }

  .zexo-header {
    padding: 40px 48px 32px;
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    gap: 24px;
    border-bottom: 1px solid var(--border2);
  }
  .zexo-badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    font-family: var(--mono);
    font-size: 11px;
    color: var(--accent2);
    background: rgba(0,229,255,0.08);
    border: 1px solid rgba(0,229,255,0.2);
    padding: 6px 14px;
    border-radius: 100px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }
  .zexo-badge-dot { width: 6px; height: 6px; background: var(--accent2); border-radius: 50%; animation: pulse-dot 2s infinite; }
  .zexo-title { font-size: 40px; font-weight: 700; letter-spacing: -0.02em; margin: 16px 0 12px; }
  .zexo-sub { color: var(--text2); font-size: 16px; line-height: 1.6; max-width: 560px; }

  .zexo-features {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 0;
  }
  .feature-block {
    padding: 32px 40px;
    border-right: 1px solid var(--border2);
    border-bottom: 1px solid var(--border2);
    transition: background 0.2s;
  }
  .feature-block:hover { background: rgba(79,140,255,0.03); }
  .feature-block:nth-child(2n) { border-right: none; }
  .feature-block:nth-child(3), .feature-block:nth-child(4) { border-bottom: none; }

  .feature-label {
    font-family: var(--mono);
    font-size: 10px;
    color: var(--accent);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 12px;
  }
  .feature-list {
    font-size: 14px;
    color: var(--text2);
    line-height: 1.8;
    list-style: none;
  }
  .feature-list li::before { content: '→ '; color: var(--accent); }

  /* APPS */
  .apps-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; }

  .app-card {
    padding: 32px 28px;
    border: 1px solid var(--border2);
    border-radius: 12px;
    background: var(--bg2);
    transition: border-color 0.3s, transform 0.3s;
    position: relative;
    overflow: hidden;
  }
  .app-card::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.3s;
  }
  .app-card:hover { border-color: rgba(79,140,255,0.3); transform: translateY(-4px); }
  .app-card:hover::after { transform: scaleX(1); }

  .app-num {
    font-family: var(--mono);
    font-size: 48px;
    font-weight: 700;
    color: rgba(79,140,255,0.15);
    line-height: 1;
    margin-bottom: 8px;
    transition: color 0.3s;
  }
  .app-card:hover .app-num { color: rgba(79,140,255,0.3); }
  .app-name { font-size: 18px; font-weight: 600; margin-bottom: 6px; }
  .app-users { font-family: var(--mono); font-size: 13px; color: var(--accent); }
  .app-status {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    font-family: var(--mono);
    font-size: 10px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    margin-top: 16px;
    padding: 4px 12px;
    border-radius: 100px;
  }
  .status-live { background: rgba(34,197,94,0.1); color: #22c55e; border: 1px solid rgba(34,197,94,0.2); }
  .status-test { background: rgba(251,191,36,0.1); color: #fbbf24; border: 1px solid rgba(251,191,36,0.2); }

  /* PROJECTS */
  .projects-list { display: flex; flex-direction: column; gap: 1px; background: var(--border2); border-radius: 12px; overflow: hidden; border: 1px solid var(--border2); }

  .project-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 28px 36px;
    background: var(--bg2);
    text-decoration: none;
    transition: background 0.2s;
    gap: 24px;
  }
  .project-row:hover { background: var(--bg3); }

  .project-left { display: flex; align-items: center; gap: 24px; flex: 1; min-width: 0; }
  .project-index {
    font-family: var(--mono);
    font-size: 12px;
    color: var(--text3);
    width: 28px;
    flex-shrink: 0;
  }
  .project-icon {
    width: 40px; height: 40px;
    border: 1px solid var(--border);
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 18px;
    flex-shrink: 0;
    background: var(--bg3);
  }
  .project-name { font-size: 16px; font-weight: 600; color: var(--text); }
  .project-desc { font-size: 13px; color: var(--text2); margin-top: 2px; }

  .project-tech {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    justify-content: flex-end;
    flex-shrink: 0;
  }
  .tag {
    font-family: var(--mono);
    font-size: 10px;
    color: var(--accent);
    background: rgba(79,140,255,0.08);
    border: 1px solid rgba(79,140,255,0.15);
    padding: 3px 10px;
    border-radius: 100px;
    letter-spacing: 0.05em;
    white-space: nowrap;
  }

  .project-arrow {
    color: var(--text3);
    font-size: 18px;
    flex-shrink: 0;
    transition: color 0.2s, transform 0.2s;
  }
  .project-row:hover .project-arrow { color: var(--accent); transform: translate(2px, -2px); }

  /* SOCIAL LINKS */
  .social-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }
  .social-card {
    padding: 32px;
    border: 1px solid var(--border2);
    border-radius: 12px;
    background: var(--bg2);
    text-decoration: none;
    display: flex;
    align-items: center;
    gap: 20px;
    transition: border-color 0.3s, transform 0.3s, box-shadow 0.3s;
    cursor: none;
  }
  .social-card:hover {
    border-color: rgba(79,140,255,0.4);
    transform: translateY(-4px);
    box-shadow: 0 20px 60px rgba(79,140,255,0.08);
  }
  .social-icon {
    width: 48px; height: 48px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 22px;
    flex-shrink: 0;
  }
  .social-name { font-size: 16px; font-weight: 600; color: var(--text); display: block; }
  .social-handle { font-family: var(--mono); font-size: 12px; color: var(--text2); margin-top: 2px; }
  .social-arrow { margin-left: auto; color: var(--text3); font-size: 20px; transition: color 0.2s; }
  .social-card:hover .social-arrow { color: var(--accent); }

  /* FOOTER */
  footer {
    border-top: 1px solid var(--border2);
    padding: 40px 48px;
    max-width: 1100px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .footer-copy { font-family: var(--mono); font-size: 12px; color: var(--text3); }
  .footer-loc { font-family: var(--mono); font-size: 12px; color: var(--text3); display: flex; align-items: center; gap: 8px; }

  /* SCROLL REVEAL */
  .reveal {
    opacity: 0;
    transform: translateY(24px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible { opacity: 1; transform: none; }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: none; }
  }
  @keyframes fadeLeft {
    from { opacity: 0; transform: translateY(-50%) translateX(20px); }
    to { opacity: 1; transform: translateY(-50%) translateX(0); }
  }

  /* SCANLINE */
  .scanline {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
    opacity: 0.4;
    animation: scan 4s linear infinite;
    z-index: 500;
    pointer-events: none;
  }
  @keyframes scan {
    from { top: -2px; }
    to { top: 100vh; }
  }

  /* COUNTER ANIM */
  @keyframes countUp {
    from { opacity: 0; transform: translateY(8px); }
    to { opacity: 1; transform: none; }
  }

  /* Responsive */
  @media (max-width: 900px) {
    nav { padding: 16px 24px; }
    .nav-links { display: none; }
    .hero { padding: 100px 24px 60px; }
    .hero-stats { position: static; transform: none; flex-direction: row; flex-wrap: wrap; animation: fadeUp 0.8s 0.9s forwards; margin-top: 48px; }
    .stat-item { text-align: left; }
    section { padding: 60px 24px; }
    .zexo-header { padding: 28px 24px; }
    .zexo-features { grid-template-columns: 1fr; }
    .feature-block:nth-child(2n) { border-right: 1px solid var(--border2); }
    .feature-block:nth-child(3) { border-bottom: 1px solid var(--border2); }
    .apps-grid { grid-template-columns: 1fr; }
    .social-grid { grid-template-columns: 1fr; }
    footer { flex-direction: column; gap: 8px; padding: 32px 24px; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>
<div class="scanline"></div>
<div class="orb orb1"></div>
<div class="orb orb2"></div>
<div class="orb orb3"></div>

<!-- NAV -->
<nav>
  <span class="nav-logo">MN.dev</span>
  <div class="nav-links">
    <a href="#stack">Stack</a>
    <a href="#project">Project</a>
    <a href="#apps">Apps</a>
    <a href="#oss">Open Source</a>
    <a href="#contact">Contact</a>
  </div>
  <div class="status-pill">
    <span class="status-dot"></span>
    Available for freelance
  </div>
</nav>

<!-- HERO -->
<section style="position:relative; padding-top: 120px; padding-bottom: 80px;">
  <div class="hero-tag">Flutter Developer · Minya, Egypt</div>
  <div class="hero-name"><span>Mina<br/>Nabil</span></div>
  <p class="hero-role">
    Building <strong>production-grade</strong> cross-platform apps<br/>& exploring AI in mobile
  </p>
  <p class="hero-desc">
    3rd Year Computer Science Student crafting real products that reach real users. Every line of code ships to production.
  </p>
  <div class="hero-actions">
    <a href="https://linkedin.com/in/mina-nabil-97bb1b300" class="btn-primary" target="_blank">
      Connect on LinkedIn ↗
    </a>
    <a href="https://github.com/ZAW3AA" class="btn-ghost" target="_blank">
      View GitHub →
    </a>
  </div>

  <div class="hero-stats" id="heroStats">
    <div class="stat-item">
      <div class="stat-num" id="count1">0</div>
      <div class="stat-label">Real Users</div>
    </div>
    <div class="stat-item">
      <div class="stat-num" id="count2">0</div>
      <div class="stat-label">Apps on Play</div>
    </div>
    <div class="stat-item">
      <div class="stat-num" id="count3">0</div>
      <div class="stat-label">Open Source</div>
    </div>
  </div>
</section>

<!-- TECH STACK -->
<section id="stack">
  <div class="section-tag reveal">Tech Stack</div>
  <h2 class="section-title reveal">Tools I <span>build with</span></h2>
  <div class="tech-grid reveal">
    <div class="tech-card">
      <span class="tech-icon">🐦</span>
      <span class="tech-name">Flutter</span>
      <span class="tech-level">Primary · Expert</span>
    </div>
    <div class="tech-card">
      <span class="tech-icon">🎯</span>
      <span class="tech-name">Dart</span>
      <span class="tech-level">Primary · Expert</span>
    </div>
    <div class="tech-card">
      <span class="tech-icon">🔥</span>
      <span class="tech-name">Firebase</span>
      <span class="tech-level">Backend · Advanced</span>
    </div>
    <div class="tech-card">
      <span class="tech-icon">⚡</span>
      <span class="tech-name">Supabase</span>
      <span class="tech-level">Backend · Advanced</span>
    </div>
    <div class="tech-card">
      <span class="tech-icon">🧊</span>
      <span class="tech-name">BLoC / Cubit</span>
      <span class="tech-level">State Mgmt · Expert</span>
    </div>
    <div class="tech-card">
      <span class="tech-icon">⚙️</span>
      <span class="tech-name">C++</span>
      <span class="tech-level">Systems · Intermediate</span>
    </div>
  </div>
</section>

<!-- ZEXO -->
<section id="project">
  <div class="section-tag reveal">Currently Building</div>
  <h2 class="section-title reveal">ZEXO — <span>Commerce OS</span></h2>
  <div class="zexo-card reveal">
    <div class="zexo-header">
      <div>
        <div class="zexo-badge">
          <span class="zexo-badge-dot"></span>
          In Active Development
        </div>
        <div class="zexo-title">ZEXO</div>
        <p class="zexo-sub">
          A production-grade ordering system for any shop or business. Full-stack Flutter commerce & order management platform with real-time admin dashboard.
        </p>
      </div>
    </div>
    <div class="zexo-features">
      <div class="feature-block">
        <div class="feature-label">User Side</div>
        <ul class="feature-list">
          <li>Browse & Cart</li>
          <li>Checkout & Receipt Upload</li>
          <li>Order Tracking</li>
          <li>Real-time Chat</li>
          <li>Push Notifications</li>
        </ul>
      </div>
      <div class="feature-block">
        <div class="feature-label">Admin Dashboard</div>
        <ul class="feature-list">
          <li>Orders & Products</li>
          <li>Categories & Users</li>
          <li>Stock & Analytics</li>
          <li>PDF Reports</li>
        </ul>
      </div>
      <div class="feature-block">
        <div class="feature-label">Auth System</div>
        <ul class="feature-list">
          <li>Email / Google / Facebook</li>
          <li>Role-based Routing</li>
          <li>User Blocking</li>
        </ul>
      </div>
      <div class="feature-block">
        <div class="feature-label">Tech Stack</div>
        <ul class="feature-list">
          <li>Flutter · Firebase · Firestore</li>
          <li>Cloud Functions · FCM</li>
          <li>Supabase Storage · Hive</li>
          <li>BLoC / Cubit Architecture</li>
        </ul>
      </div>
    </div>
  </div>
</section>

<!-- APPS -->
<section id="apps">
  <div class="section-tag reveal">Published</div>
  <h2 class="section-title reveal">3 Apps · <span>346 Real Users</span></h2>
  <div class="apps-grid reveal">
    <div class="app-card">
      <div class="app-num">01</div>
      <div class="app-name">MN – CS1</div>
      <div class="app-users">278 users</div>
      <br/>
      <span class="app-status status-live">
        <span style="width:5px;height:5px;background:#22c55e;border-radius:50%;display:inline-block;"></span>
        Live on Play
      </span>
    </div>
    <div class="app-card">
      <div class="app-num">02</div>
      <div class="app-name">MN – CS2</div>
      <div class="app-users">68 users</div>
      <br/>
      <span class="app-status status-live">
        <span style="width:5px;height:5px;background:#22c55e;border-radius:50%;display:inline-block;"></span>
        Live on Play
      </span>
    </div>
    <div class="app-card">
      <div class="app-num">03</div>
      <div class="app-name">ZEXO</div>
      <div class="app-users">Open Testing</div>
      <br/>
      <span class="app-status status-test">
        <span style="width:5px;height:5px;background:#fbbf24;border-radius:50%;display:inline-block;"></span>
        Testing Phase
      </span>
    </div>
  </div>
</section>

<!-- OPEN SOURCE -->
<section id="oss">
  <div class="section-tag reveal">Open Source</div>
  <h2 class="section-title reveal">Projects I've <span>shipped</span></h2>
  <div class="projects-list reveal">
    <a href="https://github.com/ZAW3AA/MotoRent" target="_blank" class="project-row">
      <div class="project-left">
        <span class="project-index">01</span>
        <div class="project-icon">🚗</div>
        <div>
          <div class="project-name">MotoRent</div>
          <div class="project-desc">Car rental platform</div>
        </div>
      </div>
      <div class="project-tech">
        <span class="tag">Flutter</span>
        <span class="tag">Dart</span>
      </div>
      <span class="project-arrow">↗</span>
    </a>
    <a href="https://github.com/ZAW3AA/EasyGPS" target="_blank" class="project-row">
      <div class="project-left">
        <span class="project-index">02</span>
        <div class="project-icon">📍</div>
        <div>
          <div class="project-name">EasyGPS</div>
          <div class="project-desc">Real-time GPS tracking</div>
        </div>
      </div>
      <div class="project-tech">
        <span class="tag">Flutter</span>
        <span class="tag">Maps API</span>
      </div>
      <span class="project-arrow">↗</span>
    </a>
    <a href="https://github.com/ZAW3AA/EasyTaskToDo-flutter" target="_blank" class="project-row">
      <div class="project-left">
        <span class="project-index">03</span>
        <div class="project-icon">✅</div>
        <div>
          <div class="project-name">EasyTaskToDo</div>
          <div class="project-desc">Clean To-Do app</div>
        </div>
      </div>
      <div class="project-tech">
        <span class="tag">Flutter</span>
        <span class="tag">Hive</span>
      </div>
      <span class="project-arrow">↗</span>
    </a>
    <a href="https://github.com/ZAW3AA/EasyCalculator" target="_blank" class="project-row">
      <div class="project-left">
        <span class="project-index">04</span>
        <div class="project-icon">🔢</div>
        <div>
          <div class="project-name">EasyCalculator</div>
          <div class="project-desc">Calculator app</div>
        </div>
      </div>
      <div class="project-tech">
        <span class="tag">C++</span>
      </div>
      <span class="project-arrow">↗</span>
    </a>
    <a href="https://github.com/ZAW3AA/EasyBooklet" target="_blank" class="project-row">
      <div class="project-left">
        <span class="project-index">05</span>
        <div class="project-icon">📖</div>
        <div>
          <div class="project-name">EasyBooklet</div>
          <div class="project-desc">Short stories reader</div>
        </div>
      </div>
      <div class="project-tech">
        <span class="tag">HTML</span>
        <span class="tag">CSS</span>
      </div>
      <span class="project-arrow">↗</span>
    </a>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="section-tag reveal">Contact</div>
  <h2 class="section-title reveal">Let's <span>build together</span></h2>
  <div class="social-grid reveal">
    <a href="https://linkedin.com/in/mina-nabil-97bb1b300" target="_blank" class="social-card">
      <div class="social-icon" style="background:rgba(10,102,194,0.1);border:1px solid rgba(10,102,194,0.2);">💼</div>
      <div>
        <span class="social-name">LinkedIn</span>
        <span class="social-handle">mina-nabil-97bb1b300</span>
      </div>
      <span class="social-arrow">↗</span>
    </a>
    <a href="https://github.com/ZAW3AA" target="_blank" class="social-card">
      <div class="social-icon" style="background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.1);">🐙</div>
      <div>
        <span class="social-name">GitHub</span>
        <span class="social-handle">@ZAW3AA</span>
      </div>
      <span class="social-arrow">↗</span>
    </a>
    <a href="https://www.facebook.com/profile.php?id=61550226644154" target="_blank" class="social-card">
      <div class="social-icon" style="background:rgba(24,119,242,0.1);border:1px solid rgba(24,119,242,0.2);">📘</div>
      <div>
        <span class="social-name">Facebook</span>
        <span class="social-handle">Mina Nabil</span>
      </div>
      <span class="social-arrow">↗</span>
    </a>
    <div class="social-card" style="border-color:rgba(79,140,255,0.15);">
      <div class="social-icon" style="background:rgba(79,140,255,0.08);border:1px solid rgba(79,140,255,0.15);">📍</div>
      <div>
        <span class="social-name">Location</span>
        <span class="social-handle">Minya, Egypt · Open to remote</span>
      </div>
    </div>
  </div>
</section>

<footer>
  <span class="footer-copy">© 2025 Mina Nabil — Built with passion</span>
  <span class="footer-loc">
    <span style="width:6px;height:6px;background:#22c55e;border-radius:50%;display:inline-block;animation:pulse-dot 2s infinite;"></span>
    Open to collaboration & freelance
  </span>
</footer>

<script>
// Custom cursor
const cursor = document.getElementById('cursor');
const ring = document.getElementById('cursorRing');
let mx = 0, my = 0, rx = 0, ry = 0;
document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
(function animCursor() {
  rx += (mx - rx) * 0.15;
  ry += (my - ry) * 0.15;
  cursor.style.left = mx + 'px';
  cursor.style.top = my + 'px';
  ring.style.left = rx + 'px';
  ring.style.top = ry + 'px';
  requestAnimationFrame(animCursor);
})();

document.querySelectorAll('a, button, .tech-card, .app-card, .stat-item').forEach(el => {
  el.addEventListener('mouseenter', () => {
    cursor.style.transform = 'translate(-50%, -50%) scale(2)';
    ring.style.width = '56px';
    ring.style.height = '56px';
  });
  el.addEventListener('mouseleave', () => {
    cursor.style.transform = 'translate(-50%, -50%) scale(1)';
    ring.style.width = '36px';
    ring.style.height = '36px';
  });
});

// Counter animation
function animateCounter(el, target, duration) {
  let start = 0, startTime = null;
  const step = (timestamp) => {
    if (!startTime) startTime = timestamp;
    const progress = Math.min((timestamp - startTime) / duration, 1);
    const eased = 1 - Math.pow(1 - progress, 3);
    el.textContent = Math.floor(eased * target);
    if (progress < 1) requestAnimationFrame(step);
    else el.textContent = target;
  };
  requestAnimationFrame(step);
}

setTimeout(() => {
  animateCounter(document.getElementById('count1'), 346, 1800);
  animateCounter(document.getElementById('count2'), 3, 600);
  animateCounter(document.getElementById('count3'), 5, 800);
}, 1200);

// Scroll reveal
const reveals = document.querySelectorAll('.reveal');
const observer = new IntersectionObserver((entries) => {
  entries.forEach((e, i) => {
    if (e.isIntersecting) {
      setTimeout(() => e.target.classList.add('visible'), i * 80);
    }
  });
}, { threshold: 0.1 });
reveals.forEach(el => observer.observe(el));
</script>
</body>
</html>
