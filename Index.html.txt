<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Kartka Świąteczna dla Pani Iwony</title>

<link href="https://fonts.googleapis.com/css2?family=Great+Vibes&display=swap" rel="stylesheet">

<style>
html, body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  font-family: 'Playfair Display', serif;
  background: radial-gradient(circle at top, #0b3d2e, #021b14);
  color: #fff;
  overflow: hidden;
}

/* ŚNIEG */
.snowflake {
  position: fixed;
  top: -10px;
  pointer-events: none;
  animation: fall linear infinite;
  font-size: 12px;
}
@keyframes fall { to { transform: translateY(110vh); } }

/* START */
#start {
  position: fixed;
  inset: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  z-index: 20;
  cursor: pointer;
}

/* KOPERTA */
#envelope {
  position: fixed;
  inset: 0;
  background: linear-gradient(to bottom, #7a1c1c, #3b0000);
  transform: translateY(100%);
  transition: transform 1.2s ease-in-out;
  z-index: 15;
}
#envelope.open { transform: translateY(0); }

/* KARTKA */
#card {
  position: fixed;
  inset: 0;
  z-index: 10;
  background: radial-gradient(circle at top, #3b0000, #1a0000);
  display: none;
  overflow-y: auto;
  -webkit-overflow-scrolling: touch;
}
#card.show { display: block; }

.content {
  min-height: 120vh;
  padding: 40px 20px 80px;
  max-width: 800px;
  margin: 0 auto;
}

h2 { text-align: center; }

/* ŻYCZENIA – pisane piórem */
.wishes span {
  display: block;
  font-family: 'Great Vibes', cursive;
  font-size: 1.6rem;
  line-height: 2;
  opacity: 0;
  animation: write 1.4s forwards;
}
@keyframes write {
  from { opacity: 0; transform: translateY(15px); }
  to { opacity: 1; transform: translateY(0); }
}

.signature {
  margin-top: 40px;
  font-family: 'Great Vibes', cursive;
  font-size: 2rem;
}

/* ŚWIECE */
.candles { display: flex; justify-content: center; gap: 30px; margin: 30px 0; }
.candle { width: 18px; height: 60px; background: #eee; border-radius: 5px; position: relative; }
.flame { position: absolute; top: -20px; left: 50%; width: 14px; height: 20px; background: orange; border-radius: 50%; transform: translateX(-50%); animation: flicker 0.15s infinite; }
.spark { position: absolute; width: 4px; height: 4px; background: gold; border-radius: 50%; animation: spark 2s infinite; }
@keyframes flicker { 50% { opacity: 0.7; } }
@keyframes spark { 0%{opacity:0;}50%{opacity:1;}100%{opacity:0;} }

/* Przycisk zamknięcia */
.close-btn {
  margin: 40px auto 0;
  display: block;
  padding: 12px 24px;
  border: none;
  border-radius: 20px;
  background: #d4af37;
  font-size: 1rem;
}
</style>
</head>

<body>

<audio id="music" loop>
<source src="https://cdn.pixabay.com/audio/2022/12/20/audio_96d3d8b2d4.mp3" type="audio/mpeg">
</audio>

<div id="start">
<h1>🎄 Kliknij, aby otworzyć kartkę 🎄</h1>
<p>🎅 🦌 ❄️</p>
</div>

<div id="envelope"></div>

<div id="card">
<div class="content">
<h2>Dla Pani Iwony</h2>

<div class="candles">
<div class="candle"><div class="flame"></div><div class="spark"></div></div>
<div class="candle"><div class="flame"></div><div class="spark"></div></div>
<div class="candle"><div class="flame"></div><div class="spark"></div></div>
</div>

<div class="wishes">
<span style="animation-delay:0s">Niech te Święta niosą Pani spokój, ciepło i chwilę wytchnienia wśród bliskich.</span>
<span style="animation-delay:1.5s">Dziękuję za Pani obecność, uważność i słowa, które potrafiły dotknąć serca i otworzyć nowe przestrzenie w moim wnętrzu.</span>
<span style="animation-delay:3s">Niech Nowy Rok przyniesie Pani radość, zdrowie i wiele pięknych chwil, które zostaną w pamięci na długo.</span>
</div>

<div class="signature">Z serdecznymi pozdrowieniami,<br>Michał</div>

<button class="close-btn" id="close">Zamknij kartkę</button>
</div>
</div>

<script>
// Śnieg
for (let i = 0; i < 50; i++) {
  const s = document.createElement('div');
  s.className = 'snowflake';
  s.textContent = '❄';
  s.style.left = Math.random()*100+'vw';
  s.style.fontSize = Math.random()*10+10+'px';
  s.style.animationDuration = Math.random()*5+5+'s';
  document.body.appendChild(s);
}

// Obsługa kliknięć
const start = document.getElementById('start');
const envelope = document.getElementById('envelope');
const card = document.getElementById('card');
const music = document.getElementById('music');

start.addEventListener('click', () => {
  envelope.classList.add('open');
  start.style.display = 'none';
  music.play().catch(()=>{});
  setTimeout(()=>card.classList.add('show'),1200);
});

document.getElementById('close').addEventListener('click',()=>{
  card.classList.remove('show');
  envelope.classList.remove('open');
  start.style.display='flex';
  music.pause();
});
</script>

</body>
</html>
