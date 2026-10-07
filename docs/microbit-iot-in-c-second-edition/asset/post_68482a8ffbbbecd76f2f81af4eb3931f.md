
# Appendix I
The Mbed Online Compiler 247

Hello Blinky................................................................................248

# Appendix II
Yotta And Offline Development 251

Build Systems...............................................................................251

How Yotta Works........................................................................252

Installing Yotta.........................................................................................253

Creating a Micro:bit Project.......................................................255

Adding a Dependency on the Micro:bit Library...............................256

Summary of Project Creation.......................................................259

# Chapter 1

## The Micro-bit Family

The micro:bit is an interesting and low-cost device. It was originally launched, under the auspices of the BBC, in 2015 when plans were announced to distribute around one million devices, free of charge, to school pupils in the UK with the aim of extending the digital technology and coding skills. The first commercial version hit the market in 2016, by which time the Micro:bit Educational Foundation had taken over from the BBC, although the device continued to use the BBC name. The micro:bit V2 made its debut at the end of 2020 and, as well as being more powerful and having more features, was based on a different microprocessor.

The micro:bit is supported by a number of high-level languages which are primarily used for educational apps and for classroom. However, the underlying device is programmed in a mix of C and C++. Working at this level is generally not something that many take on and it isn't as easy as say, programming in Python. Although it is more difficult to get started with C/C++ than other languages, the effort is worth it and if you want to use the micro:bit in IoT or embedded applications then C is by far the best choice. Programming the micro:bit in C is the subject of the rest of this book, but first let's take a look at the micro:bit itself and find out what makes it attractive and what the problems are.

## Meet the Micro:bits

To date there are three versions of the micro:bit - V1.3, V1.5 and V2. The differences between V1.3 and V1.5 are small and relate to the addresses for some of the peripherals. You can program the 1.3 and 1.5 using the same tools and software mostly you can regard them as the same device, collectively referred to as micro:bit V1 in this book. The V2 is comparatively recent and not only has additional and different hardware, also uses different software and this is something of a problem.

You can compare the specifications of the V1 and the V2 in these diagrams:

### V1.3 and V1.5

![](img/23976341c9281123e7b181beea6e9dbd_11_0.png)

- Micro USB
- MSC, UART, CMIS-DAP
- Drag-and-drop programming
- 5x5 LED Matrix
- Digital/analog IO
- Mixable to SPI, UART, I2C
- Pads for crocodile clips
- Holes for banana plugs
- FRONT
- User buttons
- External supply
- Regulated 3.3V in or battery out
- Edge Connector

![](img/23976341c9281123e7b181beea6e9dbd_11_1.png)

- V2GHZ
- Bluetooth low energy
- Broadcast radio
- Nordic nRF51822
- Magnetometer
- Freescale MAG3110
- Accelerometer
- Freescale MMA8653FC
- Battery connector
- JST connection for 3V
- Reset Button
- Freescale KL26Z
- USB Interface chip

| Model | Nordic nRF51822-QFAA-R rev 3 |
|---|---|
| Core variant | Arm Cortex-M0 32-bit processor |
| Flash ROM | 256KB |
| RAM | 16KB |
| Speed | 16MHz |

The two variants have the same CPU, ROM and RAM, but differ in their peripheral chips.

### V2

![](img/23976341c9281123e7b181beea6e9dbd_12_0.png)

- Touch sensitive logo
- Micro USB
- Front
- Microphone
- LED indicator
- Microphone
- 5x5 LED matrix
- External supply
- Mixable to SPI, UART, I2C
- Pads for crocodile clips
- Holes for banana plugs
- User buttons
- Regulated 3.3V in or battery out
- Edge Connector
- Bluetooth low energy
- Broadcast radio
- Nordic nRF51822
- Magnetometer
- Freescale MAG3110
- Accelerometer
- Freescale MMA8653FC
- Battery connector
- JST connection for 3V
- Reset Button
- Freescale KL26Z
- USB Interface chip

| Model | Nordic nRF51822-QFAA-R rev 3 |
|---|---|
| Core variant | Arm Cortex-M4 with FPU |
| Flash ROM | 512KB |
| RAM | 128KB |
| Speed | 64MHz |

The two variants have the same CPU, ROM and RAM, but differ in their peripheral chips.

## Why Choose a Micro:bit?

The first thing to explain is that the micro:bit is an mbed device. Mbed is a project started by Arm to promote the 32-bit ARM Cortex-M as an IoT device. The mbed operating system is designed to make a range of ARM-based devices work in the same way. It is a low-level operating system that provides uniform access to hardware. The V1 micro:bit uses mbed version 2, which has now been deprecated. It also has to be said that the micro:bit never really seemed a good fit with the more professional devices it was sharing the mbed website with. Today support for the micro:bit still exists, but it hasn't been upgraded and isn't likely to be. The newer mbed tools, such as the offline development tool, Mbed Studio, don't support the micro:bit and even finding the micro:bit page, if you don't know where it is, is difficult.

## Software

The software used by the V1 isn't simple. The mbed operating system sits on top of a lower-level library that works with the hardware, the NRF5 SDK, and on top of it is CODAL (Component Oriented Device Abstraction Layer), a library created by Lancaster University to provide a higher level access to the devices. The latest V2 micro:bit is no longer an mbed device and the CODAL software has grown to replace mbed.
