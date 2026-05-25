<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>I have a question... 👉👈</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Fredoka+One&family=Quicksand:wght=600&display=swap');

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background-color: #ffeef2;
            font-family: 'Quicksand', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
            text-align: center;
        }

        .card {
            background: white;
            padding: 2.5rem;
            border-radius: 30px;
            box-shadow: 0 10px 30px rgba(255, 182, 193, 0.4);
            max-width: 450px;
            width: 90%;
            min-height: 400px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            position: relative;
            transition: all 0.5s ease-in-out;
        }

        .step {
            display: none;
            flex-direction: column;
            align-items: center;
            animation: popIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .step.active {
            display: flex;
        }

        @keyframes popIn {
            0% { transform: scale(0.7); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        h1 {
            font-family: 'Fredoka One', cursive;
            color: #ff6584;
            font-size: 2rem;
            margin-bottom: 1.5rem;
            line-height: 1.3;
        }

        p {
            color: #666;
            font-size: 1.1rem;
            margin-bottom: 1.5rem;
        }

        .gif-container {
            font-size: 4rem;
            margin-bottom: 1.5rem;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        .btn-container {
            display: flex;
            gap: 15px;
            justify-content: center;
            align-items: center;
            width: 100%;
            margin-top: 1rem;
        }

        button {
            padding: 12px 28px;
            border: none;
            border-radius: 50px;
            font-family: 'Fredoka One', cursive;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
        }

        .btn-yes {
            background-color: #ff6584;
            color: white;
        }

        .btn-yes:hover {
            background-color: #ff476c;
            transform: scale(1.05);
        }

        .btn-no {
            background-color: #ececec;
            color: #777;
            /* Added smooth, slower glide transition */
            transition: left 0.4s cubic-bezier(0.25, 1, 0.5, 1), top 0.4s cubic-bezier(0.25, 1, 0.5, 1), background-color 0.2s;
        }

        input[type="date"], input[type="time"] {
            padding: 12px;
            border: 2px solid #ffb6c1;
            border-radius: 15px;
            font-family: 'Quicksand', sans-serif;
            font-size: 1rem;
            margin-bottom: 1rem;
            width: 80%;
            color: #555;
            outline: none;
        }

        input[type="date"]:focus, input[type="time"]:focus {
            border-color: #ff6584;
        }

        .hearts {
            position: absolute;
            font-size: 1.5rem;
            opacity: 0;
            animation: floatUp 2s linear forwards;
            pointer-events: none;
        }

        @keyframes floatUp {
            0% { transform: translateY(0) scale(0); opacity: 1; }
            100% { transform: translateY(-150px) scale(1.2); opacity: 0; }
        }
    </style>
</head>
<body>

    <div class="card" id="card">
        
        <div class="step active" id="step1">
            <div class="gif-container">🥺👉👈</div>
            <h1>Hey! I was wondering... will you go on a date with me?</h1>
            <div class="btn-container">
                <button class="btn-yes" id="yesBtn1" onclick="nextStep(2)">Yes!</button>
                <button class="btn-no" id="noBtn">No</button>
            </div>
        </div>

        <div class="step" id="step2">
            <div class="gif-container">🥳✨</div>
            <h1>Oh, really?!</h1>
            <p>You actually said yes! You're not pulling my leg, right? 🥰</p>
            <div class="btn-container">
                <button class="btn-yes" onclick="nextStep(3)">Heck yeah, let's do it!</button>
            </div>
        </div>

        <div class="step" id="step3">
            <div class="gif-container">📅✏️</div>
            <h1>Let's make it official!</h1>
            <p>When are you free to hang out?</p>
            <input type="date" id="datePicker" required>
            <input type="time" id="timePicker" required>
            <div class="btn-container">
                <button class="btn-yes" onclick="submitDate()">Lock it in! 💕</button>
            </div>
        </div>

        <div class="step" id="step4">
            <div class="gif-container">💖😭</div>
            <h1>Yay! It's a date!</h1>
            <p id="finalMessage">Thank you! I'm already looking forward to it. See you then! ✨</p>
        </div>

    </div>

    <script>
        function nextStep(stepNumber) {
            document.querySelectorAll('.step').forEach(step => {
                step.classList.remove('active');
            });
            document.getElementById(`step${stepNumber}`).classList.add('active');
            
            if (stepNumber === 2 || stepNumber === 4) {
                createHearts();
            }
        }

        const noBtn = document.getElementById('noBtn');
        let escapeCount = 0; // Tracks how many times it teleported

        noBtn.addEventListener('mouseenter', () => {
            if (escapeCount < 10) {
                noBtn.style.position = 'absolute';
                
                const padding = 60;
                const randomX = Math.random() * (window.innerWidth - noBtn.offsetWidth - padding * 2) + padding;
                const randomY = Math.random() * (window.innerHeight - noBtn.offsetHeight - padding * 2) + padding;
                
                noBtn.style.left = `${randomX}px`;
                noBtn.style.top = `${randomY}px`;
                
                escapeCount++;
                
                // Extra detail: Change button text dynamically as they keep trying
                if (escapeCount === 3) noBtn.innerText = "Wait, seriously? 😂";
                if (escapeCount === 6) noBtn.innerText = "Can't catch me! 🏃‍♂️";
                if (escapeCount === 9) noBtn.innerText = "Last try! 😜";
            } else {
                // After 10 times, the button surrenders and becomes a secret second 'Yes' button!
                noBtn.style.position = 'static'; 
                noBtn.innerText = "Fine, you win... no.. :<";
                noBtn.style.backgroundColor = "#ff6584";
                noBtn.style.color = "white";
                
                // Re-route clicking this worn-out button to progress the page
                noBtn.onclick = () => nextStep(2);
            }
        });

        function submitDate() {
            const dateVal = document.getElementById('datePicker').value;
            const timeVal = document.getElementById('timePicker').value;

            if (!dateVal) {
                alert("Please pick a day! 🥺");
                return;
            }

            const options = { weekday: 'long', month: 'short', day: 'numeric' };
            const formattedDate = new Date(dateVal + 'T00:00:00').toLocaleDateString('en-US', options);
            const timeDisplay = timeVal ? ` at ${timeVal}` : '';

            document.getElementById('finalMessage').innerHTML = 
                `Thank you!! I can't wait for <strong>${formattedDate}${timeDisplay}</strong>. <br>You just made my entire week! 🥰✨`;

            nextStep(4);
        }

        function createHearts() {
            const card = document.getElementById('card');
            const heartEmojis = ['💖', '💝', '✨', '💕', '🥰'];
            
            for (let i = 0; i < 15; i++) {
                const heart = document.createElement('div');
                heart.classList.add('hearts');
                heart.innerText = heartEmojis[Math.floor(Math.random() * heartEmojis.length)];
                
                heart.style.left = Math.random() * 80 + 10 + '%';
                heart.style.bottom = '20%';
                heart.style.animationDelay = Math.random() * 0.5 + 's';
                
                card.appendChild(heart);
                
                setTimeout(() => {
                    heart.remove();
                }, 2000);
            }
        }
    </script>
</body>
</html>
