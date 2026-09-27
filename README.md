<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport"
      content="width=device-width, initial-scale=1.0, maximum-scale=1.0">

<title>Spiritual Power: Shadowbound</title>

<style>
* {
    box-sizing: border-box;
    -webkit-tap-highlight-color: transparent;
}

body {
    margin: 0;
    background: #050812;
    color: white;
    font-family: Arial, Helvetica, sans-serif;
    overflow-x: hidden;
}

button,
input,
select {
    font-family: inherit;
}

button {
    border: none;
    border-radius: 12px;
    padding: 13px 18px;
    font-weight: bold;
    cursor: pointer;
}

button:active {
    transform: scale(.96);
}

.screen {
    min-height: 100vh;
    display: none;
    align-items: center;
    justify-content: center;
    padding: 20px;
}

.screen.active {
    display: flex;
}

/* MAIN MENU */

.panel {
    width: min(900px, 96vw);
    background:
        linear-gradient(145deg, #171e34, #080c17);
    border: 2px solid #40527d;
    border-radius: 22px;
    padding: 25px;
    box-shadow: 0 0 45px rgba(0,0,0,.7);
}

.title {
    font-size: clamp(35px, 8vw, 65px);
    font-weight: 900;
    text-transform: uppercase;
    letter-spacing: 3px;
    text-align: center;
    margin: 5px 0;

    text-shadow:
        0 4px 0 #000,
        0 0 20px #526cff;
}

.subtitle {
    text-align: center;
    color: #b9c6e6;
}

.description {
    color: #dce4f7;
    line-height: 1.5;
}

.save-grid {
    display: grid;
    grid-template-columns:
        repeat(3, 1fr);
    gap: 15px;
}

.save-slot {
    background: #10172a;
    border: 2px solid #344567;
    border-radius: 15px;
    padding: 16px;
}

.save-slot:hover {
    border-color: #7189d0;
}

.save-slot h3 {
    margin-top: 0;
}

.save-buttons {
    display: flex;
    gap: 7px;
    flex-wrap: wrap;
}

.primary {
    background: #e7bd45;
    color: #171208;
}

.dark {
    background: #2d3d60;
    color: white;
}

.danger {
    background: #a82f42;
    color: white;
}

/* CHARACTER CREATION */

.creation {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
}

.preview {
    min-height: 300px;
    display: flex;
    align-items: center;
    justify-content: center;

    background:
        radial-gradient(circle, #28375c, #0a0d17);
    border-radius: 18px;
}

label {
    display: block;
    margin-top: 13px;
    margin-bottom: 5px;
    color: #bfcbe8;
}

input,
select {
    width: 100%;
    padding: 13px;
    background: #090e1b;
    border: 1px solid #4a5a7c;
    color: white;
    border-radius: 9px;
}

/* AVATAR */

.avatar {
    width: 130px;
    height: 210px;
    position: relative;
    filter:
        drop-shadow(0 0 15px #607cff);
}

.head {
    position: absolute;
    width: 60px;
    height: 60px;
    left: 35px;
    top: 0;

    background: #efbd91;
    border: 4px solid #151a2a;
    border-radius: 50%;
}

.body {
    position: absolute;
    width: 82px;
    height: 105px;
    left: 24px;
    top: 60px;

    background: #385ce0;
    border: 4px solid #151a2a;
    border-radius: 20px 20px 12px 12px;
}

.body::after {
    content: "✦";
    position: absolute;
    left: 27px;
    top: 28px;
    color: white;
    font-size: 30px;
}

.arm {
    position: absolute;
    width: 25px;
    height: 75px;
    top: 70px;

    background: #385ce0;
    border: 4px solid #151a2a;
    border-radius: 15px;
}

.arm.left {
    left: 1px;
    transform: rotate(12deg);
}

.arm.right {
    right: 1px;
    transform: rotate(-12deg);
}

.leg {
    position: absolute;
    width: 30px;
    height: 65px;
    top: 160px;

    background: #202b4b;
    border: 4px solid #151a2a;
}

.leg.left {
    left: 28px;
}

.leg.right {
    right: 28px;
}

/* GAME */

#game {
    align-items: stretch;
    padding: 0;
}

.game {
    min-height: 100vh;
    width: 100%;
    display: flex;
    flex-direction: column;
}

.topbar {
    display: flex;
    align-items: center;
    gap: 12px;

    padding: 10px;

    background: #080d1b;
    border-bottom: 2px solid #293958;
}

.player-info {
    min-width: 150px;
}

.meters {
    flex: 1;
    min-width: 180px;
}

.meter {
    height: 12px;
    background: #252c40;
    border-radius: 20px;
    overflow: hidden;
    margin: 4px 0 8px;
}

.meter-fill {
    height: 100%;
    width: 100%;
}

.hp {
    background: #e14e60;
}

.spirit {
    background: #e9bf45;
}

/* ARENA */

.arena {
    position: relative;
    flex: 1;
    min-height: 580px;
    overflow: hidden;

    background:
        radial-gradient(
            circle at 50% 35%,
            #27365d,
            #090d18 68%
        );
}

.stars {
    position: absolute;
    inset: 0;

    background-image:
        radial-gradient(#fff 1px, transparent 1px);

    background-size: 50px 50px;
    opacity: .15;
}

.ground {
    position: absolute;
    bottom: 0;
    width: 100%;
    height: 25%;

    background:
        linear-gradient(#151c2c, #06080e);

    border-top: 2px solid #3c4c6e;
}

/* CHARACTERS */

.battle-character {
    position: absolute;
    bottom: 16%;
    z-index: 3;
}

.player {
    left: 10%;
}

.enemy {
    right: 12%;
}

.character {
    width: 130px;
    height: 210px;
    position: relative;
}

.character .head {
    left: 35px;
}

.character .body {
    left: 24px;
}

.character .left {
    left: 1px;
}

.character .right {
    right: 1px;
}

.enemy .character {
    transform: scale(1.25);

    filter:
        drop-shadow(0 0 25px #6e4dff);
}

.enemy .head {
    background: #17151e;
}

.enemy .body {
    background: #28263d;
}

.enemy .arm,
.enemy .leg {
    background: #1c1b2b;
}

.enemy.boss .character {
    transform: scale(1.7);
}

/* NAME PLATES */

.nameplate {
    position: absolute;
    bottom: calc(16% + 220px);

    background: rgba(5,8,18,.85);

    padding: 7px 11px;
    border-radius: 8px;

    z-index: 5;

    font-weight: bold;
}

.player-name {
    left: 10%;
}

.enemy-name {
    right: 12%;
}

/* BATTLE UI */

.controls {
    background: #080d1b;
    border-top: 2px solid #293958;
    padding: 12px;
}

.verse {
    background: #161e34;
    border-left: 4px solid #e6bd45;

    padding: 10px;

    border-radius: 8px;

    margin-bottom: 8px;

    line-height: 1.4;
}

.verse-title {
    color: #f1ca56;
    font-weight: bold;
}

.log {
    height: 95px;

    overflow-y: auto;

    background: #050812;

    border-radius: 10px;

    padding: 8px;

    margin-bottom: 8px;

    font-size: 14px;
}

.actions {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
}

.action {
    flex: 1;
    min-width: 130px;

    background: #33476f;
    color: white;
}

.power-button {
    background: #8144c6;
}

.action:disabled {
    opacity: .35;
}

/* OVERLAY */

.overlay {
    position: absolute;
    inset: 0;

    background: rgba(3,5,12,.9);

    z-index: 20;

    display: none;

    align-items: center;
    justify-content: center;

    padding: 20px;
}

.overlay.show {
    display: flex;
}

.overlay-card {
    max-width: 650px;

    text-align: center;

    background: #11192c;

    border: 2px solid #50658e;

    border-radius: 20px;

    padding: 30px;
}

.level-up {
    font-size: 40px;
    color: #f1ca56;
    font-weight: 900;
}

/* MOBILE */

@media(max-width:700px) {

    .save-grid {
        grid-template-columns: 1fr;
    }

    .creation {
        grid-template-columns: 1fr;
    }

    .preview {
        min-height: 230px;
    }

    .arena {
        min-height: 450px;
    }

    .player {
        left: 3%;
    }

    .enemy {
        right: 3%;
    }

    .player-name {
        left: 3%;
    }

    .enemy-name {
        right: 3%;
    }

    .battle-character .character {
        transform: scale(.8);
    }

    .enemy .character {
        transform: scale(1.05);
    }

    .enemy.boss .character {
        transform: scale(1.3);
    }

    .nameplate {
        font-size: 12px;
    }

    .topbar {
        flex-wrap: wrap;
    }
}
</style>
</head>

<body>

<!-- =========================
     SAVE MENU
========================= -->

<section id="home" class="screen active">

<div class="panel">

<h1 class="title">
SPIRITUAL POWER
</h1>

<p class="subtitle">
SHADOWBOUND
</p>

<p class="description">
Level up your spiritual power, unlock new moves,
and stand against the forces of darkness.
</p>

<h2>Choose Your Save</h2>

<div id="saveSlots" class="save-grid"></div>

</div>

</section>


<!-- =========================
     CHARACTER CREATION
========================= -->

<section id="customize" class="screen">

<div class="panel">

<h2>Create Your Warrior</h2>

<div class="creation">

<div class="preview">

<div
    class="avatar"
    id="previewAvatar"
>

<div
    class="head"
    id="previewHead">
</div>

<div
    class="body"
    id="previewBody">
</div>

<div class="arm left"></div>
<div class="arm right"></div>

<div class="leg left"></div>
<div class="leg right"></div>

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

<option value="#a53d4e">
Crimson
</option>

<option value="#399b77">
Emerald
</option>

<option value="#8750b8">
Violet
</option>

<option value="#d18b2d">
Gold
</option>

</select>


<label>
Helmet / Hair
</label>

<select id="helmetInput">

<option value="#171b2c">
Dark
</option>

<option value="#e2d7c5">
Light
</option>

<option value="#6b3b22">
Brown
</option>

<option value="#314f87">
Blue
</option>

</select>

<br><br>

<button
    class="primary"
    onclick="createPlayer()"
>
BEGIN JOURNEY
</button>

<button
    class="dark"
    onclick="showScreen('home')"
>
BACK
</button>

</div>

</div>

</div>

</section>


<!-- =========================
     GAME
========================= -->

<section id="game" class="screen">

<div class="game">

<div class="topbar">

<div class="player-info">

<b id="playerDisplay">
Warrior
</b>

<div>
Level
<span id="levelDisplay">1</span>
</div>

<div>
Spiritual Power:
<span id="powerDisplay">0</span>
</div>

</div>


<div class="meters">

<div>
HP
</div>

<div class="meter">
<div
    id="hpMeter"
    class="meter-fill hp">
</div>
</div>


<div>
SPIRIT
</div>

<div class="meter">
<div
    id="spiritMeter"
    class="meter-fill spirit">
</div>
</div>

</div>


<button
    class="dark"
    onclick="saveAndExit()"
>
SAVE & EXIT
</button>

</div>


<div class="arena">

<div class="stars"></div>

<div class="ground"></div>


<!-- PLAYER -->

<div
    id="playerNamePlate"
    class="nameplate player-name">
</div>

<div class="battle-character player">

<div class="character">

<div
    class="head"
    id="playerHead">
</div>

<div
    class="body"
    id="playerBody">
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
    class="overlay"
>

<div
    id="overlayCard"
    class="overlay-card">
</div>

</div>

</div>


<!-- CONTROLS -->

<div class="controls">

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
    onclick="attack('strike')"
>
SPIRIT STRIKE
</button>


<button
    class="action"
    onclick="attack('shield')"
>
SHIELD OF FAITH
</button>


<button
    class="action"
    onclick="attack('word')"
>
WORD OF TRUTH
</button>


<button
    id="powerMove"
    class="action power-button"
    onclick="attack('special')"
>
POWER MOVE
</button>

</div>

</div>

</div>

</section>


<script>

/* ==========================================
   SAVE SYSTEM
========================================== */

const SAVE_KEY =
"spiritualPowerShadowboundSaves";

let saves =
JSON.parse(
    localStorage.getItem(SAVE_KEY)
) || [null, null, null];

let currentSlot = -1;

let player = null;

let enemy = null;

let battleLocked = false;


/* ==========================================
   LEVEL DATA
========================================== */

const levels = [

{
    name: "Shadow Demons",

    enemyHP: 90,

    requiredPower: 5,

    verse:
    "Ephesians 6:11 — " +
    "\"Put on the whole armour of God, " +
    "that ye may be able to stand against " +
    "the wiles of the devil.\"",

    special:
    "LIGHT BURST"
},

{
    name: "Dark Angel",

    enemyHP: 180,

    requiredPower: 12,

    verse:
    "Psalm 18:2 — " +
    "\"The LORD is my rock, and my fortress, " +
    "and my deliverer; my God, my strength, " +
    "in whom I will trust.\"",

    special:
    "HOLY BREAKER"
},

{
    name: "Shadow Colossus",

    enemyHP: 330,

    requiredPower: 25,

    verse:
    "1 John 4:4 — " +
    "\"Greater is he that is in you, " +
    "than he that is in the world.\"",

    special:
    "VICTORY ROAR"
}

];


/* ==========================================
   SCREEN SYSTEM
========================================== */

function showScreen(id) {

    document
        .querySelectorAll(".screen")
        .forEach(screen => {

            screen.classList.remove("active");

        });

    document
        .getElementById(id)
        .classList.add("active");
}


/* ==========================================
   SAVE MENU
========================================== */

function renderSaveSlots() {

    const container =
        document.getElementById("saveSlots");

    container.innerHTML = "";

    saves.forEach((save, index) => {

        const slot =
            document.createElement("div");

        slot.className = "save-slot";

        if (save) {

            slot.innerHTML = `

                <h3>
                    SAVE ${index + 1}
                </h3>

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
                        onclick="continueSave(${index})"
                    >
                        CONTINUE
                    </button>

                    <button
                        class="danger"
                        onclick="deleteSave(${index})"
                    >
                        DELETE
                    </button>

                </div>
            `;

        } else {

            slot.innerHTML = `

                <h3>
                    SAVE ${index + 1}
                </h3>

                <p>
                    Empty Save
                </p>

                <button
                    class="primary"
                    onclick="newSave(${index})"
                >
                    NEW GAME
                </button>
            `;
        }

        container.appendChild(slot);

    });
}


/* ==========================================
   ESCAPE HTML
========================================== */

function escapeHTML(text) {

    return String(text)
        .replace(/[&<>"']/g, char => {

            const map = {

                "&": "&amp;",
                "<": "&lt;",
                ">": "&gt;",
                '"': "&quot;",
                "'": "&#039;"

            };

            return map[char];

        });

}


/* ==========================================
   NEW GAME
========================================== */

function newSave(index) {

    currentSlot = index;

    document
        .getElementById("playerNameInput")
        .value = "";

    showScreen("customize");
}


/* ==========================================
   CONTINUE SAVE
========================================== */

function continueSave(index) {

    currentSlot = index;

    player =
        JSON.parse(
            JSON.stringify(saves[index])
        );

    startGame();
}


/* ==========================================
   DELETE SAVE
========================================== */

function deleteSave(index) {

    const confirmDelete =
        confirm(
            "Delete Save " +
            (index + 1) +
            "?\n\nThis cannot be undone."
        );

    if (!confirmDelete)
        return;

    saves[index] = null;

    localStorage.setItem(
        SAVE_KEY,
        JSON.stringify(saves)
    );

    renderSaveSlots();
}


/* ==========================================
   CHARACTER CREATION
========================================== */

function createPlayer() {

    const name =
        document
            .getElementById("playerNameInput")
            .value
            .trim();

    player = {

        name:
            name || "Warrior",

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

        level: 1,

        power: 0,

        hp: 100,

        spirit: 0,

        defense: 0

    };

    saveGame();

    startGame();
}


/* ==========================================
   SAVE GAME
========================================== */

function saveGame() {

    if (currentSlot < 0)
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
   SAVE AND EXIT
========================================== */

function saveAndExit() {

    saveGame();

    renderSaveSlots();

    showScreen("home");
}


/* ==========================================
   START GAME
========================================== */

function startGame() {

    const levelData =
        levels[player.level - 1];

    enemy = {

        hp:
            levelData.enemyHP,

        maxHP:
            levelData.enemyHP,

        name:
            levelData.name

    };

    player.hp =
        Math.min(
            player.hp || 100,
            100
        );

    player.spirit =
        player.spirit || 0;

    player.defense = 0;

    document
        .getElementById("playerBody")
        .style.background =
            player.armor;

    document
        .getElementById("playerHead")
        .style.background =
            player.helmet;

    showScreen("game");

    writeLog(
        "Your journey begins..."
    );

    renderGame();
}


/* ==========================================
   RENDER GAME
========================================== */

function renderGame() {

    const levelData =
        levels[player.level - 1];

    document
        .getElementById("playerDisplay")
        .textContent =
            player.name;

    document
        .getElementById("playerNamePlate")
        .textContent =
            player.name;

    document
        .getElementById("levelDisplay")
        .textContent =
            player.level;

    document
        .getElementById("powerDisplay")
        .textContent =
            player.power;

    document
        .getElementById("hpMeter")
        .style.width =
            player.hp + "%";

    document
        .getElementById("spiritMeter")
        .style.width =
            player.spirit + "%";

    document
        .getElementById("enemyNamePlate")
        .textContent =
            enemy.name +
            " • " +
            Math.max(0, enemy.hp) +
            " HP";

    document
        .getElementById("battleVerse")
        .innerHTML = `

            <div class="verse-title">
                BATTLE VERSE
            </div>

            ${levelData.verse}
        `;

    const powerButton =
        document.getElementById(
            "powerMove"
        );

    powerButton.textContent =
        levelData.special +
        " • " +
        levelData.requiredPower +
        " SP";

    powerButton.disabled =
        player.power <
        levelData.requiredPower ||
        player.spirit < 50;

    /* Make boss visually larger */

    const enemyElement =
        document.getElementById(
            "enemyCharacter"
        );

    if (player.level === 3) {

        enemyElement.classList.add(
            "boss"
        );

    } else {

        enemyElement.classList.remove(
            "boss"
        );

    }

}


/* ==========================================
   BATTLE LOG
========================================== */

function writeLog(message) {

    const log =
        document.getElementById(
            "battleLog"
        );

    log.innerHTML =
        "<div>" +
        escapeHTML(message) +
        "</div>" +
        log.innerHTML;
}


/* ==========================================
   ATTACK SYSTEM
========================================== */

function attack(type) {

    if (battleLocked)
        return;

    battleLocked = true;

    let damage = 0;

    let spiritGain = 0;


    /* SPIRIT STRIKE */

    if (type === "strike") {

        damage =
            15 +
            player.level * 4;

        spiritGain = 12;

        writeLog(
            "You used Spirit Strike!"
        );

    }


    /* SHIELD OF FAITH */

    if (type === "shield") {

        damage = 6;

        spiritGain = 20;

        player.defense = 25;

        writeLog(
            "Shield of Faith surrounds you!"
        );

    }


    /* WORD OF TRUTH */

    if (type === "word") {

        damage =
            25 +
            player.level * 5;

        spiritGain = 25;

        writeLog(
            "The Word of Truth strikes the darkness!"
        );

    }


    /* SPECIAL */

    if (type === "special") {

        damage =
            55 +
            player.level * 18;

        player.spirit -= 50;

        spiritGain = 10;

        writeLog(
            "SPIRITUAL POWER MOVE!"
        );

    }


    enemy.hp -= damage;

    player.spirit =
        Math.min(
            100,
            player.spirit +
            spiritGain
        );

    renderGame();


    /* ENEMY DEFEATED */

    if (enemy.hp <= 0) {

        setTimeout(
            levelComplete,
            500
        );

        return;
    }


    /* ENEMY ATTACK */

    setTimeout(
        enemyAttack,
        700
    );
}


/* ==========================================
   ENEMY ATTACK
========================================== */

function enemyAttack() {

    const rawDamage =
        10 +
        player.level * 5;

    const blocked =
        Math.min(
            rawDamage,
            player.defense || 0
        );

    player.defense = 0;

    const damage =
        Math.max(
            2,
            rawDamage - blocked
        );

    player.hp -= damage;

    player.spirit =
        Math.min(
            100,
            player.spirit + 5
        );

    writeLog(
        enemy.name +
        " attacks!"
    );

    renderGame();


    /* PLAYER DEFEATED */

    if (player.hp <= 0) {

        player.hp = 100;

        player.spirit = 0;

        enemy.hp =
            enemy.maxHP;

        showOverlay(

            "BATTLE LOST",

            "Stand again and continue your journey. " +
            "Your level and Spiritual Power remain.",

            "RISE AGAIN"

        );

        return;
    }


    saveGame();

    battleLocked = false;
}


/* ==========================================
   LEVEL COMPLETE
========================================== */

function levelComplete() {

    if (player.level < 3) {

        player.level++;

        player.power +=
            levels[
                player.level - 1
            ].requiredPower;

        player.hp = 100;

        player.spirit = 0;

        const nextLevel =
            levels[
                player.level - 1
            ];

        enemy = {

            hp:
                nextLevel.enemyHP,

            maxHP:
                nextLevel.enemyHP,

            name:
                nextLevel.name

        };

        saveGame();

        writeLog(
            "LEVEL UP! New Spiritual Power unlocked!"
        );

        renderGame();

        showOverlay(

            "LEVEL UP!",

            "Your Spiritual Power has grown. " +
            "A stronger enemy approaches.",

            "ENTER NEXT BATTLE"

        );

    } else {

        player.power += 50;

        saveGame();

        showOverlay(

            "VICTORY!",

            "The Shadow Colossus has been defeated. " +
            "You completed all three battles " +
            "and gained 50 additional Spiritual Power.",

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
    buttonText
) {

    document
        .getElementById("overlayCard")
        .innerHTML = `

            <div class="level-up">
                ${title}
            </div>

            <p>
                ${message}
            </p>

            <button
                class="primary"
                onclick="closeOverlay()"
            >
                ${buttonText}
            </button>

        `;

    document
        .getElementById("overlay")
        .classList.add("show");
}


/* ==========================================
   CLOSE OVERLAY
========================================== */

function closeOverlay() {

    document
        .getElementById("overlay")
        .classList.remove("show");

    player.hp = 100;

    player.spirit = 0;

    player.defense = 0;

    const levelData =
        levels[player.level - 1];

    enemy = {

        hp:
            levelData.enemyHP,

        maxHP:
            levelData.enemyHP,

        name:
            levelData.name

    };

    renderGame();

    battleLocked = false;

    saveGame();
}


/* ==========================================
   CHARACTER PREVIEW
========================================== */

document
    .getElementById("armorInput")
    .addEventListener(
        "change",
        updatePreview
    );

document
    .getElementById("helmetInput")
    .addEventListener(
        "change",
        updatePreview
    );


function updatePreview() {

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
            "previewHead"
        )
        .style.background =
            helmet;
}


/* ==========================================
   AUTO SAVE
========================================== */

setInterval(
    () => {

        if (
            player &&
            currentSlot >= 0 &&
            document
                .getElementById("game")
                .classList.contains("active")
        ) {

            saveGame();

        }

    },
    5000
);


/* ==========================================
   START
========================================== */

renderSaveSlots();

updatePreview();

</script>

</body>
</html>
