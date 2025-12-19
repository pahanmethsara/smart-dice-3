# smart-dice-3
coard of arduino project 1 :-

const int buttonPin = 8;
const int ledPins[6] = {2, 3, 4, 5, 6, 7};

int lastButtonState = HIGH;

void setup() {
  pinMode(buttonPin, INPUT_PULLUP);

  for (int i = 0; i < 6; i++) {
    pinMode(ledPins[i], OUTPUT);
    digitalWrite(ledPins[i], LOW);
  }

  randomSeed(analogRead(A0));
}

void loop() {
  int buttonState = digitalRead(buttonPin);

  if (buttonState == LOW && lastButtonState == HIGH) {
    lightRandomLEDs();
    delay(300); // debounce
  }

  lastButtonState = buttonState;
}

void lightRandomLEDs() {
  // Turn OFF all LEDs
  for (int i = 0; i < 6; i++) {
    digitalWrite(ledPins[i], LOW);
  }

  // Random number of LEDs (1 to 6)
  int ledCount = random(1, 7);

  // Turn ON first 'ledCount' LEDs
  for (int i = 0; i < ledCount; i++) {
    digitalWrite(ledPins[i], HIGH);
  }
} 
