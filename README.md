<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Arcade Whack-A-Mole</title>
    <style>
        body { margin: 0; background: #111827; color: white; font-family: system-ui, sans-serif; display: flex; flex-direction: column; align-items: center; justify-content: center; min-height: 100vh; overflow: hidden; }
        h1 { margin: 10px 0; color: #fbbf24; text-shadow: 0 4px 10px rgba(251,191,36,0.3); }
        .score-board { font-size: 24px; font-weight: bold; margin-bottom: 20px; background: #1f2937; padding: 10px 30px; border-radius: 50px; border: 2px solid #374151; }
        .grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; max-width: 400px; width: 90%; }
        .hole { background: #374151; border: 4px solid #4b5563; border-radius: 50px; height: 110px; position: relative; overflow: hidden; box-shadow: inset 0 10px 20px rgba(0,0,0,0.6); }
        .mole { width: 80px; height: 80px; background: #92400e; border-radius: 50% 50% 0 0; position: absolute; left: 50%; transform: translateX(-50%); bottom: -90px; transition: bottom 0.1s ease; cursor: pointer; border: 3px solid #78350f; }
        .mole::before { content: '👀'; position: absolute; top: 15px; left: 18px; font-size: 24px; }
        .hole.active .mole { bottom: 0; }
        button { background: #10b981; color: white; border: none; padding: 12px 30px; font-size: 18px; font-weight: bold; border-radius: 8px; cursor: pointer; margin-top: 25px; transition: transform 0.1s; }
        button:hover { background: #059669; transform: scale(1.05); }
    </style>
</head>
<body>

    <h1>🔨 WHACK-A-MOLE!</h1>
    <div class="score-board">Score: <span id="score">0</span></div>
    
    <div class="grid">
        <div class="hole"><div class="mole"></div></div>
        <div class="hole"><div class="mole"></div></div>
        <div class="hole"><div class="mole"></div></div>
        <div class="hole"><div class="mole"></div></div>
        <div class="hole"><div class="mole"></div></div>
        <div class="hole"><div class="mole"></div></div>
        <div class="hole"><div class="mole"></div></div>
        <div class="hole"><div class="mole"></div></div>
        <div class="hole"><div class="mole"></div></div>
    </div>

    <button id="start-btn" onclick="startGame()">Start Game</button>

    <script>
        const holes = document.querySelectorAll('.hole');
        const scoreDisplay = document.getElementById('score');
        const startBtn = document.getElementById('start-btn');
        let lastHole;
        let score = 0;
        let timeUp = false;

        function randomHole(holes) {
            const idx = Math.floor(Math.random() * holes.length);
            const hole = holes[idx];
            if (hole === lastHole) return randomHole(holes);
            lastHole = hole;
            return hole;
        }

        function peep() {
            const time = Math.random() * (1000 - 400) + 400; // random speed
            const hole = randomHole(holes);
            hole.classList.add('active');
            setTimeout(() => {
                hole.classList.remove('active');
                if (!timeUp) peep();
            }, time);
        }

        function startGame() {
            score = 0;
            scoreDisplay.textContent = 0;
            timeUp = false;
            startBtn.disabled = true;
            startBtn.textContent = "Whack away!";
            peep();
            setTimeout(() => {
                timeUp = true;
                startBtn.disabled = false;
                startBtn.textContent = "Play Again";
                alert('💥 Game Over! Your final score is: ' + score);
            }, 15000); // 15-second rounds
        }

        document.querySelectorAll('.mole').forEach(mole => {
            mole.addEventListener('click', () => {
                score++;
                scoreDisplay.textContent = score;
                mole.parentNode.classList.remove('active');
            });
        });
    </script>
</body>
</html>
