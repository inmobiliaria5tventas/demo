<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tierras del Ñuble | Parcelas de Agrado con Geoportal Interactivo</title>
    <meta name="description" content="Parcelas de agrado en Ñuble con geoportal interactivo. Visualiza servicios, plusvalía y potencial productivo antes de comprar. Proyectos rurales transparentes y verificados.">
    
    <!-- Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;500;600;700&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Leaflet -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
    
    <style>
        :root {
            --color-primary: #1a4d2e;
            --color-primary-light: #2d6a4f;
            --color-secondary: #bc6c25;
            --color-secondary-light: #dda15e;
            --color-accent: #e9edc9;
            --color-dark: #1b1b1b;
            --color-gray: #6b7280;
            --color-light: #f8f9fa;
            --color-white: #ffffff;
            --font-serif: 'Playfair Display', serif;
            --font-sans: 'Inter', sans-serif;
            --shadow-sm: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
            --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
            --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
            --shadow-xl: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
            --radius-sm: 8px;
            --radius-md: 12px;
            --radius-lg: 16px;
            --radius-xl: 24px;
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
            color: var(--color-dark);
            line-height: 1.6;
            background-color: var(--color-white);
        }

        h1, h2, h3, h4 {
            font-family: var(--font-serif);
            font-weight: 600;
            line-height: 1.2;
        }

        img {
            max-width: 100%;
            height: auto;
            display: block;
        }

        a {
            text-decoration: none;
            color: inherit;
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
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            border-bottom: 1px solid rgba(0,0,0,0.05);
            transition: all 0.3s ease;
        }

        .navbar.scrolled {
            box-shadow: var(--shadow-md);
        }

        .navbar-content {
            display: flex;
            align-items: center;
            justify-content: space-between;
            height: 80px;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .logo-icon {
            width: 48px;
            height: 48px;
            background: var(--color-primary);
            border-radius: var(--radius-md);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.5rem;
        }

        .logo-text {
            display: flex;
            flex-direction: column;
        }

        .logo-brand {
            font-family: var(--font-serif);
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--color-primary);
            line-height: 1;
        }

        .logo-tagline {
            font-size: 0.75rem;
            color: var(--color-gray);
            letter-spacing: 0.05em;
            text-transform: uppercase;
        }

        .nav-links {
            display: flex;
            align-items: center;
            gap: 2.5rem;
            list-style: none;
        }

        .nav-links a {
            font-size: 0.95rem;
            font-weight: 500;
            color: var(--color-dark);
            position: relative;
            padding: 0.5rem 0;
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--color-secondary);
            transition: width 0.3s ease;
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        .nav-cta {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            padding: 0.875rem 1.75rem;
            border-radius: var(--radius-md);
            font-weight: 600;
            font-size: 0.95rem;
            transition: all 0.3s ease;
        }

        .btn-primary {
            background: var(--color-primary);
            color: white;
        }

        .btn-primary:hover {
            background: var(--color-primary-light);
            transform: translateY(-2px);
            box-shadow: var(--shadow-lg);
        }

        .btn-secondary {
            background: var(--color-secondary);
            color: white;
        }

        .btn-secondary:hover {
            background: #a05a1f;
            transform: translateY(-2px);
        }

        .btn-outline {
            background: transparent;
            color: var(--color-primary);
            border: 2px solid var(--color-primary);
        }

        .btn-outline:hover {
            background: var(--color-primary);
            color: white;
        }

        .btn-large {
            padding: 1.125rem 2.5rem;
            font-size: 1.1rem;
        }

        .mobile-menu-btn {
            display: none;
            background: none;
            font-size: 1.5rem;
            color: var(--color-dark);
        }

        /* Hero Section */
        .hero {
            min-height: 100vh;
            position: relative;
            display: flex;
            align-items: center;
            overflow: hidden;
            margin-top: 80px;
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
        }

        .hero-overlay {
            position: absolute;
            inset: 0;
            background: linear-gradient(135deg, rgba(26, 77, 46, 0.85) 0%, rgba(27, 27, 27, 0.7) 100%);
            z-index: -1;
        }

        .hero-content {
            position: relative;
            z-index: 1;
            color: white;
            padding: 4rem 0;
        }

        .hero-badge {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            padding: 0.5rem 1rem;
            border-radius: 50px;
            font-size: 0.875rem;
            font-weight: 500;
            margin-bottom: 1.5rem;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .hero-title {
            font-size: clamp(2.5rem, 5vw, 4.5rem);
            font-weight: 700;
            margin-bottom: 1.5rem;
            max-width: 800px;
        }

        .hero-title span {
            color: var(--color-secondary-light);
        }

        .hero-description {
            font-size: 1.25rem;
            max-width: 600px;
            margin-bottom: 2.5rem;
            opacity: 0.95;
            font-weight: 300;
        }

        .hero-cta {
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
        }

        .hero-stats {
            display: flex;
            gap: 3rem;
            margin-top: 4rem;
            padding-top: 2rem;
            border-top: 1px solid rgba(255, 255, 255, 0.2);
        }

        .hero-stat {
            text-align: center;
        }

        .hero-stat-number {
            font-family: var(--font-serif);
            font-size: 2.5rem;
            font-weight: 700;
            color: var(--color-secondary-light);
        }

        .hero-stat-label {
            font-size: 0.875rem;
            opacity: 0.9;
        }

        /* Geoportal Preview */
        .geoportal-section {
            padding: 6rem 0;
            background: var(--color-light);
        }

        .section-header {
            text-align: center;
            max-width: 700px;
            margin: 0 auto 4rem;
        }

        .section-label {
            display: inline-block;
            color: var(--color-secondary);
            font-weight: 600;
            font-size: 0.875rem;
            text-transform: uppercase;
            letter-spacing: 0.1em;
            margin-bottom: 1rem;
        }

        .section-title {
            font-size: clamp(2rem, 4vw, 3rem);
            color: var(--color-primary);
            margin-bottom: 1rem;
        }

        .section-description {
            color: var(--color-gray);
            font-size: 1.125rem;
        }

        .geoportal-container {
            background: white;
            border-radius: var(--radius-xl);
            box-shadow: var(--shadow-xl);
            overflow: hidden;
            border: 1px solid rgba(0,0,0,0.05);
        }

        .geoportal-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 1.5rem 2rem;
            background: var(--color-primary);
            color: white;
        }

        .geoportal-title {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            font-weight: 600;
        }

        .geoportal-controls {
            display: flex;
            gap: 1rem;
        }

        .geoportal-control {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            padding: 0.5rem 1rem;
            background: rgba(255,255,255,0.15);
            border-radius: var(--radius-sm);
            font-size: 0.875rem;
            cursor: pointer;
            transition: all 0.2s;
        }

        .geoportal-control:hover {
            background: rgba(255,255,255,0.25);
        }

        #map {
            height: 500px;
            width: 100%;
        }

        .geoportal-features {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 0;
            border-top: 1px solid rgba(0,0,0,0.05);
        }

        .geoportal-feature {
            padding: 1.5rem;
            text-align: center;
            border-right: 1px solid rgba(0,0,0,0.05);
        }

        .geoportal-feature:last-child {
            border-right: none;
        }

        .geoportal-feature-icon {
            width: 48px;
            height: 48px;
            background: var(--color-accent);
            border-radius: var(--radius-md);
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 0.75rem;
            color: var(--color-primary);
            font-size: 1.25rem;
        }

        .geoportal-feature-title {
            font-weight: 600;
            font-size: 0.95rem;
            margin-bottom: 0.25rem;
        }

        .geoportal-feature-desc {
            font-size: 0.875rem;
            color: var(--color-gray);
        }

        /* Projects Section */
        .projects-section {
            padding: 6rem 0;
        }

        .projects-header {
            display: flex;
            justify-content: space-between;
            align-items: end;
            margin-bottom: 3rem;
        }

        .projects-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 2rem;
        }

        .project-card {
            background: white;
            border-radius: var(--radius-lg);
            overflow: hidden;
            box-shadow: var(--shadow-md);
            transition: all 0.3s ease;
            border: 1px solid rgba(0,0,0,0.05);
        }

        .project-card:hover {
            transform: translateY(-8px);
            box-shadow: var(--shadow-xl);
        }

        .project-image {
            position: relative;
            height: 240px;
            overflow: hidden;
        }

        .project-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s ease;
        }

        .project-card:hover .project-image img {
            transform: scale(1.05);
        }

        .project-badge {
            position: absolute;
            top: 1rem;
            left: 1rem;
            background: var(--color-secondary);
            color: white;
            padding: 0.375rem 0.875rem;
            border-radius: 50px;
            font-size: 0.75rem;
            font-weight: 600;
            text-transform: uppercase;
        }

        .project-favorite {
            position: absolute;
            top: 1rem;
            right: 1rem;
            width: 40px;
            height: 40px;
            background: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--color-gray);
            cursor: pointer;
            transition: all 0.2s;
        }

        .project-favorite:hover {
            color: #e74c3c;
            transform: scale(1.1);
        }

        .project-content {
            padding: 1.5rem;
        }

        .project-location {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            color: var(--color-gray);
            font-size: 0.875rem;
            margin-bottom: 0.5rem;
        }

        .project-title {
            font-size: 1.25rem;
            color: var(--color-primary);
            margin-bottom: 0.75rem;
        }

        .project-features {
            display: flex;
            gap: 1rem;
            margin-bottom: 1rem;
        }

        .project-feature {
            display: flex;
            align-items: center;
            gap: 0.375rem;
            font-size: 0.875rem;
            color: var(--color-gray);
        }

        .project-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-top: 1rem;
            border-top: 1px solid rgba(0,0,0,0.05);
        }

        .project-price {
            font-family: var(--font-serif);
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--color-primary);
        }

        .project-price span {
            font-size: 0.875rem;
            color: var(--color-gray);
            font-weight: 400;
        }

        /* Why Us Section */
        .why-section {
            padding: 6rem 0;
            background: var(--color-primary);
            color: white;
            position: relative;
            overflow: hidden;
        }

        .why-section::before {
            content: '';
            position: absolute;
            top: -50%;
            right: -20%;
            width: 800px;
            height: 800px;
            background: rgba(255,255,255,0.03);
            border-radius: 50%;
        }

        .why-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
            align-items: center;
        }

        .why-content .section-label {
            color: var(--color-secondary-light);
        }

        .why-content .section-title {
            color: white;
            margin-bottom: 1.5rem;
        }

        .why-content .section-description {
            color: rgba(255,255,255,0.9);
            margin-bottom: 2rem;
        }

        .why-features {
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
        }

        .why-feature {
            display: flex;
            gap: 1rem;
        }

        .why-feature-icon {
            width: 56px;
            height: 56px;
            background: rgba(255,255,255,0.1);
            border-radius: var(--radius-md);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            flex-shrink: 0;
        }

        .why-feature-content h4 {
            font-size: 1.125rem;
            margin-bottom: 0.5rem;
        }

        .why-feature-content p {
            color: rgba(255,255,255,0.8);
            font-size: 0.95rem;
        }

        .why-image {
            position: relative;
        }

        .why-image img {
            border-radius: var(--radius-xl);
            box-shadow: var(--shadow-xl);
        }

        .why-stats-card {
            position: absolute;
            bottom: -2rem;
            left: -2rem;
            background: white;
            color: var(--color-dark);
            padding: 2rem;
            border-radius: var(--radius-lg);
            box-shadow: var(--shadow-xl);
        }

        .why-stats-card-number {
            font-family: var(--font-serif);
            font-size: 3rem;
            font-weight: 700;
            color: var(--color-primary);
        }

        .why-stats-card-text {
            font-size: 0.95rem;
            color: var(--color-gray);
        }

        /* Process Section */
        .process-section {
            padding: 6rem 0;
            background: var(--color-light);
        }

        .process-steps {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 2rem;
            margin-top: 4rem;
        }

        .process-step {
            text-align: center;
            position: relative;
        }

        .process-step:not(:last-child)::after {
            content: '';
            position: absolute;
            top: 2rem;
            right: -1rem;
            width: 2rem;
            height: 2px;
            background: var(--color-secondary);
        }

        .process-step-number {
            width: 64px;
            height: 64px;
            background: var(--color-primary);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-family: var(--font-serif);
            font-size: 1.5rem;
            font-weight: 700;
            margin: 0 auto 1.5rem;
            position: relative;
        }

        .process-step-title {
            font-size: 1.25rem;
            color: var(--color-primary);
            margin-bottom: 0.75rem;
        }

        .process-step-description {
            color: var(--color-gray);
            font-size: 0.95rem;
        }

        /* Testimonials */
        .testimonials-section {
            padding: 6rem 0;
        }

        .testimonials-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 2rem;
            margin-top: 4rem;
        }

        .testimonial-card {
            background: white;
            padding: 2rem;
            border-radius: var(--radius-lg);
            box-shadow: var(--shadow-md);
            border: 1px solid rgba(0,0,0,0.05);
            position: relative;
        }

        .testimonial-card::before {
            content: '"';
            position: absolute;
            top: 1rem;
            right: 1.5rem;
            font-family: var(--font-serif);
            font-size: 4rem;
            color: var(--color-accent);
            line-height: 1;
        }

        .testimonial-stars {
            color: #fbbf24;
            margin-bottom: 1rem;
        }

        .testimonial-text {
            color: var(--color-gray);
            margin-bottom: 1.5rem;
            font-style: italic;
        }

        .testimonial-author {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .testimonial-avatar {
            width: 48px;
            height: 48px;
            border-radius: 50%;
            object-fit: cover;
        }

        .testimonial-info h4 {
            font-size: 1rem;
            color: var(--color-primary);
        }

        .testimonial-info p {
            font-size: 0.875rem;
            color: var(--color-gray);
        }

        /* CTA Section */
        .cta-section {
            padding: 6rem 0;
            background: linear-gradient(135deg, var(--color-primary) 0%, var(--color-primary-light) 100%);
            color: white;
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .cta-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg width="60" height="60" viewBox="0 0 60 60" xmlns="http://www.w3.org/2000/svg"><g fill="none" fill-rule="evenodd"><g fill="%23ffffff" fill-opacity="0.05"><path d="M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z"/></g></g></svg>');
            opacity: 0.5;
        }

        .cta-content {
            position: relative;
            z-index: 1;
        }

        .cta-title {
            font-size: clamp(2rem, 4vw, 3rem);
            margin-bottom: 1rem;
        }

        .cta-description {
            font-size: 1.25rem;
            opacity: 0.95;
            max-width: 600px;
            margin: 0 auto 2rem;
        }

        /* Footer */
        .footer {
            background: var(--color-dark);
            color: white;
            padding: 4rem 0 2rem;
        }

        .footer-grid {
            display: grid;
            grid-template-columns: 2fr 1fr 1fr 1fr;
            gap: 3rem;
            margin-bottom: 3rem;
        }

        .footer-brand {
            max-width: 300px;
        }

        .footer-logo {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            margin-bottom: 1rem;
        }

        .footer-logo-icon {
            width: 40px;
            height: 40px;
            background: var(--color-primary);
            border-radius: var(--radius-sm);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
        }

        .footer-logo-text {
            font-family: var(--font-serif);
            font-size: 1.25rem;
            font-weight: 700;
        }

        .footer-description {
            color: rgba(255,255,255,0.7);
            font-size: 0.95rem;
            margin-bottom: 1.5rem;
        }

        .footer-social {
            display: flex;
            gap: 1rem;
        }

        .footer-social a {
            width: 40px;
            height: 40px;
            background: rgba(255,255,255,0.1);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s;
        }

        .footer-social a:hover {
            background: var(--color-secondary);
            transform: translateY(-3px);
        }

        .footer-title {
            font-size: 1rem;
            font-weight: 600;
            margin-bottom: 1.5rem;
            color: var(--color-secondary-light);
        }

        .footer-links {
            list-style: none;
        }

        .footer-links li {
            margin-bottom: 0.75rem;
        }

        .footer-links a {
            color: rgba(255,255,255,0.7);
            font-size: 0.95rem;
            transition: color 0.2s;
        }

        .footer-links a:hover {
            color: white;
        }

        .footer-contact-item {
            display: flex;
            align-items: flex-start;
            gap: 0.75rem;
            margin-bottom: 1rem;
            color: rgba(255,255,255,0.7);
            font-size: 0.95rem;
        }

        .footer-contact-item i {
            color: var(--color-secondary);
            margin-top: 0.25rem;
        }

        .footer-bottom {
            padding-top: 2rem;
            border-top: 1px solid rgba(255,255,255,0.1);
            display: flex;
            justify-content: space-between;
            align-items: center;
            color: rgba(255,255,255,0.5);
            font-size: 0.875rem;
        }

        /* Responsive */
        @media (max-width: 1024px) {
            .projects-grid,
            .testimonials-grid {
                grid-template-columns: repeat(2, 1fr);
            }

            .process-steps {
                grid-template-columns: repeat(2, 1fr);
            }

            .process-step:not(:last-child)::after {
                display: none;
            }

            .footer-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        @media (max-width: 768px) {
            .nav-links,
            .nav-cta .btn-outline {
                display: none;
            }

            .mobile-menu-btn {
                display: block;
            }

            .hero-stats {
                flex-direction: column;
                gap: 1.5rem;
            }

            .geoportal-features {
                grid-template-columns: repeat(2, 1fr);
            }

            .projects-grid,
            .testimonials-grid,
            .process-steps {
                grid-template-columns: 1fr;
            }

            .why-grid {
                grid-template-columns: 1fr;
            }

            .why-stats-card {
                position: relative;
                bottom: auto;
                left: auto;
                margin-top: 2rem;
            }

            .footer-grid {
                grid-template-columns: 1fr;
            }

            .footer-bottom {
                flex-direction: column;
                gap: 1rem;
                text-align: center;
            }
        }

        /* Animations */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .animate-on-scroll {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.6s ease;
        }

        .animate-on-scroll.visible {
            opacity: 1;
            transform: translateY(0);
        }
    </style>
</head>
<body>
    <!-- Navigation -->
    <nav class="navbar" id="navbar">
        <div class="container navbar-content">
            <a href="#" class="logo">
                <div class="logo-icon">
                    <i class="fas fa-mountain"></i>
                </div>
                <div class="logo-text">
                    <span class="logo-brand">Tierras del Ñuble</span>
                    <span class="logo-tagline">Parcelas de Agrado</span>
                </div>
            </a>

            <ul class="nav-links">
                <li><a href="#proyectos">Proyectos</a></li>
                <li><a href="#geoportal">Geoportal</a></li>
                <li><a href="#por-que-nosotros">¿Por qué nosotros?</a></li>
                <li><a href="#proceso">Proceso</a></li>
                <li><a href="#testimonios">Testimonios</a></li>
            </ul>

            <div class="nav-cta">
                <a href="#contacto" class="btn btn-outline">Contactar</a>
                <a href="#geoportal" class="btn btn-primary">Ver Geoportal</a>
                <button class="mobile-menu-btn">
                    <i class="fas fa-bars"></i>
                </button>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <section class="hero">
        <div class="hero-bg">
            <img src="https://images.unsplash.com/photo-1500382017468-9049fed747ef?w=1920&q=80" alt="Paisaje rural de Ñuble">
        </div>
        <div class="hero-overlay"></div>
        
        <div class="container hero-content">
            <div class="hero-badge">
                <i class="fas fa-map-marked-alt"></i>
                <span>Primera inmobiliaria con Geoportal Interactivo en Ñuble</span>
            </div>
            
            <h1 class="hero-title">
                Tu parcela de agrado en Ñuble, <span>visualizada antes de comprar</span>
            </h1>
            
            <p class="hero-description">
                Proyectos rurales verificados con tecnología geoespacial. Explora servicios, 
                plusvalía proyectada y potencial productivo desde tu computador o celular.
            </p>
            
            <div class="hero-cta">
                <a href="#geoportal" class="btn btn-secondary btn-large">
                    <i class="fas fa-layer-group"></i>
                    Explorar Geoportal
                </a>
                <a href="#proyectos" class="btn btn-outline btn-large" style="color: white; border-color: white;">
                    <i class="fas fa-th-large"></i>
                    Ver Proyectos
                </a>
            </div>

            <div class="hero-stats">
                <div class="hero-stat">
                    <div class="hero-stat-number">12+</div>
                    <div class="hero-stat-label">Proyectos activos</div>
                </div>
                <div class="hero-stat">
                    <div class="hero-stat-number">450+</div>
                    <div class="hero-stat-label">Familias instaladas</div>
                </div>
                <div class="hero-stat">
                    <div class="hero-stat-number">2.500</div>
                    <div class="hero-stat-label">Hectáreas vendidas</div>
                </div>
                <div class="hero-stat">
                    <div class="hero-stat-number">8</div>
                    <div class="hero-stat-label">Comunas de Ñuble</div>
                </div>
            </div>
        </div>
    </section>

    <!-- Geoportal Section -->
    <section class="geoportal-section" id="geoportal">
        <div class="container">
            <div class="section-header">
                <span class="section-label">Tecnología</span>
                <h2 class="section-title">Geoportal Interactivo: Tu parcela en detalle</h2>
                <p class="section-description">
                    La primera plataforma de visualización inmobiliaria de Ñuble. 
                    Accede a información que otras inmobiliarias no te entregan.
                </p>
            </div>

            <div class="geoportal-container">
                <div class="geoportal-header">
                    <div class="geoportal-title">
                        <i class="fas fa-map"></i>
                        <span>Geoportal Tierras del Ñuble - Proyecto Valle del Itata</span>
                    </div>
                    <div class="geoportal-controls">
                        <div class="geoportal-control">
                            <i class="fas fa-layer-group"></i>
                            <span>Capas</span>
                        </div>
                        <div class="geoportal-control">
                            <i class="fas fa-ruler-combined"></i>
                            <span>Medir</span>
                        </div>
                        <div class="geoportal-control">
                            <i class="fas fa-location-arrow"></i>
                            <span>Ubicarme</span>
                        </div>
                    </div>
                </div>
                
                <div id="map"></div>
                
                <div class="geoportal-features">
                    <div class="geoportal-feature">
                        <div class="geoportal-feature-icon">
                            <i class="fas fa-bolt"></i>
                        </div>
                        <div class="geoportal-feature-title">Servicios verificados</div>
                        <div class="geoportal-feature-desc">Luz, agua y conectividad</div>
                    </div>
                    <div class="geoportal-feature">
                        <div class="geoportal-feature-icon">
                            <i class="fas fa-chart-line"></i>
                        </div>
                        <div class="geoportal-feature-title">Plusvalía proyectada</div>
                        <div class="geoportal-feature-desc">Estimación 5-10 años</div>
                    </div>
                    <div class="geoportal-feature">
                        <div class="geoportal-feature-icon">
                            <i class="fas fa-seedling"></i>
                        </div>
                        <div class="geoportal-feature-title">Potencial productivo</div>
                        <div class="geoportal-feature-desc">Análisis de suelo y clima</div>
                    </div>
                    <div class="geoportal-feature">
                        <div class="geoportal-feature-icon">
                            <i class="fas fa-gavel"></i>
                        </div>
                        <div class="geoportal-feature-title">Normativa vigente</div>
                        <div class="geoportal-feature-desc">PRMU y restricciones</div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Projects Section -->
    <section class="projects-section" id="proyectos">
        <div class="container">
            <div class="projects-header">
                <div>
                    <span class="section-label">Proyectos</span>
                    <h2 class="section-title">Parcelas de agrado disponibles</h2>
                </div>
                <a href="#" class="btn btn-outline">Ver todos los proyectos</a>
            </div>

            <div class="projects-grid">
                <!-- Project 1 -->
                <div class="project-card">
                    <div class="project-image">
                        <img src="https://images.unsplash.com/photo-1500076656116-558758c991c1?w=800&q=80" alt="Valle del Itata">
                        <span class="project-badge">Últimas unidades</span>
                        <button class="project-favorite">
                            <i class="far fa-heart"></i>
                        </button>
                    </div>
                    <div class="project-content">
                        <div class="project-location">
                            <i class="fas fa-map-marker-alt"></i>
                            <span>San Nicolás, Ñuble</span>
                        </div>
                        <h3 class="project-title">Valle del Itata</h3>
                        <div class="project-features">
                            <span class="project-feature">
                                <i class="fas fa-expand"></i> 5.000 m²
                            </span>
                            <span class="project-feature">
                                <i class="fas fa-road"></i> Acceso pavimentado
                            </span>
                            <span class="project-feature">
                                <i class="fas fa-tint"></i> APR
                            </span>
                        </div>
                        <div class="project-footer">
                            <div class="project-price">
                                $39.900.000 <span>CLP</span>
                            </div>
                            <button class="btn btn-primary" style="padding: 0.625rem 1.25rem;">
                                Ver detalle
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Project 2 -->
                <div class="project-card">
                    <div class="project-image">
                        <img src="https://images.unsplash.com/photo-1518780664697-55e3ad937233?w=800&q=80" alt="Lomas de Chillán">
                        <span class="project-badge" style="background: var(--color-primary);">Nuevo</span>
                        <button class="project-favorite">
                            <i class="far fa-heart"></i>
                        </button>
                    </div>
                    <div class="project-content">
                        <div class="project-location">
                            <i class="fas fa-map-marker-alt"></i>
                            <span>Chillán Viejo, Ñuble</span>
                        </div>
                        <h3 class="project-title">Lomas de Chillán</h3>
                        <div class="project-features">
                            <span class="project-feature">
                                <i class="fas fa-expand"></i> 3.500 m²
                            </span>
                            <span class="project-feature">
                                <i class="fas fa-road"></i> Camino mantenido
                            </span>
                            <span class="project-feature">
                                <i class="fas fa-wifi"></i> Fibra óptica
                            </span>
                        </div>
                        <div class="project-footer">
                            <div class="project-price">
                                $28.500.000 <span>CLP</span>
                            </div>
                            <button class="btn btn-primary" style="padding: 0.625rem 1.25rem;">
                                Ver detalle
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Project 3 -->
                <div class="project-card">
                    <div class="project-image">
                        <img src="https://images.unsplash.com/photo-1464146072230-91cabc968266?w=800&q=80" alt="Mirador del Cordón">
                        <button class="project-favorite">
                            <i class="far fa-heart"></i>
                        </button>
                    </div>
                    <div class="project-content">
                        <div class="project-location">
                            <i class="fas fa-map-marker-alt"></i>
                            <span>San Fabián, Ñuble</span>
                        </div>
                        <h3 class="project-title">Mirador del Cordón</h3>
                        <div class="project-features">
                            <span class="project-feature">
                                <i class="fas fa-expand"></i> 10.000 m²
                            </span>
                            <span class="project-feature">
                                <i class="fas fa-mountain"></i> Vista cordillera
                            </span>
                            <span class="project-feature">
                                <i class="fas fa-tree"></i> Nativo
                            </span>
                        </div>
                        <div class="project-footer">
                            <div class="project-price">
                                $45.000.000 <span>CLP</span>
                            </div>
                            <button class="btn btn-primary" style="padding: 0.625rem 1.25rem;">
                                Ver detalle
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Why Us Section -->
    <section class="why-section" id="por-que-nosotros">
        <div class="container">
            <div class="why-grid">
                <div class="why-content">
                    <span class="section-label">Diferencia</span>
                    <h2 class="section-title">¿Por qué comprar con nosotros?</h2>
                    <p class="section-description">
                        Somos la única inmobiliaria de Ñuble que combina desarrollo de proyectos 
                        rurales con tecnología geoespacial de precisión. No vendemos parcelas, 
                        vendemos certeza territorial.
                    </p>

                    <div class="why-features">
                        <div class="why-feature">
                            <div class="why-feature-icon">
                                <i class="fas fa-map-marked-alt"></i>
                            </div>
                            <div class="why-feature-content">
                                <h4>Geoportal exclusivo</h4>
                                <p>Visualiza tu parcela con servicios, normativa y potencial productivo antes de visitar.</p>
                            </div>
                        </div>
                        <div class="why-feature">
                            <div class="why-feature-icon">
                                <i class="fas fa-file-contract"></i>
                            </div>
                            <div class="why-feature-content">
                                <h4>Documentación transparente</h4>
                                <p>Todos nuestros proyectos cuentan con estudios de suelo, factibilidad de servicios y normativa vigente.</p>
                            </div>
                        </div>
                        <div class="why-feature">
                            <div class="why-feature-icon">
                                <i class="fas fa-hands-helping"></i>
                            </div>
                            <div class="why-feature-content">
                                <h4>Acompañamiento post-venta</h4>
                                <p>Te ayudamos con conexión de servicios, permisos de edificación y asesoría productiva.</p>
                            </div>
                        </div>
                        <div class="why-feature">
                            <div class="why-feature-icon">
                                <i class="fas fa-shield-alt"></i>
                            </div>
                            <div class="why-feature-content">
                                <h4>Garantía de plusvalía</h4>
                                <p>Proyectos en zonas con crecimiento demográfico y desarrollo de infraestructura verificados.</p>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="why-image">
                    <img src="https://images.unsplash.com/photo-1564013799919-ab600027ffc6?w=800&q=80" alt="Familia en parcela">
                    <div class="why-stats-card">
                        <div class="why-stats-card-number">98%</div>
                        <div class="why-stats-card-text">de clientes recomiendan<br>Tierras del Ñuble</div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Process Section -->
    <section class="process-section" id="proceso">
        <div class="container">
            <div class="section-header">
                <span class="section-label">Proceso</span>
                <h2 class="section-title">De la visualización a tu parcela en 4 pasos</h2>
                <p class="section-description">
                    Hemos simplificado el proceso de compra de parcelas de agrado 
                    combinando tecnología digital con asesoría humana.
                </p>
            </div>

            <div class="process-steps">
                <div class="process-step">
                    <div class="process-step-number">1</div>
                    <h3 class="process-step-title">Explora en el Geoportal</h3>
                    <p class="process-step-description">
                        Navega proyectos, compara parcelas, visualiza servicios y solicita información específica online.
                    </p>
                </div>
                <div class="process-step">
                    <div class="process-step-number">2</div>
                    <h3 class="process-step-title">Visita con asesor</h3>
                    <p class="process-step-description">
                        Agendamos visita guiada al proyecto. Recorres la parcela real con GPS y verificas todo lo visto online.
                    </p>
                </div>
                <div class="process-step">
                    <div class="process-step-number">3</div>
                    <h3 class="process-step-title">Reserva y documentación</h3>
                    <p class="process-step-description">
                        Reserva con 10% del valor. Nuestro equipo gestiona estudios de título, firmas y permisos necesarios.
                    </p>
                </div>
                <div class="process-step">
                    <div class="process-step-number">4</div>
                    <h3 class="process-step-title">Escritura y post-venta</h3>
                    <p class="process-step-description">
                        Firma escritura pública. Te acompañamos en conexión de servicios y asesoría para desarrollar tu proyecto.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- Testimonials Section -->
    <section class="testimonials-section" id="testimonios">
        <div class="container">
            <div class="section-header">
                <span class="section-label">Testimonios</span>
                <h2 class="section-title">Lo que dicen nuestros clientes</h2>
                <p class="section-description">
                    Familias que encontraron su lugar en el campo de Ñuble.
                </p>
            </div>

            <div class="testimonials-grid">
                <div class="testimonial-card">
                    <div class="testimonial-stars">
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                    </div>
                    <p class="testimonial-text">
                        "El geoportal fue clave. Pudimos ver que la parcela tenía acceso directo a la ruta y la red de agua potable antes de ir a terreno. Eso no lo tiene ninguna otra inmobiliaria."
                    </p>
                    <div class="testimonial-author">
                        <img src="https://randomuser.me/api/portraits/men/32.jpg" alt="Carlos" class="testimonial-avatar">
                        <div class="testimonial-info">
                            <h4>Carlos Muñoz</h4>
                            <p>Valle del Itata, San Nicolás</p>
                        </div>
                    </div>
                </div>

                <div class="testimonial-card">
                    <div class="testimonial-stars">
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                    </div>
                    <p class="testimonial-text">
                        "Vivimos en Santiago y compramos sin visitar primero gracias al geoportal. La información era tan detallada que nos sentimos seguros. Luego fuimos a firmar y todo coincidió."
                    </p>
                    <div class="testimonial-author">
                        <img src="https://randomuser.me/api/portraits/women/44.jpg" alt="María" class="testimonial-avatar">
                        <div class="testimonial-info">
                            <h4>María José Riquelme</h4>
                            <p>Lomas de Chillán, Chillán Viejo</p>
                        </div>
                    </div>
                </div>

                <div class="testimonial-card">
                    <div class="testimonial-stars">
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                        <i class="fas fa-star"></i>
                    </div>
                    <p class="testimonial-text">
                        "Nos ayudaron con todo el proceso de conexión a la APR de la zona. Ahora tenemos agua potable rural funcionando perfecto. Un servicio que no esperábamos y valoramos mucho."
                    </p>
                    <div class="testimonial-author">
                        <img src="https://randomuser.me/api/portraits/men/67.jpg" alt="Pedro" class="testimonial-avatar">
                        <div class="testimonial-info">
                            <h4>Pedro y Ana González</h4>
                            <p>Mirador del Cordón, San Fabián</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- CTA Section -->
    <section class="cta-section" id="contacto">
        <div class="container cta-content">
            <h2 class="cta-title">Encuentra tu parcela ideal hoy</h2>
            <p class="cta-description">
                Explora nuestro geoportal interactivo o agenda una visita guiada 
                con nuestros asesores especializados en desarrollo rural.
            </p>
            <div style="display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap;">
                <a href="#geoportal" class="btn btn-secondary btn-large">
                    <i class="fas fa-layer-group"></i>
                    Explorar Geoportal
                </a>
                <a href="https://wa.me/569XXXXXXXX" class="btn btn-outline btn-large" style="color: white; border-color: white;">
                    <i class="fab fa-whatsapp"></i>
                    Hablar por WhatsApp
                </a>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
        <div class="container">
            <div class="footer-grid">
                <div class="footer-brand">
                    <div class="footer-logo">
                        <div class="footer-logo-icon">
                            <i class="fas fa-mountain"></i>
                        </div>
                        <span class="footer-logo-text">Tierras del Ñuble</span>
                    </div>
                    <p class="footer-description">
                        Primera inmobiliaria de Ñuble con tecnología geoespacial. 
                        Desarrollamos proyectos de parcelas de agrado con transparencia 
                        y acompañamiento integral.
                    </p>
                    <div class="footer-social">
                        <a href="#"><i class="fab fa-facebook-f"></i></a>
                        <a href="#"><i class="fab fa-instagram"></i></a>
                        <a href="#"><i class="fab fa-linkedin-in"></i></a>
                        <a href="#"><i class="fab fa-youtube"></i></a>
                    </div>
                </div>

                <div>
                    <h4 class="footer-title">Proyectos</h4>
                    <ul class="footer-links">
                        <li><a href="#">Valle del Itata</a></li>
                        <li><a href="#">Lomas de Chillán</a></li>
                        <li><a href="#">Mirador del Cordón</a></li>
                        <li><a href="#">Los Robles</a></li>
                        <li><a href="#">Ver todos</a></li>
                    </ul>
                </div>

                <div>
                    <h4 class="footer-title">Servicios</h4>
                    <ul class="footer-links">
                        <li><a href="#">Geoportal Interactivo</a></li>
                        <li><a href="#">Asesoría Productiva</a></li>
                        <li><a href="#">Gestión de Servicios</a></li>
                        <li><a href="#">Permisos y Normativa</a></li>
                        <li><a href="#">Post-venta</a></li>
                    </ul>
                </div>

                <div>
                    <h4 class="footer-title">Contacto</h4>
                    <div class="footer-contact-item">
                        <i class="fas fa-map-marker-alt"></i>
                        <span>Av. Libertad 1234, Chillán, Ñuble</span>
                    </div>
                    <div class="footer-contact-item">
                        <i class="fas fa-phone"></i>
                        <span>+56 9 XXXX XXXX</span>
                    </div>
                    <div class="footer-contact-item">
                        <i class="fas fa-envelope"></i>
                        <span>contacto@tierrasdelnuble.cl</span>
                    </div>
                    <div class="footer-contact-item">
                        <i class="fas fa-clock"></i>
                        <span>Lun-Vie: 9:00 - 18:00 hrs</span>
                    </div>
                </div>
            </div>

            <div class="footer-bottom">
                <p>&copy; 2024 Tierras del Ñuble SpA. Todos los derechos reservados.</p>
                <div style="display: flex; gap: 2rem;">
                    <a href="#" style="color: inherit;">Política de privacidad</a>
                    <a href="#" style="color: inherit;">Términos de uso</a>
                </div>
            </div>
        </div>
    </footer>

    <!-- Scripts -->
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
    <script>
        // Navbar scroll effect
        window.addEventListener('scroll', () => {
            const navbar = document.getElementById('navbar');
            if (window.scrollY > 50) {
                navbar.classList.add('scrolled');
            } else {
                navbar.classList.remove('scrolled');
            }
        });

        // Initialize Map
        document.addEventListener('DOMContentLoaded', () => {
            // Coordenadas de Ñuble (aproximadas)
            const map = L.map('map').setView([-36.6, -72.1], 10);

            // Capas base
            const satellite = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
                attribution: 'Esri',
                maxZoom: 18
            });

            const osm = L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
                attribution: 'OpenStreetMap',
                maxZoom: 19
            });

            satellite.addTo(map);

            // Control de capas
            L.control.layers({
                "Satélite": satellite,
                "Mapa": osm
            }).addTo(map);

            // Marcadores de ejemplo (proyectos)
            const proyectos = [
                { lat: -36.5, lng: -72.0, nombre: "Valle del Itata", precio: "$39.9M" },
                { lat: -36.65, lng: -72.1, nombre: "Lomas de Chillán", precio: "$28.5M" },
                { lat: -36.55, lng: -71.55, nombre: "Mirador del Cordón", precio: "$45M" }
            ];

            proyectos.forEach(proy => {
                const marker = L.marker([proy.lat, proy.lng]).addTo(map);
                marker.bindPopup(`
                    <div style="font-family: Inter, sans-serif; min-width: 200px;">
                        <h4 style="margin: 0 0 8px 0; color: #1a4d2e; font-family: Playfair Display, serif;">${proy.nombre}</h4>
                        <p style="margin: 0 0 8px 0; color: #666; font-size: 0.9rem;">Parcelas desde ${proy.precio}</p>
                        <button style="background: #bc6c25; color: white; border: none; padding: 6px 12px; border-radius: 6px; cursor: pointer; font-size: 0.85rem;">Ver detalle</button>
                    </div>
                `);
            });

            // Ajustar tamaño cuando la sección es visible
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        setTimeout(() => {
                            map.invalidateSize();
                        }, 100);
                    }
                });
            });

            observer.observe(document.getElementById('map'));
        });

        // Smooth scroll para enlaces internos
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });

        // Animación on scroll
        const observerOptions = {
            threshold: 0.1,
            rootMargin: '0px 0px -50px 0px'
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('visible');
                }
            });
        }, observerOptions);

        document.querySelectorAll('.animate-on-scroll').forEach(el => {
            observer.observe(el);
        });
    </script>
</body>
</html>
