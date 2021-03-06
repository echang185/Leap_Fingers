```java
import de.voidplus.leapmotion.*;
import processing.serial.*;

Serial port;
LeapMotion leap;

String angle1, angle2, angle3, angle4, angle5, sending;

void setup()
{
  size(1024,768,OPENGL);
  background(255);
  leap = new LeapMotion(this);
  println("Available serial ports:");
  println((Object[])Serial.list());
  port = new Serial(this,Serial.list()[1], 9600);
}

void draw()
{
  background(255);
  
  for (Hand hand : leap.getHands()){
    //initialize hand attributes for each hand seen by the leap object
    int     hand_id         = hand.getId();
    PVector hand_position   = hand.getPosition();
    PVector hand_stabilized = hand.getStabilizedPosition();
    PVector hand_direction  = hand.getDirection();
    PVector hand_dynamics   = hand.getDynamics();
    float   hand_roll       = hand.getRoll();
    float   hand_pitch      = hand.getPitch();
    float   hand_yaw        = hand.getYaw();
    boolean hand_is_left    = hand.isLeft();
    boolean hand_is_right   = hand.isRight();
    float   hand_grab       = hand.getGrabStrength();
    float   hand_pinch      = hand.getPinchStrength();
    float   hand_time       = hand.getTimeVisible();
    PVector sphere_position = hand.getSpherePosition();
    float   sphere_radius   = hand.getSphereRadius();
    

    //Specific Finger (initialize fingers for each hand seen by the leap object)
    Finger finger_thumb = hand.getThumb();
    Finger finger_index = hand.getIndexFinger();
    Finger finger_ring  = hand.getRingFinger();
    Finger finger_pink  = hand.getPinkyFinger();
    
    //Drawing (actions to be taken when a hand is being seen)
    PVector indexMcp = hand.getIndexFinger().getRawPositionOfJointMcp();
    PVector indexTip = hand.getIndexFinger().getRawPositionOfJointTip();
    PVector middleTip = hand.getMiddleFinger().getRawPositionOfJointTip();
    PVector middleMcp = hand.getMiddleFinger().getRawPositionOfJointMcp();
    PVector ringTip = hand.getRingFinger().getRawPositionOfJointTip();
    PVector ringMcp = hand.getRingFinger().getRawPositionOfJointMcp();
    PVector pinkyTip = hand.getPinkyFinger().getRawPositionOfJointTip();
    PVector pinkyMcp = hand.getPinkyFinger().getRawPositionOfJointMcp();
    PVector thumbTip = hand.getThumb().getRawPositionOfJointTip();
    PVector thumbMcp = hand.getThumb().getRawPositionOfJointMcp();
    
    float index = indexTip.dist(indexMcp);
    float middle = middleTip.dist(middleMcp);
    float ring = ringTip.dist(ringMcp);
    float pinky = pinkyTip.dist(pinkyMcp);
    float thumb = thumbTip.dist(thumbMcp);
    print(thumb+" ");
    
    hand.draw();
    if (index < 50){
      angle1 = Integer.toString(180);
    }
    else {
      angle1 = Integer.toString(0);
    }
    
    if (middle < 60){
      angle2 = Integer.toString(180);
    }
    else {
      angle2 = Integer.toString(0);
    }
    
    if (ring < 60){
      angle3 = Integer.toString(180);
    }
    else {
      angle3 = Integer.toString(0);
    }
    
    if (pinky < 44){
      angle4 = Integer.toString(180);
    }
    else {
      angle4 = Integer.toString(0);
    }
    
    if (thumb < 87){
      angle5 = Integer.toString(180);
    }
    else {
      angle5 = Integer.toString(0);
    }
    
    while(angle1.length()< 4){
      angle1 = '0' + angle1;
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
    while(angle5.length()<5){
      angle5 = '0' + angle5;
    }
      sending = angle1+angle2+angle3+angle4+angle5;
     port.write(sending);
     //delay(500);
     //println(sending);
    for (Finger finger: hand.getFingers())
    {
      //Initialize finger attributes for each finger on a hand
      int     finger_id         = finger.getId();
      PVector finger_position   = finger.getPosition();
      PVector finger_stabilized = finger.getStabilizedPosition();
      PVector finger_velocity   = finger.getVelocity();
      PVector finger_direction  = finger.getDirection();
      float   finger_time       = finger.getTimeVisible();
      
      
      //Specific Finger (Actions to be taken with a specific finger
      switch(finger.getType())
      {
       
        case 0:  //Thumb
          break;
        case 1:  //Index
          break;
        case 2:  //Middle
          break;
        case 3:  //Ring
          break;
        case 4:  //Pinky
          break;
      }

    }
  }
}
