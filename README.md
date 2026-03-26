<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jardinería LTC | Profesionales del Jardín</title>
    <style>
        :root { --verde: #76b82a; --oscuro: #1a1a1a; }
        body { font-family: 'Segoe UI', sans-serif; margin: 0; background-color: #f0f0f0; color: var(--oscuro); overflow-x: hidden; }

        /* ESTILOS DE LA TARJETA 3D */
        .scene { width: 100%; display: flex; flex-direction: column; align-items: center; justify-content: center; padding: 40px 20px; perspective: 1000px; }
        .card-wrap { 
            width: 460px; height: 280px; transform-style: preserve-3d; 
            transform: rotateY(-18deg) rotateX(8deg); cursor: pointer;
            filter: drop-shadow(0px 30px 45px rgba(0,0,0,0.38)); 
        }
        .card-face { position: absolute; inset: 0; border-radius: 14px; backface-visibility: hidden; overflow: hidden; }
        .card-front { display: flex; flex-direction: column; background: #fff; }
        
        /* Imagen de tu tarjeta real dentro del diseño 3D */
        .card-front img { width: 100%; height: 100%; object-fit: cover; }

        .card-back { 
            background: linear-gradient(135deg, #2a2a2a, #1a1a1a); 
            transform: rotateY(180deg); display: flex; align-items: center; justify-content: center; 
        }
        .card-back-inner { color: #fff; font-size: 1.2em; letter-spacing: 3px; text-transform: uppercase; }
        .card-shine { position: absolute; inset: 0; border-radius: 14px; pointer-events: none; z-index: 20; background: linear-gradient(125deg, rgba(255,255,255,0.15) 0%, rgba(255,255,255,0.0) 50%); }

        /* SECCIONES DE LA WEB */
        .hero-text { background-color: var(--verde); color: white; padding: 20px; text-align: center; font-size: 1.5em; font-weight: bold; text-transform: uppercase; }
        .servicios { display: flex; justify-content: center; gap: 20px; flex-wrap: wrap; padding: 50px 20px; }
        .card-info { background: white; padding: 30px; border-radius: 15px; width: 250px; box-shadow: 0 10px 20px rgba(0,0,0,0.05); text-align: center; border-bottom: 5px solid var(--verde); }
        .contacto { padding: 60px 20px; text-align: center; background: white; }
        .btn-whatsapp { background: #25d366; color: white; padding: 20px 40px; text-decoration: none; border-radius: 50px; font-weight: bold; font-size: 1.3em; display: inline-block; transition: 0.3s; box-shadow: 0 10px 20px rgba(37,211,102,0.3); }
        .btn-whatsapp:hover { transform: translateY(-5px); background: #128c7e; }

        @media (max-width: 520px) { .card-wrap { width: 320px; height: 195px; } }
    </style>
</head>
<body>

    <div class="scene" id="scene">
        <div class="card-wrap" id="card">
            <div class="card-face card-front">
                <div class="card-shine" id="shine"></div>
                <img src="jardineria_ltc_logo.jpg" alt="Jardinería LTC">
            </div>
            <div class="card-face card-back">
                <div class="card-back-inner">Jardinería LTC</div>
            </div>
        </div>
        <p style="color: #888; margin-top: 20px; font-size: 0.9em;">Mueve el ratón o toca la tarjeta</p>
    </div>

    <div class="hero-text">Mantenimiento • Podas • Desbroces</div>

    <section class="servicios">
        <div class="card-info"><h3>🌿 Jardines</h3><p>Cuidado integral para que tu jardín luzca siempre verde.</p></div>
        <div class="card-info"><h3>✂️ Podas</h3><p>Especialistas en recorte de setos y poda de árboles.</p></div>
        <div class="card-info"><h3>🚜 Desbroces</h3><p>Limpieza de fincas y terrenos con maquinaria profesional.</p></div>
    </section>

    <section class="contacto">
        <h2>¿Hablamos?</h2>
        <p style="font-size: 2em; font-weight: bold; color: var(--verde); margin: 10px 0;">629 44 20 13</p>
        <a href="https://wa.me/34629442013" class="btn-whatsapp">PEDIR PRESUPUESTO GRATIS</a>
    </section>

    <footer style="padding: 20px; text-align: center; color: #aaa;">&copy; 2024 Jardinería LTC</footer>

    <script>
        const card = document.getElementById('card');
        const scene = document.getElementById('scene');
        const shine = document.getElementById('shine');
        let baseX = 8, baseY = -18;
        let targetX = baseX, targetY = baseY;
        let currentX = baseX, currentY = baseY;

        scene.addEventListener('mousemove', (e) => {
            const rect = scene.getBoundingClientRect();
            const dx = (e.clientX - (rect.left + rect.width / 2)) / (rect.width / 2);
            const dy = (e.clientY - (rect.top + rect.height / 2)) / (rect.height / 2);
            targetY = baseY + dx * 25;
            targetX = baseX - dy * 15;
            shine.style.background = `radial-gradient(ellipse at ${50 + dx * 30}% ${50 + dy * 30}%, rgba(255,255,255,0.25) 0%, rgba(255,255,255,0) 65%)`;
        });

        scene.addEventListener('mouseleave', () => { targetX = baseX; targetY = baseY; shine.style.background = 'none'; });

        function animate() {
            currentX += (targetX - currentX) * 0.1;
            currentY += (targetY - currentY) * 0.1;
            card.style.transform = `rotateY(${currentY}deg) rotateX(${currentX}deg)`;
            requestAnimationFrame(animate);
        }
        animate();
    </script>
</body>
</html>
