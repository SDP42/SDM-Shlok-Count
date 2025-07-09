<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Vikhroli SDM Count Leaderboard</title>
    <style>
      * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
      }

      body {
        font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        min-height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 10px;
      }

      .leaderboard-container {
        background: rgba(255, 255, 255, 0.95);
        border-radius: 20px;
        padding: 20px;
        box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
        backdrop-filter: blur(10px);
        max-width: 600px;
        width: 100%;
        animation: fadeInUp 0.6s ease-out;
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

      .title {
        text-align: center;
        font-size: 2.2em;
        font-weight: 700;
        color: #2c3e50;
        margin-bottom: 8px;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        line-height: 1.2;
      }

      .subtitle {
        text-align: center;
        color: #7f8c8d;
        font-size: 1.1em;
        margin-bottom: 25px;
        font-weight: 500;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 15px;
      }

      .subtitle-icon {
        font-size: 1.5em;
        color: #e74c3c;
        display: none;
      }

      .subtitle-logo {
        height: 40px;
        width: 40px;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        transition: transform 0.3s ease;
      }

      .subtitle-logo:hover {
        transform: scale(1.1);
      }

      /* Show icons if images fail to load */
      @media screen {
        .subtitle-logo[style*="display: none"] ~ .subtitle-icon,
        .subtitle-logo:not([src]) ~ .subtitle-icon {
          display: inline-block;
        }
      }

      .leaderboard {
        list-style: none;
      }

      .leaderboard-item {
        display: flex;
        align-items: center;
        padding: 12px 15px;
        margin-bottom: 10px;
        border-radius: 15px;
        transition: all 0.3s ease;
        animation: slideIn 0.5s ease-out;
        animation-fill-mode: both;
        position: relative;
        overflow: hidden;
      }

      .leaderboard-item:hover {
        transform: translateY(-2px);
        box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
      }

      .leaderboard-item:nth-child(1) {
        background: linear-gradient(135deg, #ffd700, #ffed4a);
        animation-delay: 0.1s;
      }

      .leaderboard-item:nth-child(2) {
        background: linear-gradient(135deg, #c0c0c0, #e5e5e5);
        animation-delay: 0.2s;
      }

      .leaderboard-item:nth-child(3) {
        background: linear-gradient(135deg, #cd7f32, #daa520);
        animation-delay: 0.3s;
      }

      .leaderboard-item:nth-child(n + 4) {
        background: linear-gradient(135deg, #f8f9fa, #e9ecef);
        animation-delay: calc(0.1s * var(--index));
      }

      @keyframes slideIn {
        from {
          opacity: 0;
          transform: translateX(-50px);
        }
        to {
          opacity: 1;
          transform: translateX(0);
        }
      }

      .rank {
        font-size: 1.3em;
        font-weight: 700;
        width: 40px;
        text-align: center;
        color: #2c3e50;
        flex-shrink: 0;
      }

      .rank.gold {
        color: #b8860b;
      }
      .rank.silver {
        color: #708090;
      }
      .rank.bronze {
        color: #8b4513;
      }

      .trophy {
        font-size: 1.5em;
        margin-right: 8px;
        flex-shrink: 0;
      }

      .name {
        flex: 1;
        font-size: 1.1em;
        font-weight: 600;
        color: #2c3e50;
        padding-left: 10px;
        word-wrap: break-word;
        min-width: 0;
      }

      .score {
        font-size: 1.2em;
        font-weight: 700;
        color: #27ae60;
        padding: 6px 12px;
        background: rgba(255, 255, 255, 0.8);
        border-radius: 20px;
        min-width: 60px;
        text-align: center;
        flex-shrink: 0;
      }

      .status {
        font-size: 0.8em;
        color: #e74c3c;
        font-style: italic;
        margin-left: 8px;
        flex-shrink: 0;
      }

      .countdown-section {
        margin: 25px 0;
        padding: 20px;
        background: linear-gradient(135deg, #ff6b6b, #ffa726);
        border-radius: 15px;
        box-shadow: 0 8px 20px rgba(255, 107, 107, 0.3);
        text-align: center;
        animation: pulse 2s infinite;
      }

      @keyframes pulse {
        0%,
        100% {
          transform: scale(1);
        }
        50% {
          transform: scale(1.02);
        }
      }

      .countdown-title {
        color: white;
        font-size: 1.3em;
        font-weight: 600;
        margin-bottom: 15px;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
      }

      .countdown-timer {
        display: flex;
        justify-content: space-around;
        align-items: center;
        gap: 10px;
        flex-wrap: wrap;
      }

      .time-unit {
        background: rgba(255, 255, 255, 0.9);
        border-radius: 12px;
        padding: 10px 15px;
        min-width: 80px;
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
        transition: transform 0.3s ease;
      }

      .time-unit:hover {
        transform: translateY(-3px);
      }

      .time-value {
        display: block;
        font-size: 1.8em;
        font-weight: 700;
        color: #2c3e50;
        text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
      }

      .time-label {
        display: block;
        font-size: 0.9em;
        color: #7f8c8d;
        font-weight: 500;
        margin-top: 5px;
      }

      .countdown-finished {
        font-size: 1.5em;
        color: white;
        font-weight: 700;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        animation: bounce 1s infinite;
      }

      @keyframes bounce {
        0%,
        20%,
        50%,
        80%,
        100% {
          transform: translateY(0);
        }
        40% {
          transform: translateY(-10px);
        }
        60% {
          transform: translateY(-5px);
        }
      }

      .update-date {
        text-align: center;
        color: #95a5a6;
        font-size: 0.9em;
        margin-top: 20px;
        padding-top: 15px;
        border-top: 1px solid #ecf0f1;
      }

      /* Mobile Styles */
      @media (max-width: 600px) {
        body {
          padding: 5px;
        }

        .leaderboard-container {
          padding: 15px;
          border-radius: 15px;
        }

        .title {
          font-size: 1.8em;
          margin-bottom: 6px;
        }

        .subtitle {
          font-size: 1em;
          margin-bottom: 20px;
          gap: 10px;
        }

        .subtitle-logo {
          height: 30px;
          width: 30px;
        }

        .countdown-section {
          margin: 20px 0;
          padding: 15px;
        }

        .countdown-title {
          font-size: 1.1em;
          margin-bottom: 12px;
        }

        .countdown-timer {
          gap: 8px;
        }

        .time-unit {
          min-width: 65px;
          padding: 8px 12px;
        }

        .time-value {
          font-size: 1.5em;
        }

        .time-label {
          font-size: 0.8em;
        }

        .leaderboard-item {
          padding: 10px 12px;
          margin-bottom: 8px;
          border-radius: 12px;
        }

        .rank {
          font-size: 1.1em;
          width: 35px;
        }

        .trophy {
          font-size: 1.3em;
          margin-right: 6px;
        }

        .name {
          font-size: 1em;
          padding-left: 8px;
        }

        .score {
          font-size: 1.1em;
          padding: 5px 10px;
          min-width: 50px;
        }

        .status {
          font-size: 0.75em;
          margin-left: 6px;
        }

        .update-date {
          font-size: 0.85em;
          margin-top: 15px;
          padding-top: 12px;
        }
      }

      /* Extra small screens */
      @media (max-width: 400px) {
        .title {
          font-size: 1.6em;
        }

        .subtitle {
          gap: 8px;
        }

        .subtitle-logo {
          height: 25px;
          width: 25px;
        }

        .countdown-section {
          margin: 15px 0;
          padding: 12px;
        }

        .countdown-title {
          font-size: 1em;
          margin-bottom: 10px;
        }

        .countdown-timer {
          gap: 6px;
        }

        .time-unit {
          min-width: 55px;
          padding: 6px 10px;
        }

        .time-value {
          font-size: 1.3em;
        }

        .time-label {
          font-size: 0.7em;
        }

        .leaderboard-item {
          padding: 8px 10px;
          flex-wrap: wrap;
        }

        .rank {
          font-size: 1em;
          width: 30px;
        }

        .trophy {
          font-size: 1.2em;
          margin-right: 5px;
        }

        .name {
          font-size: 0.95em;
          padding-left: 6px;
        }

        .score {
          font-size: 1em;
          padding: 4px 8px;
          min-width: 45px;
        }

        .status {
          font-size: 0.7em;
          margin-left: 4px;
          width: 100%;
          margin-top: 2px;
          padding-left: 46px;
        }
      }

      /* Very small screens - status on new line */
      @media (max-width: 320px) {
        .subtitle {
          flex-direction: column;
          gap: 8px;
        }

        .subtitle-logo {
          height: 20px;
          width: 20px;
        }

        .countdown-timer {
          flex-direction: column;
          gap: 8px;
        }

        .time-unit {
          min-width: 120px;
          display: flex;
          align-items: center;
          justify-content: space-between;
          padding: 8px 15px;
        }

        .time-value {
          font-size: 1.5em;
        }

        .time-label {
          font-size: 0.8em;
          margin-top: 0;
        }

        .leaderboard-item {
          flex-direction: column;
          align-items: flex-start;
        }

        .leaderboard-item > div {
          display: flex;
          align-items: center;
          width: 100%;
          justify-content: space-between;
        }

        .status {
          width: 100%;
          margin-left: 0;
          margin-top: 4px;
          padding-left: 0;
          text-align: center;
        }
      }
    </style>
  </head>
  <body>
    <div class="leaderboard-container">
      <h1 class="title">🏆 Vikhroli SDM Balaks Shlok Status</h1>
      <p class="subtitle">
        <img
          src="https://img.youtube.com/vi/4oFPgtMdkUk/maxresdefault.jpg"
          alt="Mission Rajipo"
          class="subtitle-logo"
          onerror="this.src='https://i.ytimg.com/vi/4oFPgtMdkUk/hqdefault.jpg'; this.onerror=function(){this.style.display='none'}"
        />
        <span class="subtitle-icon">🎯</span>
        Mission Rajipo
        <span class="subtitle-icon">🎯</span>
        <img
          src="https://img.youtube.com/vi/4oFPgtMdkUk/maxresdefault.jpg"
          alt="Mission Rajipo"
          class="subtitle-logo"
          onerror="this.src='https://i.ytimg.com/vi/4oFPgtMdkUk/hqdefault.jpg'; this.onerror=function(){this.style.display='none'}"
        />
      </p>

      <ul class="leaderboard">
        <li class="leaderboard-item" style="--index: 1">
          <span class="rank gold">1</span>
          <span class="trophy">🥇</span>
          <span class="name">Divyam Patel</span>
          <span class="score">315</span>
        </li>

        <li class="leaderboard-item" style="--index: 2">
          <span class="rank silver">2</span>
          <span class="trophy">🥈</span>
          <span class="name">Tirth Panchal</span>
          <span class="score">315</span>
          <span class="status">(Adhiveshan Pending)</span>
        </li>

        <li class="leaderboard-item" style="--index: 3">
          <span class="rank bronze">3</span>
          <span class="trophy">🥉</span>
          <span class="name">Shubhan Dhume</span>
          <span class="score">315</span>
          <span class="status">(Adhiveshan Pending)</span>
        </li>

        <li class="leaderboard-item" style="--index: 4">
          <span class="rank">4</span>
          <span class="name">Sanjeev Konar</span>
          <span class="score">273</span>
        </li>

        <li class="leaderboard-item" style="--index: 5">
          <span class="rank">5</span>
          <span class="name">Vraj Panchal</span>
          <span class="score">200</span>
        </li>

        <li class="leaderboard-item" style="--index: 6">
          <span class="rank">6</span>
          <span class="name">Vibhu Kariya</span>
          <span class="score">130</span>
        </li>

        <li class="leaderboard-item" style="--index: 7">
          <span class="rank">7</span>
          <span class="name">Avyan Panchal</span>
          <span class="score">125</span>
        </li>

        <li class="leaderboard-item" style="--index: 8">
          <span class="rank">8</span>
          <span class="name">Smith Vadoliya</span>
          <span class="score">115</span>
        </li>

        <li class="leaderboard-item" style="--index: 9">
          <span class="rank">9</span>
          <span class="name">Mayank Vadoliya</span>
          <span class="score">115</span>
        </li>

        <li class="leaderboard-item" style="--index: 10">
          <span class="rank">10</span>
          <span class="name">Kushal Wala</span>
          <span class="score">105</span>
        </li>

        <li class="leaderboard-item" style="--index: 11">
          <span class="rank">11</span>
          <span class="name">Mayank Patel</span>
          <span class="score">100</span>
        </li>

        <li class="leaderboard-item" style="--index: 12">
          <span class="rank">12</span>
          <span class="name">Girish Deshmukh</span>
          <span class="score">55</span>
        </li>

        <li class="leaderboard-item" style="--index: 13">
          <span class="rank">13</span>
          <span class="name">Daiwik Jadeja</span>
          <span class="score">45</span>
        </li>
      </ul>

      <div class="countdown-section">
        <h3 class="countdown-title">⏰ Time Left Until October 19th</h3>
        <div class="countdown-timer" id="countdown">
          <div class="time-unit">
            <span class="time-value" id="days">00</span>
            <span class="time-label">Days</span>
          </div>
          <div class="time-unit">
            <span class="time-value" id="hours">00</span>
            <span class="time-label">Hours</span>
          </div>
          <div class="time-unit">
            <span class="time-value" id="minutes">00</span>
            <span class="time-label">Minutes</span>
          </div>
          <div class="time-unit">
            <span class="time-value" id="seconds">00</span>
            <span class="time-label">Seconds</span>
          </div>
        </div>
      </div>

      <div class="update-date">📅 Last Updated: July 6th, 2025</div>
    </div>

    <script>
      function updateCountdown() {
        // Target date: October 19, 2025 (assuming current year)
        const targetDate = new Date("2025-10-19T00:00:00").getTime();
        const now = new Date().getTime();
        const difference = targetDate - now;

        if (difference > 0) {
          // Calculate time units
          const days = Math.floor(difference / (1000 * 60 * 60 * 24));
          const hours = Math.floor(
            (difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)
          );
          const minutes = Math.floor(
            (difference % (1000 * 60 * 60)) / (1000 * 60)
          );
          const seconds = Math.floor((difference % (1000 * 60)) / 1000);

          // Update the display
          document.getElementById("days").textContent = days
            .toString()
            .padStart(2, "0");
          document.getElementById("hours").textContent = hours
            .toString()
            .padStart(2, "0");
          document.getElementById("minutes").textContent = minutes
            .toString()
            .padStart(2, "0");
          document.getElementById("seconds").textContent = seconds
            .toString()
            .padStart(2, "0");
        } else {
          // Countdown finished
          document.getElementById("countdown").innerHTML =
            '<div class="countdown-finished">🎉 Time\'s Up! 🎉</div>';
        }
      }

      // Update countdown every second
      updateCountdown();
      setInterval(updateCountdown, 1000);
    </script>
  </body>
</html>

