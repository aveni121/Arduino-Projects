#include <Adafruit_NeoPixel.h>
int LED_PIN = 6;
int LED_COUNT = 192;
int micPin = A0;

int micVal = 0;
int mappedMicVal = 0;

int ambientSound = 0;
Adafruit_NeoPixel strip(LED_COUNT, LED_PIN, NEO_GRB + NEO_KHZ800);


void setup() {
  strip.begin();
  strip.show();
  
  strip.setBrightness(255);// put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println(F("Initialize System"));

  pinMode(micPin, INPUT);
}

void loop() {

  static int iterCount = 0;
  randomSeed(iterCount);
  int rgb[] = {random(0,256),random(0,256),random(0,256)};
  uint32_t color = strip.Color(rgb[0],rgb[1],rgb[2]);

  if(iterCount == 0){
    calibrateAmbientSound();
  }

  else{
   micVal = readMicrophone();
   colorWipeLevels(color, micVal);    
   strip.clear();
  }
   iterCount++;
   
}

void calibrateAmbientSound(){

  int average = 0;
  int runningTotal = 0;
  int tempVal = 0;
  for(int i = 0; i < 50; i++){
    tempVal = analogRead(micPin);
    Serial.print("Temp Val");
    Serial.println(tempVal);
    runningTotal += tempVal;
  }

  average = runningTotal/50;
  ambientSound = average;
  micVal = readMicrophone();
  
}
int readMicrophone( ) { /* function readMicrophone */
  ////Test routine for Microphone
  int micValtoRet = 0;
  micValtoRet = analogRead(micPin);

  Serial.print("Ambient Sound: ");
  Serial.println(ambientSound);
  Serial.print("Mic Val:");
  Serial.println(micVal);
  return micValtoRet;
}


void colorWipeLevels(uint32_t color, int micVal){
  int micDiff = micVal - ambientSound;
  int micRange = micDiff + 70;

  Serial.print("Mic Diff:");
  Serial.println(micDiff);

   if(micDiff > 100){
    lightUpColors(color, LED_COUNT, 2);
   }
   else if(micDiff > 90){
    lightUpColors(color, 171, 2);
   }
   else if(micDiff > 80){
    lightUpColors(color, 152, 2);
   }
   else if(micDiff > 70){
    lightUpColors(color, 133, 2);
   }
   else if(micDiff > 60){
    lightUpColors(color, 114, 2);
   }
   else if(micDiff > 50){
    lightUpColors(color, 95, 2);
   }
   else if(micDiff > 40){
    lightUpColors(color, 76, 2);
   }
   else if(micDiff > 30){
    lightUpColors(color, 57, 2);
   }
   else if(micDiff > 20){
    lightUpColors(color, 38, 2);
   }
   else if(micDiff < 10){
    lightUpColors(color, 10,2);
   }
}

void lightUpColors(uint32_t color, int val, int increment){
  for(int i=0; i< val; i++) { 
      i = increment+i;
      strip.fill(color ,0 ,i);         //  Set pixel's color (in RAM)
      strip.show();                          //  Update strip to match
    }
}
