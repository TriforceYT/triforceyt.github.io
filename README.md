<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>FUNCAPP TECH – GitHub</title>
  <link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;800&display=swap" rel="stylesheet" />
  <style>
    :root {
      --bg: #0a0a0f;
      --surface: #13131c;
      --card: #1a1a28;
      --accent: #00e5a0;
      --accent2: #7c4dff;
      --accent3: #ff4d6d;
      --text: #f0f0f8;
      --muted: #6b6b8a;
      --border: rgba(255,255,255,0.07);
      --glow: 0 0 40px rgba(0,229,160,0.15);
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'Syne', sans-serif;
      min-height: 100vh;
      overflow-x: hidden;
    }

    /* ── Grid background ── */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image:
        linear-gradient(rgba(0,229,160,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(0,229,160,0.03) 1px, transparent 1px);
      background-size: 60px 60px;
      pointer-events: none;
      z-index: 0;
      animation: gridShift 20s linear infinite;
    }
    @keyframes gridShift {
      from { background-position: 0 0; }
      to   { background-position: 60px 60px; }
    }

    /* ── Canvas for particles ── */
    #particles-canvas {
      position: fixed;
      inset: 0;
      pointer-events: none;
      z-index: 0;
    }

    /* ── Blobs ── */
    .blob {
      position: fixed;
      border-radius: 50%;
      filter: blur(80px);
      opacity: 0.18;
      pointer-events: none;
      z-index: 0;
      animation: drift 12s ease-in-out infinite alternate;
    }
    .blob-1 { width: 500px; height: 500px; background: var(--accent2); top: -100px; left: -150px; animation-delay: 0s; }
    .blob-2 { width: 400px; height: 400px; background: var(--accent);  bottom: -80px; right: -100px; animation-delay: -4s; }
    .blob-3 { width: 300px; height: 300px; background: var(--accent3); top: 50%;    left: 60%;    animation-delay: -8s; }
    @keyframes drift {
      from { transform: translate(0, 0) scale(1); }
      to   { transform: translate(30px, 20px) scale(1.08); }
    }

    /* ── Layout ── */
    .wrapper {
      position: relative;
      z-index: 1;
      max-width: 860px;
      margin: 0 auto;
      padding: 60px 24px 80px;
    }

    /* ── Reveal animation ── */
    .reveal {
      opacity: 0;
      transform: translateY(32px);
      transition: opacity .7s cubic-bezier(.16,1,.3,1), transform .7s cubic-bezier(.16,1,.3,1);
    }
    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }

    /* ── Header ── */
    header {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 14px;
      margin-bottom: 56px;
      text-align: center;
    }

    /* Glitch text effect */
    h1 {
      font-size: clamp(2.4rem, 6vw, 4rem);
      font-weight: 800;
      line-height: 1;
      letter-spacing: -.02em;
      background: linear-gradient(135deg, #fff 0%, var(--accent) 60%, var(--accent2) 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      position: relative;
      animation: titleReveal 1s cubic-bezier(.16,1,.3,1) both;
    }
    @keyframes titleReveal {
      from { opacity: 0; transform: scale(.92) translateY(20px); filter: blur(8px); }
      to   { opacity: 1; transform: scale(1) translateY(0);     filter: blur(0); }
    }

    /* Typewriter subtitle */
    .subtitle {
      font-size: 1.05rem;
      color: var(--muted);
      max-width: 400px;
      overflow: hidden;
      white-space: nowrap;
      border-right: 2px solid var(--accent);
      width: 0;
      animation: typeIn 1.4s steps(46, end) .8s forwards, blinkCursor .7s step-end .8s 4;
    }
    @keyframes typeIn    { from { width: 0 } to { width: 100%; border-right-color: transparent; } }
    @keyframes blinkCursor { 50% { border-right-color: transparent; } }

    /* ── Slider container ── */
    .slider-label {
      font-family: 'Space Mono', monospace;
      font-size: .7rem;
      letter-spacing: .18em;
      color: var(--muted);
      text-transform: uppercase;
      margin-bottom: 20px;
      display: flex;
      align-items: center;
      gap: 10px;
    }
    .slider-label::after {
      content: '';
      flex: 1;
      height: 1px;
      background: var(--border);
      animation: expandLine 1s ease forwards;
      transform-origin: left;
    }
    @keyframes expandLine { from { transform: scaleX(0); } to { transform: scaleX(1); } }

    .slider-box {
      position: relative;
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 24px;
      overflow: hidden;
      box-shadow: var(--glow), 0 24px 60px rgba(0,0,0,0.5);
      aspect-ratio: 16/7;
      min-height: 220px;
      transition: box-shadow .4s;
    }
    .slider-box:hover {
      box-shadow: 0 0 60px rgba(0,229,160,.25), 0 24px 60px rgba(0,0,0,.5);
    }

    /* ── Slides ── */
    .slides-track {
      display: flex;
      height: 100%;
      transition: transform .65s cubic-bezier(.77,0,.18,1);
      will-change: transform;
    }

    .slide {
      flex: 0 0 100%;
      position: relative;
      display: flex;
      align-items: center;
      padding: 40px 52px;
      gap: 36px;
      overflow: hidden;
    }

    .slide-1 { background: linear-gradient(135deg, #0f0f1e 0%, #1a1030 50%, #0d1a2e 100%); }
    .slide-1 .bg-shape { position: absolute; inset: 0; overflow: hidden; pointer-events: none; }
    .slide-1 .bg-shape::before {
      content: ''; position: absolute;
      width: 400px; height: 400px;
      border-radius: 50%;
      border: 1px solid rgba(124,77,255,.15);
      top: -100px; right: -80px;
      animation: spinRing 20s linear infinite;
    }
    .slide-1 .bg-shape::after {
      content: ''; position: absolute;
      width: 250px; height: 250px;
      border-radius: 50%;
      border: 1px solid rgba(0,229,160,.12);
      bottom: -60px; left: 30%;
      animation: spinRing 14s linear infinite reverse;
    }

    .slide-2 { background: linear-gradient(135deg, #0e1a14 0%, #0a1f18 50%, #061210 100%); }
    .slide-2 .bg-shape { position: absolute; inset: 0; overflow: hidden; pointer-events: none; }
    .slide-2 .bg-shape::before {
      content: ''; position: absolute;
      width: 350px; height: 350px;
      background: radial-gradient(circle, rgba(0,229,160,.07) 0%, transparent 70%);
      top: -50px; right: 10%;
      animation: breathe 4s ease-in-out infinite;
    }
    .slide-2 .bg-shape::after {
      content: ''; position: absolute;
      width: 200px; height: 200px;
      border-radius: 50%;
      border: 1px solid rgba(0,229,160,.1);
      bottom: -40px; left: 10%;
      animation: spinRing 10s linear infinite;
    }

    @keyframes spinRing  { to { transform: rotate(360deg); } }
    @keyframes breathe   { 0%,100%{opacity:.6;transform:scale(1)} 50%{opacity:1;transform:scale(1.15)} }

    /* Slide content */
    .slide-icon {
      flex-shrink: 0;
      width: 80px; height: 80px;
      border-radius: 20px;
      display: flex; align-items: center; justify-content: center;
      font-size: 2.2rem;
      position: relative; z-index: 1;
      animation: iconFloat 3s ease-in-out infinite;
    }
    @keyframes iconFloat { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-6px)} }
    .slide-1 .slide-icon {
      background: linear-gradient(135deg, #7c4dff22, #7c4dff44);
      border: 1px solid rgba(124,77,255,.3);
      box-shadow: 0 0 30px rgba(124,77,255,.25);
    }
    .slide-2 .slide-icon {
      background: linear-gradient(135deg, #00e5a022, #00e5a044);
      border: 1px solid rgba(0,229,160,.3);
      box-shadow: 0 0 30px rgba(0,229,160,.25);
    }

    .slide-content { flex: 1; position: relative; z-index: 1; }
    .slide-tag {
      display: inline-block;
      font-family: 'Space Mono', monospace;
      font-size: .65rem;
      letter-spacing: .15em;
      text-transform: uppercase;
      padding: 4px 12px;
      border-radius: 100px;
      margin-bottom: 12px;
    }
    .slide-1 .slide-tag { background: rgba(124,77,255,.15); color: #a67fff; border: 1px solid rgba(124,77,255,.25); }
    .slide-2 .slide-tag { background: rgba(0,229,160,.12); color: var(--accent); border: 1px solid rgba(0,229,160,.2); }

    .slide-title {
      font-size: clamp(1.3rem, 3vw, 1.9rem);
      font-weight: 800; line-height: 1.1; margin-bottom: 8px;
    }
    .slide-1 .slide-title { color: #e0d4ff; }
    .slide-2 .slide-title { color: #c8fff0; }

    .slide-desc {
      font-size: .88rem;
      color: var(--muted);
      margin-bottom: 22px;
      line-height: 1.5;
      max-width: 340px;
    }

    .slide-btn {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 10px 22px;
      border-radius: 100px;
      font-family: 'Syne', sans-serif;
      font-weight: 600;
      font-size: .82rem;
      text-decoration: none;
      transition: transform .2s, box-shadow .2s, opacity .2s;
      cursor: pointer;
      position: relative;
      overflow: hidden;
    }
    /* Shimmer on button */
    .slide-btn::after {
      content: '';
      position: absolute;
      top: 0; left: -100%;
      width: 60%;
      height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,.25), transparent);
      transform: skewX(-20deg);
      transition: left .5s;
    }
    .slide-btn:hover::after { left: 160%; }
    .slide-btn:hover { transform: translateY(-2px); }
    .slide-btn:active { transform: translateY(0); }
    .slide-1 .slide-btn {
      background: linear-gradient(135deg, #7c4dff, #a67fff);
      color: #fff;
      box-shadow: 0 4px 20px rgba(124,77,255,.4);
    }
    .slide-2 .slide-btn {
      background: linear-gradient(135deg, #00e5a0, #00c882);
      color: #061210;
      box-shadow: 0 4px 20px rgba(0,229,160,.35);
    }

    /* Phone mockup */
    .slide-mockup { flex-shrink: 0; width: 90px; position: relative; z-index: 1; }
    .phone {
      width: 70px; height: 120px;
      border-radius: 14px;
      position: relative;
      margin: 0 auto;
      animation: phoneTilt 4s ease-in-out infinite alternate;
    }
    @keyframes phoneTilt { from{transform:rotate(-3deg)} to{transform:rotate(3deg)} }
    .slide-1 .phone {
      background: linear-gradient(160deg,#3d2080,#1e0f4a);
      border: 1.5px solid rgba(124,77,255,.4);
      box-shadow: 0 8px 30px rgba(124,77,255,.3);
    }
    .slide-2 .phone {
      background: linear-gradient(160deg,#003d2a,#001a12);
      border: 1.5px solid rgba(0,229,160,.35);
      box-shadow: 0 8px 30px rgba(0,229,160,.25);
    }
    .phone::before {
      content: '';
      position: absolute;
      top: 8px; left: 50%; transform: translateX(-50%);
      width: 28px; height: 4px;
      background: rgba(255,255,255,.15);
      border-radius: 10px;
    }
    .phone-screen {
      position: absolute;
      inset: 16px 6px 8px;
      border-radius: 6px;
      display: flex; flex-direction: column;
      align-items: center; justify-content: center;
      gap: 5px;
    }
    .slide-1 .phone-screen { background: linear-gradient(160deg,#1e0f4a,#150833); }
    .slide-2 .phone-screen { background: linear-gradient(160deg,#001a12,#000e09); }
    .screen-dot { width: 22px; height: 22px; border-radius: 6px; animation: screenPulse 2s ease-in-out infinite; }
    .slide-1 .screen-dot { background: linear-gradient(135deg,#7c4dff,#a67fff); }
    .slide-2 .screen-dot { background: linear-gradient(135deg,#00e5a0,#00c882); }
    @keyframes screenPulse { 0%,100%{opacity:.8} 50%{opacity:1;transform:scale(1.05)} }
    .screen-line { height: 3px; border-radius: 10px; opacity: .3; animation: lineScan 2.4s ease-in-out infinite; }
    .slide-1 .screen-line { background: #a67fff; }
    .slide-2 .screen-line { background: #00e5a0; }
    .screen-line.w-full { width: 32px; }
    .screen-line.w-half { width: 22px; }
    @keyframes lineScan { 0%,100%{opacity:.15} 50%{opacity:.45} }

    /* ── Slider controls ── */
    .slider-controls {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 20px;
      margin-top: 22px;
    }
    .ctrl-btn {
      width: 40px; height: 40px;
      border-radius: 50%;
      background: var(--card);
      border: 1px solid var(--border);
      color: var(--text);
      cursor: pointer;
      display: flex; align-items: center; justify-content: center;
      font-size: 1rem;
      transition: background .2s, border-color .2s, transform .15s, box-shadow .2s;
      flex-shrink: 0;
    }
    .ctrl-btn:hover {
      background: var(--surface);
      border-color: rgba(255,255,255,.18);
      transform: scale(1.12);
      box-shadow: 0 0 16px rgba(0,229,160,.2);
    }
    .ctrl-btn:active { transform: scale(.92); }

    .dots { display: flex; gap: 8px; align-items: center; }
    .dot-ind {
      width: 8px; height: 8px;
      border-radius: 50%;
      background: var(--muted);
      cursor: pointer;
      transition: background .3s, width .3s, box-shadow .3s;
    }
    .dot-ind.active {
      background: var(--accent);
      width: 24px;
      border-radius: 4px;
      box-shadow: 0 0 8px rgba(0,229,160,.6);
    }

    /* Progress bar */
    .progress-bar {
      position: absolute;
      bottom: 0; left: 0;
      height: 3px;
      background: linear-gradient(90deg, var(--accent), var(--accent2));
      animation: progress 5s linear infinite;
      transform-origin: left;
    }
    @keyframes progress { from { width: 0 } to { width: 100% } }

    /* ── Footer links ── */
    .footer-links {
      margin-top: 52px;
      display: flex;
      gap: 16px;
      justify-content: center;
      flex-wrap: wrap;
    }
    .flink {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 10px 20px;
      border-radius: 100px;
      font-size: .82rem;
      font-weight: 600;
      text-decoration: none;
      background: var(--card);
      border: 1px solid var(--border);
      color: var(--muted);
      transition: color .2s, border-color .2s, transform .2s, box-shadow .2s;
      position: relative;
      overflow: hidden;
    }
    .flink::before {
      content: '';
      position: absolute;
      inset: 0;
      background: linear-gradient(135deg, rgba(0,229,160,.06), rgba(124,77,255,.06));
      opacity: 0;
      transition: opacity .3s;
    }
    .flink:hover { color: var(--text); border-color: rgba(255,255,255,.2); transform: translateY(-3px); box-shadow: 0 8px 24px rgba(0,0,0,.3); }
    .flink:hover::before { opacity: 1; }
    .flink svg { width: 16px; height: 16px; }

    /* ── Email button ── */
    .email-section {
      margin-top: 40px;
      display: flex;
      justify-content: center;
    }
    .email-btn {
      display: inline-flex;
      align-items: center;
      gap: 10px;
      padding: 14px 30px;
      border-radius: 100px;
      font-family: 'Syne', sans-serif;
      font-weight: 700;
      font-size: .9rem;
      text-decoration: none;
      background: linear-gradient(135deg, #ff4d6d, #ff7a4d);
      color: #fff;
      box-shadow: 0 4px 24px rgba(255,77,109,.35);
      transition: transform .2s, box-shadow .2s;
      position: relative;
      overflow: hidden;
    }
    .email-btn::after {
      content: '';
      position: absolute;
      top: 0; left: -100%;
      width: 60%;
      height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,.3), transparent);
      transform: skewX(-20deg);
      transition: left .6s;
    }
    .email-btn:hover { transform: translateY(-3px) scale(1.03); box-shadow: 0 10px 36px rgba(255,77,109,.55); }
    .email-btn:hover::after { left: 160%; }
    .email-btn:active { transform: translateY(0) scale(.98); }
    .email-btn svg { width: 18px; height: 18px; flex-shrink: 0; animation: mailWiggle 3s ease-in-out infinite; }
    @keyframes mailWiggle { 0%,100%{transform:rotate(0)} 20%{transform:rotate(-8deg)} 40%{transform:rotate(8deg)} 60%{transform:rotate(-4deg)} 80%{transform:rotate(4deg)} }

    /* ── Legal section ── */
    .legal-section {
      margin-top: 52px;
      border-top: 1px solid var(--border);
      padding-top: 36px;
    }
    .legal-title {
      font-family: 'Space Mono', monospace;
      font-size: .7rem;
      letter-spacing: .18em;
      color: var(--muted);
      text-transform: uppercase;
      margin-bottom: 20px;
      display: flex;
      align-items: center;
      gap: 10px;
    }
    .legal-title::after { content: ''; flex: 1; height: 1px; background: var(--border); }
    .legal-cards {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
    }
    .legal-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 24px 24px 20px;
      text-decoration: none;
      transition: border-color .3s, transform .3s, box-shadow .3s;
      display: block;
      transform-style: preserve-3d;
      will-change: transform;
    }
    .legal-card:hover {
      border-color: rgba(255,255,255,.18);
      transform: translateY(-6px) rotateX(3deg);
      box-shadow: 0 18px 40px rgba(0,0,0,.45);
    }
    .legal-card-icon {
      width: 40px; height: 40px;
      border-radius: 10px;
      display: flex; align-items: center; justify-content: center;
      font-size: 1.2rem;
      margin-bottom: 14px;
      transition: transform .3s;
    }
    .legal-card:hover .legal-card-icon { transform: scale(1.15) rotate(-5deg); }
    .legal-card:nth-child(1) .legal-card-icon { background: rgba(0,229,160,.1); border: 1px solid rgba(0,229,160,.2); }
    .legal-card:nth-child(2) .legal-card-icon { background: rgba(124,77,255,.1); border: 1px solid rgba(124,77,255,.2); }
    .legal-card-title { font-size: .95rem; font-weight: 700; color: var(--text); margin-bottom: 6px; }
    .legal-card-desc  { font-size: .78rem; color: var(--muted); line-height: 1.5; }
    .legal-card-arrow {
      margin-top: 14px; font-size: .75rem;
      display: flex; align-items: center; gap: 4px;
      transition: gap .2s;
    }
    .legal-card:hover .legal-card-arrow { gap: 10px; }
    .legal-card:nth-child(1) .legal-card-arrow { color: var(--accent); }
    .legal-card:nth-child(2) .legal-card-arrow { color: #a67fff; }

    /* ── Site footer ── */
    .site-footer {
      margin-top: 40px;
      text-align: center;
      font-family: 'Space Mono', monospace;
      font-size: .68rem;
      color: var(--muted);
      letter-spacing: .08em;
    }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* Responsive */
    @media (max-width: 560px) {
      .slide { padding: 28px; gap: 20px; }
      .slide-mockup { display: none; }
      .slide-icon { width: 60px; height: 60px; font-size: 1.6rem; }
      .slide-desc { display: none; }
      .legal-cards { grid-template-columns: 1fr; }
      .subtitle { white-space: normal; border-right: none; width: auto; animation: none; opacity: 1; }
    }
  </style>
</head>
<body>

  <canvas id="particles-canvas"></canvas>
  <div class="blob blob-1"></div>
  <div class="blob blob-2"></div>
  <div class="blob blob-3"></div>

  <div class="wrapper">

    <!-- Header -->
    <header>
      <h1>FUNCAPP TECH</h1>
      <p class="subtitle">Aplicaciones móviles funcionales con diseño excepcional</p>
    </header>

    <!-- Slider -->
    <div class="slider-wrapper reveal">
      <div class="slider-label">Nuestros proyectos</div>
      <div class="slider-box" id="sliderBox">
        <div class="slides-track" id="slidesTrack">

          <!-- Slide 1 -->
          <div class="slide slide-1">
            <div class="bg-shape"></div>
            <div class="slide-icon">🛍️</div>
            <div class="slide-content">
              <span class="slide-tag">Desarrollador</span>
              <div class="slide-title">FUNCAPP TECH<br>en Play Store</div>
              <p class="slide-desc">Descubre todas nuestras aplicaciones publicadas en Google Play Store.</p>
              <a class="slide-btn" href="https://play.google.com/store/apps/developer?id=FUNCAPP+TECH" target="_blank" rel="noopener">
                <svg viewBox="0 0 24 24" fill="currentColor" width="15" height="15"><path d="M3 20.5v-17c0-.83 1-1.3 1.6-.8l14 8.5c.53.32.53 1.08 0 1.4l-14 8.5c-.6.5-1.6.03-1.6-.8z"/></svg>
                Ver en Play Store
              </a>
            </div>
            <div class="slide-mockup">
              <div class="phone">
                <div class="phone-screen">
                  <div class="screen-dot"></div>
                  <div class="screen-line w-full"></div>
                  <div class="screen-line w-half"></div>
                  <div class="screen-line w-full"></div>
                </div>
              </div>
            </div>
          </div>

          <!-- Slide 2 -->
          <div class="slide slide-2">
            <div class="bg-shape"></div>
            <div class="slide-icon">📷</div>
            <div class="slide-content">
              <span class="slide-tag">App destacada</span>
              <div class="slide-title">GoScan<br>App</div>
              <p class="slide-desc">Escanea, digitaliza y gestiona documentos desde tu móvil de forma rápida.</p>
              <a class="slide-btn" href="https://play.google.com/store/apps/details?id=com.goscan" target="_blank" rel="noopener">
                <svg viewBox="0 0 24 24" fill="currentColor" width="15" height="15"><path d="M3 20.5v-17c0-.83 1-1.3 1.6-.8l14 8.5c.53.32.53 1.08 0 1.4l-14 8.5c-.6.5-1.6.03-1.6-.8z"/></svg>
                Descargar gratis
              </a>
            </div>
            <div class="slide-mockup">
              <div class="phone">
                <div class="phone-screen">
                  <div class="screen-dot"></div>
                  <div class="screen-line w-full"></div>
                  <div class="screen-line w-half"></div>
                  <div class="screen-line w-full"></div>
                </div>
              </div>
            </div>
          </div>

        </div>
        <div class="progress-bar" id="progressBar"></div>
      </div>

      <div class="slider-controls">
        <button class="ctrl-btn" id="prevBtn" aria-label="Anterior">&#8592;</button>
        <div class="dots">
          <div class="dot-ind active" data-idx="0"></div>
          <div class="dot-ind"       data-idx="1"></div>
        </div>
        <button class="ctrl-btn" id="nextBtn" aria-label="Siguiente">&#8594;</button>
      </div>
    </div>

    <!-- Footer links -->
    <div class="footer-links reveal">
      <a class="flink" href="https://play.google.com/store/apps/developer?id=FUNCAPP+TECH" target="_blank" rel="noopener">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2z"/><path d="M8 12l3-3 2 2 4-4"/></svg>
        Play Store Developer
      </a>
      <a class="flink" href="https://play.google.com/store/apps/details?id=com.goscan" target="_blank" rel="noopener">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="18" height="18" rx="2"/><path d="M9 9h6v6H9z"/></svg>
        GoScan App
      </a>
    </div>

    <!-- Email -->
    <div class="email-section reveal">
      <a class="email-btn" href="mailto:supportfuncapp@gmail.com">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <rect x="2" y="4" width="20" height="16" rx="2"/>
          <path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/>
        </svg>
        Contáctanos — supportfuncapp@gmail.com
      </a>
    </div>

    <!-- Legal -->
    <div class="legal-section reveal">
      <div class="legal-title">Legal</div>
      <div class="legal-cards">
        <a class="legal-card" href="privacy-policy.html">
          <div class="legal-card-icon">🔒</div>
          <div class="legal-card-title">Política de Privacidad</div>
          <div class="legal-card-desc">Cómo recopilamos, usamos y protegemos tu información personal.</div>
          <div class="legal-card-arrow">Leer documento →</div>
        </a>
        <a class="legal-card" href="terms-of-service.html">
          <div class="legal-card-icon">📋</div>
          <div class="legal-card-title">Términos de Servicio</div>
          <div class="legal-card-desc">Condiciones de uso de nuestras aplicaciones y servicios.</div>
          <div class="legal-card-arrow">Leer documento →</div>
        </a>
      </div>
    </div>

    <div class="site-footer reveal">
      © 2025 FUNCAPP TECH · Todos los derechos reservados
    </div>

  </div>

  <script>
    /* ── Particles ── */
    (function(){
      const canvas = document.getElementById('particles-canvas');
      const ctx = canvas.getContext('2d');
      let W, H, particles = [];
      const COUNT = 55;
      const COLORS = ['#00e5a0','#7c4dff','#ff4d6d','#ffffff'];

      function resize(){ W = canvas.width = innerWidth; H = canvas.height = innerHeight; }
      window.addEventListener('resize', resize);
      resize();

      for(let i=0;i<COUNT;i++) particles.push({
        x: Math.random()*W, y: Math.random()*H,
        r: Math.random()*1.8+.4,
        vx: (Math.random()-.5)*.35,
        vy: (Math.random()-.5)*.35,
        color: COLORS[Math.floor(Math.random()*COLORS.length)],
        alpha: Math.random()*.5+.1
      });

      function draw(){
        ctx.clearRect(0,0,W,H);
        particles.forEach(p=>{
          ctx.beginPath();
          ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
          ctx.fillStyle = p.color;
          ctx.globalAlpha = p.alpha;
          ctx.fill();
          p.x += p.vx; p.y += p.vy;
          if(p.x<0||p.x>W) p.vx*=-1;
          if(p.y<0||p.y>H) p.vy*=-1;
        });
        ctx.globalAlpha = 1;
        requestAnimationFrame(draw);
      }
      draw();
    })();

    /* ── Scroll reveal ── */
    const revealEls = document.querySelectorAll('.reveal');
    const observer = new IntersectionObserver(entries => {
      entries.forEach((e, i) => {
        if(e.isIntersecting){
          e.target.style.transitionDelay = (i * .08) + 's';
          e.target.classList.add('visible');
        }
      });
    }, { threshold: .12 });
    revealEls.forEach(el => observer.observe(el));

    /* ── Slider ── */
    const track    = document.getElementById('slidesTrack');
    const dotEls   = document.querySelectorAll('.dot-ind');
    const progress = document.getElementById('progressBar');
    const total    = 2;
    let current    = 0;
    let timer;

    function goTo(idx){
      current = (idx + total) % total;
      track.style.transform = `translateX(-${current * 100}%)`;
      dotEls.forEach((d,i) => d.classList.toggle('active', i===current));
      resetTimer();
    }
    function resetTimer(){
      progress.style.animation = 'none';
      void progress.offsetWidth;
      progress.style.animation = 'progress 5s linear forwards';
      clearTimeout(timer);
      timer = setTimeout(() => goTo(current+1), 5000);
    }

    document.getElementById('nextBtn').addEventListener('click', () => goTo(current+1));
    document.getElementById('prevBtn').addEventListener('click', () => goTo(current-1));
    dotEls.forEach(d => d.addEventListener('click', () => goTo(+d.dataset.idx)));

    let startX = 0;
    const box = document.getElementById('sliderBox');
    box.addEventListener('touchstart', e => { startX = e.touches[0].clientX; }, {passive:true});
    box.addEventListener('touchend',   e => {
      const diff = startX - e.changedTouches[0].clientX;
      if(Math.abs(diff) > 40) goTo(diff>0 ? current+1 : current-1);
    });

    box.addEventListener('mouseenter', () => { clearTimeout(timer); progress.style.animationPlayState='paused'; });
    box.addEventListener('mouseleave', () => { progress.style.animationPlayState='running'; resetTimer(); });

    resetTimer();

    /* ── Cursor glow ── */
    let mouseX=0, mouseY=0;
    document.addEventListener('mousemove', e => { mouseX=e.clientX; mouseY=e.clientY; });
    const glow = document.createElement('div');
    Object.assign(glow.style, {
      position:'fixed', pointerEvents:'none', zIndex:'0',
      width:'400px', height:'400px',
      borderRadius:'50%',
      background:'radial-gradient(circle, rgba(0,229,160,.06) 0%, transparent 70%)',
      transform:'translate(-50%,-50%)',
      transition:'left .12s ease, top .12s ease',
    });
    document.body.appendChild(glow);
    setInterval(()=>{ glow.style.left=mouseX+'px'; glow.style.top=mouseY+'px'; }, 30);
  </script>
</body>
</html>
