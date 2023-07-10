# Laboratorio
Laboratorio - Diseño Biomédico I

// Incluye la biblioteca de Arduino, para Visual 
#include <Arduino.h>

// Define los pines de los componentes
const int PinMotor = 11;                              // Pin del motor de corriente continua (DC)
const int PinPot = A0;                                // Pin del potenciómetro
const int PinsLED[] = {12, 14, 15, 16, 17, 19, 20};   // Pines de los 7 LEDs

void setup() {
  // Configura los pines como salidas o entradas
  pinMode(PinMotor, OUTPUT);
  for (int i = 0; i < 7; i++) {
    pinMode(PinsLED[i], OUTPUT);
  }
}

void loop() {
  // Lee el valor del potenciómetro
  int ValorPot = analogRead(PinPot);

  // Mapea el valor del potenciómetro al rango de velocidad del motor
  int VelocidadMotor = map(ValorPot, 0, 1023, 0, 255);

  // Controla la velocidad del motor
  analogWrite(PinMotor, VelocidadMotor);

  // Muestra visualmente la velocidad mediante los LEDs
  int ContLed = map(VelocidadMotor, 0, 255, 0, 7);
  for (int i = 0; i < 7; i++) {
    digitalWrite(PinsLED[i], i < ContLed ? HIGH : LOW);
  }

  delay(10);
}
