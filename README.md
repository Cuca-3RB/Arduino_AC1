# Grupo Cuca 
### Membros:
- **Ana Beatriz**

Oie! Sou a Ana Beatriz e tenho 18 anos eu gosto de jogar e ver lives e anime, tenho 1,80 de altura moro em São Paulo, gosto de ler mangas e de ficar em casa;
- **Ana Clara**

Oii! Sou a Ana Clara e tenho 17 anos, gosto de viajar e ouvir musica, more em SP, amo os animais;
- **Bianca**

oieee! Sou a Bianca e tenho 17 anos, moro em são Paulo, tenho 1,63 de altura e amo viajar, conversar, tirar fotos, cantar e dançar;
- **Julia Gomes**

Oioii! Sou a Julia, tenho 17 anos e sou pisciana , amo qualquer tipo de arte ou movimento artístico, amo dançar, ver filmes e ler vários livros, meu passatempo preferido é fazer nada;
- **Lana**

oii! Sou a Lana e tenho 16 anos, moro em sp, amo viajar;
- **Luiza Poroca**

Oie! Sou a Luiza Poroca, tenho 16 anos e 1,58 de altura! Amo teatro musical, cinema, instrumentos, música, enfim.. tudo que está relacionado a arte.

### Imagem de cada membro


**Ana Beatriz**
 
 ![](https://github.com/Cuca-3RB/Arduino_AC1/blob/main/d0aa16d9-0021-4f76-ae4b-7d9a46fb3c87.jpg)

**Ana Clara**

![](https://github.com/Cuca-3RB/Arduino_AC1/blob/main/image%20(4).png)

**Bianca**

![](https://github.com/Cuca-3RB/Arduino_AC1/blob/main/image%20(2).png)

**Julia Gomes**

![](https://github.com/Cuca-3RB/Arduino_AC1/blob/main/image%20(6).png)


**Lana**

![](https://github.com/Cuca-3RB/Arduino_AC1/blob/main/image%20(5).png)

**Luiza Poroca**

![](https://github.com/Cuca-3RB/Arduino_AC1/blob/main/image%20(7).png)

## *O PROBLEMA:* 

Seu grupo foi contratado para realizar a automação do chão de fábrica de uma farmacêutica responsável por produzir doses de vacina, a automação levará em conta alguns sensores e avisos luminosos para os funcionários responsáveis pela produção.

### Funcionalidades 
- Um botão para ligar e outro para desligar a produção indicados pelo led vermelho.
- Leitura do sensor de temperatura e teste, ao atingir *15℃* o led azul deve acender, deve ser informado via serial e somente apagar o led quando a temperatura for mais baixa que isso.
- Leitura do sensor de luminosidade e teste, ao indicar um valor acima de *5* a luminosidade do ambiente esta muito alta, deve ser informado via serial e o led verde deve permanecer aceso até a luminosidade diminuir.

### Imagem  da automação
![](https://github.com/Cuca-3RB/Arduino_AC1/blob/main/image.png)
### Link para ver a  funcionalidade da automação
https://www.tinkercad.com/things/8YGc1t7gm6s-magnificent-wolt-robo/editel?tenant=circuits

####  código  usado
```javascript
//variaveis da led
const int vermelho = 5;
const int verde = 6;
const int azul = 7;

bool estadoLedVermelho = false;

//adiçao de um botao 
const int botao1 = 2;
const int botao2 = 3;
unsigned long lastDebounceTime1 = 0;
unsigned long lastDebounceTime2 = 0;
const int botaoDelay = 100;

void setup()
{
  pinMode(A0, INPUT);
  pinMode(A1, INPUT);
  pinMode(vermelho, OUTPUT);
  pinMode(verde, OUTPUT);
  pinMode(azul, OUTPUT);
  
  Serial.begin(9600);
  //nome do grupo
  Serial.println("AC1 - Meu Primeiro Projeto 2021");
  Serial.println("                           V1.0");
  Serial.println("Grupo: CUCA");
}
//acender e apagar led vermelho
void loop()
{
  if((millis() - lastDebounceTime1) > botaoDelay && digitalRead(botao1)){
  	Serial.println("botao 1 apertado");
    ledVermelho(true);
  	lastDebounceTime1 = millis();
  }
  if((millis() - lastDebounceTime2) > botaoDelay && digitalRead(botao2)){
  	Serial.println("botao 2 apertado");
    ledVermelho(false);
  	lastDebounceTime2 = millis();
  }
  //temperatura
  if(getTemperatura() > 15){
    ledAzul(true);
    Serial.println("temepatura elevada");
  }else{
  	ledAzul(false);
    Serial.println("temepatura ideal");
  }
  //luminosidade
  	if(getLuminosidade() > 5){
    ledVerde(true);
    Serial.println("luminosidade elevada");
  }else{
  	ledVerde(false);
    Serial.println("luminosidade ideal");
  }
  delay(10);
}

void ledVermelho(bool estado){
 digitalWrite(vermelho,estado);
}
void ledVerde(bool estado){
 digitalWrite(verde,estado);  
}
void ledAzul(bool estado){
	digitalWrite(azul,estado);
}
//funcao temperatura
int getTemperatura(){
  	int temperaturaC;
	temperaturaC = map(((analogRead(A0) - 20) * 3.04), 0, 1023, -40, 125);
  	return temperaturaC;
} 
//funcao da luminosidade
int getLuminosidade(){
  	int luminosidade;
	luminosidade = map(analogRead(A1), 6, 619, -3, 10);
  	return luminosidade;
}
```
### Fim ;)
