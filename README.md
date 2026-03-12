<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Hemant Maurya — GitHub Profile</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=JetBrains+Mono:wght@300;400;600&family=Clash+Display:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --gold: #FFD700;
    --gold2: #FFA500;
    --cyan: #00FFFF;
    --neon-blue: #2F81F7;
    --violet: #8B5CF6;
    --bg: #020408;
    --bg2: #060D18;
    --card: rgba(15,25,45,0.85);
    --glass: rgba(255,255,255,0.04);
    --border: rgba(255,215,0,0.15);
    --text: #E8F4FF;
    --muted: #7A9BBF;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'JetBrains Mono', monospace;
    min-height: 100vh;
    overflow-x: hidden;
    cursor: none;
  }

  /* ── Custom Cursor ── */
  #cursor {
    width: 12px; height: 12px;
    background: var(--gold);
    border-radius: 50%;
    position: fixed; pointer-events: none; z-index: 9999;
    transform: translate(-50%,-50%);
    transition: transform 0.1s, width 0.2s, height 0.2s, background 0.2s;
    box-shadow: 0 0 20px var(--gold), 0 0 40px rgba(255,215,0,0.4);
  }
  #cursor-trail {
    width: 32px; height: 32px;
    border: 1.5px solid rgba(255,215,0,0.5);
    border-radius: 50%;
    position: fixed; pointer-events: none; z-index: 9998;
    transform: translate(-50%,-50%);
    transition: left 0.12s ease, top 0.12s ease;
  }

  /* ── Animated BG ── */
  #bg-canvas {
    position: fixed; inset: 0; z-index: 0;
    pointer-events: none;
  }

  /* ── Grid overlay ── */
  .grid-overlay {
    position: fixed; inset: 0; z-index: 0; pointer-events: none;
    background-image:
      linear-gradient(rgba(47,129,247,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(47,129,247,0.04) 1px, transparent 1px);
    background-size: 60px 60px;
  }

  /* ── Main layout ── */
  .wrapper {
    max-width: 960px;
    margin: 0 auto;
    padding: 0 24px 80px;
    position: relative; z-index: 2;
  }

  /* ── HERO ── */
  .hero {
    min-height: 100vh;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    text-align: center;
    padding-top: 60px;
  }

  .hero-badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(255,215,0,0.1);
    border: 1px solid rgba(255,215,0,0.3);
    border-radius: 100px;
    padding: 6px 18px;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--gold);
    margin-bottom: 32px;
    animation: fadeSlideUp 0.6s 0.2s both;
  }
  .hero-badge::before {
    content: '';
    width: 6px; height: 6px;
    background: var(--gold);
    border-radius: 50%;
    animation: pulse 1.5s infinite;
  }

  @keyframes pulse {
    0%,100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.4; transform: scale(0.7); }
  }

  .hero-avatar {
    width: 120px; height: 120px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--gold) 0%, #FF8C00 50%, var(--violet) 100%);
    display: flex; align-items: center; justify-content: center;
    font-size: 52px;
    margin: 0 auto 28px;
    position: relative;
    animation: fadeSlideUp 0.6s 0.3s both;
  }
  .hero-avatar::before {
    content: '';
    position: absolute; inset: -4px;
    border-radius: 50%;
    background: conic-gradient(var(--gold), var(--cyan), var(--violet), var(--gold));
    z-index: -1;
    animation: spin 4s linear infinite;
  }
  .hero-avatar::after {
    content: '';
    position: absolute; inset: -8px;
    border-radius: 50%;
    background: conic-gradient(transparent 60%, rgba(255,215,0,0.3) 100%);
    z-index: -2;
    animation: spin 3s linear infinite reverse;
  }

  @keyframes spin { to { transform: rotate(360deg); } }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2.8rem, 8vw, 5.5rem);
    font-weight: 800;
    line-height: 1;
    letter-spacing: -2px;
    animation: fadeSlideUp 0.6s 0.4s both;
    background: linear-gradient(135deg, #fff 0%, var(--gold) 50%, var(--cyan) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-tagline {
    font-size: 14px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--muted);
    margin: 12px 0 28px;
    animation: fadeSlideUp 0.6s 0.5s both;
  }

  .typewriter-container {
    font-family: 'JetBrains Mono', monospace;
    font-size: 16px;
    color: var(--cyan);
    height: 28px;
    animation: fadeSlideUp 0.6s 0.6s both;
  }
  .typewriter-container span { border-right: 2px solid var(--cyan); animation: blink 0.8s infinite; }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  .hero-pills {
    display: flex; gap: 12px; flex-wrap: wrap; justify-content: center;
    margin-top: 32px;
    animation: fadeSlideUp 0.6s 0.8s both;
  }
  .pill {
    background: var(--glass);
    border: 1px solid var(--border);
    border-radius: 100px;
    padding: 8px 20px;
    font-size: 12px;
    color: var(--text);
    backdrop-filter: blur(10px);
    transition: all 0.3s;
  }
  .pill:hover {
    border-color: var(--gold);
    color: var(--gold);
    background: rgba(255,215,0,0.08);
    transform: translateY(-2px);
    box-shadow: 0 8px 24px rgba(255,215,0,0.15);
  }

  .scroll-indicator {
    position: absolute; bottom: 40px; left: 50%;
    transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center;
    gap: 8px; color: var(--muted); font-size: 10px; letter-spacing: 2px;
    animation: fadeSlideUp 1s 1.2s both;
  }
  .scroll-line {
    width: 1px; height: 40px;
    background: linear-gradient(to bottom, var(--gold), transparent);
    animation: scrollPulse 2s infinite;
  }
  @keyframes scrollPulse {
    0%,100% { opacity: 0.3; transform: scaleY(1); }
    50% { opacity: 1; transform: scaleY(1.2); }
  }

  @keyframes fadeSlideUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ── Section styles ── */
  section { margin-bottom: 80px; }

  .section-label {
    display: flex; align-items: center; gap: 14px;
    margin-bottom: 36px;
  }
  .section-label::before {
    content: '';
    height: 2px; flex: 1;
    background: linear-gradient(to right, transparent, var(--gold));
  }
  .section-label::after {
    content: '';
    height: 2px; flex: 1;
    background: linear-gradient(to left, transparent, var(--gold));
  }
  .section-label span {
    font-family: 'Syne', sans-serif;
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--gold);
    white-space: nowrap;
  }

  /* ── About cards ── */
  .about-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 16px;
  }
  .about-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 24px;
    backdrop-filter: blur(20px);
    transition: all 0.4s cubic-bezier(0.23,1,0.32,1);
    position: relative;
    overflow: hidden;
  }
  .about-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, var(--gold), transparent);
    opacity: 0;
    transition: opacity 0.4s;
  }
  .about-card:hover::before { opacity: 1; }
  .about-card:hover {
    border-color: rgba(255,215,0,0.4);
    transform: translateY(-6px);
    box-shadow: 0 24px 60px rgba(0,0,0,0.5), 0 0 40px rgba(255,215,0,0.06);
  }
  .about-icon { font-size: 28px; margin-bottom: 12px; }
  .about-card h3 { font-size: 12px; letter-spacing: 2px; text-transform: uppercase; color: var(--gold); margin-bottom: 6px; }
  .about-card p { font-size: 13px; color: var(--muted); line-height: 1.6; }

  /* ── Skill badges ── */
  .skills-grid {
    display: flex; flex-wrap: wrap; gap: 12px;
  }
  .skill-tag {
    display: flex; align-items: center; gap: 8px;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 10px 16px;
    font-size: 12px;
    font-weight: 600;
    letter-spacing: 0.5px;
    transition: all 0.3s;
    cursor: default;
    backdrop-filter: blur(10px);
  }
  .skill-tag:hover {
    border-color: var(--gold);
    background: rgba(255,215,0,0.06);
    transform: scale(1.05) translateY(-2px);
    box-shadow: 0 12px 30px rgba(0,0,0,0.4), 0 0 20px rgba(255,215,0,0.1);
  }
  .skill-dot {
    width: 8px; height: 8px; border-radius: 50%;
  }

  .skill-section-title {
    font-size: 10px; letter-spacing: 3px; text-transform: uppercase;
    color: var(--muted); margin-bottom: 12px; margin-top: 24px;
  }

  /* ── Stats cards ── */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 20px;
  }
  .stat-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 24px;
    backdrop-filter: blur(20px);
    overflow: hidden;
    position: relative;
    transition: all 0.4s;
  }
  .stat-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 20px 50px rgba(0,0,0,0.5);
    border-color: rgba(47,129,247,0.4);
  }
  .stat-card img { width: 100%; border-radius: 12px; display: block; }
  .stat-card .glow-frame {
    position: absolute; inset: 0; border-radius: 20px;
    box-shadow: inset 0 0 40px rgba(47,129,247,0.05);
    pointer-events: none;
  }

  /* ── Trophies ── */
  .trophy-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 28px;
    text-align: center;
    backdrop-filter: blur(20px);
    transition: all 0.4s;
  }
  .trophy-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 20px 50px rgba(0,0,0,0.5), 0 0 60px rgba(255,215,0,0.08);
    border-color: rgba(255,215,0,0.4);
  }
  .trophy-card img { width: 100%; border-radius: 12px; }

  /* ── Quote ── */
  .quote-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 40px;
    text-align: center;
    backdrop-filter: blur(20px);
    position: relative;
    overflow: hidden;
  }
  .quote-card::before {
    content: '"';
    position: absolute; top: -20px; left: 24px;
    font-family: 'Syne', sans-serif;
    font-size: 140px; font-weight: 800;
    color: rgba(255,215,0,0.05);
    line-height: 1;
    pointer-events: none;
  }
  .quote-text {
    font-family: 'Syne', sans-serif;
    font-size: 18px;
    font-weight: 600;
    color: var(--text);
    line-height: 1.6;
    margin-bottom: 16px;
    position: relative;
  }
  .quote-author { font-size: 12px; color: var(--gold); letter-spacing: 2px; text-transform: uppercase; }

  /* ── Social links ── */
  .socials {
    display: flex; gap: 16px; flex-wrap: wrap; justify-content: center;
  }
  .social-btn {
    display: inline-flex; align-items: center; gap: 10px;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 12px 22px;
    text-decoration: none;
    font-size: 13px;
    font-weight: 600;
    color: var(--text);
    backdrop-filter: blur(10px);
    transition: all 0.3s cubic-bezier(0.23,1,0.32,1);
    letter-spacing: 0.5px;
  }
  .social-btn:hover {
    transform: translateY(-4px) scale(1.03);
    box-shadow: 0 16px 40px rgba(0,0,0,0.4), 0 0 24px var(--glow);
    border-color: var(--glow);
    color: #fff;
  }
  .social-btn .icon { font-size: 18px; }

  /* ── Wings Hero ── */
  .wings {
    display: flex; align-items: center; justify-content: center;
    gap: 12px; margin-bottom: 20px;
    animation: wings-float 3s ease-in-out infinite;
  }
  @keyframes wings-float {
    0%,100% { transform: translateY(0); }
    50% { transform: translateY(-8px); }
  }
  .wing {
    font-size: 52px;
    filter: drop-shadow(0 0 20px rgba(255,215,0,0.8));
  }
  .crown { font-size: 40px; filter: drop-shadow(0 0 16px rgba(255,215,0,0.9)); }

  /* ── Game zone ── */
  .games-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 16px;
  }
  .game-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 24px;
    text-align: center;
    backdrop-filter: blur(10px);
    transition: all 0.3s;
    text-decoration: none;
    color: var(--text);
    display: flex; flex-direction: column; align-items: center; gap: 12px;
  }
  .game-card:hover {
    transform: translateY(-6px) scale(1.02);
    border-color: var(--cyan);
    box-shadow: 0 20px 50px rgba(0,0,0,0.4), 0 0 30px rgba(0,255,255,0.1);
  }
  .game-card .game-icon { font-size: 38px; }
  .game-card h3 { font-size: 14px; font-weight: 700; font-family: 'Syne', sans-serif; }
  .game-card p { font-size: 11px; color: var(--muted); }
  .game-card .play-btn {
    display: inline-flex; align-items: center; gap: 6px;
    background: rgba(0,255,255,0.1);
    border: 1px solid rgba(0,255,255,0.3);
    border-radius: 8px;
    padding: 8px 18px;
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 1px;
    color: var(--cyan);
    text-decoration: none;
    text-transform: uppercase;
    transition: all 0.3s;
  }
  .game-card:hover .play-btn {
    background: rgba(0,255,255,0.2);
    box-shadow: 0 0 20px rgba(0,255,255,0.2);
  }

  /* ── Footer ── */
  .footer {
    text-align: center;
    padding: 40px 0;
    border-top: 1px solid var(--border);
    margin-top: 40px;
  }
  .footer p { font-size: 12px; color: var(--muted); margin-top: 8px; }

  /* ── Number counter animation ── */
  .counter { font-family: 'Syne', sans-serif; font-size: 32px; font-weight: 800; color: var(--gold); }

  /* ── Glow bars for skill categories ── */
  .skill-category {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 24px;
    backdrop-filter: blur(10px);
    margin-bottom: 16px;
  }
  .skill-bar-row { margin-bottom: 14px; }
  .skill-bar-label {
    display: flex; justify-content: space-between;
    font-size: 11px; margin-bottom: 6px;
    color: var(--muted);
  }
  .skill-bar-label span:first-child { color: var(--text); font-weight: 600; }
  .skill-bar-track {
    height: 5px; background: rgba(255,255,255,0.06);
    border-radius: 999px; overflow: hidden;
  }
  .skill-bar-fill {
    height: 100%; border-radius: 999px;
    background: linear-gradient(90deg, var(--neon-blue), var(--cyan));
    transform: scaleX(0); transform-origin: left;
    transition: transform 1.2s cubic-bezier(0.23,1,0.32,1);
    box-shadow: 0 0 12px rgba(0,255,255,0.4);
  }
  .skill-bar-fill.animate { transform: scaleX(1); }

  /* ── Floating particles ── */
  .particle {
    position: fixed; pointer-events: none; z-index: 1;
    border-radius: 50%;
    animation: float-particle linear infinite;
  }
  @keyframes float-particle {
    0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
    10% { opacity: 1; }
    90% { opacity: 1; }
    100% { transform: translateY(-20px) rotate(720deg); opacity: 0; }
  }

  /* ── Holographic shimmer ── */
  @keyframes holographic {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  .holo {
    background: linear-gradient(135deg, var(--gold), var(--cyan), var(--violet), var(--gold));
    background-size: 300% 300%;
    animation: holographic 4s ease infinite;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  /* stats mini cards */
  .mini-stats {
    display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px;
    margin-bottom: 24px;
  }
  .mini-stat {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px; padding: 20px;
    text-align: center; backdrop-filter: blur(10px);
    transition: all 0.3s;
  }
  .mini-stat:hover {
    border-color: rgba(255,215,0,0.4);
    transform: translateY(-4px);
    box-shadow: 0 16px 40px rgba(0,0,0,0.4);
  }
  .mini-stat .num {
    font-family: 'Syne', sans-serif; font-size: 28px; font-weight: 800;
    background: linear-gradient(135deg, var(--gold), var(--cyan));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
  }
  .mini-stat .label { font-size: 10px; color: var(--muted); letter-spacing: 1.5px; text-transform: uppercase; margin-top: 4px; }

  @media (max-width: 600px) {
    .mini-stats { grid-template-columns: 1fr; }
    .stats-grid { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<!-- Custom cursor -->
<div id="cursor"></div>
<div id="cursor-trail"></div>

<!-- Background canvas -->
<canvas id="bg-canvas"></canvas>
<div class="grid-overlay"></div>

<div class="wrapper">

  <!-- ── HERO ── -->
  <section class="hero" style="position:relative">
    <div class="hero-badge">⚡ Available for Projects</div>
    <div class="hero-avatar">👨‍💻</div>
    <h1 class="hero-name">Hemant Maurya</h1>
    <p class="hero-tagline">Full Stack Developer · VGU · India</p>
    <div class="typewriter-container">
      <span id="typewriter"></span>
    </div>
    <div class="hero-pills">
      <div class="pill">🎓 VGU Student</div>
      <div class="pill">⚛️ React Dev</div>
      <div class="pill">☕ Java Enthusiast</div>
      <div class="pill">🎵 Codes with Music</div>
      <div class="pill">🌱 Always Learning</div>
    </div>
    <div class="scroll-indicator" style="position:static;margin-top:48px">
      <div class="scroll-line"></div>
      <span>SCROLL</span>
    </div>
  </section>

  <!-- ── ABOUT ── -->
  <section>
    <div class="section-label"><span>✦ About Me</span></div>
    <div class="about-grid">
      <div class="about-card">
        <div class="about-icon">🎓</div>
        <h3>Education</h3>
        <p>Studying at Vivekananda Global University, pursuing my passion for tech every day.</p>
      </div>
      <div class="about-card">
        <div class="about-icon">💻</div>
        <h3>Development</h3>
        <p>Crafting full-stack web applications with React, Node.js, and modern tooling.</p>
      </div>
      <div class="about-card">
        <div class="about-icon">🎯</div>
        <h3>Goals</h3>
        <p>Building innovative solutions and contributing to open-source projects.</p>
      </div>
      <div class="about-card">
        <div class="about-icon">📧</div>
        <h3>Contact</h3>
        <p>hemantjimi@gmail.com — always open to new ideas and collaborations!</p>
      </div>
    </div>
  </section>

  <!-- ── MINI STATS ── -->
  <section>
    <div class="section-label"><span>✦ At a Glance</span></div>
    <div class="mini-stats">
      <div class="mini-stat">
        <div class="num" data-target="12">0</div>
        <div class="label">Repositories</div>
      </div>
      <div class="mini-stat">
        <div class="num" data-target="8">0</div>
        <div class="label">Projects</div>
      </div>
      <div class="mini-stat">
        <div class="num" data-target="5">0</div>
        <div class="label">Technologies</div>
      </div>
    </div>
  </section>

  <!-- ── SKILLS ── -->
  <section>
    <div class="section-label"><span>✦ Tech Stack</span></div>

    <div class="skill-section-title">Languages</div>
    <div class="skills-grid">
      <div class="skill-tag"><span class="skill-dot" style="background:#ED8B00"></span>Java</div>
      <div class="skill-tag"><span class="skill-dot" style="background:#F7DF1E"></span>JavaScript</div>
      <div class="skill-tag"><span class="skill-dot" style="background:#3776AB"></span>Python</div>
      <div class="skill-tag"><span class="skill-dot" style="background:#E34F26"></span>HTML5</div>
      <div class="skill-tag"><span class="skill-dot" style="background:#1572B6"></span>CSS3</div>
    </div>

    <div class="skill-section-title">Frameworks & Libraries</div>
    <div class="skills-grid">
      <div class="skill-tag"><span class="skill-dot" style="background:#61DAFB"></span>React</div>
      <div class="skill-tag"><span class="skill-dot" style="background:#339933"></span>Node.js</div>
      <div class="skill-tag"><span class="skill-dot" style="background:#ffffff"></span>Express.js</div>
      <div class="skill-tag"><span class="skill-dot" style="background:#7952B3"></span>Bootstrap</div>
    </div>

    <div class="skill-section-title">Tools & Databases</div>
    <div class="skills-grid">
      <div class="skill-tag"><span class="skill-dot" style="background:#F05032"></span>Git</div>
      <div class="skill-tag"><span class="skill-dot" style="background:#ffffff"></span>GitHub</div>
      <div class="skill-tag"><span class="skill-dot" style="background:#007ACC"></span>VS Code</div>
      <div class="skill-tag"><span class="skill-dot" style="background:#FF6C37"></span>Postman</div>
      <div class="skill-tag"><span class="skill-dot" style="background:#47A248"></span>MongoDB</div>
      <div class="skill-tag"><span class="skill-dot" style="background:#4479A1"></span>MySQL</div>
    </div>

    <br>
    <div class="skill-category">
      <div class="skill-bar-row">
        <div class="skill-bar-label"><span>Frontend Development</span><span>90%</span></div>
        <div class="skill-bar-track"><div class="skill-bar-fill" style="width:90%"></div></div>
      </div>
      <div class="skill-bar-row">
        <div class="skill-bar-label"><span>Java Programming</span><span>85%</span></div>
        <div class="skill-bar-track"><div class="skill-bar-fill" style="width:85%"></div></div>
      </div>
      <div class="skill-bar-row">
        <div class="skill-bar-label"><span>Backend (Node/Express)</span><span>75%</span></div>
        <div class="skill-bar-track"><div class="skill-bar-fill" style="width:75%"></div></div>
      </div>
      <div class="skill-bar-row">
        <div class="skill-bar-label"><span>Database Design</span><span>70%</span></div>
        <div class="skill-bar-track"><div class="skill-bar-fill" style="width:70%"></div></div>
      </div>
      <div class="skill-bar-row" style="margin-bottom:0">
        <div class="skill-bar-label"><span>UI/UX Design</span><span>80%</span></div>
        <div class="skill-bar-track"><div class="skill-bar-fill" style="width:80%"></div></div>
      </div>
    </div>
  </section>

  <!-- ── GITHUB STATS ── -->
  <section>
    <div class="section-label"><span>✦ GitHub Stats</span></div>
    <div class="stats-grid">
      <div class="stat-card">
        <img src="https://github-readme-stats.vercel.app/api?username=HemantJimin&show_icons=true&theme=tokyonight&hide_border=true&count_private=true&bg_color=060D18&text_color=E8F4FF&icon_color=FFD700&title_color=FFD700" alt="GitHub Stats" />
        <div class="glow-frame"></div>
      </div>
      <div class="stat-card">
        <img src="https://github-readme-streak-stats.herokuapp.com/?user=HemantJimin&theme=tokyonight&hide_border=true&background=060D18&stroke=2F81F7&ring=FFD700&fire=FF6600&currStreakLabel=FFD700" alt="GitHub Streak" />
        <div class="glow-frame"></div>
      </div>
    </div>
    <br>
    <div class="stat-card" style="max-width:400px;margin:0 auto">
      <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=HemantJimin&layout=compact&theme=tokyonight&hide_border=true&bg_color=060D18&text_color=E8F4FF&title_color=FFD700" alt="Top Languages" />
      <div class="glow-frame"></div>
    </div>
  </section>

  <!-- ── TROPHIES ── -->
  <section>
    <div class="section-label"><span>✦ Trophies</span></div>
    <div class="trophy-card">
      <img src="https://github-profile-trophy.vercel.app/?username=HemantJimin&theme=onestar&no-frame=true&row=1&column=6&margin-w=12" alt="Trophies" />
    </div>
  </section>

  <!-- ── GOLDEN WINGS ── -->
  <section style="text-align:center">
    <div class="section-label"><span>✦ Golden Angel</span></div>
    <div class="wings">
      <span class="wing">🪽</span>
      <span class="crown">👑</span>
      <span class="wing" style="transform:scaleX(-1);display:inline-block">🪽</span>
    </div>
    <p style="color:var(--muted);font-size:12px;letter-spacing:2px;text-transform:uppercase">Hemant Jimin — #HemantJimin</p>
  </section>

  <!-- ── SNAKE ── -->
  <section>
    <div class="section-label"><span>✦ Contribution Snake</span></div>
    <div class="stat-card">
      <img src="https://raw.githubusercontent.com/HemantJimin/HemantJimin/output/github-contribution-grid-snake.svg" alt="Snake" />
      <div class="glow-frame"></div>
    </div>
  </section>

  <!-- ── GAMES ── -->
  <section>
    <div class="section-label"><span>✦ Game Zone</span></div>
    <div class="games-grid">
      <div class="game-card">
        <div class="game-icon">🕹️</div>
        <h3>Tetris</h3>
        <p>Classic block stacking action</p>
        <a href="https://tetris.com/play-tetris" target="_blank" class="play-btn">▶ Play Now</a>
      </div>
      <div class="game-card">
        <div class="game-icon">🔢</div>
        <h3>2048</h3>
        <p>Merge tiles to reach 2048</p>
        <a href="https://play2048.co/" target="_blank" class="play-btn">▶ Play Now</a>
      </div>
      <div class="game-card">
        <div class="game-icon">👾</div>
        <h3>Games Hub</h3>
        <p>Explore hundreds of free games</p>
        <a href="https://www.crazygames.com/" target="_blank" class="play-btn">▶ Explore</a>
      </div>
    </div>
  </section>

  <!-- ── SOCIALS ── -->
  <section>
    <div class="section-label"><span>✦ Connect</span></div>
    <div class="socials">
      <a href="https://github.com/HemantJimin" target="_blank" class="social-btn" style="--glow:#ffffff">
        <span class="icon">🐙</span> GitHub
      </a>
      <a href="https://www.instagram.com/hemantjimin/" target="_blank" class="social-btn" style="--glow:#E1306C">
        <span class="icon">📸</span> Instagram
      </a>
      <a href="http://webdevsoft.com/" target="_blank" class="social-btn" style="--glow:#2F81F7">
        <span class="icon">🌐</span> Website
      </a>
      <a href="mailto:hemantjimi@gmail.com" class="social-btn" style="--glow:#FFD700">
        <span class="icon">✉️</span> Email
      </a>
    </div>
  </section>

  <!-- ── QUOTE ── -->
  <section>
    <div class="section-label"><span>✦ Dev Wisdom</span></div>
    <div class="quote-card">
      <p class="quote-text">"Code is like humor. When you have to explain it, it's bad."</p>
      <p class="quote-author">— Cory House</p>
    </div>
  </section>

  <!-- ── FOOTER ── -->
  <div class="footer">
    <h2 class="holo" style="font-family:'Syne',sans-serif;font-size:24px;font-weight:800">✨ Star Some Repos! 🌟</h2>
    <p>© 2026 Hemant Maurya · Made with ❤️ and ☕</p>
  </div>

</div><!-- /wrapper -->

<script>
// ── Custom cursor
const cursor = document.getElementById('cursor');
const trail = document.getElementById('cursor-trail');
let mx = 0, my = 0;
document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  cursor.style.left = mx + 'px';
  cursor.style.top = my + 'px';
  setTimeout(() => {
    trail.style.left = mx + 'px';
    trail.style.top = my + 'px';
  }, 80);
});
document.querySelectorAll('a,.about-card,.skill-tag,.game-card,.social-btn').forEach(el => {
  el.addEventListener('mouseenter', () => {
    cursor.style.width = '20px'; cursor.style.height = '20px';
    cursor.style.background = 'var(--cyan)';
  });
  el.addEventListener('mouseleave', () => {
    cursor.style.width = '12px'; cursor.style.height = '12px';
    cursor.style.background = 'var(--gold)';
  });
});

// ── Animated background canvas
const canvas = document.getElementById('bg-canvas');
const ctx = canvas.getContext('2d');
let W, H, stars = [], nebulas = [];
function resize() {
  W = canvas.width = window.innerWidth;
  H = canvas.height = window.innerHeight;
}
resize();
window.addEventListener('resize', resize);

for (let i = 0; i < 200; i++) {
  stars.push({
    x: Math.random() * 2000, y: Math.random() * 2000,
    r: Math.random() * 1.5 + 0.2,
    speed: Math.random() * 0.3 + 0.05,
    opacity: Math.random() * 0.8 + 0.2,
    flicker: Math.random() * Math.PI * 2
  });
}
for (let i = 0; i < 5; i++) {
  nebulas.push({
    x: Math.random() * 2000, y: Math.random() * 2000,
    r: Math.random() * 300 + 150,
    hue: [240, 270, 200, 45, 280][i],
    opacity: Math.random() * 0.03 + 0.01
  });
}

let frame = 0;
function drawBg() {
  ctx.clearRect(0, 0, W, H);
  frame++;
  nebulas.forEach(n => {
    const grd = ctx.createRadialGradient(n.x % W, n.y % H, 0, n.x % W, n.y % H, n.r);
    grd.addColorStop(0, `hsla(${n.hue},80%,60%,${n.opacity})`);
    grd.addColorStop(1, 'transparent');
    ctx.fillStyle = grd;
    ctx.beginPath();
    ctx.arc(n.x % W, n.y % H, n.r, 0, Math.PI * 2);
    ctx.fill();
  });
  stars.forEach(s => {
    s.y -= s.speed;
    if (s.y < 0) { s.y = H; s.x = Math.random() * W; }
    const flicker = Math.sin(frame * 0.03 + s.flicker) * 0.3 + 0.7;
    ctx.beginPath();
    ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(255,255,255,${s.opacity * flicker})`;
    ctx.fill();
  });
  requestAnimationFrame(drawBg);
}
drawBg();

// ── Typewriter
const phrases = ['Full Stack Developer', 'React Enthusiast', 'Java Programmer', 'UI/UX Designer', 'Open Source Fan'];
let pi = 0, ci = 0, deleting = false;
const tw = document.getElementById('typewriter');
function type() {
  const cur = phrases[pi];
  if (!deleting) {
    tw.textContent = cur.slice(0, ++ci);
    if (ci === cur.length) { deleting = true; setTimeout(type, 1600); return; }
    setTimeout(type, 70);
  } else {
    tw.textContent = cur.slice(0, --ci);
    if (ci === 0) { deleting = false; pi = (pi + 1) % phrases.length; setTimeout(type, 400); return; }
    setTimeout(type, 35);
  }
}
type();

// ── Skill bar animation on scroll
const bars = document.querySelectorAll('.skill-bar-fill');
const obs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) { e.target.classList.add('animate'); obs.unobserve(e.target); }
  });
}, { threshold: 0.3 });
bars.forEach(b => obs.observe(b));

// ── Counter animation
const counters = document.querySelectorAll('.num[data-target]');
const cobs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      const el = e.target;
      const target = +el.dataset.target;
      let cur = 0;
      const step = () => {
        cur += Math.ceil(target / 30);
        if (cur >= target) { el.textContent = target + '+'; return; }
        el.textContent = cur + '+';
        requestAnimationFrame(step);
      };
      step();
      cobs.unobserve(el);
    }
  });
}, { threshold: 0.5 });
counters.forEach(c => cobs.observe(c));

// ── Floating particles
function spawnParticle() {
  const p = document.createElement('div');
  p.className = 'particle';
  const size = Math.random() * 3 + 1;
  const colors = ['#FFD700','#00FFFF','#8B5CF6','#2F81F7','#FF8C00'];
  p.style.cssText = `
    width:${size}px;height:${size}px;
    left:${Math.random()*100}vw;
    background:${colors[Math.floor(Math.random()*colors.length)]};
    opacity:0.6;
    animation-duration:${Math.random()*12+8}s;
    animation-delay:${Math.random()*4}s;
    box-shadow:0 0 6px currentColor;
  `;
  document.body.appendChild(p);
  setTimeout(() => p.remove(), 20000);
}
setInterval(spawnParticle, 800);

// ── Reveal on scroll
const reveals = document.querySelectorAll('section, .about-card, .stat-card, .skill-tag, .game-card');
const revObs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.style.opacity = '1';
      e.target.style.transform = 'translateY(0)';
    }
  });
}, { threshold: 0.05 });
reveals.forEach(el => {
  el.style.opacity = '0';
  el.style.transform = 'translateY(30px)';
  el.style.transition = 'opacity 0.7s ease, transform 0.7s cubic-bezier(0.23,1,0.32,1)';
  revObs.observe(el);
});
</script>
</body>
</html>
