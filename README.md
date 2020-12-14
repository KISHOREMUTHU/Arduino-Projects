// # Arduino-Projects
// In this repository , I am going to post all the codes of my arduino projects 

#include <Servo.h>

// Defines Trig and Echo pins of the Ultrasonic Sensor

const int trigPin = 6;
const int echoPin = 7;
long duration;
int distance;

// Creates a servo object for controlling the servo motor
Servo myServo;

void setup() {

  pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
  pinMode(echoPin, INPUT); // Sets the echoPin as an Input
  Serial.begin(9600);
  myServo.attach(9); // connect servo motor pin to 9
  
             }

void loop() {

   distance = calculateDistance();
   
   // check whether the distance is less than 10 cm or not 
   
   if (distance < 10 ){
   
  // rotates the servo motor from 15 to 165 degrees
  for (int i = 15; i <= 165; i++) {
    myServo.write(i);
    delay(30);
  
    Serial.print(i); 
    Serial.print(","); 
    Serial.print(distance); 
    Serial.print("."); 
    
                                   }
  
  // Repeats the previous lines from 165 to 15 degrees
  for (int i = 165; i > 15; i--) {
    myServo.write(i);
    delay(30);
   
    Serial.print(i);
    Serial.print(",");
    Serial.print(distance);
    Serial.print(".");
    
                                  }
  
                       }
   
              }

// Function for calculating the distance measured by the Ultrasonic sensor

int calculateDistance() {
 
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  
  distance = duration * 0.034 / 2;  // formula to calculate distance 
  return distance;
  
}
