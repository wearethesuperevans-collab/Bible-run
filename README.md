<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
<title>Shadowbound</title>

<style>
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{margin:0;background:#02030a;color:white;font-family:Arial,sans-serif;min-height:100%;overflow-x:hidden}
button{font:inherit;border:0;color:white;cursor:pointer;touch-action:manipulation}
.hidden{display:none!important}

/* ================= MENU ================= */

.screen{
 min-height:100vh;display:flex;align-items:center;justify-content:center;
 padding:18px;background:
 radial-gradient(circle at 50% 20%,#18245c 0,#050713 55%,#010208 100%);
}

.panel{
 width:min(650px,100%);padding:30px;border-radius:28px;
 background:linear-gradient(145deg,#121d42,#050711);
 border:1px solid #526eff;
 box-shadow:0 0 60px #315cff55,inset 0 0 40px #1d347755;
 text-align:center;
}

.title{
 font-size:clamp(40px,10vw,76px);letter-spacing:5px;margin:0;
 background:linear-gradient(#fff,#78aaff,#fff);
 -webkit-background-clip:text;color:transparent;
 text-shadow:0 0 30px #467bff;
}

.subtitle{color:#aabaff;margin:8px 0 28px;letter-spacing:3px}

.saveGrid{display:grid;gap:12px}
.save{
 padding:16px;border-radius:15px;background:#080e20;
 border:1px solid #344b91;text-align:left;
}
.saveName{font-size:18px;font-weight:bold}
.saveInfo{font-size:13px;color:#91a1cb;margin:5px 0 10px}

.menuBtn,.createBtn{
 padding:13px 20px;border-radius:13px;
 background:linear-gradient(135deg,#527aff,#1939c4);
 box-shadow:0 7px 20px #0009;
 font-weight:bold;
}

.delete{background:#8d2436;margin-left:6px}

/* ================= GAME ================= */

#game{min-height:100vh;padding:7px}

.top{
 width:min(1280px,100%);margin:auto;
 display:flex;justify-content:space-between;align-items:center;
 padding:7px 10px;
}

.level{font-weight:bold;font-size:20px}
.power{color:#ffe35b;text-shadow:0 0 12px #ffcf36}

.arena{
 position:relative;width:min(1280px,100%);
 height:min(720px,76vh);min-height:470px;margin:auto;
 overflow:hidden;border-radius:26px;
 border:1px solid #405b9e;
 background:
 radial-gradient(circle at 50% 34%,#253a82 0,#111a40 28%,#050817 66%,#02030a 100%);
 box-shadow:0 0 80px #183b9a55,inset 0 0 100px #000;
}

/* cinematic background */

.arena:before{
 content:"";position:absolute;inset:0;pointer-events:none;
 background-image:
 radial-gradient(circle,#fff 1px,transparent 1.5px),
 radial-gradient(circle,#7da0ff 1px,transparent 1.5px),
 radial-gradient(circle,#fff 1px,transparent 1.5px);
 background-size:73px 73px,121px 121px,193px 193px;
 opacity:.42;
 animation:stars 18s linear infinite;
}

@keyframes stars{
 from{background-position:0 0,30px 20px,70px 80px}
 to{background-position:73px 73px,151px 141px,263px 180px}
}

.horizon{
 position:absolute;left:0;right:0;bottom:31%;
 height:2px;background:#6f91ff;
 box-shadow:0 0 25px #5277ff;opacity:.65;
}

.floor{
 position:absolute;left:-10%;right:-10%;bottom:-18%;height:53%;
 transform:perspective(550px) rotateX(61deg);
 transform-origin:bottom;
 background:
 linear-gradient(#3b58a0 1px,transparent 1px),
 linear-gradient(90deg,#3b58a0 1px,transparent 1px);
 background-size:65px 45px;
 opacity:.38;
}

.ambient{
 position:absolute;left:50%;top:52%;width:50%;height:25%;
 transform:translate(-50%,-50%);
 background:#497bff18;filter:blur(35px);pointer-events:none;
}

/* ================= HEALTH ================= */

.health{
 position:absolute;top:17px;width:32%;min-width:175px;z-index:200;
}

.playerHealth{left:2.5%}
.enemyHealth{right:2.5%;text-align:right}

.name{font-size:16px;font-weight:bold;text-shadow:0 2px 8px #000}
.bar{
 height:19px;border-radius:20px;background:#050711;
 border:2px solid #65729a;overflow:hidden;margin-top:4px;
}
.fill{height:100%;transition:width .35s cubic-bezier(.2,.8,.2,1)}
.gold{
 background:linear-gradient(90deg,#9b6100,#ffd52e,#fff3a1,#d08a00);
 box-shadow:0 0 22px #ffd62e;
}
.red{
 background:linear-gradient(90deg,#680014,#e51e40,#ff7181);
 box-shadow:0 0 22px #ff173e;
}
.hp{font-size:11px;color:#b9c4e4}

.status{
 position:absolute;top:19px;left:50%;transform:translateX(-50%);
 z-index:210;padding:7px 16px;border-radius:30px;
 background:#02040ccc;border:1px solid #526aa7;
 font-size:12px;white-space:nowrap;
}

/* ================= FIGHTERS ================= */

.fighter{
 position:absolute;bottom:84px;width:250px;height:340px;
 z-index:100;pointer-events:none;
}

#player{
 left:5%;
}

#enemy{
 right:5%;
}

/* Never let the enemy cross to the player's side */
#enemy{transform:none}

/* ================= PLAYER ================= */

.playerAura{
 position:absolute;left:20px;top:75px;width:210px;height:210px;
 border-radius:50%;background:#4285ff20;filter:blur(25px);
 animation:aura 2s infinite;
}

@keyframes aura{
 50%{transform:scale(1.17);opacity:.55}
}

.head{
 position:absolute;left:87px;top:0;width:76px;height:82px;
 border-radius:47%;background:linear-gradient(145deg,#ffd4b4,#a9634e);
 border:3px solid #633c38;z-index:5;
}

.hair{
 position:absolute;left:-4px;top:-5px;width:80px;height:37px;
 border-radius:50% 50% 35% 35%;background:#161922;
}

.eye{
 position:absolute;top:38px;width:7px;height:7px;border-radius:50%;background:#111
}
.eye1{left:20px}.eye2{right:20px}

.mouth{
 position:absolute;left:27px;top:61px;width:20px;height:5px;
 border-bottom:2px solid #522b2b;
}

.neck{
 position:absolute;left:107px;top:74px;width:36px;height:24px;
 background:#a7654f;
}

.chest{
 position:absolute;left:56px;top:86px;width:138px;height:139px;
 border-radius:37px 37px 22px 22px;
 background:linear-gradient(145deg,#6685ff,#293ba5,#10174a);
 border:3px solid #b8c7ff;
 box-shadow:inset 0 0 30px #aec0ff44,0 0 22px #416eff55;
}

.core{
 position:absolute;left:52px;top:43px;width:34px;height:34px;border-radius:50%;
 background:white;
 box-shadow:0 0 14px white,0 0 30px #72c0ff,0 0 60px #3378ff;
 animation:core 1.2s infinite;
}
@keyframes core{50%{transform:scale(1.13)}}

.shoulder{
 position:absolute;top:89px;width:56px;height:54px;border-radius:50%;
 background:linear-gradient(145deg,#9eb1ff,#26399d);
 border:3px solid #b9c8ff;
}
.shoulder1{left:24px}.shoulder2{right:24px}

.arm{
 position:absolute;top:128px;width:35px;height:104px;border-radius:20px;
 background:linear-gradient(#536dd4,#111b4e);
 border:3px solid #8298ff;
}
.arm1{left:24px;transform:rotate(8deg)}
.arm2{right:24px;transform:rotate(-8deg)}

.leg{
 position:absolute;top:218px;width:47px;height:93px;border-radius:14px;
 background:linear-gradient(#384eae,#10152e);
 border:3px solid #7186ef;
}
.leg1{left:78px}.leg2{right:78px}

.boot{
 position:absolute;top:301px;width:60px;height:25px;border-radius:15px;
 background:#080b18;border:2px solid #748aff;
}
.boot1{left:66px}.boot2{right:66px}

/* ================= BOSS SHARED ================= */

.boss{
 position:absolute;inset:0;
}

/* ================= LEVEL 1 ================= */

.l1head{
 position:absolute;left:73px;top:28px;width:105px;height:94px;
 border-radius:48% 48% 38% 38%;
 background:linear-gradient(145deg,#512866,#08060d);
 border:3px solid #a052c4;
 box-shadow:0 0 35px #8b36b055;
}

.horn{
 position:absolute;top:-49px;width:38px;height:61px;
 background:linear-gradient(145deg,#9254ad,#160b1f);
 border:3px solid #a95ac7;
 clip-path:polygon(50% 0,100% 100%,0 100%);
}
.horn1{left:4px;transform:rotate(-17deg)}
.horn2{right:4px;transform:rotate(17deg)}

.redEye{
 position:absolute;top:45px;width:26px;height:12px;border-radius:50%;
 background:#ff173c;box-shadow:0 0 22px #ff1740;
}
.redEye1{left:18px}.redEye2{right:18px}

.demonBody{
 position:absolute;left:51px;top:117px;width:150px;height:134px;
 border-radius:42px 42px 20px 20px;
 background:linear-gradient(145deg,#4b245c,#0e0714);
 border:3px solid #793d91;
 box-shadow:inset 0 0 28px #b74bd033;
}

.demonCore{
 position:absolute;left:54px;top:43px;width:42px;height:42px;border-radius:50%;
 background:#ff163e;
 box-shadow:0 0 20px #ff163e,0 0 55px #a0002d;
 animation:demonCore 1s infinite;
}
@keyframes demonCore{50%{transform:scale(1.16)}}

.demonArm{
 position:absolute;top:142px;width:48px;height:112px;border-radius:24px;
 background:#1e1029;border:3px solid #753c8e;
}
.demonArm1{left:20px;transform:rotate(13deg)}
.demonArm2{right:20px;transform:rotate(-13deg)}

.demonLeg{
 position:absolute;top:242px;width:51px;height:82px;border-radius:15px;
 background:#130a1b;border:3px solid #633172;
}
.demonLeg1{left:65px}.demonLeg2{right:65px}

/* ================= LEVEL 2 ================= */

.wing{
 position:absolute;top:48px;width:132px;height:205px;
 background:linear-gradient(145deg,#e4eaff,#65729b 48%,#121625);
 border:3px solid #b8c7ff;
 clip-path:polygon(50% 0,75% 15%,100% 34%,76% 39%,100% 60%,66% 57%,83% 84%,49% 72%,50% 100%,30% 70%,0 83%,21% 56%,0 59%,25% 38%,0 34%,32% 17%);
 filter:drop-shadow(0 0 15px #849cff66);
}
.wing1{left:-14px;transform:rotate(-16deg)}
.wing2{right:-14px;transform:scaleX(-1) rotate(-16deg)}

.halo{
 position:absolute;left:73px;top:4px;width:105px;height:105px;
 border:7px solid #ffe66b;border-radius:50%;
 box-shadow:0 0 25px #ffe66b,0 0 55px #ffc928;
 animation:halo 2s infinite;
}
@keyframes halo{50%{transform:rotate(180deg) scale(1.05)}}

.angelHead{
 position:absolute;left:86px;top:32px;width:78px;height:82px;
 border-radius:50%;background:linear-gradient(145deg,#dfe4ef,#555d75);
 border:3px solid #c3d0f2;z-index:4;
}
.visor{
 position:absolute;left:10px;top:31px;width:54px;height:18px;
 border-radius:5px;background:#0c1120;border:2px solid #8298ff;
 box-shadow:0 0 15px #6480ff;
}

.angelBody{
 position:absolute;left:58px;top:107px;width:134px;height:143px;
 border-radius:31px;background:linear-gradient(145deg,#c4cee2,#374059,#111625);
 border:3px solid #d2dcff;
 box-shadow:inset 0 0 35px #dbe5ff44;
}
.angelCore{
 position:absolute;left:48px;top:45px;width:38px;height:38px;border-radius:50%;
 background:white;box-shadow:0 0 20px white,0 0 60px #9eafff;
 animation:core 1.1s infinite;
}

.angelArm{
 position:absolute;top:139px;width:39px;height:108px;border-radius:20px;
 background:#39435c;border:3px solid #8c9abd;
}
.angelArm1{left:30px;transform:rotate(8deg)}
.angelArm2{right:30px;transform:rotate(-8deg)}

.angelLeg{
 position:absolute;top:244px;width:46px;height:82px;border-radius:13px;
 background:#202638;border:3px solid #68789d;
}
.angelLeg1{left:73px}.angelLeg2{right:73px}

/* ================= LEVEL 3 ================= */

.colWing{
 position:absolute;top:8px;width:175px;height:245px;
 background:linear-gradient(145deg,#292d49,#070912);
 border:4px solid #59618d;
 clip-path:polygon(50% 0,72% 14%,100% 9%,78% 34%,100% 31%,70% 53%,91% 66%,58% 63%,68% 92%,45% 70%,34% 100%,30% 65%,0 77%,25% 51%,0 48%,27% 30%,3% 25%,32% 14%);
 box-shadow:0 0 30px #252b55;
}
.colWing1{left:-34px;transform:rotate(-12deg)}
.colWing2{right:-34px;transform:scaleX(-1) rotate(-12deg)}

.colHead{
 position:absolute;left:64px;top:38px;width:125px;height:108px;
 border-radius:45% 45% 34% 34%;
 background:linear-gradient(145deg,#2c304b,#06070d);
 border:4px solid #606992;z-index:5;
}

.colHorn{
 position:absolute;top:-62px;width:45px;height:77px;
 background:#11131f;border:4px solid #59628b;
 clip-path:polygon(50% 0,100% 100%,0 100%);
}
.colHorn1{left:3px;transform:rotate(-16deg)}
.colHorn2{right:3px;transform:rotate(16deg)}

.colEye{
 position:absolute;top:53px;width:33px;height:14px;border-radius:50%;
 background:#ff143e;box-shadow:0 0 25px #ff143e;
}
.colEye1{left:21px}.colEye2{right:21px}

.colBody{
 position:absolute;left:35px;top:140px;width:184px;height:184px;
 border-radius:50px 50px 26px 26px;
 background:linear-gradient(145deg,#363b56,#090b14 65%);
 border:4px solid #5d668f;
 box-shadow:inset 0 0 40px #6c78aa44,0 0 30px #11152e;
}
.plate{
 position:absolute;left:25px;top:21px;width:126px;height:86px;
 border:3px solid #737da9;border-radius:25px;background:#141725;
}
.colCore{
 position:absolute;left:62px;top:38px;width:54px;height:54px;border-radius:50%;
 background:#ff153d;
 box-shadow:0 0 25px #ff153d,0 0 70px #ae002d;
 animation:demonCore .8s infinite;
}

.colArm{
 position:absolute;top:174px;width:61px;height:151px;border-radius:30px;
 background:linear-gradient(#272c42,#090b14);border:4px solid #59628a;
}
.colArm1{left:-2px;transform:rotate(8deg)}
.colArm2{right:-2px;transform:rotate(-8deg)}

.colLeg{
 position:absolute;top:311px;width:63px;height:91px;border-radius:16px;
 background:#10121d;border:4px solid #50597e;
}
.colLeg1{left:51px}.colLeg2{right:51px}

/* ================= ATTACK EFFECTS ================= */

.fx{
 position:absolute;z-index:500;pointer-events:none;
}

.projectile{
 width:30px;height:30px;border-radius:50%;background:#fff;
 box-shadow:0 0 15px #fff,0 0 35px #6cc5ff,0 0 70px #327aff;
}

.projectile:after{
 content:"";position:absolute;width:100px;height:9px;right:15px;top:10px;
 background:linear-gradient(90deg,transparent,#69bdff,#fff);
 filter:blur(4px);
}

.beam{
 left:2%;right:2%;top:44%;height:42px;border-radius:50%;
 background:linear-gradient(90deg,#fff,#83c9ff,#fff);
 box-shadow:0 0 25px #fff,0 0 65px #55aaff,0 0 120px #3477ff;
 transform-origin:left center;
 animation:beam .55s ease-out;
}

.superBeam{
 left:-10%;right:-10%;top:35%;height:110px;border-radius:50%;
 background:#fff;
 box-shadow:0 0 35px #fff,0 0 90px #63baff,0 0 170px #2d6fff;
 animation:superbeam .8s ease-out;
}

@keyframes beam{
 from{transform:scaleX(.01);opacity:0}
 to{transform:scaleX(1);opacity:1}
}
@keyframes superbeam{
 from{transform:scaleX(.01);opacity:0}
 to{transform:scaleX(1);opacity:1}
}

.shield{
 left:1%;top:25%;width:305px;height:305px;border-radius:50%;
 border:6px solid #64caff;
 background:#48aaff0b;
 box-shadow:0 0 30px #63caff,inset 0 0 55px #3d9cff44;
 animation:shield .7s ease-out;
}
@keyframes shield{
 from{transform:scale(.35);opacity:0}
 55%{transform:scale(1);opacity:1}
 to{transform:scale(1.08);opacity:.4}
}

.impact{
 width:25px;height:25px;border-radius:50%;
 border:4px solid white;
 box-shadow:0 0 20px white,0 0 55px #52aaff;
 animation:impact .5s ease-out forwards;
}
@keyframes impact{
 from{transform:scale(.2);opacity:1}
 to{transform:scale(5);opacity:0}
}

/* hit shakes */

.hit{
 animation:hit .42s ease;
}
@keyframes hit{
 20%{transform:translateX(18px)}
 40%{transform:translateX(-18px)}
 60%{transform:translateX(13px)}
 80%{transform:translateX(-7px)}
}

.playerDash{
 animation:playerDash .55s cubic-bezier(.2,.8,.2,1);
}
@keyframes playerDash{
 45%{transform:translateX(155px) scale(1.06)}
}

.enemyDash{
 animation:enemyDash .55s cubic-bezier(.2,.8,.2,1);
}
@keyframes enemyDash{
 45%{transform:translateX(-155px) scale(1.06)}
}

/* ================= CONTROLS ================= */

.controls{
 width:min(1280px,100%);margin:10px auto;
 display:grid;grid-template-columns:repeat(4,1fr);gap:10px;
 position:relative;z-index:900;
}

.controls button{
 min-height:64px;border-radius:14px;
 border:2px solid #4669ec;
 background:linear-gradient(145deg,#1b2e6d,#070e29);
 box-shadow:0 7px 20px #0009,inset 0 0 18px #567cff22;
 font-weight:bold;
 transition:.12s;
}
.controls button:active{transform:translateY(3px) scale(.97)}
.controls button:disabled{opacity:.35}
.special{border-color:#ffe05a!important;color:#ffe66d}

/* ================= LOG ================= */

.log{
 width:min(1280px,100%);margin:auto;min-height:48px;max-height:95px;
 overflow-y:auto;padding:9px 13px;border-radius:12px;
 background:#050914;border:1px solid #2f4277;color:#bac8ec;
 font-size:13px;
}

/* ================= OVERLAY ================= */

.overlay{
 position:fixed;inset:0;z-index:2000;background:#000c;
 display:flex;align-items:center;justify-content:center;padding:20px;
}

.overlayBox{
 width:min(560px,100%);padding:32px;text-align:center;
 border-radius:25px;background:linear-gradient(145deg,#121d42,#050711);
 border:2px solid #5d7cff;
 box-shadow:0 0 70px #315cff77;
}

.overlayBox h1{font-size:42px;margin:0 0 10px}

/* ================= MOBILE ================= */

@media(max-width:700px){

 .arena{height:57vh;min-height:415px}

 .fighter{
   transform:scale(.66);
   transform-origin:bottom center;
 }

 #player{left:-28px}
 #enemy{right:-28px}

 .health{width:43%;min-width:0}
 .status{top:64px;font-size:10px}

 .controls{grid-template-columns:repeat(2,1fr)}
 .controls button{min-height:60px;font-size:12px;padding:7px}

 .log{font-size:12px}

}

/* Very small screens */
@media(max-width:430px){
 .fighter{transform:scale(.57)}
 #player{left:-42px}
 #enemy{right:-42px}
 .arena{min-height:390px}
}
</style>
</head>

<body>

<!-- ================= SAVE ================= -->

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


<!-- ================= CREATE ================= -->

<div id="customScreen" class="screen hidden">
<div class="panel">

<h2>Create Your Warrior</h2>

<input id="nameInput" placeholder="Warrior name"
 maxlength="20"
 style="width:100%;padding:13px;margin:8px 0;border-radius:10px">

<select id="genderInput"
 style="width:100%;padding:13px;margin:8px 0;border-radius:10px">
<option>Male</option>
<option>Female</option>
</select>

<label>Armor Color</label>
<input id="armorInput" type="color" value="#315cff">

<label>Hair / Helmet Color</label>
<input id="helmetInput" type="color" value="#171822">

<br><br>

<button class="createBtn" onclick="createCharacter()">
BEGIN JOURNEY
</button>

</div>
</div>


<!-- ================= GAME ================= -->

<div id="game" class="hidden">

<div class="top">
<div class="level">LEVEL <span id="level">1</span></div>
<div class="power">SPIRITUAL POWER: <span id="power">0</span></div>
</div>


<div class="arena" id="arena">

<div class="ambient"></div>
<div class="horizon"></div>
<div class="floor"></div>


<!-- PLAYER HEALTH -->

<div class="health playerHealth">
<div class="name" id="playerName">Warrior</div>
<div class="bar">
<div id="playerBar" class="fill gold" style="width:100%"></div>
</div>
<div class="hp" id="playerHP">100 / 100</div>
</div>


<!-- ENEMY HEALTH -->

<div class="health enemyHealth">
<div class="name" id="enemyName">Shadow Demon</div>
<div class="bar">
<div id="enemyBar" class="fill red" style="width:100%"></div>
</div>
<div class="hp" id="enemyHP">100 / 100</div>
</div>


<div class="status" id="status">YOUR TURN</div>


<!-- PLAYER -->

<div id="player" class="fighter">

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


<!-- ENEMY -->

<div id="enemy" class="fighter">

<div id="boss"></div>

</div>

</div>


<!-- CONTROLS -->

<div class="controls" id="controls">

<button onclick="attack('strike')">
✨<br>SPIRIT STRIKE
</button>

<button onclick="attack('shield')">
🛡<br>SHIELD OF FATE
</button>

<button onclick="attack('truth')">
☀<br>WORD OF TRUTH
</button>

<button id="burst" class="special"
 onclick="attack('burst')" disabled>
⚡<br>LIGHT BURST
</button>

</div>


<div class="log" id="log">
Your journey begins...
</div>

</div>


<!-- ================= OVERLAY ================= -->

<div id="overlay" class="overlay hidden">
<div class="overlayBox">
<h1 id="overlayTitle"></h1>
<p id="overlayText"></p>
<button class="menuBtn" onclick="overlayContinue()">CONTINUE</button>
</div>
</div>


<script>

/* =========================================================
   DATA
========================================================= */

const SAVE_KEY="ShadowboundMaximumEdition";

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
   HELPERS
========================================================= */

function esc(x){
 return String(x||"")
 .replaceAll("&","&amp;")
 .replaceAll("<","&lt;")
 .replaceAll(">","&gt;")
 .replaceAll('"',"&quot;")
 .replaceAll("'","&#039;");
}

function save(){
 localStorage.setItem(SAVE_KEY,JSON.stringify(saves));
}

function gameSave(){
 if(slot!==null){
  saves[slot]=JSON.parse(JSON.stringify(state));
  save();
 }
}


/* =========================================================
   SAVES
========================================================= */

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
   <button class="menuBtn" onclick="load(${i})">
   CONTINUE
   </button>
   <button class="delete" onclick="del(${i})">
   DELETE
   </button>
   `;

  }else{

   box.innerHTML=`
   <div class="saveName">EMPTY SAVE ${i+1}</div>
   <button class="menuBtn" onclick="newSave(${i})">
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
  if(i<0){alert("All save slots are full.");return}
 }

 slot=i;

 document.getElementById("saveScreen")
 .classList.add("hidden");

 document.getElementById("customScreen")
 .classList.remove("hidden");
}

function load(i){

 slot=i;

 state=JSON.parse(
  JSON.stringify(saves[i])
 );

 document.getElementById("saveScreen")
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
 document.getElementById("nameInput").value.trim()
 ||"Warrior";

 state.gender=
 document.getElementById("genderInput").value;

 state.armor=
 document.getElementById("armorInput").value;

 state.helmet=
 document.getElementById("helmetInput").value;

 state.level=1;
 state.power=0;
 state.hp=100;
 state.turns=0;
 state.spirit=0;
 state.special=false;

 gameSave();

 document.getElementById("customScreen")
 .classList.add("hidden");

 start();
}


/* =========================================================
   START
========================================================= */

function start(){

 document.getElementById("game")
 .classList.remove("hidden");

 busy=false;
 shield=false;

 loadLevel();

 applyPlayer();

 update();

 log(
 levels[0].verse+" — "+
 levels[0].text
 );
}


/* =========================================================
   LOAD LEVEL
========================================================= */

function loadLevel(){

 const l=levels[state.level-1];

 enemy.name=l.name;
 enemy.max=l.hp;
 enemy.hp=l.hp;

 state.hp=100+(state.level-1)*35;
 state.turns=0;
 state.spirit=0;
 state.special=false;

 busy=false;
 shield=false;

 buildBoss();
 update();
}


/* =========================================================
   BOSS GRAPHICS
========================================================= */

function buildBoss(){

 const b=document.getElementById("boss");

 b.className="boss";

 if(state.level===1){

  b.classList.add("level1");

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

  b.classList.add("level2");

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

  b.classList.add("level3");

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
   PLAYER CUSTOMIZATION
========================================================= */

function applyPlayer(){

 document.querySelector(".chest").style.background=
 `linear-gradient(145deg,
 ${state.armor},
 #293ca7,
 #10174a)`;

 document.querySelector(".hair")
 .style.background=state.helmet;

 document.getElementById("playerName")
 .textContent=state.name;
}


/* =========================================================
   UI
========================================================= */

function update(){

 const max=100+(state.level-1)*35;

 document.getElementById("level")
 .textContent=state.level;

 document.getElementById("power")
 .textContent=state.power;

 document.getElementById("playerName")
 .textContent=state.name;

 document.getElementById("enemyName")
 .textContent=enemy.name;

 document.getElementById("playerBar")
 .style.width=Math.max(0,state.hp/max*100)+"%";

 document.getElementById("enemyBar")
 .style.width=Math.max(0,enemy.hp/enemy.max*100)+"%";

 document.getElementById("playerHP")
 .textContent=`${Math.max(0,state.hp)} / ${max}`;

 document.getElementById("enemyHP")
 .textContent=`${Math.max(0,enemy.hp)} / ${enemy.max}`;

 document.getElementById("burst").disabled=
 !state.special||busy;

 document.getElementById("status")
 .textContent=busy?"ENEMY TURN...":"YOUR TURN";
}


/* =========================================================
   LOG
========================================================= */

function log(x){

 const l=document.getElementById("log");

 l.innerHTML+=`<div>${esc(x)}</div>`;
 l.scrollTop=l.scrollHeight;
}


/* =========================================================
   COMBAT
========================================================= */

function attack(type){

 if(busy)return;

 if(type==="burst"&&!state.special)return;

 busy=true;
 update();

 if(type==="strike")strike();
 if(type==="shield")shieldAttack();
 if(type==="truth")truth();
 if(type==="burst")burst();
}


/* ================= STRIKE ================= */

function strike(){

 log("✨ SPIRIT STRIKE!");

 const p=document.getElementById("player");

 p.classList.add("playerDash");

 setTimeout(()=>{

  p.classList.remove("playerDash");

  projectile();

  enemy.hp=Math.max(
   0,
   enemy.hp-(20+state.level*5)
  );

  state.spirit+=12;

  impact();

  enemyHit();
  update();

 },300);

 finish(850);
}


/* ================= SHIELD ================= */

function shieldAttack(){

 log("🛡 SHIELD OF FATE!");

 shield=true;
 state.spirit+=20;

 makeShield();

 update();

 finish(750);
}


/* ================= TRUTH ================= */

function truth(){

 log("☀ WORD OF TRUTH!");

 makeBeam();

 enemy.hp=Math.max(
  0,
  enemy.hp-(32+state.level*6)
 );

 state.spirit+=24;

 impact();
 enemyHit();

 update();

 finish(900);
}


/* ================= BURST ================= */

function burst(){

 log("⚡ LIGHT BURST!");

 makeSuperBeam();

 enemy.hp=Math.max(
  0,
  enemy.hp-(100+state.level*25)
 );

 state.spirit=0;
 state.special=false;

 impact();
 enemyHit();

 update();

 finish(1150);
}


/* =========================================================
   FINISH PLAYER MOVE
========================================================= */

function finish(ms){

 setTimeout(()=>{

  if(enemy.hp<=0){
   defeated();
  }else{
   enemyTurn();
  }

 },ms);
}


/* =========================================================
   ENEMY TURN
========================================================= */

function enemyTurn(){

 document.getElementById("status")
 .textContent="ENEMY TURN...";

 const e=document.getElementById("enemy");

 if(shield){

  log("🛡 Shield of Fate blocked the attack!");

  shield=false;

  makeShield();

  setTimeout(endEnemyTurn,700);

  return;
 }

 log(enemy.name+" attacks!");

 e.classList.add("enemyDash");

 enemyEffect();

 setTimeout(()=>{

  e.classList.remove("enemyDash");

  state.hp=Math.max(
   0,
   state.hp-(12+state.level*5)
  );

  playerHit();
  update();

 },320);

 setTimeout(()=>{

  if(state.hp<=0){
   defeatedPlayer();
  }else{
   endEnemyTurn();
  }

 },850);
}


/* =========================================================
   CRITICAL BUTTON FIX
========================================================= */

function endEnemyTurn(){

 state.turns++;

 if(state.turns>=3){

  state.special=true;

  log("⚡ Your spiritual power is fully charged!");

 }

 gameSave();

 shield=false;

 busy=false;

 /*
  Explicitly restore every button.
 */
 document.querySelectorAll("#controls button")
 .forEach(b=>{
  b.style.pointerEvents="auto";
  b.style.opacity="1";
 });

 document.getElementById("burst").disabled=
 !state.special;

 document.getElementById("controls")
 .style.pointerEvents="auto";

 update();

 log("YOUR TURN — choose an attack.");
}


/* =========================================================
   EFFECTS
========================================================= */

function projectile(){

 const a=document.getElementById("arena");

 const x=document.createElement("div");

 x.className="fx projectile";

 x.style.left="25%";
 x.style.top="49%";

 a.appendChild(x);

 x.animate([
  {transform:"translateX(0) scale(.3)",opacity:0},
  {transform:"translateX(250px) scale(1)",opacity:1},
  {transform:"translateX(540px) scale(.15)",opacity:0}
 ],{
  duration:620,
  easing:"cubic-bezier(.2,.8,.2,1)"
 }).onfinish=()=>x.remove();
}


function makeBeam(){

 const a=document.getElementById("arena");

 const x=document.createElement("div");

 x.className="fx beam";

 a.appendChild(x);

 setTimeout(()=>x.remove(),650);
}


function makeSuperBeam(){

 const a=document.getElementById("arena");

 const x=document.createElement("div");

 x.className="fx superBeam";

 a.appendChild(x);

 setTimeout(()=>x.remove(),900);
}


function makeShield(){

 const a=document.getElementById("arena");

 const x=document.createElement("div");

 x.className="fx shield";

 a.appendChild(x);

 setTimeout(()=>x.remove(),850);
}


function impact(){

 const a=document.getElementById("arena");

 const x=document.createElement("div");

 x.className="fx impact";

 x.style.left="73%";
 x.style.top="48%";

 a.appendChild(x);

 setTimeout(()=>x.remove(),550);
}


/* =========================================================
   BOSS-SPECIFIC ATTACKS
========================================================= */

function enemyEffect(){

 const a=document.getElementById("arena");

 const x=document.createElement("div");

 x.className="fx";

 if(state.level===1){

  x.style.width="34px";
  x.style.height="34px";
  x.style.borderRadius="50%";
  x.style.background="#ff1744";
  x.style.boxShadow="0 0 25px #ff1744,0 0 70px #9d0030";
  x.style.left="73%";
  x.style.top="50%";

  a.appendChild(x);

  x.animate([
   {transform:"translateX(0) scale(.4)",opacity:0},
   {transform:"translateX(-390px) scale(1)",opacity:1},
   {transform:"translateX(-470px) scale(.2)",opacity:0}
  ],{duration:570}).onfinish=()=>x.remove();

 }

 else if(state.level===2){

  x.className="fx beam";
  x.style.background="linear-gradient(90deg,#fff,#b8c4ff,#fff)";
  x.style.boxShadow="0 0 30px #fff,0 0 80px #899cff";

  a.appendChild(x);
  setTimeout(()=>x.remove(),700);

 }

 else{

  x.className="fx superBeam";
  x.style.background="#ff173f";
  x.style.boxShadow="0 0 40px #ff173f,0 0 110px #a5002d";

  a.appendChild(x);
  setTimeout(()=>x.remove(),850);
 }
}


/* =========================================================
   HIT
========================================================= */

function enemyHit(){

 const e=document.getElementById("enemy");

 e.classList.add("hit");

 setTimeout(()=>e.classList.remove("hit"),450);
}

function playerHit(){

 const p=document.getElementById("player");

 p.classList.add("hit");

 setTimeout(()=>p.classList.remove("hit"),450);
}


/* =========================================================
   DEFEATED
========================================================= */

function defeated(){

 busy=false;

 state.power+=100*state.level;

 gameSave();

 if(state.level===3){

  show(
   "VICTORY!",
   "The Shadow Colossus has fallen. You completed Shadowbound."
  );

 }else{

  show(
   "BOSS DEFEATED!",
   `${enemy.name} has been defeated.`
  );
 }
}


function defeatedPlayer(){

 busy=false;

 state.hp=100+(state.level-1)*35;
 state.turns=0;
 state.spirit=0;
 state.special=false;

 gameSave();

 show(
  "DEFEATED",
  "The battle is over for now. Rise and try again."
 );
}


/* =========================================================
   OVERLAY
========================================================= */

function show(title,text){

 document.getElementById("overlayTitle")
 .textContent=title;

 document.getElementById("overlayText")
 .textContent=text;

 document.getElementById("overlay")
 .classList.remove("hidden");
}


function overlayContinue(){

 document.getElementById("overlay")
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
  return;
 }

 loadLevel();
}


/* =========================================================
   AUTO SAVE
========================================================= */

setInterval(()=>{

 if(!document.getElementById("game")
 .classList.contains("hidden")){

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
