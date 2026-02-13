<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Will You Be My Valentine? 💕</title>
  <style>
    :root {
      --pink: #ff85c2;
      --dark-pink: #e065a3;
      --bg: #fff0f5;
      --text: #4a2c3f;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: system-ui, -apple-system, sans-serif;
      background: linear-gradient(135deg, #fff0f5, #ffe4e9);
      color: var(--text);
      min-height: 100vh;
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;
    }

    .hearts {
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      pointer-events: none;
      z-index: 1;
    }

    .heart {
      position: absolute;
      font-size: 1.8rem;
      animation: float 8s linear infinite;
      opacity: 0.7;
    }

    @keyframes float {
      0%   { transform: translateY(100vh) rotate(0deg); }
      100% { transform: translateY(-15vh) rotate(360deg); }
    }

    .container {
      text-align: center;
      padding: 30px;
      max-width: 90%;
      z-index: 10;
      background: rgba(255,255,255,0.75);
      border-radius: 24px;
      box-shadow: 0 10px 40px rgba(255,105,180,0.3);
      backdrop-filter: blur(8px);
      border: 2px solid rgba(255,182,193,0.6);
    }

    h1 {
      font-size: 3.4rem;
      color: var(--dark-pink);
      margin-bottom: 1.5rem;
      text-shadow: 0 2px 10px rgba(255,105,180,0.4);
    }

    .emoji {
      font-size: 4.5rem;
      margin: 20px 0;
      display: block;
      animation: beat 1.4s infinite;
    }

    @keyframes beat {
      0%, 100% { transform: scale(1); }
      50%      { transform: scale(1.15); }
    }

    .question {
      font-size: 2.1rem;
      margin: 30px 0 40px;
      line-height: 1.4;
    }

    .buttons {
      display: flex;
      justify-content: center;
      gap: 60px;
      flex-wrap: wrap;
    }

    button {
      font-size: 1.5rem;
      padding: 18px 50px;
      border: none;
      border-radius: 50px;
      cursor: pointer;
      transition: all 0.3s;
      font-weight: bold;
    }

    #yesBtn {
      background: var(--pink);
      color: white;
      box-shadow: 0 6px 20px rgba(255,105,180,0.5);
    }

    #yesBtn:hover {
      transform: scale(1.12);
      background: #ff4da6;
    }

    #noBtn {
      background: #e0e0e0;
      color: #555;
      box-shadow: 0 6px 20px rgba(0,0,0,0.15);
      position: relative;
      transition: all 0.25s;
    }

    #noBtn:hover {
      background: #ff9999;
      color: white;
    }

    .message {
      display: none;
      margin-top: 50px;
      font-size: 2.2rem;
      color: var(--dark-pink);
      animation: fadeIn 1.5s;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(30px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    .hidden {
      display: none !important;
    }

    @media (max-width: 600px) {
      h1 { font-size: 2.6rem; }
      .question { font-size: 1.7rem; }
      button { font-size: 1.3rem; padding: 14px 40px; }
      .emoji { font-size: 3.8rem; }
    }
  </style>
</head>
<body>

  <div class="hearts" id="hearts"></div>

  <div class="container">
    <div class="emoji">💖</div>
    <h1>Hey [Their Name / Cutie]!</h1>
    
    <div id="questionScreen">
      <div class="question">
        Will you be my Valentine? 💕<br>
        <small>(no pressure... okay maybe a little 😭)</small>
      </div>

      <div class="buttons">
        <button id="yesBtn">Yes! 💘</button>
        <button id="noBtn">No 😢</button>
      </div>
    </div>

    <div id="happyScreen" class="message">
      <div class="emoji">🎉🥰💕</div>
      <p>Yayyyy! You said YES!</p>
      <p>I’m the luckiest person in the world right now 💗</p>
      <p>Thank you for making my heart do little flips every day</p>
      <p>Love you tons × infinity ♾️</p>
    </div>
  </div>

  <script>
    // Floating hearts
    function createHeart() {
      const heart = document.createElement('div');
      heart.className = 'heart';
      heart.innerHTML = ['❤️','💖','💕','💗','💞'][Math.floor(Math.random()*5)];
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.animationDuration = (Math.random() * 5 + 6) + 's';
      heart.style.fontSize = (Math.random() * 1.2 + 1.1) + 'rem';
      document.getElementById('hearts').appendChild(heart);
      
      setTimeout(() => heart.remove(), 9000);
    }

    setInterval(createHeart, 400);

    // Interaction logic
    const yesBtn = document.getElementById('yesBtn');
    const noBtn  = document.getElementById('noBtn');
    const questionScreen = document.getElementById('questionScreen');
    const happyScreen    = document.getElementById('happyScreen');

    yesBtn.addEventListener('click', () => {
      questionScreen.classList.add('hidden');
      happyScreen.style.display = 'block';
      
      // Extra celebration hearts
      for(let i = 0; i < 30; i++) {
        setTimeout(createHeart, i * 80);
      }
    });

    noBtn.addEventListener('mouseover', () => {
      const x = Math.random() * (window.innerWidth - 200);
      const y = Math.random() * (window.innerHeight - 200);
      noBtn.style.position = 'absolute';
      noBtn.style.left = x + 'px';
      noBtn.style.top  = y + 'px';
    });

    noBtn.addEventListener('click', (e) => {
      e.preventDefault();
      alert("Wait... you weren't supposed to click that one 😭\nTry the other button pls 🥺");
      noBtn.style.position = 'relative';
      noBtn.style.left = 'auto';
      noBtn.style.top = 'auto';
    });
  </script>
</body>
</html>
