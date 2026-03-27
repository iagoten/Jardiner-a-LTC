<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Jardinería LTC — Mantenimiento de Jardines</title>
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Nunito:wght@300;400;600;700&display=swap" rel="stylesheet">
  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --verde-oscuro: #2d5a00;
      --verde-medio: #4a8a00;
      --verde-claro: #8cc800;
      --verde-lima: #b8d840;
      --tierra: #6b3a10;
      --crema: #f5f2eb;
      --blanco: #ffffff;
      --negro: #111111;
      --gris-texto: #444;
    }

    html { scroll-behavior: smooth; }

    body {
      font-family: 'Nunito', sans-serif;
      background: var(--crema);
      color: var(--negro);
      overflow-x: hidden;
    }

    /* ─── NAVBAR ─── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      padding: 0 5%;
      height: 70px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      background: rgba(245,242,235,0.92);
      backdrop-filter: blur(10px);
      border-bottom: 1px solid rgba(74,138,0,0.15);
      transition: box-shadow 0.3s;
    }
    nav.scrolled { box-shadow: 0 4px 24px rgba(0,0,0,0.08); }

    .nav-logo {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 28px;
      letter-spacing: 3px;
      color: var(--verde-oscuro);
      text-decoration: none;
      display: flex;
      align-items: center;
      gap: 10px;
    }
    .nav-logo span {
      background: var(--verde-medio);
      color: white;
      padding: 2px 8px;
      border-radius: 4px;
      font-size: 22px;
    }

    .nav-links {
      display: flex;
      gap: 32px;
      list-style: none;
    }
    .nav-links a {
      text-decoration: none;
      font-size: 14px;
      font-weight: 600;
      color: var(--gris-texto);
      letter-spacing: 1px;
      text-transform: uppercase;
      position: relative;
      transition: color 0.2s;
    }
    .nav-links a::after {
      content: '';
      position: absolute;
      bottom: -4px; left: 0;
      width: 0; height: 2px;
      background: var(--verde-claro);
      transition: width 0.25s;
    }
    .nav-links a:hover { color: var(--verde-oscuro); }
    .nav-links a:hover::after { width: 100%; }

    .nav-tel {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 20px;
      letter-spacing: 2px;
      color: var(--verde-oscuro);
      text-decoration: none;
      border: 2px solid var(--verde-medio);
      padding: 6px 16px;
      border-radius: 6px;
      transition: all 0.2s;
    }
    .nav-tel:hover {
      background: var(--verde-medio);
      color: white;
    }

    /* ─── HERO ─── */
    #hero {
      min-height: 100vh;
      display: grid;
      grid-template-columns: 1fr 1fr;
      align-items: center;
      padding: 100px 6% 60px;
      gap: 40px;
      position: relative;
      overflow: hidden;
    }

    /* Fondo con patrón de hojas */
    #hero::before {
      content: '';
      position: absolute;
      inset: 0;
      background:
        radial-gradient(ellipse 70% 80% at 80% 50%, rgba(140,200,0,0.08) 0%, transparent 70%),
        radial-gradient(ellipse 40% 40% at 10% 80%, rgba(45,90,0,0.06) 0%, transparent 60%);
      pointer-events: none;
    }

    .hero-text { position: relative; z-index: 1; }

    .hero-badge {
      display: inline-block;
      background: var(--verde-claro);
      color: var(--verde-oscuro);
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 2px;
      text-transform: uppercase;
      padding: 6px 14px;
      border-radius: 20px;
      margin-bottom: 20px;
      opacity: 0;
      animation: fadeUp 0.6s 0.2s forwards;
    }

    .hero-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(52px, 7vw, 90px);
      line-height: 0.95;
      color: var(--negro);
      letter-spacing: 2px;
      margin-bottom: 24px;
      opacity: 0;
      animation: fadeUp 0.7s 0.35s forwards;
    }
    .hero-title .green { color: var(--verde-medio); }
    .hero-title .outline {
      -webkit-text-stroke: 2px var(--verde-oscuro);
      color: transparent;
    }

    .hero-desc {
      font-size: 17px;
      line-height: 1.7;
      color: var(--gris-texto);
      max-width: 480px;
      margin-bottom: 36px;
      font-weight: 300;
      opacity: 0;
      animation: fadeUp 0.7s 0.5s forwards;
    }

    .hero-btns {
      display: flex;
      gap: 14px;
      flex-wrap: wrap;
      opacity: 0;
      animation: fadeUp 0.7s 0.65s forwards;
    }

    .btn-primary {
      background: var(--verde-medio);
      color: white;
      font-family: 'Nunito', sans-serif;
      font-size: 15px;
      font-weight: 700;
      padding: 14px 32px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      text-decoration: none;
      transition: background 0.2s, transform 0.15s;
      letter-spacing: 0.5px;
    }
    .btn-primary:hover { background: var(--verde-oscuro); transform: translateY(-2px); }

    .btn-secondary {
      background: transparent;
      color: var(--verde-oscuro);
      font-family: 'Nunito', sans-serif;
      font-size: 15px;
      font-weight: 700;
      padding: 14px 32px;
      border: 2px solid var(--verde-medio);
      border-radius: 8px;
      cursor: pointer;
      text-decoration: none;
      transition: all 0.2s;
    }
    .btn-secondary:hover { background: var(--verde-medio); color: white; transform: translateY(-2px); }

    /* Tarjeta 3D hero */
    .hero-card-area {
      display: flex;
      align-items: center;
      justify-content: center;
      perspective: 1000px;
      position: relative;
      z-index: 1;
      opacity: 0;
      animation: fadeIn 1s 0.8s forwards;
    }

    .card-wrap {
      width: 400px;
      height: 245px;
      transform-style: preserve-3d;
      transform: rotateY(-18deg) rotateX(8deg);
      cursor: pointer;
      filter: drop-shadow(0px 30px 45px rgba(0,0,0,0.3)) drop-shadow(0px 10px 18px rgba(0,0,0,0.18));
      transition: filter 0.3s;
    }
    .card-wrap:hover {
      filter: drop-shadow(0px 40px 60px rgba(0,0,0,0.38)) drop-shadow(0px 14px 22px rgba(0,0,0,0.22));
    }
    .card-face {
      position: absolute; inset: 0;
      border-radius: 14px;
      backface-visibility: hidden;
      overflow: hidden;
    }
    .card-front { display: flex; flex-direction: column; background: #d8dbd5; }
    .card-back {
      background: linear-gradient(135deg, #2a2a2a, #1a1a1a);
      transform: rotateY(180deg);
      display: flex; align-items: center; justify-content: center;
    }
    .card-back-inner { color: #444; font-size: 12px; letter-spacing: 3px; text-transform: uppercase; font-family: 'Bebas Neue', sans-serif; }
    .card-shine {
      position: absolute; inset: 0; border-radius: 14px;
      pointer-events: none; z-index: 20;
      background: linear-gradient(125deg, rgba(255,255,255,0.15) 0%, rgba(255,255,255,0) 50%);
    }
    .top-section {
      flex: 1.15;
      background: linear-gradient(175deg, #f8f8f6 55%, #ddddd8 100%);
      display: flex; flex-direction: column;
      align-items: center; justify-content: center;
      padding: 10px 16px 4px;
    }
    .brand-jardineria {
      font-family: Impact, 'Arial Narrow', Arial, sans-serif;
      font-size: 27px; font-weight: 900; color: white;
      letter-spacing: 3px; text-transform: uppercase; line-height: 1;
      -webkit-text-stroke: 2.5px #111;
      text-shadow: 3px 3px 0 rgba(0,0,0,0.15);
      margin-bottom: -4px;
    }
    .logo-ltc {
      font-family: Impact, 'Arial Narrow', Arial, sans-serif;
      font-size: 82px; font-weight: 900; color: white;
      line-height: 0.9; letter-spacing: -3px;
      -webkit-text-stroke: 4px #111;
      text-shadow: 5px 5px 0 rgba(0,0,0,0.15);
    }
    .bottom-section {
      flex: 1;
      background: linear-gradient(180deg, #b8d840 0%, #8ab818 55%, #5a8000 100%);
      position: relative; display: flex; align-items: stretch; overflow: hidden;
    }
    .grass-top { position: absolute; top: -2px; left: 0; right: 0; height: 20px; z-index: 2; }
    .tree-col {
      width: 80px; display: flex; align-items: flex-end;
      justify-content: center; flex-shrink: 0; position: relative; z-index: 1;
    }
    .info-col {
      flex: 1; display: flex; flex-direction: column; justify-content: center;
      padding: 22px 12px 10px 4px; z-index: 1;
    }
    .card-services {
      font-size: 9.5px; font-weight: 700; color: #1c3800;
      letter-spacing: 0.3px; line-height: 1.6; text-transform: uppercase;
    }
    .card-phone {
      font-family: Impact, 'Arial Narrow', Arial, sans-serif;
      font-size: 22px; color: white; letter-spacing: 1px; margin-top: 4px;
      -webkit-text-stroke: 0.5px rgba(0,0,0,0.4);
      text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
    }
    .card-edge-r {
      position: absolute; right: -7px; top: 5px; bottom: 5px; width: 7px;
      background: linear-gradient(to right, #aaa, #777);
      transform: rotateY(90deg) translateZ(3.5px); transform-origin: left;
      border-radius: 0 2px 2px 0;
    }
    .card-edge-b {
      position: absolute; bottom: -5px; left: 5px; right: 5px; height: 5px;
      background: linear-gradient(to bottom, #aaa, #777);
      transform: rotateX(-90deg) translateZ(2.5px); transform-origin: top;
      border-radius: 0 0 2px 2px;
    }

    /* Césped decorativo hero */
    .hero-grass {
      position: absolute;
      bottom: 0; left: 0; right: 0;
      height: 80px;
      pointer-events: none;
    }

    /* ─── STATS ─── */
    #stats {
      background: var(--verde-oscuro);
      padding: 50px 6%;
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 20px;
    }
    .stat-item {
      text-align: center;
      color: white;
      padding: 20px;
      border-right: 1px solid rgba(255,255,255,0.1);
    }
    .stat-item:last-child { border-right: none; }
    .stat-num {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 56px;
      color: var(--verde-lima);
      line-height: 1;
      display: block;
    }
    .stat-label {
      font-size: 13px;
      font-weight: 600;
      letter-spacing: 1.5px;
      text-transform: uppercase;
      opacity: 0.75;
      margin-top: 6px;
    }

    /* ─── SERVICIOS ─── */
    #servicios {
      padding: 100px 6%;
      background: var(--crema);
    }

    .section-header {
      text-align: center;
      margin-bottom: 64px;
    }
    .section-tag {
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 3px;
      text-transform: uppercase;
      color: var(--verde-medio);
      display: block;
      margin-bottom: 12px;
    }
    .section-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(36px, 5vw, 56px);
      letter-spacing: 2px;
      line-height: 1;
      color: var(--negro);
    }
    .section-title .green { color: var(--verde-medio); }

    .servicios-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 24px;
    }

    .servicio-card {
      background: white;
      border-radius: 16px;
      padding: 36px 28px;
      border: 1px solid rgba(74,138,0,0.12);
      transition: transform 0.25s, box-shadow 0.25s, border-color 0.25s;
      position: relative;
      overflow: hidden;
    }
    .servicio-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0;
      height: 4px;
      background: linear-gradient(90deg, var(--verde-medio), var(--verde-lima));
      transform: scaleX(0);
      transform-origin: left;
      transition: transform 0.3s;
    }
    .servicio-card:hover {
      transform: translateY(-6px);
      box-shadow: 0 20px 50px rgba(45,90,0,0.12);
      border-color: rgba(74,138,0,0.25);
    }
    .servicio-card:hover::before { transform: scaleX(1); }

    .servicio-icon {
      width: 64px; height: 64px;
      background: linear-gradient(135deg, var(--verde-lima), var(--verde-claro));
      border-radius: 16px;
      display: flex; align-items: center; justify-content: center;
      margin-bottom: 20px;
      font-size: 28px;
    }
    .servicio-card h3 {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 24px;
      letter-spacing: 1px;
      color: var(--negro);
      margin-bottom: 10px;
    }
    .servicio-card p {
      font-size: 14px;
      line-height: 1.7;
      color: var(--gris-texto);
      font-weight: 300;
    }

    /* ─── POR QUÉ NOSOTROS ─── */
    #nosotros {
      padding: 100px 6%;
      background: white;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 80px;
      align-items: center;
    }

    .nosotros-visual {
      position: relative;
    }
    .nosotros-img-box {
      width: 100%;
      aspect-ratio: 4/3;
      background: linear-gradient(135deg, var(--verde-oscuro) 0%, var(--verde-medio) 50%, var(--verde-lima) 100%);
      border-radius: 20px;
      overflow: hidden;
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .nosotros-img-box svg {
      width: 80%;
      opacity: 0.25;
    }
    .nosotros-badge-float {
      position: absolute;
      bottom: -20px;
      right: -20px;
      background: var(--verde-lima);
      border-radius: 16px;
      padding: 20px 24px;
      box-shadow: 0 12px 30px rgba(0,0,0,0.15);
    }
    .nosotros-badge-float .big { font-family: 'Bebas Neue', sans-serif; font-size: 42px; color: var(--verde-oscuro); line-height: 1; }
    .nosotros-badge-float .small { font-size: 11px; font-weight: 700; letter-spacing: 1px; text-transform: uppercase; color: var(--verde-oscuro); opacity: 0.7; }

    .nosotros-text {}
    .nosotros-text .section-header { text-align: left; margin-bottom: 32px; }

    .check-list { list-style: none; display: flex; flex-direction: column; gap: 16px; margin-bottom: 36px; }
    .check-list li {
      display: flex;
      align-items: flex-start;
      gap: 14px;
      font-size: 15px;
      line-height: 1.5;
      color: var(--gris-texto);
    }
    .check-list li::before {
      content: '✓';
      flex-shrink: 0;
      width: 26px; height: 26px;
      background: var(--verde-claro);
      color: var(--verde-oscuro);
      font-weight: 900;
      font-size: 13px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-top: 1px;
    }

    /* ─── PROCESO ─── */
    #proceso {
      padding: 100px 6%;
      background: var(--crema);
    }

    .proceso-steps {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 16px;
      margin-top: 60px;
      position: relative;
    }
    .proceso-steps::before {
      content: '';
      position: absolute;
      top: 36px;
      left: 10%;
      right: 10%;
      height: 2px;
      background: linear-gradient(90deg, var(--verde-medio), var(--verde-lima));
      z-index: 0;
    }

    .paso {
      text-align: center;
      position: relative;
      z-index: 1;
      padding: 0 12px;
    }
    .paso-num {
      width: 72px; height: 72px;
      background: white;
      border: 3px solid var(--verde-medio);
      border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      margin: 0 auto 20px;
      font-family: 'Bebas Neue', sans-serif;
      font-size: 28px;
      color: var(--verde-oscuro);
      box-shadow: 0 4px 16px rgba(74,138,0,0.15);
    }
    .paso h4 {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 20px;
      letter-spacing: 1px;
      color: var(--negro);
      margin-bottom: 8px;
    }
    .paso p {
      font-size: 13px;
      line-height: 1.6;
      color: var(--gris-texto);
      font-weight: 300;
    }

    /* ─── CONTACTO ─── */
    #contacto {
      padding: 100px 6%;
      background: var(--verde-oscuro);
      position: relative;
      overflow: hidden;
    }
    #contacto::before {
      content: '';
      position: absolute;
      top: -100px; right: -100px;
      width: 500px; height: 500px;
      border-radius: 50%;
      background: rgba(140,200,0,0.06);
      pointer-events: none;
    }

    .contacto-inner {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 80px;
      align-items: center;
      position: relative;
      z-index: 1;
    }

    .contacto-info .section-tag { color: var(--verde-lima); }
    .contacto-info .section-title { color: white; }

    .contacto-desc {
      font-size: 16px;
      line-height: 1.7;
      color: rgba(255,255,255,0.65);
      font-weight: 300;
      margin-top: 20px;
      margin-bottom: 36px;
    }

    .contact-items { display: flex; flex-direction: column; gap: 18px; }
    .contact-item {
      display: flex;
      align-items: center;
      gap: 14px;
      color: white;
    }
    .contact-icon {
      width: 44px; height: 44px;
      background: rgba(255,255,255,0.08);
      border-radius: 10px;
      display: flex; align-items: center; justify-content: center;
      font-size: 18px;
      flex-shrink: 0;
    }
    .contact-item .label {
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 1.5px;
      text-transform: uppercase;
      opacity: 0.55;
      display: block;
      margin-bottom: 2px;
    }
    .contact-item .value {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 20px;
      letter-spacing: 1.5px;
      color: white;
    }

    /* Formulario */
    .contacto-form {
      background: rgba(255,255,255,0.06);
      border: 1px solid rgba(255,255,255,0.1);
      border-radius: 20px;
      padding: 40px 36px;
    }

    .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin-bottom: 16px; }
    .form-group { display: flex; flex-direction: column; gap: 8px; margin-bottom: 16px; }

    .form-group label {
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 1.5px;
      text-transform: uppercase;
      color: rgba(255,255,255,0.55);
    }
    .form-row .form-group { margin-bottom: 0; }

    .form-group input,
    .form-group textarea,
    .form-group select {
      background: rgba(255,255,255,0.07);
      border: 1px solid rgba(255,255,255,0.12);
      border-radius: 8px;
      padding: 12px 16px;
      font-family: 'Nunito', sans-serif;
      font-size: 14px;
      color: white;
      outline: none;
      transition: border-color 0.2s, background 0.2s;
      width: 100%;
    }
    .form-group input::placeholder,
    .form-group textarea::placeholder { color: rgba(255,255,255,0.3); }
    .form-group input:focus,
    .form-group textarea:focus,
    .form-group select:focus {
      border-color: var(--verde-lima);
      background: rgba(255,255,255,0.1);
    }
    .form-group select option { background: #2d5a00; color: white; }
    .form-group textarea { resize: vertical; min-height: 100px; }

    .btn-send {
      width: 100%;
      background: linear-gradient(90deg, var(--verde-medio), var(--verde-claro));
      color: white;
      font-family: 'Bebas Neue', sans-serif;
      font-size: 18px;
      letter-spacing: 2px;
      padding: 16px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: opacity 0.2s, transform 0.15s;
      margin-top: 8px;
    }
    .btn-send:hover { opacity: 0.9; transform: translateY(-2px); }

    /* ─── FOOTER ─── */
    footer {
      background: #0d1f00;
      padding: 40px 6%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 16px;
    }
    .footer-logo {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 22px;
      letter-spacing: 3px;
      color: var(--verde-lima);
    }
    .footer-copy {
      font-size: 12px;
      color: rgba(255,255,255,0.3);
      letter-spacing: 0.5px;
    }
    .footer-links { display: flex; gap: 24px; }
    .footer-links a {
      font-size: 12px;
      font-weight: 600;
      letter-spacing: 1px;
      text-transform: uppercase;
      color: rgba(255,255,255,0.4);
      text-decoration: none;
      transition: color 0.2s;
    }
    .footer-links a:hover { color: var(--verde-lima); }

    /* ─── ANIMACIONES ─── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    @keyframes fadeIn {
      from { opacity: 0; }
      to   { opacity: 1; }
    }

    .reveal {
      opacity: 0;
      transform: translateY(30px);
      transition: opacity 0.65s ease, transform 0.65s ease;
    }
    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }

    /* ─── RESPONSIVE ─── */
    @media (max-width: 900px) {
      #hero { grid-template-columns: 1fr; text-align: center; padding-top: 100px; }
      .hero-btns { justify-content: center; }
      .hero-card-area { display: none; }
      #stats { grid-template-columns: repeat(2,1fr); }
      .stat-item { border-right: none; border-bottom: 1px solid rgba(255,255,255,0.1); }
      .servicios-grid { grid-template-columns: 1fr; }
      #nosotros { grid-template-columns: 1fr; }
      .proceso-steps { grid-template-columns: repeat(2,1fr); }
      .proceso-steps::before { display: none; }
      .contacto-inner { grid-template-columns: 1fr; }
      .nav-links { display: none; }
      .form-row { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>

<!-- NAVBAR -->
<nav id="navbar">
  <a href="#hero" class="nav-logo">Jardinería <span>LTC</span></a>
  <ul class="nav-links">
    <li><a href="#servicios">Servicios</a></li>
    <li><a href="#nosotros">Nosotros</a></li>
    <li><a href="#proceso">Cómo trabajamos</a></li>
    <li><a href="#contacto">Contacto</a></li>
  </ul>
  <a href="tel:629442013" class="nav-tel">629 44 20 13</a>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-text">
    <div class="hero-badge">🌿 Expertos en jardinería</div>
    <h1 class="hero-title">
      Tu jardín,<br>
      <span class="green">nuestra</span><br>
      <span class="outline">pasión</span>
    </h1>
    <p class="hero-desc">
      Mantenimiento profesional de jardines, podas y desbroces en A Coruña y alrededores. Más de 10 años cuidando espacios verdes con dedicación y experiencia.
    </p>
    <div class="hero-btns">
      <a href="#contacto" class="btn-primary">Solicitar presupuesto</a>
      <a href="#servicios" class="btn-secondary">Ver servicios</a>
    </div>
  </div>

  <!-- Tarjeta 3D -->
  <div class="hero-card-area" id="cardArea">
    <div class="card-wrap" id="card3d">
      <div class="card-face card-front">
        <div class="card-shine" id="shine3d"></div>
        <div class="top-section">
          <div class="brand-jardineria">Jardinería</div>
          <div class="logo-ltc">LTC</div>
        </div>
        <div class="bottom-section">
          <div class="grass-top">
            <svg viewBox="0 0 400 20" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg" width="100%" height="100%">
              <path d="M0,20 C5,8 10,14 15,6 C20,0 25,10 30,4 C35,0 40,12 46,5 C52,0 57,10 62,3 C67,0 72,11 78,5 C84,0 89,9 95,3 C101,0 106,10 112,4 C118,0 124,11 130,5 C140,0 150,10 160,4 C170,0 180,11 190,5 C200,0 210,10 220,4 C230,0 240,11 250,5 C260,0 270,10 280,4 C290,0 300,11 310,5 C320,0 330,10 340,4 C350,0 360,11 370,5 C380,0 390,10 400,5 L400,20 Z" fill="#3a6800"/>
            </svg>
          </div>
          <div class="tree-col">
            <svg width="68" height="95" viewBox="0 0 68 95" xmlns="http://www.w3.org/2000/svg">
              <rect x="28" y="60" width="12" height="32" rx="4" fill="#6b3a10"/>
              <ellipse cx="34" cy="56" rx="26" ry="18" fill="#2d6e00"/>
              <ellipse cx="34" cy="42" rx="20" ry="15" fill="#3d8e00"/>
              <ellipse cx="34" cy="28" rx="16" ry="14" fill="#4daa00"/>
              <ellipse cx="34" cy="14" rx="10" ry="10" fill="#5cc400"/>
              <ellipse cx="26" cy="16" rx="4" ry="3" fill="#88e030" opacity="0.55"/>
              <ellipse cx="25" cy="34" rx="6" ry="4" fill="#88e030" opacity="0.4"/>
            </svg>
          </div>
          <div class="info-col">
            <div class="card-services">Mantenimientos de jardines<br>Podas y desbroces</div>
            <div class="card-phone">TELF. 629 44 20 13</div>
          </div>
        </div>
      </div>
      <div class="card-face card-back">
        <div class="card-back-inner">Jardinería LTC</div>
      </div>
      <div class="card-edge-r"></div>
      <div class="card-edge-b"></div>
    </div>
  </div>

  <!-- Césped decorativo -->
  <div class="hero-grass">
    <svg viewBox="0 0 1440 80" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg" width="100%" height="100%">
      <path d="M0,80 C60,50 100,65 150,40 C200,15 240,55 300,35 C360,15 400,60 460,38 C520,16 560,58 620,40 C680,22 720,62 780,42 C840,22 880,58 940,38 C1000,18 1040,60 1100,40 C1160,20 1200,58 1260,36 C1320,14 1380,55 1440,35 L1440,80 Z" fill="#2d5a00" opacity="0.15"/>
      <path d="M0,80 C80,55 140,70 200,50 C260,30 320,68 400,50 C480,32 540,70 620,52 C700,34 760,70 840,54 C920,38 980,68 1060,50 C1140,32 1200,66 1280,50 C1360,34 1400,60 1440,48 L1440,80 Z" fill="#3d7a00" opacity="0.2"/>
    </svg>
  </div>
</section>

<!-- STATS -->
<section id="stats">
  <div class="stat-item reveal">
    <span class="stat-num" data-target="10">0</span>
    <span class="stat-label">Años de experiencia</span>
  </div>
  <div class="stat-item reveal">
    <span class="stat-num" data-target="250">0</span>
    <span class="stat-label">Clientes satisfechos</span>
  </div>
  <div class="stat-item reveal">
    <span class="stat-num" data-target="500">0</span>
    <span class="stat-label">Jardines cuidados</span>
  </div>
  <div class="stat-item reveal">
    <span class="stat-num" data-target="100">0</span>
    <span class="stat-label">% Compromiso</span>
  </div>
</section>

<!-- SERVICIOS -->
<section id="servicios">
  <div class="section-header reveal">
    <span class="section-tag">Lo que hacemos</span>
    <h2 class="section-title">Nuestros <span class="green">Servicios</span></h2>
  </div>
  <div class="servicios-grid">
    <div class="servicio-card reveal">
      <div class="servicio-icon">🌿</div>
      <h3>Mantenimiento de jardines</h3>
      <p>Cuidado regular de jardines privados y comunidades: corte de césped, abonado, riego y control de malas hierbas para mantener tu jardín siempre perfecto.</p>
    </div>
    <div class="servicio-card reveal">
      <div class="servicio-icon">✂️</div>
      <h3>Podas profesionales</h3>
      <p>Poda de árboles, arbustos y setos con técnica y criterio. Formación de copa, poda sanitaria y poda de fructificación para la salud y belleza de tus plantas.</p>
    </div>
    <div class="servicio-card reveal">
      <div class="servicio-icon">🌾</div>
      <h3>Desbroces y limpieza</h3>
      <p>Desbroce de terrenos, parcelas y fincas. Eliminación de maleza, hierbas invasoras y vegetación no deseada. Dejamos tu terreno limpio y ordenado.</p>
    </div>
    <div class="servicio-card reveal">
      <div class="servicio-icon">🌱</div>
      <h3>Plantación y diseño</h3>
      <p>Asesoramiento y plantación de especies adaptadas a tu espacio y clima. Creamos jardines desde cero con criterio estético y bajo mantenimiento.</p>
    </div>
    <div class="servicio-card reveal">
      <div class="servicio-icon">💧</div>
      <h3>Sistemas de riego</h3>
      <p>Instalación y mantenimiento de sistemas de riego automático. Ahorra agua y tiempo con soluciones adaptadas al tamaño y necesidades de tu jardín.</p>
    </div>
    <div class="servicio-card reveal">
      <div class="servicio-icon">🍂</div>
      <h3>Limpieza de otoño</h3>
      <p>Recogida de hojas caídas, limpieza de jardines tras el verano y preparación de las plantas para el invierno. Dejamos tu espacio listo para la nueva temporada.</p>
    </div>
  </div>
</section>

<!-- NOSOTROS -->
<section id="nosotros">
  <div class="nosotros-visual reveal">
    <div class="nosotros-img-box">
      <svg viewBox="0 0 300 200" xmlns="http://www.w3.org/2000/svg">
        <ellipse cx="150" cy="160" rx="120" ry="30" fill="white"/>
        <rect x="136" y="80" width="28" height="80" rx="8" fill="white"/>
        <ellipse cx="150" cy="120" rx="55" ry="40" fill="white"/>
        <ellipse cx="150" cy="90" rx="45" ry="35" fill="white"/>
        <ellipse cx="150" cy="60" rx="35" ry="32" fill="white"/>
        <ellipse cx="150" cy="34" rx="22" ry="22" fill="white"/>
      </svg>
      <div class="nosotros-badge-float">
        <div class="big">10+</div>
        <div class="small">Años de<br>experiencia</div>
      </div>
    </div>
  </div>

  <div class="nosotros-text">
    <div class="section-header reveal">
      <span class="section-tag">Por qué elegirnos</span>
      <h2 class="section-title">Cuidamos tu<br><span class="green">jardín como el nuestro</span></h2>
    </div>
    <ul class="check-list reveal">
      <li>Profesionales con más de 10 años de experiencia en jardinería y paisajismo</li>
      <li>Presupuesto sin compromiso y totalmente personalizado</li>
      <li>Materiales y herramientas de primera calidad</li>
      <li>Puntualidad y seriedad en cada trabajo</li>
      <li>Atención cercana y trato personal en cada proyecto</li>
      <li>Cobertura en A Coruña y toda la comarca</li>
    </ul>
    <a href="#contacto" class="btn-primary reveal">Pide tu presupuesto gratis</a>
  </div>
</section>

<!-- PROCESO -->
<section id="proceso">
  <div class="section-header reveal">
    <span class="section-tag">Cómo trabajamos</span>
    <h2 class="section-title">Simple y <span class="green">Transparente</span></h2>
  </div>
  <div class="proceso-steps">
    <div class="paso reveal">
      <div class="paso-num">01</div>
      <h4>Contacto</h4>
      <p>Llámanos o escríbenos. Te respondemos en menos de 24 horas para atender tu consulta.</p>
    </div>
    <div class="paso reveal">
      <div class="paso-num">02</div>
      <h4>Visita gratuita</h4>
      <p>Visitamos tu jardín o terreno para valorar el trabajo y conocer exactamente lo que necesitas.</p>
    </div>
    <div class="paso reveal">
      <div class="paso-num">03</div>
      <h4>Presupuesto</h4>
      <p>Te enviamos un presupuesto detallado, claro y sin sorpresas. Sin compromiso.</p>
    </div>
    <div class="paso reveal">
      <div class="paso-num">04</div>
      <h4>¡Manos a la obra!</h4>
      <p>Nos ponemos a trabajar con dedicación y dejamos tu jardín impecable.</p>
    </div>
  </div>
</section>

<!-- CONTACTO -->
<section id="contacto">
  <div class="contacto-inner">
    <div class="contacto-info">
      <div class="section-header" style="text-align:left; margin-bottom:0">
        <span class="section-tag">Hablemos</span>
        <h2 class="section-title">Solicita tu<br>presupuesto <span style="color:var(--verde-lima)">gratis</span></h2>
      </div>
      <p class="contacto-desc">Sin compromiso y totalmente personalizado. Cuéntanos qué necesitas y te damos respuesta enseguida.</p>
      <div class="contact-items">
        <div class="contact-item">
          <div class="contact-icon">📞</div>
          <div>
            <span class="label">Teléfono</span>
            <a href="tel:629442013" class="value" style="text-decoration:none">629 44 20 13</a>
          </div>
        </div>
        <div class="contact-item">
          <div class="contact-icon">📍</div>
          <div>
            <span class="label">Zona de trabajo</span>
            <span class="value">A Coruña y comarca</span>
          </div>
        </div>
        <div class="contact-item">
          <div class="contact-icon">🕐</div>
          <div>
            <span class="label">Horario</span>
            <span class="value">Lun – Sáb · 8:00 – 19:00</span>
          </div>
        </div>
      </div>
    </div>

    <div class="contacto-form reveal">
      <div class="form-row">
        <div class="form-group">
          <label>Nombre</label>
          <input type="text" placeholder="Tu nombre">
        </div>
        <div class="form-group">
          <label>Teléfono</label>
          <input type="tel" placeholder="600 000 000">
        </div>
      </div>
      <div class="form-group">
        <label>Servicio</label>
        <select>
          <option value="">Selecciona un servicio...</option>
          <option>Mantenimiento de jardín</option>
          <option>Poda de árboles/arbustos</option>
          <option>Desbroce de terreno</option>
          <option>Plantación y diseño</option>
          <option>Sistema de riego</option>
          <option>Limpieza de otoño</option>
          <option>Otro</option>
        </select>
      </div>
      <div class="form-group">
        <label>Mensaje</label>
        <textarea placeholder="Cuéntanos qué necesitas..."></textarea>
      </div>
      <button class="btn-send" onclick="alert('¡Mensaje enviado! Nos pondremos en contacto contigo pronto.')">ENVIAR MENSAJE →</button>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">Jardinería LTC</div>
  <div class="footer-links">
    <a href="#servicios">Servicios</a>
    <a href="#nosotros">Nosotros</a>
    <a href="#contacto">Contacto</a>
  </div>
  <div class="footer-copy">© 2025 Jardinería LTC · Todos los derechos reservados</div>
</footer>

<script>
  /* ── Navbar scroll ── */
  const navbar = document.getElementById('navbar');
  window.addEventListener('scroll', () => {
    navbar.classList.toggle('scrolled', window.scrollY > 20);
  });

  /* ── Tarjeta 3D ── */
  const card3d   = document.getElementById('card3d');
  const cardArea = document.getElementById('cardArea');
  const shine3d  = document.getElementById('shine3d');
  let bX = 8, bY = -18, tX = bX, tY = bY, cX = bX, cY = bY;

  cardArea.addEventListener('mousemove', e => {
    const r = cardArea.getBoundingClientRect();
    const dx = (e.clientX - r.left - r.width/2)  / (r.width/2);
    const dy = (e.clientY - r.top  - r.height/2) / (r.height/2);
    tY = bY + dx * 24; tX = bX - dy * 15;
    shine3d.style.background = `radial-gradient(ellipse at ${50+dx*30}% ${50+dy*30}%, rgba(255,255,255,0.26) 0%, transparent 65%)`;
  });
  cardArea.addEventListener('mouseleave', () => {
    tX = bX; tY = bY;
    shine3d.style.background = 'linear-gradient(125deg,rgba(255,255,255,0.15) 0%,transparent 50%)';
  });
  (function loop() {
    cX += (tX-cX)*0.1; cY += (tY-cY)*0.1;
    card3d.style.transform = `rotateY(${cY}deg) rotateX(${cX}deg)`;
    requestAnimationFrame(loop);
  })();

  /* ── Reveal on scroll ── */
  const reveals = document.querySelectorAll('.reveal');
  const obs = new IntersectionObserver(entries => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), i * 80);
        obs.unobserve(e.target);
      }
    });
  }, { threshold: 0.12 });
  reveals.forEach(el => obs.observe(el));

  /* ── Contadores animados ── */
  const counters = document.querySelectorAll('.stat-num[data-target]');
  const cObs = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (!e.isIntersecting) return;
      const el = e.target, target = +el.dataset.target;
      let count = 0;
      const step = Math.ceil(target / 50);
      const t = setInterval(() => {
        count = Math.min(count + step, target);
        el.textContent = count + (target === 100 ? '%' : '+');
        if (count >= target) clearInterval(t);
      }, 30);
      cObs.unobserve(el);
    });
  }, { threshold: 0.5 });
  counters.forEach(el => cObs.observe(el));
</script>
</body>
</html>
