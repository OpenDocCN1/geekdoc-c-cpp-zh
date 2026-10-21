receiver has already processed the data, it still has to be transformed and interpreted according to some complicated rules. Also, Arduino's digitalRead() method isn't always accurate enough to deal with all types of incoming signals. You have to directly access the micro-controller to get the best results.

Fortunately, we don't have to do this ourselves, because the IRremote library² hides the nasty details. It supports the most popular infrared protocols, and can both receive and send data. After you've downloaded and extracted the ZIP file,³ copy the directory IRremote to either ~/Documents/Arduino/libraries (on a Mac) or My Documents\Arduino\libraries (on a Windows box). Then restart your IDE.

With the following sketch, you can then decode incoming infrared signals, if the IRremote library supports their encoding:

Download RemoteControl/InfraredDumper/InfraredDumper.pde

```
#include <IRremote.h>

const unsigned int IR_RECEIVER_PIN = 11;
const unsigned int BAUD_RATE = 9600;

IRrecv ir_receiver(IR_RECEIVER_PIN);
decode_results results;

void setup() {
  Serial.begin(BAUD_RATE);
  ir_receiver.enableIRIn();
}

void dump(const decode_results* results) {
  const int protocol = results->decode_type;
  Serial.print("Protocol: ");
  if (protocol == UNKNOWN) {
    Serial.println("not recognized.");
  } else {
    if (protocol == NEC) {
      Serial.println("NEC");
    } else if (protocol == SONY) {
      Serial.println("SONY");
    } else if (protocol == RC5) {
      Serial.println("RC5");
    } else if (protocol == RC6) {
      Serial.println("RC6");
    }
  }
```

2. http://www.arcfn.com/2009/08/multi-protocol-infrared-remote-library.html
3. http://arcfn.com/files/IRremote.zip