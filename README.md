<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday!</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background-color: #8B5CF6; /* Violet color */
            background: linear-gradient(135deg, #8B5CF6 0%, #7C3AED 50%, #6D28D9 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Arial', 'Segoe UI', 'Poppins', sans-serif;
            padding: 20px;
        }

        .birthday-card {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 30px;
            padding: 50px 40px;
            max-width: 600px;
            width: 100%;
            text-align: center;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            animation: fadeIn 1s ease-in;
        }

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

        h1 {
            font-size: 48px;
            color: #6D28D9;
            margin-bottom: 20px;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-10px);
            }
        }

        .cake {
            font-size: 80px;
            margin: 20px 0;
            animation: wiggle 3s infinite;
        }

        @keyframes wiggle {
            0%, 100% {
                transform: rotate(0deg);
            }
            25% {
                transform: rotate(5deg);
            }
            75% {
                transform: rotate(-5deg);
            }
        }

        .message {
            font-size: 20px;
            color: #333;
            line-height: 1.6;
            margin: 20px 0;
        }

        .birthday-person {
            font-size: 32px;
            font-weight: bold;
            color: #8B5CF6;
            margin: 20px 0;
            background: linear-gradient(135deg, #8B5CF6, #6D28D9);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .balloons {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 30px 0;
            flex-wrap: wrap;
        }

        .balloon {
            font-size: 50px;
            animation: float 3s ease-in-out infinite;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .balloon:hover {
            transform: scale(1.2);
        }

        .balloon:nth-child(1) { animation-delay: 0s; }
        .balloon:nth-child(2) { animation-delay: 0.5s; }
        .balloon:nth-child(3) { animation-delay: 1s; }
        .balloon:nth-child(4) { animation-delay: 1.5s; }
        .balloon:nth-child(5) { animation-delay: 2s; }

        @keyframes float {
            0%, 100% {
                transform: translateY(0px);
            }
            50% {
                transform: translateY(-20px);
            }
        }

        button {
            background: linear-gradient(135deg, #8B5CF6, #6D28D9);
            color: white;
            border: none;
            padding: 12px 30px;
            font-size: 18px;
            border-radius: 50px;
            cursor: pointer;
            margin-top: 20px;
            transition: transform 0.3s, box-shadow 0.3s;
        }

        button:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 20px rgba(107, 70, 193, 0.4);
        }

        .sparkle {
            position: absolute;
            pointer-events: none;
            font-size: 20px;
            animation: sparkleAnim 1s ease-out forwards;
        }

        @keyframes sparkleAnim {
            0% {
                opacity: 1;
                transform: scale(1);
            }
            100% {
                opacity: 0;
                transform: scale(0);
            }
        }

        @media (max-width: 600px) {
            .birthday-card {
                padding: 30px 20px;
            }
            
            h1 {
                font-size: 36px;
            }
            
            .message {
                font-size: 16px;
            }
            
            .birthday-person {
                font-size: 24px;
            }
        }
    </style>
</head>
<body>
    <div class="birthday-card">
        <div class="cake">🎂🎉</div>
        
        <h1>HAPPY BIRTHDAY! 🎈</h1>
        
        <div class="birthday-person" id="nameDisplay">
            Dear Friend!
        </div>
        
        <div class="message">
            Wishing you a day filled with joy,<br>
            laughter, and wonderful surprises!<br>
            May this year bring you everything you've been dreaming of. ✨
        </div>
        
        <div class="balloons">
            <div class="balloon" onclick="popBalloon(this)">🎈</div>
            <div class="balloon" onclick="popBalloon(this)">🎈</div>
            <div class="balloon" onclick="popBalloon(this)">🎈</div>
            <div class="balloon" onclick="popBalloon(this)">🎈</div>
            <div class="balloon" onclick="popBalloon(this)">🎈</div>
        </div>
        
        <button onclick="playConfetti()">🎁 Send Wishes 🎁</button>
        
        <div class="message" style="font-size: 14px; margin-top: 20px;">
            🎂 Enjoy your special day! 🎂
        </div>
    </div>

    <script>
        // You can change the name here
        const birthdayPerson = "Jasmin";
        document.getElementById('nameDisplay').innerHTML = birthdayPerson;
        
        // Balloon pop effect
        function popBalloon(balloon) {
            if (balloon.style.opacity !== "0") {
                balloon.style.opacity = "0";
                balloon.style.transform = "scale(0)";
                createSparkle(balloon);
                setTimeout(() => {
                    balloon.innerHTML = "💥";
                    balloon.style.opacity = "1";
                    balloon.style.transform = "scale(1)";
                    setTimeout(() => {
                        balloon.innerHTML = "🎈";
                    }, 500);
                }, 200);
            }
        }
        
        // Create sparkle effect
        function createSparkle(element) {
            for (let i = 0; i < 10; i++) {
                const sparkle = document.createElement('div');
                sparkle.className = 'sparkle';
                sparkle.innerHTML = ['✨', '⭐', '💫', '🌟'][Math.floor(Math.random() * 4)];
                const rect = element.getBoundingClientRect();
                sparkle.style.left = rect.left + (Math.random() * 30) + 'px';
                sparkle.style.top = rect.top + (Math.random() * 30) + 'px';
                sparkle.style.position = 'fixed';
                document.body.appendChild(sparkle);
                
                setTimeout(() => {
                    sparkle.remove();
                }, 1000);
            }
        }
        
        // Confetti effect when clicking button
        function playConfetti() {
            // Create confetti particles
            for (let i = 0; i < 100; i++) {
                createConfetti();
            }
            alert("🎉 Happy Birthday! Wishing you all the best! 🎉");
        }
        
        function createConfetti() {
            const confetti = document.createElement('div');
            confetti.innerHTML = ['🎊', '🎉', '✨', '⭐', '💝', '🎂', '🎈'][Math.floor(Math.random() * 7)];
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
        
        // Add more sparkles on page load
        window.addEventListener('load', () => {
            console.log('Happy Birthday! 🎂');
        });
    </script>
</body>
</html>
