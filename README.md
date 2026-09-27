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
  background:#050713;
  color:white;
  font-family:Arial,Helvetica,sans-serif;
  overflow-x:hidden;
}

#game{
  width:min(1100px,100%);
  margin:auto;
  padding:12px;
}

.header{
  display:flex;
  justify-content:space-between;
  align-items:center;
  margin-bottom:10px;
  gap:10px;
}

.title{
  font-size:clamp(23px,5vw,38px);
  font-weight:900;
  letter-spacing:1px;
  text-shadow:0 0 18px #4fa8ff;
}

.level{
  background:#111a35;
  border:1px solid #4b67a5;
  border-radius:20px;
  padding:8px 13px;
  font-weight:bold;
}

.arena{
  position:relative;
  height:570px;
  overflow:hidden;
  border-radius:25px;
  border:2px solid #334c80;
  background:
    radial-gradient(circle at 50% 48%,#263a69 0%,#10182e 38%,#060812 85%);
  box-shadow:
    inset 0 0 100px #000,
    0 10px 35px #000;
}

.stars{
  position:absolute;
  inset:0;
  opacity:.5;
  background-image:
    radial-gradient(circle,#fff 1px,transparent 2px),
    radial-gradient(circle,#8cbcff 1px,transparent 2px);
  background-size:83px 83px,151px 151px;
}

.mist{
  position:absolute;
  left:-10%;
  right:-10%;
  bottom:70px;
  height:180px;
  background:radial-gradient(ellipse,rgba(80,130,255,.13),transparent 65%);
  filter:blur(15px);
}

.ground{
  position:absolute;
  bottom:0;
  width:100%;
  height:115px;
  background:
    linear-gradient(transparent,#050711),
    repeating-linear-gradient(
      165deg,
      #10172a 0 2px,
      transparent 2px 45px
    );
  border-top:2px solid #25365d;
}

.status{
  position:absolute;
  top:15px;
  left:15px;
  right:15px;
  display:flex;
  justify-content:space-between;
  z-index:100;
}

.healthBox{
  width:40%;
  min-width:150px;
}

.name{
  font-size:14px;
  font-weight:900;
  margin-bottom:5px;
  text-shadow:0 2px 4px #000;
}

.health{
  height:20px;
  border-radius:20px;
  overflow:hidden;
  background:#090b13;
  border:2px solid #e3bd39;
  box-shadow:0 0 12px rgba(255,205,50,.4);
}

.healthFill{
  width:100%;
  height:100%;
  background:linear-gradient(
    #fff39a,
    #e5bd24 45%,
    #b98400
  );
  transition:width .35s cubic-bezier(.2,.8,.2,1);
}

.enemyHealth{
  border-color:#dc465b;
}

.enemyHealth .healthFill{
  background:linear-gradient(
    #ff9ca7,
    #e52e48 45%,
    #8e1025
  );
}

/* =========================
   CHARACTER
========================= */

.character{
  position:absolute;
  width:210px;
  height:430px;
  bottom:62px;
  z-index:20;
  transform-origin:50% 90%;
}

.player{
  left:3%;
}

.enemy{
  right:3%;
}

.model{
  position:absolute;
  inset:0;
  transform-origin:50% 85%;
}

/* shadow underneath */

.character:after{
  content:"";
  position:absolute;
  left:42px;
  bottom:0;
  width:125px;
  height:24px;
  border-radius:50%;
  background:rgba(0,0,0,.65);
  filter:blur(7px);
  transform:scaleX(1);
  transition:.2s;
}

/* HEAD */

.head{
  position:absolute;
  width:64px;
  height:70px;
  left:73px;
  top:25px;
  border-radius:45% 45% 42% 42%;
  background:
    linear-gradient(
      110deg,
      #9a5d42,
      #edbd94 38%,
      #c27e5d 75%,
      #70402f
    );
  border:3px solid #dce8ff;
  z-index:15;
  transform-origin:50% 85%;
  box-shadow:inset -7px -5px 12px rgba(0,0,0,.25);
}

.face{
  position:absolute;
  left:10px;
  top:29px;
  width:44px;
  height:16px;
}

.eye{
  position:absolute;
  width:7px;
  height:5px;
  top:1px;
  border-radius:50%;
  background:#17233c;
}

.eye.a{left:5px}
.eye.b{right:5px}

.nose{
  position:absolute;
  left:20px;
  top:7px;
  width:4px;
  height:7px;
  border-right:2px solid #704735;
  transform:rotate(15deg);
}

.mouth{
  position:absolute;
  left:16px;
  top:12px;
  width:13px;
  height:5px;
  border-bottom:2px solid #733d35;
  border-radius:50%;
}

/* HAIR */

.hair{
  position:absolute;
  left:0;
  top:-5px;
  width:64px;
  height:25px;
  border-radius:50% 50% 20% 20%;
  background:#172036;
  z-index:4;
}

/* BODY */

.body{
  position:absolute;
  left:51px;
  top:91px;
  width:108px;
  height:143px;
  border-radius:32px 32px 22px 22px;
  background:
    linear-gradient(
      90deg,
      #33486f,
      #dbe8ff 38%,
      #f6fbff 50%,
      #b5c9e9 64%,
      #344a73
    );
  border:4px solid #dbe8ff;
  z-index:10;
  transform-origin:50% 20%;
  box-shadow:
    inset 0 0 12px rgba(0,0,0,.35),
    0 0 10px rgba(100,160,255,.2);
}

.shoulder{
  position:absolute;
  width:125px;
  height:35px;
  left:-12px;
  top:0;
  border-radius:50%;
  background:linear-gradient(#eaf4ff,#8198bd);
  border:3px solid #dbe8ff;
}

.chest{
  position:absolute;
  width:53px;
  height:58px;
  left:24px;
  top:22px;
  border-radius:50%;
  background:
    radial-gradient(
      circle,
      #fff 0 8%,
      #b7f8ff 15%,
      #4edaff 32%,
      #2360d1 57%,
      #122a67 70%,
      transparent 72%
    );
  box-shadow:
    0 0 12px #57dcff,
    0 0 25px rgba(70,180,255,.55);
}

.chestCore{
  position:absolute;
  width:14px;
  height:14px;
  left:19px;
  top:21px;
  border-radius:50%;
  background:white;
  box-shadow:0 0 12px white;
}

.belt{
  position:absolute;
  left:-2px;
  right:-2px;
  top:96px;
  height:18px;
  background:linear-gradient(#ffe779,#b58712,#e6bd35);
  border-top:3px solid #fff0a0;
  border-bottom:3px solid #71520a;
}

/* ARMS */

.arm{
  position:absolute;
  top:99px;
  width:37px;
  height:135px;
  z-index:9;
  transform-origin:50% 10px;
}

.arm.left{
  left:25px;
  transform:rotate(12deg);
}

.arm.right{
  right:25px;
  transform:rotate(-12deg);
}

.upperArm{
  position:absolute;
  top:0;
  left:2px;
  width:33px;
  height:66px;
  border-radius:18px;
  background:linear-gradient(
    90deg,
    #506a96,
    #f3f8ff 48%,
    #7188ac
  );
  border:3px solid #dce8ff;
  transform-origin:50% 8px;
}

.elbow{
  position:absolute;
  left:5px;
  top:55px;
  width:28px;
  height:28px;
  border-radius:50%;
  background:radial-gradient(circle,#fff,#7187aa);
  border:3px solid #dce8ff;
  z-index:5;
}

.forearm{
  position:absolute;
  left:4px;
  top:67px;
  width:30px;
  height:60px;
  border-radius:16px;
  background:linear-gradient(
    90deg,
    #4e6791,
    #f4f9ff 48%,
    #667fa7
  );
  border:3px solid #dce8ff;
  transform-origin:50% 5px;
}

.hand{
  position:absolute;
  left:4px;
  top:118px;
  width:28px;
  height:30px;
  border-radius:45%;
  background:linear-gradient(145deg,#f0c19a,#a96a4e);
  border:3px solid #dce8ff;
  transform-origin:50% 15%;
  z-index:8;
}

.finger{
  position:absolute;
  width:5px;
  height:14px;
  top:-8px;
  border-radius:5px;
  background:#d99d79;
}

.f1{left:1px;transform:rotate(-18deg)}
.f2{left:7px;transform:rotate(-7deg)}
.f3{left:13px;transform:rotate(6deg)}
.f4{left:19px;transform:rotate(18deg)}

/* LEGS */

.leg{
  position:absolute;
  top:218px;
  width:43px;
  height:165px;
  z-index:5;
  transform-origin:50% 10px;
}

.leg.left{left:54px}
.leg.right{right:54px}

.thigh{
  position:absolute;
  left:3px;
  top:0;
  width:37px;
  height:82px;
  border-radius:19px;
  background:linear-gradient(
    90deg,
    #526b96,
    #f2f7ff 48%,
    #607ba5
  );
  border:3px solid #dce8ff;
  transform-origin:50% 8px;
}

.knee{
  position:absolute;
  left:5px;
  top:70px;
  width:33px;
  height:33px;
  border-radius:50%;
  background:radial-gradient(circle,#fff,#748aad);
  border:3px solid #dce8ff;
  z-index:4;
}

.shin{
  position:absolute;
  left:5px;
  top:82px;
  width:35px;
  height:78px;
  border-radius:18px;
  background:linear-gradient(
    90deg,
    #536d99,
    #f3f8ff 48%,
    #607aa3
  );
  border:3px solid #dce8ff;
  transform-origin:50% 7px;
}

.boot{
  position:absolute;
  left:-4px;
  top:144px;
  width:53px;
  height:28px;
  border-radius:12px 22px 9px 9px;
  background:linear-gradient(#38538a,#101d3e);
  border:3px solid #dce8ff;
}

/* =========================
   DEMON
========================= */

.enemy .body{
  background:
    linear-gradient(
      90deg,
      #190d20,
      #64182e 40%,
      #2a0b20 70%,
      #100813
    );
  border-color:#c93a56;
}

.enemy .shoulder{
  background:linear-gradient(#74223d,#260b1b);
  border-color:#c93a56;
}

.enemy .chest{
  background:
    radial-gradient(
      circle,
      #fff 0 8%,
      #ff8190 13%,
      #ff294c 30%,
      #80152c 60%,
      transparent 72%
    );
  box-shadow:0 0 20px #ff294c;
}

.enemy .upperArm,
.enemy .forearm,
.enemy .thigh,
.enemy .shin{
  background:linear-gradient(
    90deg,
    #1a1022,
    #65203a 48%,
    #170a18
  );
  border-color:#b83350;
}

.enemy .elbow,
.enemy .knee{
  background:radial-gradient(circle,#a62d48,#1b0a18);
  border-color:#b83350;
}

.enemy .hand{
  background:#481427;
  border-color:#b83350;
}

.enemy .head{
  background:
    linear-gradient(
      145deg,
      #180916,
      #641b31 45%,
      #230914
    );
  border-color:#b83350;
}

.horns{
  position:absolute;
  width:30px;
  height:45px;
  top:-35px;
  background:linear-gradient(90deg,#160913,#72182f);
  clip-path:polygon(50% 0,100% 100%,55% 73%,0 100%);
}

.horn1{left:0}
.horn2{right:0}

.enemy .eye{
  background:#ff334f;
  box-shadow:0 0 8px #ff334f;
}

/* WINGS */

.wings{
  position:absolute;
  width:250px;
  height:220px;
  left:-20px;
  top:55px;
  z-index:1;
}

.wing{
  position:absolute;
  width:120px;
  height:210px;
  background:
    linear-gradient(
      135deg,
      #100914,
      #421328,
      #130812
    );
  clip-path:polygon(
    48% 0,
    100% 22%,
    76% 35%,
    100% 52%,
    69% 55%,
    82% 82%,
    50% 65%,
    32% 100%,
    28% 66%,
    0 79%,
    21% 48%,
    0 39%,
    34% 27%
  );
}

.wing.one{
  left:-28px;
  transform:scaleX(-1);
}

.wing.two{
  right:-28px;
}

/* =========================
   HAND ENERGY
========================= */

.handGlow{
  position:absolute;
  width:48px;
  height:48px;
  border-radius:50%;
  background:radial-gradient(
    circle,
    #fff,
    #9df7ff 20%,
    #3da6ff 45%,
    transparent 70%
  );
  box-shadow:0 0 25px #67e8ff;
  opacity:0;
  z-index:50;
  pointer-events:none;
}

/* =========================
   ATTACK ANIMATION STATES
========================= */

.player.attackStrike .model{
  animation:strikeBody 1.05s cubic-bezier(.2,.8,.2,1);
}

.player.attackStrike .head{
  animation:strikeHead 1.05s ease;
}

.player.attackStrike .arm.right{
  animation:strikeShoulder 1.05s cubic-bezier(.2,.8,.2,1);
}

.player.attackStrike .arm.right .forearm{
  animation:strikeElbow 1.05s cubic-bezier(.2,.8,.2,1);
}

.player.attackStrike .arm.right .hand{
  animation:strikeWrist 1.05s cubic-bezier(.2,.8,.2,1);
}

.player.attackStrike .arm.left{
  animation:strikeBackArm 1.05s cubic-bezier(.2,.8,.2,1);
}

.player.attackStrike .leg.left{
  animation:strikeFrontLeg 1.05s cubic-bezier(.2,.8,.2,1);
}

.player.attackStrike .leg.right{
  animation:strikeBackLeg 1.05s cubic-bezier(.2,.8,.2,1);
}

/* BODY */

@keyframes strikeBody{
  0%{
    transform:translateX(0) rotate(0);
  }
  18%{
    transform:translateX(-8px) rotate(-7deg);
  }
  48%{
    transform:translateX(5px) rotate(4deg);
  }
  62%{
    transform:translateX(17px) rotate(-2deg);
  }
  78%{
    transform:translateX(9px) rotate(2deg);
  }
  100%{
    transform:translateX(0) rotate(0);
  }
}

@keyframes strikeHead{
  0%{transform:rotate(0)}
  20%{transform:rotate(-9deg)}
  52%{transform:rotate(7deg)}
  75%{transform:rotate(-3deg)}
  100%{transform:rotate(0)}
}

/* SHOULDER */

@keyframes strikeShoulder{
  0%{
    transform:rotate(-12deg);
  }
  20%{
    transform:rotate(-63deg);
  }
  43%{
    transform:rotate(-76deg);
  }
  59%{
    transform:rotate(-24deg);
  }
  74%{
    transform:rotate(-2deg);
  }
  100%{
    transform:rotate(-12deg);
  }
}

/* ELBOW */

@keyframes strikeElbow{
  0%{
    transform:rotate(5deg);
  }
  25%{
    transform:rotate(62deg);
  }
  43%{
    transform:rotate(72deg);
  }
  58%{
    transform:rotate(-18deg);
  }
  72%{
    transform:rotate(-5deg);
  }
  100%{
    transform:rotate(5deg);
  }
}

/* WRIST */

@keyframes strikeWrist{
  0%{
    transform:scale(1) rotate(0);
  }
  42%{
    transform:scale(1.03) rotate(12deg);
  }
  58%{
    transform:scale(1.2) rotate(-12deg);
  }
  68%{
    transform:scale(.9) rotate(8deg);
  }
  100%{
    transform:scale(1) rotate(0);
  }
}

/* BACK ARM */

@keyframes strikeBackArm{
  0%{transform:rotate(12deg)}
  25%{transform:rotate(48deg)}
  45%{transform:rotate(37deg)}
  68%{transform:rotate(20deg)}
  100%{transform:rotate(12deg)}
}

/* LEGS */

@keyframes strikeFrontLeg{
  0%{transform:rotate(0)}
  25%{transform:rotate(8deg) translateY(3px)}
  45%{transform:rotate(14deg) translateY(5px)}
  68%{transform:rotate(-5deg)}
  100%{transform:rotate(0)}
}

@keyframes strikeBackLeg{
  0%{transform:rotate(0)}
  25%{transform:rotate(-7deg)}
  50%{transform:rotate(-10deg)}
  70%{transform:rotate(3deg)}
  100%{transform:rotate(0)}
}

/* =========================
   SHIELD
========================= */

.player.attackShield .model{
  animation:shieldBody .9s ease;
}

.player.attackShield .arm.left{
  animation:shieldShoulder .9s cubic-bezier(.2,.8,.2,1);
}

.player.attackShield .arm.left .forearm{
  animation:shieldElbow .9s cubic-bezier(.2,.8,.2,1);
}

.player.attackShield .arm.left .hand{
  animation:shieldWrist .9s ease;
}

.player.attackShield .leg.left{
  animation:shieldLeg .9s ease;
}

@keyframes shieldBody{
  0%{transform:translateX(0) rotate(0)}
  30%{transform:translateX(-7px) rotate(5deg)}
  58%{transform:translateX(-3px) rotate(2deg)}
  100%{transform:translateX(0) rotate(0)}
}

@keyframes shieldShoulder{
  0%{transform:rotate(12deg)}
  25%{transform:rotate(-25deg)}
  48%{transform:rotate(-52deg)}
  65%{transform:rotate(-43deg)}
  100%{transform:rotate(12deg)}
}

@keyframes shieldElbow{
  0%{transform:rotate(0)}
  30%{transform:rotate(-40deg)}
  52%{transform:rotate(-72deg)}
  72%{transform:rotate(-35deg)}
  100%{transform:rotate(0)}
}

@keyframes shieldWrist{
  0%{transform:rotate(0)}
  48%{transform:rotate(-30deg) scale(1.08)}
  65%{transform:rotate(-5deg)}
  100%{transform:rotate(0)}
}

@keyframes shieldLeg{
  0%{transform:rotate(0)}
  35%{transform:rotate(7deg)}
  60%{transform:rotate(-4deg)}
  100%{transform:rotate(0)}
}

/* =========================
   WORD OF TRUTH
========================= */

.player.attackTruth .model{
  animation:truthBody .95s ease;
}

.player.attackTruth .arm.left{
  animation:truthLeft .95s cubic-bezier(.2,.8,.2,1);
}

.player.attackTruth .arm.right{
  animation:truthRight .95s cubic-bezier(.2,.8,.2,1);
}

.player.attackTruth .arm.left .forearm{
  animation:truthLeftElbow .95s ease;
}

.player.attackTruth .arm.right .forearm{
  animation:truthRightElbow .95s ease;
}

.player.attackTruth .arm.left .hand,
.player.attackTruth .arm.right .hand{
  animation:truthHands .95s ease;
}

.player.attackTruth .head{
  animation:truthHead .95s ease;
}

@keyframes truthBody{
  0%{transform:translateY(0)}
  35%{transform:translateY(-7px) rotate(0)}
  58%{transform:translateY(-13px)}
  78%{transform:translateY(-4px)}
  100%{transform:translateY(0)}
}

@keyframes truthLeft{
  0%{transform:rotate(12deg)}
  30%{transform:rotate(-35deg)}
  53%{transform:rotate(-57deg)}
  68%{transform:rotate(-37deg)}
  100%{transform:rotate(12deg)}
}

@keyframes truthRight{
  0%{transform:rotate(-12deg)}
  30%{transform:rotate(35deg)}
  53%{transform:rotate(57deg)}
  68%{transform:rotate(37deg)}
  100%{transform:rotate(-12deg)}
}

@keyframes truthLeftElbow{
  0%{transform:rotate(0)}
  35%{transform:rotate(-55deg)}
  58%{transform:rotate(-80deg)}
  75%{transform:rotate(-25deg)}
  100%{transform:rotate(0)}
}

@keyframes truthRightElbow{
  0%{transform:rotate(0)}
  35%{transform:rotate(55deg)}
  58%{transform:rotate(80deg)}
  75%{transform:rotate(25deg)}
  100%{transform:rotate(0)}
}

@keyframes truthHands{
  0%{transform:scale(1)}
  40%{transform:scale(1.12)}
  58%{transform:scale(1.32) rotate(5deg)}
  70%{transform:scale(1)}
  100%{transform:scale(1)}
}

@keyframes truthHead{
  0%{transform:rotate(0)}
  40%{transform:rotate(-4deg)}
  60%{transform:rotate(4deg)}
  100%{transform:rotate(0)}
}

/* =========================
   LIGHT BURST
========================= */

.player.attackBurst .model{
  animation:burstBody 1.3s cubic-bezier(.2,.8,.2,1);
}

.player.attackBurst .arm.left{
  animation:burstLeft 1.3s cubic-bezier(.2,.8,.2,1);
}

.player.attackBurst .arm.right{
  animation:burstRight 1.3s cubic-bezier(.2,.8,.2,1);
}

.player.attackBurst .arm.left .forearm{
  animation:burstLeftElbow 1.3s ease;
}

.player.attackBurst .arm.right .forearm{
  animation:burstRightElbow 1.3s ease;
}

.player.attackBurst .arm.left .hand,
.player.attackBurst .arm.right .hand{
  animation:burstHands 1.3s ease;
}

.player.attackBurst .leg.left{
  animation:burstLegLeft 1.3s ease;
}

.player.attackBurst .leg.right{
  animation:burstLegRight 1.3s ease;
}

@keyframes burstBody{
  0%{transform:scale(1) translateY(0)}
  22%{transform:scale(.93) translateY(9px)}
  48%{transform:scale(.98) translateY(2px)}
  67%{transform:scale(1.13) translateY(-15px)}
  82%{transform:scale(1.05) translateY(-4px)}
  100%{transform:scale(1)}
}

@keyframes burstLeft{
  0%{transform:rotate(12deg)}
  25%{transform:rotate(67deg)}
  45%{transform:rotate(76deg)}
  62%{transform:rotate(-62deg)}
  78%{transform:rotate(-37deg)}
  100%{transform:rotate(12deg)}
}

@keyframes burstRight{
  0%{transform:rotate(-12deg)}
  25%{transform:rotate(-67deg)}
  45%{transform:rotate(-76deg)}
  62%{transform:rotate(62deg)}
  78%{transform:rotate(37deg)}
  100%{transform:rotate(-12deg)}
}

@keyframes burstLeftElbow{
  0%{transform:rotate(0)}
  30%{transform:rotate(-70deg)}
  48%{transform:rotate(-90deg)}
  65%{transform:rotate(60deg)}
  80%{transform:rotate(25deg)}
  100%{transform:rotate(0)}
}

@keyframes burstRightElbow{
  0%{transform:rotate(0)}
  30%{transform:rotate(70deg)}
  48%{transform:rotate(90deg)}
  65%{transform:rotate(-60deg)}
  80%{transform:rotate(-25deg)}
  100%{transform:rotate(0)}
}

@keyframes burstHands{
  0%{transform:scale(1)}
  35%{transform:scale(1.15)}
  60%{transform:scale(1.4)}
  72%{transform:scale(.8)}
  100%{transform:scale(1)}
}

@keyframes burstLegLeft{
  0%{transform:rotate(0)}
  25%{transform:rotate(12deg) translateY(8px)}
  48%{transform:rotate(-7deg)}
  70%{transform:rotate(4deg)}
  100%{transform:rotate(0)}
}

@keyframes burstLegRight{
  0%{transform:rotate(0)}
  25%{transform:rotate(-12deg) translateY(8px)}
  48%{transform:rotate(7deg)}
  70%{transform:rotate(-4deg)}
  100%{transform:rotate(0)}
}

/* =========================
   ENEMY ATTACK
========================= */

.enemy.enemyAttack .model{
  animation:demonBody .9s cubic-bezier(.2,.8,.2,1);
}

.enemy.enemyAttack .arm.right{
  animation:demonShoulder .9s cubic-bezier(.2,.8,.2,1);
}

.enemy.enemyAttack .arm.right .forearm{
  animation:demonElbow .9s cubic-bezier(.2,.8,.2,1);
}

.enemy.enemyAttack .arm.right .hand{
  animation:demonHand .9s ease;
}

.enemy.enemyAttack .leg.left{
  animation:demonLeg .9s ease;
}

@keyframes demonBody{
  0%{transform:translateX(0)}
  25%{transform:translateX(-8px) rotate(-6deg)}
  50%{transform:translateX(8px) rotate(5deg)}
  67%{transform:translateX(13px) rotate(-2deg)}
  100%{transform:translateX(0)}
}

@keyframes demonShoulder{
  0%{transform:rotate(-12deg)}
  28%{transform:rotate(63deg)}
  48%{transform:rotate(76deg)}
  63%{transform:rotate(-20deg)}
  100%{transform:rotate(-12deg)}
}

@keyframes demonElbow{
  0%{transform:rotate(0)}
  28%{transform:rotate(70deg)}
  50%{transform:rotate(85deg)}
  65%{transform:rotate(-25deg)}
  100%{transform:rotate(0)}
}

@keyframes demonHand{
  0%{transform:scale(1)}
  48%{transform:scale(1.3)}
  62%{transform:scale(.82)}
  100%{transform:scale(1)}
}

@keyframes demonLeg{
  0%{transform:rotate(0)}
  35%{transform:rotate(-12deg)}
  60%{transform:rotate(7deg)}
  100%{transform:rotate(0)}
}

/* =========================
   EFFECTS
========================= */

.projectile{
  position:absolute;
  width:30px;
  height:30px;
  border-radius:50%;
  background:
    radial-gradient(
      circle,
      #fff 0 12%,
      #a8faff 25%,
      #43a9ff 52%,
      transparent 72%
    );
  box-shadow:
    0 0 15px white,
    0 0 30px #54dfff,
    0 0 50px #287cff;
  z-index:70;
}

.projectileTrail{
  position:absolute;
  height:9px;
  width:110px;
  border-radius:20px;
  background:linear-gradient(
    90deg,
    transparent,
    #65eaff,
    white
  );
  filter:blur(2px);
  z-index:69;
}

.beam{
  position:absolute;
  left:175px;
  top:250px;
  width:0;
  height:28px;
  border-radius:20px;
  background:
    linear-gradient(
      #fff,
      #9af8ff,
      #3c8cff,
      #fff
    );
  box-shadow:
    0 0 15px white,
    0 0 30px #57dcff,
    0 0 55px #267aff;
  z-index:65;
  animation:beamGrow .55s cubic-bezier(.15,.8,.2,1) forwards;
}

@keyframes beamGrow{
  0%{
    width:0;
    opacity:0;
  }
  20%{
    width:130px;
    opacity:1;
  }
  100%{
    width:700px;
    opacity:1;
  }
}

.bigBeam{
  position:absolute;
  left:155px;
  top:220px;
  width:0;
  height:95px;
  border-radius:50%;
  background:
    radial-gradient(
      ellipse,
      white 0 10%,
      #b9fbff 18%,
      #56dfff 38%,
      #287aff 60%,
      transparent 76%
    );
  box-shadow:
    0 0 35px white,
    0 0 65px #53dcff;
  z-index:66;
  animation:bigBeamGrow .75s cubic-bezier(.15,.8,.2,1) forwards;
}

@keyframes bigBeamGrow{
  0%{
    width:0;
    opacity:0;
  }
  20%{
    width:160px;
    opacity:1;
  }
  100%{
    width:760px;
    opacity:1;
  }
}

.shield{
  position:absolute;
  left:92px;
  top:145px;
  width:105px;
  height:140px;
  border-radius:50% 50% 55% 55%;
  border:6px solid #ffe66a;
  background:
    radial-gradient(
      circle,
      rgba(255,255,255,.75),
      rgba(77,196,255,.28) 35%,
      rgba(20,70,170,.12) 65%,
      transparent
    );
  box-shadow:
    0 0 18px #ffe66a,
    inset 0 0 25px #72ddff;
  z-index:80;
  animation:shieldIn .32s cubic-bezier(.2,1.4,.4,1) forwards;
}

@keyframes shieldIn{
  from{
    opacity:0;
    transform:scale(.35) rotate(-20deg);
  }
  to{
    opacity:1;
    transform:scale(1) rotate(0);
  }
}

.ring{
  position:absolute;
  left:55px;
  top:105px;
  width:105px;
  height:105px;
  border-radius:50%;
  border:7px solid #72eaff;
  box-shadow:0 0 30px #4ddcff;
  z-index:60;
  animation:ringExpand .8s ease-out forwards;
}

@keyframes ringExpand{
  from{
    transform:scale(.3);
    opacity:1;
  }
  to{
    transform:scale(4);
    opacity:0;
  }
}

.impact{
  position:absolute;
  right:80px;
  top:205px;
  width:110px;
  height:110px;
  border-radius:50%;
  border:7px solid white;
  box-shadow:0 0 35px #fff;
  z-index:100;
  animation:impact .45s ease-out forwards;
}

@keyframes impact{
  from{
    transform:scale(.15);
    opacity:1;
  }
  to{
    transform:scale(1.8);
    opacity:0;
  }
}

.flash{
  position:absolute;
  inset:0;
  background:white;
  opacity:0;
  z-index:150;
  pointer-events:none;
  animation:flash .25s ease;
}

@keyframes flash{
  0%{opacity:.7}
  100%{opacity:0}
}

.damageNumber{
  position:absolute;
  right:115px;
  top:170px;
  font-size:28px;
  font-weight:900;
  color:#fff;
  text-shadow:
    0 0 5px #000,
    0 0 15px #65eaff;
  z-index:200;
  animation:damageFloat .7s ease-out forwards;
}

@keyframes damageFloat{
  from{
    transform:translateY(0) scale(.7);
    opacity:0;
  }
  20%{
    opacity:1;
  }
  to{
    transform:translateY(-65px) scale(1.1);
    opacity:0;
  }
}

/* CAMERA HIT */

.arena.hit{
  animation:cameraHit .22s ease;
}

@keyframes cameraHit{
  0%{transform:translateX(0)}
  25%{transform:translateX(-6px)}
  50%{transform:translateX(7px)}
  75%{transform:translateX(-4px)}
  100%{transform:translateX(0)}
}

/* CONTROLS */

.controls{
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:10px;
  margin-top:12px;
}

.attack{
  min-height:62px;
  border-radius:15px;
  color:white;
  font-weight:900;
  background:
    linear-gradient(#324d8b,#17284e);
  border:2px solid #6889d1;
  box-shadow:0 4px 0 #080f21;
  transition:transform .1s,filter .1s;
}

.attack:active{
  transform:translateY(3px);
  filter:brightness(1.25);
}

.attack:disabled{
  opacity:.4;
  cursor:not-allowed;
}

.log{
  min-height:70px;
  margin-top:12px;
  padding:13px;
  border-radius:15px;
  background:#090d1d;
  border:1px solid #304777;
  line-height:1.45;
}

.verse{
  margin-top:10px;
  padding:12px;
  border-left:4px solid #e4c34b;
  background:rgba(228,195,75,.06);
  color:#fff0a3;
  font-style:italic;
}

@media(max-width:700px){

  .arena{
    height:500px;
  }

  .character{
    transform:scale(.82);
    transform-origin:50% 90%;
  }

  .player{
    left:-3%;
  }

  .enemy{
    right:-3%;
  }

  .controls{
    grid-template-columns:repeat(2,1fr);
  }
}

@media(max-width:480px){

  .arena{
    height:450px;
  }

  .character{
    transform:scale(.68);
  }

  .status{
    left:10px;
    right:10px;
  }

  .healthBox{
    min-width:0;
    width:45%;
  }

  .name{
    font-size:11px;
  }
}
</style>
</head>

<body>

<div id="game">

  <div class="header">
    <div class="title">SPIRITUAL POWER</div>
    <div class="level" id="levelText">
      LEVEL 1 — SHADOW DEMON
    </div>
  </div>

  <div class="arena" id="arena">

    <div class="stars"></div>
    <div class="mist"></div>
    <div class="ground"></div>

    <div class="status">

      <div class="healthBox">
        <div class="name">SPIRIT WARRIOR</div>
        <div class="health">
          <div class="healthFill" id="playerHP"></div>
        </div>
      </div>

      <div class="healthBox">
        <div class="name" id="enemyName">
          SHADOW DEMON
        </div>
        <div class="health enemyHealth">
          <div class="healthFill" id="enemyHP"></div>
        </div>
      </div>

    </div>


    <!-- PLAYER -->

    <div class="character player" id="player">

      <div class="model">

        <div class="head">

          <div class="hair"></div>

          <div class="face">
            <div class="eye a"></div>
            <div class="eye b"></div>
            <div class="nose"></div>
            <div class="mouth"></div>
          </div>

        </div>

        <div class="body">

          <div class="shoulder"></div>

          <div class="chest">
            <div class="chestCore"></div>
          </div>

          <div class="belt"></div>

        </div>


        <div class="arm left">
          <div class="upperArm"></div>
          <div class="elbow"></div>
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
          <div class="elbow"></div>
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
          <div class="knee"></div>
          <div class="shin"></div>
          <div class="boot"></div>
        </div>


        <div class="leg right">
          <div class="thigh"></div>
          <div class="knee"></div>
          <div class="shin"></div>
          <div class="boot"></div>
        </div>

      </div>

      <div class="handGlow" id="handGlow"></div>

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

          <div class="face">
            <div class="eye a"></div>
            <div class="eye b"></div>
          </div>

        </div>

        <div class="body">

          <div class="shoulder"></div>

          <div class="chest">
            <div class="chestCore"></div>
          </div>

          <div class="belt"></div>

        </div>


        <div class="arm left">
          <div class="upperArm"></div>
          <div class="elbow"></div>
          <div class="forearm"></div>
          <div class="hand"></div>
        </div>


        <div class="arm right">
          <div class="upperArm"></div>
          <div class="elbow"></div>
          <div class="forearm"></div>
          <div class="hand"></div>
        </div>


        <div class="leg left">
          <div class="thigh"></div>
          <div class="knee"></div>
          <div class="shin"></div>
          <div class="boot"></div>
        </div>


        <div class="leg right">
          <div class="thigh"></div>
          <div class="knee"></div>
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

const strikeBtn = document.getElementById("strikeBtn");
const shieldBtn = document.getElementById("shieldBtn");
const truthBtn = document.getElementById("truthBtn");
const burstBtn = document.getElementById("burstBtn");

const log = document.getElementById("log");
const levelText = document.getElementById("levelText");
const enemyName = document.getElementById("enemyName");
const verse = document.getElementById("verse");

let playerHP = 100;
let enemyHP = 100;

let busy = false;
let shieldActive = false;
let turnsSurvived = 0;
let specialUnlocked = false;
let level = 1;


function wait(ms){
  return new Promise(resolve => setTimeout(resolve,ms));
}


function message(text){
  log.innerHTML = text;
}


function buttons(enabled){

  strikeBtn.disabled = !enabled;
  shieldBtn.disabled = !enabled;
  truthBtn.disabled = !enabled;

  burstBtn.disabled =
    !enabled ||
    !specialUnlocked;
}


function updateHP(){

  playerHP = Math.max(0,Math.min(100,playerHP));
  enemyHP = Math.max(0,Math.min(100,enemyHP));

  playerHPBar.style.width = playerHP+"%";
  enemyHPBar.style.width = enemyHP+"%";
}


function clearStates(){

  player.classList.remove(
    "attackStrike",
    "attackShield",
    "attackTruth",
    "attackBurst"
  );

  enemy.classList.remove("enemyAttack");
}


function screenHit(){

  arena.classList.remove("hit");

  void arena.offsetWidth;

  arena.classList.add("hit");
}


function impact(){

  const x = document.createElement("div");

  x.className = "impact";

  arena.appendChild(x);

  screenHit();

  setTimeout(()=>x.remove(),500);
}


function damageText(amount){

  const d = document.createElement("div");

  d.className = "damageNumber";
  d.textContent = "-"+amount;

  arena.appendChild(d);

  setTimeout(()=>d.remove(),800);
}


async function spiritStrike(){

  if(busy || enemyHP<=0)return;

  busy=true;
  buttons(false);
  clearStates();

  message("⚡ The warrior plants his back foot...");

  player.classList.add("attackStrike");

  await wait(250);

  message("⚡ His shoulder pulls back and his fist charges...");

  const glow=document.getElementById("handGlow");

  glow.style.left="140px";
  glow.style.top="200px";
  glow.style.opacity="1";

  await wait(280);

  message("⚡ SPIRIT STRIKE!");

  glow.style.opacity="0";

  const projectile=document.createElement("div");
  projectile.className="projectile";
  projectile.style.left="165px";
  projectile.style.top="220px";

  const trail=document.createElement("div");
  trail.className="projectileTrail";
  trail.style.left="70px";
  trail.style.top="230px";

  arena.appendChild(trail);
  arena.appendChild(projectile);

  await wait(500);

  projectile.remove();
  trail.remove();

  const damage=22;

  enemyHP-=damage;

  updateHP();
  damageText(damage);
  impact();

  await wait(450);

  clearStates();

  if(enemyHP<=0){
    winLevel();
    return;
  }

  await enemyTurn();
}


async function shieldOfFate(){

  if(busy || enemyHP<=0)return;

  busy=true;
  buttons(false);
  clearStates();

  message("🛡️ The warrior lowers his stance...");

  player.classList.add("attackShield");

  await wait(300);

  message("🛡️ He swings his arm across his body...");

  await wait(250);

  message("🛡️ SHIELD OF FATE!");

  const s=document.createElement("div");
  s.className="shield";

  arena.appendChild(s);

  shieldActive=true;

  await wait(800);

  s.remove();

  clearStates();

  await enemyTurn();
}


async function wordOfTruth(){

  if(busy || enemyHP<=0)return;

  busy=true;
  buttons(false);
  clearStates();

  message("✋ The warrior raises both arms...");

  player.classList.add("attackTruth");

  await wait(350);

  message("✋ His hands draw together...");

  const glow=document.getElementById("handGlow");

  glow.style.left="120px";
  glow.style.top="165px";
  glow.style.opacity="1";

  await wait(250);

  message("✋ WORD OF TRUTH!");

  glow.style.opacity="0";

  const beam=document.createElement("div");
  beam.className="beam";

  arena.appendChild(beam);

  await wait(600);

  beam.remove();

  const damage=30;

  enemyHP-=damage;

  updateHP();
  damageText(damage);
  impact();

  await wait(400);

  clearStates();

  if(enemyHP<=0){
    winLevel();
    return;
  }

  await enemyTurn();
}


async function lightBurst(){

  if(
    busy ||
    enemyHP<=0 ||
    !specialUnlocked
  )return;

  busy=true;
  buttons(false);
  clearStates();

  message("☀️ The warrior crouches and gathers power...");

  player.classList.add("attackBurst");

  await wait(420);

  message("☀️ His arms rise as the armor floods with light...");

  const glow=document.getElementById("handGlow");

  glow.style.left="125px";
  glow.style.top="135px";
  glow.style.width="65px";
  glow.style.height="65px";
  glow.style.opacity="1";

  await wait(350);

  message("☀️ LIGHT BURST!");

  glow.style.opacity="0";

  const ring=document.createElement("div");
  ring.className="ring";

  const beam=document.createElement("div");
  beam.className="bigBeam";

  arena.appendChild(ring);
  arena.appendChild(beam);

  await wait(750);

  ring.remove();
  beam.remove();

  const damage=50;

  enemyHP-=damage;

  updateHP();

  damageText(damage);
  impact();

  const flash=document.createElement("div");
  flash.className="flash";

  arena.appendChild(flash);

  setTimeout(()=>flash.remove(),300);

  await wait(450);

  glow.style.width="48px";
  glow.style.height="48px";

  clearStates();

  if(enemyHP<=0){
    winLevel();
    return;
  }

  await enemyTurn();
}


async function enemyTurn(){

  if(enemyHP<=0)return;

  await wait(400);

  message("👹 The enemy shifts its weight...");

  enemy.classList.add("enemyAttack");

  await wait(300);

  message("👹 The Shadow Demon pulls its arm back...");

  await wait(300);

  message("👹 The Shadow Demon attacks!");

  await wait(250);

  if(shieldActive){

    shieldActive=false;

    const s=document.createElement("div");
    s.className="shield";

    arena.appendChild(s);

    message("🛡️ SHIELD OF FATE BLOCKED THE ATTACK!");

    impact();

    await wait(550);

    s.remove();

  }else{

    const damage=8+Math.floor(Math.random()*9);

    playerHP-=damage;

    updateHP();

    damageText(damage);
    impact();

    message(
      "💥 The attack hits! "+
      damage+
      " spiritual power lost."
    );

    await wait(500);
  }

  turnsSurvived++;

  clearStates();

  if(turnsSurvived>=3 && !specialUnlocked){

    specialUnlocked=true;

    message(
      "🔥 SPIRITUAL POWER SURGE! LIGHT BURST UNLOCKED!"
    );

    await wait(900);
  }

  if(playerHP<=0){

    message(
      "The warrior has fallen. Refresh the page to try again."
    );

    buttons(false);

    return;
  }

  busy=false;
  buttons(true);
}


function winLevel(){

  message("✨ The enemy has been defeated!");

  buttons(false);

  setTimeout(nextLevel,1200);
}


function nextLevel(){

  level++;

  if(level>3){

    levelText.textContent="VICTORY";

    enemyName.textContent="DEFEATED";

    message(
      "🏆 VICTORY! The Shadow Colossus has been defeated!"
    );

    return;
  }

  enemyHP=100+(level-1)*20;
  playerHP=100;

  turnsSurvived=0;
  specialUnlocked=false;
  shieldActive=false;

  updateHP();

  if(level===2){

    levelText.textContent="LEVEL 2 — DARK ANGEL";
    enemyName.textContent="DARK ANGEL";

    message(
      "🌑 A Dark Angel descends into the arena..."
    );

    verse.textContent=
      "“The LORD is my rock, and my fortress, and my deliverer.” — Psalm 18:2";

  }else{

    levelText.textContent="LEVEL 3 — SHADOW COLOSSUS";
    enemyName.textContent="SHADOW COLOSSUS";

    enemy.style.transform="scale(1.18)";

    message(
      "👹 THE SHADOW COLOSSUS AWAKENS!"
    );

    verse.textContent=
      "“Greater is he that is in you, than he that is in the world.” — 1 John 4:4";
  }

  busy=false;

  buttons(true);
}


strikeBtn.addEventListener(
  "click",
  spiritStrike
);

shieldBtn.addEventListener(
  "click",
  shieldOfFate
);

truthBtn.addEventListener(
  "click",
  wordOfTruth
);

burstBtn.addEventListener(
  "click",
  lightBurst
);

updateHP();
buttons(true);

</script>

</body>
</html>
