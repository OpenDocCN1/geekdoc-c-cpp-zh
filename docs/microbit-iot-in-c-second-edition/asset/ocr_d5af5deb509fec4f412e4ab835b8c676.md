As an example of using serial events let's write a program that simply copies characters to the LED display. The event handler is just:

```
```
void onChar(MicroBitEvent e) {
ManagedString s = uBit.serial.read(1);
uBit.serial.clearRxBuffer();
uBit.display.scroll(s);
uBit.serial.eventAfter(1);
}

```
```

The main program is:

```
```
#include "MicroBit.h"
//define baud setBaudrate //uncomment for V2
MicroBit uBit;
int main() {
uBit.init();
uBit.serial(20);
uBit.messageBus.listen(MICROBIT_ID_SERIAL, MICROBIT_SERIAL_EVT_HEAD_MATCH, onChar);
uBit.serial.eventAfter(1);
while (1)uBit.sleep(1000)
release_fiber();
}
```
```

Notice that we use a setRxBufferSize size to make the framework actually create a buffer. The eventAfter function sets the event ready to happen and the while(1) sleep(1000) keeps the fiber running while waiting for the event. Alternatively you could simply release the fiber and let the scheduler call the event handler.

The event handler is simple enough, but notice that we have to reset the event to happen a second time. These features of the framework might change well in future versions.

# # Problems With Serial

The biggest problem with using micro:bit serial is that, even though you can connect to it to GPIO lines, there is only one serial hardware device, i.e. one UART. A standard problem when trying to multiplex between different lines is that, when the switch happens, the Rx and Tx buffers are swapped to the new pins. For example, suppose you are connected to a device on pins 0 and 1 and suddenly switch the UART to USB. If there was data coming in on pin 1 switching pins will cause all sorts of problems as it alters the transfer and can crash the microbit V1.

In general, you have to make sure that all data traffic has stopped before you switch pins. You might think this is an easy task, but it can be very difficult because of the use of ASYNC and SLEEP, which can allow your fiber to do things while data is being received or transmitted.