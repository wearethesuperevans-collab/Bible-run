<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport"
      content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Spiritual Power: Shadowbound</title>

<style>
*{
  box-sizing:border-box;
  -webkit-tap-highlight-color:transparent;
}

html,body{
  margin:0;
  width:100%;
  height:100%;
  overflow:hidden;
  background:#050817;
  color:white;
  font-family:Arial,Helvetica,sans-serif;
}

button{
  font:inherit;
  touch-action:manipulation;
}

#game{
  width:100%;
  height:100%;
  position:relative;
  overflow:hidden;
  background:
    radial-gradient(circle at 50% 25%,#192c63 0%,#080d21 48%,#02030a 100%);
}

#stars{
  position:absolute;
  inset:0;
  pointer-events:none;
  opacity:.8;
  background-image:
    radial-gradient(circle,#fff 1px,transparent 1px),
    radial-gradient(circle,#8ab4ff 1px,transparent 1px);
  background-size:90px 90px,140px 140px;
  background-position:15px 20px,50px 70px;
}

#topbar{
  position:absolute;
  z-index:20;
  top:0;
  left:0;
  right:0;
  min-height:70px;
  padding:10px 14px;
  display:flex;
  justify-content:space-between;
  align-items:center;
  gap:10px;
  background:linear-gradient(180deg,rgba(2,5,15,.94),rgba(2,5,15,.55),transparent);
}

.logo{
  font-weight:900;
  font-size:clamp(16px,3vw,25px);
  letter-spacing:1px;
  color:#ffd84d;
  text-shadow:0 0 14px rgba(255,216,77,.6);
}

#levelText{
  font-weight:bold;
  font-size:14px;
  color:#d8e5ff;
  text-align:right;
}

#arena{
  position:absolute;
  left:0;
  right:0;
  top:68px;
  bottom:215px;
  min-height:300px;
  overflow:hidden;
}

#arena:before{
  content:"";
  position:absolute;
  left:5%;
  right:5%;
  bottom:8%;
  height:30%;
  background:radial-gradient(ellipse,rgba(47,110,255,.25),transparent 70%);
  filter:blur(15px);
}

#arena:after{
  content:"";
  position:absolute;
  left:0;
  right:0;
  bottom:0;
  height:28%;
  background:linear-gradient(180deg,transparent,#03040c);
  pointer-events:none;
}

canvas{
  position:absolute;
  inset:0;
  width:100%;
  height:100%;
}

#hud{
  position:absolute;
  z-index:10;
  left:12px;
  right:12px;
  top:12px;
  display:flex;
  justify-content:space-between;
  pointer-events:none;
}

.fighterHUD{
  width:min(37%,300px);
}

.hudName{
  font-weight:900;
  margin-bottom:5px;
  text-shadow:0 2px 5px #000;
}

.bar{
  height:14px;
  border-radius:20px;
  background:#101524;
  border:1px solid rgba(255,255,255,.3);
  overflow:hidden;
  box-shadow:0 2px 8px #000;
}

.fill{
  height:100%;
  width:100%;
  transition:width .3s ease;
}

#playerHP{
  background:linear-gradient(90deg,#fff08a,#ffd21c,#e5a800);
  box-shadow:0 0 14px rgba(255,210,30,.8);
}

#enemyHP{
  background:linear-gradient(90deg,#ff5b73,#d41539,#72051b);
  box-shadow:0 0 14px rgba(255,30,70,.7);
}

.hpText{
  font-size:11px;
  margin-top:3px;
  color:#dce6ff;
}

#turnText{
  position:absolute;
  z-index:15;
  left:50%;
  top:7px;
  transform:translateX(-50%);
  padding:6px 12px;
  border-radius:20px;
  background:rgba(5,8,20,.7);
  border:1px solid rgba(255,255,255,.16);
  font-size:12px;
  font-weight:900;
  letter-spacing:1px;
}

#combatMessage{
  position:absolute;
  z-index:30;
  left:50%;
  bottom:12px;
  transform:translateX(-50%);
  width:min(90%,700px);
  text-align:center;
  padding:10px 15px;
  border-radius:14px;
  background:rgba(2,5,15,.76);
  border:1px solid rgba(255,255,255,.14);
  backdrop-filter:blur(8px);
  font-size:14px;
  line-height:1.35;
  box-shadow:0 8px 30px rgba(0,0,0,.35);
}

#controls{
  position:absolute;
  z-index:40;
  left:0;
  right:0;
  bottom:0;
  min-height:215px;
  padding:12px;
  background:
    linear-gradient(180deg,rgba(5,8,20,.3),rgba(3,5,14,.98) 18%);
  border-top:1px solid rgba(255,255,255,.08);
}

#buttons{
  width:min(760px,100%);
  margin:auto;
  display:grid;
  grid-template-columns:repeat(2,1fr);
  gap:9px;
}

.attackBtn{
  min-height:56px;
  border:1px solid rgba(255,255,255,.16);
  border-radius:14px;
  color:white;
  font-weight:900;
  cursor:pointer;
  background:linear-gradient(145deg,#1d3b7d,#0b1531);
  box-shadow:
    inset 0 1px rgba(255,255,255,.15),
    0 5px 15px rgba(0,0,0,.35);
  transition:transform .1s,filter .1s,opacity .15s;
}

.attackBtn:active:not(:disabled){
  transform:scale(.96);
}

.attackBtn:disabled{
  opacity:.32;
  cursor:not-allowed;
  filter:grayscale(.5);
}

#shieldBtn{
  background:linear-gradient(145deg,#664d13,#211a08);
}

#truthBtn{
  background:linear-gradient(145deg,#45277b,#160d2c);
}

#burstBtn{
  background:linear-gradient(145deg,#1e6f70,#092a2c);
}

#verseBox{
  width:min(760px,100%);
  margin:9px auto 0;
  padding:8px 12px;
  text-align:center;
  border-radius:10px;
  color:#dce7ff;
  background:rgba(255,255,255,.035);
  font-size:11px;
  line-height:1.3;
}

#overlay{
  position:absolute;
  z-index:100;
  inset:0;
  display:flex;
  justify-content:center;
  align-items:center;
  padding:20px;
  background:rgba(1,3,10,.86);
  backdrop-filter:blur(12px);
}

.modal{
  width:min(560px,100%);
  max-height:92vh;
  overflow:auto;
  padding:22px;
  border-radius:22px;
  background:
    linear-gradient(145deg,rgba(25,37,78,.98),rgba(6,10,25,.98));
  border:1px solid rgba(255,255,255,.15);
  box-shadow:0 25px 80px rgba(0,0,0,.7);
}

.modal h1{
  margin:0 0 8px;
  color:#ffd84d;
  text-align:center;
  font-size:clamp(25px,6vw,42px);
}

.modal p{
  color:#bdc9e5;
  text-align:center;
  line-height:1.4;
}

.saveGrid{
  display:grid;
  gap:10px;
  margin-top:18px;
}

.saveRow{
  display:flex;
  gap:8px;
}

.saveBtn{
  flex:1;
  min-height:58px;
  border-radius:13px;
  border:1px solid rgba(255,255,255,.16);
  color:white;
  background:#101a36;
  cursor:pointer;
  text-align:left;
  padding:10px 13px;
}

.saveBtn strong{
  display:block;
  color:#fff;
}

.saveBtn small{
  display:block;
  margin-top:3px;
  color:#91a3ca;
}

.deleteBtn{
  width:52px;
  border:0;
  border-radius:13px;
  color:white;
  background:#4a1220;
  font-size:18px;
  cursor:pointer;
}

.input{
  width:100%;
  padding:13px;
  margin:7px 0;
  border-radius:11px;
  border:1px solid rgba(255,255,255,.15);
  outline:none;
  background:#080e22;
  color:white;
}

.startBtn{
  width:100%;
  margin-top:12px;
  padding:14px;
  border:0;
  border-radius:13px;
  background:linear-gradient(90deg,#ffd21c,#ff9f1c);
  color:#171006;
  font-weight:900;
  cursor:pointer;
}

.gender{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:8px;
  margin-top:8px;
}

.gender button{
  padding:12px;
  border-radius:11px;
  border:1px solid rgba(255,255,255,.15);
  background:#101a36;
  color:white;
}

.gender button.selected{
  background:#294b91;
  border-color:#8eb5ff;
}

.hidden{
  display:none!important;
}

@media(max-height:650px){
  #arena{
    bottom:185px;
  }

  #controls{
    min-height:185px;
    padding:8px;
  }

  .attackBtn{
    min-height:45px;
    font-size:12px;
  }

  #verseBox{
    margin-top:5px;
    padding:5px;
  }

  #combatMessage{
    bottom:7px;
    font-size:12px;
  }
}

@media(max-width:520px){
  #topbar{
    min-height:55px;
  }

  #arena{
    top:55px;
  }

  #buttons{
    gap:7px;
  }

  .attackBtn{
    min-height:51px;
    font-size:12px;
  }
}
</style>
</head>

<body>

<div id="game">

<div id="stars"></div>

<div id="topbar">
  <div class="logo">SPIRITUAL POWER</div>
  <div id="levelText">SHADOWBOUND</div>
</div>

<div id="arena">

  <canvas id="battleCanvas"></canvas>

  <div id="hud">

    <div class="fighterHUD">
      <div class="hudName" id="playerNameHUD">WARRIOR</div>
      <div class="bar">
        <div class="fill" id="playerHP"></div>
      </div>
      <div class="hpText" id="playerHPText">100 / 100</div>
    </div>

    <div class="fighterHUD" style="text-align:right">
      <div class="hudName" id="enemyNameHUD">SHADOW DEMON</div>
      <div class="bar">
        <div class="fill" id="enemyHP"></div>
      </div>
      <div class="hpText" id="enemyHPText">100 / 100</div>
    </div>

  </div>

  <div id="turnText">YOUR TURN</div>

  <div id="combatMessage">
    Choose a save slot to begin your journey.
  </div>

</div>

<div id="controls">

  <div id="buttons">

    <button class="attackBtn" id="strikeBtn" onclick="spiritStrike()">
      ⚡ SPIRIT STRIKE
    </button>

    <button class="attackBtn" id="shieldBtn" onclick="shieldOfFate()">
      🛡️ SHIELD OF FATE
    </button>

    <button class="attackBtn" id="truthBtn" onclick="wordOfTruth()">
      ✨ WORD OF TRUTH
    </button>

    <button class="attackBtn" id="burstBtn" onclick="lightBurst()">
      ☀️ LIGHT BURST
    </button>

  </div>

  <div id="verseBox">
    <strong id="verseReference">Ephesians 6:11</strong>
    —
    <span id="verseText">
      Put on the whole armour of God, that ye may be able to stand against the wiles of the devil.
    </span>
  </div>

</div>

<div id="overlay">

  <div class="modal" id="saveModal">

    <h1>SPIRITUAL POWER</h1>

    <p>
      Choose a save slot. Your journey automatically saves as you progress.
    </p>

    <div class="saveGrid" id="saveGrid"></div>

  </div>

  <div class="modal hidden" id="customModal">

    <h1>CREATE WARRIOR</h1>

    <p>Customize your warrior before entering the Shadowbound realm.</p>

    <input class="input" id="nameInput"
           maxlength="18"
           placeholder="Warrior name">

    <div class="gender">
      <button id="maleBtn" onclick="chooseGender('male')">MALE</button>
      <button id="femaleBtn" onclick="chooseGender('female')">FEMALE</button>
    </div>

    <button class="startBtn" onclick="startGame()">
      BEGIN JOURNEY
    </button>

  </div>

</div>

</div>

<script>
/* =========================================================
   SPIRITUAL POWER: SHADOWBOUND
   Full game engine
   ========================================================= */

const canvas = document.getElementById("battleCanvas");
const ctx = canvas.getContext("2d");

const overlay = document.getElementById("overlay");
const saveModal = document.getElementById("saveModal");
const customModal = document.getElementById("customModal");

const saveGrid = document.getElementById("saveGrid");
const combatMessage = document.getElementById("combatMessage");
const turnText = document.getElementById("turnText");

const playerHPBar = document.getElementById("playerHP");
const enemyHPBar = document.getElementById("enemyHP");

const playerHPText = document.getElementById("playerHPText");
const enemyHPText = document.getElementById("enemyHPText");

const playerNameHUD = document.getElementById("playerNameHUD");
const enemyNameHUD = document.getElementById("enemyNameHUD");
const levelText = document.getElementById("levelText");

const verseReference = document.getElementById("verseReference");
const verseText = document.getElementById("verseText");

const strikeBtn = document.getElementById("strikeBtn");
const shieldBtn = document.getElementById("shieldBtn");
const truthBtn = document.getElementById("truthBtn");
const burstBtn = document.getElementById("burstBtn");

const SAVE_KEY = "spiritual_power_shadowbound_v4";

let selectedSlot = null;
let selectedGender = "male";

let running = false;
let busy = false;
let gameOver = false;

let shake = 0;
let flash = 0;

let particles = [];
let projectiles = [];
let beams = [];
let effects = [];

let animationTime = 0;

const player = {
  name:"Warrior",
  gender:"male",
  hp:100,
  maxHP:100,
  power:0,
  turns:0,
  shield:false,
  level:1
};

const enemy = {
  name:"Shadow Demon",
  hp:100,
  maxHP:100,
  level:1
};

const verses = [
  {
    ref:"Ephesians 6:11",
    text:"Put on the whole armour of God, that ye may be able to stand against the wiles of the devil."
  },
  {
    ref:"Psalm 18:2",
    text:"The LORD is my rock, and my fortress, and my deliverer; my God, my strength, in whom I will trust."
  },
  {
    ref:"1 John 4:4",
    text:"Greater is he that is in you, than he that is in the world."
  }
];

/* =========================================================
   CANVAS
   ========================================================= */

function resizeCanvas(){

  const rect = canvas.getBoundingClientRect();

  const dpr = Math.min(window.devicePixelRatio || 1,2);

  canvas.width = Math.floor(rect.width * dpr);
  canvas.height = Math.floor(rect.height * dpr);

  ctx.setTransform(dpr,0,0,dpr,0,0);
}

window.addEventListener("resize",resizeCanvas);

resizeCanvas();

/* =========================================================
   SAVE SYSTEM
   ========================================================= */

function getSaves(){

  try{
    return JSON.parse(localStorage.getItem(SAVE_KEY)) || {};
  }catch(e){
    return {};
  }
}

function writeSaves(saves){

  localStorage.setItem(SAVE_KEY,JSON.stringify(saves));
}

function saveGame(){

  if(selectedSlot === null) return;

  const saves = getSaves();

  saves[selectedSlot] = {
    name:player.name,
    gender:player.gender,
    hp:player.hp,
    maxHP:player.maxHP,
    power:player.power,
    turns:player.turns,
    level:player.level,
    enemyLevel:enemy.level,
    savedAt:Date.now()
  };

  writeSaves(saves);

  renderSaveSlots();
}

function renderSaveSlots(){

  const saves = getSaves();

  saveGrid.innerHTML = "";

  for(let i=0;i<3;i++){

    const row = document.createElement("div");
    row.className = "saveRow";

    const button = document.createElement("button");
    button.className = "saveBtn";

    const save = saves[i];

    if(save){

      button.innerHTML =
        `<strong>Save Slot ${i+1}</strong>
         <small>${escapeHTML(save.name || "Warrior")} • Level ${save.level || 1}</small>`;

      button.onclick = () => loadSave(i);

    }else{

      button.innerHTML =
        `<strong>Save Slot ${i+1}</strong>
         <small>Empty — create new journey</small>`;

      button.onclick = () => createNewSave(i);
    }

    row.appendChild(button);

    if(save){

      const del = document.createElement("button");
      del.className = "deleteBtn";
      del.textContent = "🗑";
      del.onclick = (event) => {

        event.stopPropagation();

        if(confirm("Delete this save slot?")){

          const current = getSaves();
          delete current[i];
          writeSaves(current);

          if(selectedSlot === i){
            selectedSlot = null;
          }

          renderSaveSlots();
        }
      };

      row.appendChild(del);
    }

    saveGrid.appendChild(row);
  }
}

function escapeHTML(value){

  return String(value)
    .replaceAll("&","&amp;")
    .replaceAll("<","&lt;")
    .replaceAll(">","&gt;")
    .replaceAll('"',"&quot;")
    .replaceAll("'","&#039;");
}

/* =========================================================
   NEW / LOAD GAME
   ========================================================= */

function createNewSave(slot){

  selectedSlot = slot;

  saveModal.classList.add("hidden");
  customModal.classList.remove("hidden");

  document.getElementById("nameInput").value = "";

  selectedGender = "male";
  updateGenderButtons();
}

function loadSave(slot){

  const saves = getSaves();
  const s = saves[slot];

  if(!s){
    createNewSave(slot);
    return;
  }

  selectedSlot = slot;

  player.name = s.name || "Warrior";
  player.gender = s.gender || "male";
  player.maxHP = s.maxHP || 100;
  player.hp = Math.max(1,Math.min(s.hp ?? player.maxHP,player.maxHP));
  player.power = s.power || 0;
  player.turns = s.turns || 0;
  player.level = s.level || 1;
  player.shield = false;

  setupLevel(s.enemyLevel || player.level);

  /*
     IMPORTANT:
     setupLevel creates the enemy, but we restore the
     saved player progress AFTER setupLevel.
  */
  player.hp = Math.max(1,Math.min(s.hp ?? player.maxHP,player.maxHP));
  player.power = s.power || 0;
  player.turns = s.turns || 0;
  player.shield = false;

  overlay.style.display = "none";

  running = true;
  busy = false;
  gameOver = false;

  turnText.textContent = "YOUR TURN";

  say(`Welcome back, ${player.name}. The ${enemy.name} awaits.`);

  setButtons(true);
  updateHUD();
  saveGame();
}

function startGame(){

  const input = document.getElementById("nameInput");

  const enteredName = input.value.trim();

  player.name = enteredName || "Warrior";
  player.gender = selectedGender;

  player.maxHP = 100;
  player.hp = 100;
  player.power = 0;
  player.turns = 0;
  player.shield = false;
  player.level = 1;

  setupLevel(1);

  overlay.style.display = "none";

  running = true;
  busy = false;
  gameOver = false;

  turnText.textContent = "YOUR TURN";

  say(`Welcome, ${player.name}. Your journey begins now.`);

  setButtons(true);

  saveGame();
}

function chooseGender(gender){

  selectedGender = gender;

  updateGenderButtons();
}

function updateGenderButtons(){

  document.getElementById("maleBtn")
    .classList.toggle("selected",selectedGender === "male");

  document.getElementById("femaleBtn")
    .classList.toggle("selected",selectedGender === "female");
}

/* =========================================================
   LEVELS
   ========================================================= */

function setupLevel(level){

  player.level = level;

  if(level === 1){

    enemy.name = "Shadow Demon";
    enemy.level = 1;
    enemy.maxHP = 100;
    enemy.hp = enemy.maxHP;

  }else if(level === 2){

    enemy.name = "Dark Angel";
    enemy.level = 2;
    enemy.maxHP = 155;
    enemy.hp = enemy.maxHP;

  }else{

    enemy.name = "Shadow Colossus";
    enemy.level = 3;
    enemy.maxHP = 260;
    enemy.hp = enemy.maxHP;
  }

  player.hp = player.maxHP;
  player.turns = 0;
  player.shield = false;

  updateHUD();
  updateVerse();
}

function updateVerse(){

  const verse = verses[(player.level - 1) % verses.length];

  verseReference.textContent = verse.ref;
  verseText.textContent = verse.text;
}

function winLevel(){

  busy = true;
  setButtons(false);

  spawnBurst(enemyX(),enemyY(),80);
  shake = 14;

  if(player.level >= 3){

    setTimeout(()=>{

      gameOver = true;
      running = false;

      turnText.textContent = "VICTORY";

      say(
        `You defeated the ${enemy.name}. The Shadowbound realm has been overcome.`
      );

      saveGame();

    },1000);

    return;
  }

  const nextLevel = player.level + 1;

  setTimeout(()=>{

    /*
      Full heal between stages.
      This preserves the original level progression behavior.
    */
    player.hp = player.maxHP;
    player.turns = 0;
    player.shield = false;

    setupLevel(nextLevel);

    busy = false;

    turnText.textContent = "YOUR TURN";

    say(
      `Level ${nextLevel}! A ${enemy.name} has appeared.`
    );

    setButtons(true);

    saveGame();

  },1000);
}

/* =========================================================
   HUD
   ========================================================= */

function updateHUD(){

  playerNameHUD.textContent = player.name.toUpperCase();
  enemyNameHUD.textContent = enemy.name.toUpperCase();

  levelText.textContent =
    `LEVEL ${player.level} • SPIRIT POWER ${player.power}`;

  playerHPBar.style.width =
    `${Math.max(0,player.hp/player.maxHP*100)}%`;

  enemyHPBar.style.width =
    `${Math.max(0,enemy.hp/enemy.maxHP*100)}%`;

  playerHPText.textContent =
    `${Math.max(0,Math.ceil(player.hp))} / ${player.maxHP}`;

  enemyHPText.textContent =
    `${Math.max(0,Math.ceil(enemy.hp))} / ${enemy.maxHP}`;

  burstBtn.disabled = player.turns < 3 || busy || !running;
}

function say(text){

  combatMessage.textContent = text;
}

function setButtons(enabled){

  const active = enabled && running && !busy && !gameOver;

  strikeBtn.disabled = !active;
  shieldBtn.disabled = !active;
  truthBtn.disabled = !active;

  burstBtn.disabled =
    !active || player.turns < 3;
}

/* =========================================================
   PLAYER ATTACKS
   ========================================================= */

function spiritStrike(){

  if(!canAttack()) return;

  beginPlayerAction();

  say(`${player.name} charges forward with Spirit Strike!`);

  effects.push({
    type:"charge",
    side:"player",
    life:1
  });

  setTimeout(()=>{

    projectiles.push({
      x:playerX()+55,
      y:playerY()-35,
      vx:10,
      vy:-.1,
      size:11,
      life:80,
      type:"light"
    });

  },300);

  setTimeout(()=>{

    damageEnemy(22);
    finishPlayerAttack();

  },700);
}

function shieldOfFate(){

  if(!canAttack()) return;

  beginPlayerAction();

  player.shield = true;

  say(`${player.name} raises the Shield of Fate!`);

  effects.push({
    type:"shield",
    side:"player",
    life:55
  });

  spawnBurst(playerX()+45,playerY()-35,25);

  setTimeout(()=>{

    finishPlayerAttack();

  },650);
}

function wordOfTruth(){

  if(!canAttack()) return;

  beginPlayerAction();

  say(`The Word of Truth releases a beam of light!`);

  setTimeout(()=>{

    beams.push({
      x:playerX()+55,
      y:playerY()-35,
      targetX:enemyX()-35,
      targetY:enemyY()-35,
      life:22,
      maxLife:22
    });

    damageEnemy(32);

  },450);

  setTimeout(()=>{

    finishPlayerAttack();

  },750);
}

function lightBurst(){

  if(!canAttack()) return;

  if(player.turns < 3) return;

  beginPlayerAction();

  say(
    `${player.name} unleashes LIGHT BURST!`
  );

  setTimeout(()=>{

    beams.push({
      x:playerX()+55,
      y:playerY()-50,
      targetX:enemyX()-30,
      targetY:enemyY()-45,
      life:35,
      maxLife:35,
      huge:true
    });

    spawnBurst(enemyX(),enemyY(),65);

    damageEnemy(55);

  },500);

  setTimeout(()=>{

    finishPlayerAttack();

  },900);
}

function canAttack(){

  return running &&
         !busy &&
         !gameOver &&
         player.hp > 0 &&
         enemy.hp > 0;
}

function beginPlayerAction(){

  busy = true;
  setButtons(false);
}

function finishPlayerAttack(){

  if(enemy.hp <= 0){

    winLevel();
    return;
  }

  player.turns++;

  /*
    The player must survive more than 3 enemy turns.
    Light Burst unlocks at 3 survived enemy turns.
  */

  setTimeout(()=>{

    enemyTurn();

  },450);
}

/* =========================================================
   ENEMY TURN
   ========================================================= */

function enemyTurn(){

  if(gameOver || enemy.hp <= 0 || player.hp <= 0) return;

  turnText.textContent = "ENEMY TURN";

  say(`${enemy.name} prepares an attack...`);

  effects.push({
    type:"enemyAttack",
    life:45
  });

  setTimeout(()=>{

    let damage;

    if(enemy.level === 1){
      damage = 14 + Math.floor(Math.random()*7);
    }else if(enemy.level === 2){
      damage = 19 + Math.floor(Math.random()*9);
    }else{
      damage = 25 + Math.floor(Math.random()*11);
    }

    if(player.shield){

      damage = Math.floor(damage * .18);

      say(
        `${player.name}'s Shield of Fate blocks most of the attack!`
      );

      spawnBurst(playerX()+45,playerY()-35,28);

    }else{

      say(
        `${enemy.name} strikes for ${damage} damage!`
      );

    }

    player.hp -= damage;

    if(player.hp < 0) player.hp = 0;

    player.shield = false;

    shake = player.hp > 0 ? 7 : 15;

    flash = 8;

    updateHUD();

    if(player.hp <= 0){

      loseGame();
      return;
    }

    turnText.textContent = "YOUR TURN";

    busy = false;

    setButtons(true);

    saveGame();

  },650);
}

/* =========================================================
   DAMAGE
   ========================================================= */

function damageEnemy(amount){

  if(enemy.hp <= 0) return;

  enemy.hp -= amount;

  if(enemy.hp < 0) enemy.hp = 0;

  player.power += Math.ceil(amount / 4);

  shake = 8;
  flash = 5;

  spawnBurst(enemyX(),enemyY()-35,30);

  updateHUD();

  if(enemy.hp <= 0){

    say(`${enemy.name} has fallen!`);

  }
}

function loseGame(){

  running = false;
  gameOver = true;
  busy = true;

  setButtons(false);

  turnText.textContent = "DEFEATED";

  say(
    `${player.name} was defeated. Your save remains available.`
  );

  saveGame();

  setTimeout(()=>{

    const again = confirm(
      "You were defeated. Restart this level?"
    );

    if(again){

      player.hp = player.maxHP;
      player.turns = 0;
      player.shield = false;

      setupLevel(player.level);

      running = true;
      gameOver = false;
      busy = false;

      turnText.textContent = "YOUR TURN";

      say(
        `Rise again, ${player.name}. The ${enemy.name} awaits.`
      );

      setButtons(true);

      saveGame();

    }else{

      overlay.style.display = "flex";
      saveModal.classList.remove("hidden");
      customModal.classList.add("hidden");

      renderSaveSlots();
    }

  },700);
}

/* =========================================================
   CHARACTER POSITIONS
   ========================================================= */

function playerX(){

  return canvas.clientWidth * .23;
}

function enemyX(){

  return canvas.clientWidth * .77;
}

function playerY(){

  return canvas.clientHeight * .66;
}

function enemyY(){

  return canvas.clientHeight * .66;
}

/* =========================================================
   PARTICLES
   ========================================================= */

function spawnBurst(x,y,count){

  for(let i=0;i<count;i++){

    const angle = Math.random()*Math.PI*2;
    const speed = 1+Math.random()*5;

    particles.push({
      x,
      y,
      vx:Math.cos(angle)*speed,
      vy:Math.sin(angle)*speed,
      life:25+Math.random()*35,
      size:2+Math.random()*5,
      glow:Math.random()*10
    });
  }
}

/* =========================================================
   DRAWING
   ========================================================= */

function drawBackground(w,h){

  const g = ctx.createLinearGradient(0,0,0,h);

  g.addColorStop(0,"#101a3b");
  g.addColorStop(.55,"#080d20");
  g.addColorStop(1,"#02030a");

  ctx.fillStyle = g;
  ctx.fillRect(0,0,w,h);

  /*
    Moon / spiritual light
  */

  const moonX = w*.5;
  const moonY = h*.25;
  const moonR = Math.min(w,h)*.12;

  const glow = ctx.createRadialGradient(
    moonX,moonY,0,
    moonX,moonY,moonR*2.4
  );

  glow.addColorStop(0,"rgba(170,205,255,.25)");
  glow.addColorStop(1,"rgba(170,205,255,0)");

  ctx.fillStyle = glow;
  ctx.beginPath();
  ctx.arc(moonX,moonY,moonR*2.4,0,Math.PI*2);
  ctx.fill();

  ctx.fillStyle = "rgba(210,230,255,.12)";
  ctx.beginPath();
  ctx.arc(moonX,moonY,moonR,0,Math.PI*2);
  ctx.fill();

  /*
    Ground
  */

  ctx.fillStyle = "#03050e";
  ctx.beginPath();
  ctx.ellipse(
    w*.5,
    h*.86,
    w*.47,
    h*.12,
    0,0,Math.PI*2
  );
  ctx.fill();

  /*
    Ground glow
  */

  const groundGlow = ctx.createRadialGradient(
    w*.5,h*.75,0,
    w*.5,h*.75,w*.48
  );

  groundGlow.addColorStop(0,"rgba(48,104,255,.14)");
  groundGlow.addColorStop(1,"rgba(0,0,0,0)");

  ctx.fillStyle = groundGlow;
  ctx.fillRect(0,h*.55,w,h*.45);
}

/* =========================================================
   ARTICULATED PLAYER
   ========================================================= */

function drawPlayer(){

  const x = playerX();
  const y = playerY();

  const bob = Math.sin(animationTime*.005)*3;

  let charge = 0;

  for(const e of effects){

    if(e.type === "charge" && e.side === "player"){

      charge = Math.sin((1-e.life)*Math.PI)*30;
    }
  }

  drawWarrior(
    x + charge,
    y + bob,
    1,
    player.gender,
    true
  );
}

/* =========================================================
   ARTICULATED ENEMY
   ========================================================= */

function drawEnemy(){

  const x = enemyX();
  const y = enemyY();

  const bob =
    Math.sin(animationTime*.004 + 2)*4;

  if(enemy.level === 1){

    drawDemon(x,y+bob,1);

  }else if(enemy.level === 2){

    drawDarkAngel(x,y+bob,1.08);

  }else{

    drawColossus(x,y+bob,1.35);
  }
}

/* =========================================================
   WARRIOR
   ========================================================= */

function drawWarrior(x,y,s,gender,isPlayer){

  ctx.save();

  ctx.translate(x,y);
  ctx.scale(s,s);

  const moving =
    effects.some(e=>e.type==="charge" && e.side==="player");

  const armMove =
    moving ? Math.sin(animationTime*.025)*.45 : 0;

  const legMove =
    moving ? Math.sin(animationTime*.025)*.25 : 0;

  /*
    Aura
  */

  const aura = ctx.createRadialGradient(
    0,-55,5,
    0,-55,90
  );

  aura.addColorStop(0,"rgba(255,230,80,.15)");
  aura.addColorStop(1,"rgba(255,220,50,0)");

  ctx.fillStyle = aura;
  ctx.beginPath();
  ctx.arc(0,-55,90,0,Math.PI*2);
  ctx.fill();

  /*
    Legs
  */

  drawLimb(
    -15,5,
    -20,55+legMove,
    -25,100+legMove,
    13,
    "#18223b",
    "#d9a92b"
  );

  drawLimb(
    15,5,
    20,55-legMove,
    25,100-legMove,
    13,
    "#18223b",
    "#d9a92b"
  );

  /*
    Boots
  */

  ctx.fillStyle="#111522";

  roundRect(-38,96,30,12,5);
  ctx.fill();

  roundRect(8,96,30,12,5);
  ctx.fill();

  /*
    Body armor
  */

  const armor =
    ctx.createLinearGradient(-35,-50,35,40);

  armor.addColorStop(0,"#e9f1ff");
  armor.addColorStop(.4,"#7691c4");
  armor.addColorStop(1,"#243352");

  ctx.fillStyle=armor;

  roundRect(-34,-55,68,65,16);
  ctx.fill();

  /*
    Chest core
  */

  const coreGlow =
    ctx.createRadialGradient(0,-24,1,0,-24,19);

  coreGlow.addColorStop(0,"#fffbd0");
  coreGlow.addColorStop(.35,"#ffe34f");
  coreGlow.addColorStop(1,"rgba(255,204,30,0)");

  ctx.fillStyle=coreGlow;

  ctx.beginPath();
  ctx.arc(0,-24,20,0,Math.PI*2);
  ctx.fill();

  ctx.fillStyle="#fff5a0";
  ctx.beginPath();
  ctx.arc(0,-24,7,0,Math.PI*2);
  ctx.fill();

  /*
    Arms with actual joints
  */

  drawLimb(
    -29,-42,
    -52,-8 + armMove*20,
    -60,25 + armMove*30,
    11,
    "#6e86b7",
    "#d7a927"
  );

  drawLimb(
    29,-42,
    52,-8 - armMove*20,
    60,25 - armMove*30,
    11,
    "#6e86b7",
    "#d7a927"
  );

  /*
    Hands
  */

  drawHand(-60,25 + armMove*30);
  drawHand(60,25 - armMove*30);

  /*
    Neck
  */

  ctx.fillStyle="#b9c9df";
  roundRect(-11,-70,22,18,7);
  ctx.fill();

  /*
    Head
  */

  const skin =
    ctx.createLinearGradient(-22,-115,22,-70);

  skin.addColorStop(0,"#f1d1b5");
  skin.addColorStop(1,"#a8755b");

  ctx.fillStyle=skin;

  ctx.beginPath();
  ctx.arc(0,-92,24,0,Math.PI*2);
  ctx.fill();

  /*
    Hair
  */

  ctx.fillStyle="#151a28";

  ctx.beginPath();
  ctx.arc(0,-102,24,Math.PI,Math.PI*2);
  ctx.lineTo(20,-89);
  ctx.lineTo(-20,-89);
  ctx.closePath();
  ctx.fill();

  /*
    Helmet crest
  */

  ctx.fillStyle="#ffd63b";

  ctx.beginPath();
  ctx.moveTo(0,-124);
  ctx.lineTo(8,-105);
  ctx.lineTo(0,-110);
  ctx.lineTo(-8,-105);
  ctx.closePath();
  ctx.fill();

  /*
    Eyes
  */

  ctx.fillStyle="#111827";

  ctx.beginPath();
  ctx.arc(-8,-92,2.5,0,Math.PI*2);
  ctx.arc(8,-92,2.5,0,Math.PI*2);
  ctx.fill();

  /*
    Shield
  */

  if(player.shield){

    const sx = -52;
    const sy = 4;

    ctx.save();

    ctx.globalAlpha=.9;

    const shield =
      ctx.createRadialGradient(
        sx,sy,5,
        sx,sy,48
      );

    shield.addColorStop(0,"rgba(255,248,150,.55)");
    shield.addColorStop(.45,"rgba(255,215,50,.2)");
    shield.addColorStop(1,"rgba(255,215,50,0)");

    ctx.fillStyle=shield;

    ctx.beginPath();
    ctx.arc(sx,sy,48,0,Math.PI*2);
    ctx.fill();

    ctx.strokeStyle="#ffe16a";
    ctx.lineWidth=3;

    ctx.beginPath();
    ctx.arc(sx,sy,35,0,Math.PI*2);
    ctx.stroke();

    ctx.restore();
  }

  ctx.restore();
}

/* =========================================================
   LIMBS
   ========================================================= */

function drawLimb(x1,y1,x2,y2,x3,y3,width,base,joint){

  ctx.strokeStyle=base;
  ctx.lineWidth=width;
  ctx.lineCap="round";

  ctx.beginPath();
  ctx.moveTo(x1,y1);
  ctx.lineTo(x2,y2);
  ctx.lineTo(x3,y3);
  ctx.stroke();

  ctx.fillStyle=joint;

  ctx.beginPath();
  ctx.arc(x2,y2,width*.55,0,Math.PI*2);
  ctx.fill();

  ctx.strokeStyle="rgba(255,255,255,.2)";
  ctx.lineWidth=2;

  ctx.beginPath();
  ctx.moveTo(x1,y1);
  ctx.lineTo(x2,y2);
  ctx.lineTo(x3,y3);
  ctx.stroke();
}

function drawHand(x,y){

  ctx.fillStyle="#e2bd9e";

  ctx.beginPath();
  ctx.arc(x,y,8,0,Math.PI*2);
  ctx.fill();
}

/* =========================================================
   DEMON
   ========================================================= */

function drawDemon(x,y,s){

  ctx.save();

  ctx.translate(x,y);
  ctx.scale(s,s);

  const pulse =
    Math.sin(animationTime*.006)*3;

  /*
    Shadow aura
  */

  const aura =
    ctx.createRadialGradient(
      0,-35,10,
      0,-35,100
    );

  aura.addColorStop(0,"rgba(180,10,50,.28)");
  aura.addColorStop(1,"rgba(120,0,30,0)");

  ctx.fillStyle=aura;

  ctx.beginPath();
  ctx.arc(0,-35,100,0,Math.PI*2);
  ctx.fill();

  /*
    Wings
  */

  ctx.fillStyle="#160914";

  ctx.beginPath();
  ctx.moveTo(-25,-55);
  ctx.lineTo(-95,-95);
  ctx.lineTo(-65,-45);
  ctx.lineTo(-105,-35);
  ctx.lineTo(-42,-10);
  ctx.closePath();
  ctx.fill();

  ctx.beginPath();
  ctx.moveTo(25,-55);
  ctx.lineTo(95,-95);
  ctx.lineTo(65,-45);
  ctx.lineTo(105,-35);
  ctx.lineTo(42,-10);
  ctx.closePath();
  ctx.fill();

  /*
    Legs
  */

  drawLimb(
    -15,5,
    -25,55,
    -33,100,
    15,
    "#28111d",
    "#8b1834"
  );

  drawLimb(
    15,5,
    25,55,
    33,100,
    15,
    "#28111d",
    "#8b1834"
  );

  /*
    Body
  */

  ctx.fillStyle="#35101e";
  roundRect(-35,-65,70,75,18);
  ctx.fill();

  ctx.strokeStyle="#b71943";
  ctx.lineWidth=3;

  roundRect(-35,-65,70,75,18);
  ctx.stroke();

  /*
    Arms
  */

  drawLimb(
    -30,-40,
    -55,-5,
    -65,25,
    13,
    "#34101c",
    "#9f1b3e"
  );

  drawLimb(
    30,-40,
    55,-5,
    65,25,
    13,
    "#34101c",
    "#9f1b3e"
  );

  /*
    Head
  */

  ctx.fillStyle="#4d1524";

  ctx.beginPath();
  ctx.arc(0,-88,28,0,Math.PI*2);
  ctx.fill();

  /*
    Horns
  */

  ctx.fillStyle="#d8b48e";

  ctx.beginPath();
  ctx.moveTo(-18,-107);
  ctx.lineTo(-36,-140);
  ctx.lineTo(-7,-112);
  ctx.closePath();
  ctx.fill();

  ctx.beginPath();
  ctx.moveTo(18,-107);
  ctx.lineTo(36,-140);
  ctx.lineTo(7,-112);
  ctx.closePath();
  ctx.fill();

  /*
    Eyes
  */

  ctx.fillStyle="#ff334f";

  ctx.shadowBlur=15;
  ctx.shadowColor="#ff193f";

  ctx.beginPath();
  ctx.ellipse(-9,-88,5,3,0,0,Math.PI*2);
  ctx.ellipse(9,-88,5,3,0,0,Math.PI*2);
  ctx.fill();

  ctx.shadowBlur=0;

  /*
    Claws
  */

  ctx.strokeStyle="#d8b48e";
  ctx.lineWidth=3;

  ctx.beginPath();
  ctx.moveTo(-66,25);
  ctx.lineTo(-73,34);
  ctx.moveTo(-62,25);
  ctx.lineTo(-66,36);
  ctx.moveTo(66,25);
  ctx.lineTo(73,34);
  ctx.moveTo(62,25);
  ctx.lineTo(66,36);
  ctx.stroke();

  ctx.restore();
}

/* =========================================================
   DARK ANGEL
   ========================================================= */

function drawDarkAngel(x,y,s){

  ctx.save();

  ctx.translate(x,y);
  ctx.scale(s,s);

  const wingWave =
    Math.sin(animationTime*.004)*5;

  /*
    Large dark wings
  */

  ctx.fillStyle="#161829";

  ctx.beginPath();
  ctx.moveTo(-22,-55);
  ctx.quadraticCurveTo(-95,-110-wingWave,-115,-45);
  ctx.quadraticCurveTo(-75,-65,-40,-10);
  ctx.closePath();
  ctx.fill();

  ctx.beginPath();
  ctx.moveTo(22,-55);
  ctx.quadraticCurveTo(95,-110-wingWave,115,-45);
  ctx.quadraticCurveTo(75,-65,40,-10);
  ctx.closePath();
  ctx.fill();

  /*
    Armor
  */

  ctx.fillStyle="#263052";
  roundRect(-38,-62,76,75,17);
  ctx.fill();

  ctx.strokeStyle="#7c8fd0";
  ctx.lineWidth=3;
  roundRect(-38,-62,76,75,17);
  ctx.stroke();

  /*
    Arms
  */

  drawLimb(
    -32,-40,
    -62,-3,
    -70,28,
    13,
    "#394b7a",
    "#a7b6ef"
  );

  drawLimb(
    32,-40,
    62,-3,
    70,28,
    13,
    "#394b7a",
    "#a7b6ef"
  );

  /*
    Legs
  */

  drawLimb(
    -16,10,
    -23,57,
    -28,100,
    15,
    "#252f50",
    "#7887bc"
  );

  drawLimb(
    16,10,
    23,57,
    28,100,
    15,
    "#252f50",
    "#7887bc"
  );

  /*
    Head
  */

  ctx.fillStyle="#d5bda9";

  ctx.beginPath();
  ctx.arc(0,-91,25,0,Math.PI*2);
  ctx.fill();

  /*
    Dark halo
  */

  ctx.strokeStyle="#6f5cff";
  ctx.lineWidth=5;
  ctx.shadowBlur=20;
  ctx.shadowColor="#6f5cff";

  ctx.beginPath();
  ctx.arc(0,-95,34,0,Math.PI*2);
  ctx.stroke();

  ctx.shadowBlur=0;

  /*
    Hair
  */

  ctx.fillStyle="#10111b";

  ctx.beginPath();
  ctx.arc(0,-101,24,Math.PI,Math.PI*2);
  ctx.fill();

  /*
    Eyes
  */

  ctx.fillStyle="#8b6cff";

  ctx.beginPath();
  ctx.arc(-8,-91,3,0,Math.PI*2);
  ctx.arc(8,-91,3,0,Math.PI*2);
  ctx.fill();

  ctx.restore();
}

/* =========================================================
   COLOSSUS
   ========================================================= */

function drawColossus(x,y,s){

  ctx.save();

  ctx.translate(x,y);
  ctx.scale(s,s);

  /*
    Giant aura
  */

  const aura =
    ctx.createRadialGradient(
      0,-70,10,
      0,-70,160
    );

  aura.addColorStop(0,"rgba(92,52,170,.28)");
  aura.addColorStop(1,"rgba(30,0,70,0)");

  ctx.fillStyle=aura;

  ctx.beginPath();
  ctx.arc(0,-70,160,0,Math.PI*2);
  ctx.fill();

  /*
    Huge wings
  */

  ctx.fillStyle="#100d1e";

  ctx.beginPath();
  ctx.moveTo(-45,-70);
  ctx.lineTo(-170,-150);
  ctx.lineTo(-120,-65);
  ctx.lineTo(-185,-45);
  ctx.lineTo(-65,-10);
  ctx.closePath();
  ctx.fill();

  ctx.beginPath();
  ctx.moveTo(45,-70);
  ctx.lineTo(170,-150);
  ctx.lineTo(120,-65);
  ctx.lineTo(185,-45);
  ctx.lineTo(65,-10);
  ctx.closePath();
  ctx.fill();

  /*
    Huge body
  */

  ctx.fillStyle="#29163c";
  roundRect(-55,-90,110,115,25);
  ctx.fill();

  ctx.strokeStyle="#8952c8";
  ctx.lineWidth=5;
  roundRect(-55,-90,110,115,25);
  ctx.stroke();

  /*
    Arms
  */

  drawLimb(
    -45,-65,
    -85,-5,
    -105,45,
    22,
    "#35204b",
    "#9155c5"
  );

  drawLimb(
    45,-65,
    85,-5,
    105,45,
    22,
    "#35204b",
    "#9155c5"
  );

  /*
    Legs
  */

  drawLimb(
    -25,20,
    -38,85,
    -45,140,
    23,
    "#271737",
    "#7340a7"
  );

  drawLimb(
    25,20,
    38,85,
    45,140,
    23,
    "#271737",
    "#7340a7"
  );

  /*
    Head
  */

  ctx.fillStyle="#45235a";

  ctx.beginPath();
  ctx.arc(0,-122,40,0,Math.PI*2);
  ctx.fill();

  /*
    Horns
  */

  ctx.fillStyle="#b48ad7";

  ctx.beginPath();
  ctx.moveTo(-25,-150);
  ctx.lineTo(-55,-205);
  ctx.lineTo(-8,-160);
  ctx.closePath();
  ctx.fill();

  ctx.beginPath();
  ctx.moveTo(25,-150);
  ctx.lineTo(55,-205);
  ctx.lineTo(8,-160);
  ctx.closePath();
  ctx.fill();

  /*
    Eyes
  */

  ctx.fillStyle="#ff3158";
  ctx.shadowBlur=22;
  ctx.shadowColor="#ff3158";

  ctx.beginPath();
  ctx.arc(-13,-123,6,0,Math.PI*2);
  ctx.arc(13,-123,6,0,Math.PI*2);
  ctx.fill();

  ctx.shadowBlur=0;

  ctx.restore();
}

/* =========================================================
   UTILITY SHAPE
   ========================================================= */

function roundRect(x,y,w,h,r){

  ctx.beginPath();

  ctx.roundRect(x,y,w,h,r);
}

/* =========================================================
   EFFECT DRAWING
   ========================================================= */

function drawProjectile(p){

  ctx.save();

  ctx.globalAlpha =
    Math.max(0,p.life/80);

  const glow =
    ctx.createRadialGradient(
      p.x,p.y,0,
      p.x,p.y,p.size*3
    );

  glow.addColorStop(0,"rgba(255,255,230,1)");
  glow.addColorStop(.35,"rgba(255,224,70,.9)");
  glow.addColorStop(1,"rgba(255,190,30,0)");

  ctx.fillStyle=glow;

  ctx.beginPath();
  ctx.arc(p.x,p.y,p.size*3,0,Math.PI*2);
  ctx.fill();

  ctx.fillStyle="#fffbd0";

  ctx.beginPath();
  ctx.arc(p.x,p.y,p.size,0,Math.PI*2);
  ctx.fill();

  ctx.restore();
}

function drawBeam(b){

  const alpha =
    b.life / b.maxLife;

  ctx.save();

  ctx.globalAlpha=alpha;

  const width = b.huge ? 32 : 16;

  ctx.strokeStyle="rgba(255,240,100,.3)";
  ctx.lineWidth=width*2.4;
  ctx.lineCap="round";

  ctx.beginPath();
  ctx.moveTo(b.x,b.y);
  ctx.lineTo(b.targetX,b.targetY);
  ctx.stroke();

  ctx.strokeStyle="#fff7a0";
  ctx.lineWidth=width;
  ctx.shadowBlur=25;
  ctx.shadowColor="#ffe33d";

  ctx.beginPath();
  ctx.moveTo(b.x,b.y);
  ctx.lineTo(b.targetX,b.targetY);
  ctx.stroke();

  ctx.strokeStyle="#ffffff";
  ctx.lineWidth=width*.35;

  ctx.beginPath();
  ctx.moveTo(b.x,b.y);
  ctx.lineTo(b.targetX,b.targetY);
  ctx.stroke();

  ctx.restore();
}

/* =========================================================
   UPDATE EFFECTS
   ========================================================= */

function updateEffects(){

  for(let i=particles.length-1;i>=0;i--){

    const p=particles[i];

    p.x += p.vx;
    p.y += p.vy;

    p.vx *= .98;
    p.vy *= .98;

    p.vy += .035;

    p.life--;

    if(p.life<=0){
      particles.splice(i,1);
    }
  }

  for(let i=projectiles.length-1;i>=0;i--){

    const p=projectiles[i];

    p.x += p.vx;
    p.y += p.vy;

    p.life--;

    if(p.life<=0){
      projectiles.splice(i,1);
    }
  }

  for(let i=beams.length-1;i>=0;i--){

    beams[i].life--;

    if(beams[i].life<=0){
      beams.splice(i,1);
    }
  }

  for(let i=effects.length-1;i>=0;i--){

    effects[i].life--;

    if(effects[i].life<=0){
      effects.splice(i,1);
    }
  }

  if(shake>0){
    shake*=.84;
    if(shake<.2) shake=0;
  }

  if(flash>0) flash--;
}

/* =========================================================
   RENDER
   ========================================================= */

function render(){

  const w=canvas.clientWidth;
  const h=canvas.clientHeight;

  ctx.clearRect(0,0,w,h);

  ctx.save();

  if(shake>0){

    ctx.translate(
      (Math.random()-.5)*shake,
      (Math.random()-.5)*shake
    );
  }

  drawBackground(w,h);

  drawEnemy();
  drawPlayer();

  for(const b of beams){
    drawBeam(b);
  }

  for(const p of projectiles){
    drawProjectile(p);
  }

  /*
    Particles
  */

  for(const p of particles){

    ctx.save();

    ctx.globalAlpha =
      Math.max(0,p.life/50);

    ctx.fillStyle="#ffe76b";

    ctx.shadowBlur=p.glow;
    ctx.shadowColor="#ffe76b";

    ctx.beginPath();
    ctx.arc(
      p.x,
      p.y,
      p.size,
      0,
      Math.PI*2
    );

    ctx.fill();

    ctx.restore();
  }

  /*
    Hit flash
  */

  if(flash>0){

    ctx.fillStyle =
      `rgba(255,255,255,${flash/35})`;

    ctx.fillRect(0,0,w,h);
  }

  ctx.restore();

  updateEffects();

  animationTime =
    performance.now();

  requestAnimationFrame(render);
}

/* =========================================================
   START RENDER LOOP
   ========================================================= */

render();

/* =========================================================
   INITIALIZATION
   ========================================================= */

renderSaveSlots();

setButtons(false);

say("Choose a save slot to begin your journey.");

/*
  Prevent accidental double taps from causing weird
  simultaneous attacks.
*/

document.addEventListener("visibilitychange",()=>{

  if(document.hidden){

    /*
      Do not reset combat or destroy the save.
      The game simply waits while the page is hidden.
    */

    if(running){
      saveGame();
    }
  }
});

window.addEventListener("beforeunload",()=>{

  if(running){
    saveGame();
  }
});
</script>

</body>
</html>
