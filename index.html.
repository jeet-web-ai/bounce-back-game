<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bounce Back - The Game</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <div class="game-container">
        <h1>BOUNCE BACK</h1>
        <p>Fall down. Bounce back. Keep going!</p>

        <div class="game-info">
            <span>Score: <span id="score">0</span></span>
            <span>Level: <span id="level">1</span></span>
        </div>

        <canvas id="gameCanvas" width="400" height="550"></canvas>

        <p class="instructions">
            Use ← and → arrow keys to move.
        </p>

        <button id="startButton">Start Game</button>
    </div>

    <script src="script.js"></script>
</body>
</html>* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background: #e8f5ff;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
}

.game-container {
    text-align: center;
    background: white;
    padding: 25px;
    border-radius: 18px;
    box-shadow: 0 5px 20px #00000015;
}

h1 {
    color: #ff784f;
    margin-bottom: 8px;
}

.game-container > p {
    color: #666;
    margin-bottom: 15px;
}

.game-info {
    display: flex;
    justify-content: space-around;
    margin: 12px 0;
    font-weight: bold;
}

canvas {
    display: block;
    width: 100%;
    max-width: 400px;
    background: #c9edff;
    border: 3px solid #333;
    border-radius: 10px;
}

.instructions {
    margin-top: 15px;
}

button {
    background: #ff784f;
    color: white;
    border: none;
    padding: 12px 28px;
    border-radius: 8px;
    font-size: 16px;
    cursor: pointer;
    margin-top: 12px;
}

button:hover {
    background: #ed613b;
}const canvas = document.getElementById("gameCanvas");
const ctx = canvas.getContext("2d");

const scoreElement = document.getElementById("score");
const startButton = document.getElementById("startButton");

let score = 0;
let running = false;

const ball = {
    x: 200,
    y: 200,
    radius: 15,
    speedX: 3,
    speedY: 0,
    gravity: 0.35,
    bouncePower: -9
};

const ground = 490;

const keys = {
    left: false,
    right: false
};

function drawBall() {
    ctx.beginPath();
    ctx.arc(
        ball.x,
        ball.y,
        ball.radius,
        0,
        Math.PI * 2
    );

    ctx.fillStyle = "#ff784f";
    ctx.fill();

    ctx.strokeStyle = "#333";
    ctx.lineWidth = 2;
    ctx.stroke();
    ctx.closePath();
}

function drawGround() {
    ctx.fillStyle = "#69bd79";
    ctx.fillRect(0, ground, canvas.width, 60);
}

function update() {
    if (!running) return;

    // Gravity pulls the ball downward
    ball.speedY += ball.gravity;
    ball.y += ball.speedY;

    // Automatic bouncing
    if (ball.y + ball.radius >= ground) {
        ball.y = ground - ball.radius;
        ball.speedY = ball.bouncePower;
        score++;
        scoreElement.textContent = score;
    }

    // Left and right movement
    if (keys.left) ball.x -= 4;
    if (keys.right) ball.x += 4;

    // Keep ball inside the canvas
    ball.x = Math.max(
        ball.radius,
        Math.min(canvas.width - ball.radius, ball.x)
    );

    // Draw the game
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    drawGround();
    drawBall();

    requestAnimationFrame(update);
}

document.addEventListener("keydown", (event) => {
    if (event.key === "ArrowLeft") keys.left = true;
    if (event.key === "ArrowRight") keys.right = true;
});

document.addEventListener("keyup", (event) => {
    if (event.key === "ArrowLeft") keys.left = false;
    if (event.key === "ArrowRight") keys.right = false;
});

startButton.addEventListener("click", () => {
    if (running) return;

    running = true;
    startButton.textContent = "Playing...";
    update();
});
