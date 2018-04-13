```C
#include <Servo.h>
Servo myServo;
Servo myServo2;
Servo myServo3;
Servo myServo4;

String readString, servo1, servo2, servo3, servo4;

void setup() {
  Serial.begin(9600);
  myServo.attach(9);
  myServo2.attach(10);
  myServo3.attach(11);
  myServo4.attach(12); 
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
     servo3 = readString.substring(8, 12);
     servo4 = readString.substring(12, 16);
     
     Serial.println(servo1);  //print out serial monitor to see results
     Serial.println(servo2);
     Serial.println(servo3);
     Serial.println(servo4);
     
     int n1; //declare as number  
     int n2;
     int n3;
     int n4;
     
     
     char carray1[6]; //needed to convert string to a number 
     servo1.toCharArray(carray1, sizeof(carray1));
     n1 = atoi(carray1); 
     
     char carray2[6];
     servo2.toCharArray(carray2, sizeof(carray2));
     n2 = atoi(carray2); 

     char carray3[6];
     servo3.toCharArray(carray3, sizeof(carray3));
     n3 = atoi(carray3); 

     char carray4[6];
     servo4.toCharArray(carray4, sizeof(carray4));
     n4 = atoi(carray4); 
     
     myServo.write(n1); //set servo position 
     myServo2.write(n2);
     myServo3.write(n3);
     myServo4.write(n4);
     readString="";
 } 

}
