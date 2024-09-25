# Codi-TDR
TDR Codi Arduino, sensor de ultrasons amb 3 leds i un buzzer
int trig = 2;
int echo = 3;
long duració;
long distancia;
int buzzerPin = 7;  // Pin per al buzzer

void setup() {
  Serial.begin(9600);
  pinMode(trig, OUTPUT);
  pinMode(echo, INPUT);
  pinMode(4, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(buzzerPin, OUTPUT); // Configurar pin del buzzer com a sortida
}

void loop() {
  // Codi per mesurar la distància
  digitalWrite(trig, LOW);
  delayMicroseconds(10);
  digitalWrite(trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(trig, LOW);
  
  duració = pulseIn(echo, HIGH);
  duració= duració / 2;
  distància = duració / 29.15;
  Serial.print("La distància és");
  Serial.print(distància);
  Serial.println("cm");
  delay(100);

  // Control dels LEDs
  if (distància >= 45) {  // 45 cm
    digitalWrite(6, LOW);  // Apagar LED verd
  } else {
    digitalWrite(6, HIGH); // Engegar LED verd
  }

  if (distancia >= 30) {  // 30 cm
    digitalWrite(5, LOW);  // Apagar LED groc
  } else {
    digitalWrite(5, HIGH); // Engegar LED groc
  }

  if (distancia >= 20) {  // 20 cm
    digitalWrite(4, LOW);  // Apagar LED vermell
  } else {
    digitalWrite(4, HIGH); // Engegar LED vermell
  }
  // Lògica per al buzzer
  if (distancia < 20) {  // Si la distància és menor a 20 cm
    digitalWrite(buzzerPin, HIGH);  // Activar el buzzer
  } else {
    digitalWrite(buzzerPin, LOW);   // Desactivar el buzzer
  } 
}
