#include <Adafruit_NeoPixel.h>
Adafruit_NeoPixel linijka = Adafruit_NeoPixel(
8, A0, NEO_GRB + NEO_KHZ800);
//variables
int s = 0;
int x = 0;
int y = 0;
int z = 0;
int mx = 4;
int my = 4;
int mz = 4;
int reset = 0;
void setup() {
linijka.begin();
linijka.show();
pinMode(2, INPUT_PULLUP);
pinMode(3, INPUT_PULLUP);
pinMode(4, INPUT_PULLUP);
pinMode(5, INPUT_PULLUP);
pinMode(9, OUTPUT);
Serial.begin(9600);// Initializing Serail communication.
pinMode(LED_BUILTIN, OUTPUT);
// initialize digital pin LED_BUILTIN as an output.
}
void loop() {
reset = 0;
digitalWrite(LED_BUILTIN, HIGH);
// turn the LED on (HIGH is the voltage level)
digitalWrite(9,HIGH);
Serial.println("more POWER");
if (digitalRead(3) == HIGH) {
if (digitalRead(4) == LOW) {
s = s + 1;
x = x + mx*60;
if (x > mx*60) x = 0;
delay (300);
}
if (digitalRead(5) == LOW) {
s = s + 1;
y = y + my*60;
if (y > my*60) y = 0;
delay (300);
}
if (digitalRead(2) == LOW) {
s = s + 1;
z = z + mz*60;
if (z > mz*60) z = 0;
delay (300);
}
}if (digitalRead(3) == LOW) {
s = 0;
x = 0;
y = 0;
z = 0;
if (digitalRead(4) == LOW) {
mx = mx + 1;
if (mx > 4) mx = 1;
delay (300);
}
if (digitalRead(5) == LOW) {
my = my + 1;
if (my > 4) my = 1;
delay (300);
}
if (digitalRead(2) == LOW) {
mz = mz + 1;
if (mz > 4) mz = 1;
delay (300);
if (digitalRead(5) == LOW) {
if (digitalRead(4) == LOW) {
s = 1;
x = 0;
y = 0;
z = 0;
reset = 1;
delay (300);
}
}
}}
if (reset == 1) {
mx = 4;
my = 4;
mz = 4;
}
if (s > 0) {
linijka.setPixelColor(0, linijka.Color(x, y, z));
linijka.show();
}
else {
linijka.setPixelColor(0, linijka.Color(0, 0, 0));
linijka.show();
}
}
