<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<title>タイピング・パズルシューティング</title>
<style>
  body {
    margin: 0;
    background: #111;
    color: white;
    font-family: sans-serif;
    text-align: center;
  }
  canvas {
    background: #000;
    display: block;
    margin: 0 auto;
  }
  #inputBox {
    margin-top: 10px;
    font-size: 20px;
    padding: 5px;
  }
</style>
</head>
<body>
<h1>タイピングシューティング</h1>
<canvas id="game" width="600" height="400"></canvas>
<br>
<input id="inputBox" placeholder="ここに入力..." />

<script>
const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");
const input = document.getElementById("inputBox");

const words = ["apple","banana","cat","dog","elephant","fire","game","hero","ice","jump"];

let enemies = [];
let score = 0;

function spawnEnemy() {
  const word = words[Math.floor(Math.random() * words.length)];
  enemies.push({
    word: word,
    x: Math.random() * 550,
    y: 0,
    speed: 1 + Math.random() * 2
  });
}

function update() {
  ctx.clearRect(0,0,600,400);

  enemies.forEach(e => {
    e.y += e.speed;
    ctx.fillStyle = "white";
    ctx.fillText(e.word, e.x, e.y);
  });

  enemies = enemies.filter(e => e.y < 400);

  ctx.fillText("Score: " + score, 10, 20);
}

function shoot(word) {
  enemies = enemies.filter(e => {
    if(e.word === word) {
      score++;
      return false;
    }
    return true;
  });
}

input.addEventListener("keydown", e => {
  if(e.key === "Enter") {
    shoot(input.value);
    input.value = "";
  }
});

setInterval(spawnEnemy, 2000);
setInterval(update, 30);
</script>
</body>
</html>
