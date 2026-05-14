# AUTOMATIC-ENGINE-LOCKING-SYSTEM-FOR-DRUNKEN-DRIVERS

This project presents an automatic engine locking system to prevent drunk driving accidents. Using an alcohol sensor and Arduino Uno, the system detects alcohol in the driver’s breath. If the alcohol level exceeds a set limit, a buzzer alerts the user and the engine ignition is disabled, improving road safety and preventing vehicle use by intoxicated drivers.


#include <LiquidCrystal.h>

// LCD pins: RS, EN, D4-D7
LiquidCrystal lcd(2, 3, 4, 5, 6, 7);

const int gassensor = A0;  // Analog pin for vibration sensor
const int motorPin = 9;          // DC motor pin (via motor driver)
const int buzzerPin = 8;         // Buzzer pin
const int Threshold = 100; // Threshold for alcohol detection (adjust based on sensor calibration)

void setup() 
{
  pinMode(gassensor, INPUT);
  pinMode(motorPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);

  lcd.begin(16, 2);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.clear();
}

void loop() 
{
  int Gassensorlevel = analogRead(gassensor); // Read alcohol sensor value
  
  // Display alcohol sensor reading on LCD
  lcd.setCursor(0, 0);
  // int val=digitalRead(2);
  if (Gassensorlevel>100)
  {
    lcd.print("Alcohol val");
    lcd.setCursor(13,0);
    lcd.print(Gassensorlevel);
    lcd.setCursor(0,1);
    lcd.print("engine Locked");
    digitalWrite(motorPin, LOW); // Turn on the motor (engine running)
    digitalWrite(buzzerPin, HIGH); // Turn off buzzer
  }
  else 
  {
  // if(val==HIGH)

  lcd.print("Alcohol val");
    lcd.setCursor(13,0);
    lcd.print(Gassensorlevel);
    lcd.setCursor(0,1);
    lcd.print(" Safe");
    Serial.println("READY TO GO");
    digitalWrite(motorPin, HIGH); // Turn on the motor (engine running)
    digitalWrite(buzzerPin, LOW); // Turn off buzzer
  }

  delay(500); // Small delay to stabilize sensor readings
  lcd.clear();
}
