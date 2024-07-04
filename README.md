# EMBEDDED-PROJECT
COLOUR BASED PRODUCT SORTING

# Arduino Code
# Header file
#include <Servo.h>
#define S0 2
#define S1 3
#define S2 4
#define S3 5
#define sensorOut 6
Servo topServo;
Servo bottomServo;
int frequency = 0;
int color=0;
void setup() {
pinMode(S0, OUTPUT);
pinMode(S1, OUTPUT);
pinMode(S2, OUTPUT);
pinMode(S3, OUTPUT);
pinMode(sensorOut, INPUT);
 # Setting frequency-scaling to 20%
digitalWrite(S0, HIGH);
digitalWrite(S1, LOW);
7
topServo.attach(7);
bottomServo.attach(8);
Serial.begin(9600);
}
void loop() {
topServo.write(115);
delay(500);
for(int i = 115; i > 65; i--) {
topServo.write(i);
delay(2);
}
delay(500);
color = readColor();
delay(10);
switch (color) {
case 1:
bottomServo.write(85);
break;
case 2:
bottomServo.write(105);
break;
case 3:
bottomServo.write(125);
break;
case 4:
bottomServo.write(150);
break;
case 0:
8
break;
}
delay(300);
for(int i = 55; i > 45; i--) {
topServo.write(i);
delay(2);
}
delay(200);
for(int i = 45; i < 80; i++) {
topServo.write(i);
delay(2);
}
color=0;
}
# Custom Function - readColor()
int readColor() {
 # setting red filtered photodiodes to be read
digitalWrite(S2, LOW);
digitalWrite(S3, LOW);
# Reading the output frequency
frequency = pulseIn(sensorOut, LOW);
int R = frequency;
# Printing the value on the serial monitor
Serial.print("R= ");//printing name
Serial.print(frequency);//printing RED color frequency
Serial.print(" ");
delay(50);
# Setting Green filtered photodiodes to be read
digitalWrite(S2, HIGH);
9
digitalWrite(S3, HIGH);
# Reading the output frequency
frequency = pulseIn(sensorOut, LOW);
int G = frequency;
# Printing the value on the serial monitor
Serial.print("G= ");//printing name
Serial.print(frequency);//printing RED color frequency
Serial.print(" ");
delay(50);
# Setting Blue filtered photodiodes to be read
digitalWrite(S2, LOW);
digitalWrite(S3, HIGH);
# Reading the output frequency
frequency = pulseIn(sensorOut, LOW);
int B = frequency;
# Printing the value on the serial monitor
Serial.print("B= ");//printing name
Serial.print(frequency);//printing RED color frequency
Serial.println(" ");
delay(50);
if(R>73 & R<100 & G>119 & G<140 & B>105 &B<122){ 
# This value should be change according to your reding please check serial monitor to know your reading.
color = 1; // Red
}
if(R>92 & R<110 & G>105 & G<135 & B>105 &B<122){
color = 2; // Green
}
if(R>73 & R<93 & G>95 & G<117 & B>100 &B<118){
color = 3; // Yellow
}
10
if(R>87 & R<115 & G>105 & G<130 & B>80 &B<105){
color = 4; // Blue
}
return color;
}
