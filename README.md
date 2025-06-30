<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Yakesh Choudhery - Full Stack AI Developer</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0a0a0a 0%, #1a1a2e 50%, #16213e 100%);
            color: #ffffff;
            overflow-x: hidden;
            line-height: 1.6;
        }

        #bg-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 1;
        }

        .hero-section {
            text-align: center;
            padding: 100px 0;
            position: relative;
        }

        .profile-card {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border-radius: 25px;
            padding: 40px;
            margin: 20px 0;
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
            transform: perspective(1000px) rotateX(5deg);
            transition: all 0.3s ease;
        }

        .profile-card:hover {
            transform: perspective(1000px) rotateX(0deg) translateY(-10px);
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.4);
        }

        .name-title {
            font-size: 3.5rem;
            font-weight: 700;
            background: linear-gradient(45deg, #00d4ff, #ff00ff, #ffff00);
            background-size: 300% 300%;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: gradientShift 3s ease-in-out infinite;
            margin-bottom: 10px;
        }

        @keyframes gradientShift {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        .subtitle {
            font-size: 1.5rem;
            color: #00d4ff;
            margin-bottom: 30px;
            text-shadow: 0 0 20px rgba(0, 212, 255, 0.5);
        }

        .about-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin: 40px 0;
        }

        .about-item {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 25px;
            border-left: 4px solid #00d4ff;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .about-item::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
            transition: left 0.5s;
        }

        .about-item:hover::before {
            left: 100%;
        }

        .about-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 30px rgba(0, 212, 255, 0.2);
        }

        .about-item h3 {
            color: #00d4ff;
            margin-bottom: 10px;
            font-size: 1.2rem;
        }

        .social-links {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 30px 0;
        }

        .social-btn {
            background: linear-gradient(45deg, #00d4ff, #0099cc);
            border: none;
            border-radius: 50px;
            padding: 15px 30px;
            color: white;
            text-decoration: none;
            font-weight: bold;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .social-btn::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            background: rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            transition: all 0.3s ease;
            transform: translate(-50%, -50%);
        }

        .social-btn:hover::before {
            width: 300px;
            height: 300px;
        }

        .social-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(0, 212, 255, 0.4);
        }

        .stats-section {
            background: rgba(255, 255, 255, 0.08);
            border-radius: 20px;
            padding: 30px;
            margin: 40px 0;
            text-align: center;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .stat-item {
            background: linear-gradient(135deg, rgba(0, 212, 255, 0.1), rgba(255, 0, 255, 0.1));
            border-radius: 15px;
            padding: 20px;
            transition: transform 0.3s ease;
        }

        .stat-item:hover {
            transform: scale(1.05);
        }

        .stat-number {
            font-size: 2rem;
            font-weight: bold;
            color: #00d4ff;
        }

        .floating-elements {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .floating-element {
            position: absolute;
            background: linear-gradient(45deg, #00d4ff, #ff00ff);
            border-radius: 50%;
            opacity: 0.1;
            animation: float 6s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(180deg); }
        }

        .contact-section {
            text-align: center;
            padding: 40px;
            background: linear-gradient(135deg, rgba(0, 212, 255, 0.1), rgba(255, 0, 255, 0.1));
            border-radius: 20px;
            margin: 40px 0;
        }

        .fun-fact {
            background: linear-gradient(45deg, #ff00ff, #00d4ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            font-size: 1.2rem;
            font-weight: bold;
            margin: 20px 0;
            animation: pulse 2s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        @media (max-width: 768px) {
            .name-title {
                font-size: 2.5rem;
            }
            
            .about-grid {
                grid-template-columns: 1fr;
            }
            
            .social-links {
                flex-direction: column;
                align-items: center;
            }
        }
    </style>
</head>
<body>
    <canvas id="bg-canvas"></canvas>
    
    <div class="floating-elements">
        <div class="floating-element" style="width: 20px; height: 20px; top: 10%; left: 10%; animation-delay: 0s;"></div>
        <div class="floating-element" style="width: 15px; height: 15px; top: 20%; left: 80%; animation-delay: 1s;"></div>
        <div class="floating-element" style="width: 25px; height: 25px; top: 60%; left: 20%; animation-delay: 2s;"></div>
        <div class="floating-element" style="width: 18px; height: 18px; top: 80%; left: 70%; animation-delay: 3s;"></div>
        <div class="floating-element" style="width: 22px; height: 22px; top: 40%; left: 90%; animation-delay: 4s;"></div>
    </div>

    <div class="container">
        <div class="hero-section">
            <div class="profile-card">
                <h1 class="name-title">Yakesh Choudhery</h1>
                <p class="subtitle">🚀 Full Stack Generative AI Developer (MERN)</p>
                
                <div class="about-grid">
                    <div class="about-item">
                        <h3>🔭 Currently Working On</h3>
                        <p>Full Stack Generative AI Development with MERN stack, building intelligent applications that push the boundaries of what's possible.</p>
                    </div>
                    
                    <div class="about-item">
                        <h3>🤝 Looking For</h3>
                        <p>Open Source Contribution opportunities to collaborate with amazing developers and contribute to impactful projects.</p>
                    </div>
                    
                    <div class="about-item">
                        <h3>🌱 Currently Learning</h3>
                        <p>Machine Learning algorithms and the Czech Language (A2 Current level) - expanding both technical and cultural horizons!</p>
                    </div>
                    
                    <div class="about-item">
                        <h3>💬 Ask Me About</h3>
                        <p>Inspiring to Innovate, Always Think About Quality Outcome. I believe in creating solutions that make a real difference.</p>
                    </div>
                </div>

                <div class="fun-fact">
                    ⚡ Fun Fact: Modern Developer = Soft_Dev(web) & UX/UI pro + Gen AI(RAG & Agentic AI)
                </div>

                <div class="social-links">
                    <a href="https://www.linkedin.com/in/yakeshchoudhery/" class="social-btn">
                        LinkedIn Connect
                    </a>
                    <a href="mailto:yakeshchoudhery08@gmail.com" class="social-btn">
                        Email Me
                    </a>
                    <a href="https://yakeshchoudhery.tech" class="social-btn">
                        View Portfolio
                    </a>
                </div>
            </div>
        </div>

        <div class="stats-section">
            <h2 style="color: #00d4ff; margin-bottom: 20px;">📊 GitHub Analytics</h2>
            <div class="stats-grid">
                <div class="stat-item">
                    <div class="stat-number">500+</div>
                    <div>Commits This Year</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number">25+</div>
                    <div>Active Repositories</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number">15+</div>
                    <div>Languages Mastered</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number">100+</div>
                    <div>Days Streak</div>
                </div>
            </div>
        </div>

        <div class="contact-section">
            <h2 style="color: #00d4ff; margin-bottom: 20px;">🌟 Let's Build Something Amazing Together!</h2>
            <p>Ready to collaborate on cutting-edge AI projects? Let's connect and create innovative solutions that shape the future of technology.</p>
            <div style="margin-top: 20px;">
                <a href="mailto:yakeshchoudhery08@gmail.com" class="social-btn">Start a Conversation</a>
            </div>
        </div>
    </div>

    <script>
        // Three.js Background Animation
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ canvas: document.getElementById('bg-canvas'), alpha: true });
        
        renderer.setSize(window.innerWidth, window.innerHeight);
        camera.position.z = 5;

        // Create floating particles
        const geometry = new THREE.SphereGeometry(0.05, 8, 8);
        const material = new THREE.MeshBasicMaterial({ 
            color: 0x00d4ff,
            transparent: true,
            opacity: 0.6
        });

        const particles = [];
        for (let i = 0; i < 50; i++) {
            const particle = new THREE.Mesh(geometry, material);
            particle.position.x = (Math.random() - 0.5) * 20;
            particle.position.y = (Math.random() - 0.5) * 20;
            particle.position.z = (Math.random() - 0.5) * 20;
            
            particle.userData = {
                velocity: {
                    x: (Math.random() - 0.5) * 0.02,
                    y: (Math.random() - 0.5) * 0.02,
                    z: (Math.random() - 0.5) * 0.02
                }
            };
            
            particles.push(particle);
            scene.add(particle);
        }

        // Create floating cubes
        const cubeGeometry = new THREE.BoxGeometry(0.1, 0.1, 0.1);
        const cubeMaterial = new THREE.MeshBasicMaterial({ 
            color: 0xff00ff,
            transparent: true,
            opacity: 0.4
        });

        const cubes = [];
        for (let i = 0; i < 20; i++) {
            const cube = new THREE.Mesh(cubeGeometry, cubeMaterial);
            cube.position.x = (Math.random() - 0.5) * 15;
            cube.position.y = (Math.random() - 0.5) * 15;
            cube.position.z = (Math.random() - 0.5) * 15;
            
            cube.userData = {
                rotationSpeed: {
                    x: Math.random() * 0.02,
                    y: Math.random() * 0.02,
                    z: Math.random() * 0.02
                }
            };
            
            cubes.push(cube);
            scene.add(cube);
        }

        // Animation loop
        function animate() {
            requestAnimationFrame(animate);

            // Animate particles
            particles.forEach(particle => {
                particle.position.x += particle.userData.velocity.x;
                particle.position.y += particle.userData.velocity.y;
                particle.position.z += particle.userData.velocity.z;

                // Bounce off boundaries
                if (Math.abs(particle.position.x) > 10) particle.userData.velocity.x *= -1;
                if (Math.abs(particle.position.y) > 10) particle.userData.velocity.y *= -1;
                if (Math.abs(particle.position.z) > 10) particle.userData.velocity.z *= -1;
            });

            // Animate cubes
            cubes.forEach(cube => {
                cube.rotation.x += cube.userData.rotationSpeed.x;
                cube.rotation.y += cube.userData.rotationSpeed.y;
                cube.rotation.z += cube.userData.rotationSpeed.z;
            });

            renderer.render(scene, camera);
        }

        animate();

        // Handle window resize
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });

        // Mouse interaction
        let mouseX = 0;
        let mouseY = 0;

        document.addEventListener('mousemove', (event) => {
            mouseX = (event.clientX / window.innerWidth) * 2 - 1;
            mouseY = -(event.clientY / window.innerHeight) * 2 + 1;
            
            camera.position.x = mouseX * 0.5;
            camera.position.y = mouseY * 0.5;
            camera.lookAt(0, 0, 0);
        });

        // Scroll animations
        window.addEventListener('scroll', () => {
            const scrolled = window.pageYOffset;
            const parallax = scrolled * 0.5;
            
            scene.rotation.y = scrolled * 0.001;
            scene.rotation.x = scrolled * 0.0005;
        });

        // Add some interactive elements
        document.querySelectorAll('.profile-card, .about-item, .stat-item').forEach(element => {
            element.addEventListener('mouseenter', () => {
                element.style.transform += ' scale(1.02)';
            });
            
            element.addEventListener('mouseleave', () => {
                element.style.transform = element.style.transform.replace(' scale(1.02)', '');
            });
        });
    </script>
</body>
</html>
