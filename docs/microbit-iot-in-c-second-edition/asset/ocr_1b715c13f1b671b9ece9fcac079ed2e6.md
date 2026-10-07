# Setup

We need a function to set up the hardware ready to communicate with the device:

V1

```
void initWiFi() {
  uBit.serial.redirect(Tx, Rx);
  uBit.serial.baud(115200);
  uBit.serial.setRxBufferSize((uint8_t)+5000);
}
```

V2

```
void initWiFi() {
  uBit.serial.redirect(uBit.io.P1 , uBit.io.P2);
  uBit.serial.setBaudrate(115200);
  uBit.serial.setRxBufferSize((uint8_t)+5000);
}
```

The pins that we are using are P0 and P1, to allow for other choices Tx and Rx are defined as constants at the start of the program:

V1

```
#define Tx MICROBIT_PIN_P0
#define Rx MICROBIT_PIN_P1
```

V2

```
#define Tx uBit.io.P0
#define Rx uBit.io.P1
```

The model of ESP8266 works at 115200 by default. Newer models and up-dated firmware is reported to work at 9600 baud. If this is the case, you need to modify the data rate and/or change the ESP8266's baud.

# Attention!

To start with the easiest, but possibly least useful, command let's implement some functions that test that we have a connection to the device, always a good thing to start with.

In this section we develop the first of a functions that send a command to the device and get back a response. To do this we need a few functions to help and are reused in other AT functions. Once you have one AT function the rest are very similar, so it is worth spending time following how this simple AT function works.

If you send the string AT\r\n then the ESP8266 replies with a single "OK". This proves that the serial interface is working and there isn't much point in moving on until you have tested it works.