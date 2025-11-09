<!doctype html>

<html lang="sw">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Ujumbe wa Motivation</title>
  <style>
    :root{--bg:#0f1724;--card:#0b1220;--accent:#06b6d4;--glass:rgba(255,255,255,0.03)}
    *{box-sizing:border-box;font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial}
    html,body{height:100%;margin:0;background:linear-gradient(180deg,var(--bg),#081020);color:#e6eef6}
    .wrap{min-height:100%;display:flex;align-items:center;justify-content:center;padding:28px}
    .card{width:100%;max-width:420px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border-radius:16px;padding:28px;box-shadow:0 6px 30px rgba(2,6,23,0.6);backdrop-filter: blur(6px);border:1px solid rgba(255,255,255,0.03)}
    .title{font-size:18px;margin:0 0 12px;opacity:0.95}
    .touch-box{display:flex;align-items:center;justify-content:center;height:130px;border-radius:12px;background:var(--glass);cursor:pointer;border:1px dashed rgba(255,255,255,0.05);transition:transform .12s ease, box-shadow .12s ease}
    .touch-box:active{transform:scale(.98)}
    .touch-text{font-weight:700;letter-spacing:.6px}
    .msg{margin-top:18px;padding:16px;border-radius:10px;background:linear-gradient(180deg, rgba(6,182,212,0.06), rgba(6,182,212,0.03));color:#dff6fb;display:none;white-space:pre-line}
    .small{font-size:13px;opacity:.7;margin-top:8px}
    .fade-in{animation:fadeIn .5s ease both}
    @keyframes fadeIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:translateY(0)}}
    .confetti{position:fixed;left:0;top:0;right:0;bottom:0;pointer-events:none;overflow:hidden}
    .confetti span{position:absolute;width:8px;height:14px;border-radius:2px;opacity:0.95;transform-origin:center;animation:fall 1200ms linear forwards}
    @keyframes fall{to{transform:translateY(110vh) rotate(720deg);opacity:1}}
    .actions{display:flex;gap:8px;margin-top:12px}
    .btn{background:transparent;border:1px solid rgba(255,255,255,0.06);padding:8px 12px;border-radius:8px;font-size:13px;cursor:pointer}
  </style>
</head>
<body>
  <div class="wrap">
    <div class="card" role="region" aria-label="Ujumbe wa Motivation">
      <h1 class="title">Ujumbe wa Motivation</h1><div id="touch" class="touch-box" tabindex="0" role="button" aria-pressed="false" aria-label="Gusa hapa kuonyesha ujumbe">
    <div class="touch-text">Touch here</div>
  </div>

  <div id="msg" class="msg" aria-live="polite"></div>
  <div class="small">Gusa au bonyeza <strong>Touch here</strong> kuonyesha ujumbe. Inafaa kwenye simu pia.</div>

  <div class="actions">
    <button id="copyBtn" class="btn" title="Nakili ujumbe">Nakili ujumbe</button>
    <button id="resetBtn" class="btn" title="Funga ujumbe">Funga</button>
  </div>
</div>

  </div>  <div id="confetti" class="confetti" aria-hidden="true"></div>  <script>
    // Ujumbe wako wa motivation (badilisha hapa kama unataka)
    const message = `Ujumbe wangu kuhusu motivation:\n\nWewe ni nguvu zaidi kuliko unavyofikiri. Hatua ndogo za leo zinaweza kubadilisha kesho yako.\n\nEndelea kujifunza, kuwa ndoto yako, na usikate tamaa — mafanikio yanahitaji uvumilivu.\n\nIva msimamo, fanya kazi kwa bidii, na kumbuka: kila kosa ni somo la mafanikio.`;

    const touch = document.getElementById('touch');
    const msg = document.getElementById('msg');
    const copyBtn = document.getElementById('copyBtn');
    const resetBtn = document.getElementById('resetBtn');
    const confetti = document.getElementById('confetti');

    function showMessage(){
      msg.textContent = message;
      msg.style.display = 'block';
      msg.classList.remove('fade-in');
      // small timeout to restart animation
      requestAnimationFrame(()=> msg.classList.add('fade-in'));
      touch.setAttribute('aria-pressed','true');
      launchConfetti();
    }

    function hideMessage(){
      msg.style.display = 'none';
      touch.setAttribute('aria-pressed','false');
      confetti.innerHTML = '';
    }

    // handle both click and touch events
    touch.addEventListener('click', ()=>{
      if (msg.style.display === 'block') hideMessage(); else showMessage();
    });
    touch.addEventListener('touchstart', (e)=>{ e.preventDefault(); touch.click(); });

    copyBtn.addEventListener('click', async ()=>{
      try{
        await navigator.clipboard.writeText(message);
        copyBtn.textContent = 'Imenakiliwa!';
        setTimeout(()=> copyBtn.textContent = 'Nakili ujumbe', 1400);
      }catch(e){
        copyBtn.textContent = 'Nakili - hairuhusu';
        setTimeout(()=> copyBtn.textContent = 'Nakili ujumbe', 1400);
      }
    });

    resetBtn.addEventListener('click', hideMessage);

    // small confetti effect
    function launchConfetti(){
      confetti.innerHTML = '';
      const colors = ['#06b6d4','#60a5fa','#34d399','#f59e0b','#f97316'];
      for(let i=0;i<24;i++){
        const el = document.createElement('span');
        el.style.left = Math.random()*100 + '%';
        el.style.top = (Math.random()*10 - 10) + 'vh';
        el.style.background = colors[Math.floor(Math.random()*colors.length)];
        el.style.transform = `rotate(${Math.random()*360}deg)`;
        el.style.animationDuration = (900 + Math.random()*700) + 'ms';
        confetti.appendChild(el);
      }
      // remove after animation
      setTimeout(()=> confetti.innerHTML = '', 1800);
    }

    // accessibility: allow Enter/Space key
    touch.addEventListener('keydown',(ev)=>{
      if(ev.key === 'Enter' || ev.key === ' ') { ev.preventDefault(); touch.click(); }
    });
  </script></body>
</html>
