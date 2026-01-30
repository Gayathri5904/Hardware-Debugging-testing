# Hardware-Debugging-testing
Performed hardware and firmware debugging using UART logs, LED indicators, and functional validation tests
// Pin definitions
const int TempPin = A0;   // Temperature sensor
const int LDRPin  = A1;   // LDR
const int LED = 8;
const int buzzerPin = 9;// Buzzer or LED

void setup() {
  Serial.begin(9600);
  pinMode(LED, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
}

void loop() {
  // ----- Temperature Sensor (LM35) -----
  int tempValue = analogRead(TempPin);
  int LDRValue = analogRead(LDRPin);
  
  float tempVoltage = tempValue * (5.0 / 1023.0);
  float temperatureC = (tempVoltage - 0.5) * 100.0; // LM35 formula

  // ----- LDR -----
  
  

  // ----- Display values -----
  Serial.print("Temperature: ");
  Serial.print(temperatureC);
  Serial.print(" °C  |  ");

  Serial.print("LDR Value: ");
  Serial.println(LDRValue);

  // ----- Alert condition -----
  if (temperatureC > 35) {
    digitalWrite(LED, LOW);
    digitalWrite(buzzerPin, LOW);
  Serial.println("TEMP ALERT");
}

if (LDRValue < 400) {
   digitalWrite(LED, HIGH);
   digitalWrite(buzzerPin, HIGH);
  Serial.println("LOW LIGHT ALERT");
}

  delay(1000);
}
