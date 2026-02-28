[tierras-nuble-dark-mode.html](https://github.com/user-attachments/files/25617625/tierras-nuble-dark-mode.html)
<!DOCTYPE html>
<html lang="es">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tierras del Ñuble | Parcelas de Agrado - Dark Edition</title>
    <meta name="description"
        content="Parcelas de agrado en Ñuble con geoportal interactivo. Visualización premium en modo oscuro.">

    <!-- Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link
        href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;500;600;700&family=Inter:wght@300;400;500;600;700&display=swap"
        rel="stylesheet">

    <!-- Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <!-- Leaflet -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />

    <style>
        :root {
            /* Palette Dark Premium */
            --color-primary: #2d6a4f;
            --color-primary-light: #52b788;
            --color-secondary: #bc6c25;
            --color-secondary-light: #dda15e;
            --color-bg: #0a0f0b;
            --color-bg-card: #141e16;
            --color-bg-alt: #0e160f;
            --color-text: #e2e8f0;
            --color-text-muted: #94a3b8;
            --color-white: #ffffff;
            --font-serif: 'Playfair Display', serif;
            --font-sans: 'Inter', sans-serif;
            --shadow-dark: 0 10px 30px rgba(0, 0, 0, 0.5);
            --radius-md: 12px;
            --radius-lg: 20px;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            font-family: var(--font-sans);
            color: var(--color-text);
            line-height: 1.6;
            background-color: var(--color-bg);
            overflow-x: hidden;
        }

        h1,
        h2,
        h3,
        h4 {
            font-family: var(--font-serif);
            font-weight: 600;
            line-height: 1.2;
            color: var(--color-white);
        }

        a {
            text-decoration: none;
            color: inherit;
            transition: 0.3s;
        }

        button {
            cursor: pointer;
            border: none;
            font-family: var(--font-sans);
        }

        .container {
            max-width: 1280px;
            margin: 0 auto;
            padding: 0 2rem;
        }

        /* Navigation */
        .navbar {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            z-index: 1000;
            background: rgba(10, 15, 11, 0.85);
            backdrop-filter: blur(20px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
            transition: all 0.3s ease;
        }

        .navbar.scrolled {
            height: 70px;
            background: rgba(10, 15, 11, 0.98);
            box-shadow: var(--shadow-dark);
        }

        .navbar-content {
            display: flex;
            align-items: center;
            justify-content: space-between;
            height: 90px;
            transition: height 0.3s;
        }

        .navbar.scrolled .navbar-content {
            height: 70px;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .logo-icon {
            width: 44px;
            height: 44px;
            background: var(--color-primary);
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.25rem;
        }

        .logo-brand {
            font-family: var(--font-serif);
            font-size: 1.4rem;
            font-weight: 700;
            color: var(--color-white);
            line-height: 1;
        }

        .logo-tagline {
            font-size: 0.7rem;
            color: var(--color-primary-light);
            letter-spacing: 0.1em;
            text-transform: uppercase;
        }

        .nav-links {
            display: flex;
            gap: 2.5rem;
            list-style: none;
        }

        .nav-links a {
            font-size: 0.9rem;
            font-weight: 500;
            color: var(--color-text-muted);
        }

        .nav-links a:hover {
            color: var(--color-primary-light);
        }

        .nav-cta {
            display: flex;
            gap: 1rem;
        }

        .btn {
            padding: 0.75rem 1.5rem;
            border-radius: var(--radius-md);
            font-weight: 600;
            font-size: 0.9rem;
            transition: 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
        }

        .btn-primary {
            background: var(--color-primary);
            color: white;
        }

        .btn-primary:hover {
            background: var(--color-primary-light);
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(45, 106, 79, 0.4);
        }

        .btn-secondary {
            background: var(--color-secondary);
            color: white;
        }

        .btn-outline {
            border: 1px solid rgba(255, 255, 255, 0.2);
            color: white;
            background: transparent;
        }

        .btn-outline:hover {
            background: white;
            color: var(--color-bg);
        }

        /* Hero */
        .hero {
            height: 100vh;
            position: relative;
            display: flex;
            align-items: center;
            padding-top: 90px;
            overflow: hidden;
        }

        .hero-bg {
            position: absolute;
            inset: 0;
            z-index: -2;
        }

        .hero-bg img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            filter: brightness(0.4) contrast(1.1);
        }

        .hero-overlay {
            position: absolute;
            inset: 0;
            background: linear-gradient(135deg, rgba(10, 15, 11, 0.9) 0%, rgba(10, 15, 11, 0.4) 100%);
            z-index: -1;
        }

        .hero-content {
            z-index: 1;
        }

        .hero-badge {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            background: rgba(45, 106, 79, 0.2);
            border: 1px solid rgba(45, 106, 79, 0.3);
            padding: 0.5rem 1rem;
            border-radius: 50px;
            font-size: 0.8rem;
            color: var(--color-primary-light);
            margin-bottom: 2rem;
        }

        .hero-title {
            font-size: clamp(2.5rem, 5vw, 4.5rem);
            margin-bottom: 1.5rem;
            max-width: 800px;
        }

        .hero-title span {
            color: var(--color-primary-light);
        }

        .hero-description {
            font-size: 1.2rem;
            color: var(--color-text-muted);
            max-width: 600px;
            margin-bottom: 3rem;
        }

        .hero-stats {
            display: flex;
            gap: 4rem;
            padding-top: 3rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }

        .stat-num {
            font-size: 2.5rem;
            color: var(--color-secondary-light);
            font-weight: 700;
            display: block;
        }

        .stat-label {
            font-size: 0.8rem;
            color: var(--color-text-muted);
            text-transform: uppercase;
        }

        /* Sections */
        .section {
            padding: 8rem 0;
        }

        .section-alt {
            background-color: var(--color-bg-alt);
        }

        .section-header {
            text-align: center;
            max-width: 700px;
            margin: 0 auto 5rem;
        }

        .label {
            color: var(--color-primary-light);
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.15em;
            font-size: 0.8rem;
            display: block;
            margin-bottom: 1rem;
        }

        .section-title {
            font-size: 3rem;
            margin-bottom: 1.5rem;
        }

        /* Geoportal */
        .gp-container {
            background: var(--color-bg-card);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: var(--radius-lg);
            overflow: hidden;
            box-shadow: var(--shadow-dark);
        }

        .gp-top {
            padding: 1.5rem 2rem;
            background: rgba(255, 255, 255, 0.02);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        #map {
            height: 550px;
            width: 100%;
            filter: saturate(0.8) brightness(0.9);
        }

        .gp-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            border-top: 1px solid rgba(255, 255, 255, 0.05);
        }

        .gp-item {
            padding: 2rem;
            text-align: center;
            border-right: 1px solid rgba(255, 255, 255, 0.05);
        }

        .gp-icon {
            font-size: 1.5rem;
            color: var(--color-primary-light);
            margin-bottom: 1rem;
        }

        /* Projects */
        .project-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 2.5rem;
        }

        .card {
            background: var(--color-bg-card);
            border-radius: var(--radius-md);
            overflow: hidden;
            border: 1px solid rgba(255, 255, 255, 0.05);
            transition: 0.4s;
        }

        .card:hover {
            transform: translateY(-10px);
            border-color: var(--color-primary-light);
        }

        .card-img {
            height: 250px;
            position: relative;
        }

        .card-img img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .card-badge {
            position: absolute;
            top: 1rem;
            left: 1rem;
            background: var(--color-primary);
            color: white;
            padding: 0.4rem 1rem;
            border-radius: 50px;
            font-size: 0.7rem;
            font-weight: 700;
        }

        .card-body {
            padding: 2rem;
        }

        .card-price {
            font-size: 1.8rem;
            color: var(--color-white);
            margin-top: 1.5rem;
            display: block;
        }

        /* Why Us */
        .why-flex {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 5rem;
            align-items: center;
        }

        .feature-list {
            display: grid;
            gap: 2rem;
            margin-top: 3rem;
        }

        .f-item {
            display: flex;
            gap: 1.5rem;
        }

        .f-icon {
            width: 60px;
            height: 60px;
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            color: var(--color-primary-light);
            flex-shrink: 0;
        }

        /* Steps */
        .step-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 2rem;
        }

        .step-card {
            text-align: center;
        }

        .step-num {
            width: 70px;
            height: 70px;
            background: var(--color-primary);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.8rem;
            font-family: var(--font-serif);
            margin: 0 auto 2rem;
        }

        /* Testimonials */
        .testi-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 2rem;
        }

        .testi-card {
            background: rgba(255, 255, 255, 0.02);
            padding: 2.5rem;
            border-radius: var(--radius-md);
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .testi-stars {
            color: #fbbf24;
            margin-bottom: 1rem;
        }

        /* Footer */
        .footer {
            padding: 6rem 0 3rem;
            background: #050805;
            border-top: 1px solid rgba(255, 255, 255, 0.05);
        }

        .footer-grid {
            display: grid;
            grid-template-columns: 2fr 1fr 1fr 1fr;
            gap: 4rem;
        }

        /* Responsive Updates */
        @media (max-width: 1024px) {

            .project-grid,
            .testi-grid,
            .step-grid {
                grid-template-columns: repeat(2, 1fr);
            }

            .why-flex {
                grid-template-columns: 1fr;
                gap: 3rem;
            }

            .hero-title {
                font-size: 3.5rem;
            }
        }

        @media (max-width: 768px) {
            .navbar-content {
                height: 70px;
            }

            .nav-links {
                position: fixed;
                top: 70px;
                left: -100%;
                width: 100%;
                height: calc(100vh - 70px);
                background: var(--color-bg);
                flex-direction: column;
                align-items: center;
                padding-top: 3rem;
                transition: 0.4s;
                z-index: 999;
            }

            .nav-links.active {
                left: 0;
            }

            .nav-cta .btn-outline {
                display: none;
            }

            .mobile-menu-btn {
                display: block;
                font-size: 1.5rem;
                color: white;
                background: none;
            }

            .hero {
                text-align: center;
                height: auto;
                padding: 120px 0 60px;
            }

            .hero-badge {
                margin: 0 auto 1.5rem;
            }

            .hero-title {
                font-size: 2.5rem;
            }

            .hero-description {
                margin: 0 auto 2.5rem;
            }

            .hero-stats {
                flex-direction: column;
                gap: 2rem;
                align-items: center;
            }

            .gp-grid {
                grid-template-columns: repeat(2, 1fr);
            }

            .gp-item {
                border-bottom: 1px solid rgba(255, 255, 255, 0.05);
            }

            .gp-item:nth-child(even) {
                border-right: none;
            }

            .section-title {
                font-size: 2rem;
            }

            .project-grid,
            .testi-grid,
            .step-grid,
            .footer-grid {
                grid-template-columns: 1fr;
            }

            .why-flex {
                text-align: center;
            }

            .f-item {
                flex-direction: column;
                align-items: center;
                text-align: center;
            }

            .footer-grid {
                text-align: center;
            }
        }

        .mobile-menu-btn {
            display: none;
        }
    </style>
</head>

<body>
    <nav class="navbar" id="navbar">
        <div class="container navbar-content">
            <a href="#" class="logo">
                <div class="logo-icon"><i class="fas fa-mountain"></i></div>
                <div>
                    <div class="logo-brand">Tierras del Ñuble</div>
                    <div class="logo-tagline">Parcelas de Agrado</div>
                </div>
            </a>
            <ul class="nav-links" id="nav-links">
                <li><a href="#proyectos">Proyectos</a></li>
                <li><a href="#geoportal">Geoportal</a></li>
                <li><a href="#por-que">¿Por qué nosotros?</a></li>
                <li><a href="#proceso">Proceso</a></li>
                <li><a href="#contacto">Contacto</a></li>
            </ul>
            <div class="nav-cta">
                <a href="#contacto" class="btn btn-outline">Contacto</a>
                <button class="mobile-menu-btn" id="mobile-menu-btn"><i class="fas fa-bars"></i></button>
            </div>
        </div>
    </nav>

    <section class="hero">
        <div class="hero-bg">
            <img src="https://images.unsplash.com/photo-1500382017468-9049fed747ef?w=1920&q=80" alt="">
        </div>
        <div class="hero-overlay"></div>
        <div class="container hero-content">
            <div class="hero-badge">
                <i class="fas fa-satellite"></i>
                <span>Tecnología Geoespacial Aplicada al Corazón de Ñuble</span>
            </div>
            <h1 class="hero-title">Tu parcela en Ñuble, <span>completamente transparente</span></h1>
            <p class="hero-description">Innovación territorial para familias que buscan seguridad. Visualiza servicios,
                entorno y realidad jurídica antes de visitar el terreno.</p>
            <div class="nav-cta">
                <a href="#geoportal" class="btn btn-primary btn-large"
                    style="padding:1.2rem 2.5rem; font-size:1rem;">Explorar Geoportal</a>
                <a href="#proyectos" class="btn btn-outline btn-large"
                    style="padding:1.2rem 2.5rem; font-size:1rem;">Ver Catálogo</a>
            </div>
            <div class="hero-stats">
                <div class="stat">
                    <span class="stat-num">12+</span>
                    <span class="stat-label">Proyectos Activos</span>
                </div>
                <div class="stat">
                    <span class="stat-num">450+</span>
                    <span class="stat-label">Familias</span>
                </div>
                <div class="stat">
                    <span class="stat-num">8</span>
                    <span class="stat-label">Comunas</span>
                </div>
            </div>
        </div>
    </section>

    <!-- Geoportal -->
    <section class="section" id="geoportal">
        <div class="container">
            <div class="section-header">
                <span class="label">Innovación</span>
                <h2 class="section-title">Geoportal Interactivo</h2>
                <p style="color:var(--color-text-muted)">Accede a información técnica real: factibilidad eléctrica,
                    recursos hídricos y topografía digital.</p>
            </div>
            <div class="gp-container">
                <div class="gp-top">
                    <div style="font-weight:700;"><i class="fas fa-map-marked-alt"
                            style="margin-right:10px; color:var(--color-primary-light)"></i> Ñuble_Data_Viz_2024</div>
                    <div style="font-size:0.8rem; color:var(--color-text-muted)">Sincronizado vía Satélite</div>
                </div>
                <div id="map"></div>
                <div class="gp-grid">
                    <div class="gp-item">
                        <i class="fas fa-bolt gp-icon"></i>
                        <h4>Servicios</h4>
                        <p style="font-size:0.8rem; color:var(--color-text-muted)">Red eléctrica proyectada</p>
                    </div>
                    <div class="gp-item">
                        <i class="fas fa-tint gp-icon"></i>
                        <h4>Agua</h4>
                        <p style="font-size:0.8rem; color:var(--color-text-muted)">Factibilidad APR</p>
                    </div>
                    <div class="gp-item">
                        <i class="fas fa-chart-area gp-icon"></i>
                        <h4>Plusvalía</h4>
                        <p style="font-size:0.8rem; color:var(--color-text-muted)">Análisis de entorno</p>
                    </div>
                    <div class="gp-item">
                        <i class="fas fa-shield-alt gp-icon" style="border-right:none"></i>
                        <h4>Legal</h4>
                        <p style="font-size:0.8rem; color:var(--color-text-muted)">Rol Propio Verificado</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Projects -->
    <section class="section section-alt" id="proyectos">
        <div class="container">
            <div class="section-header">
                <span class="label">Disponibilidad</span>
                <h2 class="section-title">Parcelas en Venta</h2>
            </div>
            <div class="project-grid">
                <div class="card">
                    <div class="card-img">
                        <img src="https://images.unsplash.com/photo-1500076656116-558758c991c1?w=800&q=80" alt="">
                        <div class="card-badge">ÚLTIMAS UNIDADES</div>
                    </div>
                    <div class="card-body">
                        <h3 style="margin-bottom:0.5rem">Valle del Itata</h3>
                        <p style="font-size:0.9rem; color:var(--color-text-muted)">San Nicolás. Microclima ideal para
                            viñedos.</p>
                        <span class="card-price">$39.900.000 <small
                                style="font-size:0.9rem; color:var(--color-text-muted)">CLP</small></span>
                        <button class="btn btn-primary" style="width:100%; margin-top:2rem;">Ver Detalles</button>
                    </div>
                </div>
                <div class="card">
                    <div class="card-img">
                        <img src="https://images.unsplash.com/photo-1518780664697-55e3ad937233?w=800&q=80" alt="">
                        <div class="card-badge" style="background:var(--color-secondary)">PROYECTO NUEVO</div>
                    </div>
                    <div class="card-body">
                        <h3 style="margin-bottom:0.5rem">Lomas de Chillán</h3>
                        <p style="font-size:0.9rem; color:var(--color-text-muted)">Chillán Viejo. Conectividad urbana y
                            paz rural.</p>
                        <span class="card-price">$28.500.000 <small
                                style="font-size:0.9rem; color:var(--color-text-muted)">CLP</small></span>
                        <button class="btn btn-primary" style="width:100%; margin-top:2rem;">Ver Detalles</button>
                    </div>
                </div>
                <div class="card">
                    <div class="card-img">
                        <img src="https://images.unsplash.com/photo-1464146072230-91cabc968266?w=800&q=80" alt="">
                        <div class="card-badge">ENTREGA INMEDIATA</div>
                    </div>
                    <div class="card-body">
                        <h3 style="margin-bottom:0.5rem">Mirador del Cordón</h3>
                        <p style="font-size:0.9rem; color:var(--color-text-muted)">San Fabián. Entorno montañoso y
                            bosque nativo.</p>
                        <span class="card-price">$45.000.000 <small
                                style="font-size:0.9rem; color:var(--color-text-muted)">CLP</small></span>
                        <button class="btn btn-primary" style="width:100%; margin-top:2rem;">Ver Detalles</button>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Why Us -->
    <section class="section" id="por-que">
        <div class="container">
            <div class="why-flex">
                <div>
                    <span class="label">Diferencia</span>
                    <h2 class="section-title">Certidumbre Territorial</h2>
                    <p style="color:var(--color-text-muted); font-size:1.1rem;">No solo vendemos tierra; entregamos un
                        ecosistema de información para que tu inversión sea 100% segura.</p>
                    <div class="feature-list">
                        <div class="f-item">
                            <div class="f-icon"><i class="fas fa-microscope"></i></div>
                            <div>
                                <h4 style="margin-bottom:0.5rem;">Estudios de Precisión</h4>
                                <p style="font-size:0.9rem; color:var(--color-text-muted);">Análisis de suelos y calidad
                                    de agua certificados por laboratorios locales.</p>
                            </div>
                        </div>
                        <div class="f-item">
                            <div class="f-icon"><i class="fas fa-file-invoice-dollar"></i></div>
                            <div>
                                <h4 style="margin-bottom:0.5rem;">Cero Burocracia</h4>
                                <p style="font-size:0.9rem; color:var(--color-text-muted);">Gestión completa de
                                    escrituración y roles ante el CBR y el SII.</p>
                            </div>
                        </div>
                        <div class="f-item">
                            <div class="f-icon"><i class="fas fa-headset"></i></div>
                            <div>
                                <h4 style="margin-bottom:0.5rem;">Acompañamiento 360</h4>
                                <p style="font-size:0.9rem; color:var(--color-text-muted);">Asesoría en construcción
                                    rural y eficiencia energética post-venta.</p>
                            </div>
                        </div>
                    </div>
                </div>
                <div style="position:relative;">
                    <img src="https://images.unsplash.com/photo-1564013799919-ab600027ffc6?w=800&q=80" alt=""
                        style="width:100%; border-radius:20px; filter:grayscale(0.3) brightness(0.8)">
                    <div
                        style="position:absolute; bottom:-30px; right:30px; background:var(--color-primary); padding:2rem; border-radius:15px; box-shadow:var(--shadow-dark)">
                        <span style="font-size:3rem; font-family:var(--font-serif); font-weight:700;">98%</span>
                        <p style="font-size:0.8rem; font-weight:700;">DE CLIENTES NOS RECOMIENDAN</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Steps -->
    <section class="section section-alt" id="proceso">
        <div class="container">
            <div class="section-header">
                <span class="label">Camino</span>
                <h2 class="section-title">Tu Parcela en 4 Pasos</h2>
            </div>
            <div class="step-grid">
                <div class="step-card">
                    <div class="step-num">1</div>
                    <h3 style="margin-bottom:1rem">Explora</h3>
                    <p style="font-size:0.9rem; color:var(--color-text-muted)">Usa el geoportal para filtrar por tus
                        necesidades reales.</p>
                </div>
                <div class="step-card">
                    <div class="step-num">2</div>
                    <h3 style="margin-bottom:1rem">Visita</h3>
                    <p style="font-size:0.9rem; color:var(--color-text-muted)">Agenda un recorrido guiado con expertos
                        en terreno.</p>
                </div>
                <div class="step-card">
                    <div class="step-num">3</div>
                    <h3 style="margin-bottom:1rem">Reserva</h3>
                    <p style="font-size:0.9rem; color:var(--color-text-muted)">Proceso legal transparente y
                        documentación digital.</p>
                </div>
                <div class="step-card">
                    <div class="step-num">4</div>
                    <h3 style="margin-bottom:1rem">Disfruta</h3>
                    <p style="font-size:0.9rem; color:var(--color-text-muted)">Te acompañamos en tu nueva vida rural en
                        Ñuble.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Testimonials -->
    <section class="section" id="testimonios">
        <div class="container">
            <div class="section-header">
                <span class="label">Confianza</span>
                <h2 class="section-title">Clientes Satisfechos</h2>
            </div>
            <div class="testi-grid">
                <div class="testi-card">
                    <div class="testi-stars"><i class="fas fa-star"></i><i class="fas fa-star"></i><i
                            class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i></div>
                    <p style="font-style:italic; margin-bottom:2rem;">"El geoportal nos permitió decidirnos sin viajar
                        600km. La precisión de los datos nos dio la confianza que faltaba."</p>
                    <div style="display:flex; align-items:center; gap:1rem;">
                        <img src="https://randomuser.me/api/portraits/men/32.jpg" style="width:50px; border-radius:50%;"
                            alt="">
                        <div>
                            <h4 style="font-size:1rem;">Carlos Muñoz</h4>
                            <p style="font-size:0.8rem; color:var(--color-text-muted)">Proyecto Valle del Itata</p>
                        </div>
                    </div>
                </div>
                <div class="testi-card">
                    <div class="testi-stars"><i class="fas fa-star"></i><i class="fas fa-star"></i><i
                            class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i></div>
                    <p style="font-style:italic; margin-bottom:2rem;">"La transparencia en los roles y certificados de
                        agua fue lo más importante para nosotros. Un servicio de primer nivel."</p>
                    <div style="display:flex; align-items:center; gap:1rem;">
                        <img src="https://randomuser.me/api/portraits/women/44.jpg"
                            style="width:50px; border-radius:50%;" alt="">
                        <div>
                            <h4 style="font-size:1rem;">María Riquelme</h4>
                            <p style="font-size:0.8rem; color:var(--color-text-muted)">Lomas de Chillán</p>
                        </div>
                    </div>
                </div>
                <div class="testi-card">
                    <div class="testi-stars"><i class="fas fa-star"></i><i class="fas fa-star"></i><i
                            class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i></div>
                    <p style="font-style:italic; margin-bottom:2rem;">"Encontramos el lugar soñado frente a la
                        cordillera. El equipo de Tierras del Ñuble nos guió en cada paso."</p>
                    <div style="display:flex; align-items:center; gap:1rem;">
                        <img src="https://randomuser.me/api/portraits/men/67.jpg" style="width:50px; border-radius:50%;"
                            alt="">
                        <div>
                            <h4 style="font-size:1rem;">Pedro González</h4>
                            <p style="font-size:0.8rem; color:var(--color-text-muted)">Mirador del Cordón</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- CTA -->
    <section class="section"
        style="background:linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)), url('https://images.unsplash.com/photo-1464822759023-fed622ff2c3b?w=1920&q=80'); background-size:cover; background-attachment:fixed; text-align:center;">
        <div class="container">
            <h2 class="section-title">¿Listo para tu nueva vida?</h2>
            <p style="max-width:600px; margin: 0 auto 3rem; color:var(--color-text-muted)">Agenda una reunión virtual o
                presencial para conocer todos los detalles de inversión.</p>
            <div style="display:flex; gap:1.5rem; justify-content:center; flex-wrap:wrap;">
                <button class="btn btn-primary" style="padding:1.2rem 3rem;">HABLAR CON UN ASESOR</button>
                <button class="btn btn-outline" style="padding:1.2rem 3rem;">CATÁLOGO PDF</button>
            </div>
        </div>
    </section>

    <footer class="footer">
        <div class="container">
            <div class="footer-grid">
                <div>
                    <div class="logo-brand" style="margin-bottom:1rem;">Tierras del Ñuble</div>
                    <p style="font-size:0.9rem; color:var(--color-text-muted)">Líderes en desarrollo rural inteligente
                        en la Región del Ñuble. Certeza legal y tecnológica.</p>
                </div>
                <div>
                    <h4 style="margin-bottom:1.5rem">Legales</h4>
                    <ul style="list-style:none; color:var(--color-text-muted); font-size:0.9rem;">
                        <li style="margin-bottom:0.5rem">Términos y condiciones</li>
                        <li style="margin-bottom:0.5rem">Política de privacidad</li>
                        <li style="margin-bottom:0.5rem">Rol propio</li>
                    </ul>
                </div>
                <div>
                    <h4 style="margin-bottom:1.5rem">Contacto</h4>
                    <ul style="list-style:none; color:var(--color-text-muted); font-size:0.9rem;">
                        <li style="margin-bottom:0.5rem">Chillán, Ñuble, Chile</li>
                        <li style="margin-bottom:0.5rem">+56 9 1234 5678</li>
                        <li style="margin-bottom:0.5rem">hola@tierrasdelnuble.cl</li>
                    </ul>
                </div>
                <div>
                    <h4 style="margin-bottom:1.5rem">Redes</h4>
                    <div style="display:flex; gap:1rem; font-size:1.5rem">
                        <i class="fab fa-instagram"></i>
                        <i class="fab fa-facebook"></i>
                        <i class="fab fa-youtube"></i>
                    </div>
                </div>
            </div>
            <div style="margin-top:5rem; text-align:center; font-size:0.8rem; color:var(--color-text-muted)">
                &copy; 2024 Tierras del Ñuble SpA. Todos los derechos reservados.
            </div>
        </div>
    </footer>

    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
    <script>
        // Navbar scroll effect
        window.addEventListener('scroll', () => {
            const nav = document.getElementById('navbar');
            if (window.scrollY > 50) nav.classList.add('scrolled');
            else nav.classList.remove('scrolled');
        });

        // Initialize Map
        const map = L.map('map').setView([-36.6, -72.1], 10);

        // Dark Sat Layer
        L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
            attribution: 'Esri'
        }).addTo(map);

        // Styling the satellite layer for dark mode
        document.getElementById('map').style.backgroundColor = '#0a0f0b';

        // Add Example Markers
        const projects = [
            { name: "Valle del Itata", coords: [-36.5, -72.4], price: "$39.9M" },
            { name: "Lomas de Chillán", coords: [-36.65, -71.95], price: "$28.5M" },
            { name: "Mirador del Cordón", coords: [-36.8, -72.2], price: "$45M" }
        ];

        const customIcon = L.divIcon({
            className: 'custom-div-icon',
            html: "<div style='background-color:#52b788; width:15px; height:15px; border-radius:50%; border:2px solid white; box-shadow:0 0 10px rgba(82,183,136,0.8);'></div>",
            iconSize: [15, 15],
            iconAnchor: [7, 7]
        });

        projects.forEach(p => {
            L.marker(p.coords, { icon: customIcon }).addTo(map)
                .bindPopup(`<strong style="color:#52b788">${p.name}</strong><br>Precio: ${p.price}<br><a href="#" style="color:#bc6c25; font-weight:700">Ver Ficha Pública</a>`);
        });

        // Mobile Menu Logic
        const mobileMenuBtn = document.getElementById('mobile-menu-btn');
        const navLinks = document.getElementById('nav-links');

        mobileMenuBtn.addEventListener('click', () => {
            navLinks.classList.toggle('active');
            const icon = mobileMenuBtn.querySelector('i');
            icon.classList.toggle('fa-bars');
            icon.classList.toggle('fa-times');
        });

        // Close menu when clicking a link
        document.querySelectorAll('.nav-links a').forEach(link => {
            link.addEventListener('click', () => {
                navLinks.classList.remove('active');
                const icon = mobileMenuBtn.querySelector('i');
                icon.classList.add('fa-bars');
                icon.classList.remove('fa-times');
            });
        });
    </script>
</body>

</html>
