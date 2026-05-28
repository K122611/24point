<!DOCTYPE html>
<html lang="zh">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>24 Point Game</title>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; }
body {
  font-family: 'Segoe UI', system-ui, sans-serif;
  background: #1a1a2e;
  color: #ecf0f1;
  display: flex; justify-content: center; align-items: center;
  min-height: 100vh; user-select: none;
}
.game {
  width: 420px; padding: 30px 20px;
  display: flex; flex-direction: column; align-items: center; gap: 16px;
}
.title { font-size: 32px; font-weight: bold; color: #e94560; letter-spacing: 2px; }
.subtitle { font-size: 13px; color: #8899aa; }
.score { font-size: 14px; color: #f1c40f; }
hr { width: 100%; border: 1px solid #2c3e50; }
.section-title { font-size: 15px; color: #b0b8c1; }

.cards { display: flex; gap: 14px; justify-content: center; }
.card {
  width: 88px; height: 120px;
  background: #16213e;
  border: 2px solid #2c3e50;
  border-radius: 14px;
  display: flex; flex-direction: column;
  justify-content: center; align-items: center;
  font-size: 30px; font-weight: bold;
  cursor: pointer; transition: all .2s;
  color: #ecf0f1;
}
.card:hover { background: #0f3460; transform: translateY(-3px); }
.card.selected { background: #e94560; border-color: #ff6b6b; transform: translateY(-4px); box-shadow: 0 6px 20px rgba(233,69,96,.4); }
.card.dim { opacity: 0.35; pointer-events: none; }
.card .suit { font-size: 22px; margin-top: 2px; }

.ops { display: flex; gap: 10px; }
.op-btn {
  width: 85px; height: 44px;
  background: #533483; color: #ecf0f1;
  border: none; border-radius: 12px;
  font-size: 18px; font-weight: bold;
  cursor: pointer; transition: all .2s;
}
.op-btn:hover { background: #7b2d8e; }
.op-btn:active { background: #3c2260; }
.op-btn:disabled { opacity: .35; cursor: not-allowed; }

.expr-box {
  width: 100%; background: #0f3460; border-radius: 12px;
  padding: 14px 16px; text-align: center;
  font-size: 14px; color: #7f8c8d; min-height: 44px;
  display: flex; align-items: center; justify-content: center;
  line-height: 1.6;
}
.expr-box.warn { color: #f39c12; }
.expr-box.gold { color: #f1c40f; }
.expr-box.success { color: #2ecc71; }

.status { font-size: 20px; font-weight: bold; min-height: 30px; text-align: center; }
.status.error { color: #e74c3c; }
.status.win { color: #2ecc71; }
.status.lose { color: #e74c3c; }

.actions { display: flex; gap: 12px; }
.act-btn {
  padding: 10px 26px; border: none; border-radius: 10px;
  font-size: 15px; font-weight: bold; cursor: pointer; color: #ecf0f1;
  transition: all .2s;
}
.act-btn:hover { filter: brightness(1.2); }
.act-btn:active { filter: brightness(.8); }
.act-btn:disabled { opacity: .35; cursor: not-allowed; }
.btn-undo { background: #7f8c8d; }
.btn-reset { background: #e67e22; }
.btn-new { background: #2ecc71; }
</style>
</head>
<body>
<div class="game">
  <div class="title">2&#65039;&#8419;4&#65039;&#8419;  24 Point Game</div>
  <div class="subtitle">Combine 4 numbers to make 24</div>
  <div class="score" id="score">Wins: 0 / 0</div>
  <hr>
  <div class="section-title">&#127188; Your Numbers</div>
  <div class="cards" id="cards"></div>
  <div class="section-title">&#128290; Choose Operator</div>
  <div class="ops">
    <button class="op-btn" id="btn-add" onclick="applyOp('+')">+ Add</button>
    <button class="op-btn" id="btn-sub" onclick="applyOp('-')">- Sub</button>
    <button class="op-btn" id="btn-mul" onclick="applyOp('*')">x Mul</button>
    <button class="op-btn" id="btn-div" onclick="applyOp('/')">/ Div</button>
  </div>
  <div class="expr-box" id="expr">Select two numbers...</div>
  <div class="status" id="status"></div>
  <hr>
  <div class="actions">
    <button class="act-btn btn-undo" id="btn-undo" onclick="undo()">&#8617; Undo</button>
    <button class="act-btn btn-reset" id="btn-reset" onclick="resetGame()">&#8634; Reset</button>
    <button class="act-btn btn-new" onclick="newGame()">&#128259; New Game</button>
  </div>
</div>

<script>
const SUITS = ["\u2660","\u2665","\u2666","\u2663"];
const VAL = {1:"A",11:"J",12:"Q",13:"K"};

let numbers = [];
let selected = [];
let history = [];
let steps = [];
let solved = false;
let wins = 0, total = 0;

function newGame() {
  total++;
  solved = false;
  selected = [];
  history = [];
  steps = [];
  numbers = [];
  for (let i = 0; i < 4; i++) numbers.push(Math.floor(Math.random()*13)+1);
  setStatus("","");
  setExpr("Select two numbers...","");
  render();
}

function render() {
  const c = document.getElementById("cards");
  c.innerHTML = "";
  numbers.forEach((v,i) => {
    const div = document.createElement("div");
    div.className = "card" + (selected.includes(i) ? " selected" : "") + (solved ? " dim" : "");
    div.innerHTML = `<span>${VAL[v]||v}</span><span class="suit">${SUITS[i%4]}</span>`;
    div.onclick = ()=>toggleCard(i);
    c.appendChild(div);
  });

  const sel = selected.length;
  const expr = document.getElementById("expr");
  expr.className = "expr-box";
  if (sel === 0) { expr.textContent = "Select two numbers..."; }
  else if (sel === 1) { expr.textContent = "Select another number..."; expr.classList.add("warn"); }
  else {
    expr.textContent = `${numbers[selected[0]]} and ${numbers[selected[1]]} selected \u2014 choose operator!`;
    expr.classList.add("gold");
  }

  const canOp = sel === 2 && !solved;
  ["btn-add","btn-sub","btn-mul","btn-div"].forEach(id => {
    document.getElementById(id).disabled = !canOp;
  });
  document.getElementById("btn-undo").disabled = history.length === 0 || solved;
}

function toggleCard(i) {
  if (solved || numbers.length <= 1) return;
  const idx = selected.indexOf(i);
  if (idx >= 0) selected.splice(idx,1);
  else {
    if (selected.length >= 2) selected.shift();
    selected.push(i);
  }
  render();
}

function applyOp(op) {
  if (selected.length !== 2 || solved) return;
  saveState();
  let [ia,ib] = [selected[0],selected[1]];
  let a = numbers[ia], b = numbers[ib], r, expr;
  switch(op) {
    case "+": r = a+b; expr = `${a} + ${b} = ${r}`; break;
    case "-":
      if (a>=b) { r = a-b; expr = `${a} - ${b} = ${r}`; }
      else { r = b-a; expr = `${b} - ${a} = ${r}`; }
      break;
    case "*": r = a*b; expr = `${a} \u00d7 ${b} = ${r}`; break;
    case "/":
      if (b&&a%b===0) { r = a/b; expr = `${a} \u00f7 ${b} = ${r}`; }
      else if (a&&b%a===0) { r = b/a; expr = `${b} \u00f7 ${a} = ${r}`; }
      else { showError(`Division not exact! (${a} and ${b})`); history.pop(); selected=[]; render(); return; }
      break;
  }
  steps.push(expr);
  let isort = [...selected].sort((x,y)=>y-x);
  numbers.splice(isort[0],1);
  numbers.splice(isort[1],1);
  numbers.push(r);
  selected = [];
  render();
  checkWin();
}

function saveState() {
  history.push({ numbers: [...numbers], selected: [...selected], steps: [...steps] });
}

function undo() {
  if (!history.length || solved) return;
  const s = history.pop();
  numbers = s.numbers; selected = s.selected; steps = s.steps;
  setStatus("","");
  render();
}

function resetGame() {
  if (solved) return;
  if (!history.length) return;
  const first = history[0];
  numbers = [...first.numbers];
  selected = [];
  steps = [];
  history = [];
  setStatus("","");
  render();
}

function checkWin() {
  if (numbers.length !== 1) return;
  if (numbers[0] === 24) {
    solved = true; wins++;
    setStatus("\ud83c\udf89 CORRECT! 24! \ud83c\udf89","win");
    setExpr(steps.join("<br>"),"success");
  } else {
    setStatus(`Result is ${numbers[0]}, not 24. Try again!`,"lose");
  }
  document.getElementById("score").textContent = `Wins: ${wins} / ${total}`;
  render();
}

function showError(msg) {
  const s = document.getElementById("status");
  s.textContent = "\u26a0 " + msg;
  s.className = "status error";
  setTimeout(()=>{ if (s.textContent.startsWith("\u26a0")) s.textContent=""; }, 2000);
}

function setStatus(msg, cls) {
  const s = document.getElementById("status");
  s.textContent = msg; s.className = "status " + (cls||"");
}

function setExpr(msg, cls) {
  const e = document.getElementById("expr");
  e.innerHTML = msg; e.className = "expr-box " + (cls||"");
}

newGame();
</script>
</body>
</html>
