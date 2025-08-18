<div align="center">
  <h1>👋 Olá, eu sou o Lucas</h1>
  <p><em>Front-End Developer | Design 3D | Design Gráfico</em></p>
  
  <img src="https://komarev.com/ghpvc/?username=luckx&color=blue&style=flat" alt="Profile views" />
</div>

---

<h2>🚀 Sobre mim</h2>
<p>
  Tenho 13 anos e sou apaixonado por tecnologia e criação visual.  
  Trabalho com <strong>Front-End</strong>, <strong>Design 3D</strong> e <strong>Design Gráfico</strong>.  
  Estou sempre aprendendo coisas novas para evoluir no mundo da programação e do design.
</p>

---

<h2>💻 Minhas Stacks</h2>
<div align="center">
  <img src="https://skillicons.dev/icons?i=html" alt="HTML" height="50" />
  <img src="https://skillicons.dev/icons?i=css" alt="CSS" height="50" />
  <img src="https://skillicons.dev/icons?i=js" alt="JavaScript" height="50" />
  <img src="https://skillicons.dev/icons?i=figma" alt="Figma" height="50" />
  <img src="https://skillicons.dev/icons?i=blender" alt="Blender" height="50" />
</div>

---

<h2>🌐 Conecte-se comigo</h2>
<div align="center">
  <a href="https://www.instagram.com/luckx.ig" target="_blank">
    <img src="https://skillicons.dev/icons?i=instagram" alt="Instagram" height="50"/>
  </a>
</div>

---

<h2>🎮 Jogo da Cobrinha</h2>
<p>Use as setas do teclado para jogar!</p>
<div style="text-align:center;">
  <canvas id="snakeGame" width="400" height="400" style="border:1px solid #000;"></canvas>
</div>

<script>
const canvas = document.getElementById("snakeGame");
const ctx = canvas.getContext("2d");

const box = 20;
let snake = [{x: 9*box, y: 10*box}];
let direction = "RIGHT";
let food = {
  x: Math.floor(Math.random()*20)*box,
  y: Math.floor(Math.random()*20)*box
};

document.addEventListener("keydown", changeDirection);

function changeDirection(event){
    if(event.key === "ArrowUp" && direction !== "DOWN") direction = "UP";
    if(event.key === "ArrowDown" && direction !== "UP") direction = "DOWN";
    if(event.key === "ArrowLeft" && direction !== "RIGHT") direction = "LEFT";
    if(event.key === "ArrowRight" && direction !== "LEFT") direction = "RIGHT";
}

function draw(){
    ctx.fillStyle = "#f0f0f0";
    ctx.fillRect(0,0,canvas.width,canvas.height);

    for(let i=0; i<snake.length; i++){
        ctx.fillStyle = (i===0) ? "green" : "lightgreen";
        ctx.fillRect(snake[i].x, snake[i].y, box, box);
        ctx.strokeStyle = "white";
        ctx.strokeRect(snake[i].x, snake[i].y, box, box);
    }

    ctx.fillStyle = "red";
    ctx.fillRect(food.x, food.y, box, box);

    let snakeX = snake[0].x;
    let snakeY = snake[0].y;

    if(direction === "LEFT") snakeX -= box;
    if(direction === "RIGHT") snakeX += box;
    if(direction === "UP") snakeY -= box;
    if(direction === "DOWN") snakeY += box;

    if(snakeX === food.x && snakeY === food.y){
        snake.push({});
        food = {
            x: Math.floor(Math.random()*20)*box,
            y: Math.floor(Math.random()*20)*box
        };
    } else {
        snake.pop();
    }

    // colisão
    if(snakeX < 0 || snakeX >= canvas.width || snakeY < 0 || snakeY >= canvas.height || collision(snakeX, snakeY, snake)){
        clearInterval(game);
        alert("Game Over!");
    }

    snake.unshift({x: snakeX, y: snakeY});
}

function collision(x, y, array){
    for(let i=0; i<array.length; i++){
        if(array[i].x === x && array[i].y === y) return true;
    }
    return false;
}

let game = setInterval(draw, 100);
</script>
