<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Should I Bunk Today?</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    
    body {
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #000000, #1a1a1a); /* Dark black gradient for a sleek look */
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 20px;
      overflow-x: hidden; /* Prevent horizontal scroll from animations */
      perspective: 1000px; /* Enable 3D space for the entire page */
    }
    
    /* 3D Background Container */
    .background-3d {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      z-index: -1;
      pointer-events: none;
      transform-style: preserve-3d;
    }
    
    .floating-cube {
      position: absolute;
      width: 40px;
      height: 40px;
      transform-style: preserve-3d;
      animation: float3D 20s infinite linear;
    }
    
    .floating-cube .face {
      position: absolute;
      width: 40px;
      height: 40px;
      background: linear-gradient(45deg, rgba(0, 255, 136, 0.2), rgba(255, 255, 255, 0.1));
      border: 1px solid rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(5px);
    }
    
    .floating-cube .front  { transform: translateZ(20px); }
    .floating-cube .back   { transform: rotateY(180deg) translateZ(20px); }
    .floating-cube .right  { transform: rotateY(90deg) translateZ(20px); }
    .floating-cube .left   { transform: rotateY(-90deg) translateZ(20px); }
    .floating-cube .top    { transform: rotateX(90deg) translateZ(20px); }
    .floating-cube .bottom { transform: rotateX(-90deg) translateZ(20px); }
    
    /* Multiple cubes with different positions and delays */
    .cube1 {
      top: 20%;
      left: 10%;
      animation-delay: 0s;
      animation-duration: 25s;
    }
    
    .cube2 {
      top: 60%;
      right: 15%;
      animation-delay: -5s;
      animation-duration: 30s;
    }
    
    .cube3 {
      top: 80%;
      left: 70%;
      animation-delay: -10s;
      animation-duration: 20s;
    }
    
    .cube4 {
      top: 40%;
      left: 80%;
      animation-delay: -15s;
      animation-duration: 35s;
    }
    
    .cube5 {
      top: 10%;
      right: 60%;
      animation-delay: -20s;
      animation-duration: 28s;
    }
    
    /* 3D Floating Animation Keyframe */
    @keyframes float3D {
      0% {
        transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg) translateX(0) translateY(0) translateZ(0);
        opacity: 0.6;
      }
      25% {
        transform: rotateX(90deg) rotateY(180deg) rotateZ(45deg) translateX(100px) translateY(-50px) translateZ(50px);
        opacity: 0.8;
      }
      50% {
        transform: rotateX(180deg) rotateY(360deg) rotateZ(90deg) translateX(200px) translateY(-100px) translateZ(-30px);
        opacity: 0.4;
      }
      75% {
        transform: rotateX(270deg) rotateY(540deg) rotateZ(135deg) translateX(100px) translateY(50px) translateZ(80px);
        opacity: 0.7;
      }
      100% {
        transform: rotateX(360deg) rotateY(720deg) rotateZ(180deg) translateX(0) translateY(0) translateZ(0);
        opacity: 0.6;
      }
    }
    
    .main-wrapper {
      width: 100%;
      max-width: 420px;
      animation: slideInUp 1s ease-out; /* Added slide-in animation for the main wrapper */
      transform-style: preserve-3d; /* Preserve 3D for main content */
    }
    
    .glass-card {
      background: rgba(255, 255, 255, 0.1); /* Adjusted for dark theme: semi-transparent light for glass effect */
      border-radius: 16px;
      backdrop-filter: blur(15px); /* Increased blur for better dark theme effect */
      border: 1px solid rgba(255, 255, 255, 0.2);
      padding: 32px 24px;
      text-align: center;
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3); /* Darker shadow for depth */
      animation: fadeIn 0.9s ease, float 3s ease-in-out infinite; /* Combined existing fadeIn with new floating animation */
      transform-style: preserve-3d;
    }
    
    h1 {
      font-size: 24px;
      font-weight: 600;
      margin-bottom: 12px;
      color: #ffffff; /* Changed to white for dark theme */
      animation: glow 2s ease-in-out infinite alternate; /* Added glowing animation for title */
    }
    
    .subtext {
      font-size: 14px;
      margin-bottom: 24px;
      color: #e0e0e0; /* Lighter gray for visibility */
      animation: fadeInUp 1.2s ease-out 0.3s both; /* Staggered entrance animation */
    }
    
    .inputs {
      animation: fadeInUp 1.2s ease-out 0.5s both; /* Entrance animation for inputs container */
    }
    
    .inputs input {
      width: 100%;
      padding: 12px;
      margin-bottom: 16px;
      border-radius: 10px;
      border: 1px solid rgba(255, 255, 255, 0.3); /* Lighter border for dark theme */
      font-size: 15px;
      background: rgba(0, 0, 0, 0.4); /* Dark semi-transparent background */
      color: #ffffff; /* White text */
      outline: none;
      transition: all 0.3s ease; /* Smooth transition for focus */
      transform: translateY(0);
    }
    
    .inputs input::placeholder {
      color: #b0b0b0; /* Lighter placeholder */
    }
    
    .inputs input:focus {
      border-color: #00ff88; /* Green glow on focus */
      box-shadow: 0 0 10px rgba(0, 255, 136, 0.3); /* Added glow effect */
      transform: translateY(-2px); /* Slight lift animation */
    }
    
    button {
      width: 100%;
      padding: 12px;
      font-size: 16px;
      background: linear-gradient(45deg, #2ecc71, #27ae60); /* Gradient for button */
      color: #fff;
      border: none;
      border-radius: 10px;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s ease;
      transform: translateY(0);
      animation: pulse 2s infinite; /* Subtle pulsing animation */
    }
    
    button:hover {
      background: linear-gradient(45deg, #27ae60, #2ecc71);
      transform: translateY(-3px) scale(1.02); /* Lift and scale on hover */
      box-shadow: 0 5px 15px rgba(46, 204, 113, 0.4); /* Glow shadow */
    }
    
    .result {
      margin-top: 20px;
      background: rgba(0, 0, 0, 0.5); /* Dark background for result */
      color: #ffffff; /* White text */
      padding: 16px;
      border-radius: 12px;
      font-size: 15px;
      animation: popIn 0.5s ease forwards, shake 0.5s ease 0.5s both; /* Combined popIn with shake for fun effect */
      font-weight: 500;
      border: 1px solid rgba(255, 255, 255, 0.2);
    }
    
    .hidden {
      display: none;
    }
    
    footer {
      margin-top: 30px;
      font-size: 13px;
      color: #cccccc; /* Lighter color for footer */
      text-align: center;
      animation: fadeIn 1.2s ease, slideInLeft 1s ease-out 0.8s both; /* Added slide-in from left */
    }
    
    footer a {
      color: #00ff88; /* Green link color */
      text-decoration: none;
      transition: color 0.3s ease;
    }
    
    footer a:hover {
      color: #ffffff;
      text-shadow: 0 0 5px rgba(0, 255, 136, 0.5); /* Glow on hover */
    }
    
    /* Existing animations */
    @keyframes fadeIn {
      from {
        opacity: 0;
        transform: translateY(40px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
    
    @keyframes popIn {
      from {
        transform: scale(0.95);
        opacity: 0;
      }
      to {
        transform: scale(1);
        opacity: 1;
      }
    }
    
    /* New animations */
    @keyframes float {
      0%, 100% { transform: translateY(0px); }
      50% { transform: translateY(-10px); }
    }
    
    @keyframes glow {
      from { text-shadow: 0 0 5px rgba(255, 255, 255, 0.5); }
      to { text-shadow: 0 0 20px rgba(0, 255, 136, 0.8), 0 0 30px rgba(0, 255, 136, 0.4); }
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
    
    @keyframes slideInUp {
      from {
        opacity: 0;
        transform: translateY(100px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
    
    @keyframes slideInLeft {
      from {
        opacity: 0;
        transform: translateX(-50px);
      }
      to {
        opacity: 1;
        transform: translateX(0);
      }
    }
    
    @keyframes pulse {
      0% { box-shadow: 0 0 0 0 rgba(46, 204, 113, 0.7); }
      70% { box-shadow: 0 0 0 10px rgba(46, 204, 113, 0); }
      100% { box-shadow: 0 0 0 0 rgba(46, 204, 113, 0); }
    }
    
    @keyframes shake {
      0%, 100% { transform: translateX(0); }
      10%, 30%, 50%, 70%, 90% { transform: translateX(-5px); }
      20%, 40%, 60%, 80% { transform: translateX(5px); }
    }
  </style>
</head>
<body>
  <!-- 3D Background Elements -->
  <div class="background-3d">
    <div class="floating-cube cube1">
      <div class="face front"></div>
      <div class="face back"></div>
      <div class="face right"></div>
      <div class="face left"></div>
      <div class="face top"></div>
      <div class="face bottom"></div>
    </div>
    <div class="floating-cube cube2">
      <div class="face front"></div>
      <div class="face back"></div>
      <div class="face right"></div>
      <div class="face left"></div>
      <div class="face top"></div>
      <div class="face bottom"></div>
    </div>
    <div class="floating-cube cube3">
      <div class="face front"></div>
      <div class="face back"></div>
      <div class="face right"></div>
      <div class="face left"></div>
      <div class="face top"></div>
      <div class="face bottom"></div>
    </div>
    <div class="floating-cube cube4">
      <div class="face front"></div>
      <div class="face back"></div>
      <div class="face right"></div>
      <div class="face left"></div>
      <div class="face top"></div>
      <div class="face bottom"></div>
    </div>
    <div class="floating-cube cube5">
      <div class="face front"></div>
      <div class="face back"></div>
      <div class="face right"></div>
      <div class="face left"></div>
      <div class="face top"></div>
      <div class="face bottom"></div>
    </div>
  </div>

  <div class="main-wrapper">
    <div class="glass-card">
      <h1>🎓 Should I Bunk Today?</h1>
      <p class="subtext">Your attendance fate is just a click away.</p>

      <div class="inputs">
        <input type="number" id="total" placeholder="📘 Total Classes" />
        <input type="number" id="attended" placeholder="✅ Classes Attended" />
        <input type="number" id="required" placeholder="📏 Required Attendance (%)" value="75" />
        <button onclick="calculateAttendance()">Check Now ➡️</button>
      </div>

      <div id="resultBox" class="result hidden">Let’s calculate that for you...</div>
    </div>
  </div>
  <footer>
    🔗 Created by <strong>Harsh Chavan</strong> • 
    <a href="mailto:harshchavan42@gmail.com">Mail me</a> for a custom one
  </footer>
  
  <script>
    function calculateAttendance() {
      const total = parseInt(document.getElementById("total").value);
      const attended = parseInt(document.getElementById("attended").value);
      const required = parseFloat(document.getElementById("required").value);
      const resultBox = document.getElementById("resultBox");
    
      if (isNaN(total) || isNaN(attended) || isNaN(required) || total <= 0) {
        resultBox.innerText = "⚠️ Please fill in all fields properly!";
        resultBox.classList.remove("hidden");
        return;
      }
    
      const currentPercentage = (attended / total) * 100;
      const requiredAttendance = required / 100;
      let message = "";
    
      if (currentPercentage >= required) {
        const maxBunk = Math.floor((attended - (requiredAttendance * total)) / requiredAttendance);
        message = `
          ✅ Attendance: <b>${currentPercentage.toFixed(2)}%</b><br>
          🎉 You're safe to bunk! You can miss <b>${maxBunk}</b> more class${maxBunk !== 1 ? "es" : ""}.<br>
          Enjoy... but don't overdo it 😎
        `;
      } else {
        let extraNeeded = 0;
        let newTotal = total;
        let newAttended = attended;
    
        while ((newAttended / newTotal) < requiredAttendance) {
          newTotal++;
          newAttended++;
          extraNeeded++;
        }
    
        message = `
          😔 Attendance: <b>${currentPercentage.toFixed(2)}%</b><br>
          You need to attend <b>${extraNeeded}</b> more class${extraNeeded !== 1 ? "es" : ""} to reach ${required}%<br>
          No bunks. Just lectures... for now 💪
        `;
      }
    
      resultBox.innerHTML = message;
      resultBox.classList.remove("hidden");
    }
  </script>
</body>
</html>

