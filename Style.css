const player = document.getElementById("player");
const enemy = document.getElementById("enemy");

let x = 400;
let y = 250;

let vida = 100;
let fome = 100;
let sede = 100;

let madeira = 0;
let comida = 0;

let tempo = 0;
let dia = 1;

let jogando = false;

const velocidade = 5;

const teclas = {};

document.addEventListener("keydown", e => {
  teclas[e.key.toLowerCase()] = true;

  // Atacar
  if (e.code === "Space") {
    atacar();
  }

  // Coletar
  if (e.key.toLowerCase() === "e") {
    coletar();
  }
});

document.addEventListener("keyup", e => {
  teclas[e.key.toLowerCase()] = false;
});

function startGame() {
  document.getElementById("menu").classList.add("hidden");
  document.getElementById("game").classList.remove("hidden");

  jogando = true;

  x = 400;
  y = 250;

  atualizar();
}

function atualizar() {

  if (!jogando) return;

  // Movimento
  if (teclas["w"]) y -= velocidade;
  if (teclas["s"]) y += velocidade;
  if (teclas["a"]) x -= velocidade;
  if (teclas["d"]) x += velocidade;

  // Limites da tela
  x = Math.max(0, Math.min(window.innerWidth - 50, x));
  y = Math.max(60, Math.min(window.innerHeight - 70, y));

  player.style.left = x + "px";
  player.style.top = y + "px";

  moverInimigo();

  requestAnimationFrame(atualizar);
}

// Sobrevivência
setInterval(() => {

  if (!jogando) return;

  tempo++;

  fome -= 1;
  sede -= 1;

  if (fome <= 0 || sede <= 0) {
    vida -= 3;
  }

  document.getElementById("vida").textContent = Math.max(0, vida);
  document.getElementById("fome").textContent = Math.max(0, fome);
  document.getElementById("sede").textContent = Math.max(0, sede);
  document.getElementById("tempo").textContent = tempo;

  if (tempo % 60 === 0) {
    dia++;
    document.getElementById("dia").textContent = dia;
  }

  if (vida <= 0) {
    morrer();
  }

}, 1000);


// Inimigo
let enemyX = 800;
let enemyY = 400;

function moverInimigo() {

  const dx = x - enemyX;
  const dy = y - enemyY;

  const distancia = Math.sqrt(dx * dx + dy * dy);

  if (distancia > 60) {
    enemyX += (dx / distancia) * 1.2;
    enemyY += (dy / distancia) * 1.2;
  } else {
    vida -= 0.2;
  }

  enemy.style.left = enemyX + "px";
  enemy.style.top = enemyY + "px";
}


// Coletar recursos
function coletar() {

  const recursos = document.querySelectorAll(".resource");

  recursos.forEach(recurso => {

    const rx = parseInt(recurso.style.left);
    const ry = parseInt(recurso.style.top);

    const distancia = Math.sqrt(
      (x - rx) ** 2 +
      (y - ry) ** 2
    );

    if (distancia < 80) {

      if (recurso.classList.contains("wood")) {
        madeira += 1;
      }

      if (recurso.classList.contains("food")) {
        comida += 1;
      }

      if (recurso.classList.contains("water")) {
        sede = Math.min(100, sede + 30);
      }

      recurso.remove();

      document.getElementById("madeira").textContent = madeira;
      document.getElementById("comida").textContent = comida;
    }

  });
}


// Comer
document.addEventListener("keydown", e => {

  if (e.key.toLowerCase() === "f" && comida > 0) {

    comida--;

    fome = Math.min(100, fome + 30);

    document.getElementById("comida").textContent = comida;
    document.getElementById("fome").textContent = fome;
  }

});


// Ataque
function atacar() {

  const dx = x - enemyX;
  const dy = y - enemyY;

  const distancia = Math.sqrt(dx * dx + dy * dy);

  if (distancia < 100) {

    enemyX = Math.random() * (window.innerWidth - 100);
    enemyY = Math.random() * (window.innerHeight - 150);

    enemy.style.left = enemyX + "px";
    enemy.style.top = enemyY + "px";
  }
}


// Morte
function morrer() {

  jogando = false;

  document.getElementById("game").classList.add("hidden");
  document.getElementById("gameOver").classList.remove("hidden");

  document.getElementById("finalTime").textContent = tempo;
}
