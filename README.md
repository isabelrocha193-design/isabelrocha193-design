
<div align="center">

# ✦ ISABEL ROCHA BATISTA ✦

### Análise e Desenvolvimento de Sistemas

**Aprendendo • Codando • Evoluindo**

![Online](https://img.shields.io/badge/STATUS-ONLINE-35d07f?style=for-the-badge)
![ADS](https://img.shields.io/badge/CURSO-ADS-a855f7?style=for-the-badge)
![Game Mode](https://img.shields.io/badge/GAME_MODE-ON-7c3aed?style=for-the-badge)

---

### 🦖 DINOSAUR RUNNER

**Um pequeno jogo para jogar enquanto você explora meu perfil!**

[![JOGAR AGORA](https://img.shields.io/badge/▶%20JOGAR%20AGORA-DINOSAUR%20RUNNER-9b5de5?style=for-the-badge)](https://isabelrocha193-design.github.io/)

---

</div>

## ✨ Sobre mim

Olá! Sou estudante de **Análise e Desenvolvimento de Sistemas**. Estou aprendendo programação e desenvolvendo projetos para colocar em prática meus conhecimentos.

## 💻 Meus projetos

- 🎮 Portfólio interativo com jogos
- ☕ Estudos e projetos em Java
- 🧠 Lógica de Programação
- ⚙️ Sistemas Operacionais

## 🚀 Em evolução

- Aprendendo a programar
- Praticando e construindo projetos
- Transformando ideias em código

---

<div align="center">

**Sonhe. Estude. Conquiste. 💜**

</div>
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Isabel Rocha | Dinosaur Runner</title>
<style>
* { box-sizing: border-box; }

body {
  margin: 0;
  padding: 20px;
  background: #0d0916;
  color: white;
  font-family: Arial, sans-serif;
}

main {
  max-width: 900px;
  margin: auto;
}

header {
  text-align: center;
  padding: 25px 5px;
}

h1 {
  color: #d8a4ff;
  font-size: clamp(30px, 7vw, 55px);
  text-shadow: 0 0 15px #9b35ff;
}

header p { color: #c77bff; }

.panel {
  background: #171022;
  border: 1px solid #b65cff;
  border-radius: 15px;
  padding: 15px;
  margin: 15px 0;
  box-shadow: 0 0 15px #7026a833;
}

.hud {
  display: flex;
  justify-content: space-between;
  gap: 10px;
  flex-wrap: wrap;
  color: #d8a4ff;
  font-weight: bold;
  margin-bottom: 12px;
}

canvas {
  width: 100%;
  display: block;
  background: #100b1b;
  border-radius: 10px;
  touch-action: manipulation;
}

.controls {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 15px;
  flex-wrap: wrap;
}

button {
  background: #35164d;
  border: 1px solid #bd72ff;
  color: white;
  padding: 12px 22px;
  border-radius: 30px;
  font-weight: bold;
  font-size: 16px;
}

.hint {
  text-align: center;
  color: #cdb9df;
}

footer {
  text-align: center;
  color: #c77bff;
  padding: 25px;
}
</style>
</head>

<body>
<main>

<header>
  <h1>ISABEL ROCHA</h1>
  <h3>Análise e Desenvolvimento de Sistemas</h3>
  <p>APRENDENDO • CODANDO • EVOLUINDO</p>
</header>

<section class="panel">

  <div class="hud">
    <span>🦖 DINOSAUR RUNNER</span>
    <span>PONTOS: <span id="score">0</span></span>
  </div>

  <canvas id="game" width="860" height="280"></canvas>

  <div class="controls">
    <button id="jump">PULAR</button>
    <button id="restart">RECOMEÇAR</button>
  </div>

  <p class="hint" id="message">
    Toque para começar e pule os obstáculos!
  </p>

</section>

<section class="panel">
  <h2>✦ Sobre mim</h2>
  <p>
    Estudante de ADS, aprendendo programação
    e criando projetos para praticar.
  </p>

  <h2>⌘ Meus projetos</h2>
  <p>
    Java • Lógica de Programação •
    Sistemas Operacionais
  </p>

  <h2>🚀 Em evolução</h2>
  <p>
    Estudando, praticando e transformando
    ideias em código.
  </p>
</section>

<footer>
  Sonhe. Estude. Conquiste. 💜
</footer>

</main>

<script>
const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

const scoreElement = document.getElementById("score");
const message = document.getElementById("message");

const ground = 226;

let dino;
let obstacles;
let score;
let speed;
let frame;
let started;
let over;

function reset() {
  dino = {
    x: 75,
    y: ground - 42,
    w: 34,
    h: 42,
    vy: 0,
    grounded: true
  };

  obstacles = [];
  score = 0;
  speed = 5;
  frame = 0;
  started = false;
  over = false;

  scoreElement.textContent = "0";
  message.textContent = "Toque para começar e pule os cactos!";

  draw();
}

function begin() {
  if (over) reset();

  started = true;
  message.textContent = "Boa sorte! Pule os cactos!";
}

function hop() {
  if (over) return;

  if (!started) begin();

  if (dino.grounded) {
    dino.vy = -13;
    dino.grounded = false;
  }
}

function end() {
  over = true;
  started = false;
  message.textContent =
    "Game Over! Toque em RECOMEÇAR para jogar novamente.";
}

function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Estrelas
  ctx.fillStyle = "#b78ad8";

  for (let i = 0; i < 18; i++) {
    let x = (i * 71 + frame * 0.25) % canvas.width;
    let y = 25 + (i * 37) % 110;

    ctx.fillRect(x, y, 2, 2);
  }

  // Chão
  ctx.fillStyle = "#79529b";
  ctx.fillRect(0, ground, canvas.width, 2);

  // Dinossauro
  ctx.fillStyle = "#d8c5ef";

  ctx.fillRect(dino.x + 5, dino.y + 10, 22, 25);
  ctx.fillRect(dino.x + 19, dino.y, 17, 17);
  ctx.fillRect(dino.x + 29, dino.y + 7, 10, 7);
  ctx.fillRect(dino.x, dino.y + 17, 8, 8);

  // Olho
  ctx.fillStyle = "#160d22";
  ctx.fillRect(dino.x + 29, dino.y + 5, 3, 3);

  // Pernas animadas
  ctx.fillStyle = "#b65cff";

  if (started && Math.floor(frame / 6) % 2 === 0) {
    ctx.fillRect(dino.x + 8, dino.y + 34, 7, 9);
    ctx.fillRect(dino.x + 23, dino.y + 34, 7, 9);
  } else {
    ctx.fillRect(dino.x + 8, dino.y + 34, 7, 9);
    ctx.fillRect(dino.x + 22, dino.y + 34, 7, 9);
  }

  // Obstáculos
  obstacles.forEach(o => {
    ctx.fillStyle = "#65f0a5";

    ctx.fillRect(o.x, o.y, o.w, o.h);
    ctx.fillRect(o.x - 7, o.y + 12, 8, 6);
    ctx.fillRect(o.x - 7, o.y + 7, 5, 8);
    ctx.fillRect(o.x + o.w - 1, o.y + 18, 8, 6);
    ctx.fillRect(o.x + o.w + 3, o.y + 12, 5, 10);
  });

  if (!started && !over) {
    ctx.fillStyle = "#e7d6fa";
    ctx.font = "bold 18px Arial";
    ctx.textAlign = "center";
    ctx.fillText("TOQUE PARA JOGAR", 430, 75);
  }

  if (over) {
    ctx.fillStyle = "#ffb4f5";
    ctx.font = "bold 30px Arial";
    ctx.textAlign = "center";
    ctx.fillText("GAME OVER", 430, 100);
  }
}

function update() {
  if (started && !over) {
    frame++;
    score++;

    speed = Math.min(10, 5 + score / 500);
    scoreElement.textContent = Math.floor(score / 5);

    // Gravidade e pulo
    dino.y += dino.vy;
    dino.vy += 0.65;

    if (dino.y >= ground - dino.h) {
      dino.y = ground - dino.h;
      dino.vy = 0;
      dino.grounded = true;
    }

    // Criar obstáculos
    if (
      frame % Math.max(48, Math.floor(95 - (speed - 5) * 7)) === 0
    ) {
      let h = 28 + Math.random() * 22;

      obstacles.push({
        x: canvas.width + 10,
        y: ground - h,
        w: 18 + Math.random() * 9,
        h: h
      });
    }

    // Movimentar obstáculos
    obstacles.forEach(o => {
      o.x -= speed;
    });

    obstacles = obstacles.filter(o => o.x + o.w > 0);

    // Colisão
    for (const o of obstacles) {
      if (
        dino.x + dino.w - 5 > o.x &&
        dino.x + 5 < o.x + o.w &&
        dino.y + dino.h - 4 > o.y
      ) {
        end();
        break;
      }
    }
  }

  draw();
  requestAnimationFrame(update);
}

// Controles para celular e computador
canvas.addEventListener("pointerdown", hop);
document.getElementById("jump").addEventListener("click", hop);
document.getElementById("restart").addEventListener("click", reset);

window.addEventListener("keydown", function(e) {
  if (e.code === "Space" || e.code === "ArrowUp") {
    e.preventDefault();
    hop();
  }
});

reset();
update();
</script>

</body>
</html>
