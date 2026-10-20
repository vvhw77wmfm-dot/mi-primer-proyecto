[index.html](https://github.com/user-attachments/files/33725856/index.html)
# mi-primer-proyecto<!doctype html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<meta name="theme-color" content="#061426">
<title>BRICK AZUL · Juego de romper ladrillos</title>
<style>
:root{color-scheme:dark;font-family:Inter,Segoe UI,Arial,sans-serif;background:#061426;color:#e7f5ff}
*{box-sizing:border-box}body{margin:0;min-height:100vh;background:radial-gradient(ellipse at 50% 10%,#123653 0,transparent 65%),#061426;padding:30px 20px}
main{width:min(100%,940px);margin:auto}header{display:flex;align-items:center;justify-content:space-between;gap:20px;margin-bottom:24px}.brand{display:flex;align-items:center;gap:14px}.logo{display:grid;grid-template-columns:repeat(2,12px);gap:4px;transform:rotate(-9deg)}.logo i{height:12px;background:#5dd5ff;border-radius:3px}.logo i:nth-child(2){background:#2188f5}.logo i:nth-child(3){background:#1670ca}.logo i:nth-child(4){background:#a6eaff}h1{font-size:24px;letter-spacing:4px;margin:0;font-weight:850}.subtitle{font-size:12px;color:#8bacc9;margin:5px 0 0;letter-spacing:1px}.tag{font-size:11px;border:1px solid #244764;border-radius:20px;padding:8px 12px;letter-spacing:1.5px;color:#a3c8e4}
.dashboard{display:flex;justify-content:space-between;align-items:center;gap:12px;flex-wrap:wrap;margin:0 0 15px}.stats{display:flex;gap:28px}.stat span{display:block;font-size:10px;letter-spacing:1.6px;color:#93b4cf;margin-bottom:6px}.stat strong{font-size:23px;font-variant-numeric:tabular-nums}.stat:last-child strong{color:#72d7ff}.actions{display:flex;gap:8px}button{font:inherit;font-size:13px;border:1px solid #30516b;background:#102c43;color:#d6eeff;padding:10px 16px;border-radius:9px;cursor:pointer;min-height:42px}button:hover{background:#1a405c}button:focus-visible,canvas:focus-visible{outline:3px solid #a2ecff;outline-offset:4px}button:disabled{opacity:.45;cursor:default}.primary{background:#60d7ff;border-color:#60d7ff;color:#052039;font-weight:750}.primary:hover{background:#94e6ff}
.arena{position:relative;border:1px solid #2a5975;border-radius:18px;overflow:hidden;box-shadow:0 28px 90px #0006,0 0 45px #208fff10;background:#061426}canvas{display:block;width:100%;aspect-ratio:900/560;touch-action:none;background:linear-gradient(#091c30,#061321)}.overlay{position:absolute;inset:0;display:flex;justify-content:center;align-items:center;background:#0410209c;padding:20px;text-align:center;backdrop-filter:blur(5px)}.overlay[hidden]{display:none}.panel{max-width:400px}.eyebrow{color:#6cd8ff;font-size:11px;letter-spacing:3px;font-weight:700}.panel h2{font-size:clamp(26px,5vw,48px);letter-spacing:-1.5px;margin:12px 0}.panel p{font-size:14px;line-height:1.6;color:#b4cde1;margin:0 0 24px}.panel button{font-size:15px;padding:13px 28px}.foot{display:flex;justify-content:space-between;gap:16px;flex-wrap:wrap;margin:17px 2px;color:#8eafc8;font-size:12px;line-height:1.8}kbd{font:inherit;color:#c9edff;background:#163249;border:1px solid #294a65;border-radius:4px;padding:2px 5px}.live{min-height:20px;font-size:12px;color:#79d5f7;margin-top:6px}footer{margin-top:28px;text-align:center;font-size:10px;letter-spacing:2px;color:#668aa7}
@media(min-width:601px){body{padding:20px}main{width:min(100%,940px,max(600px,calc((100svh - 260px)*1.607)))}header{margin-bottom:18px}footer{margin-top:16px}}
@media(max-width:600px){body{padding:18px 12px}.tag{display:none}h1{font-size:21px}.stats{gap:20px}.stat strong{font-size:19px}.actions{gap:6px}button{padding:9px 12px}.arena{border-radius:12px}canvas{aspect-ratio:4/5}.foot{gap:4px}.panel h2{font-size:32px}.panel p{font-size:13px}.dashboard{gap:18px}}
@media(prefers-reduced-motion:reduce){.overlay{backdrop-filter:none}}
</style>
</head>
<body>
<main>
 <header><div class="brand"><div class="logo" aria-hidden="true"><i></i><i></i><i></i><i></i></div><div><h1>BRICK AZUL</h1><p class="subtitle">UN CLÁSICO. UNA NUEVA OLA.</p></div></div><div class="tag">ARCADE / 01</div></header>
 <section class="dashboard" aria-label="Marcador y controles">
  <div class="stats"><div class="stat"><span>PUNTOS</span><strong id="score">0000</strong></div><div class="stat"><span>NIVEL</span><strong id="level">01</strong></div><div class="stat"><span>VIDAS</span><strong id="lives">3</strong></div></div>
  <div class="actions"><button id="pause" disabled>Pausar</button><button id="restart">Reiniciar</button><button id="sound" aria-pressed="false" aria-label="Activar sonido">Sonido: no</button></div>
 </section>
 <div class="arena">
  <canvas id="game" width="900" height="560" aria-label="Juego de romper ladrillos. Mueve la pala con el ratón, las flechas o el dedo. Espacio para lanzar la pelota; P para pausar.">Tu navegador necesita admitir Canvas para jugar.</canvas>
  <div class="overlay" id="overlay"><div class="panel"><div class="eyebrow" id="eyebrow">ENTRA EN LA ZONA AZUL</div><h2 id="title">Rompe la rutina.</h2><p id="description">Despeja los ladrillos y mantén la pelota en juego. Tienes 3 vidas y 3 niveles por conquistar.</p><button class="primary" id="play">Jugar ahora</button></div></div>
 </div>
 <div class="foot"><span>Ratón / dedo o <kbd>←</kbd> <kbd>→</kbd> para mover</span><span><kbd>Espacio</kbd> lanzar · <kbd>P</kbd> pausa</span></div>
 <div class="live" id="status" role="status" aria-live="polite">Todo listo. Pulsa «Jugar ahora».</div>
 <footer>PRECISIÓN · REFLEJOS · AZUL</footer>
</main>
<script>
(() => {
 'use strict';
 const canvas=document.getElementById('game'),ctx=canvas.getContext('2d');
 const ui={};for(const id of ['score','level','lives','pause','restart','sound','overlay','eyebrow','title','description','play','status'])ui[id]=document.getElementById(id);
 const W=900,H=560,R=8,colors=['#1573d1','#2189ef','#36a8f5','#55c5fa','#8de3ff'];
 const reduced=matchMedia('(prefers-reduced-motion: reduce)').matches;
 let state='intro',previousState='ready',score=0,lives=3,level=1,bricks=[],particles=[],trail=[],keys={},last=0,accumulator=0;
 let paddle={x:W/2,w:128,h:13,y:H-42},ball={x:W/2,y:H-65,vx:0,vy:0};
 let soundOn=false,audio=null;
 function tone(freq=420){if(!soundOn)return;try{audio??=new (window.AudioContext||window.webkitAudioContext)();audio.resume().catch(()=>{});const o=audio.createOscillator(),g=audio.createGain();o.type='sine';o.frequency.setValueAtTime(freq,audio.currentTime);g.gain.setValueAtTime(.055,audio.currentTime);g.gain.exponentialRampToValueAtTime(.001,audio.currentTime+.09);o.connect(g);g.connect(audio.destination);o.start();o.stop(audio.currentTime+.1);}catch{}}
 function hud(){ui.score.textContent=String(score).padStart(4,'0');ui.level.textContent=String(level).padStart(2,'0');ui.lives.textContent=lives;ui.pause.disabled=!['ready','playing','paused'].includes(state);ui.pause.textContent=state==='paused'?'Continuar':'Pausar';}
 function message(text){ui.status.textContent=text;}
 function overlay(eyebrow,title,description,button){ui.eyebrow.textContent=eyebrow;ui.title.textContent=title;ui.description.textContent=description;ui.play.textContent=button;ui.overlay.hidden=false;}
 function field(){bricks=[];const cols=10,rows=4+level,gap=8,bw=(W-96-(cols-1)*gap)/cols;for(let row=0;row<rows;row++)for(let col=0;col<cols;col++)bricks.push({x:48+col*(bw+gap),y:64+row*30,w:bw,h:22,alive:true,color:colors[row%5],value:(rows-row)*10});}
 function ready(text){state='ready';paddle.x=W/2;paddle.w=128-(level-1)*9;ball={x:paddle.x,y:paddle.y-R-2,vx:0,vy:0};trail=[];ui.overlay.hidden=true;message(text||'Pulsa Espacio o toca el tablero para lanzar.');hud();}
 function reset(){score=0;lives=3;level=1;particles=[];keys={};field();ready();}
 function launch(){if(state!=='ready')return;const speed=340+(level-1)*45;ball.vx=speed*.42;ball.vy=-Math.sqrt(speed*speed-ball.vx*ball.vx);state='playing';message('¡En juego! Rompe todos los ladrillos.');hud();tone(520);}
 function pause(){if(state==='paused'){state=previousState;ui.overlay.hidden=true;message(state==='ready'?'Pulsa Espacio o toca el tablero para lanzar.':'¡Seguimos!');}else if(state==='playing'||state==='ready'){previousState=state;state='paused';keys={};overlay('UN RESPIRO','En pausa','La partida te espera.','Continuar');message('Partida en pausa.');}hud();}
 function burst(brick){if(reduced)return;for(let i=0;i<9;i++)particles.push({x:brick.x+brick.w/2,y:brick.y+brick.h/2,vx:(Math.random()-.5)*220,vy:(Math.random()-.5)*200,life:.45,color:brick.color});}
 function finish(won){state=won?'won':'lost';keys={};hud();const text=`Has conseguido ${score} puntos.`;overlay(won?'LOS TRES NIVELES COMPLETADOS':'OTRA OLA TE ESPERA',won?'¡Lo has bordado!':'Fin de la partida',text, 'Volver a jugar');message((won?'¡Victoria! ':'Fin de la partida. ')+text);}
 function update(dt){
  particles=particles.filter(p=>(p.life-=dt)>0);for(const p of particles){p.x+=p.vx*dt;p.y+=p.vy*dt;p.vy+=220*dt;}
  if(state!=='playing'&&state!=='ready')return;
  if(keys.ArrowLeft||keys.a||keys.A)paddle.x-=620*dt;
  if(keys.ArrowRight||keys.d||keys.D)paddle.x+=620*dt;
  paddle.x=Math.max(paddle.w/2+10,Math.min(W-paddle.w/2-10,paddle.x));
  if(state==='ready'){ball.x=paddle.x;ball.y=paddle.y-R-2;return;}
  const oldX=ball.x,oldY=ball.y;ball.x+=ball.vx*dt;ball.y+=ball.vy*dt;
  if(ball.x<R){ball.x=R;ball.vx=Math.abs(ball.vx);tone(240);}else if(ball.x>W-R){ball.x=W-R;ball.vx=-Math.abs(ball.vx);tone(240);}
  if(ball.y<R){ball.y=R;ball.vy=Math.abs(ball.vy);tone(240);}
  if(ball.vy>0&&oldY+R<=paddle.y&&ball.y+R>=paddle.y&&ball.x+R>=paddle.x-paddle.w/2&&ball.x-R<=paddle.x+paddle.w/2){const offset=Math.max(-1,Math.min(1,(ball.x-paddle.x)/(paddle.w/2)));const angle=offset*1.08;const speed=Math.min(560,Math.hypot(ball.vx,ball.vy)+4);ball.vx=Math.sin(angle)*speed;ball.vy=-Math.cos(angle)*speed;ball.y=paddle.y-R-.1;tone(400);}
  for(const b of bricks){if(!b.alive)continue;const nearestX=Math.max(b.x,Math.min(ball.x,b.x+b.w)),nearestY=Math.max(b.y,Math.min(ball.y,b.y+b.h));if((ball.x-nearestX)**2+(ball.y-nearestY)**2>R*R)continue;b.alive=false;score+=b.value;burst(b);tone(560+Math.random()*200);
   if(oldY+R<=b.y){ball.vy=-Math.abs(ball.vy);ball.y=b.y-R-.1;}else if(oldY-R>=b.y+b.h){ball.vy=Math.abs(ball.vy);ball.y=b.y+b.h+R+.1;}else if(oldX<b.x){ball.vx=-Math.abs(ball.vx);ball.x=b.x-R-.1;}else{ball.vx=Math.abs(ball.vx);ball.x=b.x+b.w+R+.1;}hud();break;}
  if(!bricks.some(b=>b.alive)){if(level===3){finish(true);return;}level++;field();ready(`¡Nivel ${level}! Pulsa Espacio o toca el tablero para lanzar.`);tone(900);return;}
  if(ball.y-R>H){lives--;tone(140);if(lives<=0)finish(false);else ready(`Te quedan ${lives} vidas. Pulsa Espacio o toca el tablero para lanzar.`);}
 }
 function rounded(x,y,w,h,r){ctx.beginPath();ctx.roundRect(x,y,w,h,r);}
 function draw(){
  ctx.clearRect(0,0,W,H);ctx.fillStyle='#36658a22';for(let x=26;x<W;x+=28)for(let y=24;y<H;y+=28){ctx.beginPath();ctx.arc(x,y,.8,0,Math.PI*2);ctx.fill();}
  ctx.strokeStyle='#36658a30';ctx.beginPath();ctx.moveTo(30,32);ctx.lineTo(W-30,32);ctx.stroke();
  for(const b of bricks){if(!b.alive)continue;ctx.shadowBlur=reduced?0:9;ctx.shadowColor=b.color+'45';ctx.fillStyle=b.color;rounded(b.x,b.y,b.w,b.h,5);ctx.fill();ctx.shadowBlur=0;ctx.fillStyle='#e4faff35';rounded(b.x+3,b.y+2,b.w-6,3,2);ctx.fill();}
  for(const p of particles){ctx.globalAlpha=Math.max(0,p.life/.45);ctx.fillStyle=p.color;ctx.fillRect(p.x,p.y,3,3);}ctx.globalAlpha=1;
  if(!reduced&&state==='playing'){trail.push({x:ball.x,y:ball.y});if(trail.length>12)trail.shift();}else trail=[];
  trail.forEach((p,i)=>{ctx.fillStyle=`rgba(100,210,255,${i/trail.length*.25})`;ctx.beginPath();ctx.arc(p.x,p.y,R*i/trail.length,0,Math.PI*2);ctx.fill();});
  ctx.shadowColor='#46caff';ctx.shadowBlur=18;const gradient=ctx.createLinearGradient(paddle.x-paddle.w/2,0,paddle.x+paddle.w/2,0);gradient.addColorStop(0,'#1687dd');gradient.addColorStop(.5,'#a2efff');gradient.addColorStop(1,'#1687dd');ctx.fillStyle=gradient;rounded(paddle.x-paddle.w/2,paddle.y,paddle.w,paddle.h,7);ctx.fill();
  ctx.fillStyle='#e0faff';ctx.shadowBlur=16;ctx.beginPath();ctx.arc(ball.x,ball.y,R,0,Math.PI*2);ctx.fill();ctx.shadowBlur=0;
  if(state==='ready'){ctx.fillStyle='#a2cce4';ctx.font='14px Segoe UI, sans-serif';ctx.textAlign='center';ctx.fillText('ESPACIO O CLIC PARA LANZAR',W/2,H-92);}
 }
 function frame(time){const dt=Math.min((time-last)/1000||0,.04);last=time;accumulator+=dt;while(accumulator>=1/240){update(1/240);accumulator-=1/240;}draw();requestAnimationFrame(frame);}
 function pointer(e){if(state!=='playing'&&state!=='ready')return;const r=canvas.getBoundingClientRect();paddle.x=Math.max(paddle.w/2+10,Math.min(W-paddle.w/2-10,(e.clientX-r.left)/r.width*W));if(state==='ready')ball.x=paddle.x;}
 canvas.addEventListener('pointermove',pointer);
 canvas.addEventListener('pointerdown',e=>{pointer(e);if(state==='ready')launch();});
 window.addEventListener('keydown',e=>{if(e.target instanceof HTMLButtonElement)return;if(['ArrowLeft','ArrowRight','Space','KeyP','KeyA','KeyD'].includes(e.code))e.preventDefault();keys[e.key]=true;if(e.repeat)return;if(e.code==='Space'){if(state==='intro'||state==='won'||state==='lost'){reset();launch();}else if(state==='ready')launch();else pause();}if(e.code==='KeyP')pause();});
 window.addEventListener('keyup',e=>{delete keys[e.key];});
 window.addEventListener('blur',()=>{keys={};if(state==='playing'||state==='ready')pause();});
 document.addEventListener('visibilitychange',()=>{if(document.hidden&&(state==='playing'||state==='ready'))pause();});
 ui.play.addEventListener('click',()=>{if(state==='paused')pause();else{reset();launch();}ui.play.blur();});
 ui.pause.addEventListener('click',()=>{pause();ui.pause.blur();});
 ui.restart.addEventListener('click',()=>{reset();ui.restart.blur();});
 ui.sound.addEventListener('click',()=>{soundOn=!soundOn;ui.sound.textContent='Sonido: '+(soundOn?'sí':'no');ui.sound.setAttribute('aria-pressed',String(soundOn));ui.sound.setAttribute('aria-label',soundOn?'Desactivar sonido':'Activar sonido');tone();ui.sound.blur();});
 field();hud();requestAnimationFrame(frame);
})();
</script>
</body>
</html>
