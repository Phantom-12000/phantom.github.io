<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Tapper</title>
    <style>
        *{margin:0;padding:0;box-sizing:border-box;user-select:none;-webkit-tap-highlight-color:transparent}
        body{background:linear-gradient(135deg,#1a1a2e,#16213e);min-height:100vh;font-family:'Segoe UI',sans-serif;color:#fff;padding:16px}
        .container{max-width:500px;margin:0 auto}
        .stats{background:rgba(255,255,255,0.1);border-radius:20px;padding:16px;margin-bottom:20px}
        .stat-item{display:flex;justify-content:space-between;margin-bottom:12px;font-size:18px}
        .stat-value{font-weight:bold;font-size:24px;color:#ffd700}
        .energy-bar{background:rgba(255,255,255,0.2);border-radius:10px;height:8px;margin-top:8px}
        .energy-fill{background:linear-gradient(90deg,#00ff87,#60efff);width:100%;height:100%;border-radius:10px;transition:width .3s}
        .tap-button{background:radial-gradient(circle at 30% 30%,#ffd700,#ff8c00);width:200px;height:200px;border-radius:50%;margin:30px auto;display:flex;align-items:center;justify-content:center;cursor:pointer;box-shadow:0 20px 40px rgba(0,0,0,0.3),0 0 0 10px rgba(255,215,0,0.3)}
        .tap-button:active{transform:scale(0.95)}
        .tap-emoji{font-size:80px}
        .tap-bonus{position:fixed;pointer-events:none;font-size:24px;font-weight:bold;color:#ffd700;animation:floatUp 1s forwards;z-index:1000}
        @keyframes floatUp{0%{opacity:1;transform:translateY(0)}100%{opacity:0;transform:translateY(-100px)scale(1.5)}}
        .bottom-nav{position:fixed;bottom:0;left:0;right:0;background:rgba(0,0,0,0.9);display:flex;justify-content:space-around;padding:12px 16px;border-top:1px solid rgba(255,255,255,0.1)}
        .nav-item{text-align:center;padding:8px;border-radius:12px;cursor:pointer;flex:1}
        .nav-item.active{background:rgba(255,215,0,0.2)}
        .nav-icon{font-size:24px;display:block}
        .nav-label{font-size:12px}
        .panel{display:none;margin-bottom:80px}
        .panel.active{display:block}
        .boost-item{background:rgba(255,255,255,0.1);border-radius:16px;padding:16px;margin-bottom:12px;display:flex;justify-content:space-between;align-items:center;cursor:pointer}
        .boost-price{color:#ffd700;font-weight:bold}
        .rating-item{display:flex;justify-content:space-between;padding:12px;border-bottom:1px solid rgba(255,255,255,0.1)}
        .shake{animation:shake .2s}
        @keyframes shake{0%,100%{transform:translateX(0)}25%{transform:translateX(-5px)}75%{transform:translateX(5px)}}
    </style>
</head>
<body>
<div class="container">
    <div class="stats">
        <div class="stat-item"><span>💰 Монеты</span><span class="stat-value" id="coins">0</span></div>
        <div class="stat-item"><span>⚡ Энергия</span><span class="stat-value" id="energy">100</span></div>
        <div class="energy-bar"><div class="energy-fill" id="energyFill"></div></div>
        <div class="stat-item"><span>💪 Сила тапа</span><span class="stat-value" id="tapPower">1</span></div>
    </div>
    <div id="gamePanel" class="panel active">
        <div class="tap-button" id="tapButton"><span class="tap-emoji">💎</span></div>
        <div style="text-align:center"><p>👇 Тапай!</p><p>+<span id="tapReward">1</span> монет</p></div>
    </div>
    <div id="boostsPanel" class="panel"><h3>📈 Улучшения</h3><div id="boostsList"></div></div>
    <div id="statsPanel" class="panel"><h3>📊 Статистика</h3>
        <div class="stat-item"><span>Всего тапов:</span><span id="totalTaps">0</span></div>
        <div class="stat-item"><span>Всего заработано:</span><span id="totalEarned">0</span></div>
        <div class="stat-item"><span>Авто-тап/сек:</span><span id="autoTap">0</span></div>
        <div class="stat-item"><span>Крит шанс:</span><span id="critChance">0%</span></div>
    </div>
    <div id="ratingPanel" class="panel"><h3>🏆 Топ</h3><div id="ratingList"></div></div>
</div>
<div class="bottom-nav">
    <div class="nav-item active" data-panel="game"><span class="nav-icon">🔨</span><span class="nav-label">Игра</span></div>
    <div class="nav-item" data-panel="boosts"><span class="nav-icon">📈</span><span class="nav-label">Бусты</span></div>
    <div class="nav-item" data-panel="stats"><span class="nav-icon">📊</span><span class="nav-label">Статистика</span></div>
    <div class="nav-item" data-panel="rating"><span class="nav-icon">🏆</span><span class="nav-label">Рейтинг</span></div>
</div>
<script src="https://telegram.org/js/telegram-web-app.js"></script>
<script>
const tg=window.Telegram.WebApp;tg.expand();tg.ready();
let p={coins:100,energy:100,maxEnergy:100,totalTaps:0,totalEarned:0,boosts:{tapPower:0,energyLimit:0,autoTap:0,critChance:0},lastEnergyUpdate:Date.now()};
const B={tapPower:{name:"💪 Усиление",baseCost:100,effect:1,max:10,desc:"+1 монета"},energyLimit:{name:"⚡ Лимит",baseCost:80,effect:10,max:20,desc:"+10 энергии"},autoTap:{name:"🤖 Авто-тап",baseCost:200,effect:1,max:5,desc:"+1/сек"},critChance:{name:"🎯 Крит",baseCost:150,effect:5,max:10,desc:"+5% шанс"}};
function load(){const s=localStorage.getItem('tapper');if(s){Object.assign(p,JSON.parse(s));p.lastEnergyUpdate=Date.now()}updE();}
function save(){localStorage.setItem('tapper',JSON.stringify(p));}
function updE(){const n=Date.now(),s=(n-p.lastEnergyUpdate)/1000,m=p.maxEnergy+p.boosts.energyLimit*10;let e=p.energy+s;if(e>m)e=m;p.energy=e;p.maxEnergy=m;p.lastEnergyUpdate=n;updUI();}
function tap(){if(p.energy<1){showMsg("❌ Нет энергии!","#ff4444");return}let r=1+p.boosts.tapPower;const c=p.boosts.critChance*5,isCrit=Math.random()*100<c;if(isCrit)r*=2;p.energy-=1;p.coins+=r;p.totalTaps++;p.totalEarned+=r;showMsg(isCrit?`КРИТ! +${r}`:`+${r}`,isCrit?"#ff4444":"#ffd700");document.getElementById('tapButton').classList.add('shake');setTimeout(()=>document.getElementById('tapButton').classList.remove('shake'),200);updUI();save();}
function showMsg(t,c){const d=document.createElement('div');d.className='tap-bonus';d.textContent=t;d.style.color=c;d.style.left=Math.random()*(window.innerWidth-100)+50+'px';d.style.top=window.innerHeight*0.4+'px';document.body.appendChild(d);setTimeout(()=>d.remove(),1000);}
function buy(bid){const b=B[bid],l=p.boosts[bid];if(l>=b.max){tg.showAlert("Максимум!");return}const cost=b.baseCost*(l+1);if(p.coins<cost){tg.showAlert(`Нужно ${cost} монет!`);return}p.coins-=cost;p.boosts[bid]++;updUI();save();tg.showAlert(`Куплен ${b.name}! Уровень ${p.boosts[bid]}`);}
function auto(){if(p.boosts.autoTap>0){p.coins+=p.boosts.autoTap;p.totalEarned+=p.boosts.autoTap;updUI();save()}}
function updUI(){document.getElementById('coins').innerText=Math.floor(p.coins);document.getElementById('energy').innerText=Math.floor(p.energy);document.getElementById('tapPower').innerText=1+p.boosts.tapPower;document.getElementById('tapReward').innerText=1+p.boosts.tapPower;document.getElementById('energyFill').style.width=(p.energy/p.maxEnergy*100)+'%';document.getElementById('totalTaps').innerText=p.totalTaps;document.getElementById('totalEarned').innerText=Math.floor(p.totalEarned);document.getElementById('autoTap').innerText=p.boosts.autoTap;document.getElementById('critChance').innerText=(p.boosts.critChance*5)+'%';const c=document.getElementById('boostsList');if(c){c.innerHTML='';for(const[id,b]of Object.entries(B)){const l=p.boosts[id],cost=b.baseCost*(l+1),d=document.createElement('div');d.className='boost-item';d.onclick=()=>buy(id);d.innerHTML=`<div><h4>${b.name} ${l}/${b.max}</h4><p>${b.desc}</p></div><div class="boost-price">${l>=b.max?'🔒 MAX':cost+' 💰'}</div>`;c.appendChild(d)}}}
function updRating(){const r=[{name:"👑 Вы",coins:p.coins},{name:"🐹 Игрок 1",coins:p.coins*0.8},{name:"🦊 Игрок 2",coins:p.coins*0.6}];r.sort((a,b)=>b.coins-a.coins);const c=document.getElementById('ratingList');if(c){c.innerHTML='';r.forEach((x,i)=>{const d=document.createElement('div');d.className='rating-item';d.innerHTML=`<span>${i===0?'🥇':i===1?'🥈':'🥉'} ${i+1}. ${x.name}</span><span>💰 ${Math.floor(x.coins)}</span>`;c.appendChild(d)})}}
function switchPanel(n){['game','boosts','stats','rating'].forEach(p=>{document.getElementById(`${p}Panel`).classList.toggle('active',p===n);document.querySelector(`.nav-item[data-panel="${p}"]`).classList.toggle('active',p===n);if(p==='rating'&&p===n)updRating()})}
load();setInterval(()=>{updE();auto()},1000);document.getElementById('tapButton').onclick=tap;document.querySelectorAll('.nav-item').forEach(i=>i.onclick=()=>switchPanel(i.dataset.panel));tg.MainButton.setText("🔨 Тапай!");tg.MainButton.onClick(tap);tg.MainButton.show();
</script>
</body>
</html>
