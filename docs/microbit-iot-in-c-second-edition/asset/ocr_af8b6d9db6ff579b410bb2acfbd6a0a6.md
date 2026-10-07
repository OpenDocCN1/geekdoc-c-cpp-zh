Finally, before you dismiss the idea of having a micro-bit do nothing but ask repeatedly "is the doorbell pressed", consider what it has to do. If it is "not much" then a polling loop will be your simplest option.

Let's find out how much overhead is inherent in using events by repeating the pulse width measurement. This time we can't simply print the results as this would stop the event handling. As a compromise we save 20 readings in an array and then print them after repeating a second - all the input pulse have to occurred before this. It is also important to keep the event handling routines short. If the event handling takes longer than the pulse width then we will get an incorrect reading due to the missed pulse.

```
#include "MicroBit.h"
MicroBit uBit;
uint64_t t[20];
uint64_t temp=0;
int i=0;
void onPulseEdge(MicroBitEvent evt) {
  t[i] = evt.timestamp;
  i++;
  temp = evt.timestamp;
  if(i<20)return;
  uBit.io.P0.event(MICROBIT_PIN_EVENT_NONE);
}
```

```
int main() {
  uBit.init();
  uBit.messageBus.listen(MICROBIT_ID_IO_P0,
    MICROBIT_PIN_EVT_RISE,
    onPulseEdge,
    MESSAGE_BUS_LISTENER_IMMEDIATE);
  uBit.messageBus.listen(MICROBIT_ID_IO_P0,
    MICROBIT_PIN_EVT_FALL,
    onPulseEdge,
    MESSAGE_BUS_LISTENER_IMMEDIATE);
  uBit.io.P0.event(MICROBIT_PIN_EVENT_ON_EDGE);
  uBit.sleep(1000);
  for(i=1;i<20;i++){
    printf("%d\n\r", (int)t[i]);
  }
}
```

Notice we have the event handler called when there is a rising edge and a falling edge.