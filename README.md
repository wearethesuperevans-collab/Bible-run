<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport"
      content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>Spiritual Power: Shadowbound</title>

<style>
*{
  box-sizing:border-box;
  -webkit-tap-highlight-color:transparent;
}

body{
  margin:0;
  font-family:Arial,Helvetica,sans-serif;
  background:
    radial-gradient(circle at 50% 15%,#26385d 0%,#101626 35%,#05070d 75%);
  color:white;
  min-height:100vh;
  overflow-x:hidden;
}

button,input,select{
  font:inherit;
}

button{
  cursor:pointer;
}

.hidden{
  display:none!important;
}

/* ---------- MAIN ---------- */

#app{
  width:100%;
  max-width:1100px;
  margin:auto;
  min-height:100vh;
  padding:14px;
}

.panel{
  background:rgba(9,13,25,.88);
  border:1px solid rgba(255,255,255,.12);
  border-radius:20px;
  box-shadow:
    0 15px 50px rgba(0,0,0,.5),
    inset 0 1px rgba(255,255,255,.08);
  padding:18px;
}

h1{
  text-align:center;
  margin:5px 0 18px;
  font-size:clamp(28px,6vw,48px);
  letter-spacing:2px;
  text-shadow:0 0 20px #ffd45a;
}

h2{
  margin-top:0;
}

/* ---------- SAVE SCREEN ---------- */

.saveGrid{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:14px;
}

.saveCard{
  min-height:150px;
  border:1px solid #47506a;
  background:linear-gradient(145deg,#151c30,#080c17);
  border-radius:18px;
  padding:18px;
  display:flex;
  flex-direction:column;
  justify-content:space-between;
  transition:.2s;
}

.saveCard:hover{
  transform:translateY(-3px);
  border-color:#ffd45a;
  box-shadow:0 0 25px rgba(255,212,90,.18);
}

.goldBtn{
  border:0;
  border-radius:12px;
  padding:13px 16px;
  color:#17120a;
  font-weight:900;
  background:linear-gradient(180deg,#fff0a2,#ffc62e,#c88b08);
  box-shadow:0 5px 15px rgba(255,194,40,.25);
}

.redBtn{
  border:1px solid #7e3040;
  background:#32121b;
  color:#ff9aaa;
  border-radius:10px;
  padding:10px;
  font-weight:bold;
}

button:active{
  transform:scale(.96);
}

/* ---------- CUSTOMIZATION ---------- */

.custom{
  max-width:650px;
  margin:auto;
}

.field{
  margin:13px 0;
}

.field label{
  display:block;
  margin-bottom:6px;
  color:#cbd3e7;
}

input,select{
  width:100%;
  padding:13px;
  border-radius:10px;
  border:1px solid #414c68;
  background:#0b1020;
  color:white;
  outline:none;
}

.colorRow{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:12px;
}

input[type="color"]{
  height:50px;
  padding:3px;
}

/* ---------- GAME HUD ---------- */

#game{
  position:relative;
}

.topHud{
  display:grid;
  grid-template-columns:1fr auto 1fr;
  gap:10px;
  align-items:center;
  margin-bottom:10px;
}

.playerInfo{
  font-weight:bold;
}

.levelBadge{
  text-align:center;
  padding:8px 14px;
  border-radius:999px;
  background:linear-gradient(180deg,#fff1a3,#c98b18);
  color:#181108;
  font-weight:900;
}

.enemyInfo{
  text-align:right;
  font-weight:bold;
}

/* GOLD HEALTH BAR */

.healthBox{
  margin:7px 0;
}

.healthLabel{
  display:flex;
  justify-content:space-between;
  font-size:12px;
  color:#d9deeb;
  margin-bottom:4px;
}

.healthBar{
  height:19px;
  padding:3px;
  border-radius:999px;
  background:#080b12;
  border:1px solid #66501b;
  box-shadow:inset 0 2px 6px #000;
  overflow:hidden;
}

.healthFill{
  height:100%;
  width:100%;
  border-radius:999px;
  background:
    linear-gradient(180deg,#fff6a5 0%,#ffd43c 38%,#e7a916 65%,#9d6500 100%);
  box-shadow:
    0 0 12px #ffd43c,
    inset 0 2px 2px rgba(255,255,255,.8);
  transition:width .45s ease;
}

/* ---------- ARENA ---------- */

.arena{
  position:relative;
  height:480px;
  overflow:hidden;
  border-radius:24px;
  border:1px solid #3b4865;
  background:
    radial-gradient(circle at 50% 35%,rgba(77,104,164,.22),transparent 35%),
    linear-gradient(180deg,#101a30 0%,#080d19 60%,#05070d 100%);
  box-shadow:
    inset 0 0 80px rgba(0,0,0,.8),
    0 15px 45px rgba(0,0,0,.5);
}

/* stars */

.arena::before{
  content:"";
  position:absolute;
  inset:0;
  background-image:
    radial-gradient(circle,#fff 1px,transparent 1px),
    radial-gradient(circle,#8da4ff 1px,transparent 1px);
  background-size:73px 61px,101px 89px;
  opacity:.3;
}

/* energy floor */

.arena::after{
  content:"";
  position:absolute;
  left:0;
  right:0;
  bottom:0;
  height:130px;
  background:
    linear-gradient(transparent,rgba(44,63,105,.3)),
    repeating-linear-gradient(
      90deg,
      transparent 0 48px,
      rgba(106,141,220,.09) 49px 50px
    );
  transform:perspective(250px) rotateX(35deg);
  transform-origin:bottom;
}

/* ---------- FIGHTERS ---------- */

.fighter{
  position:absolute;
  z-index:5;
  bottom:75px;
  width:130px;
  height:220px;
  transition:left .35s ease, right .35s ease;
}

#playerSprite{
  left:15%;
}

#enemySprite{
  right:15%;
  transform:scaleX(-1);
}

/* head */

.head{
  position:absolute;
  width:52px;
  height:55px;
  left:39px;
  top:4px;
  border-radius:45% 45% 42% 42%;
  background:linear-gradient(145deg,#eef5ff,#7f8ba6);
  border:3px solid #242d42;
  box-shadow:0 0 15px rgba(255,255,255,.18);
}

.visor{
  position:absolute;
  left:5px;
  top:18px;
  width:42px;
  height:12px;
  border-radius:8px;
  background:linear-gradient(90deg,#111,#bceaff,#111);
  box-shadow:0 0 10px #80dfff;
}

/* body */

.bodyArmor{
  position:absolute;
  left:25px;
  top:57px;
  width:80px;
  height:105px;
  border-radius:27px 27px 17px 17px;
  background:
    linear-gradient(145deg,#fff 0%,var(--armor) 25%,#111827 100%);
  border:4px solid #273147;
  box-shadow:
    0 0 18px var(--armor),
    inset 5px 0 10px rgba(255,255,255,.3);
}

.chestCore{
  position:absolute;
  left:25px;
  top:23px;
  width:30px;
  height:30px;
  transform:rotate(45deg);
  background:#fff;
  border:4px solid #ffd84d;
  box-shadow:0 0 20px #ffe16a;
}

/* arms */

.arm{
  position:absolute;
  width:25px;
  height:86px;
  top:65px;
  background:linear-gradient(90deg,#111827,var(--armor),#eef3ff);
  border:3px solid #273147;
  border-radius:18px;
}

.arm.left{
  left:4px;
  transform:rotate(15deg);
}

.arm.right{
  right:4px;
  transform:rotate(-15deg);
}

/* legs */

.leg{
  position:absolute;
  top:154px;
  width:29px;
  height:78px;
  background:linear-gradient(90deg,#101827,var(--armor),#9ca8bf);
  border:3px solid #273147;
  border-radius:10px;
}

.leg.left{
  left:31px;
  transform:rotate(4deg);
}

.leg.right{
  right:31px;
  transform:rotate(-4deg);
}

/* enemy variation */

.enemy .bodyArmor{
  background:
    linear-gradient(145deg,#050509 0%,#252a3c 45%,#030305 100%);
  box-shadow:0 0 22px #7258ff;
}

.enemy .head{
  background:linear-gradient(145deg,#17182a,#050508);
  border-color:#654cff;
}

.enemy .visor{
  background:linear-gradient(90deg,#24000d,#ff315e,#24000d);
  box-shadow:0 0 14px #ff315e;
}

.enemy .chestCore{
  background:#26143e;
  border-color:#b47cff;
  box-shadow:0 0 20px #9d57ff;
}

/* ---------- ANIMATIONS ---------- */

.playerAttack{
  animation:playerAttack .7s ease;
}

.enemyAttack{
  animation:enemyAttack .7s ease;
}

.hit{
  animation:hit .4s ease;
}

.defend{
  animation:defend .6s ease;
}

.specialAttack{
  animation:specialAttack 1s ease;
}

@keyframes playerAttack{
  0%{transform:translateX(0) scale(1)}
  35%{transform:translateX(115px) scale(1.08)}
  55%{transform:translateX(115px) scale(1.08) rotate(-4deg)}
  100%{transform:translateX(0) scale(1)}
}

@keyframes enemyAttack{
  0%{transform:scaleX(-1) translateX(0)}
  35%{transform:scaleX(-1) translateX(115px)}
  55%{transform:scaleX(-1) translateX(115px) rotate(4deg)}
  100%{transform:scaleX(-1) translateX(0)}
}

@keyframes hit{
  0%,100%{filter:none}
  25%{filter:brightness(3)}
  50%{transform:translateX(-12px)}
  75%{transform:translateX(12px)}
}

@keyframes defend{
  0%,100%{filter:none}
  50%{
    filter:brightness(1.7);
    box-shadow:0 0 50px #62baff;
  }
}

@keyframes specialAttack{
  0%{transform:scale(1)}
  35%{transform:scale(1.25) translateX(100px)}
  60%{transform:scale(1.25) translateX(100px)}
  100%{transform:scale(1)}
}

/* ---------- ATTACK EFFECTS ---------- */

.energyBlast{
  position:absolute;
  z-index:10;
  width:30px;
  height:30px;
  border-radius:50%;
  background:white;
  box-shadow:
    0 0 10px white,
    0 0 25px #ffd83d,
    0 0 55px #ff9e00;
  pointer-events:none;
  animation:blast .55s linear forwards;
}

@keyframes blast{
  0%{
    transform:scale(.5);
    opacity:1;
  }
  100%{
    transform:translateX(430px) scale(2.5);
    opacity:0;
  }
}

.impact{
  position:absolute;
  z-index:20;
  width:100px;
  height:100px;
  border-radius:50%;
  border:7px solid #fff;
  box-shadow:0 0 30px #ffd83d;
  animation:impact .45s ease-out forwards;
  pointer-events:none;
}

@keyframes impact{
  from{
    transform:scale(.2);
    opacity:1;
  }
  to{
    transform:scale(1.7);
    opacity:0;
  }
}

/* ---------- CONTROLS ---------- */

.controls{
  margin-top:12px;
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:10px;
}

.attackBtn{
  min-height:58px;
  border-radius:14px;
  border:1px solid #59647d;
  color:white;
  font-weight:900;
  background:linear-gradient(145deg,#26324b,#101728);
  box-shadow:0 6px 15px rgba(0,0,0,.3);
}

.attackBtn.special{
  border-color:#ffd34c;
  background:linear-gradient(145deg,#5a4710,#201706);
  color:#ffe88a;
}

.attackBtn:disabled{
  opacity:.35;
  cursor:not-allowed;
}

.log{
  margin-top:12px;
  min-height:58px;
  padding:12px;
  border-radius:12px;
  background:#080c15;
  border:1px solid #252d42;
  color:#d8deed;
}

/* ---------- VERSE ---------- */

.verse{
  margin-top:12px;
  padding:14px;
  border-left:4px solid #ffd34c;
  background:rgba(255,207,62,.06);
  border-radius:10px;
  color:#eee5bd;
  line-height:1.5;
}

.verse b{
  color:#ffd34c;
}

/* ---------- VICTORY ---------- */

.overlay{
  position:fixed;
  inset:0;
  z-index:100;
  background:rgba(0,0,0,.78);
  display:flex;
  align-items:center;
  justify-content:center;
  padding:20px;
}

.overlayBox{
  max-width:520px;
  width:100%;
  text-align:center;
  padding:35px;
  border-radius:24px;
  background:linear-gradient(145deg,#182039,#080b14);
  border:1px solid #ffd34c;
  box-shadow:0 0 70px rgba(255,210,60,.25);
}

@media(max-width:700px){
  #app{
    padding:8px;
  }

  .saveGrid{
    grid-template-columns:1fr;
  }

  .arena{
    height:400px;
  }

  .fighter{
    transform:scale(.82);
    bottom:50px;
  }

  #playerSprite{
    left:2%;
  }

  #enemySprite{
    right:2%;
  }

  .controls{
    grid-template-columns:1fr 1fr;
  }

  .topHud{
    grid-template-columns:1fr auto;
  }

  .enemyInfo{
    grid-column:1/-1;
    text-align:left;
  }
}
</style>
</head>

<body>

<div id="app">

  <!-- SAVE SCREEN -->
  <section id="saveScreen" class="panel">
    <h1>⚡ SPIRITUAL POWER</h1>
    <p style="text-align:center;color:#aeb7cd">
      SHADOWBOUND
    </p>

    <div id="saveGrid" class="saveGrid"></div>
  </section>

  <!-- CUSTOMIZATION -->
  <section id="customScreen" class="panel hidden custom">
    <h2>⚔️ Create Your Warrior</h2>

    <div class="field">
      <label>Name</label>
      <input id="nameInput" maxlength="18" placeholder="Warrior name">
    </div>

    <div class="field">
      <label>Gender</label>
      <select id="genderInput">
        <option>Male</option>
        <option>Female</option>
      </select>
    </div>

    <div class="colorRow">
      <div class="field">
        <label>Armor</label>
        <input id="armorInput" type="color" value="#d92929">
      </div>

      <div class="field">
        <label>Helmet</label>
        <input id="helmetInput" type="color" value="#ffffff">
      </div>
    </div>

    <button class="goldBtn" style="width:100%" onclick="startGame()">
      ENTER THE BATTLE
    </button>

    <br><br>

    <button class="redBtn" style="width:100%" onclick="showSaves()">
      BACK
    </button>
  </section>

  <!-- GAME -->
  <section id="game" class="hidden">

    <div class="topHud panel">

      <div>
        <div class="playerInfo" id="playerName"></div>
        <div class="healthBox">
          <div class="healthLabel">
            <span>SPIRIT HEALTH</span>
            <span id="playerHpText">100 / 100</span>
          </div>
          <div class="healthBar">
            <div id="playerHealth" class="healthFill"></div>
          </div>
        </div>
      </div>

      <div id="levelBadge" class="levelBadge">
        LEVEL 1
      </div>

      <div class="enemyInfo">
        <div id="enemyName"></div>
        <div class="healthBox">
          <div class="healthLabel">
            <span>ENEMY</span>
            <span id="enemyHpText">100 / 100</span>
          </div>
          <div class="healthBar">
            <div id="enemyHealth"
                 class="healthFill"
                 style="background:linear-gradient(180deg,#ff9cae,#e92f52,#760c24);
                        box-shadow:0 0 12px #ff315e">
            </div>
          </div>
        </div>
      </div>

    </div>

    <div class="arena" id="arena">

      <div id="playerSprite" class="fighter">
        <div class="head">
          <div class="visor"></div>
        </div>
        <div class="bodyArmor">
          <div class="chestCore"></div>
        </div>
        <div class="arm left"></div>
        <div class="arm right"></div>
        <div class="leg left"></div>
        <div class="leg right"></div>
      </div>

      <div id="enemySprite" class="fighter enemy">
        <div class="head">
          <div class="visor"></div>
        </div>
        <div class="bodyArmor">
          <div class="chestCore"></div>
        </div>
        <div class="arm left"></div>
        <div class="arm right"></div>
        <div class="leg left"></div>
        <div class="leg right"></div>
      </div>

    </div>

    <div class="panel" style="margin-top:10px">

      <div style="display:flex;justify-content:space-between">
        <b>TURN <span id="turnCount">0</span></b>
        <b>SPIRIT <span id="spiritCount">0</span></b>
      </div>

      <div class="controls">

        <button class="attackBtn"
                onclick="playerAttack('strike')">
          ⚡ SPIRIT STRIKE
        </button>

        <button class="attackBtn"
                onclick="playerAttack('shield')">
          🛡️ SHIELD OF FAITH
        </button>

        <button class="attackBtn"
                onclick="playerAttack('word')">
          ✨ WORD OF TRUTH
        </button>

        <button id="specialBtn"
                class="attackBtn special"
                disabled
                onclick="playerAttack('special')">
          🔥 POWER ATTACK
          <br>
          <small>Survive 3 turns</small>
        </button>

      </div>

      <div id="combatLog" class="log">
        The battle begins...
      </div>

      <div id="verseBox" class="verse"></div>

    </div>

  </section>
</div>

<!-- VICTORY -->
<div id="victoryOverlay" class="overlay hidden">
  <div class="overlayBox">
    <h1>🏆 VICTORY</h1>
    <p id="victoryText"></p>
    <button class="goldBtn" onclick="showSaves()">
      RETURN TO SAVES
    </button>
  </div>
</div>

<script>
/* =========================================================
   SAVE SYSTEM
========================================================= */

const SAVE_KEY = "spiritualPowerShadowboundSaves";

let saves = JSON.parse(
  localStorage.getItem(SAVE_KEY) || "[null,null,null]"
);

let currentSave = -1;

let player = null;
let enemy = null;
let busy = false;

const levels = {
  1:{
    name:"Shadow Demons",
    hp:100,
    requiredPower:5,
    verse:"Ephesians 6:11",
    text:"Put on the whole armour of God, that ye may be able to stand against the wiles of the devil.",
    special:"LIGHT BURST"
  },

  2:{
    name:"Dark Angel",
    hp:200,
    requiredPower:12,
    verse:"Psalm 18:2",
    text:"The LORD is my rock, and my fortress, and my deliverer; my God, my strength, in whom I will trust.",
    special:"HOLY BREAKER"
  },

  3:{
    name:"Shadow Colossus",
    hp:380,
    requiredPower:25,
    verse:"1 John 4:4",
    text:"Greater is he that is in you, than he that is in the world.",
    special:"VICTORY ROAR"
  }
};

/* =========================================================
   SAVE UI
========================================================= */

function saveAll(){
  localStorage.setItem(SAVE_KEY,JSON.stringify(saves));
}

function showSaves(){

  document.getElementById("saveScreen")
    .classList.remove("hidden");

  document.getElementById("customScreen")
    .classList.add("hidden");

  document.getElementById("game")
    .classList.add("hidden");

  document.getElementById("victoryOverlay")
    .classList.add("hidden");

  renderSaves();
}

function renderSaves(){

  const grid=document.getElementById("saveGrid");
  grid.innerHTML="";

  saves.forEach((save,i)=>{

    const card=document.createElement("div");
    card.className="saveCard";

    if(save){

      card.innerHTML=`
        <div>
          <h2>Save ${i+1}</h2>
          <b>${escapeHTML(save.name)}</b>
          <p>Level ${save.level}</p>
          <p>Power: ${save.power}</p>
        </div>

        <button class="goldBtn" onclick="loadSave(${i})">
          CONTINUE
        </button>

        <button class="redBtn" onclick="deleteSave(${i})">
          DELETE SAVE
        </button>
      `;

    }else{

      card.innerHTML=`
        <div>
          <h2>Save ${i+1}</h2>
          <p style="color:#7e8aa5">Empty slot</p>
        </div>

        <button class="goldBtn" onclick="newSave(${i})">
          NEW GAME
        </button>
      `;
    }

    grid.appendChild(card);
  });
}

function newSave(i){

  currentSave=i;

  document.getElementById("saveScreen")
    .classList.add("hidden");

  document.getElementById("customScreen")
    .classList.remove("hidden");
}

function deleteSave(i){

  if(confirm("Delete Save "+(i+1)+"?")){

    saves[i]=null;
    saveAll();
    renderSaves();
  }
}

function loadSave(i){

  currentSave=i;

  player=JSON.parse(JSON.stringify(saves[i]));

  document.getElementById("saveScreen")
    .classList.add("hidden");

  document.getElementById("game")
    .classList.remove("hidden");

  loadLevel();

  updateUI();
}

/* =========================================================
   START
========================================================= */

function startGame(){

  player={
    name:
      document.getElementById("nameInput").value.trim()
      || "Warrior",

    gender:
      document.getElementById("genderInput").value,

    armor:
      document.getElementById("armorInput").value,

    helmet:
      document.getElementById("helmetInput").value,

    level:1,
    power:0,
    hp:100,
    spirit:0,
    defense:0,
    turns:0,
    specialUnlocked:false
  };

  saves[currentSave]=JSON.parse(JSON.stringify(player));
  saveAll();

  document.getElementById("customScreen")
    .classList.add("hidden");

  document.getElementById("game")
    .classList.remove("hidden");

  loadLevel();
  updateUI();
}

function loadLevel(){

  const data=levels[player.level];

  enemy={
    name:data.name,
    maxHp:data.hp,
    hp:data.hp
  };

  document.documentElement.style
    .setProperty("--armor",player.armor);

  const head=document.querySelector("#playerSprite .head");

  head.style.background=
    `linear-gradient(145deg,${player.helmet},#7f8ba6)`;

  document.getElementById("verseBox").innerHTML=
    `<b>${data.verse}</b><br>${data.text}`;

  document.getElementById("combatLog").textContent=
    `A ${data.name} stands before you.`;

  updateUI();
}

/* =========================================================
   UI
========================================================= */

function updateUI(){

  if(!player || !enemy)return;

  document.getElementById("playerName")
    .textContent=player.name;

  document.getElementById("enemyName")
    .textContent=enemy.name;

  document.getElementById("levelBadge")
    .textContent="LEVEL "+player.level;

  document.getElementById("playerHpText")
    .textContent=Math.max(0,player.hp)+" / 100";

  document.getElementById("enemyHpText")
    .textContent=
      Math.max(0,enemy.hp)+" / "+enemy.maxHp;

  document.getElementById("playerHealth")
    .style.width=Math.max(0,player.hp)+"%";

  document.getElementById("enemyHealth")
    .style.width=
      Math.max(0,(enemy.hp/enemy.maxHp)*100)+"%";

  document.getElementById("turnCount")
    .textContent=player.turns;

  document.getElementById("spiritCount")
    .textContent=player.spirit;

  const special=document.getElementById("specialBtn");

  special.disabled=
    !player.specialUnlocked || busy;

  special.innerHTML=
    player.specialUnlocked
      ? `🔥 ${levels[player.level].special}<br><small>READY</small>`
      : `🔥 POWER ATTACK<br><small>Survive 3 turns</small>`;
}

/* =========================================================
   COMBAT
========================================================= */

function playerAttack(type){

  if(busy || player.hp<=0)return;

  if(type==="special" && !player.specialUnlocked)return;

  busy=true;

  let damage=0;
  let message="";

  const p=document.getElementById("playerSprite");
  const e=document.getElementById("enemySprite");

  if(type==="strike"){

    damage=15 + player.level*5;
    player.spirit+=12;
    message="Spirit Strike!";
    p.classList.add("playerAttack");

    createBlast();

  }

  else if(type==="shield"){

    damage=7;
    player.spirit+=18;
    player.defense=28;
    message="Shield of Faith!";
    p.classList.add("defend");

  }

  else if(type==="word"){

    damage=24 + player.level*6;
    player.spirit+=24;
    message="Word of Truth!";
    p.classList.add("specialAttack");

    createBlast(true);

  }

  else if(type==="special"){

    damage=75 + player.level*25;

    player.spirit=0;
    player.specialUnlocked=false;

    message=levels[player.level].special+"!";

    p.classList.add("specialAttack");

    createBlast(true);
  }

  combatLog(message+" You strike for "+damage+" power.");

  setTimeout(()=>{

    p.classList.remove(
      "playerAttack",
      "defend",
      "specialAttack"
    );

    enemy.hp-=damage;

    e.classList.add("hit");

    createImpact();

    setTimeout(()=>{
      e.classList.remove("hit");

      updateUI();

      if(enemy.hp<=0){

        enemyDefeated();

      }else{

        setTimeout(enemyAttack,650);
      }

    },350);

  },550);
}

/* =========================================================
   ENEMY ATTACK
========================================================= */

function enemyAttack(){

  const p=document.getElementById("playerSprite");

  let damage=
    8 +
    player.level*5 +
    Math.floor(Math.random()*8);

  if(player.defense>0){

    damage=Math.max(2,damage-20);
    player.defense=0;

    combatLog(
      enemy.name+
      " attacks, but your shield reduces the damage."
    );

  }else{

    combatLog(
      enemy.name+
      " attacks for "+damage+" damage."
    );
  }

  p.classList.add("hit");

  setTimeout(()=>{

    p.classList.remove("hit");

    player.hp-=damage;

    player.turns++;

    if(player.turns>=3){
      player.specialUnlocked=true;
    }

    if(player.hp<=0){

      player.hp=0;
      updateUI();

      setTimeout(playerDefeated,500);

      return;
    }

    updateUI();

    autoSave();

    busy=false;

  },450);
}

/* =========================================================
   DEFEATED
========================================================= */

function playerDefeated(){

  combatLog(
    "Your warrior falls, but the battle is not over."
  );

  setTimeout(()=>{

    player.hp=100;
    player.spirit=0;
    player.turns=0;
    player.defense=0;
    player.specialUnlocked=false;

    enemy.hp=enemy.maxHp;

    combatLog("Your strength returns. Fight again!");

    busy=false;

    updateUI();

  },900);
}

function enemyDefeated(){

  busy=false;

  combatLog(
    enemy.name+" has been defeated!"
  );

  player.power+=5;

  if(player.level<3){

    setTimeout(()=>{

      player.level++;

      player.hp=100;
      player.spirit=0;
      player.turns=0;
      player.defense=0;
      player.specialUnlocked=false;

      loadLevel();

      combatLog(
        "LEVEL UP! Your spiritual power grows."
      );

      autoSave();

      busy=false;

    },1000);

  }else{

    player.power+=50;

    autoSave();

    document.getElementById("victoryText")
      .textContent=
      "You defeated the Shadow Colossus and completed the three levels.";

    document.getElementById("victoryOverlay")
      .classList.remove("hidden");
  }
}

/* =========================================================
   VISUAL EFFECTS
========================================================= */

function createBlast(big=false){

  const arena=document.getElementById("arena");

  const blast=document.createElement("div");

  blast.className="energyBlast";

  blast.style.left="28%";
  blast.style.top="45%";

  if(big){

    blast.style.width="45px";
    blast.style.height="45px";
    blast.style.boxShadow=
      "0 0 20px white,0 0 45px #ffd83d,0 0 90px #ff9e00";
  }

  arena.appendChild(blast);

  setTimeout(()=>blast.remove(),650);
}

function createImpact(){

  const arena=document.getElementById("arena");

  const impact=document.createElement("div");

  impact.className="impact";

  impact.style.left="68%";
  impact.style.top="43%";

  arena.appendChild(impact);

  setTimeout(()=>impact.remove(),500);
}

/* =========================================================
   LOG
========================================================= */

function combatLog(text){

  document.getElementById("combatLog")
    .textContent=text;
}

/* =========================================================
   AUTO SAVE
========================================================= */

function autoSave(){

  if(currentSave<0 || !player)return;

  saves[currentSave]=JSON.parse(
    JSON.stringify(player)
  );

  saveAll();
}

setInterval(()=>{

  if(
    currentSave>=0 &&
    player &&
    !document.getElementById("game")
      .classList.contains("hidden")
  ){
    autoSave();
  }

},5000);

/* =========================================================
   SECURITY / TEXT
========================================================= */

function escapeHTML(str){

  return String(str)
    .replaceAll("&","&amp;")
    .replaceAll("<","&lt;")
    .replaceAll(">","&gt;")
    .replaceAll('"',"&quot;")
    .replaceAll("'","&#039;");
}

/* =========================================================
   START SCREEN
========================================================= */

showSaves();
</script>

</body>
</html>
