<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Happy Birthday Mhin - 19th Birthday</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', 'Segoe UI', 'Poppins', sans-serif;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: background-color 0.8s ease;
            overflow-x: hidden;
        }

        /* Screen 1 - Black background */
        body.screen1 {
            background-color: #0a0a0a;
        }

        /* Screen 2 - Violet/Pink gradient background */
        body.screen2 {
            background: linear-gradient(135deg, #8B5CF6 0%, #c084fc 50%, #e879f9 100%);
        }

        .container {
            text-align: center;
            padding: 20px;
            width: 100%;
        }

        /* Screen 1 Styles */
        .welcome-text {
            font-size: 80px;
            font-weight: bold;
            color: white;
            margin-bottom: 40px;
            animation: fadeIn 1s ease-in;
            text-shadow: 0 0 20px rgba(139, 92, 246, 0.5);
        }

        .continue-btn {
            background: linear-gradient(135deg, #8B5CF6, #c084fc);
            color: white;
            font-size: 24px;
            font-weight: bold;
            padding: 15px 50px;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            animation: fadeIn 1s ease-in 0.3s both;
            box-shadow: 0 5px 20px rgba(139, 92, 246, 0.4);
        }

        .continue-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 30px rgba(139, 92, 246, 0.6);
        }

        /* Screen 2 Styles */
        .screen2-content {
            display: none;
        }

        body.screen2 .screen1-content {
            display: none;
        }

        body.screen2 .screen2-content {
            display: block;
        }

        /* 3D Canvas styling */
        #cakeCanvas {
            width: 100%;
            max-width: 500px;
            height: auto;
            aspect-ratio: 1 / 1;
            display: block;
            margin: 0 auto;
            cursor: pointer;
            border-radius: 20px;
        }

        .birthday-text {
            font-size: 48px;
            font-weight: bold;
            color: white;
            text-shadow: 3px 3px 6px rgba(0, 0, 0, 0.3);
            margin-top: 20px;
            animation: fadeInUp 0.8s ease;
            background: linear-gradient(135deg, #fff, #fbcfe8);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: none;
        }

        .instruction {
            color: rgba(255, 255, 255, 0.7);
            margin-top: 15px;
            font-size: 14px;
            animation: fadeInUp 1s ease;
        }

        /* Animations */
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: scale(0.9);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

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

        @keyframes float {
            0%, 100% {
                transform: translateY(0px);
            }
            50% {
                transform: translateY(-10px);
            }
        }

        /* Confetti styles */
        .confetti-particle {
            position: fixed;
            pointer-events: none;
            z-index: 10000;
        }

        @keyframes fall {
            to {
                transform: translateY(100vh) rotate(360deg);
            }
        }

        /* Responsive */
        @media (max-width: 600px) {
            .welcome-text {
                font-size: 50px;
            }
            
            .continue-btn {
                font-size: 18px;
                padding: 12px 40px;
            }
            
            .birthday-text {
                font-size: 32px;
            }
            
            #cakeCanvas {
                max-width: 350px;
            }
        }

        /* Heart decoration */
        .hearts {
            position: fixed;
            bottom: 20px;
            right: 20px;
            font-size: 30px;
            opacity: 0.6;
            pointer-events: none;
        }
    </style>
</head>
<body class="screen1">
    <div class="container">
        <!-- Screen 1: Welcome + Continue Button -->
        <div class="screen1-content">
            <div class="welcome-text">
                Welcome
            </div>
            <button class="continue-btn" onclick="goToBirthday()">
                Continue 💜
            </button>
        </div>

        <!-- Screen 2: 3D Cake + Happy Birthday Mhin -->
        <div class="screen2-content">
            <canvas id="cakeCanvas"></canvas>
            <div class="birthday-text">
                🎀 Happy Birthday Mhin! 🎀
            </div>
            <div class="instruction">
                ✨ Click the cake for confetti! ✨
            </div>
        </div>
    </div>
    <div class="hearts">💜💗💕</div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script>
        let scene, camera, renderer, cakeGroup, birthdayText3D;

        function goToBirthday() {
            // Change background to violet gradient
            document.body.classList.remove('screen1');
            document.body.classList.add('screen2');
            
            // Initialize 3D cake after transition
            setTimeout(() => {
                init3DCake();
                createSparkles();
            }, 100);
        }

        function init3DCake() {
            const canvas = document.getElementById('cakeCanvas');
            const container = canvas.parentElement;
            
            // Get canvas size
            const width = canvas.clientWidth;
            const height = canvas.clientHeight;
            
            // Create scene
            scene = new THREE.Scene();
            scene.background = null; // Transparent
            
            // Create camera
            camera = new THREE.PerspectiveCamera(45, width / height, 0.1, 1000);
            camera.position.set(0, 2, 5);
            camera.lookAt(0, 1, 0);
            
            // Create renderer
            renderer = new THREE.WebGLRenderer({ canvas: canvas, alpha: true });
            renderer.setSize(width, height);
            renderer.setClearColor(0x000000, 0); // Transparent
            
            // Add lights
            // Ambient light
            const ambientLight = new THREE.AmbientLight(0x404060);
            scene.add(ambientLight);
            
            // Main directional light
            const mainLight = new THREE.DirectionalLight(0xffffff, 1);
            mainLight.position.set(5, 10, 7);
            mainLight.castShadow = true;
            scene.add(mainLight);
            
            // Fill light from below
            const fillLight = new THREE.PointLight(0xffaaff, 0.5);
            fillLight.position.set(0, -1, 0);
            scene.add(fillLight);
            
            // Back rim light
            const rimLight = new THREE.PointLight(0xff88cc, 0.6);
            rimLight.position.set(-2, 3, -3);
            scene.add(rimLight);
            
            // Warm front light
            const warmLight = new THREE.PointLight(0xffccaa, 0.4);
            warmLight.position.set(2, 2, 3);
            scene.add(warmLight);
            
            // Create cake group
            cakeGroup = new THREE.Group();
            
            // Bottom tier (largest) - Pink
            const bottomGeometry = new THREE.CylinderGeometry(1.4, 1.4, 0.6, 32);
            const bottomMaterial = new THREE.MeshStandardMaterial({ color: 0xff85a1, roughness: 0.3, metalness: 0.1 });
            const bottomTier = new THREE.Mesh(bottomGeometry, bottomMaterial);
            bottomTier.position.y = 0.3;
            bottomTier.castShadow = true;
            bottomTier.receiveShadow = true;
            cakeGroup.add(bottomTier);
            
            // Bottom frosting (ruffled edge)
            const frostingBottomGeo = new THREE.TorusGeometry(1.45, 0.08, 32, 100);
            const frostingMaterial = new THREE.MeshStandardMaterial({ color: 0xffc0d0, roughness: 0.2 });
            for (let i = 0; i < 3; i++) {
                const frostingRing = new THREE.Mesh(frostingBottomGeo, frostingMaterial);
                frostingRing.rotation.x = Math.PI / 2;
                frostingRing.position.y = 0.6 + (i * 0.05);
                frostingRing.position.z = 0;
                cakeGroup.add(frostingRing);
            }
            
            // Middle tier
            const middleGeometry = new THREE.CylinderGeometry(1.05, 1.1, 0.55, 32);
            const middleMaterial = new THREE.MeshStandardMaterial({ color: 0xffa5c2, roughness: 0.3, metalness: 0.1 });
            const middleTier = new THREE.Mesh(middleGeometry, middleMaterial);
            middleTier.position.y = 0.9;
            middleTier.castShadow = true;
            cakeGroup.add(middleTier);
            
            // Middle frosting
            const frostingMiddleGeo = new THREE.TorusGeometry(1.1, 0.07, 32, 100);
            for (let i = 0; i < 2; i++) {
                const frostingRing = new THREE.Mesh(frostingMiddleGeo, frostingMaterial);
                frostingRing.rotation.x = Math.PI / 2;
                frostingRing.position.y = 1.15 + (i * 0.04);
                cakeGroup.add(frostingRing);
            }
            
            // Top tier (smallest)
            const topGeometry = new THREE.CylinderGeometry(0.75, 0.8, 0.5, 32);
            const topMaterial = new THREE.MeshStandardMaterial({ color: 0xffb8d0, roughness: 0.3 });
            const topTier = new THREE.Mesh(topGeometry, topMaterial);
            topTier.position.y = 1.45;
            topTier.castShadow = true;
            cakeGroup.add(topTier);
            
            // Top frosting swirl
            const swirlGeo = new THREE.SphereGeometry(0.78, 32, 32);
            const swirlMaterial = new THREE.MeshStandardMaterial({ color: 0xffd0e0, roughness: 0.2 });
            const swirlTop = new THREE.Mesh(swirlGeo, swirlMaterial);
            swirlTop.position.y = 1.7;
            swirlTop.scale.set(1, 0.25, 1);
            cakeGroup.add(swirlTop);
            
            // Drip details on top tier
            const dripMaterial = new THREE.MeshStandardMaterial({ color: 0xffc0d5 });
            for (let i = 0; i < 12; i++) {
                const angle = (i / 12) * Math.PI * 2;
                const dripGeo = new THREE.SphereGeometry(0.09, 16, 16);
                const drip = new THREE.Mesh(dripGeo, dripMaterial);
                drip.position.x = Math.cos(angle) * 0.82;
                drip.position.z = Math.sin(angle) * 0.82;
                drip.position.y = 1.68;
                cakeGroup.add(drip);
            }
            
            // Create the number "19" using text geometry
            const loader = new THREE.FontLoader();
            // Use a simpler approach - make 3D spheres to form "19" since font loading is complex
            // Instead, let's create 19 small candles around the cake!
            
            // Candles on top
            const candleColor = 0xff69b4;
            const flameColor = 0xffaa44;
            
            // Center candle with "19" decoration
            const centerCandleGeo = new THREE.CylinderGeometry(0.12, 0.12, 0.4, 8);
            const candleMaterial = new THREE.MeshStandardMaterial({ color: candleColor, emissive: 0x441133 });
            const centerCandle = new THREE.Mesh(centerCandleGeo, candleMaterial);
            centerCandle.position.y = 1.95;
            centerCandle.castShadow = true;
            cakeGroup.add(centerCandle);
            
            // Flame
            const flameGeo = new THREE.ConeGeometry(0.08, 0.18, 8);
            const flameMaterial = new THREE.MeshStandardMaterial({ color: flameColor, emissive: 0xff6600 });
            const flame = new THREE.Mesh(flameGeo, flameMaterial);
            flame.position.y = 2.12;
            cakeGroup.add(flame);
            
            // Create "1" and "9" using small spheres on the cake face
            const numberMaterial = new THREE.MeshStandardMaterial({ color: 0xff69b4, emissive: 0xff3399 });
            
            // Number "1"
            const oneStick = new THREE.BoxGeometry(0.08, 0.25, 0.08);
            const oneVertical = new THREE.Mesh(oneStick, numberMaterial);
            oneVertical.position.set(-0.25, 1.72, 0.85);
            cakeGroup.add(oneVertical);
            
            // Number "9"
            const nineCircle = new THREE.TorusGeometry(0.12, 0.04, 16, 32);
            const nineRing = new THREE.Mesh(nineCircle, numberMaterial);
            nineRing.position.set(0.25, 1.78, 0.85);
            nineRing.rotation.x = Math.PI / 2;
            nineRing.rotation.z = Math.PI / 2;
            cakeGroup.add(nineRing);
            
            const nineStick = new THREE.BoxGeometry(0.07, 0.22, 0.07);
            const nineVertical = new THREE.Mesh(nineStick, numberMaterial);
            nineVertical.position.set(0.3, 1.72, 0.85);
            cakeGroup.add(nineVertical);
            
            // Add small decorative hearts around the cake
            const heartMaterial = new THREE.MeshStandardMaterial({ color: 0xff3399 });
            for (let i = 0; i < 16; i++) {
                const angle = (i / 16) * Math.PI * 2;
                const heartGeo = new THREE.SphereGeometry(0.06, 8, 8);
                const heart = new THREE.Mesh(heartGeo, heartMaterial);
                heart.position.x = Math.cos(angle) * 1.6;
                heart.position.z = Math.sin(angle) * 1.6;
                heart.position.y = 0.35;
                cakeGroup.add(heart);
            }
            
            // Add sprinkles
            const sprinkleColors = [0xff69b4, 0xff85a1, 0xffa5c2, 0xffc0d5, 0xffdbe8];
            for (let i = 0; i < 200; i++) {
                const sprinkleGeo = new THREE.BoxGeometry(0.03, 0.03, 0.08);
                const sprinkleMat = new THREE.MeshStandardMaterial({ color: sprinkleColors[Math.floor(Math.random() * sprinkleColors.length)] });
                const sprinkle = new THREE.Mesh(sprinkleGeo, sprinkleMat);
                
                // Random position on cake surface
                const tier = Math.random();
                let yBase, radius;
                if (tier < 0.33) {
                    yBase = 0.3 + Math.random() * 0.5;
                    radius = 1.2;
                } else if (tier < 0.66) {
                    yBase = 0.9 + Math.random() * 0.5;
                    radius = 0.9;
                } else {
                    yBase = 1.45 + Math.random() * 0.3;
                    radius = 0.65;
                }
                
                const angle = Math.random() * Math.PI * 2;
                sprinkle.position.x = Math.cos(angle) * radius * (0.7 + Math.random() * 0.3);
                sprinkle.position.z = Math.sin(angle) * radius * (0.7 + Math.random() * 0.3);
                sprinkle.position.y = yBase;
                sprinkle.rotation.z = Math.random() * Math.PI;
                cakeGroup.add(sprinkle);
            }
            
            scene.add(cakeGroup);
            
            // Add floating particles around cake
            const particleCount = 100;
            const particles = [];
            for (let i = 0; i < particleCount; i++) {
                const particleGeo = new THREE.SphereGeometry(0.02, 6, 6);
                const particleMat = new THREE.MeshStandardMaterial({ color: 0xff88cc });
                const particle = new THREE.Mesh(particleGeo, particleMat);
                particle.userData = {
                    speed: 0.005 + Math.random() * 0.01,
                    angle: Math.random() * Math.PI * 2,
                    radius: 1.5 + Math.random() * 1.5,
                    yOffset: Math.random() * Math.PI * 2
                };
                scene.add(particle);
                particles.push(particle);
            }
            
            // Animation loop
            let time = 0;
            function animate() {
                requestAnimationFrame(animate);
                time += 0.02;
                
                // Gentle floating rotation of cake
                if (cakeGroup) {
                    cakeGroup.rotation.y = Math.sin(time * 0.2) * 0.1;
                }
                
                // Animate particles
                particles.forEach((particle, idx) => {
                    const data = particle.userData;
                    const x = Math.cos(time * data.speed * 2 + data.angle) * data.radius;
                    const z = Math.sin(time * data.speed * 2 + data.angle) * data.radius;
                    const y = 1 + Math.sin(time * 2 + data.yOffset) * 0.5;
                    particle.position.set(x, y, z);
                });
                
                // Animate flame (flicker)
                if (flame) {
                    flame.scale.setScalar(0.8 + Math.sin(time * 30) * 0.15);
                }
                
                renderer.render(scene, camera);
            }
            
            animate();
            
            // Handle window resize
            window.addEventListener('resize', () => {
                const newWidth = canvas.clientWidth;
                const newHeight = canvas.clientHeight;
                camera.aspect = newWidth / newHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(newWidth, newHeight);
            });
            
            // Make cake clickable
            canvas.style.cursor = 'pointer';
            canvas.onclick = () => {
                celebrate();
            };
        }
        
        function createSparkles() {
            for (let i = 0; i < 60; i++) {
                const sparkle = document.createElement('div');
                sparkle.innerHTML = ['✨', '⭐', '💫', '🌟', '💜', '🌸', '🎀'][Math.floor(Math.random() * 7)];
                sparkle.style.position = 'fixed';
                sparkle.style.left = Math.random() * window.innerWidth + 'px';
                sparkle.style.top = Math.random() * window.innerHeight + 'px';
                sparkle.style.fontSize = (Math.random() * 20 + 15) + 'px';
                sparkle.style.pointerEvents = 'none';
                sparkle.style.zIndex = '9999';
                sparkle.style.opacity = '1';
                sparkle.style.animation = 'fadeOut 1s ease-out forwards';
                document.body.appendChild(sparkle);
                
                setTimeout(() => {
                    sparkle.remove();
                }, 1000);
            }
        }
        
        function celebrate() {
            for (let i = 0; i < 150; i++) {
                createConfetti();
            }
        }
        
        function createConfetti() {
            const confetti = document.createElement('div');
            const colors = ['#FF69B4', '#FF85A1', '#FFA5C2', '#FFC0D5', '#9B59B6', '#E879F9', '#FFB6C1'];
            const shapes = ['🎊', '🎉', '✨', '💜', '🌸', '🎀', '⭐', '💗'];
            
            confetti.innerHTML = shapes[Math.floor(Math.random() * shapes.length)];
            confetti.style.position = 'fixed';
            confetti.style.left = Math.random() * window.innerWidth + 'px';
            confetti.style.top = '-20px';
            confetti.style.fontSize = (Math.random() * 20 + 15) + 'px';
            confetti.style.pointerEvents = 'none';
            confetti.style.zIndex = '9999';
            confetti.style.opacity = '1';
            confetti.style.color = colors[Math.floor(Math.random() * colors.length)];
            document.body.appendChild(confetti);
            
            let pos = -20;
            const animation = setInterval(() => {
                pos += 5;
                confetti.style.top = pos + 'px';
                confetti.style.transform = `rotate(${pos}deg)`;
                
                if (pos > window.innerHeight) {
                    clearInterval(animation);
                    confetti.remove();
                }
            }, 30);
            
            setTimeout(() => {
                clearInterval(animation);
                confetti.remove();
            }, 3000);
        }
        
        // Add fadeOut animation
        const style = document.createElement('style');
        style.textContent = `
            @keyframes fadeOut {
                0% {
                    opacity: 1;
                    transform: scale(1);
                }
                100% {
                    opacity: 0;
                    transform: scale(0);
                }
            }
        `;
        document.head.appendChild(style);
    </script>
</body>
</html>
