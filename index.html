<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Estrategias de validación: Monte Carlo vs K-Fold</title>
<style>
:root{
  --bg:#eef1f6; --card:#f7f8fb; --ink:#202124; --muted:#5f6368; --line:#dfe3ea;
  --train:#3b6ff0; --test:#fbbc04; --track:#dde1e8; --seg:#e8eaee;
  box-sizing:border-box; padding-top:env(safe-area-inset-top,0px); padding-bottom:env(safe-area-inset-bottom,0px);
}
@media (prefers-color-scheme:dark){
  :root:not([data-theme="light"]){
    --bg:#14171c; --card:#1c2027; --ink:#eceff4; --muted:#9aa3b0; --line:#2b313b;
    --train:#5b8cff; --test:#fbbc04; --track:#343a46; --seg:#2a303a;
  }
}
:root[data-theme="dark"]{
  --bg:#14171c; --card:#1c2027; --ink:#eceff4; --muted:#9aa3b0; --line:#2b313b;
  --train:#5b8cff; --test:#fbbc04; --track:#343a46; --seg:#2a303a;
}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font-family:"Google Sans","Segoe UI",Roboto,system-ui,sans-serif;padding:24px 12px}
.card{max-width:1000px;margin:0 auto;background:var(--card);border-radius:28px;border:1px solid var(--line);overflow:hidden}
.legend{display:flex;gap:24px;flex-wrap:wrap;padding:18px 28px;border-bottom:1px solid var(--line);font-size:15px;color:var(--muted)}
.legend span{display:flex;align-items:center;gap:10px}
.dot{width:20px;height:20px;border-radius:5px;display:inline-block}
.stage{padding:28px 28px 14px}
.row{display:flex;align-items:center;gap:20px;margin-bottom:22px}
.row .lbl{width:64px;flex:none;font-size:15px;color:var(--muted)}
.cells{flex:1;display:grid;grid-template-columns:repeat(var(--n),1fr);gap:4px}
.cell{aspect-ratio:3/4;max-height:46px;width:100%;border-radius:7px;background:var(--train);transition:background .35s}
.cell.t{background:var(--test)}
.axis{display:flex;justify-content:space-between;margin:-4px 0 0 84px;font-size:13px;color:var(--muted)}
.stats{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;text-align:center;padding:20px 28px;border-top:1px solid var(--line);border-bottom:1px solid var(--line);margin-top:16px}
.stats small{display:block;font-size:15px;color:var(--muted);margin-bottom:6px}
.stats b{font-size:19px;font-weight:600}
.ctrl{display:grid;grid-template-columns:1fr 1fr;gap:22px 40px;padding:26px 28px;align-items:center}
.ctrl h4{margin:0 0 12px;font-weight:500;font-size:18px;color:var(--muted)}
.seg{display:flex;background:var(--seg);border-radius:999px;padding:5px}
.seg button{flex:1;border:0;background:none;color:var(--muted);font:inherit;font-weight:600;font-size:17px;padding:12px;border-radius:999px;cursor:pointer;transition:.2s}
.seg button[aria-pressed="true"]{background:var(--train);color:#fff}
.sl{display:flex;align-items:center;gap:20px}
.sl output{min-width:36px;text-align:right;font-weight:600;font-size:17px}
input[type=range]{flex:1;accent-color:var(--train);height:6px}
.btn{border:0;background:var(--seg);color:var(--ink);font:inherit;font-weight:600;font-size:17px;padding:14px 24px;border-radius:999px;cursor:pointer;display:flex;gap:10px;align-items:center;justify-content:center}
.btn:hover{filter:brightness(.96)}
:focus-visible{outline:3px solid var(--train);outline-offset:2px}
.hint{grid-column:1/-1;margin:0;font-size:14px;color:var(--muted);border-top:1px solid var(--line);padding-top:16px}
.ctrl.off .tr{opacity:.45;pointer-events:none}
@media(max-width:700px){
  .ctrl{grid-template-columns:1fr}
  .row .lbl{width:44px;font-size:13px}.row{gap:10px}.axis{margin-left:54px}
  .stats small{font-size:13px}.stats b{font-size:16px}
  .stage,.legend,.ctrl{padding-left:16px;padding-right:16px}
  .seg button{font-size:15px}
}
</style>
</head>
<body>
<div class="card">
  <div class="legend">
    <span><i class="dot" style="background:var(--train)"></i>Entrenamiento (Train)</span>
    <span><i class="dot" style="background:var(--test)"></i>Validación / Prueba (Test)</span>
  </div>
  <div class="stage">
    <div id="rows"></div>
    <div class="axis"><span>Índice inicial [0]</span><span>Índice final [N]</span></div>
  </div>
  <div class="stats">
    <div><small>Tipo de División</small><b id="sType">Aleatorio Libre</b></div>
    <div><small>Tamaño de Test promedio</small><b id="sTest">20 %</b></div>
    <div><small>Solapamiento</small><b id="sOver">Posible / Variado</b></div>
  </div>
  <div class="ctrl" id="ctrl">
    <div>
      <h4>Estrategia de Validación</h4>
      <div class="seg">
        <button id="bMC" aria-pressed="true">Monte Carlo Split</button>
        <button id="bKF" aria-pressed="false">K-Fold CV</button>
      </div>
    </div>
    <div>
      <h4 id="itLbl">Número de Iteraciones (Splits)</h4>
      <div class="sl"><input id="iters" type="range" min="1" max="10" value="4" aria-labelledby="itLbl"><output id="iV">4</output></div>
    </div>
    <div class="tr">
      <h4>Proporción de Entrenamiento (Train Ratio)</h4>
      <div class="sl"><input id="ratio" type="range" min="50" max="95" step="5" value="80" aria-label="Proporción de entrenamiento"><output id="rV">80 %</output></div>
    </div>
    <button class="btn" id="shuffle"><svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M16 3h5v5M4 20 21 3M21 16v5h-5M15 15l6 6M4 4l5 5"/></svg>Reordenar Aleatoriamente</button>
    <p class="hint" id="hint"></p>
  </div>
</div>
<script>
(function(){
  var N = 19, mode = 'mc';
  var $ = function(id){return document.getElementById(id)};
  var rows = $('rows');

  function shuffled(){
    var a = []; for (var i=0;i<N;i++) a.push(i);
    for (var j=N-1;j>0;j--){ var k=Math.floor(Math.random()*(j+1)); var t=a[j];a[j]=a[k];a[k]=t; }
    return a;
  }

  // Cada split es un arreglo de N booleanos: true = test
  function build(){
    var k = +$('iters').value, ratio = +$('ratio').value/100, splits = [];
    if (mode === 'mc'){
      var nTest = Math.max(1, Math.round(N*(1-ratio)));
      for (var s=0;s<k;s++){
        var perm = shuffled(), m = new Array(N).fill(false);
        for (var i=0;i<nTest;i++) m[perm[i]] = true;
        splits.push(m);
      }
    } else {
      var kk = Math.max(2, k), perm2 = shuffled(), folds = [];
      for (var f=0;f<kk;f++) folds.push([]);
      perm2.forEach(function(idx,i){ folds[i%kk].push(idx); });
      for (var f2=0; f2<kk; f2++){
        var m2 = new Array(N).fill(false);
        folds[f2].forEach(function(idx){ m2[idx]=true; });
        splits.push(m2);
      }
    }
    return splits;
  }

  function overlap(splits){
    if (mode==='kf') return 'Ninguno';
    var seen = new Array(N).fill(0);
    splits.forEach(function(m){ m.forEach(function(v,i){ if(v) seen[i]++; }); });
    return seen.some(function(c){return c>1}) ? 'Posible / Variado' : 'Ninguno';
  }

  function render(){
    var splits = build(), pct;
    rows.innerHTML = '';
    splits.forEach(function(m, i){
      var r = document.createElement('div'); r.className='row';
      r.innerHTML = '<div class="lbl">'+(mode==='kf'?'Fold ':'Split ')+(i+1)+'</div>';
      var c = document.createElement('div'); c.className='cells'; c.style.setProperty('--n',N);
      m.forEach(function(v){ var d=document.createElement('div'); d.className='cell'+(v?' t':''); c.appendChild(d); });
      r.appendChild(c); rows.appendChild(r);
    });
    var avg = splits.reduce(function(a,m){return a+m.filter(Boolean).length},0)/splits.length;
    pct = Math.round(avg/N*100);
    $('sTest').textContent = pct + ' %';
    $('sType').textContent = mode==='mc' ? 'Aleatorio Libre' : 'Particiones disjuntas';
    $('sOver').textContent = overlap(splits);
    $('iV').textContent = $('iters').value;
    $('rV').textContent = $('ratio').value + ' %';
    $('hint').textContent = mode==='mc'
      ? 'Monte Carlo: en cada iteración se elige al azar una porción de los datos para test. Un mismo dato puede caer en test varias veces o ninguna.'
      : 'K-Fold: los datos se reparten en K bloques y cada bloque es test exactamente una vez. El número de iteraciones es K y el tamaño de test es 1/K.';
    $('itLbl').textContent = mode==='mc' ? 'Número de Iteraciones (Splits)' : 'Número de Folds (K)';
    $('ctrl').classList.toggle('off', mode==='kf');
  }

  function setMode(m){
    mode = m;
    $('bMC').setAttribute('aria-pressed', m==='mc');
    $('bKF').setAttribute('aria-pressed', m==='kf');
    var it = $('iters');
    if (m==='kf'){ it.min=2; if(+it.value<2) it.value=2; } else { it.min=1; }
    render();
  }

  $('bMC').onclick = function(){ setMode('mc') };
  $('bKF').onclick = function(){ setMode('kf') };
  $('iters').oninput = render;
  $('ratio').oninput = render;
  $('shuffle').onclick = render;
  render();
})();
</script>
</body>
</html>
