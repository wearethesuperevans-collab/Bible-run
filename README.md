<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport"
      content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
<title>Spiritual Power: Shadowbound</title>

<style>
*{
  box-sizing:border-box;
  -webkit-tap-highlight-color:transparent;
}

html,body{
  margin:0;
  width:100%;
  min-height:100%;
  background:#03050d;
  color:#fff;
  font-family:Inter,Arial,sans-serif;
}

body{
  overflow-x:hidden;
}

button{
  font:inherit;
  color:inherit;
}

#app{
  width:100%;
  min-height:100vh;
  display:flex;
  justify-content:center;
  background:
    radial-gradient(circle at 50% -10%,#182a55,#050814 55%,#020309);
}

#game{
  width:min(1180px,100%);
  padding:10px;
}

.topbar{
  height:58px;
  display:flex;
  align-items:center;
  justify-content:space-between;
  gap:10px;
}

.logo{
  font-size:clamp(18px,4vw,30px);
  font-weight:1000;
  letter-spacing:.08em;
  text-shadow:
    0 0 10px #52cfff,
    0 0 28px rgba(82,207,255,.45);
}

.stageLabel{
  padding:8px 13px;
  border:1px solid #40598e;
  border-radius:999px;
  background:rgba(12,21,43,.8);
  font-size:12px;
  font-weight:900;
  letter-spacing:.05em;
  white-space:nowrap;
}

/* ARENA */

#arena{
  position:relative;
  width:100%;
  aspect-ratio:16/9;
  min-height:390px;
  max-height:690px;
  overflow:hidden;
  border-radius:24px;
  border:1px solid #39527e;
  background:#050812;
  box-shadow:
    0 25px 70px rgba(0,0,0,.6),
    inset 0 0 80px rgba(0,0,0,.6);
}

#canvas{
  position:absolute;
  inset:0;
  width:100%;
  height:100%;
  display:block;
}

/* HUD */

.hud{
  position:absolute;
  z-index:20;
  top:14px;
  left:14px;
  right:14px;
  display:grid;
  grid-template-columns:1fr auto 1fr;
  gap:12px;
  pointer-events:none;
}

.hudCard{
  min-width:0;
  padding:9px 11px;
  border:1px solid rgba(137,174,230,.4);
  border-radius:14px;
  background:rgba(5,10,24,.72);
  backdrop-filter:blur(10px);
  box-shadow:0 8px 25px rgba(0,0,0,.25);
}

.hudCard.enemyCard{
  text-align:right;
}

.hudName{
  font-size:11px;
  font-weight:1000;
  letter-spacing:.08em;
  margin-bottom:5px;
}

.bar{
  position:relative;
  height:15px;
  border-radius:999px;
  background:#070a13;
  overflow:hidden;
  border:1px solid rgba(255,255,255,.25);
}

.barFill{
  height:100%;
  width:100%;
  transition:width .35s ease;
}

.playerFill{
  background:
    linear-gradient(90deg,#9e6c00,#ffd85c,#fff2a5);
  box-shadow:0 0 15px #ffd34f;
}

.enemyFill{
  background:
    linear-gradient(90deg,#731126,#f0445d,#ff9aa7);
  box-shadow:0 0 15px #f0445d;
}

.centerHud{
  align-self:start;
  text-align:center;
  min-width:120px;
}

.turnText{
  font-size:10px;
  color:#9eb7e9;
  font-weight:900;
  letter-spacing:.1em;
}

.powerText{
  margin-top:4px;
  color:#75e9ff;
  font-size:13px;
  font-weight:1000;
}

/* COMBAT MESSAGE */

.combatMessage{
  position:absolute;
  z-index:30;
  left:50%;
  bottom:18px;
  transform:translateX(-50%);
  width:min(700px,90%);
  text-align:center;
  padding:10px 16px;
  border-radius:14px;
  background:rgba(3,7,18,.74);
  border:1px solid rgba(120,170,235,.32);
  backdrop-filter:blur(10px);
  font-size:13px;
  font-weight:800;
  pointer-events:none;
  text-shadow:0 2px 5px #000;
}

/* CONTROLS */

.controls{
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:10px;
  margin-top:10px;
}

.attackButton{
  position:relative;
  min-height:70px;
  padding:10px;
  border-radius:17px;
  border:1px solid #506da8;
  background:
    linear-gradient(180deg,#263d6c,#101c39);
  box-shadow:
    inset 0 1px rgba(255,255,255,.12),
    0 6px 0 #050914,
    0 12px 25px rgba(0,0,0,.25);
  cursor:pointer;
  user-select:none;
  touch-action:manipulation;
  transition:
    transform .1s,
    filter .15s,
    border-color .15s;
}

.attackButton:active{
  transform:translateY(5px);
  box-shadow:
    inset 0 1px rgba(255,255,255,.12),
    0 2px 0 #050914;
}

.attackButton:disabled{
  opacity:.38;
  filter:grayscale(.5);
  cursor:not-allowed;
}

.attackIcon{
  display:block;
  font-size:23px;
  margin-bottom:4px;
}

.attackName{
  display:block;
  font-size:11px;
  font-weight:1000;
  letter-spacing:.05em;
}

.attackInfo{
  display:block;
  margin-top:3px;
  color:#9db4df;
  font-size:9px;
}

.special{
  border-color:#d4a932;
  background:
    linear-gradient(180deg,#55451c,#1c1730);
  box-shadow:
    inset 0 1px rgba(255,255,255,.15),
    0 6px 0 #08070d,
    0 0 25px rgba(255,205,60,.15);
}

/* BOTTOM */

.bottom{
  display:grid;
  grid-template-columns:1fr 1.6fr;
  gap:10px;
  margin-top:10px;
}

.panel{
  padding:13px;
  border-radius:16px;
  border:1px solid #293c64;
  background:rgba(7,12,26,.8);
}

.panelTitle{
  font-size:10px;
  font-weight:1000;
  letter-spacing:.12em;
  color:#7794c8;
  margin-bottom:7px;
}

.log{
  min-height:55px;
  font-size:12px;
  line-height:1.45;
}

.verse{
  color:#ffe99a;
  font-style:italic;
  line-height:1.45;
  font-size:12px;
}

.verseRef{
  margin-top:5px;
  color:#a9bce1;
  font-style:normal;
  font-weight:900;
}

/* MENU */

.overlay{
  position:fixed;
  inset:0;
  z-index:500;
  display:none;
  align-items:center;
  justify-content:center;
  padding:20px;
  background:
    radial-gradient(circle at 50% 30%,rgba(41,83,160,.25),rgba(0,0,0,.88) 65%);
  backdrop-filter:blur(10px);
}

.overlay.active{
  display:flex;
}

.menu{
  width:min(520px,100%);
  max-height:90vh;
  overflow:auto;
  padding:24px;
  border:1px solid #46659a;
  border-radius:24px;
  background:
    linear-gradient(145deg,rgba(15,28,56,.98),rgba(5,9,21,.98));
  box-shadow:
    0 30px 100px rgba(0,0,0,.7),
    inset 0 1px rgba(255,255,255,.1);
}

.menu h1{
  margin:0 0 5px;
  text-align:center;
  font-size:clamp(25px,7vw,42px);
  font-weight:1000;
  letter-spacing:.06em;
}

.menuSub{
  text-align:center;
  color:#91a9d5;
  font-size:12px;
  margin-bottom:22px;
}

.saveGrid{
  display:grid;
  gap:10px;
}

.saveSlot{
  display:flex;
  align-items:center;
  justify-content:space-between;
  gap:10px;
  padding:15px;
  border-radius:16px;
  border:1px solid #354d7d;
  background:#0b1429;
}

.saveInfo{
  min-width:0;
}

.saveName{
  font-weight:1000;
}

.saveDetails{
  color:#7892bd;
  font-size:10px;
  margin-top:4px;
}

.menuButton{
  border:1px solid #5575ae;
  border-radius:12px;
  padding:10px 14px;
  background:#1a315c;
  font-weight:900;
  cursor:pointer;
}

.deleteButton{
  background:#351827;
  border-color:#793449;
}

.customize{
  display:none;
}

.customize.active{
  display:block;
}

.field{
  margin:12px 0;
}

.field label{
  display:block;
  color:#91a9d5;
  font-size:11px;
  font-weight:900;
  margin-bottom:6px;
}

select,input{
  width:100%;
  padding:12px;
  color:#fff;
  background:#081125;
  border:1px solid #3a578d;
  border-radius:12px;
}

.bigButton{
  width:100%;
  margin-top:10px;
  padding:14px;
  border-radius:14px;
  border:1px solid #6c8ed0;
  background:linear-gradient(#31569a,#162c55);
  font-weight:1000;
  cursor:pointer;
}

/* LEVEL TRANSITION */

.levelFlash{
  position:fixed;
  inset:0;
  z-index:450;
  pointer-events:none;
  display:flex;
  align-items:center;
  justify-content:center;
  background:rgba(0,0,0,.75);
  opacity:0;
}

.levelFlash.show{
  animation:levelFlash 1.5s ease forwards;
}

.levelTitle{
  text-align:center;
  font-size:clamp(28px,8vw,70px);
  font-weight:1000;
  letter-spacing:.08em;
  text-shadow:
    0 0 20px #5adfff,
    0 0 50px #287cff;
}

@keyframes levelFlash{
  0%{opacity:0}
  20%{opacity:1}
  70%{opacity:1}
  100%{opacity:0}
}

/* MOBILE */

@media(max-width:700px){

  #game{
    padding:7px;
  }

  .topbar{
    height:48px;
  }

  .stageLabel{
    font-size:9px;
    padding:7px 9px;
  }

  #arena{
    aspect-ratio:4/3;
    min-height:390px;
    border-radius:18px;
  }

  .hud{
    top:8px;
    left:8px;
    right:8px;
    gap:6px;
  }

  .hudCard{
    padding:7px;
  }

  .hudName{
    font-size:8px;
  }

  .centerHud{
    min-width:75px;
  }

  .controls{
    grid-template-columns:repeat(2,1fr);
  }

  .attackButton{
    min-height:62px;
  }

  .bottom{
    grid-template-columns:1fr;
  }

  .combatMessage{
    bottom:9px;
    font-size:11px;
  }
}
</style>
</head>

<body>

<div id="app">

<div id="game">

  <div class="topbar">
    <div class="logo">SPIRITUAL POWER</div>
    <div class="stageLabel" id="stageLabel">
      LEVEL 1 • SHADOW DEMON
    </div>
  </div>

  <div id="arena">

    <canvas id="canvas"></canvas>

    <div class="hud">

      <div class="hudCard">
        <div class="hudName">SPIRIT WARRIOR</div>
        <div class="bar">
          <div id="playerBar" class="barFill playerFill"></div>
        </div>
      </div>

      <div class="hudCard centerHud">
        <div class="turnText" id="turnText">YOUR TURN</div>
        <div class="powerText" id="powerText">POWER 0</div>
      </div>

      <div class="hudCard enemyCard">
        <div class="hudName" id="enemyHUDName">SHADOW DEMON</div>
        <div class="bar">
          <div id="enemyBar" class="barFill enemyFill"></div>
        </div>
      </div>

    </div>

    <div class="combatMessage" id="combatMessage">
      A shadow emerges from the darkness...
    </div>

  </div>

  <div class="controls">

    <button class="attackButton" id="strike">
      <span class="attackIcon">⚡</span>
      <span class="attackName">SPIRIT STRIKE</span>
      <span class="attackInfo">Fast energy attack</span>
    </button>

    <button class="attackButton" id="shield">
      <span class="attackIcon">🛡️</span>
      <span class="attackName">SHIELD OF FATE</span>
      <span class="attackInfo">Block the next hit</span>
    </button>

    <button class="attackButton" id="truth">
      <span class="attackIcon">✋</span>
      <span class="attackName">WORD OF TRUTH</span>
      <span class="attackInfo">Powerful beam</span>
    </button>

    <button class="attackButton special" id="burst">
      <span class="attackIcon">☀️</span>
      <span class="attackName">LIGHT BURST</span>
      <span class="attackInfo">Unlock after surviving 3 turns</span>
    </button>

  </div>

  <div class="bottom">

    <div class="panel">
      <div class="panelTitle">COMBAT LOG</div>
      <div class="log" id="log">
        Prepare yourself.
      </div>
    </div>

    <div class="panel">
      <div class="panelTitle">SCRIPTURE</div>
      <div class="verse" id="verse">
        “Put on the whole armour of God, that ye may be able to stand against the wiles of the devil.”
        <div class="verseRef">Ephesians 6:11</div>
      </div>
    </div>

  </div>

</div>
</div>


<!-- SAVE MENU -->

<div class="overlay active" id="saveOverlay">

  <div class="menu">

    <h1>SHADOWBOUND</h1>

    <div class="menuSub">
      Choose your save slot
    </div>

    <div class="saveGrid" id="saveGrid"></div>

  </div>

</div>


<!-- CUSTOMIZATION -->

<div class="overlay" id="customOverlay">

  <div class="menu">

    <h1>WARRIOR</h1>

    <div class="menuSub">
      Create your spiritual warrior
    </div>

    <div class="field">

      <label>WARRIOR NAME</label>

      <input
        id="warriorName"
        maxlength="18"
        placeholder="Spirit Warrior"
      >

    </div>

    <div class="field">

      <label>GENDER</label>

      <select id="gender">
        <option value="male">Male</option>
        <option value="female">Female</option>
      </select>

    </div>

    <div class="field">

      <label>ARMOR STYLE</label>

      <select id="armor">
        <option value="light">Light Guardian</option>
        <option value="royal">Royal Guardian</option>
        <option value="celestial">Celestial Guardian</option>
      </select>

    </div>

    <button class="bigButton" id="startGame">
      BEGIN JOURNEY
    </button>

  </div>

</div>


<div class="levelFlash" id="levelFlash">

  <div class="levelTitle" id="levelTitle">
    LEVEL 2
  </div>

</div>


<script>

/* =========================================================
   SPIRITUAL POWER: SHADOWBOUND
   Full Canvas Game
========================================================= */

const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

const arena = document.getElementById("arena");

const playerBar = document.getElementById("playerBar");
const enemyBar = document.getElementById("enemyBar");

const stageLabel = document.getElementById("stageLabel");
const enemyHUDName = document.getElementById("enemyHUDName");

const turnText = document.getElementById("turnText");
const powerText = document.getElementById("powerText");

const combatMessage =
  document.getElementById("combatMessage");

const log =
  document.getElementById("log");

const verse =
  document.getElementById("verse");

const saveOverlay =
  document.getElementById("saveOverlay");

const customOverlay =
  document.getElementById("customOverlay");

const saveGrid =
  document.getElementById("saveGrid");

const levelFlash =
  document.getElementById("levelFlash");

const levelTitle =
  document.getElementById("levelTitle");

const warriorName =
  document.getElementById("warriorName");

const gender =
  document.getElementById("gender");

const armor =
  document.getElementById("armor");

const startGame =
  document.getElementById("startGame");


const buttons = {
  strike:document.getElementById("strike"),
  shield:document.getElementById("shield"),
  truth:document.getElementById("truth"),
  burst:document.getElementById("burst")
};


/* =========================================================
   GAME STATE
========================================================= */

let W = 1000;
let H = 560;

let running = false;
let busy = false;

let selectedSlot = null;

let player = {
  x:.22,
  hp:100,
  maxHP:100,
  power:0,
  turns:0,
  shield:false,
  name:"Spirit Warrior",
  gender:"male",
  armor:"light"
};

let enemy = {
  x:.78,
  hp:100,
  maxHP:100,
  level:1,
  name:"Shadow Demon"
};

let camera = {
  shake:0,
  x:0,
  y:0
};

let worldTime = 0;

let particles = [];
let effects = [];
let projectiles = [];
let floatingText = [];


/* =========================================================
   SAVE SYSTEM
========================================================= */

const SAVE_KEY =
  "ShadowboundUltimateSave_v4";


function getSaves(){

  try{

    return JSON.parse(
      localStorage.getItem(SAVE_KEY)
    ) || {};

  }catch{

    return {};

  }

}


function saveGame(){

  if(selectedSlot===null)return;

  const saves=getSaves();

  saves[selectedSlot]={
    player:{
      name:player.name,
      gender:player.gender,
      armor:player.armor
    },
    level:enemy.level,
    hp:player.hp,
    power:player.power,
    turns:player.turns
  };

  localStorage.setItem(
    SAVE_KEY,
    JSON.stringify(saves)
  );

}


function loadSave(slot){

  const saves=getSaves();

  if(!saves[slot]){

    selectedSlot=slot;

    customOverlay.classList.add("active");

    return;

  }

  selectedSlot=slot;

  const s=saves[slot];

  player.name=s.player.name;
  player.gender=s.player.gender;
  player.armor=s.player.armor;

  player.hp=s.hp;
  player.power=s.power;
  player.turns=s.turns;

  enemy.level=s.level;

  setupLevel(enemy.level);

  saveOverlay.classList.remove("active");

  running=true;

}


function deleteSave(slot){

  const saves=getSaves();

  delete saves[slot];

  localStorage.setItem(
    SAVE_KEY,
    JSON.stringify(saves)
  );

  renderSaveSlots();

}


function renderSaveSlots(){

  saveGrid.innerHTML="";

  const saves=getSaves();

  for(let i=1;i<=3;i++){

    const save=saves[i];

    const slot=document.createElement("div");

    slot.className="saveSlot";

    if(save){

      slot.innerHTML=`

        <div class="saveInfo">

          <div class="saveName">
            SAVE ${i} — ${escapeHTML(save.player.name)}
          </div>

          <div class="saveDetails">
            Level ${save.level} • ${save.player.armor} armor
          </div>

        </div>

        <div>

          <button
            class="menuButton"
            data-load="${i}">
            LOAD
          </button>

          <button
            class="menuButton deleteButton"
            data-delete="${i}">
            DELETE
          </button>

        </div>

      `;

    }else{

      slot.innerHTML=`

        <div class="saveInfo">

          <div class="saveName">
            SAVE ${i}
          </div>

          <div class="saveDetails">
            Empty slot
          </div>

        </div>

        <button
          class="menuButton"
          data-load="${i}">
          NEW GAME
        </button>

      `;

    }

    saveGrid.appendChild(slot);

  }

}


function escapeHTML(text){

  return String(text)
    .replaceAll("&","&amp;")
    .replaceAll("<","&lt;")
    .replaceAll(">","&gt;")
    .replaceAll('"',"&quot;");

}


saveGrid.addEventListener("click",e=>{

  const load=e.target.dataset.load;
  const del=e.target.dataset.delete;

  if(load){
    loadSave(Number(load));
  }

  if(del){
    deleteSave(Number(del));
  }

});


startGame.addEventListener("click",()=>{

  player.name =
    warriorName.value.trim() ||
    "Spirit Warrior";

  player.gender=gender.value;
  player.armor=armor.value;

  player.hp=100;
  player.power=0;
  player.turns=0;

  enemy.level=1;

  setupLevel(1);

  customOverlay.classList.remove("active");
  saveOverlay.classList.remove("active");

  running=true;

  saveGame();

});


/* =========================================================
   LEVELS
========================================================= */

const LEVELS={

  1:{
    name:"SHADOW DEMON",
    hp:100,
    color:"#d52e4b",
    verse:
      "“Put on the whole armour of God, that ye may be able to stand against the wiles of the devil.”",
    ref:"Ephesians 6:11"
  },

  2:{
    name:"DARK ANGEL",
    hp:145,
    color:"#9c5cff",
    verse:
      "“The LORD is my rock, and my fortress, and my deliverer; my God, my strength, in whom I will trust.”",
    ref:"Psalm 18:2"
  },

  3:{
    name:"SHADOW COLOSSUS",
    hp:230,
    color:"#ff3e6c",
    verse:
      "“Greater is he that is in you, than he that is in the world.”",
    ref:"1 John 4:4"
  }

};


function setupLevel(level){

  const data=LEVELS[level];

  enemy.level=level;
  enemy.name=data.name;
  enemy.maxHP=data.hp;
  enemy.hp=data.hp;

  player.hp=player.maxHP;

  stageLabel.textContent=
    `LEVEL ${level} • ${data.name}`;

  enemyHUDName.textContent=data.name;

  verse.innerHTML=`
    ${data.verse}
    <div class="verseRef">
      ${data.ref}
    </div>
  `;

  player.turns=0;
  player.shield=false;

  updateHUD();

}


function showLevel(title){

  levelTitle.textContent=title;

  levelFlash.classList.remove("show");

  void levelFlash.offsetWidth;

  levelFlash.classList.add("show");

}


/* =========================================================
   HUD
========================================================= */

function updateHUD(){

  playerBar.style.width=
    `${Math.max(0,player.hp/player.maxHP*100)}%`;

  enemyBar.style.width=
    `${Math.max(0,enemy.hp/enemy.maxHP*100)}%`;

  powerText.textContent=
    `POWER ${player.power}`;

}


function say(text){

  combatMessage.textContent=text;
  log.textContent=text;

}


function setButtons(enabled){

  Object.values(buttons).forEach(b=>{
    b.disabled=!enabled;
  });

  buttons.burst.disabled=
    !enabled ||
    player.turns<3;

}


/* =========================================================
   CANVAS
========================================================= */

function resize(){

  const rect=arena.getBoundingClientRect();

  const dpr=
    Math.min(window.devicePixelRatio||1,2);

  W=rect.width;
  H=rect.height;

  canvas.width=W*dpr;
  canvas.height=H*dpr;

  canvas.style.width=W+"px";
  canvas.style.height=H+"px";

  ctx.setTransform(
    dpr,0,0,dpr,0,0
  );

}


window.addEventListener("resize",resize);

resize();


/* =========================================================
   DRAWING HELPERS
========================================================= */

function lerp(a,b,t){

  return a+(b-a)*t;

}


function ease(t){

  return t<.5
    ? 4*t*t*t
    : 1-Math.pow(-2*t+2,3)/2;

}


function roundRect(x,y,w,h,r){

  ctx.beginPath();

  ctx.roundRect(
    x,y,w,h,r
  );

}


function glowCircle(x,y,r,color,alpha=1){

  ctx.save();

  ctx.globalAlpha=alpha;

  const g=ctx.createRadialGradient(
    x,y,0,
    x,y,r
  );

  g.addColorStop(0,color);
  g.addColorStop(.25,color);
  g.addColorStop(1,"transparent");

  ctx.fillStyle=g;

  ctx.beginPath();
  ctx.arc(x,y,r,0,Math.PI*2);
  ctx.fill();

  ctx.restore();

}


function line(x1,y1,x2,y2,width,color){

  ctx.save();

  ctx.strokeStyle=color;
  ctx.lineWidth=width;
  ctx.lineCap="round";

  ctx.beginPath();

  ctx.moveTo(x1,y1);
  ctx.lineTo(x2,y2);

  ctx.stroke();

  ctx.restore();

}


function limb(
  x1,y1,
  x2,y2,
  width,
  colors
){

  ctx.save();

  const angle=Math.atan2(
    y2-y1,
    x2-x1
  );

  const length=Math.hypot(
    x2-x1,
    y2-y1
  );

  ctx.translate(x1,y1);
  ctx.rotate(angle);

  const g=ctx.createLinearGradient(
    0,-width/2,
    0,width/2
  );

  g.addColorStop(0,colors[0]);
  g.addColorStop(.5,colors[1]);
  g.addColorStop(1,colors[2]);

  ctx.fillStyle=g;

  roundRect(
    0,
    -width/2,
    length,
    width,
    width/2
  );

  ctx.fill();

  ctx.strokeStyle=colors[3]||"#dcecff";
  ctx.lineWidth=2;

  ctx.stroke();

  ctx.restore();

}


/* =========================================================
   BACKGROUND
========================================================= */

function drawBackground(){

  const lv=enemy.level;

  let top="#081329";
  let bottom="#02040b";

  if(lv===2){

    top="#160c32";
    bottom="#05030d";

  }

  if(lv===3){

    top="#21091d";
    bottom="#050208";

  }

  const g=ctx.createLinearGradient(
    0,0,0,H
  );

  g.addColorStop(0,top);
  g.addColorStop(1,bottom);

  ctx.fillStyle=g;
  ctx.fillRect(0,0,W,H);


  /* moon */

  const moonX=W*.5;
  const moonY=H*.25;

  glowCircle(
    moonX,
    moonY,
    105,
    lv===3 ? "#ff365b":"#67dfff",
    .11
  );

  ctx.fillStyle=
    lv===3 ? "#3b1022":"#d8f7ff";

  ctx.globalAlpha=.9;

  ctx.beginPath();

  ctx.arc(
    moonX,
    moonY,
    36,
    0,
    Math.PI*2
  );

  ctx.fill();

  ctx.globalAlpha=1;


  /* stars */

  for(let i=0;i<70;i++){

    const x=
      (i*137.3)%W;

    const y=
      (i*71.7)%(H*.62);

    const twinkle=
      .35+
      Math.sin(worldTime*.002+i)*.25;

    ctx.globalAlpha=twinkle;

    ctx.fillStyle="#dff7ff";

    ctx.fillRect(
      x,
      y,
      1.5,
      1.5
    );

  }

  ctx.globalAlpha=1;


  /* distant mountains */

  ctx.fillStyle=
    lv===3 ? "#170916":"#0a1224";

  ctx.beginPath();

  ctx.moveTo(0,H*.67);

  for(let x=0;x<=W;x+=90){

    const y=
      H*.58+
      Math.sin(x*.011)*45+
      Math.sin(x*.027)*20;

    ctx.lineTo(x,y);

  }

  ctx.lineTo(W,H);
  ctx.lineTo(0,H);
  ctx.closePath();

  ctx.fill();


  /* ground */

  const ground=ctx.createLinearGradient(
    0,H*.73,
    0,H
  );

  ground.addColorStop(
    0,
    lv===3 ? "#170b16":"#0a1427"
  );

  ground.addColorStop(
    1,
    "#02040a"
  );

  ctx.fillStyle=ground;

  ctx.fillRect(
    0,
    H*.72,
    W,
    H*.28
  );


  /* arena lines */

  ctx.globalAlpha=.3;

  for(let i=-5;i<20;i++){

    line(
      W*.5,
      H*.73,
      W*.5+i*100,
      H,
      1,
      "#46648d"
    );

  }

  ctx.globalAlpha=1;

}


/* =========================================================
   CHARACTER POSE SYSTEM
========================================================= */

function getPlayerPose(){

  return getPose(
    false,
    playerAnimation
  );

}


function getEnemyPose(){

  return getPose(
    true,
    enemyAnimation
  );

}


let playerAnimation={
  type:"idle",
  start:0,
  duration:0
};

let enemyAnimation={
  type:"idle",
  start:0,
  duration:0
};


function animationProgress(anim){

  if(anim.duration<=0)return 0;

  return Math.min(
    1,
    Math.max(
      0,
      (performance.now()-anim.start)/anim.duration
    )
  );

}


function getPose(isEnemy,anim){

  const p=animationProgress(anim);

  let t=ease(p);

  let bodyX=0;
  let bodyY=0;
  let torso=0;

  let frontShoulder=0;
  let backShoulder=0;

  let frontElbow=0;
  let backElbow=0;

  let frontWrist=0;
  let backWrist=0;

  let frontKnee=0;
  let backKnee=0;

  if(anim.type==="strike"){

    if(p<.25){

      const q=ease(p/.25);

      bodyX=lerp(0,-18,q);
      torso=lerp(0,-.10,q);

      frontShoulder=lerp(0,-.9,q);
      frontElbow=lerp(0,.8,q);

      backShoulder=lerp(0,.35,q);

      frontKnee=lerp(0,.12,q);

    }else if(p<.55){

      const q=ease((p-.25)/.30);

      bodyX=lerp(-18,24,q);
      bodyY=lerp(0,-5,q);
      torso=lerp(-.10,.10,q);

      frontShoulder=lerp(-.9,1.05,q);
      frontElbow=lerp(.8,-.95,q);
      frontWrist=lerp(0,.4,q);

      backShoulder=lerp(.35,-.25,q);

      frontKnee=lerp(.12,-.08,q);

    }else{

      const q=ease((p-.55)/.45);

      bodyX=lerp(24,0,q);
      bodyY=lerp(-5,0,q);
      torso=lerp(.10,0,q);

      frontShoulder=lerp(1.05,0,q);
      frontElbow=lerp(-.95,0,q);
      frontWrist=lerp(.4,0,q);

      backShoulder=lerp(-.25,0,q);

      frontKnee=lerp(-.08,0,q);

    }

  }


  if(anim.type==="shield"){

    const q=ease(p);

    bodyX=
      Math.sin(p*Math.PI)*-10;

    bodyY=
      Math.sin(p*Math.PI)*-2;

    torso=
      Math.sin(p*Math.PI)*.06;

    frontShoulder=
      lerp(0,-1.05,q);

    frontElbow=
      lerp(0,-.75,q);

    frontWrist=
      lerp(0,-.25,q);

    frontKnee=
      Math.sin(p*Math.PI)*.1;

  }


  if(anim.type==="truth"){

    if(p<.45){

      const q=ease(p/.45);

      bodyY=lerp(0,-18,q);

      frontShoulder=lerp(0,-1.25,q);
      backShoulder=lerp(0,1.25,q);

      frontElbow=lerp(0,-1.0,q);
      backElbow=lerp(0,1.0,q);

    }else{

      const q=ease((p-.45)/.55);

      bodyY=lerp(-18,0,q);

      frontShoulder=lerp(-1.25,0,q);
      backShoulder=lerp(1.25,0,q);

      frontElbow=lerp(-1,0,q);
      backElbow=lerp(1,0,q);

    }

  }


  if(anim.type==="burst"){

    if(p<.32){

      const q=ease(p/.32);

      bodyY=lerp(0,12,q);
      torso=lerp(0,-.06,q);

      frontShoulder=lerp(0,-1.35,q);
      backShoulder=lerp(0,1.35,q);

      frontElbow=lerp(0,-1.3,q);
      backElbow=lerp(0,1.3,q);

      frontKnee=lerp(0,.15,q);
      backKnee=lerp(0,-.15,q);

    }else if(p<.65){

      const q=ease((p-.32)/.33);

      bodyY=lerp(12,-25,q);

      frontShoulder=lerp(-1.35,-.2,q);
      backShoulder=lerp(1.35,.2,q);

      frontElbow=lerp(-1.3,.15,q);
      backElbow=lerp(1.3,-.15,q);

      frontKnee=lerp(.15,-.08,q);
      backKnee=lerp(-.15,.08,q);

    }else{

      const q=ease((p-.65)/.35);

      bodyY=lerp(-25,0,q);

      frontShoulder=lerp(-.2,0,q);
      backShoulder=lerp(.2,0,q);

      frontElbow=lerp(.15,0,q);
      backElbow=lerp(-.15,0,q);

    }

  }


  if(anim.type==="enemyAttack"){

    if(p<.35){

      const q=ease(p/.35);

      bodyX=lerp(0,18,q);
      torso=lerp(0,.08,q);

      frontShoulder=lerp(0,1.15,q);
      frontElbow=lerp(0,-.8,q);

      frontKnee=lerp(0,-.1,q);

    }else if(p<.58){

      const q=ease((p-.35)/.23);

      bodyX=lerp(18,-22,q);

      frontShoulder=lerp(1.15,-1.1,q);
      frontElbow=lerp(-.8,1,q);

    }else{

      const q=ease((p-.58)/.42);

      bodyX=lerp(-22,0,q);

      frontShoulder=lerp(-1.1,0,q);
      frontElbow=lerp(1,0,q);

    }

  }


  return {
    bodyX,
    bodyY,
    torso,
    frontShoulder,
    backShoulder,
    frontElbow,
    backElbow,
    frontWrist,
    backWrist,
    frontKnee,
    backKnee
  };

}


/* =========================================================
   CHARACTER DRAW
========================================================= */

function drawCharacter(
  isEnemy,
  x,
  y,
  scale,
  pose
){

  ctx.save();

  ctx.translate(
    x+camera.x,
    y+camera.y
  );

  ctx.scale(
    isEnemy ? -scale:scale,
    scale
  );

  const lv=enemy.level;

  const enemyColor=
    lv===1 ? "#a51d3d":
    lv===2 ? "#6f39c4":
    "#c12d53";

  const armorColor=
    player.armor==="celestial"
      ? "#e9fbff"
      : player.armor==="royal"
        ? "#d9e7ff"
        : "#b8cae8";

  const accent=
    player.armor==="celestial"
      ? "#65eaff"
      : player.armor==="royal"
        ? "#ffd85a"
        : "#7cc7ff";


  /* shadow */

  ctx.save();

  ctx.globalAlpha=.45;

  ctx.fillStyle="#000";

  ctx.beginPath();

  ctx.ellipse(
    0,
    205,
    70,
    15,
    0,
    0,
    Math.PI*2
  );

  ctx.fill();

  ctx.restore();


  /* wings */

  if(isEnemy){

    drawWing(-30,-35,-1,enemyColor);
    drawWing(30,-35,1,enemyColor);

  }


  /* body position */

  ctx.save();

  ctx.translate(
    pose.bodyX,
    pose.bodyY
  );

  ctx.rotate(pose.torso);


  /* legs */

  drawLeg(
    -22,
    78,
    pose.frontKnee,
    false,
    isEnemy,
    armorColor
  );

  drawLeg(
    22,
    78,
    pose.backKnee,
    false,
    isEnemy,
    armorColor
  );


  /* torso */

  const torsoG=
    ctx.createLinearGradient(
      -38,0,
      38,0
    );

  if(isEnemy){

    torsoG.addColorStop(0,"#160813");
    torsoG.addColorStop(.45,enemyColor);
    torsoG.addColorStop(.7,"#2a0b25");
    torsoG.addColorStop(1,"#09050d");

  }else{

    torsoG.addColorStop(0,"#344c78");
    torsoG.addColorStop(.35,armorColor);
    torsoG.addColorStop(.5,"#ffffff");
    torsoG.addColorStop(.7,armorColor);
    torsoG.addColorStop(1,"#354a73");

  }

  ctx.fillStyle=torsoG;

  roundRect(
    -39,
    -65,
    78,
    145,
    25
  );

  ctx.fill();

  ctx.strokeStyle=
    isEnemy ? enemyColor:"#e8f4ff";

  ctx.lineWidth=3;

  ctx.stroke();


  /* shoulder armor */

  ctx.fillStyle=
    isEnemy ? "#501126":accent;

  ctx.globalAlpha=.95;

  roundRect(
    -48,
    -60,
    28,
    35,
    12
  );

  ctx.fill();

  roundRect(
    20,
    -60,
    28,
    35,
    12
  );

  ctx.fill();

  ctx.globalAlpha=1;


  /* chest core */

  const coreColor=
    isEnemy ? "#ff294f":accent;

  glowCircle(
    0,
    -25,
    38,
    coreColor,
    .16
  );

  ctx.fillStyle=
    isEnemy ? "#ff304f":"#b8fbff";

  ctx.beginPath();

  ctx.arc(
    0,
    -25,
    16,
    0,
    Math.PI*2
  );

  ctx.fill();

  ctx.strokeStyle=
    isEnemy ? "#ff9baa":"#ffffff";

  ctx.lineWidth=2;

  ctx.stroke();


  /* belt */

  ctx.fillStyle=
    isEnemy ? "#280916":"#7c5c11";

  ctx.fillRect(
    -40,
    45,
    80,
    13
  );

  ctx.fillStyle=
    isEnemy ? "#ff3657":"#ffd64e";

  ctx.beginPath();

  ctx.arc(
    0,
    51,
    8,
    0,
    Math.PI*2
  );

  ctx.fill();


  /* back arm */

  drawArm(
    -40,
    -48,
    pose.backShoulder,
    pose.backElbow,
    pose.backWrist,
    isEnemy,
    armorColor,
    accent
  );


  /* front arm */

  drawArm(
    40,
    -48,
    pose.frontShoulder,
    pose.frontElbow,
    pose.frontWrist,
    isEnemy,
    armorColor,
    accent
  );


  /* neck */

  ctx.fillStyle=
    isEnemy ? "#491326":"#bb8164";

  ctx.fillRect(
    -11,
    -80,
    22,
    25
  );


  /* head */

  if(isEnemy){

    drawDemonHead(enemyColor);

  }else{

    drawHumanHead();

  }


  ctx.restore();

  ctx.restore();

}


/* =========================================================
   LIMBS
========================================================= */

function drawLeg(
  hipX,
  hipY,
  kneeAngle,
  enemyMode,
  isEnemy,
  armorColor
){

  const thighLength=55;
  const shinLength=55;

  const a=
    hipX<0
      ? .04+kneeAngle
      : -.04+kneeAngle;

  const kneeX=
    hipX+
    Math.sin(a)*
    thighLength;

  const kneeY=
    hipY+
    Math.cos(a)*
    thighLength;

  const footAngle=
    hipX<0 ? -.04:-.04;

  const footX=
    kneeX+
    Math.sin(footAngle)*
    shinLength;

  const footY=
    kneeY+
    Math.cos(footAngle)*
    shinLength;


  limb(
    hipX,
    hipY,
    kneeX,
    kneeY,
    24,
    isEnemy
      ? ["#180914","#6b203c","#130710","#a52b49"]
      : ["#506b98","#f3f8ff","#627ba4","#dbe9ff"]
  );


  ctx.fillStyle=
    isEnemy ? "#7b2342":"#c9dbf3";

  ctx.beginPath();

  ctx.arc(
    kneeX,
    kneeY,
    13,
    0,
    Math.PI*2
  );

  ctx.fill();


  limb(
    kneeX,
    kneeY,
    footX,
    footY,
    22,
    isEnemy
      ? ["#150811","#5b1934","#10060e","#922540"]
      : ["#526e9c","#f7fbff","#5c75a0","#dbe9ff"]
  );


  ctx.fillStyle=
    isEnemy ? "#12060d":"#142544";

  roundRect(
    footX-17,
    footY-3,
    38,
    18,
    8
  );

  ctx.fill();

}


function drawArm(
  shoulderX,
  shoulderY,
  shoulderAngle,
  elbowAngle,
  wristAngle,
  isEnemy,
  armorColor,
  accent
){

  const upper=47;
  const lower=46;

  const shoulderSide=
    shoulderX<0 ? -1:1;

  const baseAngle=
    shoulderX<0 ? .25:-.25;

  const a=
    baseAngle+
    shoulderAngle;

  const elbowX=
    shoulderX+
    Math.sin(a)*
    upper;

  const elbowY=
    shoulderY+
    Math.cos(a)*
    upper;


  const b=
    a+
    elbowAngle;

  const handX=
    elbowX+
    Math.sin(b)*
    lower;

  const handY=
    elbowY+
    Math.cos(b)*
    lower;


  limb(
    shoulderX,
    shoulderY,
    elbowX,
    elbowY,
    23,
    isEnemy
      ? ["#180914","#67213b","#130710","#a42d4b"]
      : ["#506b98","#f2f7ff","#607aa3","#dcecff"]
  );


  ctx.fillStyle=
    isEnemy ? "#7e2847":"#d8e8ff";

  ctx.beginPath();

  ctx.arc(
    elbowX,
    elbowY,
    11,
    0,
    Math.PI*2
  );

  ctx.fill();

  ctx.strokeStyle=
    isEnemy ? "#a52b49":"#dbe9ff";

  ctx.lineWidth=2;

  ctx.stroke();


  limb(
    elbowX,
    elbowY,
    handX,
    handY,
    20,
    isEnemy
      ? ["#150811","#581a35","#10060e","#932642"]
      : ["#536f9b","#f6faff","#607ba5","#dbe9ff"]
  );


  /* glove / hand */

  ctx.save();

  ctx.translate(handX,handY);

  ctx.rotate(b+wristAngle);

  ctx.fillStyle=
    isEnemy ? "#531528":"#b87959";

  ctx.beginPath();

  ctx.ellipse(
    0,
    0,
    13,
    15,
    0,
    0,
    Math.PI*2
  );

  ctx.fill();

  ctx.strokeStyle=
    isEnemy ? "#a42a48":"#dcecff";

  ctx.lineWidth=2;

  ctx.stroke();


  /* fingers */

  ctx.strokeStyle=
    isEnemy ? "#9b2b4b":"#d99876";

  ctx.lineWidth=3;

  for(let i=-1;i<=1;i++){

    line(
      i*4,
      -8,
      i*4,
      -17,
      3,
      ctx.strokeStyle
    );

  }

  ctx.restore();

}


/* =========================================================
   HEADS
========================================================= */

function drawHumanHead(){

  /* hair */

  ctx.fillStyle="#182237";

  ctx.beginPath();

  ctx.arc(
    0,
    -101,
    31,
    Math.PI,
    Math.PI*2
  );

  ctx.fill();


  const skin=ctx.createLinearGradient(
    -25,-125,
    25,-75
  );

  skin.addColorStop(0,"#f0c19a");
  skin.addColorStop(.6,"#c98561");
  skin.addColorStop(1,"#754531");

  ctx.fillStyle=skin;

  ctx.beginPath();

  ctx.ellipse(
    0,
    -101,
    27,
    33,
    0,
    0,
    Math.PI*2
  );

  ctx.fill();

  ctx.strokeStyle="#dcecff";
  ctx.lineWidth=2;
  ctx.stroke();


  /* hair front */

  ctx.fillStyle="#172035";

  ctx.beginPath();

  ctx.arc(
    0,
    -120,
    28,
    Math.PI,
    Math.PI*2
  );

  ctx.fill();


  /* eyes */

  ctx.fillStyle="#18233a";

  ctx.beginPath();

  ctx.ellipse(
    -10,
    -103,
    4,
    2.5,
    0,
    0,
    Math.PI*2
  );

  ctx.ellipse(
    10,
    -103,
    4,
    2.5,
    0,
    0,
    Math.PI*2
  );

  ctx.fill();


  /* nose */

  line(
    0,-101,
    3,-93,
    2,
    "#754735"
  );


  /* mouth */

  line(
    -7,-87,
    7,-87,
    2,
    "#733d35"
  );

}


function drawDemonHead(color){

  ctx.fillStyle="#120710";

  ctx.beginPath();

  ctx.ellipse(
    0,
    -102,
    30,
    34,
    0,
    0,
    Math.PI*2
  );

  ctx.fill();


  ctx.strokeStyle=color;
  ctx.lineWidth=3;
  ctx.stroke();


  /* horns */

  ctx.fillStyle="#421226";

  ctx.beginPath();

  ctx.moveTo(-18,-128);
  ctx.lineTo(-43,-162);
  ctx.lineTo(-11,-137);
  ctx.closePath();

  ctx.fill();


  ctx.beginPath();

  ctx.moveTo(18,-128);
  ctx.lineTo(43,-162);
  ctx.lineTo(11,-137);
  ctx.closePath();

  ctx.fill();


  /* eyes */

  ctx.shadowColor="#ff3657";
  ctx.shadowBlur=15;

  ctx.fillStyle="#ff3657";

  ctx.beginPath();

  ctx.ellipse(
    -11,
    -103,
    6,
    3,
    -.15,
    0,
    Math.PI*2
  );

  ctx.ellipse(
    11,
    -103,
    6,
    3,
    .15,
    0,
    Math.PI*2
  );

  ctx.fill();

  ctx.shadowBlur=0;


  /* mouth */

  ctx.strokeStyle="#c82e4c";
  ctx.lineWidth=3;

  ctx.beginPath();

  ctx.moveTo(-12,-86);
  ctx.quadraticCurveTo(
    0,-78,
    12,-86
  );

  ctx.stroke();

}


/* =========================================================
   WINGS
========================================================= */

function drawWing(
  x,
  y,
  side,
  color
){

  ctx.save();

  ctx.translate(x,y);
  ctx.scale(side,1);

  ctx.globalAlpha=.9;

  const g=ctx.createLinearGradient(
    0,0,
    100,80
  );

  g.addColorStop(0,"#100812");
  g.addColorStop(.5,color);
  g.addColorStop(1,"#0b0610");

  ctx.fillStyle=g;

  ctx.beginPath();

  ctx.moveTo(0,0);
  ctx.quadraticCurveTo(
    90,-70,
    155,-35
  );
  ctx.quadraticCurveTo(
    115,15,
    160,70
  );
  ctx.quadraticCurveTo(
    90,45,
    100,125
  );
  ctx.quadraticCurveTo(
    55,70,
    0,95
  );

  ctx.closePath();

  ctx.fill();

  ctx.strokeStyle=color;
  ctx.lineWidth=2;
  ctx.stroke();

  ctx.globalAlpha=1;

  ctx.restore();

}


/* =========================================================
   PARTICLES
========================================================= */

function spawnParticles(
  x,
  y,
  color,
  count=20,
  power=1
){

  for(let i=0;i<count;i++){

    const angle=
      Math.random()*
      Math.PI*2;

    const speed=
      (1+Math.random()*4)*
      power;

    particles.push({

      x,
      y,

      vx:Math.cos(angle)*speed,
      vy:Math.sin(angle)*speed,

      life:.45+Math.random()*.7,
      max:.45+Math.random()*.7,

      size:1+Math.random()*4,

      color

    });

  }

}


function updateParticles(dt){

  for(let i=particles.length-1;i>=0;i--){

    const p=particles[i];

    p.x+=p.vx;
    p.y+=p.vy;

    p.vy+=.025;

    p.vx*=.985;
    p.vy*=.985;

    p.life-=dt;

    if(p.life<=0){

      particles.splice(i,1);

    }

  }

}


function drawParticles(){

  for(const p of particles){

    ctx.globalAlpha=
      Math.max(0,p.life/p.max);

    ctx.fillStyle=p.color;

    ctx.beginPath();

    ctx.arc(
      p.x,
      p.y,
      p.size,
      0,
      Math.PI*2
    );

    ctx.fill();

  }

  ctx.globalAlpha=1;

}


/* =========================================================
   EFFECTS
========================================================= */

function addEffect(effect){

  effects.push(effect);

}


function updateEffects(dt){

  for(let i=effects.length-1;i>=0;i--){

    const e=effects[i];

    e.life-=dt;

    if(e.update){
      e.update(e,dt);
    }

    if(e.life<=0){

      effects.splice(i,1);

    }

  }

}


function drawEffects(){

  for(const e of effects){

    if(e.draw){
      e.draw(e);
    }

  }

}


/* =========================================================
   PROJECTILES
========================================================= */

function fireProjectile(
  fromX,
  fromY,
  toX,
  toY,
  color,
  damage,
  big=false
){

  projectiles.push({

    x:fromX,
    y:fromY,

    startX:fromX,
    startY:fromY,

    targetX:toX,
    targetY:toY,

    progress:0,
    speed:big?.045:.075,

    color,
    damage,
    big

  });

}


function updateProjectiles(){

  for(let i=projectiles.length-1;i>=0;i--){

    const p=projectiles[i];

    p.progress+=p.speed;

    const q=ease(
      Math.min(1,p.progress)
    );

    p.x=lerp(
      p.startX,
      p.targetX,
      q
    );

    p.y=lerp(
      p.startY,
      p.targetY,
      q
    );

    if(p.progress>=1){

      spawnParticles(
        p.targetX,
        p.targetY,
        p.color,
        p.big?70:30,
        p.big?2:1
      );

      addImpact(
        p.targetX,
        p.targetY,
        p.color,
        p.big
      );

      if(p.damage){

        enemy.hp=
          Math.max(
            0,
            enemy.hp-p.damage
          );

        updateHUD();

        floatingText.push({
          x:p.targetX,
          y:p.targetY-30,
          text:"-"+p.damage,
          life:1,
          color:"#fff"
        });

      }

      projectiles.splice(i,1);

    }

  }

}


function drawProjectiles(){

  for(const p of projectiles){

    const size=
      p.big ? 22:11;

    glowCircle(
      p.x,
      p.y,
      p.big?70:40,
      p.color,
      .4
    );

    ctx.fillStyle="#fff";

    ctx.beginPath();

    ctx.arc(
      p.x,
      p.y,
      size,
      0,
      Math.PI*2
    );

    ctx.fill();

    ctx.strokeStyle=p.color;
    ctx.lineWidth=5;

    ctx.stroke();

  }

}


/* =========================================================
   IMPACT
========================================================= */

function addImpact(
  x,
  y,
  color,
  big=false
){

  addEffect({

    x,
    y,

    life:.65,
    max:.65,

    draw(e){

      const q=1-e.life/e.max;

      ctx.save();

      ctx.globalAlpha=1-q;

      ctx.strokeStyle=color;
      ctx.lineWidth=5;

      ctx.beginPath();

      ctx.arc(
        e.x,
        e.y,
        q*(big?100:55),
        0,
        Math.PI*2
      );

      ctx.stroke();

      ctx.restore();

    }

  });

  camera.shake=
    Math.max(
      camera.shake,
      big?14:7
    );

}


/* =========================================================
   BEAMS
========================================================= */

function addBeam(
  x1,
  y1,
  x2,
  y2,
  color,
  width=18
){

  addEffect({

    life:.55,
    max:.55,

    draw(e){

      const q=
        Math.min(
          1,
          (1-e.life/e.max)*2
        );

      const alpha=
        e.life<.15
          ? e.life/.15
          : 1;

      ctx.save();

      ctx.globalAlpha=alpha;

      const dx=x2-x1;
      const dy=y2-y1;

      const len=Math.hypot(dx,dy);

      const angle=Math.atan2(dy,dx);

      ctx.translate(x1,y1);
      ctx.rotate(angle);

      const g=ctx.createLinearGradient(
        0,-width,
        0,width
      );

      g.addColorStop(0,"transparent");
      g.addColorStop(.35,color);
      g.addColorStop(.5,"#fff");
      g.addColorStop(.65,color);
      g.addColorStop(1,"transparent");

      ctx.fillStyle=g;

      ctx.fillRect(
        0,
        -width*q,
        len*q,
        width*2*q
      );

      ctx.restore();

    }

  });

}


/* =========================================================
   FLOATING TEXT
========================================================= */

function updateFloatingText(dt){

  for(let i=floatingText.length-1;i>=0;i--){

    const f=floatingText[i];

    f.y-=.7;
    f.life-=dt;

    if(f.life<=0){
      floatingText.splice(i,1);
    }

  }

}


function drawFloatingText(){

  ctx.save();

  ctx.font="900 24px Arial";
  ctx.textAlign="center";

  for(const f of floatingText){

    ctx.globalAlpha=
      Math.max(0,f.life);

    ctx.fillStyle=f.color;

    ctx.shadowColor="#000";
    ctx.shadowBlur=6;

    ctx.fillText(
      f.text,
      f.x,
      f.y
    );

  }

  ctx.restore();

}


/* =========================================================
   ANIMATION LOOP
========================================================= */

let lastTime=performance.now();

function loop(now){

  const dt=
    Math.min(
      .05,
      (now-lastTime)/1000
    );

  lastTime=now;

  worldTime+=dt*1000;

  updateParticles(dt);
  updateEffects(dt);
  updateProjectiles();
  updateFloatingText(dt);

  camera.x=
    (Math.random()-.5)*
    camera.shake;

  camera.y=
    (Math.random()-.5)*
    camera.shake;

  camera.shake*=.88;

  ctx.clearRect(
    0,
    0,
    W,
    H
  );

  drawBackground();

  const playerPose=
    getPlayerPose();

  const enemyPose=
    getEnemyPose();


  /* energy behind player */

  glowCircle(
    W*player.x,
    H*.57,
    100,
    "#3edcff",
    .055
  );


  /* energy behind enemy */

  glowCircle(
    W*enemy.x,
    H*.55,
    enemy.level===3?170:110,
    LEVELS[enemy.level].color,
    .06
  );


  drawCharacter(
    false,
    W*player.x,
    H*.58,
    Math.min(W/950,1.15),
    playerPose
  );


  drawCharacter(
    true,
    W*enemy.x,
    H*.57,
    Math.min(W/950,1.15)*
      (enemy.level===3?1.35:1),
    enemyPose
  );


  drawParticles();
  drawProjectiles();
  drawEffects();
  drawFloatingText();

  requestAnimationFrame(loop);

}

requestAnimationFrame(loop);


/* =========================================================
   ANIMATION START
========================================================= */

function startPlayerAnimation(type,duration){

  playerAnimation={
    type,
    start:performance.now(),
    duration
  };

}


function startEnemyAnimation(type,duration){

  enemyAnimation={
    type,
    start:performance.now(),
    duration
  };

}


/* =========================================================
   COMBAT
========================================================= */

function getPlayerHandPosition(){

  const pose=getPlayerPose();

  const scale=
    Math.min(W/950,1.15);

  return {

    x:W*player.x+
       pose.bodyX*scale+
       90*scale,

    y:H*.58+
       pose.bodyY*scale-
       40*scale

  };

}


async function spiritStrike(){

  if(busy || !running || enemy.hp<=0)return;

  busy=true;
  setButtons(false);

  say(
    "⚡ The warrior shifts his weight and draws his arm back..."
  );

  startPlayerAnimation(
    "strike",
    1050
  );

  spawnParticles(
    W*player.x,
    H*.48,
    "#65eaff",
    18
  );

  await wait(300);

  say(
    "⚡ His hand charges with spiritual energy..."
  );

  spawnParticles(
    W*player.x+55,
    H*.50,
    "#bafaff",
    25
  );

  await wait(270);

  say("⚡ SPIRIT STRIKE!");

  const hand=
    getPlayerHandPosition();

  fireProjectile(
    hand.x,
    hand.y,
    W*enemy.x-60,
    H*.53,
    "#56ddff",
    22
  );

  await wait(650);

  finishAttack();

}


async function shieldOfFate(){

  if(busy || !running || enemy.hp<=0)return;

  busy=true;
  setButtons(false);

  say(
    "🛡️ The warrior plants his feet and raises his arm..."
  );

  startPlayerAnimation(
    "shield",
    900
  );

  await wait(380);

  say(
    "🛡️ SHIELD OF FATE!"
  );

  player.shield=true;

  addShieldEffect();

  await wait(550);

  await enemyTurn();

}


async function wordOfTruth(){

  if(busy || !running || enemy.hp<=0)return;

  busy=true;
  setButtons(false);

  say(
    "✋ The warrior raises both hands..."
  );

  startPlayerAnimation(
    "truth",
    1000
  );

  await wait(420);

  say(
    "✋ Light gathers between his hands..."
  );

  spawnParticles(
    W*player.x,
    H*.43,
    "#ffffff",
    45,
    1.2
  );

  await wait(220);

  say("✋ WORD OF TRUTH!");

  addBeam(
    W*player.x+50,
    H*.48,
    W*enemy.x-60,
    H*.48,
    "#65eaff",
    25
  );

  await wait(580);

  const damage=30;

  enemy.hp=
    Math.max(
      0,
      enemy.hp-damage
    );

  updateHUD();

  floatingText.push({
    x:W*enemy.x,
    y:H*.43,
    text:"-"+damage,
    life:1,
    color:"#bafaff"
  });

  spawnParticles(
    W*enemy.x-55,
    H*.48,
    "#65eaff",
    45,
    1.3
  );

  addImpact(
    W*enemy.x-55,
    H*.48,
    "#65eaff",
    false
  );

  await wait(500);

  finishAttack();

}


async function lightBurst(){

  if(
    busy ||
    !running ||
    enemy.hp<=0 ||
    player.turns<3
  )return;

  busy=true;
  setButtons(false);

  say(
    "☀️ The warrior crouches as his armor begins to glow..."
  );

  startPlayerAnimation(
    "burst",
    1350
  );

  spawnParticles(
    W*player.x,
    H*.52,
    "#ffe66a",
    35,
    1.5
  );

  await wait(450);

  say(
    "☀️ SPIRITUAL POWER IS SURGING!"
  );

  spawnParticles(
    W*player.x,
    H*.45,
    "#ffffff",
    55,
    1.8
  );

  await wait(330);

  say(
    "☀️ LIGHT BURST!"
  );

  addBeam(
    W*player.x+45,
    H*.45,
    W*enemy.x-50,
    H*.45,
    "#fff",
    80
  );

  addBeam(
    W*player.x+45,
    H*.45,
    W*enemy.x-50,
    H*.45,
    "#53dfff",
    42
  );

  await wait(650);

  const damage=50;

  enemy.hp=
    Math.max(
      0,
      enemy.hp-damage
    );

  updateHUD();

  floatingText.push({
    x:W*enemy.x,
    y:H*.38,
    text:"-"+damage,
    life:1.1,
    color:"#ffe77a"
  });

  spawnParticles(
    W*enemy.x,
    H*.45,
    "#ffe66a",
    90,
    2
  );

  addImpact(
    W*enemy.x,
    H*.45,
    "#ffe66a",
    true
  );

  await wait(550);

  finishAttack();

}


function finishAttack(){

  if(enemy.hp<=0){

    winLevel();

    return;

  }

  enemyTurn();

}


/* =========================================================
   ENEMY TURN
========================================================= */

async function enemyTurn(){

  await wait(350);

  if(enemy.hp<=0)return;

  turnText.textContent="ENEMY TURN";

  say(
    `👹 ${enemy.name} prepares an attack...`
  );

  startEnemyAnimation(
    "enemyAttack",
    900
  );

  await wait(390);

  say(
    `👹 ${enemy.name} strikes!`
  );

  await wait(250);

  if(player.shield){

    player.shield=false;

    say(
      "🛡️ SHIELD OF FATE BLOCKED THE ATTACK!"
    );

    addShieldImpact();

    await wait(500);

  }else{

    let damage;

    if(enemy.level===1){
      damage=8+Math.floor(Math.random()*6);
    }

    if(enemy.level===2){
      damage=11+Math.floor(Math.random()*7);
    }

    if(enemy.level===3){
      damage=14+Math.floor(Math.random()*9);
    }

    player.hp=
      Math.max(
        0,
        player.hp-damage
      );

    updateHUD();

    floatingText.push({
      x:W*player.x,
      y:H*.42,
      text:"-"+damage,
      life:1,
      color:"#ff8b9c"
    });

    spawnParticles(
      W*player.x,
      H*.52,
      "#ff4664",
      25
    );

    addImpact(
      W*player.x,
      H*.52,
      "#ff4664",
      false
    );

    say(
      `💥 ${damage} spiritual power lost.`
    );

    await wait(500);

  }

  player.turns++;

  player.power+=10;

  updateHUD();

  if(
    player.turns===3
  ){

    say(
      "🔥 SPIRITUAL POWER SURGE — LIGHT BURST UNLOCKED!"
    );

    await wait(900);

  }

  if(player.hp<=0){

    gameOver();

    return;

  }

  turnText.textContent="YOUR TURN";

  busy=false;

  setButtons(true);

  saveGame();

}


/* =========================================================
   SHIELD EFFECT
========================================================= */

function addShieldEffect(){

  addEffect({

    life:.9,
    max:.9,

    draw(e){

      const q=
        1-e.life/e.max;

      const x=W*player.x+20;
      const y=H*.48;

      ctx.save();

      ctx.translate(x,y);

      ctx.scale(
        1+q*.08,
        1+q*.08
      );

      ctx.strokeStyle=
        "#ffe66a";

      ctx.lineWidth=6;

      ctx.shadowColor="#ffe66a";
      ctx.shadowBlur=25;

      ctx.beginPath();

      ctx.arc(
        0,
        0,
        58,
        -Math.PI*.75,
        Math.PI*.75
      );

      ctx.stroke();

      ctx.restore();

    }

  });

}


function addShieldImpact(){

  addEffect({

    life:.65,
    max:.65,

    draw(e){

      const q=
        1-e.life/e.max;

      ctx.save();

      ctx.globalAlpha=1-q;

      ctx.strokeStyle="#ffe66a";
      ctx.lineWidth=7;

      ctx.beginPath();

      ctx.arc(
        W*player.x+25,
        H*.48,
        45+q*45,
        0,
        Math.PI*2
      );

      ctx.stroke();

      ctx.restore();

    }

  });

  camera.shake=10;

}


/* =========================================================
   WIN / LOSE
========================================================= */

async function winLevel(){

  busy=true;
  setButtons(false);

  say(
    `✨ ${enemy.name} has been defeated!`
  );

  spawnParticles(
    W*enemy.x,
    H*.48,
    "#ffe66a",
    120,
    2
  );

  await wait(1300);

  if(enemy.level>=3){

    showLevel("VICTORY");

    say(
      "🏆 THE SHADOWBOUND JOURNEY IS COMPLETE!"
    );

    turnText.textContent="VICTORY";

    saveGame();

    return;

  }

  const next=enemy.level+1;

  showLevel(
    `LEVEL ${next}`
  );

  await wait(600);

  setupLevel(next);

  say(
    `A new enemy enters the battlefield: ${enemy.name}!`
  );

  busy=false;

  setButtons(true);

  saveGame();

}


function gameOver(){

  busy=true;

  setButtons(false);

  turnText.textContent="DEFEATED";

  say(
    "The warrior has fallen. Reload your save to continue."
  );

  saveGame();

}


/* =========================================================
   UTILITIES
========================================================= */

function wait(ms){

  return new Promise(
    resolve=>setTimeout(resolve,ms)
  );

}


/* =========================================================
   BUTTON EVENTS
========================================================= */

buttons.strike.addEventListener(
  "click",
  spiritStrike
);

buttons.shield.addEventListener(
  "click",
  shieldOfFate
);

buttons.truth.addEventListener(
  "click",
  wordOfTruth
);

buttons.burst.addEventListener(
  "click",
  lightBurst
);


/* =========================================================
   INITIALIZATION
========================================================= */

renderSaveSlots();

setButtons(false);

say(
  "Choose a save slot to begin your journey."
);

</script>

</body>
</html>
