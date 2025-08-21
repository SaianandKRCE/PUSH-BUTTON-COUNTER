# PUSH-BUTTON-COUNTER

#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2); // Change 0x27 if needed

const int buttonPin = 2;
int count = 0;
int buttonState = HIGH;
int lastButtonState = HIGH;

void setup() {
  pinMode(buttonPin, INPUT_PULLUP); // Internal pull-up, so other end of button goes to GND
  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("Press Count:");
  lcd.setCursor(0, 1);
  lcd.print(count);
}

void loop() {
  buttonState = digitalRead(buttonPin);

  if (lastButtonState == HIGH && buttonState == LOW) {
    count++;
    lcd.setCursor(0, 1);
    lcd.print("                ");
    lcd.setCursor(0, 1);
    lcd.print(count);
    delay(200); // Simple debounce
  }

  lastButtonState = buttonState;
}

