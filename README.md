# LED
Arduino: Αναβοσβήνει LED + εντολές r και s

const int ledPin = 13;  



bool stopped = false;



void setup() {

 pinMode(ledPin, OUTPUT);

 Serial.begin(9600);

 Serial.println("System Ready. Send 'r' to restart or 's' to stop.");

}



void loop() {

 

 if (Serial.available()) {

  char command = Serial.read();



  if (command == 'r') {

   Serial.println("Restarting...");

   delay(500);

   asm volatile ("jmp 0"); // Restart Arduino

  }

  else if (command == 's') {

   Serial.println("Stopped. Send 'r' to reset.");

   stopped = true;

   digitalWrite(ledPin, LOW); // Σβήσε LED

  }

 }



 

 if (stopped) return;





 digitalWrite(ledPin, HIGH);

 delay(500);

 digitalWrite(ledPin, LOW);

 delay(500);

}

Message
Type Message

