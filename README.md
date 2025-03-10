<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Holi, Shakshi!</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Festive&family=Pacifico&display=swap');
        body {
            background-color: #ffb6c1;
            text-align: center;
            font-family: 'Pacifico', cursive;
            overflow: hidden;
        }
        .popup {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 15px rgba(0,0,0,0.3);
            display: none;
            font-size: 24px;
            z-index: 10;
            animation: splash 1s infinite alternate, colorSpread 1.5s ease-in-out;
            font-family: 'Festive', cursive;
        }
        @keyframes splash {
            0% { color: red; }
            25% { color: blue; }
            50% { color: green; }
            75% { color: purple; }
            100% { color: orange; }
        }
        @keyframes colorSpread {
            0% { box-shadow: 0 0 10px rgba(255,0,0,0.5); }
            50% { box-shadow: 0 0 20px rgba(0,255,0,0.5); }
            100% { box-shadow: 0 0 30px rgba(0,0,255,0.5); }
        }
        .button {
            background-color: #ff5722;
            color: white;
            border: none;
            padding: 10px 20px;
            font-size: 18px;
            cursor: pointer;
            border-radius: 5px;
            margin-top: 10px;
        }
        .color-splash {
            position: absolute;
            width: 100px;
            height: 100px;
            background: radial-gradient(circle, rgba(255, 0, 0, 0.8), rgba(255, 255, 0, 0));
            border-radius: 50%;
            opacity: 0.7;
            animation: spread 1s ease-out;
        }
        @keyframes spread {
            0% { transform: scale(0); opacity: 1; }
            100% { transform: scale(5); opacity: 0; }
        }
    </style>
</head>
<body>

    <h1>Click Below to Start the Celebration 🎉</h1>
    <button class="button" onclick="startCelebration()">Start Holi</button>

    <!-- Popups -->
    <div id="popup1" class="popup">
        <h2>Happy Holi, Shakshi! 🎨</h2>
    </div>
    <div id="popup2" class="popup">
        <h2>To move forward, click Enjoy!</h2>
        <button class="button" onclick="showPopup3()">Enjoy</button>
    </div>
    <div id="popup3" class="popup">
        <h2>बिना तुम्हें रंग लगाए या फागुन लौट ना जाए!</h2>
    </div>

    <script>
        function createColorSplash() {
            const splash = document.createElement("div");
            splash.classList.add("color-splash");
            splash.style.top = Math.random() * window.innerHeight + "px";
            splash.style.left = Math.random() * window.innerWidth + "px";
            document.body.appendChild(splash);
            setTimeout(() => splash.remove(), 1000);
        }

        function startCelebration() {
            document.querySelector('.button').style.display = 'none'; // Hide start button
            showPopup1();
        }

        function showPopup1() {
            document.getElementById("popup1").style.display = "block";
            playGuitarSong(); // 🎸 Play guitar music
            for (let i = 0; i < 15; i++) setTimeout(createColorSplash, i * 200);
            setTimeout(() => {
                document.getElementById("popup1").style.display = "none";
                document.getElementById("popup2").style.display = "block";
            }, 3000);
        }

        function showPopup3() {
            document.getElementById("popup2").style.display = "none";
            document.getElementById("popup3").style.display = "block";
            playGuitarSong(); // 🎸 Play guitar again
            for (let i = 0; i < 15; i++) setTimeout(createColorSplash, i * 200);
        }

        function playGuitarTone(frequency, duration, startTime) {
            const audioContext = new (window.AudioContext || window.webkitAudioContext)();
            const oscillator = audioContext.createOscillator();
            const gainNode = audioContext.createGain();

            oscillator.frequency.value = frequency;
            oscillator.type = "triangle";  // Triangle wave for a soft guitar pluck

            oscillator.connect(gainNode);
            gainNode.connect(audioContext.destination);

            // Soft pluck effect (attack and decay)
            gainNode.gain.setValueAtTime(0, audioContext.currentTime + startTime);
            gainNode.gain.linearRampToValueAtTime(0.8, audioContext.currentTime + startTime + 0.05);
            gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + startTime + duration);

            oscillator.start(audioContext.currentTime + startTime);
            oscillator.stop(audioContext.currentTime + startTime + duration);
        }

        function playGuitarSong() {
            let melody = [
                { note: 220, duration: 0.5 },  // A (Low)
                { note: 247, duration: 0.5 },  // B
                { note: 294, duration: 0.5 },  // D
                { note: 330, duration: 0.5 },  // E
                { note: 392, duration: 0.7 },  // G
                { note: 349, duration: 0.7 },  // F
                { note: 330, duration: 0.7 },  // E
                { note: 294, duration: 1.0 },  // D (hold)
            ];

            let startTime = 0;
            melody.forEach((tone) => {
                playGuitarTone(tone.note, tone.duration, startTime);
                startTime += tone.duration;
            });
        }
    </script>

</body>
</html>
