<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport"
      content="width=device-width,initial-scale=1.0,maximum-scale=1.0">

<title>Spiritual Power: Shadowbound</title>

<style>

/* =========================================================
   CORE
========================================================= */

*{
    box-sizing:border-box;
    -webkit-tap-highlight-color:transparent;
}

html,body{
    margin:0;
    min-height:100%;
    background:#03050a;
    color:white;
    font-family:Arial,Helvetica,sans-serif;
}

body{
    overflow-x:hidden;
}

button,
input,
select{
    font:inherit;
}

button{
    cursor:pointer;
}

.hidden{
    display:none!important;
}

/* =========================================================
   APP
========================================================= */

#app{
    width:100%;
    max-width:1150px;
    margin:auto;
    padding:12px;
    min-height:100vh;
}

.panel{
    background:
        linear-gradient(
            145deg,
            rgba(22,30,52,.94),
            rgba(5,8,16,.96)
        );
    border:1px solid rgba(145,165,210,.2);
    border-radius:20px;
    padding:18px;

    box-shadow:
        0 20px 60px rgba(0,0,0,.55),
        inset 0 1px rgba(255,255,255,.07);
}

/* =========================================================
   SAVE SCREEN
========================================================= */

.title{
    text-align:center;
    margin:5px 0 0;
    font-size:clamp(30px,7vw,55px);
    letter-spacing:3px;

    color:#fff5bd;

    text-shadow:
        0 0 10px #ffe36b,
        0 0 30px #ffb300;
}

.subtitle{
    text-align:center;
    color:#aeb9d4;
    margin:8px 0 25px;
}

.saveGrid{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:15px;
}

.saveCard{
    min-height:180px;

    display:flex;
    flex-direction:column;
    justify-content:space-between;

    padding:18px;

    border-radius:18px;

    background:
        linear-gradient(
            145deg,
            #18213a,
            #080c16
        );

    border:1px solid #3d4964;

    transition:.2s;
}

.saveCard:hover{
    border-color:#ffd54a;
    transform:translateY(-3px);
    box-shadow:0 0 30px rgba(255,207,60,.14);
}

.goldButton{
    border:0;
    padding:14px;
    border-radius:12px;

    font-weight:900;
    color:#171109;

    background:
        linear-gradient(
            180deg,
            #fff3a6,
            #ffd33d,
            #b97600
        );

    box-shadow:
        0 5px 18px rgba(255,198,50,.25);
}

.redButton{
    border:1px solid #793444;
    padding:10px;
    border-radius:10px;

    color:#ff9aaa;
    background:#2d1119;
}

/* =========================================================
   CHARACTER CREATION
========================================================= */

.custom{
    max-width:650px;
    margin:30px auto;
}

.field{
    margin:15px 0;
}

.field label{
    display:block;
    margin-bottom:7px;
    color:#cbd4e9;
}

input,
select{
    width:100%;
    padding:13px;

    border-radius:11px;
    border:1px solid #414e6c;

    color:white;
    background:#080d19;
}

.colorGrid{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:12px;
}

input[type=color]{
    height:52px;
    padding:3px;
}

/* =========================================================
   HUD
========================================================= */

.topHud{
    display:grid;
    grid-template-columns:1fr auto 1fr;
    gap:12px;
    align-items:center;
}

.playerName{
    font-size:17px;
    font-weight:900;
}

.enemyName{
    text-align:right;
    font-size:17px;
    font-weight:900;
}

.levelBadge{
    padding:9px 15px;
    border-radius:999px;

    color:#1b1304;
    font-weight:900;

    background:
        linear-gradient(
            180deg,
            #fff3a2,
            #d69a1d
        );

    box-shadow:
        0 0 15px rgba(255,207,63,.3);
}

/* =========================================================
   HEALTH
========================================================= */

.healthBox{
    margin-top:7px;
}

.healthText{
    display:flex;
    justify-content:space-between;

    font-size:12px;
    color:#cbd3e4;

    margin-bottom:4px;
}

.healthBar{
    height:20px;
    padding:3px;

    overflow:hidden;

    border-radius:999px;

    background:#06080d;

    border:1px solid #6c551c;

    box-shadow:
        inset 0 2px 7px #000;
}

.playerHealth{
    width:100%;
    height:100%;

    border-radius:999px;

    background:
        linear-gradient(
            180deg,
            #fff9b2 0%,
            #ffe047 30%,
            #e5a913 65%,
            #8e5900 100%
        );

    box-shadow:
        0 0 12px #ffd83d,
        inset 0 2px rgba(255,255,255,.9);

    transition:width .45s ease;
}

.enemyHealth{
    width:100%;
    height:100%;

    border-radius:999px;

    background:
        linear-gradient(
            180deg,
            #ffabb9,
            #ed3158,
            #740d27
        );

    box-shadow:
        0 0 13px #ff315e;

    transition:width .45s ease;
}

/* =========================================================
   ARENA
========================================================= */

.arena{
    position:relative;

    height:500px;

    overflow:hidden;

    margin-top:12px;

    border-radius:25px;

    border:1px solid #394967;

    background:

        radial-gradient(
            circle at 50% 28%,
            rgba(84,119,190,.24),
            transparent 30%
        ),

        radial-gradient(
            circle at 50% 100%,
            rgba(255,196,45,.08),
            transparent 35%
        ),

        linear-gradient(
            180deg,
            #101a31,
            #070b15 65%,
            #03050a
        );

    box-shadow:
        inset 0 0 90px rgba(0,0,0,.85),
        0 20px 55px rgba(0,0,0,.5);
}

/* stars */

.arena::before{
    content:"";

    position:absolute;
    inset:0;

    opacity:.32;

    background-image:
        radial-gradient(circle,#fff 1px,transparent 1px),
        radial-gradient(circle,#8ba8ff 1px,transparent 1px);

    background-size:
        67px 59px,
        109px 83px;
}

/* floor */

.floor{
    position:absolute;

    left:-10%;
    right:-10%;
    bottom:-70px;

    height:220px;

    transform:
        perspective(300px)
        rotateX(55deg);

    background:

        repeating-linear-gradient(
            90deg,
            transparent 0 55px,
            rgba(105,153,232,.13) 56px 57px
        ),

        repeating-linear-gradient(
            0deg,
            transparent 0 40px,
            rgba(105,153,232,.10) 41px 42px
        );

    box-shadow:
        0 -20px 50px rgba(61,106,188,.1);
}

/* =========================================================
   WARRIOR
========================================================= */

.fighter{
    position:absolute;

    width:135px;
    height:235px;

    bottom:75px;

    z-index:10;
}

#player{
    left:12%;
}

#enemy{
    right:12%;
    transform:scaleX(-1);
}

/* head */

.head{
    position:absolute;

    left:41px;
    top:3px;

    width:53px;
    height:56px;

    border-radius:
        48%
        48%
        42%
        42%;

    background:
        linear-gradient(
            145deg,
            #ffffff,
            #8793aa
        );

    border:3px solid #222c42;

    box-shadow:
        0 0 17px rgba(255,255,255,.2);
}

.visor{
    position:absolute;

    left:5px;
    top:19px;

    width:43px;
    height:13px;

    border-radius:10px;

    background:
        linear-gradient(
            90deg,
            #0b111b,
            #c9f5ff,
            #0b111b
        );

    box-shadow:
        0 0 13px #8beaff;
}

/* body */

.body{
    position:absolute;

    left:25px;
    top:57px;

    width:84px;
    height:108px;

    border-radius:
        27px
        27px
        17px
        17px;

    background:
        linear-gradient(
            145deg,
            #ffffff 0%,
            var(--armor) 28%,
            #111927 100%
        );

    border:4px solid #263148;

    box-shadow:
        0 0 20px var(--armor),
        inset 6px 0 11px rgba(255,255,255,.28);
}

/* chest light */

.core{
    position:absolute;

    left:26px;
    top:22px;

    width:31px;
    height:31px;

    transform:rotate(45deg);

    background:#fff;

    border:4px solid #ffd83f;

    box-shadow:
        0 0 10px #fff,
        0 0 28px #ffd83f;
}

/* arms */

.arm{
    position:absolute;

    top:67px;

    width:26px;
    height:86px;

    border-radius:18px;

    background:
        linear-gradient(
            90deg,
            #111927,
            var(--armor),
            #dce5f4
        );

    border:3px solid #263148;
}

.leftArm{
    left:3px;
    transform:rotate(14deg);
}

.rightArm{
    right:3px;
    transform:rotate(-14deg);
}

/* legs */

.leg{
    position:absolute;

    top:157px;

    width:30px;
    height:79px;

    border-radius:10px;

    background:
        linear-gradient(
            90deg,
            #101725,
            var(--armor),
            #9da9bd
        );

    border:3px solid #263148;
}

.leftLeg{
    left:31px;
}

.rightLeg{
    right:31px;
}

/* =========================================================
   ENEMY DESIGN
========================================================= */

.enemy .head{
    background:
        linear-gradient(
            145deg,
            #1a1b2a,
            #050509
        );

    border-color:#694eff;
}

.enemy .visor{
    background:
        linear-gradient(
            90deg,
            #21000b,
            #ff315e,
            #21000b
        );

    box-shadow:
        0 0 16px #ff315e;
}

.enemy .body{
    background:
        linear-gradient(
            145deg,
            #050509,
            #292d3f,
            #030305
        );

    box-shadow:
        0 0 24px #7954ff;
}

.enemy .core{
    background:#241437;

    border-color:#a86cff;

    box-shadow:
        0 0 25px #a86cff;
}

/* =========================================================
   GENERAL ANIMATIONS
========================================================= */

.dash{
    animation:dashAttack .7s ease-in-out;
}

@keyframes dashAttack{

    0%{
        transform:translateX(0);
    }

    35%{
        transform:translateX(105px);
    }

    55%{
        transform:translateX(105px) scale(1.08);
    }

    100%{
        transform:translateX(0);
    }
}

.enemyDash{
    animation:enemyDash .7s ease-in-out;
}

@keyframes enemyDash{

    0%{
        transform:scaleX(-1) translateX(0);
    }

    35%{
        transform:scaleX(-1) translateX(105px);
    }

    55%{
        transform:scaleX(-1) translateX(105px);
    }

    100%{
        transform:scaleX(-1) translateX(0);
    }
}

/* =========================================================
   ATTACK 1 — LIGHT SHOT
========================================================= */

.lightShot{
    position:absolute;

    z-index:30;

    width:25px;
    height:25px;

    border-radius:50%;

    background:#fff;

    box-shadow:
        0 0 10px #fff,
        0 0 25px #fff0a0,
        0 0 55px #ffc400;

    animation:
        lightShotMove .65s linear forwards;
}

@keyframes lightShotMove{

    from{
        left:24%;
        top:47%;
        transform:scale(.5);
    }

    to{
        left:73%;
        top:47%;
        transform:scale(2);
    }
}

/* =========================================================
   ATTACK 2 — SHIELD
========================================================= */

.shield{
    position:absolute;

    z-index:25;

    left:9%;
    top:28%;

    width:150px;
    height:220px;

    border-radius:
        50%
        18%
        50%
        18%;

    border:5px solid #a8ddff;

    background:
        radial-gradient(
            circle,
            rgba(170,230,255,.24),
            rgba(40,130,255,.05)
        );

    box-shadow:
        0 0 20px #63c8ff,
        inset 0 0 30px rgba(180,235,255,.25);

    animation:shieldAppear .5s ease;
}

@keyframes shieldAppear{

    from{
        opacity:0;
        transform:scale(.5);
    }

    to{
        opacity:1;
        transform:scale(1);
    }
}

.shieldBreak{
    animation:shieldBlock .5s ease;
}

@keyframes shieldBlock{

    0%{
        filter:brightness(1);
    }

    35%{
        filter:brightness(3);
        transform:scale(1.08);
    }

    100%{
        filter:brightness(1);
        transform:scale(1);
    }
}

/* =========================================================
   ATTACK 3 — WORD OF TRUTH
========================================================= */

.truthBeam{
    position:absolute;

    z-index:25;

    right:22%;

    top:-10px;

    width:45px;
    height:480px;

    background:
        linear-gradient(
            90deg,
            transparent,
            #fff,
            #ffe776,
            #fff,
            transparent
        );

    box-shadow:
        0 0 20px #fff,
        0 0 50px #ffd83d,
        0 0 90px #ffb300;

    animation:
        truthBeam .75s ease-out forwards;
}

@keyframes truthBeam{

    0%{
        opacity:0;
        transform:scaleY(.1);
    }

    35%{
        opacity:1;
        transform:scaleY(1);
    }

    100%{
        opacity:.1;
        transform:scaleY(1);
    }
}

/* =========================================================
   SPECIAL — MASSIVE LIGHT BEAM
========================================================= */

.superBeam{
    position:absolute;

    z-index:40;

    left:22%;
    top:43%;

    width:0;
    height:38px;

    border-radius:30px;

    background:
        linear-gradient(
            90deg,
            #fff,
            #fffbd4,
            #ffd42e,
            #fff,
            #fff
        );

    box-shadow:
        0 0 15px white,
        0 0 35px #fff,
        0 0 75px #ffd21f,
        0 0 120px #ff9d00;

    animation:
        superBeam .9s ease-out forwards;
}

@keyframes superBeam{

    0%{
        width:0;
        opacity:0;
    }

    15%{
        width:15%;
        opacity:1;
    }

    100%{
        width:65%;
        opacity:0;
    }
}

/* =========================================================
   IMPACTS
========================================================= */

.impact{
    position:absolute;

    z-index:50;

    width:90px;
    height:90px;

    border-radius:50%;

    border:5px solid white;

    box-shadow:
        0 0 20px white,
        0 0 45px #ffd83d;

    animation:
        impact .45s ease-out forwards;
}

@keyframes impact{

    from{
        transform:scale(.2);
        opacity:1;
    }

    to{
        transform:scale(2);
        opacity:0;
    }
}

/* enemy hit */

.enemyHit{
    animation:enemyHit .4s ease;
}

@keyframes enemyHit{

    0%,100%{
        filter:none;
    }

    30%{
        filter:brightness(3);
    }

    50%{
        transform:scaleX(-1) translateX(13px);
    }

    70%{
        transform:scaleX(-1) translateX(-13px);
    }
}

/* player hit */

.playerHit{
    animation:playerHit .4s ease;
}

@keyframes playerHit{

    0%,100%{
        filter:none;
    }

    30%{
        filter:brightness(2.5);
    }

    50%{
        transform:translateX(-13px);
    }

    70%{
        transform:translateX(13px);
    }
}

/* =========================================================
   CONTROLS
========================================================= */

.controls{
    display:grid;

    grid-template-columns:
        repeat(4,1fr);

    gap:10px;

    margin-top:12px;
}

.attackButton{
    min-height:70px;

    padding:10px;

    border-radius:14px;

    border:1px solid #4c5974;

    color:white;

    background:
        linear-gradient(
            145deg,
            #27344f,
            #0d1423
        );

    font-weight:900;

    box-shadow:
        0 7px 15px rgba(0,0,0,.35);
}

.attackButton small{
    color:#aebbd6;
}

.attackButton.special{
    border-color:#ffd23d;

    background:
        linear-gradient(
            145deg,
            #5b4710,
            #1b1405
        );

    color:#ffe88a;
}

.attackButton:disabled{
    opacity:.35;
}

/* =========================================================
   LOG
========================================================= */

.log{
    margin-top:12px;

    min-height:58px;

    padding:13px;

    border-radius:12px;

    background:#060a13;

    border:1px solid #283248;

    color:#d9dfed;
}

/* =========================================================
   VERSE
========================================================= */

.verse{
    margin-top:12px;

    padding:15px;

    line-height:1.5;

    border-left:4px solid #ffd23d;

    background:
        rgba(255,208,61,.055);

    color:#eee6bd;

    border-radius:10px;
}

.verse strong{
    color:#ffd23d;
}

/* =========================================================
   VICTORY
========================================================= */

.overlay{
    position:fixed;

    inset:0;

    z-index:200;

    display:flex;

    align-items:center;
    justify-content:center;

    padding:20px;

    background:rgba(0,0,0,.82);
}

.overlayBox{
    width:100%;
    max-width:520px;

    text-align:center;

    padding:35px;

    border-radius:25px;

    border:1px solid #ffd23d;

    background:
        linear-gradient(
            145deg,
            #19223c,
            #060912
        );

    box-shadow:
        0 0 70px rgba(255,210,50,.25);
}

/* =========================================================
   MOBILE
========================================================= */

@media(max-width:750px){

    #app{
        padding:7px;
    }

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
        height:420px;
    }

    .fighter{
        transform:scale(.78);
        bottom:48px;
    }

    #player{
        left:0%;
    }

    #enemy{
        right:0%;
    }

    .controls{
        grid-template-columns:1fr 1fr;
    }

    .attackButton{
        min-height:64px;
    }
}

</style>
</head>

<body>

<div id="app">

<!-- =====================================================
     SAVE SCREEN
===================================================== -->

<section id="saveScreen" class="panel">

    <h1 class="title">
        SPIRITUAL POWER
    </h1>

    <div class="subtitle">
        SHADOWBOUND
    </div>

    <div id="saveGrid" class="saveGrid"></div>

</section>


<!-- =====================================================
     CHARACTER CREATION
===================================================== -->

<section id="customScreen"
         class="panel custom hidden">

    <h2>⚔️ CREATE YOUR WARRIOR</h2>

    <div class="field">

        <label>Warrior Name</label>

        <input
            id="nameInput"
            maxlength="18"
            placeholder="Enter your name">

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

        <input
            id="armorInput"
            type="color"
            value="#d92b35">

    </div>

    <div class="field">

        <label>Helmet Color</label>

        <input
            id="helmetInput"
            type="color"
            value="#ffffff">

    </div>

    <button
        class="goldButton"
        style="width:100%"
        onclick="startGame()">

        ENTER THE BATTLE

    </button>

    <br><br>

    <button
        class="redButton"
        style="width:100%"
        onclick="showSaves()">

        BACK

    </button>

</section>


<!-- =====================================================
     GAME
===================================================== -->

<section id="game" class="hidden">

    <!-- HUD -->

    <div class="topHud panel">

        <div>

            <div
                class="playerName"
                id="playerName">
            </div>

            <div class="healthBox">

                <div class="healthText">

                    <span>
                        SPIRIT HEALTH
                    </span>

                    <span id="playerHpText">
                        100 / 100
                    </span>

                </div>

                <div class="healthBar">

                    <div
                        id="playerHealth"
                        class="playerHealth">
                    </div>

                </div>

            </div>

        </div>


        <div
            id="levelBadge"
            class="levelBadge">

            LEVEL 1

        </div>


        <div>

            <div
                class="enemyName"
                id="enemyName">
            </div>

            <div class="healthBox">

                <div class="healthText">

                    <span>
                        ENEMY
                    </span>

                    <span id="enemyHpText">
                        100 / 100
                    </span>

                </div>

                <div class="healthBar">

                    <div
                        id="enemyHealth"
                        class="enemyHealth">
                    </div>

                </div>

            </div>

        </div>

    </div>


    <!-- ARENA -->

    <div
        id="arena"
        class="arena">

        <div class="floor"></div>


        <!-- PLAYER -->

        <div
            id="player"
            class="fighter">

            <div class="head">
                <div class="visor"></div>
            </div>

            <div class="body">
                <div class="core"></div>
            </div>

            <div class="arm leftArm"></div>
            <div class="arm rightArm"></div>

            <div class="leg leftLeg"></div>
            <div class="leg rightLeg"></div>

        </div>


        <!-- ENEMY -->

        <div
            id="enemy"
            class="fighter enemy">

            <div class="head">
                <div class="visor"></div>
            </div>

            <div class="body">
                <div class="core"></div>
            </div>

            <div class="arm leftArm"></div>
            <div class="arm rightArm"></div>

            <div class="leg leftLeg"></div>
            <div class="leg rightLeg"></div>

        </div>

    </div>


    <!-- COMBAT -->

    <div
        class="panel"
        style="margin-top:10px">

        <div
            style="
            display:flex;
            justify-content:space-between;
            ">

            <b>
                TURN
                <span id="turnCount">0</span>
            </b>

            <b>
                SPIRIT
                <span id="spiritCount">0</span>
            </b>

        </div>


        <div class="controls">

            <button
                id="strikeButton"
                class="attackButton"
                onclick="attack('strike')">

                ⚡
                <br>
                SPIRIT STRIKE
                <br>
                <small>
                    LIGHT SHOT
                </small>

            </button>


            <button
                id="shieldButton"
                class="attackButton"
                onclick="attack('shield')">

                🛡️
                <br>
                SHIELD OF FATE
                <br>
                <small>
                    BLOCK NEXT HIT
                </small>

            </button>


            <button
                id="truthButton"
                class="attackButton"
                onclick="attack('truth')">

                ✨
                <br>
                WORD OF TRUTH
                <br>
                <small>
                    LIGHT BEAM
                </small>

            </button>


            <button
                id="specialButton"
                class="attackButton special"
                onclick="attack('special')"
                disabled>

                ☀️
                <br>
                POWER ATTACK
                <br>
                <small>
                    SURVIVE 3 TURNS
                </small>

            </button>

        </div>


        <div
            id="combatLog"
            class="log">

            The battle begins...

        </div>


        <div
            id="verseBox"
            class="verse">
        </div>

    </div>

</section>

</div>


<!-- =====================================================
     VICTORY
===================================================== -->

<div
    id="victoryOverlay"
    class="overlay hidden">

    <div class="overlayBox">

        <h1 class="title">
            VICTORY
        </h1>

        <p id="victoryText"></p>

        <button
            class="goldButton"
            onclick="showSaves()">

            RETURN TO SAVES

        </button>

    </div>

</div>


<script>

/* =========================================================
   SAVE DATA
========================================================= */

const SAVE_KEY =
    "spiritualPowerShadowboundSaves";

let saves =
    JSON.parse(
        localStorage.getItem(SAVE_KEY)
        || "[null,null,null]"
    );

let currentSave=-1;

let player=null;
let enemy=null;

let busy=false;

let shieldActive=false;


/* =========================================================
   LEVEL DATA
========================================================= */

const levels={

    1:{
        name:"Shadow Demons",
        hp:100,
        verse:"Ephesians 6:11",
        text:
        "Put on the whole armour of God, that ye may be able to stand against the wiles of the devil."
    },

    2:{
        name:"Dark Angel",
        hp:200,
        verse:"Psalm 18:2",
        text:
        "The LORD is my rock, and my fortress, and my deliverer; my God, my strength, in whom I will trust."
    },

    3:{
        name:"Shadow Colossus",
        hp:380,
        verse:"1 John 4:4",
        text:
        "Greater is he that is in you, than he that is in the world."
    }

};


/* =========================================================
   SAVE
========================================================= */

function saveAll(){

    localStorage.setItem(
        SAVE_KEY,
        JSON.stringify(saves)
    );
}


function autoSave(){

    if(
        currentSave>=0 &&
        player
    ){

        saves[currentSave]=
            JSON.parse(JSON.stringify(player));

        saveAll();
    }
}


/* =========================================================
   SAVE SCREEN
========================================================= */

function showSaves(){

    document
        .getElementById("saveScreen")
        .classList.remove("hidden");

    document
        .getElementById("customScreen")
        .classList.add("hidden");

    document
        .getElementById("game")
        .classList.add("hidden");

    document
        .getElementById("victoryOverlay")
        .classList.add("hidden");

    renderSaves();
}


function renderSaves(){

    const grid=
        document.getElementById("saveGrid");

    grid.innerHTML="";

    saves.forEach((save,index)=>{

        const card=
            document.createElement("div");

        card.className="saveCard";

        if(save){

            card.innerHTML=`

                <div>

                    <h2>
                        SAVE ${index+1}
                    </h2>

                    <b>
                        ${safe(save.name)}
                    </b>

                    <p>
                        Level ${save.level}
                    </p>

                    <p>
                        Spiritual Power:
                        ${save.power}
                    </p>

                </div>

                <button
                    class="goldButton"
                    onclick="loadSave(${index})">

                    CONTINUE

                </button>

                <button
                    class="redButton"
                    onclick="deleteSave(${index})">

                    DELETE SAVE

                </button>

            `;

        }else{

            card.innerHTML=`

                <div>

                    <h2>
                        SAVE ${index+1}
                    </h2>

                    <p style="color:#7d89a5">
                        Empty slot
                    </p>

                </div>

                <button
                    class="goldButton"
                    onclick="newSave(${index})">

                    NEW GAME

                </button>

            `;
        }

        grid.appendChild(card);
    });
}


function newSave(index){

    currentSave=index;

    document
        .getElementById("saveScreen")
        .classList.add("hidden");

    document
        .getElementById("customScreen")
        .classList.remove("hidden");
}


function deleteSave(index){

    if(
        confirm(
            "Delete Save "+(index+1)+"?"
        )
    ){

        saves[index]=null;

        saveAll();

        renderSaves();
    }
}


/* =========================================================
   NEW PLAYER
========================================================= */

function startGame(){

    player={

        name:
            document
            .getElementById("nameInput")
            .value
            .trim()
            || "Warrior",

        gender:
            document
            .getElementById("genderInput")
            .value,

        armor:
            document
            .getElementById("armorInput")
            .value,

        helmet:
            document
            .getElementById("helmetInput")
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

    document
        .getElementById("customScreen")
        .classList.add("hidden");

    document
        .getElementById("game")
        .classList.remove("hidden");

    loadLevel();
}


/* =========================================================
   LOAD SAVE
========================================================= */

function loadSave(index){

    currentSave=index;

    player=
        JSON.parse(
            JSON.stringify(saves[index])
        );

    shieldActive=false;

    document
        .getElementById("saveScreen")
        .classList.add("hidden");

    document
        .getElementById("game")
        .classList.remove("hidden");

    loadLevel();
}


/* =========================================================
   LEVEL
========================================================= */

function loadLevel(){

    const data=levels[player.level];

    enemy={

        name:data.name,

        maxHp:data.hp,

        hp:data.hp

    };

    shieldActive=false;

    document
        .documentElement
        .style
        .setProperty(
            "--armor",
            player.armor
        );

    document
        .querySelector(
            "#player .head"
        )
        .style
        .background=
        `
        linear-gradient(
            145deg,
            ${player.helmet},
            #7f8ba6
        )
        `;

    document
        .getElementById("verseBox")
        .innerHTML=
        `
        <strong>
            ${data.verse}
        </strong>
        <br>
        ${data.text}
        `;

    log(
        "A "+data.name+
        " approaches..."
    );

    updateUI();
}


/* =========================================================
   UI
========================================================= */

function updateUI(){

    if(!player || !enemy)return;

    document
        .getElementById("playerName")
        .textContent=
        player.name;

    document
        .getElementById("enemyName")
        .textContent=
        enemy.name;

    document
        .getElementById("levelBadge")
        .textContent=
        "LEVEL "+player.level;

    document
        .getElementById("playerHpText")
        .textContent=
        Math.max(0,player.hp)
        +" / 100";

    document
        .getElementById("enemyHpText")
        .textContent=
        Math.max(0,enemy.hp)
        +" / "
        +enemy.maxHp;

    document
        .getElementById("playerHealth")
        .style.width=
        Math.max(0,player.hp)
        +"%";

    document
        .getElementById("enemyHealth")
        .style.width=
        Math.max(
            0,
            enemy.hp/enemy.maxHp*100
        )
        +"%";

    document
        .getElementById("turnCount")
        .textContent=
        player.turns;

    document
        .getElementById("spiritCount")
        .textContent=
        player.spirit;

    const special=
        document.getElementById(
            "specialButton"
        );

    special.disabled=
        !player.specialUnlocked
        || busy;

    special.innerHTML=
        player.specialUnlocked
        ?
        `
        ☀️
        <br>
        LIGHT BURST
        <br>
        <small>READY</small>
        `
        :
        `
        ☀️
        <br>
        POWER ATTACK
        <br>
        <small>
        SURVIVE 3 TURNS
        </small>
        `;

    document
        .getElementById("strikeButton")
        .disabled=busy;

    document
        .getElementById("shieldButton")
        .disabled=busy;

    document
        .getElementById("truthButton")
        .disabled=busy;
}


/* =========================================================
   ATTACK ROUTER
========================================================= */

function attack(type){

    if(
        busy ||
        !player ||
        player.hp<=0
    )return;

    if(
        type==="special"
        &&
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
   1 — SPIRIT STRIKE
========================================================= */

function spiritStrike(){

    const playerSprite=
        document.getElementById("player");

    const enemySprite=
        document.getElementById("enemy");

    playerSprite.classList.add("dash");

    log(
        "SPIRIT STRIKE — LIGHT SHOT!"
    );

    const shot=
        document.createElement("div");

    shot.className="lightShot";

    arena().appendChild(shot);

    setTimeout(()=>{

        enemySprite
            .classList.add("enemyHit");

        impactAtEnemy();

        enemy.hp-=20+player.level*5;

        player.spirit+=12;

        shot.remove();

    },520);

    setTimeout(()=>{

        playerSprite
            .classList.remove("dash");

        enemySprite
            .classList.remove("enemyHit");

        finishPlayerAttack();

    },850);
}


/* =========================================================
   2 — SHIELD OF FATE
========================================================= */

function shieldOfFate(){

    const playerSprite=
        document.getElementById("player");

    playerSprite.classList.add("defending");

    shieldActive=true;

    const shield=
        document.createElement("div");

    shield.id="activeShield";

    shield.className="shield";

    arena().appendChild(shield);

    player.spirit+=20;

    log(
        "SHIELD OF FATE — YOUR NEXT ATTACK IS BLOCKED!"
    );

    updateUI();

    setTimeout(()=>{

        busy=false;

        updateUI();

        /* The shield does NOT cause an enemy turn
           until the enemy attacks. */

        setTimeout(enemyAttack,700);

    },650);
}


/* =========================================================
   3 — WORD OF TRUTH
========================================================= */

function wordOfTruth(){

    const enemySprite=
        document.getElementById("enemy");

    log(
        "WORD OF TRUTH — HEAVEN'S LIGHT DESCENDS!"
    );

    const beam=
        document.createElement("div");

    beam.className="truthBeam";

    arena().appendChild(beam);

    setTimeout(()=>{

        enemySprite
            .classList.add("enemyHit");

        impactAtEnemy();

        enemy.hp-=32+player.level*6;

        player.spirit+=24;

    },430);

    setTimeout(()=>{

        beam.remove();

        enemySprite
            .classList.remove("enemyHit");

        finishPlayerAttack();

    },900);
}


/* =========================================================
   4 — LIGHT BURST
========================================================= */

function lightBurst(){

    const playerSprite=
        document.getElementById("player");

    const enemySprite=
        document.getElementById("enemy");

    playerSprite.classList.add("dash");

    log(
        "LIGHT BURST — THE WARRIOR'S CORE UNLEASHES!"
    );

    const beam=
        document.createElement("div");

    beam.className="superBeam";

    arena().appendChild(beam);

    setTimeout(()=>{

        enemySprite
            .classList.add("enemyHit");

        impactAtEnemy();

        enemy.hp-=100+player.level*25;

        player.spirit=0;

        player.specialUnlocked=false;

    },500);

    setTimeout(()=>{

        beam.remove();

        playerSprite
            .classList.remove("dash");

        enemySprite
            .classList.remove("enemyHit");

        finishPlayerAttack();

    },1100);
}


/* =========================================================
   FINISH PLAYER ATTACK
========================================================= */

function finishPlayerAttack(){

    updateUI();

    if(enemy.hp<=0){

        enemyDefeated();

        return;
    }

    setTimeout(
        enemyAttack,
        450
    );
}


/* =========================================================
   ENEMY ATTACK
========================================================= */

function enemyAttack(){

    if(enemy.hp<=0)return;

    const enemySprite=
        document.getElementById("enemy");

    const playerSprite=
        document.getElementById("player");

    /* SHIELD BLOCK */

    if(shieldActive){

        const shield=
            document.getElementById(
                "activeShield"
            );

        log(
            "SHIELD OF FATE BLOCKED THE ATTACK!"
        );

        if(shield){

            shield.classList.add(
                "shieldBreak"
            );

            setTimeout(
                ()=>shield.remove(),
                450
            );
        }

        shieldActive=false;

        player.turns++;

        if(player.turns>=3){

            player.specialUnlocked=true;

        }

        updateUI();

        autoSave();

        setTimeout(()=>{

            busy=false;
            updateUI();

        },550);

        return;
    }


    /* NORMAL ENEMY ATTACK */

    enemySprite.classList.add(
        "enemyDash"
    );

    log(
        enemy.name+
        " launches a shadow attack!"
    );

    setTimeout(()=>{

        playerSprite
            .classList.add("playerHit");

        const damage=
            10+
            player.level*5+
            Math.floor(
                Math.random()*7
            );

        player.hp-=damage;

        createShadowImpact();

    },500);

    setTimeout(()=>{

        enemySprite
            .classList.remove("enemyDash");

        playerSprite
            .classList.remove("playerHit");

        player.turns++;

        if(player.turns>=3){

            player.specialUnlocked=true;

            log(
                "YOUR POWER ATTACK IS READY!"
            );

        }

        if(player.hp<=0){

            player.hp=0;

            updateUI();

            playerDefeated();

            return;
        }

        updateUI();

        autoSave();

        busy=false;

    },850);
}


/* =========================================================
   PLAYER DEFEATED
========================================================= */

function playerDefeated(){

    log(
        "Your warrior is out of strength..."
    );

    setTimeout(()=>{

        player.hp=100;

        player.spirit=0;

        player.turns=0;

        player.specialUnlocked=false;

        shieldActive=false;

        enemy.hp=enemy.maxHp;

        log(
            "The light returns. Rise and fight again!"
        );

        busy=false;

        updateUI();

    },900);
}


/* =========================================================
   ENEMY DEFEATED
========================================================= */

function enemyDefeated(){

    busy=false;

    player.power+=5;

    log(
        enemy.name+
        " has been defeated!"
    );

    updateUI();

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

            log(
                "LEVEL UP! Spiritual power increased."
            );

            autoSave();

            busy=false;

            updateUI();

        },1000);

    }else{

        player.power+=50;

        autoSave();

        document
            .getElementById("victoryText")
            .textContent=
            "The Shadow Colossus has fallen. You completed all three levels.";

        document
            .getElementById("victoryOverlay")
            .classList.remove("hidden");
    }
}


/* =========================================================
   EFFECT HELPERS
========================================================= */

function arena(){

    return document.getElementById(
        "arena"
    );
}


function impactAtEnemy(){

    const effect=
        document.createElement("div");

    effect.className="impact";

    effect.style.left="72%";
    effect.style.top="43%";

    arena().appendChild(effect);

    setTimeout(
        ()=>effect.remove(),
        500
    );
}


function createShadowImpact(){

    const effect=
        document.createElement("div");

    effect.className="impact";

    effect.style.left="20%";
    effect.style.top="43%";

    effect.style.borderColor=
        "#a66cff";

    effect.style.boxShadow=
        "0 0 20px #a66cff,0 0 50px #5c31ff";

    arena().appendChild(effect);

    setTimeout(
        ()=>effect.remove(),
        500
    );
}


/* =========================================================
   LOG
========================================================= */

function log(text){

    document
        .getElementById("combatLog")
        .textContent=text;
}


/* =========================================================
   SAFE TEXT
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
   AUTOSAVE LOOP
========================================================= */

setInterval(()=>{

    if(
        player &&
        currentSave>=0 &&
        !document
            .getElementById("game")
            .classList
            .contains("hidden")
    ){

        autoSave();

    }

},5000);


/* =========================================================
   INITIAL SCREEN
========================================================= */

showSaves();

</script>

</body>
</html>
