<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Be My Valentine 💖</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Comic Sans MS',cursive}

body{
height:100vh;
overflow:hidden;
display:flex;
justify-content:center;
align-items:center;
background:linear-gradient(270deg,#ff0080,#ff8c00,#40e0d0,#ff0080);
background-size:800% 800%;
animation:bg 12s ease infinite;
}

@keyframes bg{
0%{background-position:0% 50%}
50%{background-position:100% 50%}
100%{background-position:0% 50%}
}

/* Glass card */
.card{
backdrop-filter:blur(20px);
background:rgba(255,255,255,0.2);
border:2px solid rgba(255,255,255,0.3);
padding:50px;
border-radius:30px;
text-align:center;
box-shadow:0 30px 60px rgba(0,0,0,0.4);
color:white;
z-index:10;
}

h1{
font-size:3rem;
text-shadow:0 0 15px pink;
}

.buttons{
margin-top:30px;
display:flex;
gap:25px;
justify-content:center;
}

button{
padding:15px 45px;
font-size:1.4rem;
border:none;
border-radius:50px;
cursor:pointer;
transition:0.3s;
}

#yesBtn{
background:#ff2e63;
color:white;
box-shadow:0 0 20px hotpink;
animation:pulse 2s infinite;
}

@keyframes pulse{
0%{transform:scale(1)}
50%{transform:scale(1.05)}
100%{transform:scale(1)}
}

#noBtn{
background:#222;
color:white;
}

/* Love meter */
.meter{
width:100%;
height:15px;
background:rgba(255,255,255,0.3);
border-radius:20px;
margin-top:20px;
overflow:hidden;
}

.fill{
height:100%;
width:0%;
background:linear-gradient(90deg,#ff2e63,#ffcccb);
transition:0.5s;
}

#message{
margin-top:15px;
font-size:1.2rem;
}

/* Floating emojis */
.float{
position:absolute;
animation:float 6s linear infinite;
font-size:24px;
}

@keyframes float{
from{transform:translateY(100vh);opacity:1}
to{transform:translateY(-10vh);opacity:0}
}

/* Sparkles */
.spark{
position:absolute;
width:6px;
height:6px;
background:gold;
border-radius:50%;
pointer-events:none;
animation:spark 1s forwards;
}

@keyframes spark{
to{transform:scale(4);opacity:0}
}

/* Confetti */
.confetti{
position:absolute;
width:10px;
height:10px;
animation:fall 3s linear infinite;
}

@keyframes fall{
from{transform:translateY(-10vh) rotate(0)}
to{transform:translateY(110vh) rotate(360deg)}
}

/* Shake */
.shake{
animation:shake 0.3s;
}

@keyframes shake{
0%{transform:translateX(0)}
25%{transform:translateX(-10px)}
50%{transform:translateX(10px)}
75%{transform:translateX(-10px)}
100%{transform:translateX(0)}
}
</style>
</head>

<body>

<div class="card" id="card">
<h1>Will you be my Valentine? 💖</h1>

<div class="buttons">
<button id="yesBtn">Yes 😍</button>
<button id="noBtn">No 🙄</button>
</div>

<div class="meter">
<div class="fill" id="fill"></div>
</div>

<div id="message"></div>
</div>

<audio id="music" loop>
<source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3">
</audio>

<script>
const yesBtn=document.getElementById("yesBtn")
const noBtn=document.getElementById("noBtn")
const msg=document.getElementById("message")
const fill=document.getElementById("fill")
const card=document.getElementById("card")
const music=document.getElementById("music")

let count=0

const texts=[
"Are you sure? 🥺",
"Think again 💭",
"My heart is breaking 💔",
"I spent hours coding this 😭",
"Don't be evil 😤",
"You cannot escape 😈",
"YES IS DESTINY 💘"
]

noBtn.onclick=()=>{
count++
msg.innerText=texts[count%texts.length]

fill.style.width=Math.min(count*15,100)+"%"

yesBtn.style.transform=`scale(${1+count*0.2})`
yesBtn.style.boxShadow=`0 0 ${20+count*10}px hotpink`

noBtn.style.position="absolute"
noBtn.style.left=Math.random()*80+"%"
noBtn.style.top=Math.random()*80+"%"

card.classList.add("shake")
setTimeout(()=>card.classList.remove("shake"),300)

spawnFloat()
}

yesBtn.onclick=()=>{
music.play()
document.body.innerHTML=`
<h1 style="font-size:4rem;color:white;text-align:center;">
💖 YOU SAID YES 💖<br><br>
THIS IS TRUE LOVE 😍💍
</h1>
`
for(let i=0;i<200;i++)spawnConfetti()
for(let i=0;i<100;i++)spawnFloat()
}

/* Floating emojis */
function spawnFloat(){
const e=document.createElement("div")
e.className="float"
const arr=["❤️","💖","💕","💋","💍","😍","🥰"]
e.innerHTML=arr[Math.floor(Math.random()*arr.length)]
e.style.left=Math.random()*100+"vw"
e.style.fontSize=Math.random()*30+20+"px"
document.body.appendChild(e)
setTimeout(()=>e.remove(),6000)
}
setInterval(spawnFloat,250)

/* Confetti */
function spawnConfetti(){
const c=document.createElement("div")
c.className="confetti"
c.style.left=Math.random()*100+"vw"
c.style.background=`hsl(${Math.random()*360},100%,50%)`
document.body.appendChild(c)
setTimeout(()=>c.remove(),3000)
}

/* Sparkles */
document.addEventListener("mousemove",e=>{
const s=document.createElement("div")
s.className="spark"
s.style.left=e.pageX+"px"
s.style.top=e.pageY+"px"
document.body.appendChild(s)
setTimeout(()=>s.remove(),1000)
})
</script>
</body>
</html>
