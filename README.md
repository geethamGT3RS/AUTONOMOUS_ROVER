
# AUTONOMUS_ROVER



***************************** HARDWARE USED *******************************
   _______________________________________________________
   |  COMPONENTS                  |      QUANTITY        |
   <_____________________________________________________>   
   | 1) Arduino Uno Board         |        x 1           |
   | 2) Ultrasonic Sensor HC-SR04 |        x 2           |
   | 3) Motor Driver              |        x 1           |
   | 4) Motor With Gear           |        x 2           |
   | 5) Wires(Male to Male)       |        x 8           |
   | 6) Wires(Male to Female)     |        x 8           |
   | 7) Batteries                 |        x 2           |
   <_____________________________________________________>
   
 ************************* ASSEMBLY INSTRUCTIONS ***************************
 
 1) Assemble the cardboard car model given first,
 2) Then fit arduino onto top of model center,
 3) Attach motor with glue below,
 4) When assembeling sensor make they are distantly apart,
 5) Try connect wires compactly as shown in circuit diagram,
 6) Postion Motor driver and connect correctly with pins,
 7) Tighten screws of arduino, front wheel and motor driver
 
 ***************************  SOURCE CODE  *********************************
 
 
// SENSOR INPUT AND OUTPUT PINS

int Trigger_sensor1 = 8;
int Echo_sensor1    = 9;
int Trigger_sensor2 = 6;
int Echo_sensor2    = 7;

// MOTOR PINS AND SETUP

int Right_t1  = 10;
int Right_t2  = 11;
int Left_t1 = 12;
int Left_t2 = 13;

// DISTANCE AND DURATION FROM SENSORS

long duration1, distance1, duration2, distance2;

// ASSIGN PIN NUMBERS USING pinMode() FUNCTION

void setup() {
  
  Serial.begin(9600);
  pinMode(Left_t1, OUTPUT); 
  pinMode(Left_t2, OUTPUT);
  pinMode(Right_t1, OUTPUT);
  pinMode(Right_t2, OUTPUT);
  pinMode(Trigger_sensor1, OUTPUT); // Set Trig Pin As O/P To Transmit Waves
  pinMode(Echo_sensor1, INPUT); //Set Echo Pin As I/P To Recieve Reflected Waves
  pinMode(Trigger_sensor2, OUTPUT); // Set Trig Pin As O/P To Transmit Waves
  pinMode(Echo_sensor2, INPUT); //Set Echo Pin As I/P To Recieve Reflected Waves
  
}

void loop() {

       //SENSOR CODE 
  
  digitalWrite(Trigger_sensor1, LOW);
  delayMicroseconds(2);   
  digitalWrite(Trigger_sensor2, HIGH); 
  delayMicroseconds(10);
  duration1 = pulseIn(Echo_sensor1, HIGH); 
  distance1 = duration1 / 58.8;
  
        // CALUCLATES DISTANCE BETWEEN ROVER AND OBSTACLE
  
  digitalWrite(Trigger_sensor2, LOW);
  delayMicroseconds(2);
  digitalWrite(Trigger_sensor1, HIGH);
  delayMicroseconds(10);
  duration2 = pulseIn(Echo_sensor2, HIGH);
  distance2 = duration2 / 58.8; 
  delay(100);

if(distance1 > 25){

        //IT MOVES FORWARD IF NO OBSTACLE DETECTED
        
    digitalWrite(Left_t1, HIGH); 
    digitalWrite(Left_t2, LOW);
    digitalWrite(Right_t1, HIGH);                                
    digitalWrite(Right_t2, LOW);
    }
if( distance1 < 25 && distance1 > 10){
    if(distance2 > 25){
    
        //TURNS RIGHT IF OBSATCLE IS DETECTED AT FRONT SENSOR
        
    digitalWrite(Left_t1, HIGH); 
    digitalWrite(Left_t2, LOW);
    digitalWrite(Right_t1, LOW);                                
    digitalWrite(Right_t2, LOW);
    delay(1000);}
    if(distance2 < 25){
    
        // TURNS LEFT IF OBSTACLE IS DETECTED AT BOTH SENSORS
        
    digitalWrite(Left_t1, LOW); 
    digitalWrite(Left_t2, LOW);
    digitalWrite(Right_t1, HIGH);                                
    digitalWrite(Right_t2, LOW);
    delay(1000);}
    }
if( distance1 < 10){
    if(distance2 > 25){
    
        //TURNS SHARP RIGHT IF SENSOR DETECTS OBSTACLE SUDDENLY
        
    digitalWrite(Left_t1, HIGH); 
    digitalWrite(Left_t2, LOW);
    digitalWrite(Right_t1, LOW);                                
    digitalWrite(Right_t2, HIGH);
    delay(1000);}
    if(distance2 < 25){
    
        // TURNS SHARP LEFTT IF BOTH SENSOR DETECTS OBSTACLE SUDDENLY
    
    digitalWrite(Left_t1, LOW); 
    digitalWrite(Left_t2, HIGH);
    digitalWrite(Right_t1, HIGH);                                
    digitalWrite(Right_t2, LOW);
    delay(1000);}
    }  

}
