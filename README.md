<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Be My Valentine 💖</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
}

body {
  height: 100vh;
  background: linear-gradient(-45deg, #ff4e50, #f857a6, #ff758c, #ff7eb3);
  background-size: 400% 400%;
  animation: bgMove 12s ease infinite;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  color: white;
}

@keyframes bgMove {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.card {
  background: rgba(255,255,255,0.15);
  backdrop-filter: blur(14px);
  padding: 45px;
  border-radius: 30px;
  text-align: center;
  width: 90%;
  max-width: 420px;
  box-shadow: 0 25px 50px rgba(0,0,0,0.35);
}

h1 {
  font-size: 2.4rem;
  margin-bottom: 15px;
}

p {
  font-size: 1.1rem;
  margin-bottom: 30px;
}

.buttons {
  position: relative;
  height: 70px;
}

button {
  padding: 14px 32px;
  font-size: 1.1rem;
  border-radius: 50px;
  border: none;
  cursor: pointer;
  transition: 0.3s ease;
}

#yes {
  background: #ff2e63;
  color: white;
  box-shadow: 0 0 25px rgba(255,46,99,0.9);
}

#no {
  background: white;
  color: #ff2e63;
  position: absolute;
  right: 0;
}

#msg {
  margin-top: 20px;
  font-size: 1.2rem;
  min-height: 30px;
}

/* Floating love items */
.love {
  position: absolute;
  font-size: 22px;
  animation: float 6s linear infinite;
  opacity: 0.9;
}

@keyframes float {
  0% { transform: translateY(100vh) scale(0.6); }
  100% { transform: translateY(-10vh) scale(1.4); }
}

/* Confetti */
.confetti {
  position: fixed;
  width: 10px;
  height: 10px;
  background: white;
  animation: fall 3s linear forwards;
}

@keyframes fall {
  0% { transform: translateY(-10vh) rotate(0deg); }
  100% { transform: translateY(110vh) rotate(720deg); }
}
</style>
</head>

<body>

<div class="card" id="card">
  <h1>💍 Will You Be My Valentine? 💖</h1>
  <p>I promise unlimited smiles, care & love 😌</p>

  <div class="buttons">
    <button id="yes">Yes 💕</button>
    <button id="no">No 🙃</button>
  </div>

  <div id="msg"></div>
</div>

<script>
let count = 0;
const messages = [
  "Are you really sure? 🥺",
  "That hurt a little 💔",
  "I’ll wait… 😌",
  "Love says try again 💖",
  "You know you want to 😏",
  "Destiny says YES 💍"
];

const yes = document.getElementById("yes");
const no = document.getElementById("no");
const msg = document.getElementById("msg");
const card = document.getElementById("card");

no.addEventListener("click", () => {
  count++;
  msg.textContent = messages[count % messages.length];

  // grow yes
  yes.style.transform = `scale(${1 + count * 0.25})`;

  // dodge no
  no.style.top = Math.random() * 40 + "px";
  no.style.left = Math.random() * 200 - 100 + "px";
});

yes.addEventListener("click", () => {
  card.innerHTML = `
    <h1>YAAAY!! 💖🎉</h1>
    <p>You just made this Valentine unforgettable 💍✨</p>
  `;
  confettiBlast();
});

// floating hearts & rings
setInterval(() => {
  const el = document.createElement("div");
  el.className = "love";
  el.innerHTML = Math.random() > 0.5 ? "💖" : "💍";
  el.style.left = Math.random() * 100 + "vw";
  el.style.animationDuration = 4 + Math.random() * 4 + "s";
  document.body.appendChild(el);
  setTimeout(() => el.remove(), 8000);
}, 250);

// confetti
function confettiBlast() {
  for (let i = 0; i < 80; i++) {
    const c = document.createElement("div");
    c.className = "confetti";
    c.style.left = Math.random() * 100 + "vw";
    c.style.background = `hsl(${Math.random()*360},100%,70%)`;
    c.style.animationDuration = 2 + Math.random() * 2 + "s";
    document.body.appendChild(c);
    setTimeout(() => c.remove(), 4000);
  }
}
</script>

</body>
</html>
