# glmry.stbry
<!DOCTYPE html>
<html lang="mn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>glmry.stbre | Hosuudiin shine jiliin beleg</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,600;1,500&family=Quicksand:wght@400;600;700&display=swap" rel="stylesheet">
<style>
:root{--red:#c8102e;--deep:#8f0a21;--rose:#ffe3e8;--cream:#fff8f5;--ink:#3a0a12;--gold:#e8c27a}
*{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{font-family:'Quicksand',system-ui,sans-serif;background:var(--cream);color:var(--ink);overflow-x:hidden}
h1,h2,h3,.serif{font-family:'Playfair Display',Georgia,serif}
button{font-family:inherit;cursor:pointer;border:0}
body.locked{overflow:hidden}

/* cursor glow + sparkles */
#glow{position:fixed;width:260px;height:260px;border-radius:50%;pointer-events:none;z-index:9998;
 background:radial-gradient(circle,rgba(255,60,90,.28),transparent 65%);transform:translate(-50%,-50%);transition:opacity .3s}
.spark{position:fixed;pointer-events:none;z-index:9999;font-size:14px;color:var(--gold);animation:spark .9s ease-out forwards}
@keyframes spark{to{transform:translate(var(--dx),var(--dy)) scale(.2) rotate(180deg);opacity:0}}
#stars{position:fixed;inset:0;z-index:0;pointer-events:none}

/* intro */
#intro{position:fixed;inset:0;z-index:9000;background:radial-gradient(ellipse at 50% 30%,#a30f28,#4a0510 75%);
 display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;color:#fff;transition:opacity .9s,visibility .9s}
#intro.hide{opacity:0;visibility:hidden}
#introCanvas{position:absolute;inset:0}
.intro-inner{position:relative;z-index:2;padding:20px}
.logo{width:96px;height:96px;border-radius:50%;object-fit:cover;background:#fff;border:3px solid var(--gold);margin-bottom:14px}
.intro-inner h1{font-size:clamp(34px,8vw,64px);letter-spacing:2px}
.intro-inner p{margin:10px 0 28px;opacity:.9;font-size:clamp(14px,3vw,18px)}
.enter{background:linear-gradient(135deg,#fff,var(--rose));color:var(--red);font-weight:700;font-size:18px;
 padding:14px 44px;border-radius:50px;letter-spacing:3px;box-shadow:0 0 0 0 rgba(255,255,255,.7);animation:pulse 2s infinite}
.enter:hover{transform:scale(1.06)}
@keyframes pulse{70%{box-shadow:0 0 0 22px rgba(255,255,255,0)}100%{box-shadow:0 0 0 0 rgba(255,255,255,0)}}

/* nav */
header{position:sticky;top:0;z-index:50;display:flex;align-items:center;justify-content:space-between;
 padding:12px 5vw;background:rgba(255,248,245,.9);backdrop-filter:blur(10px);border-bottom:1px solid var(--rose)}
.brand{display:flex;align-items:center;gap:10px;font-weight:700;color:var(--red);text-decoration:none;font-size:20px}
.brand img{width:42px;height:42px;border-radius:50%;object-fit:cover;background:var(--rose)}
nav{display:flex;gap:22px;align-items:center}
nav a{color:var(--ink);text-decoration:none;font-weight:600}
nav a:hover{color:var(--red)}
.cartbtn{background:var(--red);color:#fff;padding:9px 18px;border-radius:30px;font-weight:700}
.cartbtn span{background:#fff;color:var(--red);border-radius:50%;padding:1px 8px;margin-left:6px;font-size:13px}
@media(max-width:640px){nav a{display:none}}

main,footer{position:relative;z-index:1}
section{padding:70px 5vw}
.title{text-align:center;margin-bottom:34px}
.title h2{font-size:clamp(28px,5vw,42px);color:var(--deep)}
.title p{opacity:.7;margin-top:6px}
.title::after{content:"✦ ✦ ✦";display:block;color:var(--red);letter-spacing:8px;margin-top:10px;font-size:12px}

/* hero */
.hero{min-height:84vh;display:grid;place-items:center;text-align:center;
 background:radial-gradient(circle at 20% 20%,var(--rose),transparent 50%),radial-gradient(circle at 85% 80%,#ffd1d9,transparent 45%)}
.badge{display:inline-block;background:var(--red);color:#fff;padding:6px 18px;border-radius:30px;font-size:13px;letter-spacing:2px;font-weight:700}
.hero h2{font-size:clamp(38px,9vw,84px);line-height:1.05;margin:18px 0;color:var(--deep)}
.hero h2 em{color:var(--red)}
.hero p{max-width:520px;margin:0 auto 28px;font-size:18px;opacity:.8}
.btn{display:inline-block;background:var(--red);color:#fff;padding:14px 34px;border-radius:40px;font-weight:700;text-decoration:none;
 box-shadow:0 10px 24px rgba(200,16,46,.3);transition:.25s}
.btn:hover{transform:translateY(-3px);background:var(--deep)}
.btn.ghost{background:#fff;color:var(--red);box-shadow:none;border:2px solid var(--red);margin-left:10px}

/* filters + products */
.filters{display:flex;gap:10px;justify-content:center;flex-wrap:wrap;margin-bottom:12px}
.filters input{padding:11px 18px;border-radius:30px;border:2px solid var(--rose);min-width:220px;font:inherit;outline:0}
.filters input:focus{border-color:var(--red)}
.chip{background:#fff;color:var(--red);border:2px solid var(--rose);padding:9px 18px;border-radius:30px;font-weight:700}
.chip.on,.chip:hover{background:var(--red);color:#fff;border-color:var(--red)}
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(230px,1fr));gap:24px;margin-top:28px}
.card{background:#fff;border-radius:22px;overflow:hidden;box-shadow:0 8px 28px rgba(143,10,33,.08);transition:.3s;display:flex;flex-direction:column}
.card:hover{transform:translateY(-8px);box-shadow:0 18px 40px rgba(143,10,33,.18)}
.pic{height:200px;display:grid;place-items:center;font-size:84px;background:linear-gradient(135deg,var(--rose),#fff);position:relative}
.pic img{width:100%;height:100%;object-fit:cover;position:absolute;inset:0}
.tag{position:absolute;top:12px;left:12px;background:var(--red);color:#fff;font-size:12px;font-weight:700;padding:4px 12px;border-radius:20px;z-index:2}
.info{padding:18px;display:flex;flex-direction:column;gap:6px;flex:1}
.info h3{font-size:19px}
.info small{opacity:.65}
.price{font-weight:700;color:var(--red);font-size:20px;margin-top:auto}
.add{margin-top:8px;background:var(--rose);color:var(--red);padding:11px;border-radius:14px;font-weight:700;transition:.2s}
.add:hover{background:var(--red);color:#fff}
.empty{text-align:center;opacity:.6;margin-top:30px;display:none}

/* about */
.why{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:20px;max-width:1000px;margin:auto}
.why div{background:#fff;border-radius:20px;padding:26px;text-align:center;border:1px solid var(--rose)}
.why b{font-size:38px;display:block;margin-bottom:8px}

/* order */
.orderbox{max-width:620px;margin:auto;background:#fff;border-radius:26px;padding:32px;box-shadow:0 12px 40px rgba(143,10,33,.1)}
.orderbox label{display:block;font-weight:700;margin:14px 0 6px}
.orderbox input,.orderbox textarea{width:100%;padding:12px 16px;border:2px solid var(--rose);border-radius:14px;font:inherit;outline:0}
.orderbox input:focus,.orderbox textarea:focus{border-color:var(--red)}
.orderbox .btn{width:100%;margin-top:20px;text-align:center}
#note{margin-top:14px;font-size:14px;color:var(--deep);white-space:pre-line}

footer{background:var(--deep);color:#fff;text-align:center;padding:40px 5vw}
footer a{color:var(--gold);text-decoration:none;margin:0 10px}

/* cart drawer */
#shade{position:fixed;inset:0;background:rgba(0,0,0,.45);z-index:100;opacity:0;visibility:hidden;transition:.3s}
#drawer{position:fixed;top:0;right:0;height:100%;width:min(400px,100%);background:#fff;z-index:101;transform:translateX(100%);
 transition:.35s;display:flex;flex-direction:column}
body.cartopen #shade{opacity:1;visibility:visible}
body.cartopen #drawer{transform:none}
.dh{padding:20px;display:flex;justify-content:space-between;align-items:center;border-bottom:1px solid var(--rose)}
.dh button{background:none;font-size:26px;color:var(--red)}
#items{flex:1;overflow:auto;padding:14px 20px}
.row{display:flex;gap:12px;align-items:center;padding:12px 0;border-bottom:1px dashed var(--rose)}
.row .e{font-size:34px}
.row .n{flex:1;font-weight:700;font-size:15px}
.row .n small{display:block;color:var(--red)}
.qty{display:flex;gap:8px;align-items:center}
.qty button{width:26px;height:26px;border-radius:50%;background:var(--rose);color:var(--red);font-weight:700}
.df{padding:20px;border-top:1px solid var(--rose)}
.total{display:flex;justify-content:space-between;font-size:20px;font-weight:700;margin-bottom:14px}
.df .btn{width:100%;text-align:center;border:0}
.toast{position:fixed;bottom:26px;left:50%;transform:translate(-50%,120px);background:var(--ink);color:#fff;padding:12px 24px;border-radius:30px;z-index:200;transition:.4s}
.toast.show{transform:translate(-50%,0)}
@media(hover:none){#glow{display:none}}
</style>
</head>
<body class="locked">

<canvas id="stars"></canvas>
<div id="glow"></div>

<!-- INTRO -->
<div id="intro">
  <canvas id="introCanvas"></canvas>
  <div class="intro-inner">
    <img class="logo" src="logo.png" alt="logo" onerror="this.style.display='none'">
    <h1 class="serif">glmry.stbre</h1>
    <p>Hosuudiin shine jiliin beleg ✦ Hairtai hunddee tusgai beleg</p>
    <button class="enter" id="enterBtn">ENTER</button>
  </div>
</div>

<header>
  <a class="brand" href="#top"><img src="logo.png" alt="" onerror="this.style.display='none'"><span class="serif">glmry.stbre</span></a>
  <nav>
    <a href="#shop">Beleg</a><a href="#why">Bidnii tuhai</a><a href="#order">Zahialga</a>
    <button class="cartbtn" id="openCart">🛒 Sags<span id="count">0</span></button>
  </nav>
</header>

<main id="top">
  <section class="hero">
    <div>
      <span class="badge">NEW YEAR 2027 COLLECTION</span>
      <h2 class="serif">Shine jil, <em>hosuud</em><br>beleg hamt</h2>
      <p>Belen baigaa, saihan baglaatai hosuudiin beleg. Songood, zahialaad l dugaarlah.</p>
      <a class="btn" href="#shop">Beleg harah</a><a class="btn ghost" href="#order">Zahialah</a>
    </div>
  </section>

  <section id="shop">
    <div class="title"><h2>Belgiin tsuglulga</h2><p>Hosuudad zoriulsan belen shine jiliin beleg</p></div>
    <div class="filters">
      <input id="q" placeholder="🔍 Hailt...">
      <button class="chip on" data-c="all">Buh</button>
      <button class="chip" data-c="set">Set</button>
      <button class="chip" data-c="matching">Hos ni</button>
      <button class="chip" data-c="sweet">Amtlag</button>
      <button class="chip" data-c="cute">Cute</button>
    </div>
    <div class="grid" id="grid"></div>
    <p class="empty" id="empty">Oldsongui. Gesen bas ugee oroltsood uzeerei ✦</p>
  </section>

  <section id="why">
    <div class="title"><h2>Yagaad glmry.stbre?</h2></div>
    <div class="why">
      <div><b>🎁</b>Zahialga 10-15 honogt</div>
      <div><b>💌</b>Hairiin zurvas</div>
      <div><b>🚚</b>Hurgelt</div>
      <div><b>✨</b>Luxury but cute</div>
    </div>
  </section>

  <section id="order">
    <div class="title"><h2>Zahialga ogoh</h2><p>Sagsand nemeed medeeleleе uldeene uu</p></div>
    <div class="orderbox">
      <label>Ner</label><input id="oName" placeholder="Taniy ner">
      <label>Utas</label><input id="oPhone" placeholder="99xx xxxx">
      <label>Hayag</label><textarea id="oAddr" rows="2" placeholder="Hurgelt hayag"></textarea>
      <button class="btn" id="sendOrder">Zahialga batalgaajuulah</button>
      <div id="note"></div>
    </div>
  </section>
</main>

<footer>
  <h3 class="serif" style="font-size:26px">glmry.stbre</h3>
  <p style="margin:10px 0 16px;opacity:.8">Hosuudiin shine jiliin beleg ✦ 2027</p>
  <a href="https://facebook.com/" target="_blank" rel="noopener">Бадамсамбуу Мөнх-Осор</a>
  <a href="https://instagram.com/" target="_blank" rel="noopener">batuka_0722</a>
  <p style="margin-top:18px;font-size:13px;opacity:.6">© glmry.stbre</p>
</footer>

<div id="shade"></div>
<aside id="drawer">
  <div class="dh"><h3 class="serif">Taniy sags</h3><button id="closeCart">×</button></div>
  <div id="items"></div>
  <div class="df">
    <div class="total"><span>Niit</span><span id="total">0₮</span></div>
    <a class="btn" href="#order" id="toOrder">Zahialah</a>
  </div>
</aside>
<div class="toast" id="toast"></div>

<script>
/* ===== BELGIIN JAGSAALT: ene hesgiig zasaad shineer beleg nemne =====
   img: "images/ner.jpg" gej zurgiin zam ogvol emoji-iin orond zurag garna */
const PRODUCTS=[
 {id:1,name:"Red Love Set",desc:"Hos kruzh + saihan baglaa",price:59000,cat:["set","matching"],e:"🎁",tag:"HIT"},
 {id:2,name:"Matching Pajama",desc:"Hosuudiin ulaan pijaam",price:89000,cat:["matching","cute"],e:"🧸",tag:""},
 {id:3,name:"Sweet Box",desc:"Shokolad, amtlag, kart",price:45000,cat:["sweet","set"],e:"🍫",tag:"NEW"},
 {id:4,name:"Couple Keychain",desc:"Hos tulhuuriin ehnuud",price:15000,cat:["matching","cute"],e:"🔑",tag:""},
 {id:5,name:"Candle & Rose",desc:"Anhuuny teeg + hunkhuun",price:38000,cat:["set"],e:"🕯️",tag:""},
 {id:6,name:"Teddy Bear Hug",desc:"Tom nuudtei hurmen",price:72000,cat:["cute"],e:"🐻",tag:"HIT"},
 {id:7,name:"Mini Cake Box",desc:"Bento torgon, 2 hunii",price:32000,cat:["sweet"],e:"🍰",tag:""},
 {id:8,name:"Love Letter Kit",desc:"Zurvas, tamga, zurag",price:25000,cat:["cute","set"],e:"💌",tag:"NEW"}
];

/* ===== ZAHIALGA GMAIL-RUU: ene 2-iig zasna =====
   ORDER_ENDPOINT: formspree.io deer shine form uusgeed ugsun link (jishee: https://formspree.io/f/abcdwxyz)
   ORDER_EMAIL: Gmail hayag (Formspree hiigeegui ued mail app neegdeed ilgeene) */
const ORDER_ENDPOINT="https://formspree.io/f/xoedwpjr";
const ORDER_EMAIL="badamsambuumunkhosor@gmail.com";

const fmt=n=>n.toLocaleString('en-US')+'₮';
let cart=[];try{cart=JSON.parse(localStorage.getItem('glmry-cart')||'[]')}catch(e){}
const save=()=>{try{localStorage.setItem('glmry-cart',JSON.stringify(cart))}catch(e){}};
const $=s=>document.querySelector(s);

/* ===== render products ===== */
let cat='all',query='';
function render(){
 const list=PRODUCTS.filter(p=>(cat==='all'||p.cat.includes(cat))&&(p.name+p.desc).toLowerCase().includes(query));
 $('#grid').innerHTML=list.map(p=>`
  <div class="card">
   <div class="pic">${p.tag?`<span class="tag">${p.tag}</span>`:''}${p.img?`<img src="${p.img}" alt="${p.name}">`:p.e}</div>
   <div class="info"><h3 class="serif">${p.name}</h3><small>${p.desc}</small>
    <div class="price">${fmt(p.price)}</div>
    <button class="add" data-id="${p.id}">+ Sagsand nemeh</button></div>
  </div>`).join('');
 $('#empty').style.display=list.length?'none':'block';
}
$('#q').oninput=e=>{query=e.target.value.toLowerCase();render()};
document.querySelectorAll('.chip').forEach(c=>c.onclick=()=>{
 document.querySelectorAll('.chip').forEach(x=>x.classList.remove('on'));c.classList.add('on');cat=c.dataset.c;render()});
$('#grid').onclick=e=>{const b=e.target.closest('.add');if(b){addCart(+b.dataset.id)}};

/* ===== cart ===== */
function toast(t){const el=$('#toast');el.textContent=t;el.classList.add('show');setTimeout(()=>el.classList.remove('show'),1600)}
function addCart(id){const it=cart.find(c=>c.id===id);it?it.q++:cart.push({id,q:1});save();drawCart();toast('Sagsand nemlee ✦')}
function drawCart(){
 const rows=cart.map(c=>{const p=PRODUCTS.find(x=>x.id===c.id);return `
  <div class="row"><div class="e">${p.e}</div>
   <div class="n">${p.name}<small>${fmt(p.price*c.q)}</small></div>
   <div class="qty"><button data-m="${p.id}">−</button>${c.q}<button data-p="${p.id}">+</button></div></div>`}).join('');
 $('#items').innerHTML=rows||'<p style="text-align:center;opacity:.6;margin-top:40px">Sags hooson baina 🎀</p>';
 $('#count').textContent=cart.reduce((a,c)=>a+c.q,0);
 $('#total').textContent=fmt(cart.reduce((a,c)=>a+c.q*PRODUCTS.find(x=>x.id===c.id).price,0));
}
$('#items').onclick=e=>{
 const m=e.target.dataset.m,p=e.target.dataset.p;
 if(p)cart.find(c=>c.id==p).q++;
 if(m){const it=cart.find(c=>c.id==m);it.q--;if(it.q<=0)cart=cart.filter(c=>c!==it)}
 save();drawCart()};
const setCart=o=>document.body.classList.toggle('cartopen',o);
$('#openCart').onclick=()=>setCart(true);$('#closeCart').onclick=()=>setCart(false);
$('#shade').onclick=()=>setCart(false);$('#toOrder').onclick=()=>setCart(false);

/* ===== order ===== */
$('#sendOrder').onclick=()=>{
 const n=$('#oName').value.trim(),ph=$('#oPhone').value.trim(),a=$('#oAddr').value.trim();
 if(!cart.length)return toast('Sagsand beleg nemne uu');
 if(!n||!ph||!a)return toast('Buh talbaraa buglunu uu');
 const lines=cart.map(c=>{const p=PRODUCTS.find(x=>x.id===c.id);return `• ${p.name} x${c.q} = ${fmt(p.price*c.q)}`}).join('\n');
 const total=cart.reduce((s,c)=>s+c.q*PRODUCTS.find(x=>x.id===c.id).price,0);
 const msg=`Zahialga - glmry.stbre\nNer: ${n}\nUtas: ${ph}\nHayag: ${a}\n${lines}\nNiit: ${fmt(total)}`;
 const btn=$('#sendOrder');
 if(ORDER_ENDPOINT){
  btn.disabled=true;btn.textContent='Ilgeej baina...';
  fetch(ORDER_ENDPOINT,{method:'POST',headers:{'Content-Type':'application/json','Accept':'application/json'},
   body:JSON.stringify({name:n,phone:ph,address:a,order:lines,total:fmt(total),message:msg})})
  .then(r=>{if(!r.ok)throw 0;cart=[];save();drawCart();$('#note').textContent='Zahialga amjilttai ilgeegdlee ✦ Bid tantai udahgui holbogdono.'})
  .catch(()=>{$('#note').textContent='Ilgeehed aldaa garlaa. Dahin oroldono uu.'})
  .finally(()=>{btn.disabled=false;btn.textContent='Zahialga batalgaajuulah'});
 }else{
  location.href='mailto:'+ORDER_EMAIL+'?subject='+encodeURIComponent('Zahialga - glmry.stbre')+'&body='+encodeURIComponent(msg);
 }
};

/* ===== intro: falling stars ===== */
function starfield(cv,count,speed,color){
 const x=cv.getContext('2d');let W,H,S=[];
 const size=()=>{W=cv.width=innerWidth;H=cv.height=innerHeight};size();addEventListener('resize',size);
 const mk=(top)=>({x:Math.random()*W,y:top?Math.random()*H:-20,r:Math.random()*3+1,v:(Math.random()*1+.5)*speed,w:Math.random()*2*Math.PI});
 for(let i=0;i<count;i++)S.push(mk(true));
 (function loop(){
  x.clearRect(0,0,W,H);
  S.forEach((s,i)=>{
   s.y+=s.v;s.w+=.03;s.x+=Math.sin(s.w)*.5;
   if(s.y>H+20)S[i]=mk(false);
   x.save();x.translate(s.x,s.y);x.rotate(s.w);x.fillStyle=color;x.globalAlpha=.55+.4*Math.sin(s.w*2);
   x.beginPath();for(let k=0;k<5;k++){x.lineTo(Math.cos((18+k*72)/180*Math.PI)*s.r*2.4,-Math.sin((18+k*72)/180*Math.PI)*s.r*2.4);
    x.lineTo(Math.cos((54+k*72)/180*Math.PI)*s.r,-Math.sin((54+k*72)/180*Math.PI)*s.r)}
   x.closePath();x.fill();x.restore()});
  requestAnimationFrame(loop)})();
}
starfield($('#introCanvas'),70,2.2,'#ffe9a8');
starfield($('#stars'),22,.9,'rgba(200,16,46,.45)');

$('#enterBtn').onclick=()=>{$('#intro').classList.add('hide');document.body.classList.remove('locked')};

/* ===== mouse follow: glow + sparkles ===== */
const glow=$('#glow');let last=0;
addEventListener('mousemove',e=>{
 glow.style.left=e.clientX+'px';glow.style.top=e.clientY+'px';
 const t=performance.now();if(t-last<45)return;last=t;
 const s=document.createElement('div');s.className='spark';s.textContent=['✦','♥','✧','b','m'][Math.random()*3|0];
 s.style.left=e.clientX+'px';s.style.top=e.clientY+'px';
 s.style.setProperty('--dx',(Math.random()*40-20)+'px');s.style.setProperty('--dy',(Math.random()*40+10)+'px');
 if(Math.random()>.5)s.style.color='#ff3b5c';
 document.body.appendChild(s);setTimeout(()=>s.remove(),900)});

render();drawCart();
</script>
</body>
</html>
