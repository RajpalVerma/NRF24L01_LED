#include <SPI.h>
#include <RF24.h>
#include <nRF24L01.h>

RF24 radio(7,8); // declaring CE and CSN pins
const byte address[] = "node1";

int mycolor =  0; // stores the received data of state of button after
 int rpin = 3;
 int gpin = 4;
 int bpin = 5;
 
void setup() {
  radio.begin(); // initializes the operations of the chip
  radio.openReadingPipe(0, address);
  radio.setPALevel(RF24_PA_MIN);
  radio.startListening();
  
  pinMode(rpin, OUTPUT); // declares LEDpin as an output
    pinMode(gpin, OUTPUT);
      pinMode(bpin, OUTPUT);
      Serial.begin(9600);
}


void loop() {
  
  
  while(radio.available()){  
    radio.read(&mycolor, sizeof(mycolor));
  }
    Serial.print(mycolor);

    if(mycolor == 1)
    {
      digitalWrite(gpin,HIGH);
      digitalWrite(rpin,LOW);
      digitalWrite(bpin,LOW);
      delay(100);
      
    }
    if(mycolor == 2)
    {
      digitalWrite(rpin,HIGH);
      digitalWrite(gpin,LOW);
      digitalWrite(bpin,LOW);
      delay(100);
      
      
    }
    if(mycolor == 3)
    {
      digitalWrite(bpin,HIGH);
      digitalWrite(rpin,LOW);
      digitalWrite(gpin,LOW);
      delay(100);
      
    }
    
    } 
