
Notice that the read returns immediately in ASYNC mode. If you select any of the other modes then it only returns when a character is received. In this case you don't need the if statement to test for a result. However, if the device you are connecting to never sends a character, the loop hangs forever.

## Using Events

There is a tendency among IoT programmers to use interrupts too often. They are useful when you need to deal with a low-priority event that occurs very rarely. For something that is important and very frequent, you usually need to use a polling loop to keep up. You still need to know how to use events to work with the serial port and there are some tricky things you have to get right.

There are two event sources that you can control:

- * int eventAfter(int len)
- * int eventAfter(int len, MicroBitSerialMode)

which trigger an event if there are the specified number of characters in the receive buffer, in addition there are another two:

- * int eventOn(ManagedString delimiters)
- * int eventOn(ManagedString delimiters, MicroBitSerialMode)

which trigger an event if any of the specified delimiters are present in the receive buffer.

There are two things to notice when using these events. The first is that, at the moment, the framework does not allocate buffers until you have actually used the serial device. What this means is that you can set up a program that looks reasonable but never fires an event because the receive buffer is never created. The second problem is that these events only fire once.

Both events have an ID of:

```
MICROBIT_ID_SERIAL
```

and respective values:

```
MICROBIT_SERIAL_EVT_HEAD_MATCH
MICROBIT_SERIAL_EVT_DELIM_MATCH
```

Notice that you can use the usual modes but SPINWAIT will return an error and SLEEP will pause the fiber and wait for the event.

As an example of using serial events let's write a program that simply copies characters to the LED display. The event handler is just:

```cpp
void onChar(MicroBitEvent e) {
  ManagedString s = uBit.serial.read(1);
  uBit.serial.clearRxBuffer();
  uBit.display.scroll(s);
  uBit.serial.eventAfter(1);
}
```

The main program is:

```cpp
#include "MicroBit.h"
//define baud setBaudrate //uncomment for V2
MicroBit uBit;
int main() {
  uBit.init();
  uBit.serial(20);
  uBit.messageBus.listen(MICROBIT_ID_SERIAL, MICROBIT_SERIAL_EVT_HEAD_MATCH, onChar);
  uBit.serial.eventAfter(1);
  while (1) uBit.sleep(1000);
  release_fiber();
}
```

Notice that we use a setRxBufferSize size to make the framework actually create a buffer. The eventAfter function sets the event ready to happen and the while(1) sleep-keeps the fiber running while waiting for the event. Alternatively you could simply release the fiber and let the scheduler call the event handler.

The event handler is simple enough, but notice that we have to reset the event to happen a second time. These features of the framework might change well in future versions.

## Problems With Serial

The biggest problem with using micro:bit serial is that, even though you can connect to it to GPIO lines, there is only one serial hardware device, i.e. one UART. A standard problem when trying to multiplex between different lines is that, when the switch happens, the Rx and Tx buffers are swapped to the new pins. For example, suppose you are connected to a device on pins 0 and 1 and suddenly switch the UART to USB. If there was data coming in on pin 1 switching pins will cause all sorts of problems as it alters the transfer and can crash the microbit V1.

In general, you have to make sure that all data traffic has stopped before you switch pins. You might think this is an easy task, but it can be very difficult because of the use of ASYNC and SLEEP, which can allow your fiber to do things while data is being received or transmitted.

## Summary

- The serial port is one of the oldest ways of connecting devices together, but it is still very much in use.
- The serial protocol is asynchronous, but simple. A start bit gives the timing for the entire exchange.
- There are many control lines, once used with telephone equipment, that are mostly ignored in computer use. Similarly, the original ±12V signaling has been mostly replaced by 5V, and even 3.3V.
- The standard hardware that implements a serial connection is usually called a UART. The microbit has a single UART.
- You can create a MicroBitSerial object or just the one provided by the uBit connected to the USB port.
- To change the uBit to another port you need to use redirect.
- You can use event handling to deal with serial port input.

## Chapter 13
### Getting On WiFi

The micro:bit has a radio that has two modes, Bluetooth LE and ad-hoc point-to-point ad-hoc but it lacks WiFi connectivity. One solution is to use the low cost ESP8266 to make the connection via the micro-bit's serial port. As we will make a lot of use of the micro:bit's serial port it is assumed that you know roughly how it works. In particular, it is assumed that you are familiar with the material in the previous chapter. Before we get on to the details of using the ESP8266 need to find out what makes it special.

## The Amazing ESP8266

The ESP8266 is a very odd and amazing device. It is remarkably low cost, $5 or less, it is a full microprocessor with GPIOs inline, RAM and built in WiFi. It is built by a Chinese company Espressif Systems but there are a number of copies on the market. The proliferation of devices and software revisions makes it difficult to work with, but it is well worth the effort.

The module used in this chapter is the ESP8266 ESP-01 which is widely available from many different sources but they all look alike:

![](img/23976341c9281123e7b181beea6e9dbd_190_0.png)

Another version, the ESP-07, which comes with a screened RF stage and other advantages, should also work.

While you can set up a development system yourself and program the ESP8266 to do almost anything, it comes with built-in software that allows it to be used as WiFi. This is how we give the microbit WiFi capability. The ESP8266 connects to the microbit using the serial port.

## Connecting the ESP8266 ESP-01

There are a number of minor problems in using the device. The first is that it comes with an 8-pin male connector which is not prototype-friendly. The best solution to this is to use some female-to-male cables to connect it to the prototype board, or use female-to-female cables to connect directly to the microbit. A second problem is caused by the fact that the device is powered from 3.3V. This might tempt you to try to power it from the microbit's 3.3V supply. **This will not work.** The ESP8266 takes a lot of current, 300mA or so, when transmitting. The microbit cannot supply this current. You need to use a separate 3.3V power supply. Of course, you can use this to power both the ESP266 and the microbit and in some situations this would be an advantage.

![](img/23976341c9281123e7b181beea6e9dbd_191_0.png)

The pinout of the ESP-01 is usually shown from the component side, but in fact the pins that you want to connect are on the other side. To make things easier the two views are given in the diagram:

![](img/23976341c9281123e7b181beea6e9dbd_192_0.png)

The pin functions are:

- 1 Ground connect to ground
- 2 TXO serial Tx pin
- 3 GPIO2 ignore
- 4 CHPD chip enable, connect to 3.3V
- 5 GPIO ignore
- 6 RST leave unconnected
- 7 RXI serial pin
- 8 VDD supply voltage, connect to 3.3V

From the pinouts you should be able to work out how the ESP266 has to be connected to the microbit. If we use P0 as Tx from the micro-bit and P1 as Rx to the micro-bit we have to connect ESP-01 pin 7 to P0, pin 2 to P1 and ESP-01 pins 8 and 4 to the external power supply. To make it all work we also have to connect ESP-01 pin 1 to the ground of the external power supply ground and to the ground of the microbit, as shown:

![](img/23976341c9281123e7b181beea6e9dbd_192_1.png)
