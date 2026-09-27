<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
<title>Spiritual Power: Shadowbound</title>

<style>
*{box-sizing:border-box}
html,body{
 margin:0;
 min-height:100%;
 background:#02030a;
 color:white;
 font-family:Arial,sans-serif;
 overflow-x:hidden;
}
button{font:inherit}
.hidden{display:none!important}

/* ================= MENU ================= */

.screen{
 min-height:100vh;
 display:flex;
 justify-content:center;
 align-items:center;
 padding:20px;
 background:
 radial-gradient(circle at 50% 20%,#172a70,#060914 55%,#010208);
}

.panel{
 width:min(650px,100%);
 padding:30px;
 border-radius:28px;
 background:linear-gradient(145deg,#111b3c,#050711);
 border:1px solid #5272e9;
 box-shadow:0 0 70px #315cff55;
 text-align:center;
}

.title{
 font-size:clamp(38px,10vw,72px);
 letter-spacing:5px;
 margin:0;
 background:linear-gradient(#fff,#79aaff,#fff);
 -webkit-background-clip:text;
 color:transparent;
}

.subtitle{
 margin:8px 0 28px;
 color:#aebcff;
 letter-spacing:4px;
}

.saveGrid{
 display:grid;
 gap:12px;
}

.save{
 padding:16px;
 border-radius:15px;
 background:#080d1e;
 border:1px solid #344b91;
 text-align:left;
}

.saveName{
 font-size:18px;
 font-weight:bold;
}

.saveInfo{
 color:#91a1cb;
 font-size:13px;
 margin:5px 0 10px;
}

.menuBtn,.createBtn{
 padding:13px 20px;
 border:0;
 border-radius:13px;
 color:white;
 font-weight:bold;
 background:linear-gradient(135deg,#527aff,#1939c4);
 box-shadow:0 7px 20px #0009;
}

.delete{
 background:#8d2436;
 border:0;
 color:white;
 padding:11px;
 border-radius:10px;
 margin-left:6px;
}

/* ================= GAME ================= */

#game{
 min-height:100vh;
 padding:7px;
 background:#02030a;
}

.top{
 width:min(1300px,100%);
 margin:auto;
 display:flex;
 justify-content:space-between;
 padding:8px 10px;
}

.level{
 font-weight:bold;
 font-size:20px;
}

.power{
 color:#ffe35b;
 text-shadow:0 0 12px #ffcf36;
}

.arena{
 position:relative;
 width:min(1300px,100%);
 height:690px;
 margin:auto;
 overflow:hidden;
 border-radius:25px;
 border:1px solid #435b9e;
 background:
 radial-gradient(circle at 50% 34%,#263d8d,#111a40 30%,#050817 70%,#02030a);
 box-shadow:0 0 90px #183b9a55,inset 0 0 100px #000;
}

/* stars */

.arena:before{
 content:"";
 position:absolute;
 inset:0;
 pointer-events:none;
 background-image:
 radial-gradient(circle,#fff 1px,transparent 1.5px),
 radial-gradient(circle,#779cff 1px,transparent 1.5px),
 radial-gradient(circle,#fff 1px,transparent 1.5px);
 background-size:75px 75px,130px 130px,190px 190px;
 opacity:.4;
 animation:stars 20s linear infinite;
}

@keyframes stars{
 to{
  background-position:75px 75px,130px 130px,190px 190px;
 }
}

.horizon{
 position:absolute;
 left:0;
 right:0;
 bottom:32%;
 height:2px;
 background:#7897ff;
 box-shadow:0 0 30px #5075ff;
}

.floor{
 position:absolute;
 left:-10%;
 right:-10%;
 bottom:-20%;
 height:55%;
 transform:perspective(550px) rotateX(60deg);
 transform-origin:bottom;
 background:
 linear-gradient(#38539a 1px,transparent 1px),
 linear-gradient(90deg,#38539a 1px,transparent 1px);
 background-size:65px 45px;
 opacity:.35;
}

.ambient{
 position:absolute;
 left:50%;
 top:55%;
 width:55%;
 height:30%;
 transform:translate(-50%,-50%);
 background:#487bff1b;
 filter:blur(35px);
}

/* ================= HEALTH ================= */

.health{
 position:absolute;
 top:18px;
 width:32%;
 min-width:175px;
 z-index:100;
}

.playerHealth{left:2.5%}
.enemyHealth{right:2.5%;text-align:right}

.name{
 font-size:16px;
 font-weight:bold;
 text-shadow:0 2px 8px #000;
}

.bar{
 height:19px;
 border-radius:20px;
 background:#050711;
 border:2px solid #68769c;
 overflow:hidden;
 margin-top:4px;
}

.fill{
 height:100%;
 transition:width .35s;
}

.gold{
 background:linear-gradient(90deg,#986000,#ffd52e,#fff2a1,#ce8500);
 box-shadow:0 0 22px #ffd62e;
}

.red{
 background:linear-gradient(90deg,#680014,#e51e40,#ff7181);
 box-shadow:0 0 22px #ff173e;
}

.hp{
 font-size:11px;
 color:#bbc6e6;
}

.status{
 position:absolute;
 top:20px;
 left:50%;
 transform:translateX(-50%);
 z-index:110;
 padding:7px 17px;
 border-radius:30px;
 background:#02040dcc;
 border:1px solid #526aa7;
 font-size:12px;
 white-space:nowrap;
}

/* =========================================================
   FIGHTER CONTAINERS
   IMPORTANT: position never changes during animations.
   Only the inner model moves.
========================================================= */

.fighter{
 position:absolute;
 bottom:75px;
 width:270px;
 height:370px;
 z-index:80;
 pointer-events:none;
}

#player{
 left:4%;
}

#enemy{
 right:4%;
}

.model{
 position:absolute;
 inset:0;
 transform-origin:50% 100%;
}

/* ================= PLAYER AURA ================= */

.playerAura{
 position:absolute;
 left:25px;
 top:70px;
 width:220px;
 height:220px;
 border-radius:50%;
 background:#3e82ff20;
 filter:blur(25px);
 animation:aura 2s infinite;
}

@keyframes aura{
 50%{
  transform:scale(1.15);
  opacity:.55;
 }
}

/* =========================================================
   PLAYER BODY
========================================================= */

.head{
 position:absolute;
 left:97px;
 top:2px;
 width:76px;
 height:82px;
 border-radius:47%;
 background:linear-gradient(145deg,#ffd4b4,#a9634e);
 border:3px solid #633c38;
 z-index:5;
}

.hair{
 position:absolute;
 left:-4px;
 top:-5px;
 width:80px;
 height:37px;
 border-radius:50% 50% 35% 35%;
 background:#171822;
}

.eye{
 position:absolute;
 top:38px;
 width:7px;
 height:7px;
 border-radius:50%;
 background:#111;
}

.eye1{left:20px}
.eye2{right:20px}

.mouth{
 position:absolute;
 left:27px;
 top:61px;
 width:20px;
 height:5px;
 border-bottom:2px solid #522b2b;
}

.neck{
 position:absolute;
 left:117px;
 top:74px;
 width:36px;
 height:24px;
 background:#a7654f;
}

.chest{
 position:absolute;
 left:64px;
 top:86px;
 width:142px;
 height:142px;
 border-radius:37px 37px 22px 22px;
 background:linear-gradient(145deg,#5278ff,#293ba5,#10174a);
 border:3px solid #b8c7ff;
 box-shadow:inset 0 0 30px #aec0ff44,0 0 22px #416eff55;
}

.core{
 position:absolute;
 left:53px;
 top:44px;
 width:36px;
 height:36px;
 border-radius:50%;
 background:white;
 box-shadow:0 0 15px white,0 0 35px #72c0ff,0 0 65px #3378ff;
 animation:corePulse 1.1s infinite;
}

@keyframes corePulse{
 50%{transform:scale(1.13)}
}

.shoulder{
 position:absolute;
 top:89px;
 width:58px;
 height:56px;
 border-radius:50%;
 background:linear-gradient(145deg,#9eb1ff,#26399d);
 border:3px solid #b9c8ff;
}

.shoulder1{left:29px}
.shoulder2{right:29px}

.arm{
 position:absolute;
 top:130px;
 width:37px;
 height:108px;
 border-radius:20px;
 background:linear-gradient(#536dd4,#111b4e);
 border:3px solid #8298ff;
}

.arm1{left:28px}
.arm2{right:28px}

.leg{
 position:absolute;
 top:222px;
 width:48px;
 height:96px;
 border-radius:14px;
 background:linear-gradient(#384eae,#10152e);
 border:3px solid #7186ef;
}

.leg1{left:85px}
.leg2{right:85px}

.boot{
 position:absolute;
 top:307px;
 width:62px;
 height:26px;
 border-radius:15px;
 background:#080b18;
 border:2px solid #748aff;
}

.boot1{left:72px}
.boot2{right:72px}

/* =========================================================
   REAL ATTACK CHOREOGRAPHY
========================================================= */

/* player preparation */

.attackPrepare{
 animation:attackPrepare .42s ease-in-out;
}

@keyframes attackPrepare{
 0%{transform:scale(1) translateX(0)}
 45%{transform:scale(.94) translateX(-18px) rotate(-3deg)}
 100%{transform:scale(1) translateX(0)}
}

/* punch / strike */

.strikeMove{
 animation:strikeMove .72s cubic-bezier(.2,.8,.2,1);
}

@keyframes strikeMove{
 0%{
  transform:translateX(0) rotate(0) scale(1);
 }
 22%{
  transform:translateX(-25px) rotate(-4deg) scale(.96);
 }
 55%{
  transform:translateX(100px) rotate(2deg) scale(1.05);
 }
 72%{
  transform:translateX(125px) rotate(0) scale(1.03);
 }
 100%{
  transform:translateX(0) rotate(0) scale(1);
 }
}

/* shield stance */

.shieldMove{
 animation:shieldMove .7s ease-in-out;
}

@keyframes shieldMove{
 0%{transform:translateY(0) rotate(0)}
 30%{transform:translateY(10px) rotate(-4deg)}
 60%{transform:translateY(-4px) rotate(2deg) scale(1.05)}
 100%{transform:translateY(0) rotate(0)}
}

/* truth casting */

.truthMove{
 animation:truthMove 1s cubic-bezier(.2,.8,.2,1);
}

@keyframes truthMove{
 0%{
  transform:translateY(0) scale(1);
 }
 25%{
  transform:translateY(-18px) scale(.95);
 }
 48%{
  transform:translateY(-5px) scale(1.04);
 }
 70%{
  transform:translateX(30px) scale(1.06);
 }
 100%{
  transform:translateX(0) scale(1);
 }
}

/* ultimate */

.burstMove{
 animation:burstMove 1.15s cubic-bezier(.15,.8,.2,1);
}

@keyframes burstMove{
 0%{
  transform:translateY(0) scale(1);
 }
 18%{
  transform:translateY(20px) scale(.88);
 }
 42%{
  transform:translateY(-22px) scale(1.1);
 }
 65%{
  transform:translateY(-8px) scale(1.18);
 }
 82%{
  transform:translateY(5px) scale(1.06);
 }
 100%{
  transform:translateY(0) scale(1);
 }
}

/* =========================================================
   ENEMY CHOREOGRAPHY
========================================================= */

.enemyPrepare{
 animation:enemyPrepare .45s ease;
}

@keyframes enemyPrepare{
 0%{transform:translateX(0)}
 50%{transform:translateX(20px) scale(.95)}
 100%{transform:translateX(0)}
}

.enemyAttack{
 animation:enemyAttack .75s cubic-bezier(.2,.8,.2,1);
}

@keyframes enemyAttack{
 0%{transform:translateX(0)}
 25%{transform:translateX(20px) scale(.95)}
 60%{transform:translateX(-110px) scale(1.07)}
 75%{transform:translateX(-130px) scale(1.04)}
 100%{transform:translateX(0)}
}

/* recoil */

.recoil{
 animation:recoil .4s ease;
}

@keyframes recoil{
 0%{transform:translateX(0)}
 30%{transform:translateX(22px)}
 60%{transform:translateX(-12px)}
 100%{transform:translateX(0)}
}

/* =========================================================
   BOSS LEVEL 1
========================================================= */

.l1head{
 position:absolute;
 left:78px;
 top:28px;
 width:110px;
 height:96px;
 border-radius:48% 48% 38% 38%;
 background:linear-gradient(145deg,#512866,#08060d);
 border:3px solid #a052c4;
 box-shadow:0 0 35px #8b36b055;
}

.horn{
 position:absolute;
 top:-49px;
 width:39px;
 height:62px;
 background:linear-gradient(145deg,#9254ad,#160b1f);
 border:3px solid #a95ac7;
 clip-path:polygon(50% 0,100% 100%,0 100%);
}

.horn1{left:4px;transform:rotate(-17deg)}
.horn2{right:4px;transform:rotate(17deg)}

.redEye{
 position:absolute;
 top:45px;
 width:27px;
 height:12px;
 border-radius:50%;
 background:#ff173c;
 box-shadow:0 0 22px #ff1740;
}

.redEye1{left:18px}
.redEye2{right:18px}

.demonBody{
 position:absolute;
 left:55px;
 top:120px;
 width:156px;
 height:139px;
 border-radius:42px 42px 20px 20px;
 background:linear-gradient(145deg,#4b245c,#0e0714);
 border:3px solid #793d91;
}

.demonCore{
 position:absolute;
 left:56px;
 top:46px;
 width:43px;
 height:43px;
 border-radius:50%;
 background:#ff163e;
 box-shadow:0 0 20px #ff163e,0 0 55px #a0002d;
 animation:corePulse .9s infinite;
}

.demonArm{
 position:absolute;
 top:143px;
 width:49px;
 height:112px;
 border-radius:24px;
 background:#1e1029;
 border:3px solid #753c8e;
}

.demonArm1{left:22px}
.demonArm2{right:22px}

.demonLeg{
 position:absolute;
 top:250px;
 width:52px;
 height:85px;
 border-radius:15px;
 background:#130a1b;
 border:3px solid #633172;
}

.demonLeg1{left:68px}
.demonLeg2{right:68px}

/* =========================================================
   LEVEL 2 ANGEL
========================================================= */

.wing{
 position:absolute;
 top:48px;
 width:140px;
 height:210px;
 background:linear-gradient(145deg,#e4eaff,#65729b 48%,#121625);
 border:3px solid #b8c7ff;
 clip-path:polygon(
  50% 0,75% 15%,100% 34%,76% 39%,
  100% 60%,66% 57%,83% 84%,49% 72%,
  50% 100%,30% 70%,0 83%,21% 56%,
  0 59%,25% 38%,0 34%,32% 17%
 );
}

.wing1{left:-20px}
.wing2{right:-20px;transform:scaleX(-1)}

.halo{
 position:absolute;
 left:77px;
 top:4px;
 width:110px;
 height:110px;
 border:7px solid #ffe66b;
 border-radius:50%;
 box-shadow:0 0 25px #ffe66b,0 0 55px #ffc928;
 animation:haloSpin 2s infinite linear;
}

@keyframes haloSpin{
 to{transform:rotate(360deg)}
}

.angelHead{
 position:absolute;
 left:95px;
 top:36px;
 width:80px;
 height:84px;
 border-radius:50%;
 background:linear-gradient(145deg,#dfe4ef,#555d75);
 border:3px solid #c3d0f2;
 z-index:4;
}

.visor{
 position:absolute;
 left:10px;
 top:31px;
 width:56px;
 height:18px;
 border-radius:5px;
 background:#0c1120;
 border:2px solid #8298ff;
 box-shadow:0 0 15px #6480ff;
}

.angelBody{
 position:absolute;
 left:65px;
 top:111px;
 width:140px;
 height:148px;
 border-radius:31px;
 background:linear-gradient(145deg,#c4cee2,#374059,#111625);
 border:3px solid #d2dcff;
}

.angelCore{
 position:absolute;
 left:50px;
 top:48px;
 width:39px;
 height:39px;
 border-radius:50%;
 background:white;
 box-shadow:0 0 20px white,0 0 60px #9eafff;
 animation:corePulse 1.1s infinite;
}

.angelArm{
 position:absolute;
 top:145px;
 width:40px;
 height:110px;
 border-radius:20px;
 background:#39435c;
 border:3px solid #8c9abd;
}

.angelArm1{left:34px}
.angelArm2{right:34px}

.angelLeg{
 position:absolute;
 top:254px;
 width:47px;
 height:85px;
 border-radius:13px;
 background:#202638;
 border:3px solid #68789d;
}

.angelLeg1{left:78px}
.angelLeg2{right:78px}

/* =========================================================
   LEVEL 3 COLOSSUS
========================================================= */

.colWing{
 position:absolute;
 top:8px;
 width:180px;
 height:250px;
 background:linear-gradient(145deg,#292d49,#070912);
 border:4px solid #59618d;
 clip-path:polygon(
  50% 0,72% 14%,100% 9%,78% 34%,100% 31%,
  70% 53%,91% 66%,58% 63%,68% 92%,45% 70%,
  34% 100%,30% 65%,0 77%,25% 51%,0 48%,
  27% 30%,3% 25%,32% 14%
 );
 box-shadow:0 0 30px #252b55;
}

.colWing1{left:-40px}
.colWing2{right:-40px;transform:scaleX(-1)}

.colHead{
 position:absolute;
 left:70px;
 top:40px;
 width:130px;
 height:112px;
 border-radius:45% 45% 34% 34%;
 background:linear-gradient(145deg,#2c304b,#06070d);
 border:4px solid #606992;
 z-index:5;
}

.colHorn{
 position:absolute;
 top:-62px;
 width:46px;
 height:78px;
 background:#11131f;
 border:4px solid #59628b;
 clip-path:polygon(50% 0,100% 100%,0 100%);
}

.colHorn1{left:3px}
.colHorn2{right:3px}

.colEye{
 position:absolute;
 top:55px;
 width:34px;
 height:14px;
 border-radius:50%;
 background:#ff143e;
 box-shadow:0 0 25px #ff143e;
}

.colEye1{left:22px}
.colEye2{right:22px}

.colBody{
 position:absolute;
 left:38px;
 top:145px;
 width:190px;
 height:190px;
 border-radius:50px 50px 26px 26px;
 background:linear-gradient(145deg,#363b56,#090b14 65%);
 border:4px solid #5d668f;
 box-shadow:inset 0 0 40px #6c78aa44;
}

.plate{
 position:absolute;
 left:26px;
 top:22px;
 width:132px;
 height:88px;
 border:3px solid #737da9;
 border-radius:25px;
 background:#141725;
}

.colCore{
 position:absolute;
 left:66px;
 top:40px;
 width:55px;
 height:55px;
 border-radius:50%;
 background:#ff153d;
 box-shadow:0 0 25px #ff153d,0 0 70px #ae002d;
 animation:corePulse .75s infinite;
}

.colArm{
 position:absolute;
 top:180px;
 width:62px;
 height:155px;
 border-radius:30px;
 background:linear-gradient(#272c42,#090b14);
 border:4px solid #59628a;
}

.colArm1{left:0}
.colArm2{right:0}

.colLeg{
 position:absolute;
 top:322px;
 width:64px;
 height:92px;
 border-radius:16px;
 background:#10121d;
 border:4px solid #50597e;
}

.colLeg1{left:54px}
.colLeg2{right:54px}

/* =========================================================
   ATTACK EFFECTS
========================================================= */

.fx{
 position:absolute;
 pointer-events:none;
 z-index:500;
}

.charge{
 left:50%;
 top:48%;
 width:45px;
 height:45px;
 transform:translate(-50%,-50%);
 border-radius:50%;
 background:white;
 box-shadow:
 0 0 15px white,
 0 0 35px #72c9ff,
 0 0 75px #317aff;
 animation:charge .65s ease-out forwards;
}

@keyframes charge{
 0%{transform:translate(-50%,-50%) scale(.2);opacity:0}
 45%{transform:translate(-50%,-50%) scale(1.3);opacity:1}
 100%{transform:translate(-50%,-50%) scale(.8);opacity:.8}
}

.projectile{
 width:32px;
 height:32px;
 border-radius:50%;
 background:#fff;
 box-shadow:
 0 0 15px #fff,
 0 0 35px #6cc5ff,
 0 0 70px #327aff;
}

.projectile:after{
 content:"";
 position:absolute;
 width:120px;
 height:10px;
 right:17px;
 top:11px;
 background:linear-gradient(90deg,transparent,#69bdff,#fff);
 filter:blur(4px);
}

.beam{
 left:3%;
 right:3%;
 top:45%;
 height:45px;
 border-radius:50%;
 background:linear-gradient(90deg,#fff,#83c9ff,#fff);
 box-shadow:
 0 0 25px #fff,
 0 0 65px #55aaff,
 0 0 120px #3477ff;
 transform-origin:left center;
 animation:beam .65s ease-out;
}

@keyframes beam{
 from{transform:scaleX(.01);opacity:0}
 to{transform:scaleX(1);opacity:1}
}

.superBeam{
 left:-10%;
 right:-10%;
 top:35%;
 height:115px;
 border-radius:50%;
 background:#fff;
 box-shadow:
 0 0 35px #fff,
 0 0 90px #63baff,
 0 0 170px #2d6fff;
 animation:superBeam .85s ease-out;
}

@keyframes superBeam{
 from{transform:scaleX(.01);opacity:0}
 to{transform:scaleX(1);opacity:1}
}

.shield{
 left:2%;
 top:27%;
 width:310px;
 height:310px;
 border-radius:50%;
 border:6px solid #64caff;
 background:#48aaff0c;
 box-shadow:
 0 0 30px #63caff,
 0 0 70px #3d9cff,
  inset 0 0 55px #3d9cff44;
 animation:shieldAppear .8s ease-out;
}

@keyframes shieldAppear{
 0%{transform:scale(.2);opacity:0}
 55%{transform:scale(1.03);opacity:1}
 100%{transform:scale(1.1);opacity:.35}
}

.impact{
 width:30px;
 height:30px;
 border-radius:50%;
 border:4px solid white;
 box-shadow:0 0 20px white,0 0 55px #52aaff;
 animation:impact .55s ease-out forwards;
}

@keyframes impact{
 from{transform:scale(.2);opacity:1}
 to{transform:scale(5);opacity:0}
}

.energyRing{
 left:50%;
 top:48%;
 width:100px;
 height:100px;
 border:5px solid white;
 border-radius:50%;
 transform:translate(-50%,-50%);
 box-shadow:0 0 30px #67c8ff;
 animation:ring .7s ease-out forwards;
}

@keyframes ring{
 from{transform:translate(-50%,-50%) scale(.2);opacity:1}
 to{transform:translate(-50%,-50%) scale(5);opacity:0}
}

/* =========================================================
   SCREEN IMPACT
========================================================= */

.screenFlash{
 position:absolute;
 inset:0;
 z-index:1000;
 pointer-events:none;
 background:white;
 animation:flash .3s ease-out forwards;
}

@keyframes flash{
 from{opacity:.85}
 to{opacity:0}
}

.cameraShake{
 animation:cameraShake .35s ease;
}

@keyframes cameraShake{
 0%,100%{transform:translate(0)}
 25%{transform:translate(7px,-4px)}
 50%{transform:translate(-8px,5px)}
 75%{transform:translate(5px,3px)}
}

/* =========================================================
   CONTROLS
========================================================= */

.controls{
 width:min(1300px,100%);
 margin:10px auto;
 display:grid;
 grid-template-columns:repeat(4,1fr);
 gap:10px;
}

.controls button{
 min-height:65px;
 border-radius:14px;
 border:2px solid #4669ec;
 background:linear-gradient(145deg,#1b2e6d,#070e29);
 color:white;
 box-shadow:0 7px 20px #0009;
 font-weight:bold;
}

.controls button:active{
 transform:translateY(3px) scale(.97);
}

.controls button:disabled{
 opacity:.35;
}

.special{
 border-color:#ffe05a!important;
 color:#ffe66d!important;
}

/* =========================================================
   LOG
========================================================= */

.log{
 width:min(1300px,100%);
 margin:auto;
 min-height:48px;
 max-height:95px;
 overflow-y:auto;
 padding:9px 13px;
 border-radius:12px;
 background:#050914;
 border:1px solid #2f4277;
 color:#bac8ec;
 font-size:13px;
}

/* =========================================================
   OVERLAY
========================================================= */

.overlay{
 position:fixed;
 inset:0;
 z-index:2000;
 background:#000d;
 display:flex;
 justify-content:center;
 align-items:center;
 padding:20px;
}

.overlayBox{
 width:min(560px,100%);
 padding:32px;
 text-align:center;
 border-radius:25px;
 background:linear-gradient(145deg,#121d42,#050711);
 border:2px solid #5d7cff;
 box-shadow:0 0 70px #315cff77;
}

.overlayBox h1{
 font-size:42px;
 margin:0 0 10px;
}

/* =========================================================
   MOBILE
========================================================= */

@media(max-width:700px){

 .arena{
  height:600px;
 }

 .fighter{
  transform:scale(.66);
  transform-origin:50% 100%;
 }

 #player{left:-35px}
 #enemy{right:-35px}

 .health{
  width:43%;
  min-width:0;
 }

 .status{
  top:63px;
  font-size:10px;
 }

 .controls{
  grid-template-columns:repeat(2,1fr);
 }

 .controls button{
  min-height:62px;
  font-size:12px;
 }

 .log{
  font-size:12px;
 }
}

@media(max-width:430px){

 .arena{
  height:560px;
 }

 .fighter{
  transform:scale(.57);
 }

 #player{left:-55px}
 #enemy{right:-55px}
}
</style>
</head>

<body>

<!-- =========================================================
 SAVE SCREEN
========================================================= -->

<div id="saveScreen" class="screen">
<div class="panel">

<h1 class="title">SHADOWBOUND</h1>
<div class="subtitle">SPIRITUAL POWER</div>

<div id="saveGrid" class="saveGrid"></div>

<br>

<button class="menuBtn" onclick="newSave()">
CREATE NEW SAVE
</button>

</div>
</div>


<!-- =========================================================
 CREATE SCREEN
========================================================= -->

<div id="customScreen" class="screen hidden">

<div class="panel">

<h2>Create Your Warrior</h2>

<input
 id="nameInput"
 placeholder="Warrior name"
 maxlength="20"
 style="width:100%;padding:13px;margin:8px 0;border-radius:10px"
>

<select
 id="genderInput"
 style="width:100%;padding:13px;margin:8px 0;border-radius:10px"
>
<option>Male</option>
<option>Female</option>
</select>

<p>Armor Color</p>

<input
 id="armorInput"
 type="color"
 value="#315cff"
>

<p>Helmet / Hair Color</p>

<input
 id="helmetInput"
 type="color"
 value="#171822"
>

<br><br>

<button class="createBtn" onclick="createCharacter()">
BEGIN JOURNEY
</button>

</div>
</div>


<!-- =========================================================
 GAME
========================================================= -->

<div id="game" class="hidden">

<div class="top">
<div class="level">
LEVEL <span id="level">1</span>
</div>

<div class="power">
SPIRITUAL POWER:
<span id="power">0</span>
</div>
</div>


<div class="arena" id="arena">

<div class="ambient"></div>
<div class="horizon"></div>
<div class="floor"></div>


<!-- PLAYER HEALTH -->

<div class="health playerHealth">

<div class="name" id="playerName">
Warrior
</div>

<div class="bar">
<div
 id="playerBar"
 class="fill gold"
 style="width:100%"
></div>
</div>

<div class="hp" id="playerHP">
100 / 100
</div>

</div>


<!-- ENEMY HEALTH -->

<div class="health enemyHealth">

<div class="name" id="enemyName">
Shadow Demon
</div>

<div class="bar">
<div
 id="enemyBar"
 class="fill red"
 style="width:100%"
></div>
</div>

<div class="hp" id="enemyHP">
100 / 100
</div>

</div>


<div class="status" id="status">
YOUR TURN
</div>


<!-- =========================================================
 PLAYER
========================================================= -->

<div id="player" class="fighter">

<div id="playerModel" class="model">

<div class="playerAura"></div>

<div class="head">
<div class="hair"></div>
<div class="eye eye1"></div>
<div class="eye eye2"></div>
<div class="mouth"></div>
</div>

<div class="neck"></div>

<div class="chest">
<div class="core"></div>
</div>

<div class="shoulder shoulder1"></div>
<div class="shoulder shoulder2"></div>

<div class="arm arm1"></div>
<div class="arm arm2"></div>

<div class="leg leg1"></div>
<div class="leg leg2"></div>

<div class="boot boot1"></div>
<div class="boot boot2"></div>

</div>
</div>


<!-- =========================================================
 ENEMY
========================================================= -->

<div id="enemy" class="fighter">

<div id="enemyModel" class="model">
<div id="boss"></div>
</div>

</div>

</div>


<!-- =========================================================
 CONTROLS
========================================================= -->

<div class="controls" id="controls">

<button onclick="attack('strike')">
✨<br>
SPIRIT STRIKE
</button>

<button onclick="attack('shield')">
🛡<br>
SHIELD OF FATE
</button>

<button onclick="attack('truth')">
☀<br>
WORD OF TRUTH
</button>

<button
 id="burst"
 class="special"
 onclick="attack('burst')"
 disabled
>
⚡<br>
LIGHT BURST
</button>

</div>


<div class="log" id="log">
Your journey begins...
</div>

</div>


<!-- =========================================================
 OVERLAY
========================================================= -->

<div id="overlay" class="overlay hidden">

<div class="overlayBox">

<h1 id="overlayTitle"></h1>

<p id="overlayText"></p>

<button
 class="menuBtn"
 onclick="overlayContinue()"
>
CONTINUE
</button>

</div>
</div>


<script>

/* =========================================================
 DATA
========================================================= */

const SAVE_KEY="ShadowboundMaximumChoreography";

let saves=JSON.parse(
 localStorage.getItem(SAVE_KEY)||"[]"
);

let slot=null;

let state={
 name:"Warrior",
 gender:"Male",
 armor:"#315cff",
 helmet:"#171822",
 level:1,
 power:0,
 hp:100,
 turns:0,
 spirit:0,
 special:false
};

let enemy={
 name:"",
 hp:0,
 max:0
};

let busy=false;
let shield=false;


/* =========================================================
 LEVELS
========================================================= */

const levels=[

 {
  name:"SHADOW DEMON",
  hp:100,
  verse:"Ephesians 6:11",
  text:"Put on the whole armour of God, that ye may be able to stand against the wiles of the devil."
 },

 {
  name:"DARK ANGEL",
  hp:220,
  verse:"Psalm 18:2",
  text:"The LORD is my rock, and my fortress, and my deliverer; my God, my strength, in whom I will trust."
 },

 {
  name:"SHADOW COLOSSUS",
  hp:420,
  verse:"1 John 4:4",
  text:"Greater is he that is in you, than he that is in the world."
 }

];


/* =========================================================
 SAVES
========================================================= */

function save(){
 localStorage.setItem(
  SAVE_KEY,
  JSON.stringify(saves)
 );
}

function gameSave(){

 if(slot!==null){
  saves[slot]=JSON.parse(
   JSON.stringify(state)
  );

  save();
 }
}

function showSaves(){

 const grid=document.getElementById("saveGrid");

 grid.innerHTML="";

 for(let i=0;i<3;i++){

  const s=saves[i];

  const box=document.createElement("div");

  box.className="save";

  if(s){

   box.innerHTML=`
    <div class="saveName">${esc(s.name)}</div>
    <div class="saveInfo">
     Level ${s.level} • Power ${s.power}
    </div>

    <button
     class="menuBtn"
     onclick="load(${i})"
    >
     CONTINUE
    </button>

    <button
     class="delete"
     onclick="del(${i})"
    >
     DELETE
    </button>
   `;

  }else{

   box.innerHTML=`
    <div class="saveName">
     EMPTY SAVE ${i+1}
    </div>

    <button
     class="menuBtn"
     onclick="newSave(${i})"
    >
     CREATE
    </button>
   `;
  }

  grid.appendChild(box);
 }
}

function newSave(i){

 if(i===undefined){

  i=saves.findIndex(x=>!x);

  if(i<0){
   alert("All save slots are full.");
   return;
  }
 }

 slot=i;

 document
 .getElementById("saveScreen")
 .classList.add("hidden");

 document
 .getElementById("customScreen")
 .classList.remove("hidden");
}

function load(i){

 slot=i;

 state=JSON.parse(
  JSON.stringify(saves[i])
 );

 document
 .getElementById("saveScreen")
 .classList.add("hidden");

 start();
}

function del(i){

 if(confirm("Delete this save?")){

  saves[i]=null;

  save();

  showSaves();
 }
}


/* =========================================================
 CREATE
========================================================= */

function createCharacter(){

 state.name=
 document.getElementById("nameInput")
 .value
 .trim()
 ||"Warrior";

 state.gender=
 document.getElementById("genderInput")
 .value;

 state.armor=
 document.getElementById("armorInput")
 .value;

 state.helmet=
 document.getElementById("helmetInput")
 .value;

 state.level=1;
 state.power=0;
 state.hp=100;
 state.turns=0;
 state.spirit=0;
 state.special=false;

 gameSave();

 document
 .getElementById("customScreen")
 .classList.add("hidden");

 start();
}


/* =========================================================
 START
========================================================= */

function start(){

 document
 .getElementById("game")
 .classList.remove("hidden");

 busy=false;
 shield=false;

 loadLevel();

 applyPlayer();

 update();

 log(
  levels[0].verse+
  " — "+
  levels[0].text
 );
}


/* =========================================================
 LEVEL
========================================================= */

function loadLevel(){

 const l=levels[state.level-1];

 enemy.name=l.name;
 enemy.max=l.hp;
 enemy.hp=l.hp;

 state.hp=
 100+
 ((state.level-1)*35);

 state.turns=0;
 state.spirit=0;
 state.special=false;

 busy=false;
 shield=false;

 buildBoss();

 update();
}


/* =========================================================
 BOSS BUILD
========================================================= */

function buildBoss(){

 const b=document.getElementById("boss");

 if(state.level===1){

  b.innerHTML=`

   <div class="l1head">

    <div class="horn horn1"></div>
    <div class="horn horn2"></div>

    <div class="redEye redEye1"></div>
    <div class="redEye redEye2"></div>

   </div>

   <div class="demonBody">
    <div class="demonCore"></div>
   </div>

   <div class="demonArm demonArm1"></div>
   <div class="demonArm demonArm2"></div>

   <div class="demonLeg demonLeg1"></div>
   <div class="demonLeg demonLeg2"></div>

  `;

 }

 else if(state.level===2){

  b.innerHTML=`

   <div class="wing wing1"></div>
   <div class="wing wing2"></div>

   <div class="halo"></div>

   <div class="angelHead">
    <div class="visor"></div>
   </div>

   <div class="angelBody">
    <div class="angelCore"></div>
   </div>

   <div class="angelArm angelArm1"></div>
   <div class="angelArm angelArm2"></div>

   <div class="angelLeg angelLeg1"></div>
   <div class="angelLeg angelLeg2"></div>

  `;

 }

 else{

  b.innerHTML=`

   <div class="colWing colWing1"></div>
   <div class="colWing colWing2"></div>

   <div class="colHead">

    <div class="colHorn colHorn1"></div>
    <div class="colHorn colHorn2"></div>

    <div class="colEye colEye1"></div>
    <div class="colEye colEye2"></div>

   </div>

   <div class="colBody">

    <div class="plate"></div>
    <div class="colCore"></div>

   </div>

   <div class="colArm colArm1"></div>
   <div class="colArm colArm2"></div>

   <div class="colLeg colLeg1"></div>
   <div class="colLeg colLeg2"></div>

  `;
 }
}


/* =========================================================
 PLAYER COLOR
========================================================= */

function applyPlayer(){

 document.querySelector(".chest").style.background=
 `
 linear-gradient(
  145deg,
  ${state.armor},
  #293ca7,
  #10174a
 )
 `;

 document
 .querySelector(".hair")
 .style.background=state.helmet;

 document
 .getElementById("playerName")
 .textContent=state.name;
}


/* =========================================================
 UI
========================================================= */

function update(){

 const max=
 100+
 ((state.level-1)*35);

 document.getElementById("level")
 .textContent=state.level;

 document.getElementById("power")
 .textContent=state.power;

 document.getElementById("playerName")
 .textContent=state.name;

 document.getElementById("enemyName")
 .textContent=enemy.name;

 document.getElementById("playerBar")
 .style.width=
 Math.max(0,state.hp/max*100)+"%";

 document.getElementById("enemyBar")
 .style.width=
 Math.max(0,enemy.hp/enemy.max*100)+"%";

 document.getElementById("playerHP")
 .textContent=
 `${Math.max(0,state.hp)} / ${max}`;

 document.getElementById("enemyHP")
 .textContent=
 `${Math.max(0,enemy.hp)} / ${enemy.max}`;

 document.getElementById("burst")
 .disabled=
 !state.special||busy;

 document.getElementById("status")
 .textContent=
 busy?"ENEMY TURN...":"YOUR TURN";
}


/* =========================================================
 LOG
========================================================= */

function esc(x){

 return String(x||"")
 .replaceAll("&","&amp;")
 .replaceAll("<","&lt;")
 .replaceAll(">","&gt;")
 .replaceAll('"',"&quot;")
 .replaceAll("'","&#039;");
}

function log(x){

 const l=
 document.getElementById("log");

 l.innerHTML+=
 `<div>${esc(x)}</div>`;

 l.scrollTop=l.scrollHeight;
}


/* =========================================================
 ATTACK START
========================================================= */

function attack(type){

 if(busy)return;

 if(
  type==="burst" &&
  !state.special
 )return;

 busy=true;

 update();

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

 log("✨ The warrior draws spiritual energy into his arm...");

 const model=
 document.getElementById("playerModel");

 model.classList.add("attackPrepare");

 setTimeout(()=>{

  createCharge();

 },150);

 setTimeout(()=>{

  model.classList.remove("attackPrepare");

  log("✨ SPIRIT STRIKE!");

  model.classList.add("strikeMove");

 },430);

 setTimeout(()=>{

  createProjectile();

 },700);

 setTimeout(()=>{

  model.classList.remove("strikeMove");

  damageEnemy(25+state.level*6);

 },900);

 setTimeout(()=>{

  finishAttack();

 },1100);
}


/* =========================================================
 SHIELD
========================================================= */

function shieldOfFate(){

 log("🛡 The warrior plants his feet and raises his hand...");

 const model=
 document.getElementById("playerModel");

 model.classList.add("shieldMove");

 setTimeout(()=>{

  shield=true;

  log("🛡 SHIELD OF FATE!");

  createShield();

  state.spirit+=20;

  update();

 },500);

 setTimeout(()=>{

  model.classList.remove("shieldMove");

  finishAttack();

 },950);
}


/* =========================================================
 WORD OF TRUTH
========================================================= */

function wordOfTruth(){

 log("☀ The warrior raises both hands toward the heavens...");

 const model=
 document.getElementById("playerModel");

 model.classList.add("truthMove");

 setTimeout(()=>{

  createCharge();

  log("☀ Light gathers around the warrior...");

 },300);

 setTimeout(()=>{

  log("☀ WORD OF TRUTH!");

  createBeam();

 },720);

 setTimeout(()=>{

  model.classList.remove("truthMove");

  damageEnemy(38+state.level*8);

 },950);

 setTimeout(()=>{

  finishAttack();

 },1150);
}


/* =========================================================
 LIGHT BURST
========================================================= */

function lightBurst(){

 log("⚡ The warrior lowers his stance...");

 const model=
 document.getElementById("playerModel");

 model.classList.add("burstMove");

 setTimeout(()=>{

  createCharge();

  createEnergyRing();

  log("⚡ Spiritual power is surging!");

 },300);

 setTimeout(()=>{

  log("⚡ LIGHT BURST!");

  createSuperBeam();

  flash();

 },780);

 setTimeout(()=>{

  model.classList.remove("burstMove");

  damageEnemy(
   105+
   state.level*28
  );

  state.spirit=0;
  state.special=false;

 },1050);

 setTimeout(()=>{

  finishAttack();

 },1350);
}


/* =========================================================
 DAMAGE
========================================================= */

function damageEnemy(amount){

 enemy.hp=
 Math.max(
  0,
  enemy.hp-amount
 );

 enemyRecoil();

 createImpact();

 update();
}


/* =========================================================
 FINISH
========================================================= */

function finishAttack(){

 if(enemy.hp<=0){

  defeated();

 }else{

  setTimeout(
   enemyTurn,
   300
  );
 }
}


/* =========================================================
 ENEMY TURN
========================================================= */

function enemyTurn(){

 document
 .getElementById("status")
 .textContent="ENEMY TURN...";

 const model=
 document.getElementById("enemyModel");

 log(
  enemy.name+
  " begins gathering power..."
 );

 model.classList.add("enemyPrepare");

 setTimeout(()=>{

  model.classList.remove("enemyPrepare");

  model.classList.add("enemyAttack");

  enemyAttackEffect();

 },420);

 setTimeout(()=>{

  model.classList.remove("enemyAttack");

  if(shield){

   log(
    "🛡 SHIELD OF FATE BLOCKED THE ATTACK!"
   );

   shield=false;

   createShield();

  }else{

   state.hp=
   Math.max(
    0,
    state.hp-
    (12+state.level*5)
   );

   playerRecoil();

   log(
    enemy.name+
    " struck the warrior."
   );
  }

  update();

 },850);

 setTimeout(()=>{

  if(state.hp<=0){

   defeatedPlayer();

  }else{

   endEnemyTurn();
  }

 },1150);
}


/* =========================================================
 TURN RESET
========================================================= */

function endEnemyTurn(){

 state.turns++;

 if(state.turns>=3){

  state.special=true;

  log(
   "⚡ LIGHT BURST IS READY!"
  );
 }

 gameSave();

 busy=false;

 document
 .getElementById("controls")
 .style.pointerEvents="auto";

 document
 .querySelectorAll("#controls button")
 .forEach(b=>{
  b.style.pointerEvents="auto";
 });

 update();

 log("YOUR TURN.");
}


/* =========================================================
 EFFECT CREATION
========================================================= */

function createCharge(){

 const arena=
 document.getElementById("arena");

 const x=
 document.createElement("div");

 x.className="fx charge";

 arena.appendChild(x);

 setTimeout(
  ()=>x.remove(),
  700
 );
}


function createProjectile(){

 const arena=
 document.getElementById("arena");

 const x=
 document.createElement("div");

 x.className="fx projectile";

 x.style.left="24%";
 x.style.top="49%";

 arena.appendChild(x);

 x.animate(
  [
   {
    transform:"translateX(0) scale(.25)",
    opacity:0
   },
   {
    transform:"translateX(220px) scale(1)",
    opacity:1
   },
   {
    transform:"translateX(590px) scale(.15)",
    opacity:0
   }
  ],
  {
   duration:700,
   easing:"cubic-bezier(.2,.8,.2,1)"
  }
 ).onfinish=
 ()=>x.remove();
}


function createShield(){

 const arena=
 document.getElementById("arena");

 const x=
 document.createElement("div");

 x.className="fx shield";

 arena.appendChild(x);

 setTimeout(
  ()=>x.remove(),
  900
 );
}


function createBeam(){

 const arena=
 document.getElementById("arena");

 const x=
 document.createElement("div");

 x.className="fx beam";

 arena.appendChild(x);

 setTimeout(
  ()=>x.remove(),
  750
 );
}


function createSuperBeam(){

 const arena=
 document.getElementById("arena");

 const x=
 document.createElement("div");

 x.className="fx superBeam";

 arena.appendChild(x);

 setTimeout(
  ()=>x.remove(),
  1000
 );
}


function createEnergyRing(){

 const arena=
 document.getElementById("arena");

 const x=
 document.createElement("div");

 x.className="fx energyRing";

 arena.appendChild(x);

 setTimeout(
  ()=>x.remove(),
  750
 );
}


function createImpact(){

 const arena=
 document.getElementById("arena");

 const x=
 document.createElement("div");

 x.className="fx impact";

 x.style.left="76%";
 x.style.top="49%";

 arena.appendChild(x);

 setTimeout(
  ()=>x.remove(),
  600
 );

 flash();
}


function flash(){

 const arena=
 document.getElementById("arena");

 const x=
 document.createElement("div");

 x.className="screenFlash";

 arena.appendChild(x);

 setTimeout(
  ()=>x.remove(),
  350
 );

 arena.classList.add("cameraShake");

 setTimeout(
  ()=>arena.classList.remove("cameraShake"),
  380
 );
}


/* =========================================================
 ENEMY ATTACK EFFECTS
========================================================= */

function enemyAttackEffect(){

 const arena=
 document.getElementById("arena");

 const x=
 document.createElement("div");

 x.className="fx";

 if(state.level===1){

  x.style.left="73%";
  x.style.top="49%";
  x.style.width="36px";
  x.style.height="36px";
  x.style.borderRadius="50%";
  x.style.background="#ff1744";

  x.style.boxShadow=
   "0 0 25px #ff1744,0 0 70px #9d0030";

  arena.appendChild(x);

  x.animate(
   [
    {
     transform:"translateX(0) scale(.3)",
     opacity:0
    },
    {
     transform:"translateX(-300px) scale(1)",
     opacity:1
    },
    {
     transform:"translateX(-520px) scale(.2)",
     opacity:0
    }
   ],
   {
    duration:650
   }
  ).onfinish=
  ()=>x.remove();

 }

 else if(state.level===2){

  x.className="fx beam";

  x.style.background=
   "linear-gradient(90deg,#fff,#b8c4ff,#fff)";

  x.style.boxShadow=
   "0 0 30px #fff,0 0 80px #899cff";

  arena.appendChild(x);

  setTimeout(
   ()=>x.remove(),
   750
  );

 }

 else{

  x.className="fx superBeam";

  x.style.background="#ff173f";

  x.style.boxShadow=
   "0 0 40px #ff173f,0 0 110px #a5002d";

  arena.appendChild(x);

  setTimeout(
   ()=>x.remove(),
   900
  );
 }
}


/* =========================================================
 RECOIL
========================================================= */

function enemyRecoil(){

 const model=
 document.getElementById("enemyModel");

 model.classList.add("recoil");

 setTimeout(
  ()=>model.classList.remove("recoil"),
  450
 );
}

function playerRecoil(){

 const model=
 document.getElementById("playerModel");

 model.classList.add("recoil");

 setTimeout(
  ()=>model.classList.remove("recoil"),
  450
 );
}


/* =========================================================
 VICTORY / DEFEAT
========================================================= */

function defeated(){

 busy=false;

 state.power+=
 100*state.level;

 gameSave();

 if(state.level===3){

  show(
   "VICTORY!",
   "The Shadow Colossus has fallen. You completed Shadowbound."
  );

 }else{

  show(
   "BOSS DEFEATED!",
   enemy.name+
   " has been defeated."
  );
 }
}

function defeatedPlayer(){

 busy=false;

 state.hp=
 100+
 ((state.level-1)*35);

 state.turns=0;
 state.spirit=0;
 state.special=false;

 gameSave();

 show(
  "DEFEATED",
  "The warrior has fallen. Rise and try again."
 );
}


/* =========================================================
 OVERLAY
========================================================= */

function show(title,text){

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

function overlayContinue(){

 document
 .getElementById("overlay")
 .classList.add("hidden");

 if(enemy.hp<=0){

  if(state.level<3){

   state.level++;

   loadLevel();

   log(
    `LEVEL ${state.level}: ${enemy.name}`
   );

  }else{

   state.level=1;
   state.power=0;

   loadLevel();
  }

  gameSave();

 }else{

  loadLevel();
 }
}


/* =========================================================
 AUTO SAVE
========================================================= */

setInterval(()=>{

 if(
  !document
  .getElementById("game")
  .classList.contains("hidden")
 ){

  gameSave();
 }

},5000);


/* =========================================================
 INITIALIZE
========================================================= */

showSaves();

</script>

</body>
</html>
