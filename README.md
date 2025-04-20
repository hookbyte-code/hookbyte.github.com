<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HookByte | Modern Marketing Solutions</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/gsap@3.12.2/dist/gsap.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #6366f1;
            --secondary: #8b5cf6;
            --accent: #ec4899;
            --dark: #0f172a;
            --light: #f8fafc;
            --glass: rgba(255, 255, 255, 0.08);
            --gradient: linear-gradient(135deg, var(--primary), var(--accent));
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        body {
            background: var(--dark);
            color: var(--light);
            overflow-x: hidden;
        }

        /* Modern 3D Background */
        #canvas3d {
            position: fixed;
            top: 0;
            left: 0;
            z-index: -1;
            filter: blur(0px) contrast(120%);
        }

        /* Ultra-slim Navigation */
        .navbar {
            position: fixed;
            width: 90%;
            margin: 1.5rem 5%;
            padding: 1.2rem 2.5rem;
            background: var(--glass);
            backdrop-filter: blur(20px);
            border-radius: 1.5rem;
            border: 1px solid rgba(255,255,255,0.12);
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
            z-index: 1000;
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
        }

        .navbar:hover {
            transform: translateY(-2px);
            box-shadow: 0 12px 48px rgba(99, 102, 241, 0.15);
        }

        .logo {
            font-size: 1.8rem;
            font-weight: 700;
            background: var(--gradient);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: -0.03em;
        }

        /* Modern Hero Section */
        .hero {
            min-height: 100vh;
            display: flex;
            align-items: center;
            padding: 0 5%;
            position: relative;
        }

        .hero-content {
            max-width: 1400px;
            margin: 0 auto;
            position: relative;
            z-index: 2;
        }

        .hero h1 {
            font-size: 5rem;
            line-height: 1.05;
            margin-bottom: 2rem;
            font-weight: 700;
            background: var(--gradient);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: -0.03em;
            max-width: 900px;
        }

        /* Futuristic Services Grid */
        .services-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 2.5rem;
            margin-top: 4rem;
        }

        .service-card {
            background: var(--glass);
            padding: 2.5rem;
            border-radius: 1.5rem;
            border: 1px solid rgba(255,255,255,0.1);
            backdrop-filter: blur(12px);
            transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
            position: relative;
            overflow: hidden;
        }

        .service-card::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: var(--gradient);
            opacity: 0.1;
            transform: rotate(45deg);
            transition: all 0.6s ease;
        }

        .service-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 16px 32px rgba(99, 102, 241, 0.15);
        }

        .service-card:hover::before {
            transform: rotate(45deg) translate(50%, -50%);
        }

        /* Holographic Buttons */
        .glow-button {
            position: relative;
            background: var(--glass);
            border: 1px solid rgba(255,255,255,0.1);
            padding: 1.2rem 2.4rem;
            border-radius: 1.2rem;
            color: var(--light);
            font-weight: 600;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
            overflow: hidden;
        }

        .glow-button::after {
            content: '';
            position: absolute;
            inset: 0;
            background: var(--gradient);
            opacity: 0;
            transition: opacity 0.4s ease;
        }

        .glow-button:hover {
            border-color: transparent;
        }

        .glow-button:hover::after {
            opacity: 0.2;
        }

        /* Floating Consultation Card */
        .zoom-box {
            background: var(--glass);
            padding: 3rem;
            border-radius: 2rem;
            border: 1px solid rgba(255,255,255,0.1);
            backdrop-filter: blur(12px);
            position: relative;
            overflow: hidden;
            animation: float 6s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }

        /* Modern Testimonials */
        .testimonials-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(340px, 1fr));
            gap: 2.5rem;
            margin-top: 4rem;
        }

        .testimonial-card {
            background: var(--glass);
            padding: 2.5rem;
            border-radius: 1.5rem;
            border: 1px solid rgba(255,255,255,0.1);
            backdrop-filter: blur(12px);
            transition: all 0.4s ease;
        }

        /* Advanced Contact Form */
        .contact-form {
            max-width: 700px;
            margin: 0 auto;
        }

        .form-group {
            margin-bottom: 2rem;
            position: relative;
        }

        input, textarea {
            width: 100%;
            padding: 1.2rem;
            background: var(--glass);
            border: 1px solid rgba(255,255,255,0.1);
            border-radius: 1rem;
            color: var(--light);
            transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
        }

        input:focus, textarea:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 24px rgba(99, 102, 241, 0.2);
        }

        @media (max-width: 1024px) {
            .hero h1 {
                font-size: 3.5rem;
            }
        }

        @media (max-width: 768px) {
            .hero h1 {
                font-size: 2.8rem;
            }
            
            .service-card {
                padding: 2rem;
            }
        }
    </style>
</head>
<body>
    <canvas id="canvas3d"></canvas>
    
    <!-- Navigation -->
    <nav class="navbar">
        <div class="logo">HookByte</div>
        <div class="nav-links">
            <a href="#home" class="glow-button">Home</a>
            <a href="#services" class="glow-button">Services</a>
            <a href="#testimonials" class="glow-button">Testimonials</a>
            <a href="#contact" class="glow-button">Contact</a>
        </div>
    </nav>

    <!-- Hero Section -->
    <section class="hero" id="home">
        <div class="hero-content">
            <h1>Redefining Digital Growth Through Intelligent Marketing Solutions</h1>
            <button class="glow-button">Explore Our Vision →</button>
        </div>
    </section>

    <!-- Services Section -->
    <section class="services" id="services">
        <h2 class="section-title">Core Solutions</h2>
        <div class="services-grid">
            <div class="service-card">
                <i class="fas fa-rocket fa-2x" style="color: var(--accent); margin-bottom: 1.5rem;"></i>
                <h3>AI-Powered Lead Generation</h3>
                <p>Machine learning-driven campaigns with real-time optimization</p>
            </div>
            <div class="service-card">
                <i class="fas fa-chart-network fa-2x" style="color: var(--accent); margin-bottom: 1.5rem;"></i>
                <h3>Social Media Mastery</h3>
                <p>Omnichannel strategies with predictive analytics</p>
            </div>
            <div class="service-card">
                <i class="fas fa-code fa-2x" style="color: var(--accent); margin-bottom: 1.5rem;"></i>
                <h3>Next-Gen Web Development</h3>
                <p>React-based solutions with Web3 integration</p>
            </div>
        </div>
    </section>

    <!-- Consultation Section -->
    <section class="consultation">
        <div class="zoom-box">
            <h2>Strategic Consultation</h2>
            <p>45-minute immersive strategy session with our experts</p>
            <button class="glow-button">Schedule Session</button>
        </div>
    </section>

    <!-- Testimonials Section -->
    <section class="testimonials" id="testimonials">
        <div class="testimonials-grid">
            <div class="testimonial-card">
                <div class="client-header">
                    <img src="https://randomuser.me/api/portraits/men/1.jpg" class="client-avatar">
                    <div class="client-info">
                        <h3>Michael Chen</h3>
                        <p>CEO, TechNova</p>
                    </div>
                </div>
                <p>"HookByte's AI-driven approach generated 300% more qualified leads in 90 days."</p>
            </div>
        </div>
    </section>

    <script>
        // Advanced Particle System
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ 
            canvas: document.querySelector('#canvas3d'),
            antialias: true,
            alpha: true
        });

        // Create dynamic particles
        const geometry = new THREE.BufferGeometry();
        const count = 5000;
        const positions = new Float32Array(count * 3);

        for(let i = 0; i < count * 3; i += 3) {
            positions[i] = (Math.random() - 0.5) * 10;
            positions[i + 1] = (Math.random() - 0.5) * 10;
            positions[i + 2] = (Math.random() - 0.5) * 10;
        }

        geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
        
        const material = new THREE.PointsMaterial({
            size: 0.02,
            color: new THREE.Color().setHSL(0.7, 0.8, 0.6),
            transparent: true,
            opacity: 0.8,
            blending: THREE.AdditiveBlending
        });

        const particles = new THREE.Points(geometry, material);
        scene.add(particles);

        camera.position.z = 3;

        // Mouse interaction
        document.addEventListener('mousemove', (e) => {
            particles.rotation.x = e.clientY * 0.0001;
            particles.rotation.y = e.clientX * 0.0001;
        });

        function animate() {
            requestAnimationFrame(animate);
            renderer.render(scene, camera);
        }
        animate();

        // GSAP Scroll Animations
        gsap.utils.toArray('.service-card').forEach(card => {
            gsap.from(card, {
                scrollTrigger: {
                    trigger: card,
                    start: "top 80%"
                },
                y: 100,
                opacity: 0,
                duration: 1.2,
                ease: "power4.out"
            });
        });
    </script>
</body>
</html>
