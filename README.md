<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cupid's Love Hunt</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #ffe6e6;
            text-align: center;
            margin: 0;
            overflow: hidden;
        }
        h1 {
            color: #cc3366;
        }
        .game-container {
            position: relative;
            width: 100vw;
            height: 80vh;
            overflow: hidden;
            background: url('https://i.imgur.com/9m3Z3wY.jpg') no-repeat center center;
            background-size: cover;
        }
        .heart {
            position: absolute;
            width: 50px;
            height: 50px;
            font-size: 30px;
            cursor: pointer;
            animation: float 3s linear infinite;
        }
        @keyframes float {
            0% { transform: translateY(0); }
            100% { transform: translateY(-100vh); }
        }
        .score {
            font-size: 24px;
            color: #cc3366;
            margin-top: 10px;
        }
        .start-button {
            padding: 10px 20px;
            font-size: 20px;
            color: white;
            background-color: #ff6699;
            border: none;
            cursor: pointer;
            margin-top: 20px;
            border-radius: 5px;
        }
        .game-over {
            display: none;
            font-size: 30px;
            color: #cc3366;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Cupid's Love Hunt 💘</h1>
    <p class="score">Score: <span id="score">0</span></p>
    <button class="start-button" onclick="startGame()">Start Game</button>
    <div class="game-container" id="gameContainer"></div>
    <p class="game-over" id="gameOver">Game Over! Your final score: <span id="finalScore"></span></p>

    <script>
        let score = 0;
        let gameInterval;
        let gameTime = 30; // Game duration in seconds

        function startGame() {
            score = 0;
            document.getElementById("score").innerText = score;
            document.getElementById("gameOver").style.display = "none";
            document.querySelector(".start-button").style.display = "none";
            gameInterval = setInterval(spawnHeart, 800); // Create hearts every 0.8 seconds

            setTimeout(() => {
                endGame();
            }, gameTime * 1000);
        }

        function spawnHeart() {
            const heart = document.createElement("div");
            heart.classList.add("heart");
            heart.innerHTML = "❤️";
            const gameContainer = document.getElementById("gameContainer");
            
            let x = Math.random() * (window.innerWidth - 50);
            let y = Math.random() * (window.innerHeight - 100);
            
            heart.style.left = `${x}px`;
            heart.style.top = `${y}px`;
            
            heart.addEventListener("click", () => {
                score += 10;
                document.getElementById("score").innerText = score;
                heart.remove();
            });

            gameContainer.appendChild(heart);

            setTimeout(() => {
                heart.remove();
            }, 2000); // Hearts disappear after 2 seconds
        }

        function endGame() {
            clearInterval(gameInterval);
            document.querySelectorAll(".heart").forEach(heart => heart.remove());
            document.getElementById("gameOver").style.display = "block";
            document.getElementById("finalScore").innerText = score;
            document.querySelector(".start-button").style.display = "block";
        }
    </script>
</body>
</html>
