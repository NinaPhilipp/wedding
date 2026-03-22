<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Our Wedding</title>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300;1,400&family=Jost:wght@200;300;400&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --sage: #7d9b76;
      --sage-light: #a8c5a0;
      --sage-dark: #4e6b4a;
      --cream: #f5f0e8;
      --cream-dark: #e8e0d0;
      --warm: #c9b99a;
      --text: #3a3228;
      --text-light: #7a6e62;
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }

    html { scroll-behavior: smooth; }

    body {
      font-family: 'Jost', sans-serif;
      background: var(--cream);
      color: var(--text);
      overflow-x: hidden;
    }

    /* ── NAV ── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex;
      justify-content: center;
      gap: 3rem;
      padding: 1.4rem 2rem;
      background: transparent;
      transition: background 0.4s;
    }
    nav.scrolled { background: rgba(245,240,232,0.92); backdrop-filter: blur(8px); }
    nav a {
      font-family: 'Jost', sans-serif;
      font-weight: 300;
      font-size: 0.75rem;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: #fff;
      text-decoration: none;
      transition: color 0.3s;
    }
    nav.scrolled a { color: var(--text); }
    nav a:hover { color: var(--sage-light); }
    nav.scrolled a:hover { color: var(--sage); }

    /* ── HERO ── */
    .hero {
      position: relative;
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
    }

    .hero-video {
      position: absolute;
      inset: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
      filter: brightness(0.55) saturate(0.85);
    }

    /* Fallback gradient when no video is provided */
    .hero-gradient {
      position: absolute;
      inset: 0;
      background: linear-gradient(
        160deg,
        #4e6b4a 0%,
        #7d9b76 35%,
        #a8c5a0 60%,
        #c9b99a 100%
      );
      filter: brightness(0.7);
    }

    .hero-overlay {
      position: absolute;
      inset: 0;
      background: linear-gradient(to bottom, rgba(0,0,0,0.1) 0%, rgba(0,0,0,0.35) 100%);
    }

    .hero-content {
      position: relative;
      text-align: center;
      color: #fff;
      padding: 2rem;
    }

    .hero-eyebrow {
      font-family: 'Jost', sans-serif;
      font-weight: 200;
      font-size: 0.7rem;
      letter-spacing: 0.4em;
      text-transform: uppercase;
      opacity: 0;
      transform: translateY(20px);
      animation: fadeUp 1s ease 0.3s forwards;
    }

    .hero-names {
      font-family: 'Cormorant Garamond', serif;
      font-weight: 300;
      font-size: clamp(4rem, 10vw, 9rem);
      line-height: 1;
      margin: 0.5rem 0;
      opacity: 0;
      transform: translateY(20px);
      animation: fadeUp 1.1s ease 0.6s forwards;
    }

    .hero-ampersand {
      font-style: italic;
      color: rgba(255,255,255,0.7);
    }

    .hero-date {
      font-family: 'Jost', sans-serif;
      font-weight: 200;
      font-size: 0.85rem;
      letter-spacing: 0.35em;
      text-transform: uppercase;
      margin-top: 1.2rem;
      opacity: 0;
      transform: translateY(20px);
      animation: fadeUp 1.1s ease 0.9s forwards;
    }

    .hero-divider {
      width: 60px;
      height: 1px;
      background: rgba(255,255,255,0.5);
      margin: 1.5rem auto;
      opacity: 0;
      animation: fadeUp 1s ease 1.1s forwards;
    }

    .hero-scroll {
      position: absolute;
      bottom: 2.5rem;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 0.5rem;
      color: rgba(255,255,255,0.6);
      font-size: 0.6rem;
      letter-spacing: 0.25em;
      text-transform: uppercase;
      animation: bounce 2s ease infinite 2s;
    }

    .hero-scroll::after {
      content: '';
      display: block;
      width: 1px;
      height: 40px;
      background: rgba(255,255,255,0.4);
    }

    @keyframes fadeUp {
      to { opacity: 1; transform: translateY(0); }
    }

    @keyframes bounce {
      0%, 100% { transform: translateX(-50%) translateY(0); }
      50% { transform: translateX(-50%) translateY(6px); }
    }

    /* ── SECTIONS SHARED ── */
    section { padding: 7rem 2rem; }

    .section-inner {
      max-width: 900px;
      margin: 0 auto;
    }

    .section-label {
      font-family: 'Jost', sans-serif;
      font-weight: 300;
      font-size: 0.65rem;
      letter-spacing: 0.35em;
      text-transform: uppercase;
      color: var(--sage);
      margin-bottom: 1rem;
    }

    .section-title {
      font-family: 'Cormorant Garamond', serif;
      font-weight: 300;
      font-size: clamp(2.5rem, 5vw, 4rem);
      line-height: 1.1;
      color: var(--text);
      margin-bottom: 2.5rem;
    }

    .section-title em {
      font-style: italic;
      color: var(--sage-dark);
    }

    .ornament {
      display: flex;
      align-items: center;
      gap: 1rem;
      margin-bottom: 3rem;
    }
    .ornament-line { flex: 1; height: 1px; background: var(--cream-dark); }
    .ornament-icon { font-size: 1.1rem; color: var(--warm); }

    /* ── COUNTDOWN ── */
    .countdown-section {
      background: var(--sage-dark);
      color: #fff;
      text-align: center;
    }

    .countdown-section .section-label { color: var(--sage-light); }
    .countdown-section .section-title { color: #fff; }

    .countdown-grid {
      display: flex;
      justify-content: center;
      gap: clamp(1.5rem, 4vw, 4rem);
      margin-top: 3rem;
      flex-wrap: wrap;
    }

    .countdown-item {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 0.5rem;
    }

    .countdown-number {
      font-family: 'Cormorant Garamond', serif;
      font-weight: 300;
      font-size: clamp(3.5rem, 7vw, 6rem);
      line-height: 1;
      color: #fff;
    }

    .countdown-label {
      font-family: 'Jost', sans-serif;
      font-weight: 200;
      font-size: 0.65rem;
      letter-spacing: 0.3em;
      text-transform: uppercase;
      color: var(--sage-light);
    }

    .countdown-sep {
      font-family: 'Cormorant Garamond', serif;
      font-size: 3rem;
      color: rgba(255,255,255,0.2);
      align-self: center;
      margin-bottom: 1.5rem;
    }

    /* ── LOCATION ── */
    .location-section { background: var(--cream); }

    .location-cards {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 2rem;
      margin-top: 3rem;
    }

    .location-card {
      background: #fff;
      border: 1px solid var(--cream-dark);
      padding: 2.5rem 2rem;
      position: relative;
      overflow: hidden;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
    }

    .location-card:hover {
      transform: translateY(-4px);
      box-shadow: 0 20px 60px rgba(78,107,74,0.1);
    }

    .location-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 3px; height: 100%;
      background: var(--sage);
    }

    .card-icon {
      font-size: 1.8rem;
      margin-bottom: 1rem;
    }

    .card-title {
      font-family: 'Cormorant Garamond', serif;
      font-weight: 400;
      font-size: 1.5rem;
      color: var(--text);
      margin-bottom: 0.5rem;
    }

    .card-subtitle {
      font-size: 0.75rem;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--sage);
      margin-bottom: 1rem;
    }

    .card-body {
      font-size: 0.9rem;
      line-height: 1.7;
      color: var(--text-light);
    }

    .card-link {
      display: inline-block;
      margin-top: 1.2rem;
      font-size: 0.7rem;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--sage-dark);
      text-decoration: none;
      border-bottom: 1px solid var(--sage-light);
      padding-bottom: 2px;
      transition: color 0.2s;
    }

    .card-link:hover { color: var(--sage); }

    /* ── TIMELINE ── */
    .timeline {
      display: flex;
      flex-direction: column;
      gap: 0;
      margin-top: 3rem;
      position: relative;
    }

    .timeline::before {
      content: '';
      position: absolute;
      left: 6.5rem;
      top: 0; bottom: 0;
      width: 1px;
      background: var(--cream-dark);
    }

    .timeline-item {
      display: flex;
      gap: 2rem;
      align-items: flex-start;
      padding: 1.5rem 0;
    }

    .timeline-time {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.1rem;
      color: var(--sage);
      min-width: 5rem;
      text-align: right;
      padding-top: 0.1rem;
    }

    .timeline-dot {
      width: 10px;
      height: 10px;
      background: var(--sage);
      border-radius: 50%;
      margin-top: 0.3rem;
      flex-shrink: 0;
      position: relative;
      z-index: 1;
    }

    .timeline-content { flex: 1; }

    .timeline-title {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.2rem;
      color: var(--text);
    }

    .timeline-desc {
      font-size: 0.85rem;
      color: var(--text-light);
      margin-top: 0.25rem;
      line-height: 1.6;
    }

    /* ── STAY ── */
    .stay-section { background: var(--cream-dark); }

    .hotel-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 1.5rem;
      margin-top: 3rem;
    }

    .hotel-card {
      background: var(--cream);
      padding: 2rem;
      border-bottom: 2px solid var(--sage);
      transition: background 0.3s;
    }

    .hotel-card:hover { background: #fff; }

    .hotel-tag {
      display: inline-block;
      font-size: 0.6rem;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      background: var(--sage-light);
      color: #fff;
      padding: 0.2rem 0.6rem;
      border-radius: 2px;
      margin-bottom: 0.8rem;
    }

    .hotel-tag.budget { background: var(--warm); }

    .hotel-name {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.4rem;
      color: var(--text);
      margin-bottom: 0.4rem;
    }

    .hotel-distance {
      font-size: 0.75rem;
      color: var(--sage);
      letter-spacing: 0.1em;
      margin-bottom: 0.8rem;
    }

    .hotel-desc {
      font-size: 0.85rem;
      color: var(--text-light);
      line-height: 1.6;
      margin-bottom: 1rem;
    }

    .hotel-price {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1rem;
      color: var(--text);
    }

    /* ── FOOTER ── */
    footer {
      background: var(--sage-dark);
      color: rgba(255,255,255,0.7);
      text-align: center;
      padding: 4rem 2rem;
    }

    .footer-names {
      font-family: 'Cormorant Garamond', serif;
      font-style: italic;
      font-size: 2.5rem;
      color: #fff;
      margin-bottom: 0.5rem;
    }

    .footer-date {
      font-size: 0.7rem;
      letter-spacing: 0.3em;
      text-transform: uppercase;
      color: var(--sage-light);
    }

    /* ── VIDEO UPLOAD HINT ── */
    .video-hint {
      position: absolute;
      bottom: 5rem;
      right: 2rem;
      background: rgba(255,255,255,0.15);
      backdrop-filter: blur(4px);
      border: 1px solid rgba(255,255,255,0.3);
      color: rgba(255,255,255,0.8);
      font-size: 0.7rem;
      letter-spacing: 0.1em;
      padding: 0.6rem 1rem;
      border-radius: 2px;
      display: flex;
      align-items: center;
      gap: 0.5rem;
      cursor: pointer;
    }

    /* ── RESPONSIVE ── */
    @media (max-width: 600px) {
      .timeline::before { left: 0; display: none; }
      .timeline-time { min-width: auto; text-align: left; }
      .timeline-item { flex-direction: column; gap: 0.5rem; }
      .timeline-dot { display: none; }
      nav { gap: 1.2rem; }
      nav a { font-size: 0.65rem; }
      .countdown-sep { display: none; }
    }
  </style>
</head>
<body>

<!-- NAV -->
<nav id="nav">
  <a href="#countdown">Datum</a>
  <a href="#location">Location</a>
  <a href="#ablauf">Ablauf</a>
  <a href="#stay">Unterkunft</a>
</nav>

<!-- HERO -->
<section class="hero">
  <!-- Replace src with your own video file -->
  <video class="hero-video" id="heroVideo" autoplay muted loop playsinline
    poster="https://images.unsplash.com/photo-1519741497674-611481863552?w=1920&q=80">
    <!-- <source src="YOUR_VIDEO.mp4" type="video/mp4"> -->
  </video>

  <!-- Fallback gradient shown when no video loads -->
  <div class="hero-gradient" id="heroGradient" style="display:none"></div>
  <div class="hero-overlay"></div>

  <div class="hero-content">
    <p class="hero-eyebrow">Wir heiraten</p>
    <h1 class="hero-names">
      Sophie<br>
      <span class="hero-ampersand">&</span><br>
      Jonas
    </h1>
    <div class="hero-divider"></div>
    <p class="hero-date">12. Juli 2025 · Toscana, Italien</p>
  </div>

  <div class="hero-scroll">Scroll</div>

  <!-- Video upload hint -->
  <label class="video-hint" for="videoUpload">
    🎬 Eigenes Video einfügen
  </label>
  <input type="file" id="videoUpload" accept="video/*" style="display:none" onchange="loadVideo(event)"/>
</section>

<!-- COUNTDOWN -->
<section class="countdown-section" id="countdown">
  <div class="section-inner" style="text-align:center">
    <p class="section-label">Noch nicht lange hin</p>
    <h2 class="section-title" style="color:#fff">Der große Tag</h2>
    <div class="countdown-grid" id="countdown-grid">
      <div class="countdown-item">
        <span class="countdown-number" id="cd-days">—</span>
        <span class="countdown-label">Tage</span>
      </div>
      <div class="countdown-sep">·</div>
      <div class="countdown-item">
        <span class="countdown-number" id="cd-hours">—</span>
        <span class="countdown-label">Stunden</span>
      </div>
      <div class="countdown-sep">·</div>
      <div class="countdown-item">
        <span class="countdown-number" id="cd-mins">—</span>
        <span class="countdown-label">Minuten</span>
      </div>
      <div class="countdown-sep">·</div>
      <div class="countdown-item">
        <span class="countdown-number" id="cd-secs">—</span>
        <span class="countdown-label">Sekunden</span>
      </div>
    </div>
  </div>
</section>

<!-- LOCATION & ABLAUF -->
<section class="location-section" id="location">
  <div class="section-inner">
    <p class="section-label">Wo wir feiern</p>
    <h2 class="section-title">Die <em>Location</em></h2>
    <div class="ornament">
      <div class="ornament-line"></div>
      <div class="ornament-icon">🌿</div>
      <div class="ornament-line"></div>
    </div>

    <div class="location-cards">
      <div class="location-card">
        <div class="card-icon">💒</div>
        <div class="card-title">Standesamt</div>
        <div class="card-subtitle">Zeremonie · 13:00 Uhr</div>
        <div class="card-body">
          Municipio di Montalcino<br>
          Piazza del Popolo 1<br>
          53024 Montalcino, Siena, Italien
        </div>
        <a href="https://maps.google.com" target="_blank" class="card-link">→ Auf Karte anzeigen</a>
      </div>

      <div class="location-card">
        <div class="card-icon">🍷</div>
        <div class="card-title">Feier & Empfang</div>
        <div class="card-subtitle">Abendessen · 17:00 Uhr</div>
        <div class="card-body">
          Tenuta di Casanova<br>
          Strada Provinciale 55, km 3<br>
          53024 Montalcino, Siena, Italien
        </div>
        <a href="https://maps.google.com" target="_blank" class="card-link">→ Auf Karte anzeigen</a>
      </div>
    </div>

    <!-- ABLAUF -->
    <div id="ablauf" style="margin-top:5rem">
      <p class="section-label">Was euch erwartet</p>
      <h2 class="section-title">Tages<em>ablauf</em></h2>
      <div class="ornament">
        <div class="ornament-line"></div>
        <div class="ornament-icon">✦</div>
        <div class="ornament-line"></div>
      </div>

      <div class="timeline">
        <div class="timeline-item">
          <div class="timeline-time">12:30</div>
          <div class="timeline-dot"></div>
          <div class="timeline-content">
            <div class="timeline-title">Ankommen & Aperitivo</div>
            <div class="timeline-desc">Empfang vor dem Standesamt mit Prosecco & kleinen Häppchen</div>
          </div>
        </div>
        <div class="timeline-item">
          <div class="timeline-time">13:00</div>
          <div class="timeline-dot"></div>
          <div class="timeline-content">
            <div class="timeline-title">Standesamtliche Trauung</div>
            <div class="timeline-desc">Die offizielle Zeremonie im historischen Municipio</div>
          </div>
        </div>
        <div class="timeline-item">
          <div class="timeline-time">14:30</div>
          <div class="timeline-dot"></div>
          <div class="timeline-content">
            <div class="timeline-title">Fotoshooting & freie Zeit</div>
            <div class="timeline-desc">Erkundet die Altstadt oder entspannt euch ein wenig</div>
          </div>
        </div>
        <div class="timeline-item">
          <div class="timeline-time">17:00</div>
          <div class="timeline-dot"></div>
          <div class="timeline-content">
            <div class="timeline-title">Empfang auf dem Weingut</div>
            <div class="timeline-desc">Aperitivo, Dinner & Tanzfläche unter freiem Himmel</div>
          </div>
        </div>
        <div class="timeline-item">
          <div class="timeline-time">23:00</div>
          <div class="timeline-dot"></div>
          <div class="timeline-content">
            <div class="timeline-title">Ende der offiziellen Feier</div>
            <div class="timeline-desc">Shuttles zurück zu den Hotels stehen bereit</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- WHERE TO STAY -->
<section class="stay-section" id="stay">
  <div class="section-inner">
    <p class="section-label">Wo ihr schlafen könnt</p>
    <h2 class="section-title">Unter<em>kunft</em></h2>
    <div class="ornament">
      <div class="ornament-line"></div>
      <div class="ornament-icon">🏡</div>
      <div class="ornament-line"></div>
    </div>

    <p style="color:var(--text-light);line-height:1.8;max-width:600px;margin-bottom:1rem;">
      Wir haben ein paar Unterkunftsmöglichkeiten für euch herausgesucht – von gemütlichen Agriturismos bis zum modernen Hotel. Bitte reserviert rechtzeitig, da die Region im Juli sehr beliebt ist.
    </p>

    <div class="hotel-grid">
      <div class="hotel-card">
        <span class="hotel-tag">Empfehlung</span>
        <div class="hotel-name">Agriturismo Poggio Salvi</div>
        <div class="hotel-distance">📍 3 km vom Weingut</div>
        <div class="hotel-desc">Charmantes Landhaus mit Pool, inmitten von Weinreben. Frühstück mit regionalen Produkten inklusive.</div>
        <div class="hotel-price">ab €140 / Nacht</div>
      </div>

      <div class="hotel-card">
        <span class="hotel-tag">Empfehlung</span>
        <div class="hotel-name">Hotel Il Giglio</div>
        <div class="hotel-distance">📍 im Ortszentrum Montalcino</div>
        <div class="hotel-desc">Gemütliches Hotel mit traumhaftem Blick über das Val d'Orcia. Fußläufig zum Standesamt.</div>
        <div class="hotel-price">ab €110 / Nacht</div>
      </div>

      <div class="hotel-card">
        <span class="hotel-tag budget">Budget-Tipp</span>
        <div class="hotel-name">La Terrazza di Gina</div>
        <div class="hotel-distance">📍 5 km entfernt</div>
        <div class="hotel-desc">Herzliche B&B-Atmosphäre mit herrlicher Terrasse. Ideal für alle, die das authentische Toskana-Flair suchen.</div>
        <div class="hotel-price">ab €75 / Nacht</div>
      </div>
    </div>

    <p style="margin-top:2rem;font-size:0.8rem;color:var(--text-light);">
      💌 Habt ihr Fragen zur Anreise oder Unterkunft? Schreibt uns: <a href="mailto:hochzeit@beispiel.de" style="color:var(--sage-dark);">hochzeit@beispiel.de</a>
    </p>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-names">Sophie & Jonas</div>
  <div class="footer-date">12. Juli 2025 · Toscana, Italien</div>
  <p style="margin-top:2rem;font-size:0.75rem;opacity:0.5;">Wir freuen uns auf euch 🌿</p>
</footer>

<script>
  // NAV scroll
  const nav = document.getElementById('nav');
  window.addEventListener('scroll', () => {
    nav.classList.toggle('scrolled', window.scrollY > 80);
  });

  // COUNTDOWN — set your wedding date here
  const weddingDate = new Date('2025-07-12T13:00:00');

  function updateCountdown() {
    const now = new Date();
    const diff = weddingDate - now;

    if (diff <= 0) {
      document.getElementById('cd-days').textContent = '0';
      document.getElementById('cd-hours').textContent = '0';
      document.getElementById('cd-mins').textContent = '0';
      document.getElementById('cd-secs').textContent = '0';
      return;
    }

    const days  = Math.floor(diff / 86400000);
    const hours = Math.floor((diff % 86400000) / 3600000);
    const mins  = Math.floor((diff % 3600000) / 60000);
    const secs  = Math.floor((diff % 60000) / 1000);

    document.getElementById('cd-days').textContent  = String(days).padStart(2,'0');
    document.getElementById('cd-hours').textContent = String(hours).padStart(2,'0');
    document.getElementById('cd-mins').textContent  = String(mins).padStart(2,'0');
    document.getElementById('cd-secs').textContent  = String(secs).padStart(2,'0');
  }

  updateCountdown();
  setInterval(updateCountdown, 1000);

  // VIDEO upload
  function loadVideo(event) {
    const file = event.target.files[0];
    if (!file) return;
    const url = URL.createObjectURL(file);
    const video = document.getElementById('heroVideo');
    video.style.display = 'block';
    document.getElementById('heroGradient').style.display = 'none';
    const source = document.createElement('source');
    source.src = url;
    source.type = file.type;
    video.innerHTML = '';
    video.appendChild(source);
    video.load();
    video.play();
  }
</script>

</body>
</html>
