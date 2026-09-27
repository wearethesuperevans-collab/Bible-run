<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>Spiritual Power: Shadowbound</title>

<style>
*{box-sizing:border-box}
body{
  margin:0;
  font-family:Arial,sans-serif;
  background:
    radial-gradient(circle at 50% 25%,#263a70 0%,#10162d 38%,#050712 100%);
  color:white;
  min-height:100vh;
  overflow-x:hidden;
}

button{
  font:inherit;
  cursor:pointer;
  border:0;
}

#game{
  width:100%;
  max-width:1100px;
  margin:auto;
  min-height:100vh;
  padding:12px;
}

.top{
  display:flex;
  justify-content:space-between;
  align-items:center;
  gap:10px;
  flex-wrap:wrap;
  margin-bottom:10px;
}

.title{
  font-size:clamp(22px,5vw,38px);
  font-weight:900;
  letter-spacing:1px;
  text-shadow:0 0 12px #68aaff;
}

.level{
  padding:8px 14px;
  border-radius:20px;
  background:#151d3a;
  border:1px solid #5875b9;
  font-weight:bold;
}

.arena{
  position:relative;
  height:540px;
  border-radius:24px;
  overflow:hidden;
  border:2px solid #344d82;
  background:
    radial-gradient(circle at 50% 65%,rgba(90,130,255,.2),transparent 35%),
    linear-gradient(#101832,#080b18);
  box-shadow:inset 0 0 80px #000;
}

.stars{
  position:absolute;
  inset:0;
  background-image:
    radial-gradient(circle,#fff 1px,transparent 2px),
    radial-gradient(circle,#9fc9ff 1px,transparent 2px);
  background-size:85px 85px,137px 137px;
  opacity:.35;
}

.ground{
  position:absolute;
  bottom:0;
  left:0;
  right:0;
  height:110px;
  background:
    linear-gradient(transparent,#080b13),
    repeating-linear-gradient(165deg,#11182a 0 2px,transparent 2px 42px);
  border-top:2px solid #28365b;
}

.status{
  position:absolute;
  top:15px;
  left:15px;
  right:15px;
  display:flex;
  justify-content:space-between;
  gap:20px;
  z-index:20;
}

.healthBox{
  width:42%;
  min-width:140px;
}

.name{
  font-weight:900;
  margin-bottom:5px;
  text-shadow:0 2px 3px #000;
}

.health{
  height:20px;
  border-radius:15px;
  overflow:hidden;
  background:#191b24;
  border:2px solid #d9b544;
  box-shadow:0 0 10px rgba(255,205,50,.4);
}

.healthFill{
  height:100%;
  width:100%;
  background:linear-gradient(#fff18b,#d8a900,#ffdf45);
  transition:width .35s;
}

.enemyHealth{
  border-color:#d74758;
}

.enemyHealth .healthFill{
  background:linear-gradient(#ff8994,#d5223c,#ff5265);
}

.character{
  position:absolute;
  bottom:75px;
  width:190px;
  height:390px;
  z-index:10;
}

.player{
  left:4%;
}

.enemy{
  right:4%;
}

/* CHARACTER SKELETON */

.model{
  position:absolute;
  inset:0;
  transform-origin:50% 85%;
}

.head{
  position:absolute;
  width:62px;
  height:68px;
  left:64px;
  top:20px;
  border-radius:45% 45% 42% 42%;
  background:linear-gradient(145deg,#f2c49c,#b87350);
  border:4px solid #dce8ff;
  z-index:8;
  transform-origin:50% 90%;
}

.face{
  position:absolute;
  width:40px;
  height:14px;
  left:7px;
  top:27px;
  border-top:4px solid #18213c;
  border-radius:50%;
}

.eye{
  position:absolute;
  width:7px;
  height:7px;
  border-radius:50%;
  background:#10203d;
  top:25px;
}

.eye.a{left:12px}
.eye.b{right:12px}

.body{
  position:absolute;
  width:90px;
  height:135px;
  left:50px;
  top:84px;
  border-radius:28px 28px 20px 20px;
  background:
    linear-gradient(90deg,#6c7b99,#eaf1ff 45%,#687a9e);
  border:4px solid #dbe8ff;
  z-index:6;
  transform-origin:50% 20%;
}

.chest{
  position:absolute;
  width:48px;
  height:55px;
  left:17px;
  top:18px;
  border-radius:50%;
  background:radial-gradient(circle,#fff,#8ce7ff 25%,#2377d5 60%,#102c65);
  box-shadow:0 0 18px #6bdcff;
}

.belt{
  position:absolute;
  left:0;
  right:0;
  top:88px;
  height:17px;
  background:#b38b1e;
  border-top:3px solid #ffe978;
  border-bottom:3px solid #70500b;
}

.arm{
  position:absolute;
  width:32px;
  height:125px;
  top:91px;
  z-index:5;
  transform-origin:50% 12px;
}

.arm.left{
  left:30px;
  transform:rotate(12deg);
}

.arm.right{
  right:30px;
  transform:rotate(-12deg);
}

.upperArm{
  position:absolute;
  width:30px;
  height:62px;
  top:0;
  border-radius:18px;
  background:linear-gradient(90deg,#65799f,#edf4ff,#65799f);
  border:3px solid #dbe8ff;
}

.forearm{
  position:absolute;
  width:28px;
  height:56px;
  top:52px;
  left:1px;
  border-radius:15px;
  background:linear-gradient(90deg,#65799f,#f2f7ff,#65799f);
  border:3px solid #dbe8ff;
  transform-origin:50% 5px;
}

.hand{
  position:absolute;
  width:27px;
  height:29px;
  left:2px;
  top:99px;
  border-radius:45% 45% 50% 50%;
  background:#e0aa83;
  border:3px solid #d9e5fa;
  transform-origin:50% 20%;
}

.finger{
  position:absolute;
  width:5px;
  height:14px;
  top:-8px;
  border-radius:5px;
  background:#e0aa83;
}

.f1{left:2px;transform:rotate(-18deg)}
.f2{left:8px;transform:rotate(-7deg)}
.f3{left:14px;transform:rotate(7deg)}
.f4{left:20px;transform:rotate(18deg)}

.leg{
  position:absolute;
  width:38px;
  height:150px;
  top:205px;
  z-index:4;
  transform-origin:50% 8px;
}

.leg.left{left:54px}
.leg.right{right:54px}

.thigh{
  position:absolute;
  width:34px;
  height:78px;
  border-radius:18px;
  background:linear-gradient(90deg,#65799f,#f0f5ff,#65799f);
  border:3px solid #dbe8ff;
}

.shin{
  position:absolute;
  top:68px;
  left:2px;
  width:34px;
  height:73px;
  border-radius:18px;
  background:linear-gradient(90deg,#65799f,#e9f1ff,#65799f);
  border:3px solid #dbe8ff;
  transform-origin:50% 7px;
}

.boot{
  position:absolute;
  width:48px;
  height:27px;
  top:128px;
  left:-5px;
  border-radius:12px 20px 8px 8px;
  background:#263d70;
  border:3px solid #dbe8ff;
}

.enemy .head{
  background:linear-gradient(145deg,#5a2032,#160b16);
  border-color:#bd3b56;
}

.enemy .body{
  background:linear-gradient(90deg,#180d20,#54182e,#130a18);
  border-color:#c73852;
}

.enemy .chest{
  background:radial-gradient(circle,#fff,#ff405c 25%,#791126 65%,#1c0710);
  box-shadow:0 0 22px #ff2448;
}

.enemy .arm,
.enemy .leg{
  filter:hue-rotate(300deg) brightness(.7);
}

.enemy .hand{
  background:#421528;
  border-color:#c73852;
}

.horns{
  position:absolute;
  width:25px;
  height:40px;
  top:-25px;
  background:#54152c;
  clip-path:polygon(50% 0,100% 100%,55% 72%,0 100%);
}

.horn1{left:2px}
.horn2{right:2px}

.wings{
  position:absolute;
  width:90px;
  height:180px;
  top:70px;
  z-index:2;
}

.wing{
  position:absolute;
  width:85px;
  height:150px;
  background:linear-gradient(135deg,#20112e,#68152e,#18091c);
  clip-path:polygon(50% 0,100% 28%,78% 45%,100% 65%,63% 60%,74% 100%,42% 67%,0 82%,23% 50%,0 42%,35% 28%);
  opacity:.9;
}

.wing.one{right:70px;transform:scaleX(-1)}
.wing.two{left:70px}

.enemy .wings{
  display:block;
}

/* HAND ENERGY */

.handEnergy{
  position:absolute;
  width:35px;
  height:35px;
  border-radius:50%;
  background:radial-gradient(circle,#fff,#71eaff 30%,#287eff 65%,transparent 72%);
  box-shadow:0 0 25px #55dfff;
  opacity:0;
  z-index:20;
  pointer-events:none;
}

/* ATTACK ANIMATIONS */

.player.spirit .body{
  animation:torsoTwist .8s ease;
}
.player.spirit .head{
  animation:headTurn .8s ease;
}
.player.spirit .arm.right{
  animation:spiritArm .8s ease;
}
.player.spirit .arm.right .forearm{
  animation:spiritForearm .8s ease;
}
.player.spirit .arm.right .hand{
  animation:spiritHand .8s ease;
}
.player.spirit .arm.left{
  animation:backArm .8s ease;
}
.player.spirit .leg.left{
  animation:stepLeg .8s ease;
}
.player.spirit .leg.right{
  animation:backLeg .8s ease;
}

@keyframes spiritArm{
  0%{transform:rotate(-12deg)}
  25%{transform:rotate(-55deg)}
  55%{transform:rotate(-38deg)}
  100%{transform:rotate(-12deg)}
}

@keyframes spiritForearm{
  0%{transform:rotate(0)}
  30%{transform:rotate(55deg)}
  60%{transform:rotate(-15deg)}
  100%{transform:rotate(0)}
}

@keyframes spiritHand{
  0%,35%{transform:rotate(0) scale(1)}
  55%{transform:rotate(15deg) scale(1.2)}
  70%{transform:rotate(0) scale(.9)}
  100%{transform:rotate(0) scale(1)}
}

@keyframes backArm{
  0%{transform:rotate(12deg)}
  35%{transform:rotate(55deg)}
  65%{transform:rotate(30deg)}
  100%{transform:rotate(12deg)}
}

@keyframes torsoTwist{
  0%{transform:rotate(0)}
  35%{transform:rotate(-8deg)}
  60%{transform:rotate(5deg)}
  100%{transform:rotate(0)}
}

@keyframes headTurn{
  0%{transform:rotate(0)}
  50%{transform:rotate(-7deg)}
  100%{transform:rotate(0)}
}

@keyframes stepLeg{
  0%{transform:rotate(0)}
  40%{transform:rotate(18deg) translateY(5px)}
  70%{transform:rotate(-5deg)}
  100%{transform:rotate(0)}
}

@keyframes backLeg{
  0%{transform:rotate(0)}
  40%{transform:rotate(-12deg)}
  70%{transform:rotate(4deg)}
  100%{transform:rotate(0)}
}

/* SHIELD */

.player.shieldMove .arm.left{
  animation:shieldArm .9s ease;
}
.player.shieldMove .arm.left .forearm{
  animation:shieldForearm .9s ease;
}
.player.shieldMove .arm.left .hand{
  animation:shieldHand .9s ease;
}
.player.shieldMove .body{
  animation:shieldBody .9s ease;
}

@keyframes shieldArm{
  0%{transform:rotate(12deg)}
  35%{transform:rotate(-30deg)}
  65%{transform:rotate(-55deg)}
  100%{transform:rotate(12deg)}
}

@keyframes shieldForearm{
  0%{transform:rotate(0)}
  40%{transform:rotate(-65deg)}
  70%{transform:rotate(-40deg)}
  100%{transform:rotate(0)}
}

@keyframes shieldHand{
  0%{transform:rotate(0)}
  45%{transform:rotate(-35deg) scale(1.15)}
  100%{transform:rotate(0)}
}

@keyframes shieldBody{
  0%{transform:rotate(0)}
  50%{transform:rotate(8deg)}
  100%{transform:rotate(0)}
}

/* WORD OF TRUTH */

.player.truth .arm.left{
  animation:truthLeft .95s ease;
}
.player.truth .arm.right{
  animation:truthRight .95s ease;
}
.player.truth .arm.left .forearm,
.player.truth .arm.right .forearm{
  animation:truthForearm .95s ease;
}
.player.truth .arm.left .hand,
.player.truth .arm.right .hand{
  animation:truthHands .95s ease;
}
.player.truth .body{
  animation:truthBody .95s ease;
}

@keyframes truthLeft{
  0%{transform:rotate(12deg)}
  40%{transform:rotate(-48deg)}
  65%{transform:rotate(-30deg)}
  100%{transform:rotate(12deg)}
}

@keyframes truthRight{
  0%{transform:rotate(-12deg)}
  40%{transform:rotate(48deg)}
  65%{transform:rotate(30deg)}
  100%{transform:rotate(-12deg)}
}

@keyframes truthForearm{
  0%{transform:rotate(0)}
  45%{transform:rotate(-55deg)}
  65%{transform:rotate(-10deg)}
  100%{transform:rotate(0)}
}

@keyframes truthHands{
  0%{transform:scale(1)}
  45%{transform:scale(1.3) rotate(15deg)}
  70%{transform:scale(1.05)}
  100%{transform:scale(1)}
}

@keyframes truthBody{
  0%{transform:translateY(0)}
  45%{transform:translateY(-10px) rotate(0)}
  70%{transform:translateY(0)}
  100%{transform:translateY(0)}
}

/* LIGHT BURST */

.player.burst .arm.left{
  animation:burstLeft 1.2s ease;
}
.player.burst .arm.right{
  animation:burstRight 1.2s ease;
}
.player.burst .leg.left{
  animation:burstLegLeft 1.2s ease;
}
.player.burst .leg.right{
  animation:burstLegRight 1.2s ease;
}
.player.burst .body{
  animation:burstBody 1.2s ease;
}
.player.burst .head{
  animation:burstHead 1.2s ease;
}

@keyframes burstLeft{
  0%{transform:rotate(12deg)}
  25%{transform:rotate(60deg)}
  55%{transform:rotate(-75deg)}
  80%{transform:rotate(-35deg)}
  100%{transform:rotate(12deg)}
}

@keyframes burstRight{
  0%{transform:rotate(-12deg)}
  25%{transform:rotate(-60deg)}
  55%{transform:rotate(75deg)}
  80%{transform:rotate(35deg)}
  100%{transform:rotate(-12deg)}
}

@keyframes burstLegLeft{
  0%{transform:rotate(0)}
  30%{transform:rotate(12deg) translateY(8px)}
  55%{transform:rotate(-10deg)}
  100%{transform:rotate(0)}
}

@keyframes burstLegRight{
  0%{transform:rotate(0)}
  30%{transform:rotate(-12deg) translateY(8px)}
  55%{transform:rotate(10deg)}
  100%{transform:rotate(0)}
}

@keyframes burstBody{
  0%{transform:scale(1)}
  35%{transform:scale(.92) translateY(8px)}
  65%{transform:scale(1.1) translateY(-12px)}
  100%{transform:scale(1)}
}

@keyframes burstHead{
  0%{transform:rotate(0)}
  45%{transform:rotate(10deg)}
  70%{transform:rotate(-10deg)}
  100%{transform:rotate(0)}
}

/* ENEMY MOVEMENT */

.enemy.enemyMove .arm.right{
  animation:enemyArm .9s ease;
}
.enemy.enemyMove .arm.right .forearm{
  animation:enemyForearm .9s ease;
}
.enemy.enemyMove .arm.right .hand{
  animation:enemyHand .9s ease;
}
.enemy.enemyMove .body{
  animation:enemyBody .9s ease;
}
.enemy.enemyMove .leg.left{
  animation:enemyLeg .9s ease;
}

@keyframes enemyArm{
  0%{transform:rotate(-12deg)}
  35%{transform:rotate(55deg)}
  65%{transform:rotate(25deg)}
  100%{transform:rotate(-12deg)}
}

@keyframes enemyForearm{
  0%{transform:rotate(0)}
  40%{transform:rotate(-55deg)}
  65%{transform:rotate(25deg)}
  100%{transform:rotate(0)}
}

@keyframes enemyHand{
  0%{transform:scale(1)}
  50%{transform:scale(1.35)}
  70%{transform:scale(.9)}
  100%{transform:scale(1)}
}

@keyframes enemyBody{
  0%{transform:rotate(0)}
  45%{transform:rotate(-8deg)}
  70%{transform:rotate(5deg)}
  100%{transform:rotate(0)}
}

@keyframes enemyLeg{
  0%{transform:rotate(0)}
  45%{transform:rotate(-12deg)}
  70%{transform:rotate(5deg)}
  100%{transform:rotate(0)}
}

/* EFFECTS */

.projectile{
  position:absolute;
  width:28px;
  height:28px;
  border-radius:50%;
  background:radial-gradient(circle,#fff,#70edff 30%,#277cff 65%,transparent 72%);
  box-shadow:0 0 25px #5ddcff;
  z-index:30;
  animation:projectileFly .5s linear forwards;
}

@keyframes projectileFly{
  from{transform:translateX(0) scale(.5);opacity:0}
  15%{opacity:1}
  to{transform:translateX(570px) scale(1.2);opacity:1}
}

.beam{
  position:absolute;
  height:25px;
  left:180px;
  top:250px;
  width:0;
  border-radius:20px;
  background:linear-gradient(90deg,#fff,#8cf3ff,#477bff,#fff);
  box-shadow:0 0 25px #65e8ff;
  z-index:25;
  animation:beamFire .65s ease-out forwards;
}

@keyframes beamFire{
  0%{width:0;opacity:0}
  25%{width:180px;opacity:1}
  100%{width:650px;opacity:1}
}

.bigBeam{
  position:absolute;
  left:150px;
  top:230px;
  height:80px;
  width:0;
  border-radius:50%;
  background:radial-gradient(ellipse,#fff,#9df8ff 25%,#398bff 55%,transparent 75%);
  filter:blur(2px);
  z-index:28;
  animation:bigBeam .8s ease-out forwards;
}

@keyframes bigBeam{
  0%{width:0;opacity:0}
  25%{width:280px;opacity:1}
  100%{width:720px;opacity:1}
}

.shield{
  position:absolute;
  left:105px;
  top:145px;
  width:90px;
  height:130px;
  border-radius:48% 48% 55% 55%;
  border:7px solid #ffe46b;
  background:radial-gradient(circle,rgba(255,255,255,.8),rgba(80,190,255,.3),rgba(20,80,180,.15));
  box-shadow:0 0 35px #ffd83d;
  z-index:35;
  animation:shieldAppear .4s ease forwards;
}

@keyframes shieldAppear{
  from{transform:scale(.2) rotate(-30deg);opacity:0}
  to{transform:scale(1) rotate(0);opacity:1}
}

.ring{
  position:absolute;
  left:55px;
  top:110px;
  width:100px;
  height:100px;
  border:7px solid #70edff;
  border-radius:50%;
  box-shadow:0 0 35px #70edff;
  z-index:24;
  animation:ringExpand .7s ease forwards;
}

@keyframes ringExpand{
  from{transform:scale(.3);opacity:0}
  to{transform:scale(4);opacity:0}
}

.impact{
  position:absolute;
  width:100px;
  height:100px;
  border-radius:50%;
  border:8px solid white;
  right:95px;
  top:210px;
  z-index:40;
  animation:impact .45s ease-out forwards;
}

@keyframes impact{
  from{transform:scale(.2);opacity:1}
  to{transform:scale(1.8);opacity:0}
}

.flash{
  position:absolute;
  inset:0;
  background:white;
  opacity:0;
  z-index:50;
  pointer-events:none;
  animation:flash .3s ease;
}

@keyframes flash{
  0%{opacity:.8}
  100%{opacity:0}
}

.controls{
  margin-top:12px;
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:10px;
}

.attack{
  min-height:60px;
  border-radius:15px;
  color:white;
  font-weight:900;
  background:linear-gradient(#314c88,#17284f);
  border:2px solid #6686ce;
  box-shadow:0 4px 0 #0b142b;
  transition:.12s;
}

.attack:active{
  transform:translateY(3px);
  box-shadow:0 1px 0 #0b142b;
}

.attack:disabled{
  opacity:.4;
  cursor:not-allowed;
}

.log{
  margin-top:12px;
  min-height:70px;
  padding:12px;
  border-radius:15px;
  background:rgba(8,12,27,.9);
  border:1px solid #334a7d;
  color:#dce8ff;
  line-height:1.45;
}

.verse{
  margin-top:10px;
  padding:12px;
  border-left:4px solid #e6c24d;
  background:rgba(255,220,80,.06);
  color:#fff1a7;
  font-style:italic;
}

@media(max-width:700px){
  .arena{
    height:480px;
  }

  .character{
    transform:scale(.82);
    transform-origin:bottom center;
  }

  .player{left:-2%}
  .enemy{right:-2%}

  .controls{
    grid-template-columns:repeat(2,1fr);
  }
}

@media(max-width:480px){
  .arena{
    height:430px;
  }

  .character{
    transform:scale(.68);
  }

  .status{
    gap:8px;
  }

  .healthBox{
    min-width:0;
    width:45%;
  }
}
</style>
</head>

<body>

<div id="game">

  <div class="top">
    <div class="title">SPIRITUAL POWER</div>
    <div class="level" id="levelText">LEVEL 1 — SHADOW DEMON</div>
  </div>

  <div class="arena" id="arena">

    <div class="stars"></div>
    <div class="ground"></div>

    <div class="status">

      <div class="healthBox">
        <div class="name">SPIRIT WARRIOR</div>
        <div class="health">
          <div class="healthFill" id="playerHP"></div>
        </div>
      </div>

      <div class="healthBox">
        <div class="name" id="enemyName">SHADOW DEMON</div>
        <div class="health enemyHealth">
          <div class="healthFill" id="enemyHP"></div>
        </div>
      </div>

    </div>

    <!-- PLAYER -->

    <div class="character player" id="player">

      <div class="model">

        <div class="head">
          <div class="eye a"></div>
          <div class="eye b"></div>
          <div class="face"></div>
        </div>

        <div class="body">
          <div class="chest"></div>
          <div class="belt"></div>
        </div>

        <div class="arm left">
          <div class="upperArm"></div>
          <div class="forearm"></div>
          <div class="hand">
            <i class="finger f1"></i>
            <i class="finger f2"></i>
            <i class="finger f3"></i>
            <i class="finger f4"></i>
          </div>
        </div>

        <div class="arm right">
          <div class="upperArm"></div>
          <div class="forearm"></div>
          <div class="hand">
            <i class="finger f1"></i>
            <i class="finger f2"></i>
            <i class="finger f3"></i>
            <i class="finger f4"></i>
          </div>
        </div>

        <div class="leg left">
          <div class="thigh"></div>
          <div class="shin"></div>
          <div class="boot"></div>
        </div>

        <div class="leg right">
          <div class="thigh"></div>
          <div class="shin"></div>
          <div class="boot"></div>
        </div>

      </div>

      <div class="handEnergy" id="handEnergy"></div>

    </div>


    <!-- ENEMY -->

    <div class="character enemy" id="enemy">

      <div class="wings">
        <div class="wing one"></div>
        <div class="wing two"></div>
      </div>

      <div class="model">

        <div class="head">

          <div class="horns">
            <div class="horn1"></div>
            <div class="horn2"></div>
          </div>

          <div class="eye a"></div>
          <div class="eye b"></div>

        </div>

        <div class="body">
          <div class="chest"></div>
          <div class="belt"></div>
        </div>

        <div class="arm left">
          <div class="upperArm"></div>
          <div class="forearm"></div>
          <div class="hand"></div>
        </div>

        <div class="arm right">
          <div class="upperArm"></div>
          <div class="forearm"></div>
          <div class="hand"></div>
        </div>

        <div class="leg left">
          <div class="thigh"></div>
          <div class="shin"></div>
          <div class="boot"></div>
        </div>

        <div class="leg right">
          <div class="thigh"></div>
          <div class="shin"></div>
          <div class="boot"></div>
        </div>

      </div>

    </div>

  </div>


  <div class="controls">

    <button class="attack" id="strikeBtn">
      ⚡ SPIRIT STRIKE
    </button>

    <button class="attack" id="shieldBtn">
      🛡️ SHIELD OF FATE
    </button>

    <button class="attack" id="truthBtn">
      ✋ WORD OF TRUTH
    </button>

    <button class="attack" id="burstBtn">
      ☀️ LIGHT BURST
    </button>

  </div>

  <div class="log" id="log">
    The Shadow Demon approaches...
  </div>

  <div class="verse" id="verse">
    “Put on the whole armour of God, that ye may be able to stand against the wiles of the devil.”
    — Ephesians 6:11
  </div>

</div>


<script>

const player = document.getElementById("player");
const enemy = document.getElementById("enemy");
const arena = document.getElementById("arena");

const playerHPBar = document.getElementById("playerHP");
const enemyHPBar = document.getElementById("enemyHP");

const log = document.getElementById("log");
const levelText = document.getElementById("levelText");
const enemyName = document.getElementById("enemyName");

const strikeBtn = document.getElementById("strikeBtn");
const shieldBtn = document.getElementById("shieldBtn");
const truthBtn = document.getElementById("truthBtn");
const burstBtn = document.getElementById("burstBtn");

let playerHP = 100;
let enemyHP = 100;
let level = 1;

let busy = false;
let shieldActive = false;
let turnsSurvived = 0;
let specialUnlocked = false;


function wait(ms){
  return new Promise(resolve => setTimeout(resolve,ms));
}


function setButtons(enabled){

  const buttons = [
    strikeBtn,
    shieldBtn,
    truthBtn,
    burstBtn
  ];

  buttons.forEach(btn => {
    btn.disabled = !enabled;
  });

  burstBtn.disabled = !enabled || !specialUnlocked;
}


function message(text){
  log.innerHTML = text;
}


function updateBars(){

  playerHP = Math.max(0,Math.min(100,playerHP));
  enemyHP = Math.max(0,Math.min(100,enemyHP));

  playerHPBar.style.width = playerHP + "%";
  enemyHPBar.style.width = enemyHP + "%";
}


function clearAnimationClasses(){

  player.classList.remove(
    "spirit",
    "shieldMove",
    "truth",
    "burst"
  );

  enemy.classList.remove("enemyMove");
}


function effect(className){

  const el = document.createElement("div");
  el.className = className;

  arena.appendChild(el);

  setTimeout(() => el.remove(),1400);

  return el;
}


async function spiritStrike(){

  if(busy || enemyHP <= 0) return;

  busy = true;
  setButtons(false);

  clearAnimationClasses();

  message("⚡ The warrior pulls his arm back...");

  player.classList.add("spirit");

  await wait(350);

  message("⚡ His shoulder twists and his hand charges with light...");

  const energy = document.getElementById("handEnergy");

  energy.style.left = "120px";
  energy.style.top = "180px";
  energy.style.opacity = "1";

  await wait(250);

  message("⚡ SPIRIT STRIKE!");

  energy.style.opacity = "0";

  const projectile = document.createElement("div");
  projectile.className = "projectile";

  projectile.style.left = "150px";
  projectile.style.top = "210px";

  arena.appendChild(projectile);

  await wait(500);

  projectile.remove();

  damageEnemy(22);

  effect("impact");

  await wait(400);

  clearAnimationClasses();

  await enemyTurn();

}


async function shieldOfFate(){

  if(busy || enemyHP <= 0) return;

  busy = true;
  setButtons(false);

  clearAnimationClasses();

  message("🛡️ The warrior raises his arm...");

  player.classList.add("shieldMove");

  await wait(550);

  message("🛡️ His hand turns forward — SHIELD OF FATE!");

  const shield = effect("shield");

  shieldActive = true;

  await wait(900);

  shield.remove();

  clearAnimationClasses();

  await enemyTurn();

}


async function wordOfTruth(){

  if(busy || enemyHP <= 0) return;

  busy = true;
  setButtons(false);

  clearAnimationClasses();

  message("✋ The warrior raises both hands...");

  player.classList.add("truth");

  await wait(400);

  message("✋ Both hands focus into a single point of light...");

  const ring = effect("ring");

  await wait(400);

  message("✋ WORD OF TRUTH!");

  const beam = effect("beam");

  await wait(650);

  beam.remove();
  ring.remove();

  damageEnemy(30);

  effect("impact");

  await wait(400);

  clearAnimationClasses();

  await enemyTurn();

}


async function lightBurst(){

  if(
    busy ||
    enemyHP <= 0 ||
    !specialUnlocked
  ) return;

  busy = true;
  setButtons(false);

  clearAnimationClasses();

  message("☀️ The warrior crouches and gathers spiritual power...");

  player.classList.add("burst");

  await wait(500);

  message("☀️ Both arms rise as the armor begins glowing...");

  await wait(350);

  message("☀️ LIGHT BURST!");

  effect("ring");

  const beam = effect("bigBeam");

  await wait(800);

  beam.remove();

  damageEnemy(50);

  effect("impact");
  effect("flash");

  await wait(500);

  clearAnimationClasses();

  await enemyTurn();

}


function damageEnemy(amount){

  enemyHP -= amount;

  if(enemyHP < 0) enemyHP = 0;

  updateBars();

  if(enemyHP <= 0){

    message("✨ The Shadow Demon has been defeated!");

    setButtons(false);

    setTimeout(nextLevel,1200);
  }
}


async function enemyTurn(){

  if(enemyHP <= 0) return;

  await wait(450);

  message("👹 The enemy prepares its attack...");

  clearAnimationClasses();

  enemy.classList.add("enemyMove");

  await wait(550);

  message("👹 The Shadow Demon strikes!");

  await wait(300);

  if(shieldActive){

    shieldActive = false;

    message("🛡️ SHIELD OF FATE blocked the attack!");

    effect("shield");

    await wait(600);

  }else{

    const damage = Math.floor(Math.random()*9)+8;

    playerHP -= damage;

    updateBars();

    effect("impact");

    message(
      "💥 The attack connects! " +
      damage +
      " spiritual power lost."
    );

    await wait(500);
  }

  turnsSurvived++;

  if(turnsSurvived >= 3 && !specialUnlocked){

    specialUnlocked = true;

    message(
      "🔥 Your spiritual power has increased! " +
      "LIGHT BURST unlocked!"
    );

    await wait(1000);
  }

  clearAnimationClasses();

  if(playerHP <= 0){

    message("The warrior has fallen. Refresh to try again.");

    setButtons(false);

    return;
  }

  busy = false;
  setButtons(true);
}


function nextLevel(){

  level++;

  if(level > 3){

    message(
      "🏆 VICTORY! You defeated the Shadow Colossus!"
    );

    levelText.textContent = "VICTORY";

    return;
  }

  enemyHP = 100 + ((level-1)*20);
  playerHP = 100;

  specialUnlocked = false;
  turnsSurvived = 0;
  shieldActive = false;

  updateBars();

  if(level === 2){

    enemyName.textContent = "DARK ANGEL";
    levelText.textContent = "LEVEL 2 — DARK ANGEL";

    message(
      "🌑 The Dark Angel descends from the shadows..."
    );

    document.getElementById("verse").textContent =
      "“The LORD is my rock, and my fortress, and my deliverer.” — Psalm 18:2";

  }else{

    enemyName.textContent = "SHADOW COLOSSUS";
    levelText.textContent = "LEVEL 3 — SHADOW COLOSSUS";

    enemy.style.transform = "scale(1.15)";

    message(
      "👹 THE SHADOW COLOSSUS AWAKENS!"
    );

    document.getElementById("verse").textContent =
      "“Greater is he that is in you, than he that is in the world.” — 1 John 4:4";
  }

  busy = false;
  setButtons(true);
}


strikeBtn.addEventListener("click",spiritStrike);
shieldBtn.addEventListener("click",shieldOfFate);
truthBtn.addEventListener("click",wordOfTruth);
burstBtn.addEventListener("click",lightBurst);

updateBars();
setButtons(true);

</script>

</body>
</html>
