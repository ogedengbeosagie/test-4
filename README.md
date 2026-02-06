# test-4
Valentine - 2026
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Click Me</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body {
    margin: 0;
    height: 100vh;
    background: #6a1bb9;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: Arial, sans-serif;
    overflow: hidden;
}

.card {
    background: white;
    border-radius: 20px;
    padding: 40px 30px;
    width: 320px;
    text-align: center;
    box-shadow: 0 15px 40px rgba(0,0,0,0.2);
    cursor: pointer;
    position: relative;
    z-index: 2;
}

h1 {
    color: #6a1bb9;
    font-size: 26px;
    margin-bottom: 30px;
}

.primary {
    background: #7b2cbf;
    color: white;
    border: none;
    padding: 14px 30px;
    border-radius: 30px;
    font-size: 16px;
    cursor: pointer;
}

.buttons {
    display: none;
    gap: 15px;
    justify-content: center;
    position: relative;
}

#yesBtn {
    transition: transform 0.2s;
}

#noBtn {
    position: absolute;
}
</style>
</head>

<body>

<div class="card" id="card">
    <h1 id="text">Hey Beautiful...</h1>

    <button class="primary" id="startBtn">Click Me</button>

    <div class="buttons" id="buttons">
        <button class="primary" id="yesBtn">YES</button>
        <button class="primary" id="noBtn">NO</button>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

<script>
const messages = [
    "We've made so many memories",
    "You make me happy",
    "You make me smile every single day",
    "I have one question to ask you",
    "Will you be my Valentine?"
];

let step = 0;
let yesScale = 1;

const text = document.getElementById("text");
const startBtn = document.getElementById("startBtn");
const buttons = document.getElementById("buttons");
const yesBtn = document.getElementById("yesBtn");
const noBtn = document.getElementById("noBtn");
const card = document.getElementById("card");

startBtn.addEventListener("click", advance);

card.addEventListener("click", () => {
    if (step > 0 && step < messages.length) advance();
});

function advance() {
    if (step < messages.length) {
        text.innerText = messages[step];
        step++;

        if (step === messages.length) {
            startBtn.style.display = "none";
            buttons.style.display = "flex";
        }
    }
}

noBtn.addEventListener("mouseenter", evadeNo);
noBtn.addEventListener("click", evadeNo);

function evadeNo() {
    const x = Math.random() * 160 - 80;
    const y = Math.random() * 100 - 50;
    noBtn.style.transform = `translate(${x}px, ${y}px)`;

    yesScale += 0.15;
    yesBtn.style.transform = `scale(${yesScale})`;
}

yesBtn.addEventListener("click", () => {
    text.innerText = "She said YES 💜";
    buttons.style.display = "none";
    launchConfetti();
});

function launchConfetti() {
    const duration = 2000;
    const end = Date.now() + duration;

    (function frame() {
        confetti({
            particleCount: 5,
            angle: 60,
            spread: 55,
            origin: { x: 0 },
            colors: ["#7b2cbf", "#9d4edd", "#c77dff"]
        });

        confetti({
            particleCount: 5,
            angle: 120,
            spread: 55,
            origin: { x: 1 },
            colors: ["#7b2cbf", "#9d4edd", "#c77dff"]
        });

        if (Date.now() < end) {
            requestAnimationFrame(frame);
        }
    })();
}
</script>

</body>
</html>
