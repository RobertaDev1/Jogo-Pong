//variáveis da bolinha
let xBolinha= 300;
let yBolinha= 200;
let diametro= 18;
let raio= diametro/2;

//variáveis da velocidade da bolinha
let velocidadeXBolinha=6;
let velocidadeYBolinha=6;

//variáveis da Raquete
let xRaquete= 4;
let yRaquete= 150;
let raqueteComprimento=10;
let raqueteAltura= 90;
let velocidadeYOponente;
let velocidadeXOponente;

let colidiu=false;

//variáveis do oponente
let xRaqueteOponente= 585;
let yRaqueteOponente=150;
let raqueteOponenteComprimento=10;
let raqueteOponenteAltura= 90;


//placar do jogo
let meusPontos =0;
let pontosDoOponente=0;

//sons do jogo
let raquetada;
let ponto;
let trilha;

//bolinha presa
let bolinhaNaoFicaPresa;



function setup() {
  createCanvas(600, 400);
  trilha.loop()
}

function draw() {
  background(0);
  mostraBolinha();
  movimentaBolinha();
  verificaColisaoBorda();
  mostraRaquete(xRaquete, yRaquete);
  movimentaMinhaRaquete(xRaquete, yRaquete, xRaqueteOponente, yRaqueteOponente);
  //verificaColisaoRaquete();
  mostraRaqueteOponente(xRaqueteOponente,yRaqueteOponente);
  rect(xRaquete,yRaquete,raqueteComprimento, raqueteAltura);
  verificaColisaoRaquete(xRaquete, yRaquete);
  movimentaRaqueteOponente();
  verificaColisaoRaquete(xRaqueteOponente,yRaqueteOponente);
  incluiPlacar();
  marcaPonto();
  bolinhaNaoFicaPresa();
  
  function bolinhaNaoFicaPresa(){
    if (xBolinha-raio<0){
      xBolinha= 23;
    }
    if (xBolinha + raio > 600){
      xBolinha = 580
    }
}

  

function mostraBolinha (){
  circle(xBolinha,yBolinha,diametro);
  
  
}
function movimentaBolinha(){
  xBolinha += velocidadeXBolinha;
  yBolinha += velocidadeYBolinha;
}
function verificaColisaoBorda(){
  if (xBolinha + raio> width ||
     xBolinha - raio< 0){
    velocidadeXBolinha *= -1;
  }
  
if (yBolinha +raio > height ||
     yBolinha - raio < 0){
    velocidadeYBolinha *= -1;
  }
}  
function mostraRaquete (x, y){
  rect(x, y,raqueteComprimento, raqueteAltura);
}

function mostraRaqueteOponente (x, y){  
  rect(x, y,raqueteComprimento, raqueteAltura);
}


function movimentaMinhaRaquete(){
  if (keyIsDown(UP_ARROW)){
    yRaquete -= 10;
  }
  if (keyIsDown(DOWN_ARROW)){
    yRaquete += 10;
  }
  //limitar a movimentação da raquete
  yRaquete= constrain (yRaquete, 10, 310);
}
  


}
function verificaColisaoRaquete(){
  if (xBolinha-raio< xRaquete + raqueteComprimento && yBolinha- raio< yRaquete+ raqueteAltura && yBolinha + raio > yRaquete){
    velocidadeXBolinha *= -1;
    raquetada.play();
  }
  
  }
function verificaColisaoRaquete(x, y){
  colidiu = collideRectCircle(x,
  y, raqueteComprimento, raqueteAltura, xBolinha,yBolinha, raio);
if (colidiu) {
  velocidadeXBolinha *= -1;
  raquetada.play();
  }
   
  }
 function movimentaRaqueteOponente(){
     if (keyIsDown(87)){
    yRaqueteOponente -= 10;
  }
  if (keyIsDown(83)){
      yRaqueteOponente += 10;
  }
  
      
    //limitar a movimentação da raquete
  yRaqueteOponente= constrain (yRaqueteOponente, 10, 310);
    }
    
    
    
    
function incluiPlacar(){
  
  stroke(255);
  textAlign(CENTER);
  textSize(26);
  
  fill(color (255, 140, 0));
  rect(150, 10, 40, 30);
   fill(255);
  text(meusPontos, 171, 34);
    fill(color (255, 140, 0));
  rect(450, 10, 40, 30);
  fill(255);
  text(pontosDoOponente, 471, 34);
 

  
}

function marcaPonto(){
  if (xBolinha > 590){
    meusPontos += 1;
    ponto.play();
  }
  if (xBolinha < 10){
      pontosDoOponente += 1;
    ponto.play();
  }
  
  
}
function preload(){
  trilha= loadSound("trilha.mp3");
  ponto= loadSound("ponto.mp3");
  raquetada= loadSound("raquetada.mp3");
}




