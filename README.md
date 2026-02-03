<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>My Cute Lil Womaniser 💜</title>

<link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Poppins:wght@300;400&display=swap" rel="stylesheet">

<style>
body {
  margin: 0;
  font-family: 'Poppins', sans-serif;
  background: linear-gradient(135deg, #cbb4ff, #f3e9ff);
  overflow-x: hidden;
  text-align: center;
}

.quiz-box, #endMessage {
  background: rgba(255,255,255,0.95);
  max-width: 600px;
  margin: 70px auto;
  padding: 35px;
  border-radius: 25px;
  box-shadow: 0 10px 30px rgba(140, 90, 255, 0.3);
}

h1 {
  font-family: 'Pacifico', cursive;
  color: #7a3db8;
  font-size: 36px;
}

p {
  font-size: 17px;
  color: #4b2a63;
}

label {
  display: block;
  margin: 10px 0;
  cursor: pointer;
}

button {
  margin-top: 25px;
  padding: 14px 30px;
  background: linear-gradient(135deg, #8f5cff, #c77dff);
  color: white;
  border: none;
  border-radius: 30px;
  font-size: 16px;
  cursor: pointer;
}

.heart {
  position: fixed;
  color: rgba(180,130,255,0.6);
  animation: float 6s linear infinite;
}

.bigHeart {
  font-size: 60px;
  color: #ff66cc;
}

@keyframes float {
  from { transform: translateY(100vh); opacity: 1; }
  to { transform: translateY(-10vh); opacity: 0; }
}

#endMessage {
  display: none;
  min-height: 100vh;
  margin: 0;
  border-radius: 0;
  padding-top: 100px;
  background: linear-gradient(135deg, #d9b3ff, #fcd6ff);
  font-family: 'Pacifico', cursive;
  font-size: 30px;
  color: #4b2a63;
}

.countdown {
  font-family: 'Poppins', sans-serif;
  font-size: 20px;
  margin-top: 20px;
}

/* confetti */
.confetti {
  position: fixed;
  width: 10px;
  height: 10px;
  top: -10px;
  animation: fall 3s linear forwards;
  opacity: 0.9;
}

@keyframes fall {
  to { transform: translateY(110vh) rotate(360deg); }
}
</style>
</head>

<body>

<audio id="bgm" loop>
  <source src="https://actions.google.com/sounds/v1/ambiences/soft_piano_loop.ogg">
</audio>
<audio id="wrong" src="https://actions.google.com/sounds/v1/cartoon/clang_and_wobble.ogg"></audio>

<div class="quiz-box" id="quizBox">
  <h1>My Cute Lil Womaniser 💜</h1>
  <p id="question"></p>
  <div id="options"></div>
  <button onclick="nextQuestion()">Next 💜</button>
</div>

<div id="endMessage">
  <div class="bigHeart">💖</div>
  Will you be my Valentine? 💜<br><br>
  Pick me up at 11am on 14th Feb and bring flowers 🌸
  <div class="countdown" id="countdown"></div>
</div>

<script>
document.body.addEventListener('click', () => {
  document.getElementById('bgm').play();
}, { once:true });

const quiz = [
  { q:"When did we first meet, lallu? 😜", options:["22nd Sep","18th Aug","04th Sep","2nd Aug"], answer:3 },
  { q:"When I call you 'lallu,' what do I mean? 😝", options:["Tease forever","My favorite person 😍","Just joking","Steal kisses"], answer:1 },
  { q:"What’s your fav? 😏", options:["Chiku","Bhaang 🍃","Kashish 😍","Purple"], answer:2 },
  { q:"If I stole your phone? 🧐", options:["Chase me","Beg","Get dramatic","Surrender 😎"], answer:3 },
  { q:"Will you be my Valentine? 😛", options:["Yes 😘","No"], answer:0 }
];

let current = 0;

function loadQuestion(){
  document.getElementById("question").innerText = quiz[current].q;
  const opt = document.getElementById("options");
  opt.innerHTML="";
  quiz[current].options.forEach((o,i)=>{
    opt.innerHTML += `<label><input type="radio" name="opt" value="${i}"> ${o}</label>`;
  });
}
loadQuestion();

function nextQuestion(){
  const sel = document.querySelector('input[name="opt"]:checked');
  if(!sel){ alert("Answer first 😝"); return; }
  if(parseInt(sel.value) !== quiz[current].answer){
    const w = document.getElementById("wrong");
    w.currentTime=0; w.play();
    alert("Wrong 😜 Try again");
    return;
  }
  current++;
  if(current < quiz.length){ loadQuestion(); }
  else { showProposal(); }
}

function showProposal(){
  document.getElementById("quizBox").style.display="none";
  document.getElementById("endMessage").style.display="block";
  setInterval(()=>createHeart(true),200);
  burstConfetti();
  startCountdown();
}

function createHeart(big=false){
  const h=document.createElement("div");
  h.className="heart";
  if(big) h.classList.add("bigHeart");
  h.innerHTML="💜";
  h.style.left=Math.random()*100+"vw";
  document.body.appendChild(h);
  setTimeout(()=>h.remove(),6000);
}

function burstConfetti(){
  const colors=["#ff66cc","#c77dff","#8f5cff","#ffd1dc","#b388ff"];
  for(let i=0;i<150;i++){
    const c=document.createElement("div");
    c.className="confetti";
    c.style.left=Math.random()*100+"vw";
    c.style.backgroundColor=colors[Math.floor(Math.random()*colors.length)];
    c.style.animationDuration=(2+Math.random()*2)+"s";
    document.body.appendChild(c);
    setTimeout(()=>c.remove(),4000);
  }
}

function startCountdown(){
  const target = new Date("Feb 14, 2026 11:00:00").getTime();
  setInterval(()=>{
    const now=new Date().getTime();
    const d=target-now;
    if(d<0){ document.getElementById("countdown").innerText="It's time 💖"; return; }
    const days=Math.floor(d/(1000*60*60*24));
    const hrs=Math.floor((d%(1000*60*60*24))/(1000*60*60));
    const mins=Math.floor((d%(1000*60*60))/(1000*60));
    document.getElementById("countdown").innerText=`${days}d ${hrs}h ${mins}m to go 💜`;
  },1000);
}
</script>

</body>
</html>
