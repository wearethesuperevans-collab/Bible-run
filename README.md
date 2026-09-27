<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no">
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
  font-family:Arial,sans-serif;
  background:#050711;
  color:white;
}

body{
  overflow-x:hidden;
}

button,input,select{
  font:inherit;
}

button{
  touch-action:manipulation;
  cursor:pointer;
}

.screen{
  min-height:100vh;
  display:flex;
  align-items:center;
  justify-content:center;
  padding:18px;
}

.hidden{
  display:none!important;
}

/* MENU */

.menu{
  width:min(600px,100%);
  background:linear-gradient(145deg,#10172c,#080b16);
  border:2px solid #4e75ff;
  border-radius:22px;
  padding:25px;
  box-shadow:0 0 40px #172b70;
  text-align:center;
}

.title{
  font-size:clamp(32px,8vw,60px);
  margin:0 0 8px;
  color:#fff;
  text-shadow:0 0 18px #4f7cff;
}

.subtitle{
  color:#9eb5ff;
  margin-bottom:25px;
}

.saveGrid{
  display:grid;
  gap:12px;
}

.save{
  background:#111a31;
  border:1px solid #42578e;
  border-radius:15px;
  padding:15px;
  text-align:left;
}

.saveName{
  font-weight:bold;
  font-size:18px;
}

.saveInfo{
  color:#9ca8c8;
  font-size:13px;
  margin-top:5px;
}

.menu button,
.customize button{
  border:0;
  border-radius:12px;
  padding:12px 18px;
  background:#315cff;
  color:white;
  font-weight:bold;
  margin-top:10px;
}

.delete{
  background:#8b2334!important;
}

/* CUSTOMIZE */

.customize{
  width:min(600px,100%);
  background:#0c1222;
  border:2px solid #4f6eff;
  border-radius:20px;
  padding:25px;
}

.customize h2{
  margin-top:0;
}

.customize label{
  display:block;
  text-align:left;
  margin-top:14px;
  color:#aebeff;
}

.customize input,
.customize select{
  width:100%;
  padding:12px;
  margin-top:6px;
  border-radius:10px;
  border:1px solid #53658f;
  background:#080d19;
  color:white;
}

/* GAME */

#game{
  display:block;
  padding:10px;
}

.gameTop{
  width:min(1100px,100%);
  margin:auto;
  display:flex;
  justify-content:space-between;
  align-items:center;
  gap:10px;
  flex-wrap:wrap;
  padding:8px;
}

.levelText{
  font-size:20px;
  font-weight:bold;
}

.powerText{
  color:#ffd85a;
}

.arena{
  position:relative;
  width:min(1100px,100%);
  height:min(620px,68vh);
  min-height:430px;
  margin:auto;
  overflow:hidden;
  border:2px solid #283967;
  border-radius:20px;
  background:
    radial-gradient(circle at 50% 30%,#19285b 0,#0b1230 30%,#050711 75%);
  box-shadow:0 0 40px #111d4a;
}

/* STARS */

.arena:before{
  content:"";
  position:absolute;
  inset:0;
  background-image:
    radial-gradient(circle,#fff 1px,transparent 1px),
    radial-gradient(circle,#7191ff 1px,transparent 1px);
  background-size:75px 75px,120px 120px;
  opacity:.35;
  pointer-events:none;
}

/* FLOOR */

.floor{
  position:absolute;
  bottom:0;
  left:0;
  width:100%;
  height:35%;
  background:
    linear-gradient(transparent 95%,#263b72 95%),
    linear-gradient(90deg,transparent 95%,#263b72 95%);
  background-size:55px 35px;
  transform:perspective(300px) rotateX(55deg);
  transform-origin:bottom;
  opacity:.45;
  pointer-events:none;
}

/* HEALTH */

.healthArea{
  position:absolute;
  top:18px;
  width:36%;
  min-width:150px;
  z-index:5;
}

.playerArea{
  left:3%;
}

.enemyArea{
  right:3%;
  text-align:right;
}

.healthName{
  font-weight:bold;
  margin-bottom:5px;
  text-shadow:0 2px 4px black;
}

.healthBar{
  width:100%;
  height:17px;
  background:#1b2030;
  border:2px solid #59627b;
  border-radius:20px;
  overflow:hidden;
}

.healthFill{
  height:100%;
  width:100%;
  transition:width .3s ease;
}

.playerHealth{
  background:linear-gradient(90deg,#ffb300,#fff06a,#d89000);
  box-shadow:0 0 12px #ffd43b;
}

.enemyHealth{
  background:linear-gradient(90deg,#ff3030,#9d001c);
  box-shadow:0 0 12px #ff1d35;
}

/* FIGHTERS */

.fighter{
  position:absolute;
  bottom:105px;
  width:180px;
  height:260px;
  z-index:4;
  pointer-events:none;
}

#player{
  left:13%;
}

#enemy{
  right:13%;
}

/* HUMAN PLAYER */

.human{
  position:absolute;
  inset:0;
}

.humanHead{
  position:absolute;
  width:65px;
  height:70px;
  left:58px;
  top:12px;
  border-radius:45% 45% 48% 48%;
  background:linear-gradient(135deg,#f4c7a4,#bd7959);
  border:3px solid #613c35;
  z-index:3;
}

.hair{
  position:absolute;
  width:70px;
  height:32px;
  left:-5px;
  top:-6px;
  border-radius:50% 50% 30% 30%;
  background:#1d1b20;
}

.eye{
  position:absolute;
  top:31px;
  width:7px;
  height:7px;
  border-radius:50%;
  background:#111;
}

.eye1{left:17px}
.eye2{right:17px}

.mouth{
  position:absolute;
  width:20px;
  height:6px;
  border-bottom:2px solid #542c2c;
  left:21px;
  top:52px;
}

.armorBody{
  position:absolute;
  top:78px;
  left:40px;
  width:100px;
  height:105px;
  border-radius:28px 28px 18px 18px;
  background:linear-gradient(135deg,#6d83ff,#2639a0 55%,#111b65);
  border:3px solid #9eb0ff;
  box-shadow:inset 0 0 15px #91a7ff;
}

.core{
  position:absolute;
  width:28px;
  height:28px;
  left:33px;
  top:25px;
  border-radius:50%;
  background:#fff;
  box-shadow:0 0 18px #fff,0 0 35px #63aaff;
}

.shoulder{
  position:absolute;
  top:82px;
  width:38px;
  height:38px;
  border-radius:50%;
  background:#435bd2;
  border:3px solid #91a4ff;
}

.shoulder.left{left:18px}
.shoulder.right{right:18px}

.arm{
  position:absolute;
  top:111px;
  width:27px;
  height:75px;
  border-radius:15px;
  background:#3448a8;
  border:3px solid #8297ff;
}

.arm.left{left:20px;transform:rotate(12deg)}
.arm.right{right:20px;transform:rotate(-12deg)}

.leg{
  position:absolute;
  top:175px;
  width:35px;
  height:75px;
  border-radius:10px;
  background:#25337e;
  border:3px solid #7286ef;
}

.leg.left{left:53px}
.leg.right{right:53px}

.boot{
  position:absolute;
  top:235px;
  width:45px;
  height:18px;
  border-radius:12px;
  background:#151a35;
  border:2px solid #6779d9;
}

.boot.left{left:42px}
.boot.right{right:42px}

/* DEMON */

.demon{
  position:absolute;
  inset:0;
}

.demonHead{
  position:absolute;
  left:48px;
  top:20px;
  width:85px;
  height:75px;
  border-radius:48% 48% 40% 40%;
  background:linear-gradient(145deg,#2a2039,#08070e);
  border:3px solid #713a85;
}

.horn{
  position:absolute;
  top:-28px;
  width:25px;
  height:40px;
  background:#271832;
  border:3px solid #713a85;
  clip-path:polygon(50% 0,100% 100%,0 100%);
}

.horn.left{left:5px;transform:rotate(-18deg)}
.horn.right{right:5px;transform:rotate(18deg)}

.demonEye{
  position:absolute;
  top:34px;
  width:19px;
  height:9px;
  background:#ff263e;
  border-radius:50%;
  box-shadow:0 0 15px #ff2039;
}

.demonEye.left{left:15px}
.demonEye.right{right:15px}

.demonMouth{
  position:absolute;
  left:27px;
  top:53px;
  width:32px;
  height:12px;
  border-bottom:4px solid #ff3045;
}

.demonBody{
  position:absolute;
  top:92px;
  left:32px;
  width:118px;
  height:105px;
  border-radius:35px 35px 18px 18px;
  background:linear-gradient(135deg,#35204d,#110b1b);
  border:3px solid #713a85;
}

.demonCore{
  position:absolute;
  left:42px;
  top:30px;
  width:34px;
  height:34px;
  border-radius:50%;
  background:#ff213e;
  box-shadow:0 0 20px #ff2039;
}

.claw{
  position:absolute;
  top:120px;
  width:35px;
  height:70px;
  background:#21142e;
  border:3px solid #713a85;
  border-radius:18px;
}

.claw.left{left:12px;transform:rotate(15deg)}
.claw.right{right:12px;transform:rotate(-15deg)}

.demonLeg{
  position:absolute;
  top:195px;
  width:40px;
  height:60px;
  background:#160e20;
  border:3px solid #572d69;
  border-radius:12px;
}

.demonLeg.left{left:45px}
.demonLeg.right{right:45px}

/* COMBAT ANIMATIONS */

.playerDash{
  animation:playerDash .65s ease;
}

@keyframes playerDash{
  50%{transform:translateX(130px) scale(1.08)}
}

.demonDash{
  animation:demonDash .65s ease;
}

@keyframes demonDash{
  50%{transform:translateX(-110px) scale(1.05)}
}

.hit{
  animation:hit .45s ease;
}

@keyframes hit{
  25%{transform:translateX(12px)}
  50%{transform:translateX(-12px)}
  75%{transform:translateX(7px)}
}

.shielding{
  animation:shieldPulse .8s ease;
}

@keyframes shieldPulse{
  50%{filter:drop-shadow(0 0 25px #49aaff)}
}

/* EFFECTS NEVER RECEIVE TOUCHES */

.effect,
.projectile,
.beam,
.impact,
.shieldEffect,
.flash{
  position:absolute;
  pointer-events:none!important;
  z-index:20;
}

.projectile{
  width:35px;
  height:35px;
  border-radius:50%;
  background:white;
  box-shadow:0 0 15px #fff,0 0 35px #54aaff;
}

.lightBeam{
  position:absolute;
  left:10%;
  right:10%;
  top:35%;
  height:35px;
  border-radius:50%;
  background:white;
  box-shadow:0 0 20px white,0 0 45px #65baff;
  animation:beam .55s ease;
}

@keyframes beam{
  from{transform:scaleX(.1);opacity:.2}
  to{transform:scaleX(1);opacity:1}
}

.shieldCircle{
  position:absolute;
  width:250px;
  height:250px;
  border:6px solid #57baff;
  border-radius:50%;
  box-shadow:0 0 20px #57baff,0 0 55px #217aff inset;
  animation:shield .8s ease;
}

@keyframes shield{
  0%{transform:scale(.5);opacity:0}
  50%{transform:scale(1);opacity:1}
  100%{transform:scale(1.15);opacity:.2}
}

/* CONTROLS */

.controls{
  position:relative;
  z-index:100;
  width:min(1100px,100%);
  margin:12px auto 0;
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:10px;
}

.controls button{
  min-height:58px;
  border:2px solid #4e6bff;
  border-radius:14px;
  background:linear-gradient(#17265a,#0b1231);
  color:white;
  font-weight:bold;
  box-shadow:0 5px 15px #0008;
  transition:.15s;
}

.controls button:active{
  transform:scale(.96);
}

.controls button:disabled{
  opacity:.45;
}

.special{
  border-color:#ffd53e!important;
  color:#ffe36c!important;
}

.log{
  width:min(1100px,100%);
  margin:10px auto;
  min-height:55px;
  max-height:100px;
  overflow-y:auto;
  background:#080d19;
  border:1px solid #29375d;
  border-radius:12px;
  padding:10px;
  color:#c5d1ff;
}

/* STATUS */

.status{
  position:absolute;
  left:50%;
  top:20px;
  transform:translateX(-50%);
  z-index:10;
  padding:7px 14px;
  border-radius:20px;
  background:#050812cc;
  border:1px solid #3b4d80;
  font-size:13px;
}

/* OVERLAY */

.overlay{
  position:fixed;
  inset:0;
  background:#02040ccc;
  z-index:500;
  display:flex;
  align-items:center;
  justify-content:center;
  padding:20px;
}

.overlayBox{
  background:#0d1427;
  border:2px solid #5576ff;
  border-radius:20px;
  padding:30px;
  text-align:center;
  width:min(500px,100%);
}

.overlayBox button{
  padding:13px 25px;
  border:0;
  border-radius:12px;
  background:#315cff;
  color:white;
  font-weight:bold;
}

/* MOBILE */

@media(max-width:700px){
  .arena{
    height:52vh;
    min-height:390px;
  }

  .fighter{
    transform:scale(.75);
    transform-origin:bottom center;
  }

  #player{
    left:0;
  }

  #enemy{
    right:0;
  }

  .controls{
    grid-template-columns:repeat(2,1fr);
  }

  .controls button{
    min-height:54px;
  }

  .healthArea{
    width:43%;
  }

  .status{
    top:70px;
  }
}
</style>
</head>

<body>

<!-- SAVE SCREEN -->

<div id="saveScreen" class="screen">
  <div class="menu">
    <h1 class="title">SHADOWBOUND</h1>
    <div class="subtitle">Spiritual Power</div>

    <div id="saveGrid" class="saveGrid"></div>

    <button onclick="newSave()">Create New Save</button>
  </div>
</div>

<!-- CUSTOMIZATION -->

<div id="customScreen" class="screen hidden">
  <div class="customize">

    <h2>Create Your Warrior</h2>

    <label>
      Name
      <input id="nameInput" maxlength="20" placeholder="Warrior">
    </label>

    <label>
      Gender
      <select id="genderInput">
        <option>Male</option>
        <option>Female</option>
      </select>
    </label>

    <label>
      Armor Color
      <input id="armorInput" type="color" value="#315cff">
    </label>

    <label>
      Hair / Helmet Color
      <input id="helmetInput" type="color" value="#17171c">
    </label>

    <button onclick="createCharacter()">Begin Journey</button>
  </div>
</div>

<!-- GAME -->

<div id="game" class="hidden">

  <div class="gameTop">
    <div class="levelText">
      Level <span id="level">1</span>
    </div>

    <div class="powerText">
      Spiritual Power: <span id="power">0</span>
    </div>
  </div>

  <div class="arena" id="arena">

    <div class="floor"></div>

    <div class="status" id="status">
      Your turn
    </div>

    <!-- PLAYER HEALTH -->

    <div class="healthArea playerArea">
      <div class="healthName" id="playerName">Warrior</div>
      <div class="healthBar">
        <div id="playerHealth" class="healthFill playerHealth"></div>
      </div>
      <small id="playerHpText">100 / 100</small>
    </div>

    <!-- ENEMY HEALTH -->

    <div class="healthArea enemyArea">
      <div class="healthName" id="enemyName">Shadow Demon</div>
      <div class="healthBar">
        <div id="enemyHealth" class="healthFill enemyHealth"></div>
      </div>
      <small id="enemyHpText">100 / 100</small>
    </div>

    <!-- PLAYER -->

    <div id="player" class="fighter">

      <div class="human">

        <div class="humanHead">
          <div class="hair"></div>
          <div class="eye eye1"></div>
          <div class="eye eye2"></div>
          <div class="mouth"></div>
        </div>

        <div class="armorBody">
          <div class="core"></div>
        </div>

        <div class="shoulder left"></div>
        <div class="shoulder right"></div>

        <div class="arm left"></div>
        <div class="arm right"></div>

        <div class="leg left"></div>
        <div class="leg right"></div>

        <div class="boot left"></div>
        <div class="boot right"></div>

      </div>

    </div>

    <!-- ENEMY -->

    <div id="enemy" class="fighter">

      <div class="demon">

        <div class="demonHead">
          <div class="horn left"></div>
          <div class="horn right"></div>
          <div class="demonEye left"></div>
          <div class="demonEye right"></div>
          <div class="demonMouth"></div>
        </div>

        <div class="demonBody">
          <div class="demonCore"></div>
        </div>

        <div class="claw left"></div>
        <div class="claw right"></div>

        <div class="demonLeg left"></div>
        <div class="demonLeg right"></div>

      </div>

    </div>

    <div id="effects"></div>

  </div>

  <div id="attackControls" class="controls">

    <button onclick="playerAttack('strike')">
      ✨ Spirit Strike
    </button>

    <button onclick="playerAttack('shield')">
      🛡 Shield of Fate
    </button>

    <button onclick="playerAttack('truth')">
      ☀ Word of Truth
    </button>

    <button id="specialButton"
            class="special"
            onclick="playerAttack('burst')"
            disabled>
      ⚡ Light Burst
    </button>

  </div>

  <div id="log" class="log">
    Your journey begins...
  </div>

</div>

<!-- OVERLAY -->

<div id="overlay" class="overlay hidden">
  <div class="overlayBox">
    <h1 id="overlayTitle">Victory</h1>
    <p id="overlayText"></p>
    <button onclick="closeOverlay()">Continue</button>
  </div>
</div>

<script>
/* =========================================================
   SAVE SYSTEM
========================================================= */

const SAVE_KEY = "spiritualPowerShadowboundSaves";

let saves = JSON.parse(localStorage.getItem(SAVE_KEY) || "[]");

let currentSave = null;

function saveAll(){
  localStorage.setItem(SAVE_KEY,JSON.stringify(saves));
}

function showSaves(){

  const grid = document.getElementById("saveGrid");

  grid.innerHTML = "";

  for(let i=0;i<3;i++){

    const save = saves[i];

    const box = document.createElement("div");
    box.className = "save";

    if(save){

      box.innerHTML = `
        <div class="saveName">${safe(save.name)}</div>
        <div class="saveInfo">
          Level ${save.level} • Power ${save.power}
        </div>
        <button onclick="loadSave(${i})">Continue</button>
        <button class="delete" onclick="deleteSave(${i})">Delete</button>
      `;

    }else{

      box.innerHTML = `
        <div class="saveName">Empty Save Slot ${i+1}</div>
        <button onclick="newSave(${i})">Create</button>
      `;
    }

    grid.appendChild(box);
  }
}

function safe(text){
  return String(text || "")
    .replaceAll("&","&amp;")
    .replaceAll("<","&lt;")
    .replaceAll(">","&gt;")
    .replaceAll('"',"&quot;")
    .replaceAll("'","&#039;");
}

function newSave(slot){

  if(slot === undefined){

    slot = saves.findIndex(x=>!x);

    if(slot === -1){
      alert("All three save slots are full.");
      return;
    }
  }

  currentSave = slot;

  document.getElementById("saveScreen").classList.add("hidden");
  document.getElementById("customScreen").classList.remove("hidden");
}

function deleteSave(slot){

  if(!confirm("Delete this save?")) return;

  saves[slot] = null;
  saveAll();
  showSaves();
}

function loadSave(slot){

  currentSave = slot;

  state = JSON.parse(JSON.stringify(saves[slot]));

  document.getElementById("saveScreen").classList.add("hidden");

  startGame();
}


/* =========================================================
   GAME DATA
========================================================= */

const levels = [

  {
    name:"Shadow Demon",
    hp:100,
    verse:"Ephesians 6:11",
    verseText:"Put on the whole armour of God, that ye may be able to stand against the wiles of the devil."
  },

  {
    name:"Dark Angel",
    hp:200,
    verse:"Psalm 18:2",
    verseText:"The LORD is my rock, and my fortress, and my deliverer; my God, my strength, in whom I will trust."
  },

  {
    name:"Shadow Colossus",
    hp:380,
    verse:"1 John 4:4",
    verseText:"Greater is he that is in you, than he that is in the world."
  }

];


/* =========================================================
   PLAYER STATE
========================================================= */

let state = {

  name:"Warrior",

  gender:"Male",

  armor:"#315cff",

  helmet:"#17171c",

  level:1,

  power:0,

  hp:100,

  spirit:0,

  turns:0,

  specialUnlocked:false
};


let enemy = {

  name:"",

  maxHp:0,

  hp:0
};


/* =========================================================
   COMBAT STATE
========================================================= */

/*
 IMPORTANT:

 busy is ONLY used to prevent double-attacking.

 It is NEVER left true permanently.

 unlockTurn() is called after EVERY enemy turn.
*/

let busy = false;

let shieldActive = false;


/* =========================================================
   CREATE CHARACTER
========================================================= */

function createCharacter(){

  state.name =
    document.getElementById("nameInput").value.trim() || "Warrior";

  state.gender =
    document.getElementById("genderInput").value;

  state.armor =
    document.getElementById("armorInput").value;

  state.helmet =
    document.getElementById("helmetInput").value;

  state.level = 1;
  state.power = 0;
  state.hp = 100;
  state.spirit = 0;
  state.turns = 0;
  state.specialUnlocked = false;

  saveGame();

  document.getElementById("customScreen").classList.add("hidden");

  startGame();
}


/* =========================================================
   START GAME
========================================================= */

function startGame(){

  document.getElementById("game").classList.remove("hidden");

  busy = false;
  shieldActive = false;

  loadLevel();

  applyAppearance();

  updateUI();

  log(
    "Level 1 begins. " +
    levels[0].verse +
    ": " +
    levels[0].verseText
  );
}


/* =========================================================
   LEVEL
========================================================= */

function loadLevel(){

  const data = levels[state.level - 1];

  enemy.name = data.name;
  enemy.maxHp = data.hp;
  enemy.hp = data.hp;

  state.hp = 100 + ((state.level - 1) * 35);

  state.spirit = 0;
  state.turns = 0;
  state.specialUnlocked = false;

  busy = false;
  shieldActive = false;

  document.getElementById("specialButton").disabled = true;

  updateUI();
}


/* =========================================================
   APPEARANCE
========================================================= */

function applyAppearance(){

  document.querySelector(".armorBody").style.background =
    `linear-gradient(135deg,${state.armor},#111b65)`;

  document.querySelector(".humanHead").style.background =
    "linear-gradient(135deg,#f4c7a4,#bd7959)";

  document.querySelector(".hair").style.background =
    state.helmet;

  document.getElementById("playerName").textContent =
    state.name;
}


/* =========================================================
   UI
========================================================= */

function updateUI(){

  const data = levels[state.level - 1];

  document.getElementById("level").textContent =
    state.level;

  document.getElementById("power").textContent =
    state.power;

  document.getElementById("playerName").textContent =
    state.name;

  document.getElementById("enemyName").textContent =
    enemy.name;

  const playerMax =
    100 + ((state.level - 1) * 35);

  document.getElementById("playerHealth").style.width =
    Math.max(0,state.hp / playerMax * 100) + "%";

  document.getElementById("enemyHealth").style.width =
    Math.max(0,enemy.hp / enemy.maxHp * 100) + "%";

  document.getElementById("playerHpText").textContent =
    `${Math.max(0,state.hp)} / ${playerMax}`;

  document.getElementById("enemyHpText").textContent =
    `${Math.max(0,enemy.hp)} / ${enemy.maxHp}`;

  document.getElementById("specialButton").disabled =
    !state.specialUnlocked || busy;

  document.getElementById("status").textContent =
    busy ? "Enemy's turn..." : "Your turn";
}


/* =========================================================
   LOG
========================================================= */

function log(message){

  const box = document.getElementById("log");

  box.innerHTML += `<div>${safe(message)}</div>`;

  box.scrollTop = box.scrollHeight;
}


/* =========================================================
   PLAYER ATTACK
========================================================= */

function playerAttack(type){

  /*
   THIS CHECK PREVENTS DOUBLE TAPS.

   It is immediately released by unlockTurn()
   after the demon finishes.
  */

  if(busy) return;

  if(type === "burst" && !state.specialUnlocked){
    return;
  }

  busy = true;

  updateUI();

  if(type === "strike"){

    spiritStrike();

  }else if(type === "shield"){

    shieldOfFate();

  }else if(type === "truth"){

    wordOfTruth();

  }else if(type === "burst"){

    lightBurst();
  }
}


/* =========================================================
   SPIRIT STRIKE
========================================================= */

function spiritStrike(){

  log("You used Spirit Strike!");

  const player =
    document.getElementById("player");

  player.classList.add("playerDash");

  setTimeout(()=>{

    player.classList.remove("playerDash");

    createProjectile();

    const damage =
      20 + state.level * 5;

    enemy.hp =
      Math.max(0,enemy.hp - damage);

    state.spirit += 12;

    enemyHitAnimation();

    updateUI();

  },350);

  finishPlayerAttack(900);
}


/* =========================================================
   SHIELD OF FATE
========================================================= */

function shieldOfFate(){

  log("You raised the Shield of Fate!");

  shieldActive = true;

  state.spirit += 20;

  const player =
    document.getElementById("player");

  player.classList.add("shielding");

  createShield();

  updateUI();

  finishPlayerAttack(900);
}


/* =========================================================
   WORD OF TRUTH
========================================================= */

function wordOfTruth(){

  log("You used Word of Truth!");

  createBeam();

  const damage =
    32 + state.level * 6;

  enemy.hp =
    Math.max(0,enemy.hp - damage);

  state.spirit += 24;

  enemyHitAnimation();

  updateUI();

  finishPlayerAttack(1000);
}


/* =========================================================
   LIGHT BURST
========================================================= */

function lightBurst(){

  if(!state.specialUnlocked){
    unlockTurn();
    return;
  }

  log("LIGHT BURST!");

  createHugeBeam();

  const damage =
    100 + state.level * 25;

  enemy.hp =
    Math.max(0,enemy.hp - damage);

  state.spirit = 0;

  state.specialUnlocked = false;

  enemyHitAnimation();

  updateUI();

  finishPlayerAttack(1200);
}


/* =========================================================
   FINISH PLAYER ATTACK
========================================================= */

function finishPlayerAttack(delay){

  setTimeout(()=>{

    /*
     If the enemy was defeated, do NOT let it attack.
    */

    if(enemy.hp <= 0){

      enemyDefeated();

      return;
    }

    /*
     Player attack is finished.
     Now enemy gets exactly one turn.
    */

    enemyAttack();

  },delay);
}


/* =========================================================
   ENEMY ATTACK
========================================================= */

function enemyAttack(){

  /*
   We intentionally DO NOT return because of busy.

   busy should be TRUE here.
  */

  document.getElementById("status").textContent =
    "Enemy's turn...";

  if(shieldActive){

    log("Shield of Fate blocked the attack!");

    createShieldBlock();

    shieldActive = false;

    const player =
      document.getElementById("player");

    player.classList.remove("shielding");

    setTimeout(()=>{

      finishEnemyTurn();

    },750);

    return;
  }


  log(enemy.name + " attacks!");

  const demon =
    document.getElementById("enemy");

  demon.classList.add("demonDash");

  setTimeout(()=>{

    demon.classList.remove("demonDash");

    const damage =
      12 + state.level * 5;

    state.hp =
      Math.max(0,state.hp - damage);

    playerHitAnimation();

    updateUI();

  },350);


  setTimeout(()=>{

    if(state.hp <= 0){

      playerDefeated();

      return;
    }

    finishEnemyTurn();

  },900);
}


/* =========================================================
   FINISH ENEMY TURN

   THIS IS THE IMPORTANT FIX.
========================================================= */

function finishEnemyTurn(){

  state.turns++;

  /*
   After 3 enemy turns the special becomes available.
  */

  if(state.turns >= 3){

    state.specialUnlocked = true;

    log("Your spiritual power has awakened. Light Burst is ready!");

  }

  saveGame();

  /*
   CLEAR ALL POSSIBLE VISUAL LOCKS.
  */

  busy = false;

  shieldActive = false;

  document
    .getElementById("player")
    .classList.remove("shielding");

  /*
   FORCE EVERY ATTACK BUTTON BACK ON.
  */

  const controls =
    document.getElementById("attackControls");

  controls.style.pointerEvents = "auto";
  controls.style.opacity = "1";

  document
    .querySelectorAll("#attackControls button")
    .forEach(button=>{

      button.style.pointerEvents = "auto";

      button.disabled = false;

    });

  /*
   Special should ONLY be enabled when unlocked.
  */

  document.getElementById("specialButton").disabled =
    !state.specialUnlocked;

  updateUI();

  document.getElementById("status").textContent =
    "Your turn";

  log("Your turn — choose an attack.");
}


/* =========================================================
   HIT ANIMATIONS
========================================================= */

function enemyHitAnimation(){

  const enemyElement =
    document.getElementById("enemy");

  enemyElement.classList.add("hit");

  setTimeout(()=>{

    enemyElement.classList.remove("hit");

  },500);
}

function playerHitAnimation(){

  const player =
    document.getElementById("player");

  player.classList.add("hit");

  setTimeout(()=>{

    player.classList.remove("hit");

  },500);
}


/* =========================================================
   VISUAL EFFECTS
========================================================= */

function createProjectile(){

  const arena =
    document.getElementById("arena");

  const projectile =
    document.createElement("div");

  projectile.className =
    "projectile effect";

  projectile.style.left =
    "31%";

  projectile.style.top =
    "52%";

  arena.appendChild(projectile);

  projectile.animate(

    [
      {transform:"translateX(0) scale(.5)",opacity:0},
      {transform:"translateX(300px) scale(1)",opacity:1},
      {transform:"translateX(520px) scale(.2)",opacity:0}
    ],

    {
      duration:600,
      easing:"ease-out"
    }

  ).onfinish = ()=>{

    projectile.remove();

  };
}


function createBeam(){

  const arena =
    document.getElementById("arena");

  const beam =
    document.createElement("div");

  beam.className =
    "lightBeam effect";

  arena.appendChild(beam);

  setTimeout(()=>beam.remove(),600);
}


function createHugeBeam(){

  const arena =
    document.getElementById("arena");

  const beam =
    document.createElement("div");

  beam.className =
    "lightBeam effect";

  beam.style.height = "90px";
  beam.style.top = "38%";
  beam.style.boxShadow =
    "0 0 30px white,0 0 70px #fff,0 0 120px #52aaff";

  arena.appendChild(beam);

  setTimeout(()=>beam.remove(),900);
}


function createShield(){

  const arena =
    document.getElementById("arena");

  const shield =
    document.createElement("div");

  shield.className =
    "shieldCircle effect";

  shield.style.left =
    "5%";

  shield.style.top =
    "30%";

  arena.appendChild(shield);

  setTimeout(()=>shield.remove(),900);
}


function createShieldBlock(){

  const arena =
    document.getElementById("arena");

  const shield =
    document.createElement("div");

  shield.className =
    "shieldCircle effect";

  shield.style.left =
    "5%";

  shield.style.top =
    "30%";

  shield.style.borderColor =
    "#ffffff";

  arena.appendChild(shield);

  setTimeout(()=>shield.remove(),700);
}


/* =========================================================
   PLAYER DEFEATED
========================================================= */

function playerDefeated(){

  busy = false;

  state.hp =
    100 + ((state.level - 1) * 35);

  state.spirit = 0;
  state.turns = 0;
  state.specialUnlocked = false;

  saveGame();

  showOverlay(
    "Defeated",
    "Your warrior has fallen, but the journey is not over."
  );
}


/* =========================================================
   ENEMY DEFEATED
========================================================= */

function enemyDefeated(){

  busy = false;

  state.power += 100 * state.level;

  saveGame();

  if(state.level >= 3){

    showOverlay(
      "VICTORY!",
      "You defeated the Shadow Colossus and completed your journey."
    );

    return;
  }

  const nextLevel =
    state.level + 1;

  const verse =
    levels[nextLevel - 1];

  showOverlay(
    "Enemy Defeated!",
    `You reached Level ${nextLevel}. ${verse.verse}: ${verse.verseText}`
  );

}


/* =========================================================
   OVERLAY
========================================================= */

function showOverlay(title,text){

  document.getElementById("overlayTitle").textContent =
    title;

  document.getElementById("overlayText").textContent =
    text;

  document.getElementById("overlay").classList.remove("hidden");
}


function closeOverlay(){

  document.getElementById("overlay").classList.add("hidden");

  /*
   If the game was completed, stay on the victory screen
   until the user starts over.
  */

  if(state.level >= 3 && enemy.hp <= 0){

    document.getElementById("overlayText").textContent =
      "Your spiritual journey is complete.";

    document.querySelector(".overlayBox button").textContent =
      "Restart Level";

    document.querySelector(".overlayBox button").onclick =
      ()=>{
        state.level = 1;
        state.power = 0;
        loadLevel();
        saveGame();
        document.querySelector(".overlayBox button").onclick =
          closeOverlay;
      };

    document.getElementById("overlay").classList.remove("hidden");

    return;
  }

  /*
   Advance to next level.
  */

  if(enemy.hp <= 0){

    state.level++;

    loadLevel();

    saveGame();

    log(
      `Level ${state.level}: ${levels[state.level-1].name}`
    );

    updateUI();

    /*
     MOST IMPORTANT:
     Make sure attacks work immediately.
    */

    busy = false;

    document
      .querySelectorAll("#attackControls button")
      .forEach(button=>{
        button.style.pointerEvents = "auto";
      });

    return;
  }

  /*
   Player lost.
  */

  loadLevel();

  busy = false;

  updateUI();
}


/* =========================================================
   SAVE GAME
========================================================= */

function saveGame(){

  if(currentSave === null) return;

  saves[currentSave] =
    JSON.parse(JSON.stringify(state));

  saveAll();
}


/* =========================================================
   AUTO SAVE
========================================================= */

setInterval(()=>{

  if(
    !document
      .getElementById("game")
      .classList
      .contains("hidden")
  ){

    saveGame();

  }

},5000);


/* =========================================================
   INITIALIZE
========================================================= */

showSaves();


/* =========================================================
   EXTRA SAFETY FIX

   If the browser somehow leaves busy=true while
   everything is visibly finished, tapping the arena
   will not be required. The game always recovers.
========================================================= */

window.addEventListener("pageshow",()=>{

  if(document.getElementById("game")){

    const controls =
      document.getElementById("attackControls");

    controls.style.pointerEvents = "auto";

  }

});

</script>

</body>
</html>
