# click-speed-test
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Click Speed Test</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: #1e1e2f;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }
    h1 {
      font-size: 2.5rem;
      margin-bottom: 0.5rem;
    }
    #timer {
      font-size: 1.2rem;
      margin-bottom: 1rem;
    }
    #click-area {
      width: 200px;
      height: 200px;
      background: #ff4081;
      border: none;
      border-radius: 50%;
      font-size: 1.2rem;
      color: white;
      cursor: pointer;
      transition: background 0.2s;
    }
    #click-area:active {
      background: #e91e63;
    }
    #result {
      margin-top: 1.5rem;
      font-size: 1.5rem;
    }
    .hidden {
      display: none;
    }
    footer {
      position: absolute;
      bottom: 10px;
      font-size: 0.8rem;
      color: #aaa;
    }
  </style>
</head>
<body>
  <h1>Click Speed Test</h1>
  <div id="timer">Click as fast as you can in <strong>5 seconds</strong>!</div>
  <button id="click-area">Start</button>
  <div id="result" class="hidden"></div>
  <footer>Made with ❤️ | Add your ad here</footer>

  <script>
    let isRunning = false;
    let clicks = 0;
    let timeLeft = 5;
    let timer;

    const clickArea = document.getElementById('click-area');
    const result = document.getElementById('result');
    const timerDisplay = document.getElementById('timer');

    clickArea.addEventListener('click', () => {
      if (!isRunning) {
        startGame();
      } else {
        clicks++;
      }
    });

    function startGame() {
      isRunning = true;
      clicks = 0;
      timeLeft = 5;
      result.classList.add('hidden');
      clickArea.textContent = 'Click!';
      timerDisplay.textContent = `Time left: ${timeLeft}s`;

      timer = setInterval(() => {
        timeLeft--;
        timerDisplay.textContent = `Time left: ${timeLeft}s`;

        if (timeLeft === 0) {
          endGame();
        }
      }, 1000);
    }

    function endGame() {
      clearInterval(timer);
      isRunning = false;
      const cps = (clicks / 5).toFixed(2);
      result.textContent = `You clicked ${clicks} times. CPS: ${cps}`;
      result.classList.remove('hidden');
      clickArea.textContent = 'Start Again';
      timerDisplay.textContent = 'Click as fast as you can in 5 seconds!';
    }
  </script>
</body>
</html>
