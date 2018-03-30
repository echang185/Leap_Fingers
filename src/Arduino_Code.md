```C
#include <Servo.h>
Servo myServo;
Servo myServo2;

String readString, servo1, servo2;

void setup() {
  Serial.begin(9600);
  myServo.attach(9);
  myServo2.attach(10); 
  Serial.println("servo-test-21");

}

void loop() {

  while (Serial.available()) {
   delay(10);  
   if (Serial.available() >0) {
     char c = Serial.read();  //gets one byte from serial buffer
     readString += c; //makes the string readString
   } 
 }

 if (readString.length() >0) {
     Serial.println(readString); //see what was received
     
     // expect a string like 07002100 containing the two servo positions      
     servo1 = readString.substring(0, 4); //get the first four characters
     servo2 = readString.substring(4, 8); //get the next four characters 
     
     Serial.println(servo1);  //print out serial monitor to see results
     Serial.println(servo2);
     
     int n1; //declare as number  
     int n2;
     
     char carray1[6]; //needed to convert string to a number 
     servo1.toCharArray(carray1, sizeof(carray1));
     n1 = atoi(carray1); 
     
     char carray2[6];
     servo2.toCharArray(carray2, sizeof(carray2));
     n2 = atoi(carray2); 
     
     myServo.write(n1); //set servo position 
     myServo2.write(n2);
     readString="";
 } 

}
```
