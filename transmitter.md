#include <RF24.h>
#include <nRF24L01.h>

RF24 radio(7,8);   // declaring CE and CSN pins
const byte address[] = "node1";
int mycolor = 0;
String msg= "enter the color \n " ;


void setup() {
  Serial.begin(9600);
   radio.begin();  // initializes the operations of the chip
  radio.openWritingPipe(address);
  radio.setPALevel(RF24_PA_MIN);
  radio.stopListening();  
  
  // put your setup code here, to run once:

}

void loop() {

  Serial.println(msg);
  while(Serial.available() ==0)
  {
  }
  mycolor = Serial.parseInt();
  Serial.println(mycolor);
    radio.write(&mycolor, sizeof(mycolor));
  }
