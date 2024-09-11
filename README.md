# ProjetoAlura

let xBolinha = 300;
let yBolinha = 200;
let diametro = 20;
let raio = diametro / 2;

let velocidadeXBolinha = 10;
let velocidadeYBolinha = 10;

let xRaquete = 5;
let yRaquete = 150;
let raqueteComprimento = 10;
let raqueteAltura = 90;

let xRaqueteOponente = 585;
let yRaqueteOponente = 150;
let VelocidadeYOponente;

let meusPontos = 0;
let pontosDoOponente = 0;

let raquetada;
let ponto;
let trilha;

let colidiu = false;


function setup() {
  createCanvas(600, 400);
}

function draw() {
    background(0);
  mostraBolinha();
  velocidadeBolinha();
  definirColisão();
  mostraRaquete(xRaquete, yRaquete);
  movimentaMinhaRaquete();
  verificaColisaoRaquete(xRaquete, yRaquete)  
  verificaColisaoRaquete(xRaqueteOponente,               yRaqueteOponente);
  mostraRaquete(xRaqueteOponente, yRaqueteOponente);
  movimentaRaqueteOponente();
    stroke(255);
    textAlign(CENTER);
    textSize(16);
    fill(color(255, 140, 0));
    rect(150, 10, 40, 20);
    fill(255);
    text(meusPontos, 170, 26);
    fill(color(255, 140, 0));
    rect(450, 10, 40, 20);
    fill(255);
    text(pontosDoOponente, 470, 26);
    marcaPonto();
  
}

function mostraBolinha(){
      circle(xBolinha, yBolinha, diametro);

}

function velocidadeBolinha(){
    xBolinha += velocidadeXBolinha;
    yBolinha += velocidadeYBolinha;
}

function definirColisão(){
    if (xBolinha > width || xBolinha < 0) {
        velocidadeXBolinha *= -1;
    }
    if (yBolinha > height || yBolinha < 0) {
        velocidadeYBolinha *= -1;
    }
}

function mostraRaquete(){
    rect(xRaquete, yRaquete, raqueteComprimento, raqueteAltura);

}

function movimentaMinhaRaquete() {
    if (keyIsDown(UP_ARROW)) {
        yRaquete -= 10;
    }
    if (keyIsDown(DOWN_ARROW)) {
        yRaquete += 10;
    }
}

function verificaColisaoRaquete() {
    if (xBolinha - raio < xRaquete + raqueteComprimento
        && yBolinha - raio < yRaquete + raqueteAltura
        && yBolinha + raio > yRaquete) {
        velocidadeXBolinha *= -1;
    }
}

function verificaColisaoRaquete(x, y) {
    colidiu = collideRectCircle(x, y, raqueteComprimento, raqueteAltura, xBolinha, yBolinha, raio);
    if (colidiu){
        velocidadeXBolinha *= -1;
    }
}

function mostraRaquete(x,y) {
    rect(x, y, raqueteComprimento, raqueteAltura);
}

function movimentaRaqueteOponente() {
    velocidadeYOponente = yBolinha - yRaqueteOponente - raqueteComprimento / 2 - 30;
    yRaqueteOponente += velocidadeYOponente
}

function movimentaRaqueteOponente() {
    velocidadeYOponente = yBolinha - yRaqueteOponente - raqueteComprimento / 2 - 30;
    yRaqueteOponente += velocidadeYOponente
}

function incluiPlacar() {
  fill(255);
  text(meusPontos, 278, 26);
  text(pontosDoOponente, 321, 26);
}

function marcaPonto() {
  if (xBolinha > 570) {
    meusPontos += 1;
  }
  if (xBolinha < -5) {
    pontosDoOponente += 1;
  }
}

