<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ZX10R TIME LOCK PANEL</title>

<style>
body {
    margin: 0;
    font-family: Arial;
    background: linear-gradient(135deg, #0f172a, #020617);
    color: white;
}

.container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

/* LOGIN */
.loginBox {
    background: black;
    padding: 25px;
    border-radius: 15px;
    text-align: center;
    width: 90%;
    max-width: 350px;
}

button, a {
    display: block;
    width: 100%;
    margin: 10px 0;
    padding: 12px;
    border-radius: 25px;
    border: none;
    font-weight: bold;
    text-decoration: none;
    color: white;
}

.enter { background: red; }
.register { background: orange; }
.vip { background: teal; }

/* PANEL */
.panel {
    display: none;
    padding: 10px;
}

.title {
    text-align: center;
    font-size: 22px;
    font-weight: bold;
}

/* RESULT */
.result {
    background: black;
    border-radius: 12px;
    padding: 20px;
    text-align: center;
    margin: 10px 0;
    font-size: 24px;
}

/* TIMER */
.timer {
    text-align: center;
    color: gold;
    font-size: 18px;
}

/* HISTORY */
.history {
    background: #111;
    border-radius: 10px;
    padding: 10px;
    max-height: 140px;
    overflow-y: auto;
    font-size: 13px;
}

/* DISABLED BUTTON */
.disabled {
    background: gray !important;
}

/* MONEY */
.money {
    position: fixed;
    top: -50px;
    font-size: 30px;
    animation: fall 2s linear;
}

@keyframes fall {
    to { transform: translateY(110vh); }
}
</style>

</head>
<body>

<!-- LOGIN -->
<div class="container" id="login">
    <div class="loginBox">
        <h2>ZX10R VIP ACCESS</h2>

        <button class="enter" onclick="enterPanel()">ENTER PANEL</button>

        <a href="https://www.jaiclub22.com/#/register?invitationCode=36367109582"
           target="_blank"
           class="register"
           onclick="unlockPanel()">REGISTER</a>

        <a href="https://t.me/+J3EWrhBninU0ZjU1"
           target="_blank"
           class="vip">JOIN VIP</a>
    </div>
</div>

<!-- PANEL -->
<div class="panel" id="panel">

<div class="title">𝐙𝐗10𝐑_𝐓𝐗 ULTRA</div>

<div class="timer" id="timer">60s WAIT</div>

<div class="result" id="result">WAITING...</div>

<button id="startBtn" class="enter disabled" onclick="startGame()">START</button>

<div class="history" id="history"><b>HISTORY</b><br></div>

</div>

<script>
let unlocked = false;
let time = 60;
let historyList = [];
let canPlay = false;

/* ENTER PANEL */
function enterPanel() {
    if (!unlocked) {
        voiceWarning();
        return;
    }
    document.getElementById("login").style.display = "none";
    document.getElementById("panel").style.display = "block";
}

/* REGISTER */
function unlockPanel() {
    unlocked = true;
}

/* TIMER */
setInterval(() => {
    if (!unlocked) return;

    time--;

    if (time <= 0) {
        document.getElementById("timer").innerText = "READY ✅";
        document.getElementById("startBtn").classList.remove("disabled");
        canPlay = true;
    } else {
        document.getElementById("timer").innerText = time + "s WAIT";
    }
}, 1000);

/* START */
function startGame() {

    if (!unlocked) {
        voiceWarning();
        return;
    }

    if (!canPlay) {
        voiceWarning();
        return;
    }

    // RESET TIMER
    time = 60;
    canPlay = false;
    document.getElementById("startBtn").classList.add("disabled");

    let num = Math.floor(Math.random() * 10);
    let size = num >= 5 ? "BIG" : "SMALL";

    // ✅ UPDATED COLOR LOGIC
    let color = num % 2 === 0 ? "RED" : "GREEN";

    let result = size + " | " + num + " | " + color;

    let box = document.getElementById("result");
    box.innerText = result;
    box.style.color = color === "GREEN" ? "#00ff00" : "red";

    addHistory(result);
    moneyRain();
}

/* HISTORY */
function addHistory(res) {
    historyList.unshift(res);
    if (historyList.length > 15) historyList.pop();

    document.getElementById("history").innerHTML =
        "<b>HISTORY</b><br>" + historyList.join("<br>");
}

/* VOICE */
function voiceWarning() {
    let msg = new SpeechSynthesisUtterance("WAIT FOR TIMER COMPLETE");
    msg.lang = "en-US";
    speechSynthesis.speak(msg);
}

/* MONEY */
function moneyRain() {
    for (let i = 0; i < 20; i++) {
        let m = document.createElement("div");
        m.innerText = "💸";
        m.className = "money";
        m.style.left = Math.random() * 100 + "vw";
        document.body.appendChild(m);
        setTimeout(() => m.remove(), 2000);
    }
}
</script>

</body>
</html>
