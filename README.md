<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
<title>Spiritual Power: Shadowbound</title>

<style>
*{
  box-sizing:border-box;
  -webkit-tap-highlight-color:transparent;
}

html,body{
  margin:0;
  min-height:100%;
  background:#02030a;
  color:#fff;
  font-family:Arial,Helvetica,sans-serif;
}

body{
  overflow-x:hidden;
}

button{
  font:inherit;
  touch-action:manipulation;
}

.hidden{
  display:none!important;
}

/* =========================================================
   MENU
========================================================= */

.screen{
  min-height:100vh;
  display:flex;
  align-items:center;
  justify-content:center;
  padding:20px;
}

.menu,
.customize{
  width:min(650px,100%);
  padding:30px;
  border-radius:25px;
  border:1px solid #526eff;
  background:
    linear-gradient(145deg,#111a3b,#050814 70%);
  box-shadow:
    0 0 35px #315cff55,
    inset 0 0 35px #16265c55;
  text-align:center;
}

.title{
  margin:0;
  font-size:clamp(38px,9vw,72px);
  letter-spacing:4px;
  background:linear-gradient(90deg,#fff,#73aaff,#fff);
  -webkit-background-clip:text;
  color:transparent;
  text-shadow:0 0 25px #4b7dff;
}

.subtitle{
  color:#aabaff;
  margin:10px 0 28px;
}

.saveGrid{
  display:grid;
  gap:12px;
}

.save{
  padding:15px;
  border-radius:15px;
  background:#0b1229;
  border:1px solid #344a89;
  text-align:left;
}

.saveName{
  font-size:18px;
  font-weight:bold;
}

.saveInfo{
  margin-top:4px;
  color:#91a1cb;
  font-size:13px;
}

button{
  border:0;
  border-radius:12px;
  padding:12px 18px;
  background:linear-gradient(135deg,#416aff,#2142c8);
  color:white;
  font-weight:bold;
  box-shadow:0 5px 15px #0008;
}

button:active{
  transform:scale(.96);
}

.delete{
  background:#8d2436;
}

.customize{
  text-align:left;
}

.customize h2{
  text-align:center;
  font-size:30px;
}

.customize label{
  display:block;
  margin-top:15px;
  color:#a9b9e8;
}

.customize input,
.customize select{
  display:block;
  width:100%;
  margin-top:6px;
  padding:12px;
  border-radius:10px;
  border:1px solid #3f548c;
  background:#050916;
  color:white;
}

/* =========================================================
   GAME
========================================================= */

#game{
  min-height:100vh;
  padding:8px;
}

.topBar{
  width:min(1200px,100%);
  margin:auto;
  display:flex;
  justify-content:space-between;
  align-items:center;
  padding:8px 10px;
}

.levelText{
  font-size:20px;
  font-weight:bold;
}

.power{
  color:#ffe45c;
  text-shadow:0 0 10px #ffcf38;
}

.arena{
  position:relative;
  width:min(1200px,100%);
  height:min(690px,73vh);
  min-height:470px;
  margin:auto;
  overflow:hidden;
  border-radius:24px;
  border:1px solid #354a86;
  background:
    radial-gradient(circle at 50% 35%,#202d70 0,#0b1230 32%,#03050d 75%);
  box-shadow:
    0 0 60px #142b77,
    inset 0 0 80px #000;
}

/* Stars */

.arena:before{
  content:"";
  position:absolute;
  inset:0;
  opacity:.6;
  background-image:
    radial-gradient(circle,#fff 1px,transparent 1.5px),
    radial-gradient(circle,#7695ff 1px,transparent 1.5px),
    radial-gradient(circle,#fff 1px,transparent 1.5px);
  background-size:70px 70px,110px 110px,170px 170px;
  background-position:0 0,30px 20px,60px 80px;
  pointer-events:none;
}

/* Horizon */

.horizon{
  position:absolute;
  left:0;
  right:0;
  bottom:30%;
  height:2px;
  background:#5277ff;
  box-shadow:0 0 20px #5277ff;
  opacity:.6;
}

/* Floor */

.floor{
  position:absolute;
  left:-10%;
  right:-10%;
  bottom:-15%;
  height:50%;
  transform:perspective(500px) rotateX(60deg);
  transform-origin:bottom;
  background:
    linear-gradient(#304a93 1px,transparent 1px),
    linear-gradient(90deg,#304a93 1px,transparent 1px);
  background-size:65px 45px;
  opacity:.45;
  pointer-events:none;
}

/* =========================================================
   HEALTH BARS
========================================================= */

.health{
  position:absolute;
  top:18px;
  width:34%;
  min-width:180px;
  z-index:80;
}

.playerHealthArea{
  left:3%;
}

.enemyHealthArea{
  right:3%;
  text-align:right;
}

.name{
  font-weight:bold;
  font-size:17px;
  margin-bottom:5px;
  text-shadow:0 2px 6px #000;
}

.bar{
  height:18px;
  border:2px solid #647092;
  background:#080b15;
  border-radius:20px;
  overflow:hidden;
}

.fill{
  height:100%;
  transition:width .3s ease;
}

.gold{
  background:linear-gradient(90deg,#a96d00,#ffd83d,#fff5a0,#d99500);
  box-shadow:0 0 18px #ffd83d;
}

.red{
  background:linear-gradient(90deg,#690014,#e51f3e,#ff5369);
  box-shadow:0 0 18px #ff263e;
}

.hpText{
  font-size:12px;
  color:#aab6d7;
}

/* =========================================================
   STATUS
========================================================= */

.status{
  position:absolute;
  left:50%;
  top:22px;
  transform:translateX(-50%);
  z-index:90;
  padding:7px 15px;
  border-radius:20px;
  background:#03050ccc;
  border:1px solid #5269a3;
  color:#d8e1ff;
  white-space:nowrap;
}

/* =========================================================
   PLAYER
========================================================= */

.fighter{
  position:absolute;
  bottom:105px;
  width:220px;
  height:320px;
  z-index:30;
  pointer-events:none;
}

#player{
  left:7%;
}

.playerGlow{
  position:absolute;
  width:190px;
  height:190px;
  left:15px;
  top:75px;
  border-radius:50%;
  background:#4f8cff22;
  filter:blur(25px);
  animation:breath 2.5s infinite;
}

@keyframes breath{
  50%{transform:scale(1.18);opacity:.55}
}

.playerHead{
  position:absolute;
  width:72px;
  height:78px;
  left:74px;
  top:0;
  border-radius:46% 46% 42% 42%;
  background:linear-gradient(145deg,#ffd0ad,#ae674d);
  border:3px solid #623b37;
  z-index:5;
}

.hair{
  position:absolute;
  width:76px;
  height:34px;
  left:-5px;
  top:-4px;
  border-radius:50% 50% 35% 35%;
  background:#151822;
}

.eye{
  position:absolute;
  top:34px;
  width:7px;
  height:7px;
  border-radius:50%;
  background:#111;
}

.eye.a{left:19px}
.eye.b{right:19px}

.mouth{
  position:absolute;
  left:25px;
  top:57px;
  width:20px;
  height:5px;
  border-bottom:2px solid #522b2b;
}

.neck{
  position:absolute;
  left:92px;
  top:69px;
  width:35px;
  height:25px;
  background:#a86650;
}

.chest{
  position:absolute;
  left:48px;
  top:82px;
  width:125px;
  height:130px;
  border-radius:35px 35px 20px 20px;
  background:
    linear-gradient(135deg,#6c88ff,#283aa7 50%,#11184d);
  border:3px solid #b1c0ff;
  box-shadow:
    inset 0 0 25px #9db2ff66,
    0 0 18px #426dff55;
}

.chest:after{
  content:"";
  position:absolute;
  left:15px;
  right:15px;
  top:14px;
  height:3px;
  background:#b8c7ff;
  box-shadow:0 80px #111a55;
  opacity:.6;
}

.core{
  position:absolute;
  left:47px;
  top:40px;
  width:31px;
  height:31px;
  border-radius:50%;
  background:#fff;
  box-shadow:
    0 0 12px white,
    0 0 25px #6bb5ff,
    0 0 45px #377eff;
  animation:corePulse 1.4s infinite;
}

@keyframes corePulse{
  50%{transform:scale(1.12)}
}

.shoulder{
  position:absolute;
  top:86px;
  width:50px;
  height:50px;
  border-radius:50%;
  background:linear-gradient(145deg,#8fa7ff,#28399c);
  border:3px solid #b0c1ff;
}

.shoulder.a{left:20px}
.shoulder.b{right:20px}

.arm{
  position:absolute;
  top:124px;
  width:32px;
  height:95px;
  border-radius:18px;
  background:linear-gradient(#4c65cc,#18245e);
  border:3px solid #8096ff;
}

.arm.a{
  left:20px;
  transform:rotate(9deg);
}

.arm.b{
  right:20px;
  transform:rotate(-9deg);
}

.leg{
  position:absolute;
  top:205px;
  width:43px;
  height:91px;
  border-radius:13px;
  background:linear-gradient(#3349a4,#121936);
  border:3px solid #7086ef;
}

.leg.a{left:70px}
.leg.b{right:70px}

.boot{
  position:absolute;
  top:287px;
  width:56px;
  height:23px;
  border-radius:14px;
  background:#080c1c;
  border:2px solid #7389ef;
}

.boot.a{left:59px}
.boot.b{right:59px}

/* =========================================================
   BOSS BASE
========================================================= */

.boss{
  position:absolute;
  inset:0;
}

/* =========================================================
   LEVEL 1 — SHADOW DEMON
========================================================= */

.boss.level1{
  transform:scale(1);
}

.demonHead{
  position:absolute;
  left:66px;
  top:22px;
  width:100px;
  height:90px;
  border-radius:48% 48% 38% 38%;
  background:linear-gradient(145deg,#442456,#08060d);
  border:3px solid #9a4db8;
  box-shadow:0 0 25px #7b35a655;
}

.demonHorn{
  position:absolute;
  top:-47px;
  width:34px;
  height:58px;
  background:linear-gradient(145deg,#7e4b9c,#160c20);
  border:3px solid #a95bc7;
  clip-path:polygon(50% 0,100% 100%,0 100%);
}

.demonHorn.a{
  left:7px;
  transform:rotate(-18deg);
}

.demonHorn.b{
  right:7px;
  transform:rotate(18deg);
}

.demonEye{
  position:absolute;
  top:42px;
  width:24px;
  height:11px;
  border-radius:50%;
  background:#ff203f;
  box-shadow:0 0 18px #ff1739;
}

.demonEye.a{left:18px}
.demonEye.b{right:18px}

.demonMouth{
  position:absolute;
  left:31px;
  top:66px;
  width:39px;
  height:13px;
  border-bottom:4px solid #ff2745;
}

.demonBody{
  position:absolute;
  left:47px;
  top:110px;
  width:138px;
  height:125px;
  border-radius:40px 40px 18px 18px;
  background:linear-gradient(145deg,#49255d,#100817);
  border:3px solid #793c91;
  box-shadow:inset 0 0 25px #a14bc044;
}

.demonCore{
  position:absolute;
  left:50px;
  top:38px;
  width:38px;
  height:38px;
  border-radius:50%;
  background:#ff183d;
  box-shadow:0 0 20px #ff183d,0 0 45px #a0002d;
}

.demonArm{
  position:absolute;
  top:132px;
  width:45px;
  height:105px;
  background:#21112d;
  border:3px solid #743b8d;
  border-radius:22px;
}

.demonArm.a{
  left:17px;
  transform:rotate(13deg);
}

.demonArm.b{
  right:17px;
  transform:rotate(-13deg);
}

.demonLeg{
  position:absolute;
  top:225px;
  width:48px;
  height:82px;
  border-radius:15px;
  background:#140b1c;
  border:3px solid #633173;
}

.demonLeg.a{left:58px}
.demonLeg.b{right:58px}

/* =========================================================
   LEVEL 2 — DARK ANGEL
========================================================= */

.boss.level2{
  transform:scale(1.02);
}

.angelGlow{
  position:absolute;
  left:15px;
  top:30px;
  width:190px;
  height:230px;
  border-radius:50%;
  background:#7b7cff18;
  filter:blur(28px);
}

.angelWing{
  position:absolute;
  top:50px;
  width:120px;
  height:190px;
  background:
    linear-gradient(145deg,#dce4ff,#6978a9 45%,#161b31);
  border:3px solid #aebeff;
  clip-path:polygon(
    50% 0,
    75% 16%,
    100% 38%,
    76% 40%,
    100% 60%,
    65% 58%,
    82% 82%,
    48% 72%,
    50% 100%,
    30% 70%,
    0 82%,
    20% 55%,
    0 58%,
    25% 38%,
    0 35%,
    32% 18%
  );
  box-shadow:0 0 25px #8da4ff55;
}

.angelWing.a{
  left:-8px;
  transform:rotate(-18deg);
}

.angelWing.b{
  right:-8px;
  transform:scaleX(-1) rotate(-18deg);
}

.angelHalo{
  position:absolute;
  left:58px;
  top:3px;
  width:104px;
  height:104px;
  border:7px solid #ffe86b;
  border-radius:50%;
  box-shadow:0 0 20px #ffe86b,0 0 50px #ffcc3a;
}

.angelHead{
  position:absolute;
  left:73px;
  top:30px;
  width:76px;
  height:80px;
  border-radius:50%;
  background:linear-gradient(145deg,#d7d8df,#555b72);
  border:3px solid #bbc7eb;
  z-index:4;
}

.angelVisor{
  position:absolute;
  left:9px;
  top:29px;
  width:52px;
  height:18px;
  border-radius:5px;
  background:#101525;
  border:2px solid #7188ff;
  box-shadow:0 0 14px #5e7cff;
}

.angelBody{
  position:absolute;
  left:48px;
  top:102px;
  width:124px;
  height:135px;
  border-radius:30px;
  background:linear-gradient(145deg,#b7c4df,#343d58 45%,#111625);
  border:3px solid #cbd7ff;
  box-shadow:inset 0 0 30px #d5e0ff44;
}

.angelCore{
  position:absolute;
  left:44px;
  top:42px;
  width:36px;
  height:36px;
  border-radius:50%;
  background:#fff;
  box-shadow:0 0 20px #fff,0 0 55px #aebaff;
}

.angelArm{
  position:absolute;
  top:130px;
  width:35px;
  height:105px;
  border-radius:20px;
  background:#3d465e;
  border:3px solid #8998bd;
}

.angelArm.a{
  left:25px;
  transform:rotate(8deg);
}

.angelArm.b{
  right:25px;
  transform:rotate(-8deg);
}

.angelLeg{
  position:absolute;
  top:235px;
  width:43px;
  height:80px;
  background:#202638;
  border:3px solid #68789d;
  border-radius:13px;
}

.angelLeg.a{left:66px}
.angelLeg.b{right:66px}

/* =========================================================
   LEVEL 3 — SHADOW COLOSSUS
========================================================= */

.boss.level3{
  transform:scale(1.35);
  transform-origin:bottom center;
}

.colossusWing{
  position:absolute;
  top:15px;
  width:150px;
  height:220px;
  background:
    linear-gradient(145deg,#24263f,#090a13);
  border:4px solid #525a85;
  clip-path:polygon(
    50% 0,
    70% 15%,
    100% 10%,
    78% 34%,
    100% 31%,
    70% 52%,
    90% 65%,
    57% 62%,
    68% 90%,
    45% 70%,
    35% 100%,
    30% 65%,
    0 76%,
    25% 51%,
    0 48%,
    27% 30%,
    3% 25%,
    32% 14%
  );
  box-shadow:0 0 30px #252b55;
}

.colossusWing.a{
  left:-28px;
  transform:rotate(-12deg);
}

.colossusWing.b{
  right:-28px;
  transform:scaleX(-1) rotate(-12deg);
}

.colossusHead{
  position:absolute;
  left:61px;
  top:35px;
  width:120px;
  height:105px;
  border-radius:45% 45% 35% 35%;
  background:linear-gradient(145deg,#262a44,#06070d);
  border:4px solid #59618d;
  z-index:5;
}

.colossusHorn{
  position:absolute;
  top:-60px;
  width:42px;
  height:75px;
  background:#11131f;
  border:4px solid #565e87;
  clip-path:polygon(50% 0,100% 100%,0 100%);
}

.colossusHorn.a{
  left:5px;
  transform:rotate(-16deg);
}

.colossusHorn.b{
  right:5px;
  transform:rotate(16deg);
}

.colossusEye{
  position:absolute;
  top:50px;
  width:32px;
  height:14px;
  background:#9f102b;
  box-shadow:0 0 22px #ff143c;
  border-radius:50%;
}

.colossusEye.a{left:20px}
.colossusEye.b{right:20px}

.colossusBody{
  position:absolute;
  left:35px;
  top:130px;
  width:172px;
  height:175px;
  border-radius:48px 48px 25px 25px;
  background:
    linear-gradient(145deg,#343852,#0b0d17 60%);
  border:4px solid #555d87;
  box-shadow:
    inset 0 0 35px #6672a544,
    0 0 30px #181d3e;
}

.colossusPlate{
  position:absolute;
  left:24px;
  top:20px;
  width:116px;
  height:80px;
  border:3px solid #707ba9;
  border-radius:25px;
  background:#151827;
}

.colossusCore{
  position:absolute;
  left:58px;
  top:35px;
  width:50px;
  height:50px;
  border-radius:50%;
  background:#ff183f;
  box-shadow:
    0 0 20px #ff183f,
    0 0 55px #ff002e,
    0 0 90px #6b0020;
}

.colossusArm{
  position:absolute;
  top:160px;
  width:58px;
  height:145px;
  border-radius:30px;
  background:linear-gradient(#24283e,#090b14);
  border:4px solid #555e89;
}

.colossusArm.a{
  left:-2px;
  transform:rotate(8deg);
}

.colossusArm.b{
  right:-2px;
  transform:rotate(-8deg);
}

.colossusLeg{
  position:absolute;
  top:292px;
  width:60px;
  height:100px;
  background:#10121d;
  border:4px solid #4c557d;
  border-radius:16px;
}

.colossusLeg.a{left:49px}
.colossusLeg.b{right:49px}

/* =========================================================
   EFFECTS
========================================================= */

.effect{
  position:absolute;
  pointer-events:none!important;
  z-index:100;
}

.lightOrb{
  width:34px;
  height:34px;
  border-radius:50%;
  background:#fff;
  box-shadow:
    0 0 15px white,
    0 0 35px #66b8ff,
    0 0 70px #3377ff;
}

.lightBeam{
  left:5%;
  right:5%;
  top:43%;
  height:38px;
  border-radius:50%;
  background:#fff;
  box-shadow:
    0 0 20px #fff,
    0 0 50px #5eb5ff,
    0 0 90px #336dff;
  animation:beam .55s ease-out;
}

.bigBeam{
  left:-5%;
  right:-5%;
  top:35%;
  height:100px;
  border-radius:50%;
  background:#fff;
  box-shadow:
    0 0 30px #fff,
    0 0 80px #6abaff,
    0 0 150px #3375ff;
  animation:bigBeam .8s ease-out;
}

@keyframes beam{
  from{transform:scaleX(.05);opacity:0}
  to{transform:scaleX(1);opacity:1}
}

@keyframes bigBeam{
  from{transform:scaleX(.05);opacity:0}
  to{transform:scaleX(1);opacity:1}
}

.shield{
  width:290px;
  height:290px;
  left:0;
  top:25%;
  border:6px solid #65c7ff;
  border-radius:50%;
  box-shadow:
    0 0 25px #65c7ff,
    inset 0 0 50px #258cff55;
  animation:shield .8s ease;
}

@keyframes shield{
  0%{transform:scale(.45);opacity:0}
  50%{transform:scale(1);opacity:1}
  100%{transform:scale(1.12);opacity:.3}
}

.hit{
  animation:hit .42s ease;
}

@keyframes hit{
  20%{transform:translateX(15px)}
  40%{transform:translateX(-17px)}
  60%{transform:translateX(12px)}
  80%{transform:translateX(-6px)}
}

.playerDash{
  animation:dash .6s ease;
}

@keyframes dash{
  50%{transform:translateX(135px) scale(1.06)}
}

.enemyDash{
  animation:enemyDash .6s ease;
}

@keyframes enemyDash{
  50%{transform:translateX(-125px) scale(1.06)}
}

/* =========================================================
   CONTROLS
========================================================= */

.controls{
  position:relative;
  z-index:500;
  width:min(1200px,100%);
  margin:12px auto;
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:10px;
}

.controls button{
  min-height:64px;
  border:2px solid #4668e9;
  background:
    linear-gradient(145deg,#1b2d68,#080e27);
  box-shadow:
    0 7px 18px #0009,
    inset 0 0 15px #5376ff22;
}

.controls button:disabled{
  opacity:.42;
}

.controls .special{
  border-color:#ffd84a;
  color:#ffe76d;
}

/* =========================================================
   LOG
========================================================= */

.log{
  position:relative;
  z-index:500;
  width:min(1200px,100%);
  min-height:55px;
  max-height:100px;
  overflow-y:auto;
  margin:auto;
  padding:10px 14px;
  border-radius:12px;
  border:1px solid #2e4071;
  background:#050914;
  color:#b9c7ed;
}

/* =========================================================
   OVERLAY
========================================================= */

.overlay{
  position:fixed;
  inset:0;
  z-index:1000;
  display:flex;
  align-items:center;
  justify-content:center;
  padding:20px;
  background:#000b;
}

.overlayBox{
  width:min(550px,100%);
  padding:30px;
  text-align:center;
  border-radius:24px;
  border:2px solid #5876ff;
  background:linear-gradient(145deg,#111b3c,#050815);
  box-shadow:0 0 60px #315cff77;
}

.overlayBox h1{
  font-size:40px;
  margin-top:0;
}

/* =========================================================
   MOBILE
========================================================= */

@media(max-width:700px){

  .arena{
    height:55vh;
    min-height:410px;
  }

  .fighter{
    transform:scale(.68);
    transform-origin:bottom center;
  }

  #player{
    left:-20px;
  }

  #enemy{
    right:-20px;
  }

  .boss.level3{
    transform:scale(.95);
    transform-origin:bottom center;
  }

  .health{
    width:43%;
    min-width:0;
  }

  .status{
    top:67px;
    font-size:11px;
  }

  .controls{
    grid-template-columns:repeat(2,1fr);
  }

  .controls button{
    min-height:58px;
    padding:8px;
    font-size:13px;
  }
}
</style>
</head>

<body>

<!-- =====================================================
     SAVE SCREEN
===================================================== -->

<div id="saveScreen" class="screen">

  <div class="menu">

    <h1 class="title">SHADOWBOUND</h1>

    <div class="subtitle">
      SPIRITUAL POWER
    </div>

    <div id="saveGrid" class="saveGrid"></div>

    <button onclick="newSave()">
      CREATE NEW SAVE
    </button>

  </div>

</div>


<!-- =====================================================
     CHARACTER CREATION
===================================================== -->

<div id="customScreen" class="screen hidden">

  <div class="customize">

    <h2>Create Your Warrior</h2>

    <label>
      Warrior Name
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
      <input id="helmetInput" type="color" value="#171822">
    </label>

    <br>

    <button onclick="createCharacter()">
      BEGIN JOURNEY
    </button>

  </div>

</div>


<!-- =====================================================
     GAME
===================================================== -->

<div id="game" class="hidden">

  <div class="topBar">

    <div class="levelText">
      LEVEL <span id="level">1</span>
    </div>

    <div class="power">
      SPIRITUAL POWER:
      <span id="power">0</span>
    </div>

  </div>


  <div class="arena" id="arena">

    <div class="horizon"></div>

    <div class="floor"></div>


    <!-- PLAYER HEALTH -->

    <div class="health playerHealthArea">

      <div class="name" id="playerName">
        Warrior
      </div>

      <div class="bar">
        <div id="playerHealth"
             class="fill gold"
             style="width:100%">
        </div>
      </div>

      <div class="hpText" id="playerHpText">
        100 / 100
      </div>

    </div>


    <!-- ENEMY HEALTH -->

    <div class="health enemyHealthArea">

      <div class="name" id="enemyName">
        Shadow Demon
      </div>

      <div class="bar">
        <div id="enemyHealth"
             class="fill red"
             style="width:100%">
        </div>
      </div>

      <div class="hpText" id="enemyHpText">
        100 / 100
      </div>

    </div>


    <div class="status" id="status">
      YOUR TURN
    </div>


    <!-- PLAYER -->

    <div id="player" class="fighter">

      <div class="playerGlow"></div>

      <div class="playerHead">

        <div class="hair"></div>

        <div class="eye a"></div>
        <div class="eye b"></div>

        <div class="mouth"></div>

      </div>

      <div class="neck"></div>

      <div class="chest">
        <div class="core"></div>
      </div>

      <div class="shoulder a"></div>
      <div class="shoulder b"></div>

      <div class="arm a"></div>
      <div class="arm b"></div>

      <div class="leg a"></div>
      <div class="leg b"></div>

      <div class="boot a"></div>
      <div class="boot b"></div>

    </div>


    <!-- =================================================
         ENEMY
         Completely rebuilt depending on level
    ================================================= -->

    <div id="enemy" class="fighter">

      <div id="bossVisual" class="boss level1">

        <!-- Level 1 is inserted by JavaScript -->

      </div>

    </div>

  </div>


  <!-- ATTACK BUTTONS -->

  <div id="attackControls" class="controls">

    <button onclick="attack('strike')">
      ✨ SPIRIT STRIKE
    </button>

    <button onclick="attack('shield')">
      🛡 SHIELD OF FATE
    </button>

    <button onclick="attack('truth')">
      ☀ WORD OF TRUTH
    </button>

    <button id="specialButton"
            class="special"
            onclick="attack('burst')"
            disabled>
      ⚡ LIGHT BURST
    </button>

  </div>


  <div id="log" class="log">
    Your journey begins...
  </div>

</div>


<!-- OVERLAY -->

<div id="overlay" class="overlay hidden">

  <div class="overlayBox">

    <h1 id="overlayTitle">
      Victory
    </h1>

    <p id="overlayText"></p>

    <button onclick="continueOverlay()">
      CONTINUE
    </button>

  </div>

</div>


<script>

/* =========================================================
   SAVE DATA
========================================================= */

const SAVE_KEY =
  "spiritualPowerShadowboundUltra";

let saves =
  JSON.parse(localStorage.getItem(SAVE_KEY) || "[]");

let currentSave = null;


/* =========================================================
   GAME DATA
========================================================= */

const levels = [

  {
    name:"SHADOW DEMON",
    hp:100,
    verse:"Ephesians 6:11",
    verseText:
      "Put on the whole armour of God, that ye may be able to stand against the wiles of the devil."
  },

  {
    name:"DARK ANGEL",
    hp:220,
    verse:"Psalm 18:2",
    verseText:
      "The LORD is my rock, and my fortress, and my deliverer; my God, my strength, in whom I will trust."
  },

  {
    name:"SHADOW COLOSSUS",
    hp:420,
    verse:"1 John 4:4",
    verseText:
      "Greater is he that is in you, than he that is in the world."
  }

];


/* =========================================================
   STATE
========================================================= */

let state = {

  name:"Warrior",

  gender:"Male",

  armor:"#315cff",

  helmet:"#171822",

  level:1,

  power:0,

  hp:100,

  spirit:0,

  turns:0,

  specialUnlocked:false

};

let enemy = {

  name:"",

  hp:0,

  maxHp:0

};

let busy = false;

let shieldActive = false;


/* =========================================================
   SAVE FUNCTIONS
========================================================= */

function saveAll(){

  localStorage.setItem(
    SAVE_KEY,
    JSON.stringify(saves)
  );

}

function safe(text){

  return String(text || "")
    .replaceAll("&","&amp;")
    .replaceAll("<","&lt;")
    .replaceAll(">","&gt;")
    .replaceAll('"',"&quot;")
    .replaceAll("'","&#039;");

}


function showSaves(){

  const grid =
    document.getElementById("saveGrid");

  grid.innerHTML="";

  for(let i=0;i<3;i++){

    const save = saves[i];

    const box =
      document.createElement("div");

    box.className="save";

    if(save){

      box.innerHTML=`

        <div class="saveName">
          ${safe(save.name)}
        </div>

        <div class="saveInfo">
          Level ${save.level}
          • Power ${save.power}
        </div>

        <button onclick="loadSave(${i})">
          CONTINUE
        </button>

        <button class="delete"
                onclick="deleteSave(${i})">
          DELETE
        </button>
      `;

    }else{

      box.innerHTML=`

        <div class="saveName">
          EMPTY SAVE SLOT ${i+1}
        </div>

        <button onclick="newSave(${i})">
          CREATE
        </button>
      `;

    }

    grid.appendChild(box);

  }

}


function newSave(slot){

  if(slot === undefined){

    slot =
      saves.findIndex(x=>!x);

    if(slot === -1){

      alert(
        "All three save slots are full."
      );

      return;
    }

  }

  currentSave=slot;

  document
    .getElementById("saveScreen")
    .classList.add("hidden");

  document
    .getElementById("customScreen")
    .classList.remove("hidden");

}


function deleteSave(slot){

  if(!confirm("Delete this save?"))
    return;

  saves[slot]=null;

  saveAll();

  showSaves();

}


function loadSave(slot){

  currentSave=slot;

  state =
    JSON.parse(
      JSON.stringify(saves[slot])
    );

  document
    .getElementById("saveScreen")
    .classList.add("hidden");

  startGame();

}


/* =========================================================
   CHARACTER CREATION
========================================================= */

function createCharacter(){

  state.name =
    document.getElementById("nameInput")
      .value.trim() || "Warrior";

  state.gender =
    document.getElementById("genderInput")
      .value;

  state.armor =
    document.getElementById("armorInput")
      .value;

  state.helmet =
    document.getElementById("helmetInput")
      .value;

  state.level=1;
  state.power=0;
  state.hp=100;
  state.spirit=0;
  state.turns=0;
  state.specialUnlocked=false;

  saveGame();

  document
    .getElementById("customScreen")
    .classList.add("hidden");

  startGame();

}


/* =========================================================
   START GAME
========================================================= */

function startGame(){

  document
    .getElementById("game")
    .classList.remove("hidden");

  busy=false;
  shieldActive=false;

  loadLevel();

  applyAppearance();

  updateUI();

  log(
    levels[0].verse +
    ": " +
    levels[0].verseText
  );

}


/* =========================================================
   LOAD LEVEL
========================================================= */

function loadLevel(){

  const data =
    levels[state.level-1];

  enemy.name=data.name;

  enemy.maxHp=data.hp;

  enemy.hp=data.hp;

  state.hp =
    100 + (state.level-1)*35;

  state.spirit=0;

  state.turns=0;

  state.specialUnlocked=false;

  busy=false;

  shieldActive=false;

  document
    .getElementById("specialButton")
    .disabled=true;

  buildBoss();

  updateUI();

}


/* =========================================================
   BOSS BUILDER
========================================================= */

function buildBoss(){

  const boss =
    document.getElementById("bossVisual");

  boss.className =
    "boss level" + state.level;


  /* LEVEL 1 */

  if(state.level===1){

    boss.innerHTML=`

      <div class="demonHead">

        <div class="demonHorn a"></div>
        <div class="demonHorn b"></div>

        <div class="demonEye a"></div>
        <div class="demonEye b"></div>

        <div class="demonMouth"></div>

      </div>

      <div class="demonBody">

        <div class="demonCore"></div>

      </div>

      <div class="demonArm a"></div>
      <div class="demonArm b"></div>

      <div class="demonLeg a"></div>
      <div class="demonLeg b"></div>

    `;

  }


  /* LEVEL 2 */

  else if(state.level===2){

    boss.innerHTML=`

      <div class="angelGlow"></div>

      <div class="angelWing a"></div>
      <div class="angelWing b"></div>

      <div class="angelHalo"></div>

      <div class="angelHead">

        <div class="angelVisor"></div>

      </div>

      <div class="angelBody">

        <div class="angelCore"></div>

      </div>

      <div class="angelArm a"></div>
      <div class="angelArm b"></div>

      <div class="angelLeg a"></div>
      <div class="angelLeg b"></div>

    `;

  }


  /* LEVEL 3 */

  else{

    boss.innerHTML=`

      <div class="colossusWing a"></div>
      <div class="colossusWing b"></div>

      <div class="colossusHead">

        <div class="colossusHorn a"></div>
        <div class="colossusHorn b"></div>

        <div class="colossusEye a"></div>
        <div class="colossusEye b"></div>

      </div>

      <div class="colossusBody">

        <div class="colossusPlate"></div>

        <div class="colossusCore"></div>

      </div>

      <div class="colossusArm a"></div>
      <div class="colossusArm b"></div>

      <div class="colossusLeg a"></div>
      <div class="colossusLeg b"></div>

    `;

  }

}


/* =========================================================
   PLAYER APPEARANCE
========================================================= */

function applyAppearance(){

  const chest =
    document.querySelector(".chest");

  chest.style.background =
    `linear-gradient(145deg,
      ${state.armor},
      #283aa7 55%,
      #11184d)`;

  document
    .querySelector(".hair")
    .style.background =
      state.helmet;

  document
    .getElementById("playerName")
    .textContent =
      state.name;

}


/* =========================================================
   UI
========================================================= */

function updateUI(){

  const maxPlayer =
    100 + (state.level-1)*35;

  document
    .getElementById("level")
    .textContent =
      state.level;

  document
    .getElementById("power")
    .textContent =
      state.power;

  document
    .getElementById("playerName")
    .textContent =
      state.name;

  document
    .getElementById("enemyName")
    .textContent =
      enemy.name;

  document
    .getElementById("playerHealth")
    .style.width =
      Math.max(
        0,
        state.hp/maxPlayer*100
      )+"%";

  document
    .getElementById("enemyHealth")
    .style.width =
      Math.max(
        0,
        enemy.hp/enemy.maxHp*100
      )+"%";

  document
    .getElementById("playerHpText")
    .textContent =
      `${Math.max(0,state.hp)} / ${maxPlayer}`;

  document
    .getElementById("enemyHpText")
    .textContent =
      `${Math.max(0,enemy.hp)} / ${enemy.maxHp}`;

  document
    .getElementById("specialButton")
    .disabled =
      !state.specialUnlocked || busy;

  document
    .getElementById("status")
    .textContent =
      busy
      ? "ENEMY TURN..."
      : "YOUR TURN";

}


/* =========================================================
   LOG
========================================================= */

function log(message){

  const box =
    document.getElementById("log");

  box.innerHTML +=
    `<div>${safe(message)}</div>`;

  box.scrollTop =
    box.scrollHeight;

}


/* =========================================================
   ATTACK SYSTEM
========================================================= */

function attack(type){

  if(busy)
    return;

  if(
    type==="burst" &&
    !state.specialUnlocked
  )
    return;

  busy=true;

  updateUI();


  if(type==="strike")
    spiritStrike();

  if(type==="shield")
    shieldOfFate();

  if(type==="truth")
    wordOfTruth();

  if(type==="burst")
    lightBurst();

}


/* =========================================================
   SPIRIT STRIKE
========================================================= */

function spiritStrike(){

  log("SPIRIT STRIKE!");

  const player =
    document.getElementById("player");

  player.classList.add("playerDash");

  setTimeout(()=>{

    player.classList.remove("playerDash");

    createLightOrb();

    const damage =
      20 + state.level*5;

    enemy.hp =
      Math.max(
        0,
        enemy.hp-damage
      );

    state.spirit+=12;

    hitEnemy();

    updateUI();

  },350);

  finishAttack(900);

}


/* =========================================================
   SHIELD
========================================================= */

function shieldOfFate(){

  log("SHIELD OF FATE!");

  shieldActive=true;

  state.spirit+=20;

  createShield();

  updateUI();

  finishAttack(850);

}


/* =========================================================
   WORD OF TRUTH
========================================================= */

function wordOfTruth(){

  log("WORD OF TRUTH!");

  createBeam();

  const damage =
    32 + state.level*6;

  enemy.hp =
    Math.max(
      0,
      enemy.hp-damage
    );

  state.spirit+=24;

  hitEnemy();

  updateUI();

  finishAttack(950);

}


/* =========================================================
   LIGHT BURST
========================================================= */

function lightBurst(){

  log("LIGHT BURST!");

  createBigBeam();

  const damage =
    100 + state.level*25;

  enemy.hp =
    Math.max(
      0,
      enemy.hp-damage
    );

  state.spirit=0;

  state.specialUnlocked=false;

  hitEnemy();

  updateUI();

  finishAttack(1100);

}


/* =========================================================
   FINISH PLAYER ATTACK
========================================================= */

function finishAttack(delay){

  setTimeout(()=>{

    if(enemy.hp<=0){

      enemyDefeated();

      return;

    }

    enemyAttack();

  },delay);

}


/* =========================================================
   ENEMY ATTACK
========================================================= */

function enemyAttack(){

  document
    .getElementById("status")
    .textContent =
      "ENEMY TURN...";


  /* SHIELD */

  if(shieldActive){

    log(
      "Shield of Fate blocked the attack!"
    );

    createShieldBlock();

    shieldActive=false;

    setTimeout(()=>{

      finishEnemyTurn();

    },700);

    return;

  }


  log(enemy.name+" attacks!");

  const boss =
    document.getElementById("enemy");

  boss.classList.add("enemyDash");


  /* DIFFERENT ATTACK EFFECT BY LEVEL */

  if(state.level===1){

    createShadowAttack();

  }

  else if(state.level===2){

    createAngelAttack();

  }

  else{

    createColossusAttack();

  }


  setTimeout(()=>{

    boss.classList.remove("enemyDash");

    const damage =
      12 + state.level*5;

    state.hp =
      Math.max(
        0,
        state.hp-damage
      );

    hitPlayer();

    updateUI();

  },350);


  setTimeout(()=>{

    if(state.hp<=0){

      playerDefeated();

      return;

    }

    finishEnemyTurn();

  },900);

}


/* =========================================================
   ENEMY TURN FINISH — COMBAT FIX
========================================================= */

function finishEnemyTurn(){

  state.turns++;

  if(state.turns>=3){

    state.specialUnlocked=true;

    log(
      "Your spiritual power has awakened!"
    );

  }

  saveGame();

  busy=false;

  shieldActive=false;


  /*
   FORCE THE CONTROLS BACK ON.
  */

  const controls =
    document.getElementById(
      "attackControls"
    );

  controls.style.pointerEvents="auto";

  controls.style.opacity="1";


  document
    .querySelectorAll(
      "#attackControls button"
    )
    .forEach(button=>{

      button.style.pointerEvents="auto";

      button.disabled=false;

    });


  document
    .getElementById("specialButton")
    .disabled =
      !state.specialUnlocked;


  updateUI();

  document
    .getElementById("status")
    .textContent =
      "YOUR TURN";

  log(
    "Your turn — choose an attack."
  );

}


/* =========================================================
   VISUAL ATTACKS
========================================================= */

function createLightOrb(){

  const arena =
    document.getElementById("arena");

  const orb =
    document.createElement("div");

  orb.className =
    "effect lightOrb";

  orb.style.left="28%";
  orb.style.top="50%";

  arena.appendChild(orb);

  orb.animate(

    [
      {
        transform:"translateX(0) scale(.3)",
        opacity:0
      },
      {
        transform:"translateX(300px) scale(1)",
        opacity:1
      },
      {
        transform:"translateX(550px) scale(.2)",
        opacity:0
      }
    ],

    {
      duration:650,
      easing:"ease-out"
    }

  ).onfinish=()=>{
    orb.remove();
  };

}


function createBeam(){

  const arena =
    document.getElementById("arena");

  const beam =
    document.createElement("div");

  beam.className =
    "effect lightBeam";

  arena.appendChild(beam);

  setTimeout(
    ()=>beam.remove(),
    650
  );

}


function createBigBeam(){

  const arena =
    document.getElementById("arena");

  const beam =
    document.createElement("div");

  beam.className =
    "effect bigBeam";

  arena.appendChild(beam);

  setTimeout(
    ()=>beam.remove(),
    900
  );

}


function createShield(){

  const arena =
    document.getElementById("arena");

  const shield =
    document.createElement("div");

  shield.className =
    "effect shield";

  shield.style.left="0";
  shield.style.top="25%";

  arena.appendChild(shield);

  setTimeout(
    ()=>shield.remove(),
    900
  );

}


function createShieldBlock(){

  const arena =
    document.getElementById("arena");

  const shield =
    document.createElement("div");

  shield.className =
    "effect shield";

  shield.style.left="0";
  shield.style.top="25%";

  shield.style.borderColor="#fff";

  arena.appendChild(shield);

  setTimeout(
    ()=>shield.remove(),
    700
  );

}


/* =========================================================
   UNIQUE BOSS ATTACK EFFECTS
========================================================= */

function createShadowAttack(){

  const arena =
    document.getElementById("arena");

  const orb =
    document.createElement("div");

  orb.className =
    "effect lightOrb";

  orb.style.background="#ff1640";

  orb.style.boxShadow =
    "0 0 20px #ff1640,0 0 50px #9b0030";

  orb.style.left="68%";
  orb.style.top="50%";

  arena.appendChild(orb);

  orb.animate(

    [
      {
        transform:"translateX(0) scale(.5)"
      },
      {
        transform:"translateX(-330px) scale(1)"
      }
    ],

    {
      duration:550
    }

  ).onfinish=()=>{
    orb.remove();
  };

}


function createAngelAttack(){

  const arena =
    document.getElementById("arena");

  const beam =
    document.createElement("div");

  beam.className =
    "effect lightBeam";

  beam.style.background=
    "linear-gradient(90deg,#fff,#9eaaff,#fff)";

  beam.style.boxShadow=
    "0 0 30px #fff,0 0 70px #8d9bff";

  beam.style.top="45%";

  arena.appendChild(beam);

  setTimeout(
    ()=>beam.remove(),
    700
  );

}


function createColossusAttack(){

  const arena =
    document.getElementById("arena");

  const beam =
    document.createElement("div");

  beam.className =
    "effect bigBeam";

  beam.style.background=
    "#ff1744";

  beam.style.boxShadow=
    "0 0 35px #ff1744,0 0 100px #b00030";

  beam.style.top="42%";

  arena.appendChild(beam);

  setTimeout(
    ()=>beam.remove(),
    850
  );

}


/* =========================================================
   HIT EFFECTS
========================================================= */

function hitEnemy(){

  const enemyEl =
    document.getElementById("enemy");

  enemyEl.classList.add("hit");

  setTimeout(
    ()=>enemyEl.classList.remove("hit"),
    450
  );

}


function hitPlayer(){

  const player =
    document.getElementById("player");

  player.classList.add("hit");

  setTimeout(
    ()=>player.classList.remove("hit"),
    450
  );

}


/* =========================================================
   PLAYER DEFEATED
========================================================= */

function playerDefeated(){

  busy=false;

  state.hp =
    100 + (state.level-1)*35;

  state.spirit=0;

  state.turns=0;

  state.specialUnlocked=false;

  saveGame();

  showOverlay(
    "DEFEATED",
    "The battle is not over. Rise and try again."
  );

}


/* =========================================================
   ENEMY DEFEATED
========================================================= */

function enemyDefeated(){

  busy=false;

  state.power +=
    100*state.level;

  saveGame();


  if(state.level>=3){

    showOverlay(
      "VICTORY!",
      "The Shadow Colossus has fallen. You completed the Shadowbound journey."
    );

    return;

  }


  showOverlay(
    "BOSS DEFEATED",
    `You defeated ${enemy.name}. Prepare for Level ${state.level+1}.`
  );

}


/* =========================================================
   OVERLAY
========================================================= */

function showOverlay(title,text){

  document
    .getElementById("overlayTitle")
    .textContent=title;

  document
    .getElementById("overlayText")
    .textContent=text;

  document
    .getElementById("overlay")
    .classList.remove("hidden");

}


function continueOverlay(){

  document
    .getElementById("overlay")
    .classList.add("hidden");


  if(
    state.level>=3 &&
    enemy.hp<=0
  ){

    state.level=1;

    state.power=0;

    loadLevel();

    saveGame();

    return;

  }


  if(enemy.hp<=0){

    state.level++;

    loadLevel();

    saveGame();

    log(
      `LEVEL ${state.level}: ${enemy.name}`
    );

    return;

  }


  loadLevel();

}


/* =========================================================
   SAVE GAME
========================================================= */

function saveGame(){

  if(currentSave===null)
    return;

  saves[currentSave] =
    JSON.parse(
      JSON.stringify(state)
    );

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
   START
========================================================= */

showSaves();


/*
 IMPORTANT TOUCH SAFETY:

 Visual effects can NEVER intercept
 taps intended for the buttons.
*/

document.addEventListener(
  "touchstart",
  ()=>{
    const controls =
      document.getElementById(
        "attackControls"
      );

    if(controls){
      controls.style.pointerEvents="auto";
    }
  },
  {passive:true}
);

</script>

</body>
</html>
