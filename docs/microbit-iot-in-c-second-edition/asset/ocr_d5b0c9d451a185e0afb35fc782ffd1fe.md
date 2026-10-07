The simplest pair of programs you can use to check that the radio is working
are:

Transmitter:

```
#include "MicroBit.h"
MicroBit uBit;
int main() {
    uBit.init();
    uBit.radio.enable();
    uBit.display.print("TX");
    while (1)
    {
        if (uBit.buttonA.isPressed())
        {
            uBit.display.print("1");
            uBit.radio.datagram.send("1");
        }
        uBit.sleep(100);
        uBit.display.clear();
    }
    return 0;
```

Receiver:

```
#include "MicroBit.h"
MicroBit uBit;
```

```
void onData(MicroBitEvent e) {
    ManagedString s = uBit.radio.datagram.recv();
    uBit.display.print(s);
}
```

```
int main() {
    uBit.init();
    uBit.messageBus.listen(MICROBIT_ID_RADIO, MICROBIT_RADIO_EVT_DATGRAM, onData);
    uBit.radio.enable();
    uBit.display.print("RX");
    while (1)
    {
        uBit.sleep(100);
        uBit.display.clear();
    }
}
```

If you try this out you should see 1 displayed on both micro:bits when Button A is pressed.