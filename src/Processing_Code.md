```java
import com.onformative.leap.*;
import com.onformative.leap.LeapMotionP5;
import com.leapmotion.leap.Finger;
import processing.serial.*;
LeapMotionP5 leap;

String angle,angle2,angle3,angle4,angle5,sending;
Serial port;


public void setup() {
  // set window, P3D = 3D rendering
  size(480, 480, P3D);
  noFill();
  stroke(255);

  // set LEAP object
  leap = new LeapMotionP5(this);

  // set com port. Currently: "/dev/tty.usbmodemfd121"
  println("Available serial ports:");
  println((Object[])Serial.list());
  port = new Serial(this,Serial.list()[0], 9600);
 }
public void draw() {
      background(0);
      fill(255);
      
      
    PVector position = leap.getTip(leap.getFinger(1));
    PVector position2 = leap.getTip(leap.getFinger(2));
    PVector position3 = leap.getTip(leap.getFinger(3));
    PVector position4 = leap.getTip(leap.getFinger(4));
    
    //PVector velocity = leap.getVelocity(f);
    ellipse(position.x, position.y, 10, 10);
    ellipse(position2.x, position2.y, 10, 10);
    ellipse(position3.x, position3.y, 10, 10);
    ellipse(position4.x, position4.y, 10, 10);
    
    rect(0,360,480,5,55);
    

    if (position.y > 360) {
      angle = Integer.toString(120);
    }
    else if (position.y < 360) {
      angle = Integer.toString(0);
    } 
    
    if (position2.y > 360) {
      angle2 = Integer.toString(120);
    }
    else if (position2.y < 360) {
      angle2 = Integer.toString(0);
    } 
    
    if (position3.y > 360) {
      angle3 = Integer.toString(120);
    }
    else if (position3.y < 360) {
      angle3 = Integer.toString(0);
    } 
  
    if (position4.y > 360) {
      angle4 = Integer.toString(120);
    }
    else if (position4.y < 360) {
      angle4 = Integer.toString(0);
    } 
    
    while(angle.length()< 4){
      angle = '0' + angle;
    }
    while(angle2.length()<4){
      angle2 = '0' + angle2;
    }
    while(angle3.length()<4){
      angle3 = '0' + angle3;
    }
    while(angle4.length()<4){
      angle4 = '0' + angle4;
    }
    sending = angle+angle2+angle3+angle4;
    
    port.write(sending);
    delay(250);
    println(sending);
    
  }
  


public void stop() {
  leap.stop();
}
