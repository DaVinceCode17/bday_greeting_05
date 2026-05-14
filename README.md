<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday Mhin</title>
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
            transition: background-color 0.5s ease;
        }

        /* Screen 1 - Black background */
        body.screen1 {
            background-color: black;
        }

        /* Screen 2 - Violet background */
        body.screen2 {
            background-color: #8B5CF6;
        }

        .container {
            text-align: center;
            padding: 20px;
        }

        /* Screen 1 Styles */
        .welcome-text {
            font-size: 80px;
            font-weight: bold;
            color: white;
            margin-bottom: 40px;
            animation: fadeIn 1s ease-in;
        }

        .continue-btn {
            background-color: #8B5CF6;
            color: white;
            font-size: 24px;
            font-weight: bold;
            padding: 15px 50px;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            animation: fadeIn 1s ease-in 0.3s both;
        }

        .continue-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 30px rgba(139, 92, 246, 0.5);
        }

        /* Screen 2 Styles */
        .cake {
            font-size: 120px;
            margin-bottom: 30px;
            animation: bounce 2s infinite;
            cursor: pointer;
        }

        .birthday-text {
            font-size: 48px;
            font-weight: bold;
            color: white;
            text-shadow: 3px 3px 6px rgba(0, 0, 0, 0.3);
            animation: fadeInUp 0.8s ease;
        }

        /* Hide screen 2 initially */
        .screen2-content {
            display: none;
        }

        body.screen2 .screen1-content {
            display: none;
        }

        body.screen2 .screen2-content {
            display: block;
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

        @keyframes bounce {
            0%, 100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-15px);
            }
        }

        /* Confetti effect */
        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            background-color: #f0f;
            position: absolute;
            animation: fall 3s linear forwards;
            pointer-events: none;
        }

        @keyframes fall {
            to {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
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
            
            .cake {
                font-size: 80px;
            }
            
            .birthday-text {
                font-size: 32px;
            }
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
                Continue
            </button>
        </div>

        <!-- Screen 2: Cake + Happy Birthday Mhin -->
        <div class="screen2-content">
            <div class="cake" onclick="celebrate()">
                🎂
            </div>
            <div class="birthday-text">
                Happy Birthday Mhin! 🎉
            </div>
        </div>
    </div>

    <script>
        function goToBirthday() {
            // Change background to violet
            document.body.classList.remove('screen1');
            document.body.classList.add('screen2');
            
            // Play a little celebration effect
            createSparkles();
        }

        function createSparkles() {
            for (let i = 0; i < 50; i++) {
                const sparkle = document.createElement('div');
                sparkle.innerHTML = ['✨', '⭐', '💫', '🌟', '🎂', '🎉', '🎈'][Math.floor(Math.random() * 7)];
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
            // Create confetti when cake is clicked
            for (let i = 0; i < 100; i++) {
                createConfetti();
            }
        }

        function createConfetti() {
            const confetti = document.createElement('div');
            confetti.innerHTML = ['🎊', '🎉', '✨', '⭐', '💝', '🎂', '🎈', '🎁'][Math.floor(Math.random() * 8)];
            confetti.style.position = 'fixed';
            confetti.style.left = Math.random() * window.innerWidth + 'px';
            confetti.style.top = '-20px';
            confetti.style.fontSize = (Math.random() * 20 + 15) + 'px';
            confetti.style.pointerEvents = 'none';
            confetti.style.opacity = '1';
            confetti.style.zIndex = '9999';
            document.body.appendChild(confetti);
            
            let pos = -20;
            const animation = setInterval(() => {
                pos += 5;
                confetti.style.top = pos + 'px';
                
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

        // Add fadeOut animation style
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
