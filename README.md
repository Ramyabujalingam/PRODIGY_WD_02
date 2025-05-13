# PRODIGY_WD_02
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Stopwatch</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #1e1e2f;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }

    h1 {
      margin-bottom: 20px;
    }

    .stopwatch {
      font-size: 48px;
      margin-bottom: 20px;
    }

    .buttons button {
      padding: 10px 20px;
      font-size: 16px;
      margin: 5px;
      cursor: pointer;
      border: none;
      border-radius: 5px;
      background-color: #4e54c8;
      color: white;
      transition: background 0.3s;
    }

    .buttons button:hover {
      background-color: #3d42a6;
    }

    .laps {
      margin-top: 20px;
      max-height: 150px;
      overflow-y: auto;
      width: 200px;
    }

    .lap {
      background: #333;
      padding: 5px 10px;
      margin: 5px 0;
      border-radius: 4px;
    }
  </style>
</head>
<body>
  <h1>Stopwatch</h1>
  <div class="stopwatch" id="display">00:00:00</div>
  <div class="buttons">
    <button onclick="start()">Start</button>
    <button onclick="pause()">Pause</button>
    <button onclick="reset()">Reset</button>
    <button onclick="lap()">Lap</button>
  </div>
  <div class="laps" id="laps"></div>

  <script>
    let [seconds, minutes, hours] = [0, 0, 0];
    let display = document.getElementById("display");
    let laps = document.getElementById("laps");
    let timer = null;

    function updateDisplay() {
      let h = hours < 10 ? "0" + hours : hours;
      let m = minutes < 10 ? "0" + minutes : minutes;
      let s = seconds < 10 ? "0" + seconds : seconds;
      display.innerText = `${h}:${m}:${s}`;
    }

    function stopwatch() {
      seconds++;
      if (seconds === 60) {
        seconds = 0;
        minutes++;
        if (minutes === 60) {
          minutes = 0;
          hours++;
        }
      }
      updateDisplay();
    }

    function start() {
      if (timer !== null) return;
      timer = setInterval(stopwatch, 1000);
    }

    function pause() {
      clearInterval(timer);
      timer = null;
    }

    function reset() {
      clearInterval(timer);
      [seconds, minutes, hours] = [0, 0, 0];
      updateDisplay();
      timer = null;
      laps.innerHTML = "";
    }

    function lap() {
      if (timer !== null) {
        const lapTime = display.innerText;
        const lapElement = document.createElement("div");
        lapElement.className = "lap";
        lapElement.innerText = lapTime;
        laps.appendChild(lapElement);
      }
    }
  </script>
</body>
</html>
