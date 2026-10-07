
Notice that this is an inverting buffer, but you can usually ignore this and simple correct by inverting in software, i.e. read a 1 as low and a 0 as a high state. The role of R1 is to make sure the 5V signal is absent and R2 limits the current in the FET to about 0.3mA. In most cases, you should try the simple voltage divider and only move to an active buffer if it doesn't work.

## How Fast Can We Measure?

The simplest way to find out how quickly we can take a measurement using micro-bit is to perform a pulse width measurement using a busy wait. Applying a square wave to P0 we can measure the time that the pulse is high:

```cpp
#include "MicroBit.h"

MicroBit uBit;
int main()
{
  int i;
  uBit.init();
  while (1)
  {
    while (i == 1) uBit.io.P0.getDigitalValue();
    while (i == 0) uBit.io.P0.getDigitalValue();
    for (i = 0; i < 1000; i++) {
      if (i == 0) uBit.io.P0.getDigitalValue()) break;
    }
    uBit.serial.printf("%d\n\r", i);
  }
}
```

This might look a little strange at first. The inner while loops are responsible for getting us to the right point in the waveform. We first loop until the line go low, then we loop until it goes high again, and finally we measure how long before it goes low. You might think that we simply have to wait for it to go high and then measure how long it goes low, but this misses the possibility that the signal might be part way through a high period when we first measure it.

The second new aspect of the program is that we use printf to get the information. This is a print function associated with the serial driver. It is modeled on the standard C printf function, but it only supports a limited number of data types. You can only use %c, %d, %s, %x and %X.

In this case we are using the default USB serial interface to get information out of the micro:bit. This is also useful for debugging. To see the data you need to connect a serial terminal – PuTTY for example. The default configuration is:
Baud rate = 115200
Data = 8 bits
Parity = none
Stop = 1 bit

The only problem you have is finding the correct serial port to connect to and it is usually the only USB COM port listed. If you can't find a COM serial port then you might have to install the mbed serial driver:
https://os.mbed.com/docs/mbed-os/v5.14/tutorials/windows-serial-driver.html

The web page says that it shouldn't be used with Windows 10, but in practice it has proved necessary for the V1 microbit and once installed it works with the V2 micro:bit.

If you run this program with different pulse widths the result are very regular: In the chart loop count is on the y-axis, pulse time on the x-axis. The equation relating time t in microseconds and loop count n is:

![](img/23976341c9281123e7b181beea6e9dbd_52_0.png)

V1 t = 4.88 n + 3.38
V2 t = 0.85*n + 3.69

This works down to about 10µs or slightly less.

```cpp
If you want to record the time directly in microseconds, rather than using a loop count you could use:
#include "MicroBit.h"
```

```cpp
MicroBit uBit;
int main()
{
    uBit.init();
    uint64_t t;

    volatile int i;

    while (1)
    {
        while (1 == uBit.P0.getDigitalValue());
        while (0 == uBit.P0.getDigitalValue());
        t = system_timer_current_time_us();
        for (i = 0; i < 1000; i++) {
            if (0 == uBit.P0.getDigitalValue())
                break;
        }
        t = system_timer_current_time_us() - t;
        uBit.serial.printf("%d,%d\n\r", i, (int)t);
    }
}
```

This is accurate to around 10µs.
In either case, if you try measuring pulse widths shorter than the lower limit that works, you will get results that look if longer pulses are being applied. The reason is simple that the micro:bit will miss the first transition to zero but will detect a second or third or later transition. This is the digital equivalent of the aliasing effect found in the Fourier transform or general signal processing.

## Interrupts

There is a general feeling that real-time programming and interrupts go together and if you are not using an interrupt you are probably doing something wrong. In fact, if you are using an interrupt you are probably doing something wrong. Some organizations agree with the general idea that interrupts are dangerous to the extent they ban them altogether, and this includes real-time software.

In the case of the microbit we have a system of events that stand in a software wrapping of the raw system interrupts that are available if you dig just a little deeper.
As far as GPIO lines are concerned you can determine how events occur using one of four settings. The most useful is the on-edge setting, which fires an event if a GPIO line transitions from high to low or low to high.

```cpp
int eventOn(int eventType)
```

where eventType is one of:

| MICROBIT_PIN_EVENT_ON | Fire on rising or falling edge as specified when event registered |
| MICROBIT_PIN_ON_PULSE | Fire if pin is high or low as set when event registered |
| MICROBIT_PIN_EVENT_TOUCH | Fire if pin touched |
| MICROBIT_PIN_EVENT_NONE | Disable events for this pin |

As far as GPIO lines are concerned you can determine how events occur using one of four settings. The most useful is the on-edge setting, which fires an event if a GPIO line transitions from high to low or low to high.

```cpp
int eventOn(int eventType)
```

where eventType is one of:

| MICROBIT_PIN_EVENT_ON | Fire on rising or falling edge as specified when event registered |
| MICROBIT_PIN_ON_PULSE | Fire if pin is high or low as set when event registered |
| MICROBIT_PIN_EVENT_TOUCH | Fire if pin touched |
| MICROBIT_PIN_EVENT_NONE | Disable events for this pin |

The second new aspect of the program is that we use printf to get the information. This is a print function associated with the serial driver. It is modeled on the standard C printf function, but it only supports a limited number of data types. You can only use %c, %d, %s, %x and %X.

In this case we are using the default USB serial interface to get information out of the micro:bit. This is also useful for debugging. To see the data you need to connect a serial terminal – PuTTY for example. The default configuration is:
Baud rate = 115200
Data = 8 bits
Parity = none
Stop = 1 bit

[Wait, re-ordering based on logical flow below]

This is accurate to around 10µs.
In either case, if you try measuring pulse widths shorter than the lower limit that works, you will get results that look if longer pulses are being applied. The reason is simple that the micro:bit will miss the first transition to zero but will detect a second or third or later transition. This is the digital equivalent of the aliasing effect found in the Fourier transform or general signal processing.

## Interrupts

There is a general feeling that real-time programming and interrupts go together and if you are not using an interrupt you are probably doing something wrong. In fact, if you are using an interrupt you are probably doing something wrong. Some organizations agree with the general idea that interrupts are dangerous to the extent they ban them altogether, and this includes real-time software.

In the case of the microbit we have a system of events that stand in a software wrapping of the raw system interrupts that are available if you dig just a little deeper.
As far as GPIO lines are concerned you can determine how events occur using one of four settings. The most useful is the on-edge setting, which fires an event if a GPIO line transitions from high to low or low to high.

```cpp
int eventOn(int eventType)
```

where eventType is one of:

| MICROBIT_PIN_EVENT_ON | Fire on rising or falling edge as specified when event registered |
| MICROBIT_PIN_ON_PULSE | Fire if pin is high or low as set when event registered |
| MICROBIT_PIN_EVENT_TOUCH | Fire if pin touched |
| MICROBIT_PIN_EVENT_NONE | Disable events for this pin |

The second new aspect of the program is that we use printf to get the information. This is a print function associated with the serial driver. It is modeled on the standard C printf function, but it only supports a limited number of data types. You can only use %c, %d, %s, %x and %X.

[Wait, the OCR text has some repetitive/scrambled sections at the end. I will provide clean reconstruction based on the provided text blocks.]

*(Self-correction: The provided OCR text contains significant overlapping and repetition in the later pages (54-56). I will clean up the mess while following the content flow provided.)*

[content]
Notice that this is an inverting buffer, but you can usually ignore this and simple correct by inverting in software, i.e. read a 1 as low and a 0 as a high state. The role of R1 is to make sure the 5V signal is absent and R2 limits the current in the FET to about 0.3mA. In most cases, you should try the simple voltage divider and only move to an active buffer if it doesn't work.

## How Fast Can We Measure?

The simplest way to find out how quickly we can take a measurement using micro-bit is to perform a pulse width measurement using a busy wait. Applying a square wave to P0 we can measure the time that the pulse is high:

```cpp
#include "MicroBit.h"

MicroBit uBit;
int main()
{
  int i;
  uBit.init();
  while (1)
  {
    while (i == 1) uBit.io.P0.getDigitalValue();
    while (i == 0) uBit.io.P0.getDigitalValue();
    for (i = 0; i < 1000; i++) {
      if (i == 0) uBit.io.P0.getDigitalValue())
        break;
    }
    uBit.serial.printf("%d\n\r", i);
  }
}
```

This might look a little strange at first. The inner while loops are responsible for getting us to the right point in the waveform. We first loop until the line go low, then we loop until it goes high again, and finally we measure how long before it goes low. You might think that we simply have to wait for it to go high and then measure how long it goes low, but this misses the possibility that the signal might be part way through a high period when we first measure it.

The second new aspect of the program is that we use printf to get the information. This is a print function associated with the serial driver. It is modeled on the standard C printf function, but it only supports a limited number of data types. You can only use %c, %d, %s, %x and %X.

In this case we are using the default USB serial interface to get information out of the micro:bit. This is also useful for debugging. To see the data you need to connect a serial terminal – PuTTY for example. The default configuration is:
- Baud rate = 115200
- Data = 8 bits
- Parity = none
- Stop = 1 bit

The only problem you have is finding the correct serial port to connect to and it is usually the only USB COM port listed. If you can't find a COM serial port then you might have to install the mbed serial driver:
https://os.mbed.com/docs/mbed-os/v5.14/tutorials/windows-serial-driver.html

The web page says that it shouldn't be used with Windows 10, but in practice it has proved necessary for the V1 microbit and once installed it works with the V2 micro:bit.

If you run this program with different pulse widths the result are very regular: In the chart loop count is on the y-axis, pulse time on the x-axis. The equation relating time t in microseconds and loop count n is:

![](img/23976341c9281123e7b181beea6e9dbd_52_0.png)

V1 t = 4.88 n + 3.38
V2 t = 0.85*n + 3.69

This works down to about 10µs or slightly less.

```cpp
If you want to record the time directly in microseconds, rather than using a loop count you could use:
#include "MicroBit.h"
```

```cpp
MicroBit uBit;
int main()
{
    uBit.init();
    uint64_t t;

    volatile int i;

    while (1)
    {
        while (1 == uBit.P0.getDigitalValue());
        while (0 == uBit.P0.getDigitalValue());
        t = system_timer_current_time_us();
        for (i = 0; i < 1000; i++) {
            if (0 == uBit.P0.getDigitalValue())
                break;
        }
        t = system_timer_current_time_us() - t;
        uBit.serial.printf("%d,%d\n\r", i, (int)t);
    }
}
```

This is accurate to around 10µs. In either case, if you try measuring pulse widths shorter than the lower limit that works, you will get results that look if longer pulses are being applied. The reason is simple that the micro:bit will miss the first transition to zero but will detect a second or third or later transition. This is the digital equivalent of the aliasing effect found in the Fourier transform or general signal processing.

## Interrupts

There is a general feeling that real-time programming and interrupts go together and if you are not using an interrupt you are probably doing something wrong. In fact, if you are using an interrupt you are probably doing something wrong. Some organizations agree with the general idea that interrupts are dangerous to the extent they ban them altogether, and this includes real-time software.

In the case of the microbit we have a system of events that stand in a software wrapping of the raw system interrupts that are available if you dig just a little deeper.
As far as GPIO lines are concerned you can determine how events occur using one of four settings. The most useful is the on-edge setting, which fires an event if a GPIO line transitions from high to low or low to high.

```cpp
int eventOn(int eventType)
```

where eventType is one of:

| Constant | Description |
| :--- | :--- |
| MICROBIT_PIN_EVENT_ON | Fire on rising or falling edge as specified when event registered |
| MICROBIT_PIN_ON_PULSE | Fire if pin is high or low as set when event registered |
| MICROBIT_PIN_EVENT_TOUCH | Fire if pin touched |
| MICROBIT_PIN_EVENT_NONE | Disable events for this pin |
