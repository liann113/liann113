<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Why So Serious, kookie?</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Faster+One&display=swap');

    body {
      margin: 0;
      height: 100vh;
      background: radial-gradient(circle at center, #000000 0%, #1e1e1e 100%);
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      font-family: 'Faster One', cursive;
      color: #39ff14;
    }

    h1 {
      font-size: 4em;
      text-shadow: 2px 2px #8b008b;
      animation: glitch 1s infinite;
    }

    p {
      font-size: 1.5em;
      color: #fff;
      margin-top: 20px;
      text-shadow: 1px 1px #ff00ff;
    }

    button {
      margin-top: 30px;
      padding: 15px 30px;
      background-color: #8b008b;
      color: #fff;
      border: none;
      border-radius: 10px;
      font-size: 1.2em;
      cursor: pointer;
      box-shadow: 0 0 10px #39ff14;
      transition: 0.3s;
    }

    button:hover {
      background-color: #39ff14;
      color: #000;
    }

    @keyframes glitch {
      0% { transform: translate(0); }
      20% { transform: translate(-2px, 2px); }
      40% { transform: translate(2px, -2px); }
      60% { transform: translate(-2px, -2px); }
      80% { transform: translate(2px, 2px); }
      100% { transform: translate(0); }
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      pointer-events: none;
      z-index: 9999;
    }
  </style>
</head>
<body>

  <h1>It's Your Birthday... HAHA!</h1>
  <p>Why so serious, kookie? Time to celebrate!</p>

  <button onclick="playMusic()">🎵 Play the Sound</button>

  <audio id="bgMusic" loop>
    <source src="https://archive.org/download/the19775rc/The%201975%20-%20The%20Sound.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
  </audio>

  <canvas id="confetti"></canvas>

  <script>
    // Confetti
    const confetti = document.getElementById('confetti');
    const ctx = confetti.getContext('2d');
    confetti.width = window.innerWidth;
    confetti.height = window.innerHeight;

    let pieces = [];
    const colors = ['#39ff14', '#8b008b', '#ffffff', '#ff00ff'];

    for (let i = 0; i < 150; i++) {
      pieces.push({
        x: Math.random() * confetti.width,
        y: Math.random() * confetti.height - confetti.height,
        size: Math.random() * 6 + 2,
        speed: Math.random() * 3 + 2,
        color: colors[Math.floor(Math.random() * colors.length)],
        rotation: Math.random() * 360
      });
    }

    function update() {
      ctx.clearRect(0, 0, confetti.width, confetti.height);
      for (let piece of pieces) {
        ctx.fillStyle = piece.color;
        ctx.beginPath();
        ctx.arc(piece.x, piece.y, piece.size, 0, 2 * Math.PI);
        ctx.fill();
        piece.y += piece.speed;
        if (piece.y > confetti.height) {
          piece.y = -10;
          piece.x = Math.random() * confetti.width;
        }
      }
      requestAnimationFrame(update);
    }

    update();

    // Music play function
    function playMusic() {
      const audio = document.getElementById('bgMusic');
      audio.play();
    }
  </script>
</body>
</html>
