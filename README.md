<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Henry Racing Game</title>
<style>
body{margin:0;background:#222;color:white;text-align:center;font-family:Arial;overflow:hidden}
#game{width:320px;height:500px;background:#444;margin:10px auto;position:relative;overflow:hidden;border:3px solid white}
#player{width:50px;height:80px;background:red;position:absolute;bottom:10px;left:135px;border-radius:10px}
.enemy{width:50px;height:80px;background:yellow;position:absolute;border-radius:10px}
#score{font-size:20px;margin:10px}
button{padding:15px 30px;font-size:18px;margin:5px;border:none;border-radius:10px}
#left{background:#0f0} #right{background:#0ff}
</style>
</head>
<body>
<h2>🏁 HENRY RACING 🏁</h2>
<div id="score">Score: 0</div>
<div id="game"><div id="player"></div></div>
<button id="left" ontouchstart="move(-30)" onmousedown="move(-30)">⬅️ LEFT</button>
<button id="right" ontouchstart="move(30)" onmousedown="move(30)">RIGHT ➡️</button>
<p>Tap buttons to move!</p>
<script>
let p=document.getElementById('player'), g=document.getElementById('game'), s=0, px=135, gameOver=false;
function move(d){ if(gameOver) return; px+=d; if(px<0)px=0; if(px>270)px=270; p.style.left=px+'px'; }
function createEnemy(){
 if(gameOver) return;
 let e=document.createElement('div'); e.className='enemy';
 e.style.left=Math.floor(Math.random()*6)*50+'px'; e.style.top='-80px';
 g.appendChild(e);
 let y=-80, speed=3+Math.random()*3;
 let fall=setInterval(()=>{
   y+=speed; e.style.top=y+'px';
   if(y>400 && y<480 && Math.abs(parseInt(e.style.left)-px)<45){ gameOver=true; alert('GAME OVER! Score: '+s); location.reload(); }
   if(y>500){ clearInterval(fall); e.remove(); s++; document.getElementById('score').innerText='Score: '+s; }
 },20);
}
setInterval(createEnemy,1000);
document.addEventListener('keydown',e=>{ if(e.key=='ArrowLeft')move(-30); if(e.key=='ArrowRight')move(30); });
</script>
</body>
</html>
