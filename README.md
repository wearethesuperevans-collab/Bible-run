<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0">
<title>Spiritual Power: Shadowbound</title>

<style>
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}

body{
    margin:0;
    background:
    radial-gradient(circle at 50% 20%,#182746,#060914 55%,#020307);
    color:white;
    font-family:Arial,sans-serif;
    min-height:100vh;
}

button,input,select{font:inherit}
button{cursor:pointer}
.hidden{display:none!important}

#app{
    max-width:1150px;
    margin:auto;
    padding:10px;
}

.panel{
    background:linear-gradient(145deg,rgba(24,32,55,.96),rgba(5,8,15,.97));
    border:1px solid #36415d;
    border-radius:20px;
    padding:17px;
    box-shadow:0 15px 50px #000b;
}

/* ================= SAVE SCREEN ================= */

.title{
    text-align:center;
    font-size:clamp(30px,7vw,55px);
    color:#fff1a0;
    text-shadow:0 0 15px #ffd42e,0 0 35px #ff9d00;
    letter-spacing:3px;
}

.subtitle{
    text-align:center;
    color:#aab6d0;
    margin-bottom:25px;
}

.saveGrid{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:15px;
}

.saveCard{
    min-height:180px;
    padding:18px;
    border-radius:18px;
    border:1px solid #3c4965;
    background:linear-gradient(145deg,#18223b,#080c16);
    display:flex;
    flex-direction:column;
    justify-content:space-between;
}

.goldButton{
    border:0;
    border-radius:12px;
    padding:14px;
    font-weight:900;
    color:#181108;
    background:linear-gradient(#fff3a5,#ffd23c,#b87300);
    box-shadow:0 5px 18px #ffbf382f;
}

.redButton{
    border:1px solid #793747;
    border-radius:10px;
    padding:10px;
    color:#ff9cac;
    background:#2c1119;
}

/* ================= CREATION ================= */

.custom{
    max-width:650px;
    margin:30px auto;
}

.field{margin:15px 0}

.field label{
    display:block;
    margin-bottom:6px;
    color:#cbd4e7;
}

input,select{
    width:100%;
    padding:13px;
    border-radius:11px;
    border:1px solid #414e6b;
    background:#080d18;
    color:white;
}

input[type=color]{height:50px;padding:3px}

/* ================= HUD ================= */

.topHud{
    display:grid;
    grid-template-columns:1fr auto 1fr;
    gap:12px;
    align-items:center;
}

.level{
    padding:9px 15px;
    border-radius:999px;
    color:#1b1204;
    font-weight:900;
    background:linear-gradient(#fff2a0,#d89a20);
}

.enemyName{text-align:right}

.healthText{
    display:flex;
    justify-content:space-between;
    font-size:12px;
    color:#cbd3e3;
    margin:5px 0;
}

.healthBar{
    height:20px;
    padding:3px;
    border-radius:999px;
    background:#05070b;
    border:1px solid #725b20;
    overflow:hidden;
}

.playerHealth{
    height:100%;
    width:100%;
    border-radius:999px;
    background:linear-gradient(#fff9b0,#ffd93e,#b87300);
    box-shadow:0 0 14px #ffd52e,inset 0 2px #fff;
    transition:.45s;
}

.enemyHealth{
    height:100%;
    width:100%;
    border-radius:999px;
    background:linear-gradient(#ffb1bf,#ed3158,#720d26);
    box-shadow:0 0 13px #ff315e;
    transition:.45s;
}

/* ================= ARENA ================= */

.arena{
    position:relative;
    height:510px;
    margin-top:12px;
    overflow:hidden;
    border-radius:25px;
    border:1px solid #3c4b6c;

    background:
    radial-gradient(circle at 50% 30%,#344b791c,transparent 30%),
    linear-gradient(#111b31,#070b15 70%,#03050a);

    box-shadow:inset 0 0 90px #000d;
}

.arena:before{
    content:"";
    position:absolute;
    inset:0;
    background-image:
    radial-gradient(circle,#fff 1px,transparent 1px),
    radial-gradient(circle,#7c9cff 1px,transparent 1px);
    background-size:71px 63px,109px 87px;
    opacity:.25;
}

.floor{
    position:absolute;
    left:-10%;
    right:-10%;
    bottom:-70px;
    height:220px;
    transform:perspective(300px) rotateX(55deg);
    background:
    repeating-linear-gradient(90deg,transparent 0 55px,#6a96e51a 56px 57px),
    repeating-linear-gradient(0deg,transparent 0 40px,#6a96e51a 41px 42px);
}

/* ================= PLAYER HUMAN DESIGN ================= */

.fighter{
    position:absolute;
    width:145px;
    height:270px;
    bottom:58px;
    z-index:10;
}

#player{
    left:10%;
}

/* human head */

.humanHead{
    position:absolute;
    left:48px;
    top:0;
    width:49px;
    height:59px;
    border-radius:45% 45% 48% 48%;
    background:
    linear-gradient(145deg,#f0c7a4,#b87955);
    border:2px solid #49352e;
    box-shadow:0 4px 8px #0008;
}

/* hair */

.hair{
    position:absolute;
    left:-2px;
    top:-4px;
    width:53px;
    height:23px;
    border-radius:50% 50% 25% 25%;
    background:#171717;
}

/* eyes */

.eye{
    position:absolute;
    top:27px;
    width:7px;
    height:5px;
    border-radius:50%;
    background:#171717;
}

.eye.left{left:12px}
.eye.right{right:12px}

/* mouth */

.mouth{
    position:absolute;
    left:18px;
    bottom:10px;
    width:14px;
    height:4px;
    border-bottom:2px solid #572e2c;
    border-radius:50%;
}

/* human armor */

.humanBody{
    position:absolute;
    left:27px;
    top:59px;
    width:87px;
    height:105px;
    border-radius:30px 30px 16px 16px;
    background:
    linear-gradient(145deg,#f5f7ff,var(--armor),#111927);
    border:4px solid #28334a;
    box-shadow:
    0 0 20px var(--armor),
    inset 6px 0 12px #fff4;
}

/* armor shoulder pieces */

.shoulder{
    position:absolute;
    top:64px;
    width:34px;
    height:35px;
    border-radius:50%;
    background:linear-gradient(145deg,#fff,var(--armor),#172033);
    border:3px solid #29344b;
}

.shoulder.left{left:8px}
.shoulder.right{right:8px}

/* core */

.core{
    position:absolute;
    left:28px;
    top:22px;
    width:30px;
    height:30px;
    transform:rotate(45deg);
    background:white;
    border:4px solid #ffd83d;
    box-shadow:0 0 10px white,0 0 30px #ffd42e;
}

/* arms */

.humanArm{
    position:absolute;
    top:78px;
    width:25px;
    height:83px;
    border-radius:16px;
    background:linear-gradient(90deg,#111927,var(--armor),#dbe5f4);
    border:3px solid #28344a;
}

.humanArm.left{left:9px;transform:rotate(12deg)}
.humanArm.right{right:9px;transform:rotate(-12deg)}

/* legs */

.humanLeg{
    position:absolute;
    top:158px;
    width:31px;
    height:91px;
    border-radius:12px;
    background:linear-gradient(90deg,#111927,var(--armor),#aab6c9);
    border:3px solid #28344a;
}

.humanLeg.left{left:36px}
.humanLeg.right{right:36px}

/* ================= DEMON ================= */

#enemy{
    right:8%;
    transform:scaleX(-1);
}

/* demon head */

.demonHead{
    position:absolute;
    left:35px;
    top:9px;
    width:70px;
    height:68px;
    border-radius:45% 45% 38% 38%;
    background:
    linear-gradient(145deg,#4d345d,#130c1a);
    border:3px solid #6c3e8d;
    box-shadow:0 0 25px #743cff;
}

/* horns */

.horn{
    position:absolute;
    top:-32px;
    width:28px;
    height:47px;
    background:linear-gradient(#201026,#7d3c93);
    clip-path:polygon(50% 0,100% 100%,55% 78%,0 100%);
}

.horn.left{left:0;transform:rotate(-25deg)}
.horn.right{right:0;transform:rotate(25deg)}

/* demon eyes */

.demonEye{
    position:absolute;
    top:27px;
    width:17px;
    height:8px;
    background:#ff174d;
    border-radius:50%;
    box-shadow:0 0 13px #ff174d;
}

.demonEye.left{left:10px}
.demonEye.right{right:10px}

/* demon mouth */

.demonMouth{
    position:absolute;
    left:14px;
    bottom:10px;
    width:42px;
    height:20px;
    border-bottom:4px solid #ff315e;
    border-radius:50%;
}

/* demon body */

.demonBody{
    position:absolute;
    left:20px;
    top:75px;
    width:100px;
    height:115px;
    border-radius:40px 40px 15px 15px;
    background:
    linear-gradient(145deg,#08070d,#33213e,#07050b);
    border:4px solid #4c2c68;
    box-shadow:0 0 30px #6f3dff;
}

/* demon chest */

.demonCore{
    position:absolute;
    left:31px;
    top:28px;
    width:34px;
    height:34px;
    border-radius:50%;
    background:#3d0920;
    border:4px solid #c44bff;
    box-shadow:0 0 28px #b52cff;
}

/* demon arms */

.demonArm{
    position:absolute;
    top:85px;
    width:30px;
    height:95px;
    border-radius:18px;
    background:linear-gradient(90deg,#08070c,#44204f,#160d1c);
    border:3px solid #4e2c69;
}

.demonArm.left{left:0;transform:rotate(18deg)}
.demonArm.right{right:0;transform:rotate(-18deg)}

/* claws */

.claw{
    position:absolute;
    bottom:-8px;
    width:32px;
    height:20px;
    background:#d6b3e8;
    clip-path:polygon(0 0,100% 30%,75% 100%,55% 45%,35% 100%,20% 45%);
}

.demonArm.left .claw{left:-3px}
.demonArm.right .claw{right:-3px}

/* demon legs */

.demonLeg{
    position:absolute;
    top:180px;
    width:36px;
    height:88px;
    border-radius:15px;
    background:linear-gradient(90deg,#08070c,#321c3d,#09060d);
    border:3px solid #4e2c69;
}

.demonLeg.left{left:27px}
.demonLeg.right{right:27px}

/* ================= ATTACK ANIMATIONS ================= */

.playerDash{
    animation:playerDash .7s ease;
}

@keyframes playerDash{
    0%,100%{transform:translateX(0)}
    35%,60%{transform:translateX(105px) scale(1.06)}
}

.demonDash{
    animation:demonDash .7s ease;
}

@keyframes demonDash{
    0%,100%{transform:scaleX(-1) translateX(0)}
    35%,60%{transform:scaleX(-1) translateX(105px)}
}

.playerHit{
    animation:playerHit .45s ease;
}

@keyframes playerHit{
    0%,100%{filter:none}
    25%{filter:brightness(3)}
    50%{transform:translateX(-14px)}
    75%{transform:translateX(14px)}
}

.demonHit{
    animation:demonHit .45s ease;
}

@keyframes demonHit{
    0%,100%{filter:none}
    25%{filter:brightness(4)}
    50%{transform:scaleX(-1) translateX(15px)}
    75%{transform:scaleX(-1) translateX(-15px)}
}

/* ================= LIGHT SHOT ================= */

.lightShot{
    position:absolute;
    z-index:40;
    width:27px;
    height:27px;
    border-radius:50%;
    background:white;
    box-shadow:0 0 15px white,0 0 35px #ffe05a,0 0 70px #ff9d00;
    animation:lightShot .65s linear forwards;
}

@keyframes lightShot{
    from{left:23%;top:48%;transform:scale(.5)}
    to{left:74%;top:48%;transform:scale(2.2)}
}

/* ================= SHIELD ================= */

.fateShield{
    position:absolute;
    z-index:35;
    left:5%;
    top:25%;
    width:155px;
    height:245px;
    border:5px solid #8ee5ff;
    border-radius:50% 18% 50% 18%;
    background:radial-gradient(circle,#9eeaff35,transparent 70%);
    box-shadow:0 0 20px #5fd8ff,0 0 60px #4aa8ff44;
    animation:shieldIn .45s ease;
}

@keyframes shieldIn{
    from{opacity:0;transform:scale(.5)}
    to{opacity:1;transform:scale(1)}
}

.shieldHit{
    animation:shieldHit .5s ease;
}

@keyframes shieldHit{
    0%{filter:brightness(1)}
    30%{filter:brightness(4);transform:scale(1.08)}
    100%{filter:brightness(1);transform:scale(1)}
}

/* ================= TRUTH BEAM ================= */

.truthBeam{
    position:absolute;
    z-index:40;
    right:21%;
    top:-20px;
    width:52px;
    height:500px;
    background:linear-gradient(90deg,transparent,#fff,#ffe66d,#fff,transparent);
    box-shadow:0 0 25px white,0 0 60px #ffd52d,0 0 100px #ff9d00;
    animation:truthBeam .8s ease forwards;
}

@keyframes truthBeam{
    0%{opacity:0;transform:scaleY(.1)}
    25%{opacity:1;transform:scaleY(1)}
    100%{opacity:0;transform:scaleY(1)}
}

/* ================= SPECIAL BEAM ================= */

.superBeam{
    position:absolute;
    z-index:45;
    left:22%;
    top:43%;
    width:0;
    height:48px;
    border-radius:30px;
    background:linear-gradient(90deg,#fff,#fffbd5,#ffd42e,#fff);
    box-shadow:0 0 20px white,0 0 50px #ffd42e,0 0 100px #ff9900;
    animation:superBeam 1s ease forwards;
}

@keyframes superBeam{
    0%{width:0;opacity:0}
    15%{width:12%;opacity:1}
    100%{width:70%;opacity:0}
}

/* ================= IMPACT ================= */

.impact{
    position:absolute;
    z-index:50;
    width:95px;
    height:95px;
    border-radius:50%;
    border:5px solid white;
    box-shadow:0 0 25px white,0 0 55px #ffd52e;
    animation:impact .45s ease forwards;
}

@keyframes impact{
    from{transform:scale(.2);opacity:1}
    to{transform:scale(2);opacity:0}
}

/* ================= BUTTONS ================= */

.controls{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:10px;
    margin-top:12px;
}

.attack{
    min-height:72px;
    border-radius:14px;
    border:1px solid #52617d;
    background:linear-gradient(145deg,#273550,#0c1322);
    color:white;
    font-weight:900;
}

.attack.special{
    border-color:#ffd23e;
    background:linear-gradient(145deg,#59460e,#191305);
    color:#ffe88c;
}

.attack:disabled{
    opacity:.4;
    cursor:not-allowed;
}

.log{
    margin-top:12px;
    min-height:58px;
    padding:13px;
    border-radius:12px;
    background:#050913;
    border:1px solid #283248;
    color:#dce2ee;
}

.verse{
    margin-top:12px;
    padding:14px;
    border-left:4px solid #ffd33d;
    background:#ffd33d08;
    border-radius:10px;
    line-height:1.5;
    color:#eee5ba;
}

.verse b{color:#ffd33d}

/* ================= VICTORY ================= */

.overlay{
    position:fixed;
    inset:0;
    z-index:100;
    background:#000d;
    display:flex;
    justify-content:center;
    align-items:center;
    padding:20px;
}

.overlayBox{
    max-width:520px;
    width:100%;
    text-align:center;
    padding:35px;
    border-radius:25px;
    border:1px solid #ffd43d;
    background:linear-gradient(145deg,#19223b,#050811);
    box-shadow:0 0 70px #ffd42e33;
}

/* ================= MOBILE ================= */

@media(max-width:750px){

    .saveGrid{
        grid-template-columns:1fr;
    }

    .topHud{
        grid-template-columns:1fr auto;
    }

    .enemyName{
        grid-column:1/-1;
        text-align:left;
    }

    .arena{
        height:430px;
    }

    .fighter{
        transform:scale(.75);
        bottom:45px;
    }

    #player{left:-2%}
    #enemy{right:-2%}

    .controls{
        grid-template-columns:1fr 1fr;
    }
}

</style>
</head>

<body>

<div id="app">

<!-- ================= SAVES ================= -->

<section id="saveScreen" class="panel">

    <h1 class="title">SPIRITUAL POWER</h1>

    <div class="subtitle">
        SHADOWBOUND
    </div>

    <div id="saveGrid" class="saveGrid"></div>

</section>


<!-- ================= CHARACTER CREATION ================= -->

<section id="customScreen" class="panel custom hidden">

    <h2>⚔️ CREATE YOUR WARRIOR</h2>

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

    <div class="field">
        <label>Armor Color</label>
        <input id="armorInput" type="color" value="#d92935">
    </div>

    <div class="field">
        <label>Helmet / Hair Color</label>
        <input id="helmetInput" type="color" value="#171717">
    </div>

    <button class="goldButton" style="width:100%" onclick="startGame()">
        ENTER THE BATTLE
    </button>

    <br><br>

    <button class="redButton" style="width:100%" onclick="showSaves()">
        BACK
    </button>

</section>


<!-- ================= GAME ================= -->

<section id="game" class="hidden">

<div class="topHud panel">

    <div>

        <b id="playerName"></b>

        <div class="healthText">
            <span>SPIRIT HEALTH</span>
            <span id="playerHpText">100 / 100</span>
        </div>

        <div class="healthBar">
            <div id="playerHealth" class="playerHealth"></div>
        </div>

    </div>

    <div id="levelBadge" class="level">
        LEVEL 1
    </div>

    <div>

        <b id="enemyName" class="enemyName"></b>

        <div class="healthText">
            <span>DEMON</span>
            <span id="enemyHpText">100 / 100</span>
        </div>

        <div class="healthBar">
            <div id="enemyHealth" class="enemyHealth"></div>
        </div>

    </div>

</div>


<!-- ARENA -->

<div id="arena" class="arena">

    <div class="floor"></div>


    <!-- HUMAN PLAYER -->

    <div id="player" class="fighter">

        <div class="humanHead">

            <div class="hair"></div>

            <div class="eye left"></div>
            <div class="eye right"></div>

            <div class="mouth"></div>

        </div>

        <div class="humanBody">
            <div class="core"></div>
        </div>

        <div class="shoulder left"></div>
        <div class="shoulder right"></div>

        <div class="humanArm left"></div>
        <div class="humanArm right"></div>

        <div class="humanLeg left"></div>
        <div class="humanLeg right"></div>

    </div>


    <!-- DEMON -->

    <div id="enemy" class="fighter">

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

        <div class="demonArm left">
            <div class="claw"></div>
        </div>

        <div class="demonArm right">
            <div class="claw"></div>
        </div>

        <div class="demonLeg left"></div>
        <div class="demonLeg right"></div>

    </div>

</div>


<!-- COMBAT PANEL -->

<div class="panel" style="margin-top:10px">

    <div style="display:flex;justify-content:space-between">
        <b>TURN <span id="turnCount">0</span></b>
        <b>SPIRIT <span id="spiritCount">0</span></b>
    </div>

    <div class="controls">

        <button id="strikeButton"
                class="attack"
                onclick="playerAttack('strike')">

            ⚡<br>
            SPIRIT STRIKE
            <br>
            <small>LIGHT SHOT</small>

        </button>

        <button id="shieldButton"
                class="attack"
                onclick="playerAttack('shield')">

            🛡️<br>
            SHIELD OF FATE
            <br>
            <small>BLOCK NEXT ATTACK</small>

        </button>

        <button id="truthButton"
                class="attack"
                onclick="playerAttack('truth')">

            ✨<br>
            WORD OF TRUTH
            <br>
            <small>LIGHT BEAM</small>

        </button>

        <button id="specialButton"
                class="attack special"
                onclick="playerAttack('special')"
                disabled>

            ☀️<br>
            LIGHT BURST
            <br>
            <small>SURVIVE 3 TURNS</small>

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

        <h1 class="title">VICTORY</h1>

        <p id="victoryText"></p>

        <button class="goldButton"
                onclick="showSaves()">

            RETURN TO SAVES

        </button>

    </div>

</div>


<script>

/* =========================================================
   DATA
========================================================= */

const SAVE_KEY="spiritualPowerShadowboundSaves";

let saves=JSON.parse(
    localStorage.getItem(SAVE_KEY) ||
    "[null,null,null]"
);

let currentSave=-1;
let player=null;
let enemy=null;

let busy=false;
let shieldActive=false;


/* =========================================================
   LEVELS
========================================================= */

const levels={

1:{
    name:"Shadow Demons",
    hp:100,
    verse:"Ephesians 6:11",
    text:"Put on the whole armour of God, that ye may be able to stand against the wiles of the devil."
},

2:{
    name:"Dark Angel",
    hp:200,
    verse:"Psalm 18:2",
    text:"The LORD is my rock, and my fortress, and my deliverer; my God, my strength, in whom I will trust."
},

3:{
    name:"Shadow Colossus",
    hp:380,
    verse:"1 John 4:4",
    text:"Greater is he that is in you, than he that is in the world."
}

};


/* =========================================================
   SAVE FUNCTIONS
========================================================= */

function saveAll(){
    localStorage.setItem(
        SAVE_KEY,
        JSON.stringify(saves)
    );
}

function autoSave(){

    if(currentSave<0 || !player)return;

    saves[currentSave]=
        JSON.parse(JSON.stringify(player));

    saveAll();
}


/* =========================================================
   SCREENS
========================================================= */

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

    const grid=
        document.getElementById("saveGrid");

    grid.innerHTML="";

    saves.forEach((save,i)=>{

        const card=
            document.createElement("div");

        card.className="saveCard";

        if(save){

            card.innerHTML=`

                <div>
                    <h2>SAVE ${i+1}</h2>
                    <b>${safe(save.name)}</b>
                    <p>Level ${save.level}</p>
                    <p>Power: ${save.power}</p>
                </div>

                <button class="goldButton"
                        onclick="loadSave(${i})">
                    CONTINUE
                </button>

                <button class="redButton"
                        onclick="deleteSave(${i})">
                    DELETE SAVE
                </button>

            `;

        }else{

            card.innerHTML=`

                <div>
                    <h2>SAVE ${i+1}</h2>
                    <p style="color:#7d89a5">
                        Empty slot
                    </p>
                </div>

                <button class="goldButton"
                        onclick="newSave(${i})">
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


/* =========================================================
   START / LOAD
========================================================= */

function startGame(){

    player={

        name:
        document.getElementById("nameInput")
        .value.trim() || "Warrior",

        gender:
        document.getElementById("genderInput")
        .value,

        armor:
        document.getElementById("armorInput")
        .value,

        helmet:
        document.getElementById("helmetInput")
        .value,

        level:1,
        power:0,
        hp:100,
        spirit:0,
        turns:0,
        specialUnlocked:false

    };

    shieldActive=false;

    autoSave();

    document.getElementById("customScreen")
        .classList.add("hidden");

    document.getElementById("game")
        .classList.remove("hidden");

    loadLevel();
}


function loadSave(i){

    currentSave=i;

    player=
        JSON.parse(JSON.stringify(saves[i]));

    shieldActive=false;

    document.getElementById("saveScreen")
        .classList.add("hidden");

    document.getElementById("game")
        .classList.remove("hidden");

    loadLevel();
}


/* =========================================================
   LOAD LEVEL
========================================================= */

function loadLevel(){

    const data=levels[player.level];

    enemy={
        name:data.name,
        maxHp:data.hp,
        hp:data.hp
    };

    shieldActive=false;

    document.documentElement.style
        .setProperty("--armor",player.armor);

    document.querySelector("#player .humanHead")
        .style.background=
        `
        linear-gradient(
            145deg,
            ${player.helmet},
            #8c563c
        )
        `;

    document.querySelector("#player .hair")
        .style.background=
        player.helmet;

    document.getElementById("verseBox")
        .innerHTML=
        `<b>${data.verse}</b><br>${data.text}`;

    log(
        "A "+data.name+" enters the arena."
    );

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
        .textContent=
        Math.max(0,player.hp)+" / 100";

    document.getElementById("enemyHpText")
        .textContent=
        Math.max(0,enemy.hp)+" / "+enemy.maxHp;

    document.getElementById("playerHealth")
        .style.width=
        Math.max(0,player.hp)+"%";

    document.getElementById("enemyHealth")
        .style.width=
        Math.max(
            0,
            enemy.hp/enemy.maxHp*100
        )+"%";

    document.getElementById("turnCount")
        .textContent=player.turns;

    document.getElementById("spiritCount")
        .textContent=player.spirit;

    const special=
        document.getElementById("specialButton");

    special.disabled=
        busy ||
        !player.specialUnlocked;

    /* IMPORTANT:
       Every button is unlocked whenever the
       actual turn has finished. */

    document.getElementById("strikeButton")
        .disabled=busy;

    document.getElementById("shieldButton")
        .disabled=busy;

    document.getElementById("truthButton")
        .disabled=busy;

    special.disabled=
        busy ||
        !player.specialUnlocked;
}


/* =========================================================
   PLAYER ATTACK ROUTER
========================================================= */

function playerAttack(type){

    /*
       HARD TURN LOCK

       Only one player action can happen at a time.
       The lock is removed AFTER the enemy has
       finished attacking.
    */

    if(busy)return;

    if(!player || !enemy)return;

    if(enemy.hp<=0)return;

    if(player.hp<=0)return;

    if(
        type==="special" &&
        !player.specialUnlocked
    )return;

    busy=true;

    updateUI();

    if(type==="strike"){
        spiritStrike();
    }

    else if(type==="shield"){
        shieldOfFate();
    }

    else if(type==="truth"){
        wordOfTruth();
    }

    else if(type==="special"){
        lightBurst();
    }
}


/* =========================================================
   SPIRIT STRIKE
========================================================= */

function spiritStrike(){

    const p=
        document.getElementById("player");

    const e=
        document.getElementById("enemy");

    p.classList.add("playerDash");

    log(
        "⚡ SPIRIT STRIKE — LIGHT SHOT!"
    );

    const shot=
        document.createElement("div");

    shot.className="lightShot";

    document.getElementById("arena")
        .appendChild(shot);

    setTimeout(()=>{

        enemy.hp-=
            20+
            player.level*5;

        player.spirit+=12;

        e.classList.add("demonHit");

        createImpact();

        shot.remove();

    },550);

    setTimeout(()=>{

        p.classList.remove("playerDash");
        e.classList.remove("demonHit");

        finishPlayerAttack();

    },850);
}


/* =========================================================
   SHIELD OF FATE
========================================================= */

function shieldOfFate(){

    shieldActive=true;

    const shield=
        document.createElement("div");

    shield.className="fateShield";
    shield.id="fateShield";

    document.getElementById("arena")
        .appendChild(shield);

    player.spirit+=20;

    log(
        "🛡️ SHIELD OF FATE — NEXT DEMON ATTACK WILL BE BLOCKED!"
    );

    updateUI();

    /*
       Shield is a defensive move.
       Enemy gets its turn.
    */

    setTimeout(()=>{

        enemyAttack();

    },700);
}


/* =========================================================
   WORD OF TRUTH
========================================================= */

function wordOfTruth(){

    const e=
        document.getElementById("enemy");

    const beam=
        document.createElement("div");

    beam.className="truthBeam";

    document.getElementById("arena")
        .appendChild(beam);

    log(
        "✨ WORD OF TRUTH — HEAVEN'S LIGHT!"
    );

    setTimeout(()=>{

        enemy.hp-=
            32+
            player.level*6;

        player.spirit+=24;

        e.classList.add("demonHit");

        createImpact();

    },450);

    setTimeout(()=>{

        beam.remove();

        e.classList.remove("demonHit");

        finishPlayerAttack();

    },900);
}


/* =========================================================
   LIGHT BURST
========================================================= */

function lightBurst(){

    const p=
        document.getElementById("player");

    const e=
        document.getElementById("enemy");

    const beam=
        document.createElement("div");

    beam.className="superBeam";

    document.getElementById("arena")
        .appendChild(beam);

    p.classList.add("playerDash");

    log(
        "☀️ LIGHT BURST — DIVINE POWER RELEASED!"
    );

    setTimeout(()=>{

        enemy.hp-=
            100+
            player.level*25;

        player.spirit=0;

        player.specialUnlocked=false;

        e.classList.add("demonHit");

        createImpact();

    },600);

    setTimeout(()=>{

        beam.remove();

        p.classList.remove("playerDash");
        e.classList.remove("demonHit");

        finishPlayerAttack();

    },1100);
}


/* =========================================================
   FINISH PLAYER ACTION
========================================================= */

function finishPlayerAttack(){

    updateUI();

    if(enemy.hp<=0){

        enemyDefeated();
        return;
    }

    /*
       PLAYER ATTACK IS OVER.
       ENEMY NOW GETS EXACTLY ONE TURN.
    */

    setTimeout(()=>{

        enemyAttack();

    },350);
}


/* =========================================================
   ENEMY TURN
========================================================= */

function enemyAttack(){

    if(enemy.hp<=0){

        unlockTurn();
        return;
    }

    const e=
        document.getElementById("enemy");

    const p=
        document.getElementById("player");

    /*
       SHIELD BLOCK
    */

    if(shieldActive){

        const shield=
            document.getElementById("fateShield");

        log(
            "🛡️ SHIELD OF FATE BLOCKED THE DEMON ATTACK!"
        );

        if(shield){

            shield.classList.add("shieldHit");

            setTimeout(()=>{

                shield.remove();

            },450);
        }

        shieldActive=false;

        /*
           The blocked attack STILL counts as the
           enemy's turn.
        */

        player.turns++;

        checkSpecial();

        updateUI();

        autoSave();

        /*
           THIS IS THE IMPORTANT PART:
           after the enemy turn, unlock attacks.
        */

        setTimeout(()=>{

            unlockTurn();

        },550);

        return;
    }


    /*
       NORMAL DEMON ATTACK
    */

    e.classList.add("demonDash");

    log(
        "👹 "+enemy.name+
        " attacks!"
    );

    setTimeout(()=>{

        const damage=
            10+
            player.level*5+
            Math.floor(Math.random()*7);

        player.hp-=damage;

        p.classList.add("playerHit");

        createDemonImpact();

        log(
            "👹 Demon attack dealt "+
            damage+
            " damage."
        );

    },500);

    setTimeout(()=>{

        e.classList.remove("demonDash");
        p.classList.remove("playerHit");

        player.turns++;

        checkSpecial();

        if(player.hp<=0){

            player.hp=0;

            updateUI();

            playerDefeated();

            return;
        }

        updateUI();

        autoSave();

        /*
           ENEMY TURN IS NOW COMPLETELY FINISHED.
           BUTTONS UNLOCK.
        */

        unlockTurn();

    },900);
}


/* =========================================================
   UNLOCK NEXT TURN
========================================================= */

function unlockTurn(){

    /*
       Explicitly release the combat lock.
       This fixes the "can't click attacks anymore"
       problem.
    */

    busy=false;

    updateUI();

    log(
        "Your turn — choose an attack."
    );
}


/* =========================================================
   SPECIAL CHECK
========================================================= */

function checkSpecial(){

    if(player.turns>=3){

        player.specialUnlocked=true;

        log(
            "☀️ LIGHT BURST IS READY!"
        );
    }
}


/* =========================================================
   PLAYER DEFEATED
========================================================= */

function playerDefeated(){

    busy=true;

    log(
        "Your warrior has fallen. The light returns..."
    );

    setTimeout(()=>{

        player.hp=100;
        player.spirit=0;
        player.turns=0;
        player.specialUnlocked=false;

        shieldActive=false;

        enemy.hp=enemy.maxHp;

        const shield=
            document.getElementById("fateShield");

        if(shield)shield.remove();

        log(
            "Rise again. Your turn."
        );

        busy=false;

        updateUI();

        autoSave();

    },1000);
}


/* =========================================================
   ENEMY DEFEATED
========================================================= */

function enemyDefeated(){

    busy=true;

    player.power+=5;

    updateUI();

    log(
        "👑 "+enemy.name+
        " has been defeated!"
    );

    if(player.level<3){

        setTimeout(()=>{

            player.level++;

            player.hp=100;
            player.spirit=0;
            player.turns=0;
            player.specialUnlocked=false;

            shieldActive=false;

            loadLevel();

            player.power+=
                player.level*4;

            busy=false;

            autoSave();

            updateUI();

        },1100);

    }else{

        player.power+=50;

        autoSave();

        document
            .getElementById("victoryText")
            .textContent=
            "The Shadow Colossus has been defeated. You completed all three levels.";

        document
            .getElementById("victoryOverlay")
            .classList.remove("hidden");
    }
}


/* =========================================================
   EFFECTS
========================================================= */

function createImpact(){

    const effect=
        document.createElement("div");

    effect.className="impact";

    effect.style.left="72%";
    effect.style.top="43%";

    document.getElementById("arena")
        .appendChild(effect);

    setTimeout(
        ()=>effect.remove(),
        500
    );
}


function createDemonImpact(){

    const effect=
        document.createElement("div");

    effect.className="impact";

    effect.style.left="20%";
    effect.style.top="43%";

    effect.style.borderColor="#b879ff";

    effect.style.boxShadow=
        "0 0 25px #a050ff,0 0 55px #5420ff";

    document.getElementById("arena")
        .appendChild(effect);

    setTimeout(
        ()=>effect.remove(),
        500
    );
}


/* =========================================================
   LOG
========================================================= */

function log(text){

    document.getElementById("combatLog")
        .textContent=text;
}


/* =========================================================
   SAFE SAVE NAME
========================================================= */

function safe(value){

    return String(value)
        .replaceAll("&","&amp;")
        .replaceAll("<","&lt;")
        .replaceAll(">","&gt;")
        .replaceAll('"',"&quot;")
        .replaceAll("'","&#039;");
}


/* =========================================================
   AUTOSAVE
========================================================= */

setInterval(()=>{

    if(
        player &&
        currentSave>=0 &&
        !document.getElementById("game")
        .classList.contains("hidden")
    ){

        autoSave();

    }

},5000);


/* =========================================================
   START
========================================================= */

showSaves();

</script>

</body>
</html>
