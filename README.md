# 🎬 Demonstração em Vídeo


<div align="center">


</div>


### Explicação 

Este código cria um sistema simples de detecção de proximidade usando um sensor ultrassônico e um LED. O sensor mede a distância de objetos
à sua frente e envia essa informação para o monitor serial.
Se algum objeto ou pessoa chegar a 10 cm ou menos do sensor, o sistema considera que há um intruso.
## Código


```
const int PINO_TRIG = 33;
const int PINO_ECHO = 32;
const int PINO_LED_INTRUSO = 25;

float obter_distancia();

void setup() {

  Serial.begin(115200);
  pinMode(PINO_TRIG, OUTPUT);
  pinMode(PINO_ECHO, INPUT);
  pinMode(PINO_LED_INTRUSO, OUTPUT);
  digitalWrite(PINO_TRIG, LOW);

}

void loop() {

  float dist = obter_distancia();

  Serial.print("Distância :");
  Serial.print(dist);
  Serial.println(" cm");
  
  if(dist > 0 && dist <= 10){
    Serial.println("Intruso detectado!");
    digitalWrite(PINO_LED_INTRUSO, HIGH);
    delay(1000);
  }else{
    Serial.println("Ambiente seguro");
    digitalWrite(PINO_LED_INTRUSO, LOW);
  }
  delay(500);
}

float obter_distancia(){

  digitalWrite(PINO_TRIG, LOW);
  delayMicroseconds(2);
  digitalWrite(PINO_TRIG, HIGH);
  delayMicroseconds(10);
  digitalWrite(PINO_TRIG, LOW);
  long duracao = pulseIn(PINO_ECHO, HIGH, 30000);
  float distancia = (duracao/2.0) * 0.0343;

 return distancia;

}

```