# SDM-Shlok-Count
#<!DOCTYPE html>
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
        padding: 20px;
      }

      .leaderboard-container {
        background: rgba(255, 255, 255, 0.95);
        border-radius: 20px;
        padding: 30px;
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
        font-size: 2.5em;
        font-weight: 700;
        color: #2c3e50;
        margin-bottom: 10px;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
      }

      .subtitle {
        text-align: center;
        color: #7f8c8d;
        font-size: 1.1em;
        margin-bottom: 30px;
        font-weight: 500;
      }

      .leaderboard {
        list-style: none;
      }

      .leaderboard-item {
        display: flex;
        align-items: center;
        padding: 15px 20px;
        margin-bottom: 12px;
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
        font-size: 1.5em;
        font-weight: 700;
        width: 50px;
        text-align: center;
        color: #2c3e50;
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

      .name {
        flex: 1;
        font-size: 1.2em;
        font-weight: 600;
        color: #2c3e50;
        padding-left: 20px;
      }

      .score {
        font-size: 1.4em;
        font-weight: 700;
        color: #27ae60;
        padding: 8px 16px;
        background: rgba(255, 255, 255, 0.8);
        border-radius: 20px;
        min-width: 80px;
        text-align: center;
      }

      .status {
        font-size: 0.9em;
        color: #e74c3c;
        font-style: italic;
        margin-left: 10px;
      }

      .trophy {
        font-size: 1.8em;
        margin-right: 10px;
      }

      .update-date {
        text-align: center;
        color: #95a5a6;
        font-size: 0.9em;
        margin-top: 25px;
        padding-top: 20px;
        border-top: 1px solid #ecf0f1;
      }

      @media (max-width: 600px) {
        .title {
          font-size: 2em;
        }

        .leaderboard-item {
          padding: 12px 15px;
        }

        .name {
          font-size: 1.1em;
        }

        .score {
          font-size: 1.2em;
        }
      }
    </style>
  </head>
  <body>
    <div class="leaderboard-container">
      <h1 class="title">🏆 Vikhroli SDM Count</h1>
      <p class="subtitle">Leadership Board</p>

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

      <div class="update-date">📅 Last Updated: July 6th, 2025</div>
    </div>
  </body>
</html>
