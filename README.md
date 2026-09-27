<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0">
<title>Spiritual Power: Shadowbound</title>

<style>
*{
    box-sizing:border-box;
    -webkit-tap-highlight-color:transparent;
}

body{
    margin:0;
    background:#05070e;
    color:white;
    font-family:Arial,Helvetica,sans-serif;
    overflow-x:hidden;
}

button,input,select{
    font-family:inherit;
}

button{
    border:0;
    border-radius:12px;
    padding:13px 18px;
    font-weight:900;
    cursor:pointer;
}

button:active{
    transform:scale(.95);
}

.screen{
    min-height:100vh;
    display:none;
    align-items:center;
    justify-content:center;
    padding:18px;
}

.screen.active{
    display:flex;
}

/* =========================
   MENU
========================= */

.panel{
    width:min(950px,96vw);
    background:
        linear-gradient(145deg,#18223e,#080b14);
    border:2px solid #536ca5;
    border-radius:24px;
    padding:25px;
    box-shadow:
        0 0 35px #000,
        inset 0 0 35px rgba(60,100,255,.08);
}

.title{
    text-align:center;
    font-size:clamp(35px,8vw,70px);
    font-weight:1000;
    letter-spacing:3px;
    margin:5px 0;

    text-shadow:
        0 4px 0 #000,
        0 0 20px #5479ff;
}

.subtitle{
    text-align:center;
    color:#aebde3;
    letter-spacing:5px;
}

.description{
    text-align:center;
    line-height:1.5;
    color:#dce4fa;
}

.save-grid{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:15px;
}

.save-slot{
    background:#0e1527;
    border:2px solid #34496f;
    border-radius:16px;
    padding:17px;
}

.save-slot:hover{
    border-color:#718cff;
    box-shadow:0 0 20px rgba(75,105,255,.25);
}

.save-buttons{
    display:flex;
    gap:7px;
    flex-wrap:wrap;
}

.primary{
    background:#e8bd43;
    color:#171208;
}

.dark{
    background:#2d426b;
    color:white;
}

.danger{
    background:#a92e43;
    color:white;
}

/* =========================
   CREATION
========================= */

.creation{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:20px;
}

.preview{
    min-height:330px;
    border-radius:18px;

    display:flex;
    align-items:center;
    justify-content:center;

    background:
        radial-gradient(
            circle,
            #354c80,
            #0b101c 65%
        );
}

label{
    display:block;
    color:#bdc9e5;
    margin-top:12px;
    margin-bottom:5px;
}

input,select{
    width:100%;
    padding:13px;
    background:#080d18;
    border:1px solid #52658c;
    border-radius:9px;
    color:white;
}

/* =========================
   HERO
========================= */

.hero{
    width:135px;
    height:225px;
    position:relative;

    filter:
        drop-shadow(0 0 15px #5275ff);
}

.hero-head{
    position:absolute;
    width:58px;
    height:58px;
    top:2px;
    left:38px;

    border:4px solid #111522;
    border-radius:50%;
    background:#e8b88e;
}

.hero-helmet{
    position:absolute;
    width:64px;
    height:28px;
    top:-4px;
    left:35px;

    background:#385ce0;
    border:4px solid #111522;

    border-radius:20px 20px 5px 5px;
}

.hero-body{
    position:absolute;
    width:86px;
    height:110px;
    top:60px;
    left:25px;

    background:#385ce0;
    border:5px solid #111522;

    border-radius:22px 22px 13px 13px;

    box-shadow:
        inset 0 0 20px rgba(255,255,255,.12);
}

.hero-body:after{
    content:"✦";
    position:absolute;
    font-size:35px;
    left:25px;
    top:30px;
    color:white;

    text-shadow:
        0 0 10px white;
}

.hero-arm{
    position:absolute;
    width:27px;
    height:78px;
    top:70px;

    background:#385ce0;
    border:4px solid #111522;
    border-radius:18px;
}

.hero-arm.left{
    left:0;
    transform:rotate(12deg);
}

.hero-arm.right{
    right:0;
    transform:rotate(-12deg);
}

.hero-leg{
    position:absolute;
    width:32px;
    height:70px;
    top:165px;

    background:#202c4d;
    border:4px solid #111522;
}

.hero-leg.left{
    left:28px;
}

.hero-leg.right{
    right:28px;
}

/* =========================
   GAME
========================= */

#game{
    padding:0;
    align-items:stretch;
}

.game{
    width:100%;
    min-height:100vh;

    display:flex;
    flex-direction:column;
}

.topbar{
    display:flex;
    align-items:center;
    gap:12px;
    padding:10px;

    background:#080c18;
    border-bottom:2px solid #34466c;

    z-index:50;
}

.player-info{
    min-width:170px;
}

.player-info b{
    font-size:18px;
}

.meters{
    flex:1;
    min-width:180px;
}

.meter{
    height:11px;
    background:#242b3c;
    border-radius:20px;
    overflow:hidden;
    margin:4px 0 7px;
}

.fill{
    height:100%;
    width:100%;
    transition:width .3s;
}

.hp{
    background:#e24d60;
}

.spirit{
    background:#f1c448;
}

/* =========================
   ARENA
========================= */

.arena{
    position:relative;
    flex:1;
    min-height:570px;
    overflow:hidden;

    background:
        radial-gradient(
            circle at 50% 35%,
            #324776 0%,
            #111a30 35%,
            #070a13 72%
        );
}

/* stars */

.stars{
    position:absolute;
    inset:0;

    background-image:
        radial-gradient(#fff 1px,transparent 1px);

    background-size:43px 43px;
    opacity:.18;

    animation:
        starMove 12s linear infinite;
}

@keyframes starMove{
    from{
        transform:translateY(0);
    }

    to{
        transform:translateY(43px);
    }
}

/* energy beams */

.energy{
    position:absolute;
    width:3px;
    height:70%;
    top:5%;

    background:#718cff;
    box-shadow:
        0 0 15px #718cff;

    opacity:.25;
}

.energy.one{
    left:20%;
    transform:rotate(12deg);
}

.energy.two{
    right:25%;
    transform:rotate(-12deg);
}

/* floor */

.ground{
    position:absolute;
    bottom:0;
    width:100%;
    height:25%;

    background:
        linear-gradient(
            #1a2337,
            #05070d
        );

    border-top:3px solid #536a99;

    box-shadow:
        0 -10px 30px rgba(70,100,200,.2);
}

/* =========================
   BATTLE CHARACTERS
========================= */

.battle-character{
    position:absolute;
    bottom:15%;
    z-index:5;
}

.player{
    left:9%;
}

.enemy{
    right:10%;
}

.character{
    width:145px;
    height:235px;
    position:relative;

    animation:
        idle 1.8s ease-in-out infinite;
}

@keyframes idle{
    0%,100%{
        transform:translateY(0);
    }

    50%{
        transform:translateY(-5px);
    }
}

.character .head{
    position:absolute;

    width:62px;
    height:62px;

    left:41px;
    top:0;

    background:#e8b88e;

    border:5px solid #111522;

    border-radius:50%;
}

.character .body{
    position:absolute;

    width:92px;
    height:120px;

    left:27px;
    top:62px;

    background:#385ce0;

    border:5px solid #111522;

    border-radius:24px 24px 15px 15px;

    box-shadow:
        inset 0 0 25px rgba(255,255,255,.12);
}

.character .body:after{
    content:"✦";

    position:absolute;

    left:29px;
    top:32px;

    font-size:37px;

    color:white;

    text-shadow:
        0 0 12px white;
}

.character .arm{
    position:absolute;

    width:29px;
    height:82px;

    top:75px;

    background:#385ce0;

    border:5px solid #111522;

    border-radius:20px;
}

.character .arm.left{
    left:0;
    transform:rotate(12deg);
}

.character .arm.right{
    right:0;
    transform:rotate(-12deg);
}

.character .leg{
    position:absolute;

    width:34px;
    height:75px;

    top:178px;

    background:#202b49;

    border:5px solid #111522;
}

.character .leg.left{
    left:31px;
}

.character .leg.right{
    right:31px;
}

/* enemy */

.enemy .character{
    transform:scale(1.35);

    filter:
        drop-shadow(0 0 25px #774cff);
}

.enemy .character .head{
    background:#161521;
}

.enemy .character .body{
    background:
        linear-gradient(
            145deg,
            #30294b,
            #171624
        );
}

.enemy .character .arm{
    background:#211d30;
}

.enemy .character .leg{
    background:#171522;
}

/* boss */

.enemy.boss .character{
    transform:scale(1.8);
}

.enemy.boss .character:before,
.enemy.boss .character:after{
    content:"";

    position:absolute;

    width:75px;
    height:45px;

    background:#302947;

    border:4px solid #171522;

    z-index:-1;

    top:30px;
}

.enemy.boss .character:before{
    left:-45px;

    transform:
        rotate(-25deg)
        skewX(-20deg);
}

.enemy.boss .character:after{
    right:-45px;

    transform:
        rotate(25deg)
        skewX(20deg);
}

/* =========================
   ATTACK ANIMATION
========================= */

.player.attacking .character{
    animation:
        playerAttack .35s ease;
}

.enemy.attacking .character{
    animation:
        enemyAttack .35s ease;
}

@keyframes playerAttack{

    0%{
        transform:translateX(0);
    }

    50%{
        transform:translateX(70px) scale(1.08);
    }

    100%{
        transform:translateX(0);
    }

}

@keyframes enemyAttack{

    0%{
        transform:translateX(0);
    }

    50%{
        transform:translateX(-70px) scale(1.08);
    }

    100%{
        transform:translateX(0);
    }

}

/* energy blast */

.blast{
    position:absolute;

    width:28px;
    height:28px;

    border-radius:50%;

    background:#fff;

    box-shadow:
        0 0 10px white,
        0 0 25px #6b8cff,
        0 0 50px #6b8cff;

    z-index:10;

    animation:
        blastMove .45s linear forwards;
}

@keyframes blastMove{
    from{
        left:22%;
        opacity:1;
    }

    to{
        left:72%;
        opacity:0;
    }
}

/* =========================
   NAMEPLATES
========================= */

.nameplate{
    position:absolute;

    bottom:calc(15% + 245px);

    padding:7px 12px;

    background:rgba(4,7,15,.9);

    border:1px solid #536991;

    border-radius:9px;

    z-index:8;

    font-weight:bold;
}

.player-name{
    left:9%;
}

.enemy-name{
    right:10%;
}

/* =========================
   COMBAT UI
========================= */

.controls{
    padding:11px;

    background:#080c18;

    border-top:2px solid #34466c;
}

.turn-display{
    text-align:center;

    font-weight:900;

    color:#f0c94c;

    font-size:17px;

    margin-bottom:7px;
}

.verse{
    background:#151e34;

    border-left:4px solid #e8bd43;

    border-radius:8px;

    padding:10px;

    line-height:1.4;

    margin-bottom:8px;
}

.verse-title{
    color:#f1cb55;
    font-weight:900;
}

.log{
    height:85px;

    overflow-y:auto;

    background:#05070d;

    border-radius:9px;

    padding:8px;

    font-size:14px;

    margin-bottom:8px;
}

.actions{
    display:flex;
    gap:8px;
    flex-wrap:wrap;
}

.action{
    flex:1;
    min-width:125px;

    background:#344b78;

    color:white;
}

.power-button{
    background:
        linear-gradient(
            135deg,
            #8b46d2,
            #5634a5
        );

    box-shadow:
        0 0 15px rgba(137,75,255,.35);
}

.action:disabled{
    opacity:.3;
}

/* =========================
   OVERLAY
========================= */

.overlay{
    position:absolute;
    inset:0;

    background:rgba(2,4,10,.9);

    display:none;

    align-items:center;
    justify-content:center;

    padding:20px;

    z-index:30;
}

.overlay.show{
    display:flex;
}

.overlay-card{
    max-width:620px;

    text-align:center;

    padding:30px;

    border-radius:20px;

    background:
        linear-gradient(
            145deg,
            #17213a,
            #090d18
        );

    border:2px solid #6178b0;

    box-shadow:
        0 0 40px #000;
}

.overlay-card h2{
    font-size:38px;
    margin-top:0;

    color:#f1c84d;

    text-shadow:
        0 0 15px #e5b93f;
}

/* =========================
   MOBILE
========================= */

@media(max-width:700px){

    .save-grid{
        grid-template-columns:1fr;
    }

    .creation{
        grid-template-columns:1fr;
    }

    .arena{
        min-height:440px;
    }

    .player{
        left:1%;
    }

    .enemy{
        right:1%;
    }

    .player-name{
        left:1%;
    }

    .enemy-name{
        right:1%;
    }

    .battle-character .character{
        transform:scale(.72);
    }

    .enemy .character{
        transform:scale(.9);
    }

    .enemy.boss .character{
        transform:scale(1.15);
    }

    .nameplate{
        font-size:11px;
    }

    .topbar{
        flex-wrap:wrap;
    }

}
</style>
</head>

<body>


<!-- ==================================
     SAVE MENU
================================== -->

<section id="home" class="screen active">

<div class="panel">

<h1 class="title">
SPIRITUAL POWER
</h1>

<div class="subtitle">
SHADOWBOUND
</div>

<p class="description">
Build your Spiritual Power, unlock new techniques,
and survive the forces of darkness.
</p>

<h2>Choose Your Save</h2>

<div
    id="saveSlots"
    class="save-grid">
</div>

</div>

</section>


<!-- ==================================
     CHARACTER CREATION
================================== -->

<section id="customize" class="screen">

<div class="panel">

<h2>Create Your Warrior</h2>

<div class="creation">

<div class="preview">

<div class="hero">

<div
    id="previewHead"
    class="hero-head">
</div>

<div
    id="previewHelmet"
    class="hero-helmet">
</div>

<div
    id="previewBody"
    class="hero-body">
</div>

<div class="hero-arm left"></div>
<div class="hero-arm right"></div>

<div class="hero-leg left"></div>
<div class="hero-leg right"></div>

</div>

</div>


<div>

<label>
Warrior Name
</label>

<input
    id="playerNameInput"
    maxlength="16"
    placeholder="Warrior"
>


<label>
Gender
</label>

<select id="genderInput">

<option>Male</option>
<option>Female</option>
<option>Other</option>

</select>


<label>
Armor Color
</label>

<select id="armorInput">

<option value="#385ce0">
Royal Blue
</option>

<option value="#a63d50">
Crimson
</option>

<option value="#399b77">
Emerald
</option>

<option value="#8750b8">
Violet
</option>

<option value="#d29a2d">
Gold
</option>

</select>


<label>
Helmet Color
</label>

<select id="helmetInput">

<option value="#171b2c">
Dark
</option>

<option value="#e1d5c0">
Light
</option>

<option value="#6b3b22">
Brown
</option>

<option value="#31538e">
Blue
</option>

</select>

<br>

<button
    class="primary"
    onclick="createPlayer()">
BEGIN JOURNEY
</button>

<button
    class="dark"
    onclick="showScreen('home')">
BACK
</button>

</div>

</div>

</div>

</section>


<!-- ==================================
     GAME
================================== -->

<section id="game" class="screen">

<div class="game">


<div class="topbar">

<div class="player-info">

<b id="playerDisplay">
Warrior
</b>

<div>
Level:
<span id="levelDisplay">1</span>
</div>

<div>
Spiritual Power:
<span id="powerDisplay">0</span>
</div>

</div>


<div class="meters">

<div>HP</div>

<div class="meter">

<div
    id="hpMeter"
    class="fill hp">
</div>

</div>


<div>SPIRIT</div>

<div class="meter">

<div
    id="spiritMeter"
    class="fill spirit">
</div>

</div>

</div>


<button
    class="dark"
    onclick="saveAndExit()">

SAVE & EXIT

</button>

</div>


<div class="arena">

<div class="stars"></div>

<div class="energy one"></div>
<div class="energy two"></div>

<div class="ground"></div>


<!-- PLAYER -->

<div
    id="playerNamePlate"
    class="nameplate player-name">
</div>

<div
    id="playerCharacter"
    class="battle-character player">

<div class="character">

<div
    id="playerBattleHead"
    class="head">
</div>

<div
    id="playerBattleBody"
    class="body">
</div>

<div class="arm left"></div>
<div class="arm right"></div>

<div class="leg left"></div>
<div class="leg right"></div>

</div>

</div>


<!-- ENEMY -->

<div
    id="enemyNamePlate"
    class="nameplate enemy-name">
</div>

<div
    id="enemyCharacter"
    class="battle-character enemy">

<div class="character">

<div class="head"></div>

<div class="body"></div>

<div class="arm left"></div>
<div class="arm right"></div>

<div class="leg left"></div>
<div class="leg right"></div>

</div>

</div>


<!-- POPUP -->

<div
    id="overlay"
    class="overlay">

<div
    id="overlayCard"
    class="overlay-card">
</div>

</div>

</div>


<!-- ==================================
     COMBAT CONTROLS
================================== -->

<div class="controls">

<div
    id="turnDisplay"
    class="turn-display">
TURN 0 / 3
</div>


<div
    id="battleVerse"
    class="verse">
</div>


<div
    id="battleLog"
    class="log">
</div>


<div class="actions">

<button
    class="action"
    onclick="attack('strike')">

SPIRIT STRIKE

</button>


<button
    class="action"
    onclick="attack('shield')">

SHIELD OF FAITH

</button>


<button
    class="action"
    onclick="attack('word')">

WORD OF TRUTH

</button>


<button
    id="powerMove"
    class="action power-button"
    onclick="attack('special')">

POWER MOVE

</button>

</div>

</div>

</div>

</section>


<script>

/* ==========================================
   SAVE DATA
========================================== */

const SAVE_KEY =
"spiritualPowerShadowboundSaves";

let saves =
JSON.parse(
    localStorage.getItem(SAVE_KEY)
) || [null,null,null];

let currentSlot = -1;

let player = null;

let enemy = null;

let battleLocked = false;


/* ==========================================
   LEVELS
========================================== */

const levels = [

{
    name:"Shadow Demons",

    hp:100,

    requiredPower:5,

    verse:
    "Ephesians 6:11 — " +
    "\"Put on the whole armour of God, " +
    "that ye may be able to stand against " +
    "the wiles of the devil.\"",

    special:"LIGHT BURST"
},

{
    name:"Dark Angel",

    hp:200,

    requiredPower:12,

    verse:
    "Psalm 18:2 — " +
    "\"The LORD is my rock, and my fortress, " +
    "and my deliverer; my God, my strength, " +
    "in whom I will trust.\"",

    special:"HOLY BREAKER"
},

{
    name:"Shadow Colossus",

    hp:380,

    requiredPower:25,

    verse:
    "1 John 4:4 — " +
    "\"Greater is he that is in you, " +
    "than he that is in the world.\"",

    special:"VICTORY ROAR"
}

];


/* ==========================================
   SCREEN
========================================== */

function showScreen(id){

    document
        .querySelectorAll(".screen")
        .forEach(x =>
            x.classList.remove("active")
        );

    document
        .getElementById(id)
        .classList.add("active");
}


/* ==========================================
   SAVE MENU
========================================== */

function renderSaveSlots(){

    const box =
        document.getElementById(
            "saveSlots"
        );

    box.innerHTML = "";

    saves.forEach((save,index)=>{

        const slot =
            document.createElement("div");

        slot.className =
            "save-slot";

        if(save){

            slot.innerHTML = `

                <h3>SAVE ${index+1}</h3>

                <p>
                    ${escapeHTML(save.name)}
                </p>

                <p>
                    Level ${save.level}
                </p>

                <p>
                    Spiritual Power:
                    ${save.power}
                </p>

                <div class="save-buttons">

                    <button
                        class="primary"
                        onclick="continueSave(${index})">

                        CONTINUE

                    </button>

                    <button
                        class="danger"
                        onclick="deleteSave(${index})">

                        DELETE

                    </button>

                </div>
            `;

        }else{

            slot.innerHTML = `

                <h3>SAVE ${index+1}</h3>

                <p>Empty Save</p>

                <button
                    class="primary"
                    onclick="newSave(${index})">

                    NEW GAME

                </button>
            `;
        }

        box.appendChild(slot);

    });
}


/* ==========================================
   ESCAPE
========================================== */

function escapeHTML(text){

    return String(text)
        .replace(/[&<>"']/g,c=>({

            "&":"&amp;",
            "<":"&lt;",
            ">":"&gt;",
            '"':"&quot;",
            "'":"&#039;"

        }[c]));

}


/* ==========================================
   NEW SAVE
========================================== */

function newSave(index){

    currentSlot = index;

    document
        .getElementById(
            "playerNameInput"
        )
        .value = "";

    showScreen("customize");
}


/* ==========================================
   CONTINUE
========================================== */

function continueSave(index){

    currentSlot = index;

    player =
        JSON.parse(
            JSON.stringify(
                saves[index]
            )
        );

    startGame();
}


/* ==========================================
   DELETE
========================================== */

function deleteSave(index){

    if(
        !confirm(
            "Delete Save " +
            (index+1) +
            "?\n\nThis cannot be undone."
        )
    )
        return;

    saves[index] = null;

    localStorage.setItem(
        SAVE_KEY,
        JSON.stringify(saves)
    );

    renderSaveSlots();
}


/* ==========================================
   CREATE PLAYER
========================================== */

function createPlayer(){

    player = {

        name:
            document
                .getElementById(
                    "playerNameInput"
                )
                .value
                .trim() ||
            "Warrior",

        gender:
            document
                .getElementById(
                    "genderInput"
                )
                .value,

        armor:
            document
                .getElementById(
                    "armorInput"
                )
                .value,

        helmet:
            document
                .getElementById(
                    "helmetInput"
                )
                .value,

        level:1,

        power:0,

        hp:100,

        spirit:0,

        defense:0,

        /* NEW */

        turns:0,

        specialUnlocked:false

    };

    saveGame();

    startGame();
}


/* ==========================================
   SAVE
========================================== */

function saveGame(){

    if(currentSlot < 0)
        return;

    saves[currentSlot] =
        JSON.parse(
            JSON.stringify(player)
        );

    localStorage.setItem(
        SAVE_KEY,
        JSON.stringify(saves)
    );
}


/* ==========================================
   EXIT
========================================== */

function saveAndExit(){

    saveGame();

    renderSaveSlots();

    showScreen("home");
}


/* ==========================================
   START GAME
========================================== */

function startGame(){

    const level =
        levels[player.level-1];

    enemy = {

        name:level.name,

        hp:level.hp,

        maxHP:level.hp

    };

    player.hp =
        Math.min(
            player.hp || 100,
            100
        );

    player.spirit =
        player.spirit || 0;

    player.turns =
        player.turns || 0;

    player.specialUnlocked =
        player.turns >= 3;

    player.defense = 0;

    document
        .getElementById(
            "playerBattleBody"
        )
        .style.background =
            player.armor;

    document
        .getElementById(
            "playerBattleHead"
        )
        .style.background =
            player.helmet;

    showScreen("game");

    writeLog(
        "A shadow appears before you..."
    );

    renderGame();
}


/* ==========================================
   RENDER
========================================== */

function renderGame(){

    const level =
        levels[player.level-1];

    document
        .getElementById(
            "playerDisplay"
        )
        .textContent =
            player.name;

    document
        .getElementById(
            "playerNamePlate"
        )
        .textContent =
            player.name;

    document
        .getElementById(
            "levelDisplay"
        )
        .textContent =
            player.level;

    document
        .getElementById(
            "powerDisplay"
        )
        .textContent =
            player.power;

    document
        .getElementById(
            "hpMeter"
        )
        .style.width =
            player.hp + "%";

    document
        .getElementById(
            "spiritMeter"
        )
        .style.width =
            player.spirit + "%";

    document
        .getElementById(
            "enemyNamePlate"
        )
        .textContent =
            enemy.name +
            " • " +
            Math.max(
                0,
                enemy.hp
            ) +
            " HP";

    document
        .getElementById(
            "battleVerse"
        )
        .innerHTML = `

            <div class="verse-title">
                BATTLE VERSE
            </div>

            ${level.verse}
        `;


    /* TURN COUNTER */

    document
        .getElementById(
            "turnDisplay"
        )
        .textContent =
            "TURNS SURVIVED: " +
            player.turns +
            " / 3";


    /* POWER MOVE */

    const power =
        document.getElementById(
            "powerMove"
        );

    if(player.specialUnlocked){

        power.disabled = false;

        power.textContent =
            level.special +
            " — UNLOCKED";

    }else{

        power.disabled = true;

        power.textContent =
            "POWER MOVE — " +
            (3-player.turns) +
            " TURNS";

    }


    /* BOSS */

    const enemyElement =
        document.getElementById(
            "enemyCharacter"
        );

    if(player.level === 3){

        enemyElement.classList.add(
            "boss"
        );

    }else{

        enemyElement.classList.remove(
            "boss"
        );

    }

}


/* ==========================================
   LOG
========================================== */

function writeLog(message){

    const log =
        document.getElementById(
            "battleLog"
        );

    log.innerHTML =
        "<div>" +
        message +
        "</div>" +
        log.innerHTML;
}


/* ==========================================
   ATTACK
========================================== */

function attack(type){

    if(battleLocked)
        return;

    /*
       POWER MOVE CAN ONLY BE USED
       AFTER 3 COMPLETE TURNS
    */

    if(
        type === "special" &&
        !player.specialUnlocked
    ){

        writeLog(
            "You must survive 3 turns first!"
        );

        return;
    }

    battleLocked = true;


    let damage = 0;

    let spiritGain = 0;


    /* SPIRIT STRIKE */

    if(type === "strike"){

        damage =
            15 +
            player.level * 5;

        spiritGain = 12;

        writeLog(
            "SPIRIT STRIKE!"
        );
    }


    /* SHIELD */

    if(type === "shield"){

        damage = 7;

        spiritGain = 18;

        player.defense = 28;

        writeLog(
            "SHIELD OF FAITH!"
        );
    }


    /* WORD */

    if(type === "word"){

        damage =
            24 +
            player.level * 6;

        spiritGain = 24;

        writeLog(
            "WORD OF TRUTH!"
        );
    }


    /* POWER MOVE */

    if(type === "special"){

        damage =
            75 +
            player.level * 25;

        player.spirit = 0;

        spiritGain = 15;

        writeLog(
            "⚡ SPIRITUAL POWER RELEASED!"
        );
    }


    /* ATTACK ANIMATION */

    const playerCharacter =
        document.getElementById(
            "playerCharacter"
        );

    playerCharacter.classList.add(
        "attacking"
    );

    createBlast();


    setTimeout(()=>{

        playerCharacter.classList.remove(
            "attacking"
        );

    },400);


    enemy.hp -= damage;

    player.spirit =
        Math.min(
            100,
            player.spirit +
            spiritGain
        );

    renderGame();


    /* ENEMY DEFEATED */

    if(enemy.hp <= 0){

        setTimeout(
            levelComplete,
            650
        );

        return;
    }


    /*
       IMPORTANT:
       THE ENEMY ALWAYS ATTACKS
       AFTER THE PLAYER.
    */

    setTimeout(
        enemyAttack,
        800
    );
}


/* ==========================================
   BLAST
========================================== */

function createBlast(){

    const arena =
        document.querySelector(
            ".arena"
        );

    const blast =
        document.createElement(
            "div"
        );

    blast.className =
        "blast";

    arena.appendChild(blast);

    setTimeout(()=>{

        blast.remove();

    },500);
}


/* ==========================================
   ENEMY ATTACK
========================================== */

function enemyAttack(){

    const enemyCharacter =
        document.getElementById(
            "enemyCharacter"
        );

    enemyCharacter.classList.add(
        "attacking"
    );

    setTimeout(()=>{

        enemyCharacter.classList.remove(
            "attacking"
        );

    },400);


    let damage =
        10 +
        player.level * 5;


    const blocked =
        Math.min(
            damage,
            player.defense || 0
        );

    damage =
        Math.max(
            2,
            damage -
            blocked
        );

    player.defense = 0;

    player.hp -= damage;

    player.spirit =
        Math.min(
            100,
            player.spirit + 7
        );


    writeLog(
        enemy.name +
        " attacks for " +
        damage +
        " damage!"
    );


    /*
       ONE COMPLETE TURN HAS NOW
       FINISHED.
    */

    player.turns++;


    /*
       AFTER 3 TURNS,
       POWER MOVE UNLOCKS.
    */

    if(
        player.turns >= 3 &&
        !player.specialUnlocked
    ){

        player.specialUnlocked = true;

        writeLog(
            "⚡ POWER MOVE UNLOCKED!"
        );
    }


    renderGame();


    /* PLAYER DEFEATED */

    if(player.hp <= 0){

        player.hp = 100;

        player.spirit = 0;

        player.turns = 0;

        player.specialUnlocked = false;

        enemy.hp = enemy.maxHP;

        showOverlay(

            "BATTLE LOST",

            "The darkness overwhelmed you. " +
            "Survive 3 turns to unlock your " +
            "stronger attack.",

            "TRY AGAIN"

        );

        return;
    }


    /*
       AUTO SAVE AFTER EVERY TURN
    */

    saveGame();

    battleLocked = false;
}


/* ==========================================
   LEVEL COMPLETE
========================================== */

function levelComplete(){

    if(player.level < 3){

        player.level++;

        player.power +=
            levels[
                player.level-1
            ].requiredPower;

        player.hp = 100;

        player.spirit = 0;

        /*
           NEW BATTLE STARTS AT TURN 0
        */

        player.turns = 0;

        player.specialUnlocked = false;


        const next =
            levels[
                player.level-1
            ];

        enemy = {

            name:next.name,

            hp:next.hp,

            maxHP:next.hp

        };


        saveGame();

        renderGame();

        showOverlay(

            "LEVEL UP!",

            "Your Spiritual Power has increased. " +
            "Survive three turns in the next battle " +
            "to unlock your stronger attack.",

            "ENTER BATTLE"

        );

    }else{

        player.power += 50;

        saveGame();

        showOverlay(

            "VICTORY!",

            "The Shadow Colossus has fallen. " +
            "You completed all three battles " +
            "and gained 50 Spiritual Power.",

            "CONTINUE"

        );
    }
}


/* ==========================================
   OVERLAY
========================================== */

function showOverlay(
    title,
    message,
    button
){

    document
        .getElementById(
            "overlayCard"
        )
        .innerHTML = `

            <h2>
                ${title}
            </h2>

            <p>
                ${message}
            </p>

            <button
                class="primary"
                onclick="closeOverlay()">

                ${button}

            </button>
        `;

    document
        .getElementById(
            "overlay"
        )
        .classList.add("show");
}


/* ==========================================
   CLOSE OVERLAY
========================================== */

function closeOverlay(){

    document
        .getElementById(
            "overlay"
        )
        .classList.remove("show");

    player.hp = 100;

    player.spirit = 0;

    player.defense = 0;

    const level =
        levels[
            player.level-1
        ];

    enemy = {

        name:level.name,

        hp:level.hp,

        maxHP:level.hp

    };


    renderGame();

    battleLocked = false;

    saveGame();
}


/* ==========================================
   PREVIEW
========================================== */

function updatePreview(){

    const armor =
        document
            .getElementById(
                "armorInput"
            )
            .value;

    const helmet =
        document
            .getElementById(
                "helmetInput"
            )
            .value;

    document
        .getElementById(
            "previewBody"
        )
        .style.background =
            armor;

    document
        .getElementById(
            "previewHelmet"
        )
        .style.background =
            armor;

    document
        .getElementById(
            "previewHead"
        )
        .style.background =
            helmet;
}


document
    .getElementById(
        "armorInput"
    )
    .addEventListener(
        "change",
        updatePreview
    );

document
    .getElementById(
        "helmetInput"
    )
    .addEventListener(
        "change",
        updatePreview
    );


/* ==========================================
   AUTO SAVE
========================================== */

setInterval(()=>{

    if(
        player &&
        currentSlot >= 0 &&
        document
            .getElementById("game")
            .classList.contains("active")
    ){

        saveGame();

    }

},5000);


/* ==========================================
   START
========================================== */

renderSaveSlots();

updatePreview();

</script>

</body>
</html>
