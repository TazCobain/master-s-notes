---
cssclasses:
  - smart-iot
---
![[ArduinoEs-1.png]]

```cpp
int ledPin10 = 10; // Pin PWM a cui è collegato il LED
int brightness = 0; // Luminosità iniziale (valore tra 0 e 255)
int fadeAmount = 150; // Incremento/decremento di luminosità a ogni ciclo

int inputPin = 12;
int ledPin = 7;
int inputState = 0;

bool buttonStatus(int pin) {
	int stato = digitalRead(pin);
	if (stato == LOW) {
		return true;
	} else {
		return false;
	}
}
 
void PinchangeStatus(int pin, bool value) {
	if (value) {
		digitalWrite(pin, LOW);
	} else {
		digitalWrite(pin, HIGH);
	}
} 

void setup() {
	pinMode(ledPin10, OUTPUT); // Imposta il pin del LED come output
	pinMode(inputPin, INPUT_PULLUP);
	pinMode(ledPin, OUTPUT);
}

  
void loop() {
	analogWrite(ledPin10, brightness); // Imposta la luminosità del LED
	brightness = brightness + fadeAmount; // Aggiorna la luminosità
 
	if (brightness <= 0 || brightness >= 255) {
		fadeAmount = -fadeAmount;
	} 

	inputState = buttonStatus(inputPin);
	if (inputState) {
		PinchangeStatus(ledPin, false);
	} else {
		PinchangeStatus(ledPin, true);
	} 

delay(300); // Pausa di 30 millisecondi per rendere visibile l'effetto
}
```