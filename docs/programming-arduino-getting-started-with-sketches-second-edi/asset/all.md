![](images/cover.jpg)

![Cover](images/cover.jpg)

**Library of Congress Control Number: 2016938700**

McGraw-Hill Education books are available at special quantity discounts to use as premiums and sales promotions or for use in corporate training programs. To contact a representative, please visit the Contact Us page at [www.mheducation.com](http://www.mheducation.com).

**Programming Arduino™: Getting Started with Sketches, Second Edition**

Copyright © 2016, 2012 by McGraw-Hill Education. All rights reserved. Printed in the United States of America. Except as permitted under the United States Copyright Act of 1976, no part of this publication may be reproduced or distributed in any form or by any means, or stored in a database or retrieval system, without the prior written permission of the publisher, with the exception that the program listings may be entered, stored, and executed in a computer system, but they may not be reproduced for publication.

McGraw-Hill Education, the McGraw-Hill Education logo, TAB, and related trade dress are trademarks or registered trademarks of McGraw-Hill Education and/or its affiliates in the United States and other countries and may not be used without written permission. All other trademarks are the property of their respective owners. McGraw-Hill Education is not associated with any product or vendor mentioned in this book.

Arduino is a trademark of Arduino LLC.

1 2 3 4 5 6 7 8 9  DOC  21 20 19 18 17 16

ISBN 978-1-25-964163-3

MHID 1-25-964163-5

This book is printed on acid-free paper.

**Sponsoring Editor**

Michael McCabe

**Editorial Supervisor**

Stephen M. Smith

**Production Supervisor**

Pamela A. Pelton

**Acquisitions Coordinator**

Lauren Rogers

**Project Manager**

Srishti Malasi,
Cenveo^® Publisher Services

**Copy Editor**

Claire Splan

**Proofreader**

Cenveo Publisher Services

**Indexer**

Jack Lewis

**Art Director, Cover**

Jeff Weeks

**Illustration**

Cenveo Publisher Services

**Composition**

Cenveo Publisher Services

Information has been obtained by McGraw-Hill Education from sources believed to be reliable. However, because of the possibility of human or mechanical error by our sources, McGraw-Hill Education, or others, McGraw-Hill Education does not guarantee the accuracy, adequacy, or completeness of any information and is not responsible for any errors or omissions or the results obtained from the use of such information.

*To my boys, Stephen and Matthew, from a very proud Dad.*

## About the Author

**Simon Monk** has a bachelor’s degree in cybernetics and computer science and a doctorate in software engineering. He has been an active electronics hobbyist since his school days and is an occasional author in hobby electronics magazines. Dr. Monk is also author of some 20 books on Maker and electronics topics, especially Arduino and Raspberry Pi. You can find out more about his books at [http://simonmonk.org](http://simonmonk.org). You can also follow him on Twitter, where he is @simonmonk2.

## PREFACE

The first edition of this book was published in November 2011 and has been Amazon’s highest ranking book on Arduino.

At the time the book was originally written, the current Arduino model was the Arduino 2009 and the software version was Beta018\. Almost at the time the book arrived in stores, the Arduino Uno and version 1.0 of the Arduino software were released. Soon after, the second printing of the book had a minor update to cover the new board and software without formally being a second edition. This edition brings the book fully up to date and is based on Arduino 1.6.

The Arduino Uno R3 is still considered to be the standard Arduino board. However, many other boards, including both official Arduino boards (like the Leonardo, Zero, 101, Due, and Yun) and other Arduino programming language–based devices like the Photon and Intel Edison, have also appeared.

This edition also addresses the use of Arduino in IoT (Internet of Things) projects and the use of various types of display including OLED and LCD.

*Simon Monk*

## ACKNOWLEDGMENTS

I thank Linda for giving me the time, space, and support to write this book and for putting up with the various messes my projects create around the house.

Many thanks to Robert “BobKat” Logan and the many other eagle-eyed and helpful folk who reported errata for the first edition. I have done my best to fix what you found.

Finally, I would like to thank Michael McCabe, Srishti Malasi, and everyone involved in the production of this book. It’s a pleasure to work with such a great team.

## INTRODUCTION

Arduino interface boards provide a low-cost, easy-to-use technology to create microcontroller-based projects. With a little electronics, you can make your Arduino do all sorts of things, from controlling lights in an art installation to managing the power on a solar energy system.

There are many project-based books that show you how to connect things to your Arduino, including *30 Arduino Projects for the Evil Genius* by this author. However, the focus of this book is on programming the Arduino.

This book will explain how to make programming the Arduino simple and enjoyable, avoiding the difficulties of uncooperative code that so often afflict a project. You will be taken through the process of programming the Arduino step by step, starting with the basics of the C programming language that Arduinos use.

* * *

### So, What Is Arduino?

Arduino is a small microcontroller board with a universal serial bus (USB) plug to connect to your computer and a number of connection sockets that can be wired to external electronics such as motors, relays, light sensors, laser diodes, loudspeakers, microphones, and more. They can be powered either through the USB connection from the computer, from a 9V battery, or from a power supply. They can be controlled from the computer or programmed by the computer and then disconnected and allowed to work independently.

The board design is open source. This means that anyone is allowed to make Arduino-compatible boards. This competition has led to low costs for the boards and all sorts of variations on the “standard” boards.

The basic boards are supplemented by accessory shield boards that can be plugged on top of the Arduino board.

The software for programming your Arduino is easy to use and also freely available for Windows, Mac, and Linux computers.

* * *

### What Will I Need?

This is a book intended for beginners, but it is also intended to be useful to those who have used Arduino for a while and want to learn more about programming the Arduino or gain a better understanding of the fundamentals. As such, this book concentrates on the use of the Arduino Uno board; however, almost all of the code will work unmodified on all the Arduino models and variants.

You do not need to have any programming experience or a technical background, and the book’s exercises do not require any soldering. All you need is the desire to make something.

If you want to make the most of the book and try out some of the experiments, then it is useful to have the following on hand:

♦ A few lengths of solid core wire

♦ A cheap digital multimeter

Both are readily available for a few dollars from a hobby electronics store or online retailer such as Adafruit or Sparkfun. You will of course also need an Arduino Uno board.

If you want to go a step further and experiment with displays and network connections, then you will need to buy shields that are available from online stores. See [Chapters 9](#18_Chapter_09.xhtml) and [10](#19_Chapter_10.xhtml) for details.

* * *

### Using This Book

This book is structured to get you started in a really simple way and gradually build on what you have learned. You may, however, find yourself skipping or skimming some of the early chapters as you find the right level to enter the book.

The book is organized into the following chapters:

♦ **Chapter 1: This Is Arduino** An introduction to the Arduino hardware, this chapter describes what it is capable of and the various types of Arduino boards that are available.

♦ **Chapter 2: Getting Started** Here you conduct your first experiments with your Arduino board: installing the software, powering it up, and uploading your first sketch.

♦ **Chapter 3: C Language Basics** This chapter covers the basics of the C language; for complete programming beginners, the chapter also serves as an introduction to programming in general.

♦ **Chapter 4: Functions** This chapter explains the key concept of using and writing functions in Arduino sketches. These sketches are demonstrated throughout with runnable code examples.

♦ **Chapter 5: Arrays and Strings** Here you learn how to make and use data structures that are more advanced than simple integer variables. A Morse code example project is slowly developed to illustrate the concepts being explained.

♦ **Chapter 6: Input and Output** You learn how to use the digital and analog inputs and outputs on the Arduino in your programs. A multimeter will be useful to show you what is happening on the Arduino’s input/output connections.

♦ **Chapter 7: The Standard Arduino Library** This chapter explains how to make use of the standard Arduino functions that come in the Arduino’s standard library.

♦ **Chapter 8: Data Storage** Here you learn how to write sketches that can save data in electrically erasable read-only memory (EEPROM) and make use of the Arduino’s built-in flash memory.

♦ **Chapter 9: Displays** In this chapter, you learn how to interface an Arduino with displays and to make a simple USB message board.

♦ **Chapter 10: Arduino Internet of Things Programming** You learn how to make the Arduino behave like a Web server and communicate with the Internet using services such as dweet and IFTTT.

♦ **Chapter 11: C++ and Libraries** You go beyond C, looking at adding object orientation and writing your own Arduino libraries.

* * *

### Resources

This book is supported by an accompanying website:

[www.arduinobook.com](http://www.arduinobook.com)

There you will find all the source code used in this book as well as other resources, such as errata.

## 1

## This Is Arduino

Arduino is a microcontroller platform that has captured the imagination of electronics enthusiasts. Its ease of use and open source nature make it a great choice for anyone wanting to build electronic projects.

Ultimately, it allows you to connect electronics through its pins so that it can control things—for instance, turn lights or motors on and off or sense things such as light and temperature. This is why Arduino is sometimes given the description *physical computing.* Because Arduinos can be connected to your computer by a universal serial bus (USB) lead, this also means that you can use the Arduino as an interface board to control those same electronics from your computer.

This chapter is an introduction to the Arduino, including the history and background of the Arduino, as well as an overview of the hardware.

* * *

### Microcontrollers

The heart of your Arduino is a microcontroller. Pretty much everything else on the board is concerned with providing the board with power and allowing it to communicate with your desktop computer.

A microcontroller really is a little computer on a chip. It has everything and more than the first home computers had. It has a processor, a kilobyte or two of random access memory (RAM) for holding data, a few kilobytes of erasable programmable read-only memory (EPROM) or flash memory for holding your programs and it has input and output pins. These input/output (I/O) pins link the microcontroller to the rest of your electronics.

Inputs can read both digital (is the switch on or off?) and analog (what is the voltage at a pin?). This opens up the opportunity of connecting many different types of sensor for light, temperature, sound, and more.

Outputs can also be analog or digital. So, you can set a pin to be on or off (0 volts or 5 volts) and this can turn light-emitting diodes (LEDs) on and off directly, or you can use the output to control higher power devices such as motors. They can also provide an analog output. That is, you can control the power output of a pin, allowing you to control the speed of a motor or the brightness of a light, rather than simply turning it on or off.

The microcontroller on an Arduino Uno board is the 28-pin chip fitted into a socket at the center of the board. This single chip contains the memory, processor, and all the electronics for the input/output pins. It is manufactured by the company Atmel, which is one of the major microcontroller manufacturers. Each of the microcontroller manufacturers actually produces dozens of different microcontrollers grouped into different families. The microcontrollers are not all created for the benefit of electronics hobbyists like us. We are a small part of this vast market. These devices are really intended for embedding into consumer products, including cars, washing machines, DVD players, children’s toys, and even air fresheners.

The great thing about the Arduino is that it reduces this bewildering array of choices by standardizing on one microcontroller and sticking with it. (Well, as we see later, this statement is not quite true, but it’s close enough.)

This means that when you are embarking on a new project, you do not first need to weigh all the pros and cons of the various flavors of microcontroller.

#### Development Boards

We have established that the microcontroller is really just a chip. A chip microcontroller will not just work on its own without some supporting electronics to provide it with a regulated and accurate supply of electricity (microcontrollers are fussy about this) as well as a means of communicating with the computer that is going to program the microcontroller.

This is where development boards come in. An Arduino Uno board is really a microcontroller development board that happens to be an independent open source hardware design. This means that the design files for the printed circuit board (PCB) and the schematic diagrams are all publicly available, and everyone is free to use the designs to make and sell his or her own Arduino boards.

All the microcontroller manufacturers—including Atmel, which makes the ATmega328 microcontroller used in an Arduino board—also provide their own development boards and programming software. Although they are usually fairly inexpensive, these tend to be aimed at professional electronics engineers rather than hobbyists. This means that such boards and software are arguably harder to use and require a greater learning investment before you can get anything useful out of them.

* * *

### A Tour of an Arduino Board

[Figure 1-1](#10_Chapter_01.xhtml_fig-ch1-1) shows an Arduino Uno board. Let’s take a quick tour of the various components on the board.

![image](images/fig-ch1-1.jpg)

Figure 1.1 *An Arduino Uno board*.

#### Power Supply

Referring to [Figure 1-1](#10_Chapter_01.xhtml_fig-ch1-1), directly below the USB connector is the 5-volt (5V) voltage regulator. This regulates whatever voltage (between 7V and 12V) is supplied from the DC power socket into a constant 5V.

The 5V voltage regulator chip is actually quite big for a surface mount component. This is so that it can dissipate the heat required to regulate the voltage at a reasonably high current. This is useful when driving external electronics.

Although powering the Arduino through the DC power socket is useful when running the Arduino from batteries or a DC power jack, the Arduino Uno can also be powered through the USB port, which is also used to program the Arduino.

#### Power Connections

Next let us look at the connectors at the bottom of [Figure 1-1](#10_Chapter_01.xhtml_fig-ch1-1). You can read the connection names next to the connectors. The connector of interest is Reset. This does the same thing as the Reset button on the Arduino. Rather like rebooting a PC, using the Reset connector resets the microcontroller so that it begins its program from the start. To reset the microcontroller with the Reset connector, you momentarily set this pin low (connecting it to 0V).

The rest of the pins in this section just provide different voltages (3.3V, 5V, GND, and Vin), as they are labeled. GND, or ground, just means zero volts. It is the reference voltage to which all other voltages on the board are relative.

#### Analog Inputs

The six pins labeled as Analog In A0 to A5 can be used to measure the voltage connected to them so that the value can be used in a sketch (Arduino Program). Note that they measure a voltage and not a current. Only a tiny current will ever flow into them and down to ground because they have a very large internal resistance. That is, the pin having a large internal resistance only allows a tiny current to flow into the pin.

Although these inputs are labeled as analog, and are analog inputs by default, these connections can also be used as digital inputs or outputs.

#### Digital Connections

We now switch to the top connector and start on the right-hand side in [Figure 1-1](#10_Chapter_01.xhtml_fig-ch1-1). Here we find pins labeled Digital 0 to 13\. These can be used as either inputs or outputs. When used as outputs, they behave rather like the power supply voltages discussed earlier in this section, except that these are all 5V and can be turned on or off from your sketch. So, if you turn them on from your sketch they will be at 5V, and if you turn them off they will be at 0V. As with the power supply connectors, you must be careful not to exceed their maximum current capabilities. The first two of these connections (0 and 1) are also labeled RX and TX, for receive and transmit. These connections are reserved for use in communication and are indirectly the receive and transmit connections for your USB link to your computer.

These digital connections can supply 40 mA (milliamps) at 5V. That is more than enough to light a standard LED, but not enough to drive an electric motor directly.

#### Microcontroller

Continuing our tour of the Arduino board, the microcontroller chip itself is the black rectangular device with 28 pins. This is fitted into a dual in-line (DIL) socket so that it can be easily replaced. The 28-pin microcontroller chip used on the Arduino Uno board is the ATmega328\. [Figure 1-2](#10_Chapter_01.xhtml_fig-ch1-2) presents a block diagram showing the main features of this device.

![image](images/fig-ch1-2.jpg)

Figure 1.2 *ATmega328 block diagram*.

The heart—or, perhaps more appropriately, the brain—of the device is the central processing unit (CPU). It controls everything that goes on within the device. It fetches program instructions stored in the flash memory and executes them. This might involve fetching data from working memory (RAM), changing it, and then putting it back. Or, it may mean changing one of the digital outputs from 0V to 5V.

The EEPROM memory is a little like the flash memory in that it is non-volatile. That is, you can turn the device off and on and it will not have forgotten what is in the EEPROM. Whereas the flash memory is intended for storing program instructions (from sketches), the EEPROM is used to store data that you do not want to lose in the event of a reset or the power being turned off.

#### Other Components

Above the microcontroller is a small, silver, rectangular component. This is a quartz crystal oscillator. It ticks 16 million times a second, and on each of those ticks, the microcontroller can perform one operation—addition, subtraction, or another mathematical operation.

In the top-left corner is the Reset switch. Clicking on this switch sends a logic pulse to the Reset pin of the microcontroller, causing the microcontroller to start its program afresh and clear its memory. Note that any program stored on the device will be retained, because this is kept in non-volatile flash memory—that is, memory that remembers even when the device is not powered.

On the right-hand edge of the board is the Serial Programming Connector. It offers another means of programming the Arduino without using the USB port. Because we do have a USB connection and software that makes it convenient to use, we will not avail ourselves of this feature.

In the top-left corner of the board next to the USB socket is the USB interface chip. This chip converts the signal levels used by the USB standard to levels that can be used directly by the Arduino board.

* * *

### The Origins of Arduino

Arduino was originally developed as an aid for teaching students. It was subsequently (in 2005) developed commercially by Massimo Banzi and David Cuartielles. It has since gone on to become enormously successful with makers, students, and artists for its ease of use and durability.

Another key factor in its success is that all the designs for Arduino are freely available under a Creative Commons license. This has allowed many lower-cost alternatives to the boards to appear. Only the name Arduino is protected, so such clones often have “*duino” names, such as Boarduino, Seeeduino, and Freeduino. In 2014 there was a falling out between the original Arduino team and their principal manufacturer. One result of this split is that you will now find that outside of the USA, the Arduino Uno is known as the Genuino Uno. Many big retailers sell only the official boards, which are nicely packaged and of high quality.

Yet another reason for the success of Arduino is that it is not limited to microcontroller boards. There are a huge number of Arduino-compatible shield boards that plug directly into the top of an Arduino board. Because shields are available for almost every conceivable application, you often can avoid using a soldering iron and instead plug together shields that can be stacked one upon another. The following are just a few of the most popular shields:

♦ Ethernet, which gives an Arduino Web-serving capabilities

♦ Motor, which drives electric motors

♦ USB Host, which allows control of USB devices

♦ Relays, which switches relays from your Arduino

[Figure 1-3](#10_Chapter_01.xhtml_fig-ch1-3) shows a motor shield (left) and relay shield (right).

![image](images/fig-ch1-3.jpg)

Figure 1.3 *Motor and relay shields*.

* * *

### The Arduino Family

It is useful to have a little background on the various Arduino boards. We will be using the Arduino Uno as our standard device—more specifically, the Arduino Uno R3 (Revision 3). Indeed, this is by far the most used of the Arduino boards, but the boards are all programmed using the same language and largely have the same connections to the outside world, so you can easily use a different board.

#### Uno and Leonardo

The Arduino Uno is just one incarnation of a long series of Arduino boards. The series includes the Diecimila (Italian for 10,000) and the Duemilanove (Italian for 2009). [Figure 1-4](#10_Chapter_01.xhtml_fig-ch1-4) shows an Arduino Leonardo. By now you may have guessed that Arduino is an Italian invention.

The Arduino Leonardo ([Figure 1-4](#10_Chapter_01.xhtml_fig-ch1-4)) is another popular choice of Arduino board and can be used in place of the Arduino Uno in most situations. It is slightly cheaper than the Uno and has the same connections as the Uno. Its processor chip is soldered onto the board and so cannot be removed (as you can an Uno’s processor.) Its lower cost is in part due to the use of a processor that includes its own USB interface rather than having to use a separate chip like the Uno.

![image](images/fig-ch1-4.jpg)

Figure 1.4 *The Arduino Leonardo*.

#### Mega and Due

The Arduino Mega is the muscle car of Arduino boards. It boasts a huge collection of input/output ports, but cleverly adds these as extra connectors at one end of the board, allowing it to remain pin-compatible with the Arduino Uno and Leonardo and all the shields available for Arduino.

It uses a processor with more input/output pins, the ATmega1280, which is a surface mount chip that is fixed permanently to the board. So, unlike with the Uno and similar boards, you cannot replace the processor if you accidentally damage it.

The extra connectors are arranged at the end of the board. Extra features provided by the Mega include the following:

♦ 54 input/output pins

♦ 128KB of flash memory for storing sketches and fixed data (compared to the Uno’s 32KB)

♦ 8KB of RAM and 4KB of EEPROM

The Arduino Due ([Figure 1-5](#10_Chapter_01.xhtml_fig-ch1-5)) has the same board size and connections as the Mega, but uses a 32-bit ARM processor running at 84MHz. It also operates at 3.3V rather than the 5V of most Arduino boards so some Arduino shields will not operate correctly.

![image](images/fig-ch1-5.jpg)

Figure 1.5 *An Arduino Due board*.

#### The Micro and Small Arduino Boards

For those situations where an Uno is too big, there are a range of smaller Arduino and Arduino-compatible boards. [Figure 1-6](#10_Chapter_01.xhtml_fig-ch1-6) shows a selection of these boards.

![image](images/fig-ch1-6.jpg)

Figure 1.6 *The Arduino Micro (left), Freetronics LeoStick (center), and Adafruit Trinket (right)*.

The Arduino Micro uses the same microcontroller as the Leonardo but is shrunk down to a more compact board. Third-party boards such as the LeoStick and Adafruit Trinket offer alternatives to the Micro.

The downside of small boards like the Micro is that because they are so much smaller than an Uno, they cannot accept Uno-sized shields.

#### Yun

The Arduino Yun ([Figure 1-7](#10_Chapter_01.xhtml_fig-ch1-7)) is essentially an Arduino Leonardo combined with a miniature WiFi module running Linux. The device is intended for Arduino applications that require a connection to the Internet. The Arduino and Linux halves of the Yun are linked using software called a bridge. The Yun is programmed using the Arduino IDE as normal, but can also be programmed wirelessly from the Arduino IDE once the Yun has been joined to your local network.

![image](images/fig-ch1-7.jpg)

Figure 1.7 *Arduino Yun*.

#### Lilypad

The Lilypad ([Figure 1-8](#10_Chapter_01.xhtml_fig-ch1-8)) is a tiny, thin Arduino board that can be stitched into clothing for applications that have become known as wearable computing.

![image](images/fig-ch1-8.jpg)

Figure 1.8 *Arduino Lilypad*.

The Lilypad does not have a USB connection, and you must use a separate adaptor to program it. It has an exceptionally beautiful design.

Adafruit also sell a board called the Flora, which is similar in concept to the Lilypad.

#### Other “Official” Boards

The previously described Arduino boards are the most useful and popular ones. However, the range of Arduino boards constantly changes, so for a complete and up-to-date picture of the Arduino family, see the official Arduino website list at [www.arduino.cc/en/Main/Hardware](http://www.arduino.cc/en/Main/Hardware).

* * *

### Arduino Clones and Variants

Unofficial boards fall into two categories. Some just take the standard open source hardware designs of Arduino and build a cheaper one. Some names you can search for boards of this nature include the following:

♦ The Sparkfun RedBoard

♦ The Adafruit Metro

♦ The Olimexino

More interestingly, some Arduino-compatible designs are intended to extend or improve the Arduino in some way. New variants are appearing all the time, and far too many exist to mention them all. However, the following are some of the more interesting and popular variants:

♦ The Node MCU board, which is based around the ESP8266 WiFi System on a chip. This provides a very low-cost solution for projects where you need a WiFi connection for your Arduino. See Ch. 10 for more information.

♦ Adafruit Trinket, a very small Arduino.

♦ Freetronics EtherTen, an Arduino with built-in Ethernet.

♦ Particle Photon, a low-cost board with WiFi. It is programmed over the Internet using Arduino C but with a Web-based IDE rather than the Arduino IDE.

* * *

### Conclusion

Now that you have explored the Arduino hardware a little, it’s time to set up your Arduino software.

## 2

## Getting Started

Having introduced the Arduino, and learned a little about what it is that we are programming, it is time to learn how to install the software that we will need on our computer and to start working on some code.

* * *

### Powering Up

When you buy an Arduino board, it is usually preinstalled with a sample Blink program that will make the little built-in light-emitting diode (LED) flash.

The LED marked *L* is wired up to one of the digital input output sockets on the board. It is connected to digital pin 13\. This does not mean that pin 13 can only be used to light the LED; you can also use it as a normal digital input or output.

All you need to do to get your Arduino up and running is supply it with some power. The easiest way to do this is to plug it into the USB port on your computer. You will need a type-A-to-type-B USB lead. This is the same type of lead that is normally used to connect a computer to a printer.

If everything is working OK, the LED should blink. New Arduino boards come with this Blink sketch already installed so that you can verify that the board works.

* * *

### Installing the Software

To be able to install new sketches onto your Arduino board, you need to do more than supply power to it over the USB. You need to install the Arduino software ([Figure 2-1](#11_Chapter_02.xhtml_fig-ch2-1)).

![image](images/fig-ch2-1.jpg)

Figure 2.1 *The Arduino application*.

Full and comprehensive instructions for installing this software on Windows, Linux, and Mac computers can be found at the Arduino website ([www.arduino.cc](http://www.arduino.cc)).

Once you have successfully installed the Arduino software and, depending on your platform, USB drivers, you should now be able to upload a program to the Arduino board.

* * *

### Uploading Your First Sketch

The blinking LED is the Arduino equivalent to the “Hello World” program used in other languages as the traditional first program to run when learning a new language. Let’s test out the environment by installing this program on your Arduino board and then modifying it.

When you start the Arduino application on your computer, it opens with an empty sketch. Fortunately, the application ships with a wide range of useful examples. So from the File menu, open the Blink example as shown in [Figure 2-2](#11_Chapter_02.xhtml_fig-ch2-2).

![image](images/fig-ch2-2.jpg)

Figure 2.2 *The Blink sketch*.

You now need to transfer or upload that sketch to your Arduino board. So plug your Arduino board into your computer using the USB lead. You should see the green “On” LED on the Arduino light up. The Arduino board will probably already be flashing, as the boards are generally shipped with the Blink sketch already installed. But let’s install it again and then modify it.

Before you can upload a sketch, you must tell the Arduino application what type of board you are using and which serial port you are connected to. [Figures 2-3](#11_Chapter_02.xhtml_fig-ch2-3) and [2-4](#11_Chapter_02.xhtml_fig-ch2-4) show how you do this from the Tools menu.

![image](images/fig-ch2-3.jpg)

Figure 2.3 *Selecting the board type*.

![image](images/fig-ch2-4.jpg)

Figure 2.4 *Selecting the serial port (in Windows)*.

On a Windows machine, the serial port is always COM followed by a number. On Macs and Linux machines, you will see a much longer list of serial devices (see [Figure 2-5](#11_Chapter_02.xhtml_fig-ch2-5)). The device will normally be the bottom selection in the list, with a name similar to /dev/cu.usbmodem621.

![image](images/fig-ch2-5.jpg)

Figure 2.5 *Selecting the serial port (on a Mac)*.

Now click on the Upload icon in the toolbar. This is shown circled in [Figure 2-6](#11_Chapter_02.xhtml_fig-ch2-6).

![image](images/fig-ch2-6.jpg)

Figure 2.6 *Uploading the sketch*.

After you click the button, there is a short pause while the sketch is compiled and then the transfer begins. If it is working, then there will be some furious blinking of LEDs as the sketch is transferred, after which you should see the message “Done Uploading” at the bottom of the Arduino application window and a further message similar to “Sketch uses 1,030 bytes (3%) of program storage space.”

Once uploaded, the board automatically starts running the sketch and you will see the yellow ‘L’ LED start to blink.

If this did not work, then check your serial and board type settings.

Now let’s modify the sketch to make the LED blink faster. To do this, let’s alter the two places in the sketch where there is a delay for 1,000 milliseconds so that the delay is 500 milliseconds. [Figure 2-7](#11_Chapter_02.xhtml_fig-ch2-7) shows the modified sketch with the changes circled.

![image](images/fig-ch2-7.jpg)

Figure 2.7 *Modifying the Blink sketch*.

Click on the Upload button again. Then, once the sketch has uploaded, you should see your LED start to blink twice as fast as it did before.

Congratulations, you are now ready to start programming your Arduino. First, though, let’s take a mini-tour of the Arduino application.

* * *

### The Arduino Application

Sketches in Arduino are like documents in a word processor. You can open them and copy parts from one to another. So you see options to Open, Save, and Save As in the File menu. You will not normally use Open because the Arduino application has the concept of a Sketchbook where all your sketches are kept carefully organized into folders. You gain access to the Sketchbook from the File menu. As you have just installed the Arduino application for the first time, your Sketchbook will be empty until you create some sketches.

As you have seen, the Arduino application comes with a selection of example sketches that can be very useful. Having modified the Blink example sketch, if you try and save it, you get a message that says, “Some files are marked read-only so you will need to save this sketch in a different location.”

Try this now. Accept the default location, but change the filename to MyBlink, as shown in [Figure 2-8](#11_Chapter_02.xhtml_fig-ch2-8).

![image](images/fig-ch2-8.jpg)

Figure 2.8 *Saving a copy of Blink*.

Now if you go to the File menu and then click on Sketches, you will see MyBlink as one of the sketches listed. If you look at your computer’s file system, you will find that, on a PC, the sketch has been written into My Documents\Arduino, and on Mac or Linux, it is in Documents/Arduino.

All of the sketches used in this book can be downloaded as a zip file (Programming_Arduino.zip) from [www.arduinobook.com](http://www.arduinobook.com). I suggest that now is the time to download this file and unzip it into the Arduino folder that contains the sketches. In other words, when you have unzipped the folder, there should be two folders in your Arduino folder: one for the newly saved MyBlink and one called Programming Arduino (see [Figure 2-9](#11_Chapter_02.xhtml_fig-ch2-9)). The Programming Arduino folder will contain all the sketches, numbered according to chapter, so that sketch 03-01, for example, is sketch 1 of [Chapter 3](#12_Chapter_03.xhtml).

![image](images/fig-ch2-9.jpg)

Figure 2.9 *Installing the sketches from the book*.

These sketches will not appear in your Sketchbook menu until you quit the Arduino application and restart it. Do so now. Then your Sketchbook menu should look similar to that shown in [Figure 2-10](#11_Chapter_02.xhtml_fig-ch2-10).

![image](images/fig-ch2-10.jpg)

Figure 2.10 *Sketchbook with the book’s sketches installed*.

* * *

### Conclusion

Your environment is all set up and ready to go.

In the next chapter, we will look at some of the basic principles of the C language that the Arduino uses and start writing some code.

## 3

## C Language Basics

The programming language used to program Arduinos is a language called C. In this chapter, you get to understand the basics of the C language. You will use what you learn here in every sketch you develop as an Arduino programmer. To get the most out of Arduino, you need to understand these fundamentals.

* * *

### Programming

It is not uncommon for people to speak more than one language. In fact, the more you learn, the easier it seems to learn spoken languages as you start to find common patterns of grammar and vocabulary. The same is true of programming languages. So, if you have used any other programming language, you will quickly pick up C.

The good news is that the vocabulary of a programming language is far smaller than that of a spoken language, and because you write it rather than say it, the dictionary can always be at hand whenever you need to look things up. Also, the grammar and syntax of a programming language are extremely regular, and once you come to grips with a few simple concepts, learning more quickly becomes second nature.

It is best to think of a program—or a sketch, as programs are called in Arduino—as a list of instructions to be carried out in the order that they are written down. For example, suppose you were to write the following:

```
digitalWrite(13, HIGH);
delay(500);
digitalWrite(13, LOW);
```

These three lines would each do something. The first line would set the output of pin 13 to HIGH. This is the pin with an LED built in to the Arduino board, so at this point the LED would light. The second line would simply wait for 500 milliseconds (half a second) and then the third line would turn the LED back off again. So these three lines would achieve the goal of making the LED blink once.

You have already seen a bewildering array of punctuation used in strange ways and words that don’t have spaces between them. A frustration of many new programmers is, “I know what I want to do, I just don’t know what I need to write!” Fear not, all will be explained.

First of all, let’s deal with the punctuation and the way the words are formed. These are both part of what is termed the syntax of the language. Most languages require you to be extremely precise about syntax, and one of the main rules is that names for things have to be a single word. That is, they cannot include spaces. So, **digitalWrite** is the name for something. It’s the name of a built-in function (you’ll learn more about functions later) that will do the job of setting an output pin on the Arduino board. Not only do you have to avoid spaces in names, but also names are case sensitive. So you must write **digitalWrite**, not **DigitalWrite** or **Digitalwrite.**

The function **digitalWrite** needs to know which pin to set and whether to set that pin HIGH or LOW. These two pieces of information are called *arguments*, which are said to be *passed* to a function when it is *called*. The parameters for a function must be enclosed in parentheses and separated by commas.

The convention is to place the opening parenthesis immediately after the last letter of the function’s name and to put a space after the comma before the next parameter. However, you can sprinkle space characters within the parentheses if you want.

If the function only has one argument, then there is no need for a comma.

Notice how each line ends with a semicolon. It would be more logical if they were periods, because the semicolon marks the end of one command, a bit like the end of a sentence.

In the next section, you will find out a bit more about what happens when you press the Upload button on the Arduino integrated development environment (IDE). Then you will be able to start trying out a few examples.

* * *

### What Is a Programming Language?

It is perhaps a little surprising that we can get to [Chapter 3](#12_Chapter_03.xhtml) in a book about programming without defining exactly what a programming language is. We can recognize an Arduino sketch and probably have a rough idea of what it is trying to do, but we need to look a bit deeper into how some programming language code goes from being words on a page to something that does something real, like turn an LED on and off.

[Figure 3-1](#12_Chapter_03.xhtml_fig-ch3-1) summarizes the process involved from typing code into the Arduino IDE to running the sketch on the board.

![image](images/fig-ch3-1.jpg)

Figure 3.1 *From code to board*.

When you press the Upload button on your Arduino IDE, it launches a chain of events that results in your sketch being installed on the Arduino and being run. This is not as straightforward as simply taking the text that you typed into the editor and moving it to the Arduino board.

The first step is to do something called *compilation*. This takes the code you have written and translates it into machine code—the binary language that the Arduino understands. If you click the Verify button on the Arduino IDE, this actually attempts to compile the C that you have written without trying to send the code to the Arduino IDE. A side-effect of compiling the code is that it is checked to make sure that it conforms to the rules of the C language.

If you type **Ciao Bella!** into your Arduino IDE and click on the Play button, the results will be as shown in [Figure 3-2](#12_Chapter_03.xhtml_fig-ch3-2).

![image](images/fig-ch3-2.jpg)

Figure 3.2 *Arduinos don’t speak Italian*.

The Arduino has tried to compile the words “Ciao Bella,” and despite its Italian heritage, it has no idea what you are talking about. This text is not C. So, the result is that at the bottom of the screen we have that cryptic message “Ciao does not name a type.” What this actually means is that there is a lot wrong with what you have written.

Let’s try another example. This time we will try compiling a sketch with no code at all in it (see [Figure 3-3](#12_Chapter_03.xhtml_fig-ch3-3)).

![image](images/fig-ch3-3.jpg)

Figure 3.3 *No **setup** or **loop***.

This time, the compiler is telling you that your sketch does not have **setup** or **loop** functions. As you know from the Blink example that you ran in [Chapter 2](#11_Chapter_02.xhtml), you have to have some “boilerplate” code, as it is called, before you can add your own code into a sketch. In Arduino programming the “boilerplate” code takes the form of the “setup” and “loop” functions that must always be present in a sketch.

You will learn much more about functions later in the book, but for now, let’s accept that you need this boilerplate code and just adapt your sketch so it will compile (see [Figure 3-4](#12_Chapter_03.xhtml_fig-ch3-4)).

![image](images/fig-ch3-4.jpg)

Figure 3.4 *A sketch that will compile*.

The Arduino IDE has looked at your efforts at writing code and found them to be acceptable. It tells you this by saying “Done Compiling” and reporting the size of the sketch to you: 450 bytes. The IDE is also telling you that the maximum size is 32,256 bytes, so you still have lots of room to make your sketch bigger.

Let’s examine this boilerplate code that will form the starting point for every sketch that you ever write. There are some new things here. For example, there is the word **void** and some curly braces. Let’s deal with **void** first.

The line **void setup()** means that you are defining a function called **setup**. In Arduino, some functions are already defined for you, such as **digitalWrite** and **delay**, whereas you must or can define others for yourself. **setup** and **loop** are two functions that you must define for yourself in every sketch that you write.

The important thing to understand is that here you are not calling **setup** or **loop** like you would call **digitalWrite**, but you are actually creating these functions so that the Arduino system itself can call them. This is a difficult concept to grasp, but one way to think of it is as being similar to a definition in a legal document.

Most legal documents have a “definitions” section that might say, for example, something like the following:

```
Definitions.
The Author: The person or persons responsible for creating the book
```

By defining a term in this way—for example, simply using the word “author” as shorthand for “The person or persons responsible for creating the book”—lawyers can make their documents shorter and more readable. Functions work much like such definitions. You define a function that you or the system itself can then use elsewhere in your sketches.

Going back to **void**, these two functions (**setup** and **loop**) do not return a value as some functions do, so you have to say that they are void, using the **void** keyword. If you imagine a function called **sin** that performed the trigonometric function of that name, then this function would return a value. The value returned to use from the call would be the sine of the angle passed as its argument.

Rather like a legal definition uses words to define a term, we write functions in C that can then be called from C.

After the special keyword **void** comes the name of the function and then parentheses to contain any arguments. In this case, there are no arguments, but we still have to include the parentheses there. There is no semicolon after the closing parenthesis because we are defining a function rather than calling it, so we need to say what will happen when something does call the function.

Those things that are to happen when the function is called must be placed between curly braces. Curly braces and the code in between them are known as a *block* of code, and this is a concept that you will meet again later.

Note that although you do have to define both the functions **setup** and **loop**, you do not actually have to put any lines of code in them. However, failing to add code will make your sketch a little dull.

* * *

### Blink—Again!

The reason that Arduino has the two functions **setup** and **loop** is to separate the things that only need to be done once, when the Arduino starts running its sketch, from the things that have to keep happening continuously.

The function **setup** will just be run once when the sketch starts. Let’s add some code to it that will blink the LED built onto the board. Add the lines to your sketch so that it appears as follows and then upload them to your board:

```
void setup()
{
  pinMode(13, OUTPUT);
  digitalWrite(13, HIGH);
}

void loop()
{
}
```

The **setup** function itself calls two built-in functions, **pinMode** and **digitalWrite**. You already know about **digitalWrite**, but **pinMode** is new. The function **pinMode** sets a particular pin to be either an input or an output. So, turning the LED on is actually a two-stage process. First, you have to set pin 13 to be an output, and second, you need to set that output to be high (5V).

When you run this sketch, on your board you will see that the L LED comes on and stays on. This is not very exciting, so let’s at least try to make it flash by turning it on and off in the **loop** function rather than in the **setup** function.

You can leave the **pinMode** call in the **setup** function because you only need to call it once. The project would still work if you moved it into the loop, but there is no need and it is a good programming habit to do things only once if you only need to do them once. So modify your sketch so that it looks like this:

```
void setup()
{
  pinMode(13, OUTPUT);
}

void loop()
{
 digitalWrite(13, HIGH);
 delay(500);
 digitalWrite(13, LOW);
}
```

Run this sketch and see what happens. It may not be quite what you were expecting. The LED is basically on all the time. Hmm, why should this be?

Try stepping through the sketch a line at a time in your head:

1.  Run **setup** and set pin 13 to be an output.
2.  Run **loop** and set pin 13 to high (LED on).
3.  Delay for half a second.
4.  Set pin 13 to low (LED off).
5.  Run **loop** again, going back to step 2, and set pin 13 to high (LED on).

The problem lies between steps 4 and 5\. What is happening is that the LED is being turned off, but the very next thing that happens is that it gets turned on again. This happens so quickly that it appears that the LED is on all the time.

The microcontroller chip on the Arduino can perform 16 million instructions per second. That’s not 16 million C language commands, but it is still very fast. So, our LED will only be off for a few millionths of a second.

To fix the problem, you need to add another delay after you turn the LED off. Your code should now look like this:

```
// sketch 3-01
void setup()
{
  pinMode(13, OUTPUT);
}

void loop()
{
 digitalWrite(13, HIGH);
 delay(500);
 digitalWrite(13, LOW);
 delay(500);
}
```

Try again and your LED should blink away merrily once per second.

You may have noticed the comment at the top of the listing saying “sketch 3-01.” To save you some typing, we have uploaded to this book’s website all the sketches with such a comment at the top. You can download them from [www.arduinobook.com](http://www.arduinobook.com).

* * *

### Variables

In this Blink example, you use pin 13 and have to refer to it in three places. If you decided to use a different pin, then you would have to change the code in three places. Similarly, if you wanted to change the rate of blinking, controlled by the argument to delay, you would have to change 500 to some other number in two places.

Variables can be thought of as giving a name to a number. Actually, they can be a lot more powerful than this, but for now, you will use them for this purpose.

When defining a variable in C, you have to specify the type of the variable. We want our variables to be whole numbers, which in C are called **int**s. So to define a variable called **ledPin** with a value of 13, you need to write the following:

```
int ledPin = 13;
```

Notice that because **ledPin** is a name, the same rules apply as those of function names. So, there cannot be any spaces. The convention is to start variables with a lowercase letter and begin each new word with an uppercase letter. Programmers will often call this “bumpy case” or “camel case.”

Let’s fit this into your Blink sketch as follows:

```
// sketch 3-02
int ledPin = 13;
int delayPeriod = 500;
```

```
void setup()
{
  pinMode(ledPin, OUTPUT);
}

void loop()
{
 digitalWrite(ledPin, HIGH);
 delay(delayPeriod);
 digitalWrite(ledPin, LOW);
 delay(delayPeriod);
}
```

We have also sneaked in another variable called **delayPeriod**.

Everywhere in the sketch where you used to refer to 13, you now refer to **ledPin**, and everywhere you used to refer to 500, you now refer to **delayPeriod**.

If you want to make the sketch blink faster, you can just change the value of **delayPeriod** in one place. Try changing it to 100 and running the sketch on your Arduino board.

There are other cunning things that you can do with variables. Let’s modify your sketch so that the blinking starts really fast and gradually gets slower and slower, as if the Arduino is getting tired. To do this, all you need to do is to add something to the **delayPeriod** variable each time that you do a blink.

Modify the sketch by adding the single line at the end of the **loop** function so that it appears, as in the following listing, and then run the sketch on the Arduino board. Press the Reset button and see it start from a fast rate of flashing again.

```
// sketch 3-03
int ledPin = 13;
int delayPeriod = 100;

void setup()
{
  pinMode(ledPin, OUTPUT);
}

void loop()
{
 digitalWrite(ledPin, HIGH);
 delay(delayPeriod);
 digitalWrite(ledPin, LOW);
 delay(delayPeriod);
 delayPeriod = delayPeriod + 100;
}
```

Your Arduino is doing arithmetic now. Every time that **loop** is called, it will do the normal flash of the LED, but then it will add 100 to the variable **delayPeriod**. We will come back to arithmetic shortly, but first you need a better way than a flashing LED to see what the Arduino is up to.

* * *

### Experiments in C

You need a way to test your experiments in C. One way is to put the C that you want to test out into the **setup** function, evaluate them on the Arduino, and then have the Arduino display any output back to something called the Serial Monitor, as shown in [Figures 3-5](#12_Chapter_03.xhtml_fig-ch3-5) and [3-6](#12_Chapter_03.xhtml_fig-ch3-6).

![image](images/fig-ch3-5.jpg)

Figure 3.5 *Writing C in **setup***.

![image](images/fig-ch3-6.jpg)

Figure 3.6 *The Serial Monitor*.

The Serial Monitor is part of the Arduino IDE. You access it by clicking on the rightmost icon in the toolbar (it looks like a magnifying glass). Its purpose is to act as a communication channel between your computer and the Arduino. You can type a message in the text entry area at the top of the Serial Monitor and when you press Return or click Send, it will send that message to the Arduino. Also if the Arduino has anything to say, this message will appear in the Serial Monitor. In both cases, the information is sent through the USB link.

As you would expect, there is a built-in function that you can use in your sketches to send a message back to the Serial Monitor. It is called **Serial.println** and it expects a single argument, which consists of the information that you want to send. This information is usually a variable.

You will use this mechanism to test out a few things that you can do with variables and arithmetic in C; frankly, it’s the only way you can see the results of your experiments in C.

#### Numeric Variables and Arithmetic

The last thing you did was add the following line to your blinking sketch to increase the blinking period steadily:

```
delayPeriod = delayPeriod + 100;
```

Looking closely at this line, it consists of a variable name, then an equals sign, then what is called an expression (**delayPeriod + 100**). The equals sign does something called assignment. That is, it assigns a new value to a variable, and the value it is given is determined by what comes after the equals sign and before the semicolon. In this case, the new value to be given to the **delayPeriod** variable is the old value of **delayPeriod** plus 100.

Let’s test out this new mechanism to see what the Arduino is up to by entering the following sketch, running it, and opening the Serial Monitor:

```
// sketch 3-04
void setup()
{
  Serial.begin(9600);
  int a = 2;
  int b = 2;
  int c = a + b;
  Serial.println(c);
}
void loop()
{}
```

[Figure 3-7](#12_Chapter_03.xhtml_fig-ch3-7) shows what you should see in the Serial Monitor after this code runs.

![image](images/fig-ch3-7.jpg)

Figure 3.7 *Simple arithmetic*.

To take a slightly more complex example, the formula for converting a temperature in degrees Centigrade into degrees Fahrenheit is to multiply it by 9, divide by 5, and then add 32\. So you could write that in a sketch like this:

```
// sketch 3-05
void setup()
{
  Serial.begin(9600);
  int degC = 20;
  int degF;
  degF = degC * 9 / 5 + 32;
  Serial.println(degF);
}
void loop()
{}
```

There are a few things to notice here. First, note the following line:

```
int degC = 20;
```

When we write such a line, we are actually doing two things: We are declaring an **int** variable called **degC**, and we are saying that its initial value will be 20\. Alternatively, you could separate these two things and write the following:

```
int degC;
degC = 20;
```

You must declare any variable just once, essentially telling the compiler what type of variable it is—in this case, **int**. However, you can assign the variable a value as many times as you want:

```
int degC;
degC = 20;
degC = 30;
```

So, in the Centigrade to Fahrenheit example, you are defining the variable **degC** and giving it an initial value of 20, but when you define **degF**, it does not get an initial value. Its value gets assigned on the next line, according to the conversion formula, before being sent to the Serial Monitor for you to see.

Looking at the expression, you can see that you use the asterisk (*****) for multiplication and the slash (**/**) for division. The arithmetic operators **+, –, ***, and **/** have an order of precedence—that is, multiplications are done first, then divisions, then additions and subtractions. This is in accordance with the usual use of arithmetic. However, sometimes it makes it clearer to use parentheses in the expressions. So, for example, you could write the following:

```
degF = ((degC * 9) / 5) + 32;
```

The expressions that you write can be as long and complex as you need them to be, and in addition to the usual arithmetic operators, there are other less commonly used operators and a big collection of various mathematical functions that are available to you. You will learn about these later.

* * *

### Commands

The C language has a number of built-in commands. In this section, we explore some of these and see how they can be of use in your sketches.

#### if

In our sketches so far, we have assumed that your lines of programming will be executed in order one after the other, with no exceptions. But what if you don’t want to do that? What if you only want to execute part of a sketch if some condition is true?

Let’s return to our gradually slowing-down Blinking LED example. At the moment, it will gradually get slower and slower until each blink is lasting hours. Let’s look at how we can change it so that once it has slowed down to a certain point, it goes back to its fast starting speed.

To do this, you must use an **if** command; the modified sketch is as follows. Try it out.

```
// sketch 3-06
int ledPin = 13;
int delayPeriod = 100;
```

```
void setup()
{
  pinMode(ledPin, OUTPUT);
}

void loop()
{
  digitalWrite(ledPin, HIGH);
  delay(delayPeriod);
  digitalWrite(ledPin, LOW);
  delay(delayPeriod);
  delayPeriod = delayPeriod + 100;
  if (delayPeriod > 3000)
  {
    delayPeriod = 100;
  }
}
```

The **if** command looks a little like a function definition, but this resemblance is only superficial. The word in the parenthesis is not an argument; it is what is called *a condition*. So in this case, the condition is that the variable **delayPeriod** has a value that is greater than 3,000\. If this is true, then the commands inside the curly braces will be executed. In this case, the code sets the value of **delayPeriod** back to 100.

If the condition is not true, then the Arduino will just continue on with the next thing. In this case, there is nothing after the “if”, so the Arduino will run the **loop** function again.

Running through the sequence of events in your head will help you understand what is going on. So, here is what happens:

1.  Arduino runs **setup** and initializes the LED pin to be an output.
2.  Arduino starts running **loop**.
3.  The LED turns on.
4.  A delay occurs.
5.  The LED turns off.
6.  A delay occurs.
7.  Add 100 to the **delayPeriod**.
8.  If the delay period is greater than 3,000, set it back to 100.
9.  Go back to step 3.

We used the symbol **>**, which means greater than. It is one example of what are called comparison operators. These operators are summarized in the following table:

| **Operator** | **Meaning** | **Examples** | **Result** |
| --- | --- | --- | --- |
| **<** | Less than |   **9 < 10****10 < 10** | truefalse |
| **>** | Greater than | **10 > 10****10 > 9** | falsetrue |
| **<=** | Less than or equal to |   **9 <= 10****10 <= 10** | truetrue |
| **>=** | Greater than or equal to | **10 >= 10****10 >= 9** | truetrue |
| **==** | Equal to |   **9 == 9** | true |
| **!=** | Not equal to |   **9 != 9** | false |

To compare two numbers, you use the **==** command. This double equals sign is easily confused with the character **=**, which is used to assign values to variables.

There is another form of **if** that allows you to do one thing if the condition is true and another if it is false. We will use this in some practical examples later in the book.

#### for

In addition to executing different commands under different circumstances, you also often will want to run a series of commands a number of times in a program. You already know one way of doing this, using the **loop** function. As soon as all the commands in the **loop** function have been run, it will start again automatically. However, sometimes you need more control than that.

So, for example, let’s say that you want to write a sketch that blinks 20 times, then pauses for 3 seconds, and then starts again. You could do that by just repeating the same code over and over again in your **loop** function, like this:

```
// sketch 3-07
int ledPin = 13;
int delayPeriod = 100;
```

```
void setup()
{
  pinMode(ledPin, OUTPUT);
}

void loop()
{
 digitalWrite(ledPin, HIGH);
 delay(delayPeriod);
 digitalWrite(ledPin, LOW);
 delay(delayPeriod);

 digitalWrite(ledPin, HIGH);
 delay(delayPeriod);
 digitalWrite(ledPin, LOW);
 delay(delayPeriod);

 digitalWrite(ledPin, HIGH);
 delay(delayPeriod);
 digitalWrite(ledPin, LOW);
 delay(delayPeriod);
// repeat the above 4 lines another 17 times

 delay(3000);
}
```

But this requires a lot of typing and there are several much better ways to do this. Let’s start by looking at how you can use a **for** loop and then look at another way of doing it using a counter and an **if** statement.

The sketch to accomplish this with a **for** loop is, as you can see, a lot shorter and easier to maintain than the previous example:

```
// sketch 3-08
int ledPin = 13;
int delayPeriod = 100;

void setup()
{
  pinMode(ledPin, OUTPUT);
}

void loop()
{
  for (int i = 0; i < 20; i ++)
  {
   digitalWrite(ledPin, HIGH);
   delay(delayPeriod);
   digitalWrite(ledPin, LOW);
   delay(delayPeriod);
  }
 delay(3000);
}
```

The **for** loop looks a bit like a function that takes three arguments, although here those arguments are separated by semicolons rather than the usual commas. This is just a quirk of the C language. The compiler will soon tell you when you get it wrong.

The first thing in the parentheses after **for** is a variable declaration. This specifies a variable to be used as a counter variable and gives it an initial value—in this case, 0.

The second part is a condition that must be true for you to stay in the **loop**. In this case, you will stay in the **loop** as long as **i** is less than 20, but as soon as **i** is 20 or more, the program will stop doing the things inside the **loop**.

The final part is what to do every time you have done all the things in the **loop**. In this case, that is to increment **i** by 1 so that it can, after 20 trips around the **loop**, cease to be less than 20 and cause the program to exit the **loop**.

Try entering this code and running it. The only way to get familiar with the syntax and all that pesky punctuation is to type it in and have the compiler tell you when you have done something wrong. Eventually, it will all start to make sense.

One potential downside of this approach is that the **loop** function is going to take a long time. This is not a problem for this sketch, because all it is doing is flashing an LED. But often, the **loop** function in a sketch will also be checking that keys have been pressed or that serial communications have been received. If the processor is busy inside a **for** loop, it will not be able to do this. Generally, it is a good idea to make the **loop** function run as fast as possible so that it can be run as frequently as possible.

The following sketch shows how to achieve this:

```
// sketch 3-09
int ledPin = 13;
int delayPeriod = 100;
int count = 0;
void setup()
{
  pinMode(ledPin, OUTPUT);
}

void loop()
{
 digitalWrite(ledPin, HIGH);
 delay(delayPeriod);
 digitalWrite(ledPin, LOW);
 delay(delayPeriod);
 count ++;
 if (count == 20)
 {
   count = 0;
   delay(3000);
 }
}
```

You may have noticed the following line:

```
count ++;
```

This is just C shorthand for the following:

```
count = count + 1;
```

So now each time that **loop** is run, it will take just a bit more than 200 milliseconds, unless it’s the 20th time round the loop, in which case it will take the same plus the three seconds delay between each batch of 20 flashes. In fact, for some applications, even this is too slow, and purists would say that you should not use **delay** at all. The best solution depends on the application.

#### while

Another way of looping in C is to use the **while** command in place of the **for** command. You can accomplish the same thing as the preceding **for** example using a **while** command as follows:

```
int i = 0;
while (i < 20)
{
  digitalWrite(ledPin, HIGH);
  delay(delayPeriod);
  digitalWrite(ledPin, LOW);
  delay(delayPeriod);
  i ++;
}
```

The expression in parentheses after **while** must be true to stay in the **loop**. When it is no longer true, then the sketch continues running the commands after the final curly brace.

* * *

### Constants

For constant values like pin assignments that do not change during the running of a sketch, use the keyword **const**, which tells the compiler that the variable has a constant value and is not going to change.

As an example, you could define a pin assignment for a LED like this:

```
const int ledPin = 13;
```

Any sketch that you write will work just as well without the **const** keyword in front of any such variables, but it will make the program slightly smaller, something that can become significant as your sketches get bigger. In any case, it’s a good habit to get into for any variables whose value is not going to change.

* * *

### Conclusion

This chapter has got you started with C. You can make LEDs blink in various exciting ways and get the Arduino to send results back to you over the USB by using the **Serial.println** function. You also worked out how to use **if** and **for** commands to control the order in which your commands are executed, and learned a little about making an Arduino do some arithmetic.

In the next chapter, you will look more closely at functions. The chapter will also introduce the variable types other than the **int** type that you used in this chapter.

## 4

## Functions

This chapter focuses mostly on the type of functions that you can write yourself rather than the built-in functions such as **digitalWrite** and **delay**, which are already defined for you.

The reason that you need to be able to write your own functions is that as sketches start to get a little complicated, then your **setup** and **loop** functions will grow and grow until they are long and complicated and it becomes difficult to see how they work.

The biggest problem in software development of any sort is managing complexity. The best programmers write software that is easy to look at and understand and requires very little in the way of explanation.

Functions are a key tool in creating easy-to-understand sketches that can be changed without difficulty or risk of the whole thing falling into a crumpled mess.

* * *

### What Is a Function?

A function is a little like a program within a program. You can use it to wrap up some little thing that you want to do. A function that you define can be called from anywhere in your sketch and contains its own variables and its own list of commands. When the commands have been run, execution returns to the point just after wherever it was in the code that called the function.

By way of an example, code that flashes a light-emitting diode (LED) is a prime example of some code that should be put in a function. So let’s modify our basic “blink 20 times” sketch to use a function that we will create called **flash**:

```
// sketch 4-01
const int ledPin = 13;
const int delayPeriod = 250;

void setup()
{
  pinMode(ledPin, OUTPUT);
}

void loop()
{
  for (int i = 0; i < 20; i ++)
  {
    flash();
  }
  delay(3000);
}

void flash()
{
   digitalWrite(ledPin, HIGH);
   delay(delayPeriod);
   digitalWrite(ledPin, LOW);
   delay(delayPeriod);
}
```

So, all we have really done here is to move the four lines of code that flash the LED from the middle of the **for** loop to be in a function of their own called **flash**. Now you can make the LED flash any time you like by just calling the new function by writing **flash()**. Note the empty parentheses after the function name. This indicates that the function does not take any parameters. The delay value that it uses is set by the same **delayPeriod** variable that you used before.

* * *

### Parameters

When dividing your sketch up into functions, it is often worth thinking about what service a function could provide. In the case of **flash**, this is fairly obvious. But this time, let’s give this function parameters that tell it both how many times to flash and how short or long the flashes should be. Read through the following code and then I will explain just how parameters work in a little more detail.

```
// sketch 4-02
const int ledPin = 13;
const int delayPeriod = 250;

void setup()
{
  pinMode(ledPin, OUTPUT);
}

void loop()
{
  flash(20, delayPeriod);
  delay(3000);
}

void flash(int numFlashes, int d)
{
  for (int i = 0; i < numFlashes; i ++)
  {
    digitalWrite(ledPin, HIGH);
    delay(d);
    digitalWrite(ledPin, LOW);
    delay(d);
  }
}
```

Now, if we look at our **loop** function, it has only two lines in it. We have moved the bulk of the work off to the **flash** function. Notice how when we call **flash** we now supply it with two arguments in parentheses.

Where we define the function at the bottom of the sketch, we have to declare the type of variable in the parameters. In this case, they are both **int**s. We are in fact defining new variables. However, these variables (**numFlashes** and **d**) can only be used within the **flash** function.

This is a good function because it wraps up everything you need in order to flash an LED. The only information that it needs from outside of the function is to which pin the LED is attached. If you wanted, you could make this a parameter too—something that would be well worth doing if you had more than one LED attached to your Arduino.

* * *

### Global, Local, and Static Variables

As was mentioned before, parameters to a function can be used only inside that function. So, if you wrote the following code, you would get an error:

```
void indicate(int x)
{
  flash(x, 10);
}
x = 15;
```

On the other hand, suppose you wrote this:

```
int x = 15;
void indicate(int x)
{
  flash(x, 10);
}
```

This code would not result in a compilation error. However, you need to be careful, because you now actually have two variables called **x** and they can each have different values. The one that you declared on the first line is called a *global variable.* It is called *global* because it can be used anywhere you like in the program, including inside any functions.

However, because you use the same variable name **x** inside the function as a parameter, you cannot use the global variable **x** simply because whenever you refer to **x** inside the function, the “local” version of **x** has priority. The parameter **x** is said to shadow the global variable of the same name. This can lead to some confusion when trying to debug a project.

In addition to defining parameters, you can also define variables that are not parameters but are just for use within a function. These are called *local variables.* For example:

```
void indicate(int x)
{
  int timesToFlash = x * 2;
  flash(timesToFlash, 10);
}
```

The local variable **timesToFlash** will only exist while the function is running. As soon as the function has finished its last command, it will disappear. This means that local variables are not accessible from anywhere in your program other than in the function in which they are defined.

So, for instance, the following example will cause an error:

```
void indicate(int x)
{
  int timesToFlash = x * 2;
  flash(timesToFlash, 10);
}
timesToFlash = 15;
```

Seasoned programmers generally treat global variables with suspicion. The reason is that they go against the principal of encapsulation. The idea of *encapsulation* is that you should wrap up in a package everything that has to do with a particular feature. Hence functions are great for encapsulation. The problem with “globals” (as global variables are often called) is that they generally get defined at the beginning of a sketch and may then be used all over the sketch. Sometimes there is a perfectly legitimate reason for this. Other times, people use them in a lazy way when it would be far more appropriate to pass parameters. In our examples so far, **ledPin** is a good use of a global variable. It’s also very convenient and easy to find up at the top of the sketch, making it easy to change.

Another feature of local variables is that their value is initialized every time the function is run. This is nowhere more true (and often inconvenient) than in the **loop** function of an Arduino sketch. Let’s try and use a local variable in place of a global variable in one of the examples from the previous chapter:

```
// sketch 4-03
const int ledPin = 13;
const int delayPeriod = 250;
void setup()
{
  pinMode(ledPin, OUTPUT);
}

void loop()
{
 int count = 0;
 digitalWrite(ledPin, HIGH);
 delay(delayPeriod);
 digitalWrite(ledPin, LOW);
 delay(delayPeriod);
 count ++;
 if (count == 20)
 {
   count = 0;
   delay(3000);
 }
}
```

Sketch 4-03 is based on sketch 3-09, but attempts to use a local variable instead of the global variable to count the number of flashes.

This sketch is broken. It will not work, because every time **loop** is run, the variable **count** will be given the value 0 again, so **count** will never reach 20 and the LED will just keep flashing forever. The whole reason that we made **count** a global in the first place was so that its value would not be reset. The only place that we use **count** is in the **loop** function, so this is where it should be placed.

Fortunately, there is a mechanism in C that gets around this conundrum. It is the keyword **static**. When you use the keyword **static** in front of a variable declaration in a function, it has the effect of initializing the variable only the first time that the function is run. Perfect! That’s just what is required in this situation. We can keep our variable in the function where it’s used without it getting set back to 0 every time the function runs. Sketch 4-04 shows this in operation:

```
// sketch 4-04
const int ledPin = 13;
const int delayPeriod = 250;
void setup()
{
  pinMode(ledPin, OUTPUT);
}

void loop()
{
 static int count = 0;
 digitalWrite(ledPin, HIGH);
 delay(delayPeriod);
 digitalWrite(ledPin, LOW);
 delay(delayPeriod);
 count ++;
 if (count == 20)
 {
   count = 0;
   delay(3000);
 }
}
```

* * *

### Return Values

Computer science, as an academic discipline, has as its parents mathematics and engineering. This heritage lingers on in many of the names associated with programming. The word *function* is itself a mathematical term. In mathematics, the input to the function (the argument) completely determines the output. We have written functions that take an input, but none that give us back a value. All our functions have been “void” functions. If a function returns a value, then you specify a return type.

Let’s look at writing a function that takes a temperature in degrees Centigrade and returns the equivalent in degrees Fahrenheit:

```
int centToFaren(int c)
{
  int f = c * 9 / 5 + 32;
  return f;
}
```

The function definition now starts with **int** rather than **void** to indicate that the function will return an **int** to whatever calls it. This might be a bit of code that looks like this:

```
int pleasantTemp = centToFaren(20);
```

Any nonvoid function has to have a **return** statement in it. If you do not put one in, the compiler will tell you that it is missing. You can have more than one **return** in the same function. This might arise if you have an **if** statement with alternative actions based on some condition. Some programmers frown on this, but if your functions are small (as all functions should be), then this practice will not be a problem.

The value after **return** can be an expression; it does not have to just be the name of a variable. So you could compress the preceding example into the following:

```
int centToFaren(int c)
{
  return (c * 9 / 5 + 32);
}
```

If the expression being returned is more than just a variable name, then it should be enclosed in parentheses as in the preceding example.

* * *

### Other Variable Types

All our examples of variables so far have been **int** variables. This is by far the most commonly used variable type, but there are some others that you should be aware of.

#### floats

One such type, which is relevant to the previous temperature conversion example, is **float**. This variable type represents floating point numbers—that is, numbers that may have a decimal point in them, such as 1.23\. You need this variable type when whole numbers are just not precise enough.

Note the following formula:

```
f = c * 9 / 5 + 32
```

If you give **c** the value 17, then **f** will be 17 * 9 / 5 + 32 or 62.6\. But if **f** is an **int**, then the value will be truncated to 62.

The problem becomes even worse if we are not careful of the order in which we evaluate things. For instance, suppose that we did the division first, as follows:

```
f = (c / 5) * 9 + 32
```

Then in normal math terms, the result would still be 62.6, but if all the numbers are **int**s, then the calculation would proceed as follows:

1.  17 is divided by 5, which gives 3.4, which is then truncated to 3.
2.  3 is then multiplied by 9 and 32 is added to give a result of 59—which is quite a long way from 62.6.

For circumstances like this, we can use **float**s. In the following example, our temperature conversion function is rewritten to use **float**s:

```
float centToFaren(float c)
{
  float f = c * 9.0 / 5.0 + 32.0;
  return f;
}
```

Notice how we have added `.0` to the end of our constants. This ensures that the compiler knows to treat them as **float**s rather than **int**s.

#### boolean

Boolean values are logical. They have a value that is either true or false.

In the C language, *Boolean* is spelled with a lowercase *b,* but in general use, *Boolean* has an uppercase initial letter, as it is named after the mathematician George Boole, who invented the Boolean logic that is crucial to computer science.

You may not realize it, but you have already met Boolean values when we were looking at the **if** command. The condition in an **if** statement, such as **(count == 20)**, is actually an expression that yields a **boolean** result. The operator **==** is called a comparison operator. Whereas **+** is an arithmetic operator that adds two numbers together, **==** is a comparison operator that compares two numbers and returns a value of either true or false.

You can define Boolean variables and use them as follows:

```
boolean tooBig = (x > 10);
if (tooBig)
{
  x = 5;
}
```

Boolean values can be manipulated using Boolean operators. So, similar to how you can perform arithmetic on numbers, you can also perform operations on Boolean values. The most commonly used Boolean operators are **and**, which is written as **&&**, and **or**, which is written as **||**.

[Figure 4-1](#13_Chapter_04.xhtml_fig-ch4-1) shows truth tables for the **and** and **or** operators.

From the truth tables in [Figure 4-1](#13_Chapter_04.xhtml_fig-ch4-1), you can see that for **and**, if both A and B are true, then the result will be true; otherwise, the result will be false.

![image](images/fig-ch4-1.jpg)

Figure 4.1 *Truth tables*.

On the other hand, with the **or** operator, if either A or B or both A and B are true, then the result will be true. The result will be false only if neither A nor B is true.

In addition to **and** and **or**, there is the **not** operator, written as **!**. You will not be surprised to learn that “not true” is false and “not false” is true.

You can combine these operators into Boolean expressions in your **if** statements, as the following example illustrates:

```
if ((x > 10) && (x < 50))
```

#### Other Data Types

As you have seen, the **int** and occasionally the **float** data types are fine for most situations; however, some other numeric types can be useful under some circumstances. In an Arduino sketch, the **int** type uses 16 bits (binary digits). This allows it to represent numbers between –32768 and 32767.

Other data types available to you are summarized in [Table 4-1](#13_Chapter_04.xhtml_tab-ch4-1). This table is provided mainly for reference. You will use some of these other types as you progress through the book.

| **Type** | **Memory (Bytes)** | **Range** | **Notes** |
| --- | --- | --- | --- |
| **boolean** | 1 | True or false (0 or 1) |  |
| **char** | 1 | –128 to +127 | Used to represent an American Standard Code for Information Interchange (ASCII) character code; e.g., *A* is represented as 65\. Its negative numbers are not normally used. |
| **byte** | 1 | 0 to 255 | Often used for communicating serial data, as a single unit of data. See [Chapter 9](#18_Chapter_09.xhtml). |
| **int** | 2 | –32768 to +32767 |  |
| **unsigned int** | 2 | 0 to 65535 | Can be used for extra precision where negative numbers are not needed. Use with caution, as arithmetic with **int**s may cause unexpected results. |
| **long** | 4 | –2,147,483,648 to 2,147,483,647 | Needed only for representing very big numbers. |
| **unsigned long** | 4 | 0 to 4,294,967,295 | See **unsigned int**. |
| **float** | 4 | –3.4028235E+38 to + 3.4028235E+38 |  |
| **double** | 4 | Same as **float** | Normally, this would be 8 bytes and higher precision than **float** with a greater range. However, on Arduino, it is the same as **float**. |

Table 4-1 *Data Types in C*

One thing to consider is that if data types exceed their range, then strange things happen. So, if you have a byte variable with 255 in it and you add 1 to it, you get 0\. More alarmingly, if you have an **int** variable with 32767 and you add 1 to it, you will end up with –32768.

Until you are completely comfortable with these different data types, I would recommend sticking to **int**, as it works for pretty much everything.

* * *

### Coding Style

The C compiler does not really care about how you lay out your code. For all it cares, you can write everything on a single line with semicolons between each statement. However, well-laid-out, neat code is much easier to read and maintain than poorly laid-out code. In this sense, reading code is just like reading a book: Formatting is important.

To some extent, formatting is a matter of personal taste. No one likes to think that he has bad taste, so arguments about how code should look can become personal. It is not unknown for programmers, on being required to do something with someone else’s code, to start by reformatting all the code into their preferred style of presentation.

As an answer to this problem, coding standards are often laid down to encourage everyone to lay out his or her code in the same way and adopt “good practice” when writing programs.

The C language has a de facto standard that has evolved over the years, and this book is generally faithful to that standard.

#### Indentation

In the example sketches that you have seen, you can see that we often indent the program code from the left margin. So, for example when defining a **void** function, the **void** keyword is at the left margin, as is the opening curly brace on the next line, but then all the text within the curly braces is indented. The amount of indentation does not really matter. Some people use two spaces, some four. You can also press TAB to indent. In this book, we use two spaces for indentation.

If you were to have an **if** statement inside a function definition, then once again you would add two more spaces for the lines within the curly braces of the **if** command, as in the following example:

```
void loop()
{
 static int count = 0;
 count ++;
 if (count == 20)
 {
   count = 0;
   delay(3000);
 }
}
```

You might include another **if** inside the first **if**, which would add yet another level of indentation, making six spaces from the left margin.

All of this might sound a bit trivial, but if you ever sort through someone else’s badly formatted sketches, you will find it very difficult.

#### Opening Braces

There are two schools of thought as to where to put the first curly brace in a function definition, **if** statement, or **for** loop. One way is to place the curly brace on the line after the rest of the command, as we have in all the examples so far, or put it on the same line, like this:

```
void loop() {
 static int count = 0;
 count ++;
 if (count == 20) {
   count = 0;
   delay(3000);
 }
}
```

This style is most commonly used in the Java programming language, which shares much of the same syntax as C.

#### Whitespace

The compiler ignores spaces, tabs, and new lines, apart from using them as a way of separating the “tokens” or words in your sketch. Thus the following example will compile without a problem:

```
void loop() {static int 
count=0;count++;if(
count==20){count=0;
delay(3000);}}
```

This will work, but good luck trying to read it.

Where assignments are made, some people will write the following:

```
int a = 10;
```

But others will write the following:

```
int a=10;
```

Which of these two styles you use really does not matter, but it is a good idea to be consistent. I use the first form.

#### Comments

Comments are text that is kept in your sketch along with all the real program code, but which actually performs no programming function whatsoever. The sole purpose of comments is to be a reminder to you or others as to why the code is written as it is. A comment line may also be used to present a title.

The compiler will completely ignore any text that is marked as being a comment. We have included comments as titles at the top of many of the sketches in the book so far.

There are two forms of syntax for comments:

♦ The single line comment that starts with **//** and finishes at the end of the line

♦ The multiline comment that starts with a **/*** and ends with a ***/**

The following is an example using both forms of comments:

```
/* A not very useful loop function.
Written by: Simon Monk
To illustrate the concept of comments
*/
void loop() {
 static int count = 0;
 count ++; // a single line comment
 if (count == 20) {
   count = 0;
   delay(3000);
 }
}
```

In this book, I mostly stick to the single-line comment format.

Good comments help explain what is happening in a sketch or how to use the sketch. They are useful if others are going to use your sketch, but equally useful to yourself when you are looking at a sketch that you have not worked on for a few weeks.

Some people are told in programming courses that the more comments, the better. Most seasoned programmers will tell you that well-written code requires very little in the way of comments because it is self-explanatory. You should use comments for the following reasons:

♦ To explain anything you have done that is a little tricky or not immediately obvious

♦ To describe anything that the user needs to do that is not part of the program; for example, **// this pin should be connected to the transistor controlling the relay**

♦ To leave yourself notes; for example, **// todo: tidy this - it’s a mess**

This last point illustrates a useful technique of **todo**s in comments. Programmers often put **todo**s in their code to remind themselves of something they need to do later. They can always use the search facility in their integrated development environment (IDE) to find all occurrences of **// todo** in their program.

The following are *not* good examples of reasons you should use comments:

♦ To state the blatantly obvious; for example, **a = a + 1; // add 1 to a**.

♦ To explain badly written code. Don’t comment on it; just write it clearly in the first place.

* * *

### Conclusion

This has been a bit of a theoretical chapter. You have had to absorb some new abstract concepts concerned with organizing our sketches into functions and adopting a style of programming that will save you time in the long run.

In the next chapter, you can start to apply some of what you have learned and look at better ways of structuring your data and using text strings.

## 5

## Arrays and Strings

After reading [Chapter 4](#13_Chapter_04.xhtml), you have a reasonable appreciation as to how to structure your sketches to make your life easier. If there is one thing that a good programmer likes, it’s an easy life. Now our attention is going to turn to the data that you use in your sketches.

The book *Algorithms + Data Structures = Programs* by Niklaus Wirth (Prentice-Hall, 1976) has been around for a good while now, but still manages to capture the essences of computer science and programming in particular. I can strongly recommend it to anyone who finds themselves bitten by the programming bug. It also captures the idea that to write a good program, you need to think about both the algorithm (what you do) and the structure of the data you use.

You have looked at **loop**s, **if** statements, and what is called the “algorithmic” side of programming an Arduino; you are now going to turn to how you structure your data.

* * *

### Arrays

Arrays are a way of containing a list of values. The variables that you have met so far have contained only a single value, usually an **int**. By contrast, an array contains a list of values, and you can access any one of those values by its position in the list.

C, in common with the majority of programming languages, begins its index positions at 0 rather than 1\. This means that the first element is actually element zero.

To illustrate the use of arrays, we could create an example application that repeatedly flashes “SOS” in Morse code using the Arduino board’s built-in LED.

Morse code used to be a vital method of communication in the 19th and 20th centuries. Because of its coding of letters as a series of long and short dots, Morse code can be sent over telegraph wires, over a radio link, and using signaling lights. The letters “SOS” (often taken to mean “save our souls”) are still recognized as an international signal of distress.

The letter “S” is represented as three short flashes (dots) and the letter “O” by three long flashes (dashes). You are going to use an array of **int**s to hold the duration of each flash that you are going to make. You can then use a **for** loop to step through each of the items in the array, making a flash of the appropriate duration.

First, let’s have a look at how you are going to create an array of **int**s containing the durations.

```
int durations[] = {200, 200, 200, 500, 500, 500, 200, 200, 200};
```

You indicate that a variable contains an array by placing **[]** after the variable name.

In this case, you are going to set the values for the durations at the time that you create the array. The syntax for doing this is to use curly braces and then values each separated by commas. Don’t forget the semicolon on the end of the line.

You can access any given element of the array using the square bracket notation. So, if you want to get the first element of the array, you can write the following:

```
durations[0]
```

To illustrate this, let’s create an array and then print out all its values to the Serial Monitor:

```
// sketch 5-01

int durations[] = {200, 200, 200, 500, 500, 500, 200, 200, 200};

void setup()
{
  Serial.begin(9600); 
  for (int i = 0; i < 9; i++)
  {
    Serial.println(durations[i]);
  }
}

void loop() {}
```

Note that you can use the keyword **const** with arrays as well as ordinary variables, just as long as you do not intend to modify the array within your sketch.

Upload the sketch to your board and then open the Serial Monitor. If all is well, you will see something like [Figure 5-1](#14_Chapter_05.xhtml_fig-ch5-1).

![image](images/fig-ch5-1.jpg)

Figure 5.1 *The Serial Monitor showing the output of sketch 5-01*.

This is quite neat, because if you wanted to add more durations to the array, all you would need to do is add them to the list inside the curly braces and change “9” in the **for** loop to the new size of the array.

You have to be a little careful with arrays, because the compiler will not try and stop you from accessing elements of data that are beyond the end of the array. This is because the array is really a pointer to an address in memory, as shown in [Figure 5-2](#14_Chapter_05.xhtml_fig-ch5-2).

![image](images/fig-ch5-2.jpg)

Figure 5.2 *Arrays and pointers*.

Programs keep their data, both ordinary variables and arrays, in *memory*. Computer memory is arranged much more rigidly than the human kind of memory. It is easiest to think of the memory in an Arduino as a collection of pigeonholes. When you define an array of nine elements, for example, the next available nine pigeonholes are reserved for its use and the variable is said to point at the first pigeonhole or *element* of the array.

Going back to our point about access being allowed beyond the bounds of your array, if you decided to access **durations[10]**, then you would still get back an **int**, but the value of this **int** could be anything. This is in itself fairly harmless, except that if you accidentally get a value outside of the array, you are likely to get confusing results in your sketch.

However, what is far worse is if you try changing a value outside of the size of the array. For instance, if you were to include something like the following in your program, the results could simply make your sketch break:

```
durations[10] = 0;
```

The pigeonhole **durations[10]** may be in use as some completely different variable. So always make sure that you do not go outside of the size of the array. If your sketch starts behaving strangely, then check for this kind of problem.

#### Morse Code SOS Using Arrays

Sketch 5-02 shows how you can use an array to make your emergency signal of SOS:

```
// sketch 5-02
const int ledPin = 13;

int durations[] = {200, 200, 200, 500, 500, 500, 200, 200, 200};

void setup()
{
  pinMode(ledPin, OUTPUT);
}

void loop()
{
  for (int i = 0; i < 9; i++)
  {
    flash(durations[i]);
  }
  delay(1000);
}

void flash(int delayPeriod)
{
   digitalWrite(ledPin, HIGH);
   delay(delayPeriod);
   digitalWrite(ledPin, LOW);
   delay(delayPeriod);
}
```

An obvious advantage of this approach is that it is very easy to change the message by simply altering the **durations** array. In sketch 5-05, you will take the use of arrays a stage further to make a more general-purpose Morse code flasher.

* * *

### String Arrays

In the programming world, the word *string* has nothing to do with long thin stuff that you tie knots in. A string is a sequence of characters. It’s the way you can get your Arduino to deal with text. For example, sketch 5-03 will repeatedly send the text “Hello” to the Serial Monitor one time per second:

```
// sketch 5-03
void setup()
{
  Serial.begin(9600);
}

void loop()
{
  Serial.println("Hello");
  delay(1000);
}
```

#### String Literals

String literals are enclosed in double quotation marks. They are literal in the sense that the string is a constant, rather like the **int** 123.

As you would expect, you can put strings in a variable. There is also an advanced string library, but for now you will use standard C strings, such as the one in sketch 5-03.

In C, a string literal is actually an array of the type **char**. The type **char** is a bit like **int** in that it is a number, but that number is between 0 and 127 and represents one character. The character may be a letter of the alphabet, a number, a punctuation mark, or a special character such as a tab or a line feed. These number codes for letters use a standard called ASCII. Some of the most commonly used ASCII codes are shown in [Table 5-1](#14_Chapter_05.xhtml_tab-ch5-1).

| **Character** | **ASCII Code (Decimal)** |
| --- | --- |
| a–z | 97–122 |
| A–Z | 65–90 |
| 0–9 | 48–57 |
| space | 32 |

Table 5-1 *Common ASCII Codes*

The string literal “Hello” is actually an array of characters, as shown in [Figure 5-3](#14_Chapter_05.xhtml_fig-ch5-3).

![image](images/fig-ch5-3.jpg)

Figure 5.3 *The string literal “Hello”*.

Note that the string literal has a special null character (\0) at the end. This character is used to indicate the end of the string.

#### String Variables

As you would expect, string variables are very similar to array variables, except that there is a useful shorthand method for defining their initial value.

```
char name[] = "Hello";
```

This defines an array of characters and initializes it to the word “Hello.” It will also add a final null value (ASCII 0) to mark the end of the string.

Although the preceding example is most consistent with what you know about writing arrays, it would be more common to write the following:

```
char *name = "Hello";
```

This is equivalent, and the ***** indicates a pointer. The idea is that **name** points to the first **char** element of the **char** array. That is the memory location that contains the letter *H.*

You can rewrite sketch 5-03 to use a variable as well as a string constant, as follows:

```
// sketch 5-04
char message[] = "Hello";

void setup()
{
  Serial.begin(9600);
}

void loop()
{
  Serial.println(message);
  delay(1000);
}
```

* * *

### A Morse Code Translator

Let’s put together what you have learned about arrays and strings to build a more complex sketch that will accept any message from the Serial Monitor and flash it out on the built-in LED.

The letters in Morse code are shown in [Table 5-2](#14_Chapter_05.xhtml_tab-ch5-2).

| A | .- | N | -. | 0 | ----- |
| B | -… | O | --- | 1 | .---- |
| C | -.-. | P | .--. | 2 | ..--- |
| D | -.. | Q | --.- | 3 | …-- |
| E | . | R | .-. | 4 | ….- |
| F | ..-. | S | … | 5 | ….. |
| G | -. | T | - | 6 | -…. |
| H | …. | U | ..- | 7 | --… |
| I | .. | V | …- | 8 | ---.. |
| J | .--- | W | .-- | 9 | ----. |
| K | -.- | X | -..- |  |  |
| L | .-.. | Y | -.-- |  |  |
| M | -- | Z | --.. |  |  |

Table 5-2 *Morse Code Letters*

Some of the rules of Morse code are that a dash is three times as long as a dot, the time between each dash or dot is equal to the duration of a dot, the space between two letters is the same length as a dash, and the space between two words is the same duration as seven dots.

For this project, we will not worry about punctuation, although it would be an interesting exercise for you to try adding this to the sketch. For a full list of all the Morse characters, see [en.wikipedia.org/wiki/Morse_code](http://en.wikipedia.org/wiki/Morse_code).

#### Data

You are going to build this example a step at a time, starting with the data structure that you are going to use to represent the codes.

It is important to understand that there is no one solution to this problem. Different programmers will come up with different ways to solve it. So, it is a mistake to think to yourself, “I would never have come up with that.” Well, no, quite possibly you would come up with something different and better. Everyone thinks in different ways, and this solution happens to be the one that first popped into the author’s head.

Representing the data is all about finding a way of expressing [Table 5-2](#14_Chapter_05.xhtml_tab-ch5-2) in C. In fact, you are going to split the data into two tables: one for the letters, and one for the numbers. The data structure for the letters is as follows:

```
char* letters[] = {
  ".-", "-...", "-.-.", "-..", ".", // A-I
  "..-.", "--.", "....", "..", 
  ".---", "-.-", ".-..", "--", "-.", // J-R
  "---", ".--.", "--.-", ".-.", 
  "...", "-", "..-", "...-", ".--", // S-Z
  "-..-", "-.--", "--.." 
};
```

What you have here is an array of string literals. So, because a string literal is actually an array of **char**, what you actually have here is an array of arrays—something that is perfectly legal and really quite useful.

This means that to find Morse for *A*, you would access **letters[0]**, which would give you the string **.-**. This approach is not terribly efficient, because you are using a whole byte (eight bits) of memory to represent a dash or a dot, which could be represented in a bit. However, you can easily justify this approach by saying that the total number of bytes is still only about 90 and we do have 2048 bytes to play with. Equally importantly, it makes the code easy to understand.

Numbers use the same approach:

```
 char* numbers[] = {
    "-----", ".----", "..---", "...--", "....-",
  ".....", "-....", "--...", "---..", "----."};
```

#### Globals and Setup

You need to define a couple of global variables: one for the delay period for a dot, and one to define which pin the LED is attached to:

```
const int dotDelay = 200;
const int ledPin = 13;
```

The **setup** function is pretty simple; you just need to set the **ledPin** as an output and set up the serial port:

```
void setup()                
{
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
}
```

#### The loop Function

You are now going to start on the real processing work in the **loop** function. The algorithm for this function is as follows:

♦ If there is a character to read from USB:

♦ If it’s a letter, flash it using the letters array.

♦ If it’s a number, flash it using the numbers array.

♦ If it’s a space, flash four times the dot delay.

That’s all. You should not think too far ahead. This algorithm represents what you want to do, or what your *intention* is, and this style of programming is called *programming by intention*.

If you write this algorithm in C, it will look like this:

```
void loop()                    
{
  char ch;
  if (Serial.available() > 0)     
  {
    ch = Serial.read();        
    if (ch >= 'a' && ch <= 'z')
    {
      flashSequence(letters[ch - 'a']);
    }
    else if (ch >= 'A' && ch <= 'Z')
    {
      flashSequence(letters[ch - 'A']);
    }
    else if (ch >= '0' && ch <= '9')
    {
      flashSequence(numbers[ch - '0']);
    }
    else if (ch == ' ')
    {
     delay(dotDelay * 4);      // gap between words  
    }
  }
}
```

There are a few things here that need explaining. First, there is **Serial.available()**. To understand this, you first need to know a little about how an Arduino communicates with your computer over USB. [Figure 5-4](#14_Chapter_05.xhtml_fig-ch5-4) summarizes this process.

![image](images/fig-ch5-4.jpg)

Figure 5.4 *Serial communication with an Arduino*.

In the situation where the computer is sending data from the Serial Monitor to the Arduino board, then the USB is converted from the USB signal levels and protocol to something that the microcontroller on the Arduino board can use. This conversion happens in a special-purpose chip on the Arduino board. The data is then received by a part of the microcontroller called the Universal Asynchronous Receiver/Transmitter (UART). The UART places the data it receives into a buffer. The buffer is a special area of memory (128 bytes) that can hold data that is removed as soon as it is read.

This communication happens regardless of what your sketch is doing. So, even though you may be merrily flashing LEDs, data will still arrive in the buffer and sit there until you are ready to read it. You can think of the buffer as being a bit like an e-mail inbox.

The way that you check to see whether you “have mail” is to use the function **Serial.available()**. This function returns the number of bytes of data in the buffer that are waiting for you to read. If there are no messages waiting to be read, then the function returns 0\. This is why the **if** statement checks to see that there are more than zero bytes available to read, and if they are, then the first thing that the statement does is read the next available **char**, using the function **Serial.read()**. This function gets assigned to the local variable **ch**.

Next is another **if** to decide what kind of thing it is that you want to flash:

```
 if (ch >= 'a' && ch <= 'z')
    {
      flashSequence(letters[ch - 'a']);
    }
```

At first, this might seem a bit strange. You are using **<=** and **>=** to compare characters. You can do that because each character is actually represented by a number (its ASCII code). So, if the code for the character is somewhere between *a* and *z* (97 and 122), then you know that the character that has come from the computer is a lowercase letter. You then call a function that you have not written yet called **flashSequence**, to which you will pass a string of dots and dashes; for example, to flash *a*, you would pass it **.-** as its argument.

You are devolving responsibility to this function for actually doing the flashing. You are not trying to do it inside the **loop**. This lets us keep the code easy to read.

Here is the C that determines the string of dashes and dots that you need to send to the **flashSequence** function:

```
letters[ch - 'a']
```

Once again, this looks a little strange. The function appears to be subtracting one character from another. This is actually a perfectly reasonable thing to do, because the function is actually subtracting the ASCII values.

Remember that you are storing the codes for the letters in an array. So the first element of the array contains a string of dashes and dots for the letter *A*, the second element includes the dots and dashes for *B*, and so on. So you need to find the right position in the array for the letter that you have just fetched from the buffer. The position for any lowercase letter will be the character code for the letter minus the character code for *a*. So, for example, *a* − *a* is actually 97 − 97 = 0\. Similarly, *c* − *a* is actually 99 − 97 = 2\. So, in the following statement, if ch **is** the letter c, then the bit inside the square brackets would evaluate to 2, and you would get element 2 from the array, which is -.-:

What this section has just described is concerned with lowercase letters. You also have to deal with uppercase letters and numbers. These are both handled in a similar manner.

#### The flashSequence Function

We have assumed a function called **flashSequence** and made use of it, but now you need to write it. We have planned for it to take a string containing a series of dashes and dots and to make the necessary flashes with the correct timings.

Thinking about the algorithm for doing this, you can break it into the following steps:

♦ For each element of the string of dashes and dots (such as .-.-):

♦ Flash that dot or dash.

Using the concept of programming by intention, let’s keep the function as simple as that.

The Morse codes are not the same length for all letters, so you need to loop around the string until you encounter the end marker, **\**0\. You also need a counter variable called i that starts at 0 and is incremented as the processing looks at each dot and dash:

```
void flashSequence(char* sequence)
{
   int i = 0;
   while (sequence[i] != '\0')
   {
       flashDotOrDash(sequence[i]);
       i++;
   }
   delay(dotDelay * 3);    // gap between letters
}
```

Again, you delegate the actual job of flashing an individual dot or dash to a new method called **flashDotOrDash**, which actually turns the LED on and off. Finally, when the program has flashed the dots and dashes, it needs to pause for three dots worth of delay. Note the helpful use of a comment.

#### The flashDotOrDash Function

The last function in your chain of functions is the one that actually does the work of turning the LED on and off. As its argument, the function has a single character that is either a dot (.) or a dash (–).

All the function needs to do is turn the LED on and delay for the duration of a dot if it’s a dot and three times the duration of a dot if it’s a dash, then turn the LED off again. Finally, it needs to delay for the period of a dot, to give the gap between flashes.

```
void flashDotOrDash(char dotOrDash)
{
  digitalWrite(ledPin, HIGH);
  if (dotOrDash == '.')
  {
    delay(dotDelay);           
  }
  else // must be a -
  {
    delay(dotDelay * 3);           
  }
  digitalWrite(ledPin, LOW);    
  delay(dotDelay); // gap between flashes
}
```

#### Putting It All Together

Putting all this together, the full listing is shown in sketch 5-05. Upload it to your Arduino board and try it out. Remember that to use it, you need to open the Serial Monitor and type some text into the area at the top and click Send. You should then see that text being flashed as Morse code.

```
// sketch 5-05
const int dotDelay = 200;
const int ledPin = 13;

char* letters[] = {
  ".-", "-...", "-.-.", "-..", ".", "..-.", "--.", "....", "..",    // A-I
  ".---", "-.-", ".-..", "--", "-.", "---", ".--.", "--.-", ".-.",  // J-R
  "...", "-", "..-", "...-", ".--", "-..-", "-.--", "--.."          // S-Z
};

char* numbers[] = {"-----", ".----", "..---", "...--", "....-", 
  ".....", "-....", "--...", "---..", "----."};

void setup()                 
{
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
}

void loop()                    
{
  char ch;
  if (Serial.available() > 0)     
  {
    ch = Serial.read();        
    if (ch >= 'a' && ch <= 'z')
    {
      flashSequence(letters[ch - 'a']);
    }
    else if (ch >= 'A' && ch <= 'Z')
    {
      flashSequence(letters[ch - 'A']);
    }
    else if (ch >= '0' && ch <= '9')
    {
      flashSequence(numbers[ch - '0']);
    }
    else if (ch == ' ')
    {
     delay(dotDelay * 4);      // gap between words  
    }
  }
}

void flashSequence(char* sequence)
{
   int i = 0;
   while (sequence[i] != '\0')
   {
       flashDotOrDash(sequence[i]);
       i++;
   }
   delay(dotDelay * 3);    // gap between letters
}

void flashDotOrDash(char dotOrDash)
{
  digitalWrite(ledPin, HIGH);
  if (dotOrDash == '.')
  {
    delay(dotDelay);           
  }
  else // must be a -
  {
    delay(dotDelay * 3);           
  }
  digitalWrite(ledPin, LOW);    
  delay(dotDelay); // gap between flashes
}
```

This sketch includes a loop function that is called automatically and repeatedly calls a **flashSequence** function that you wrote, which itself repeatedly calls a **flashDotOrDash** function that you wrote, which calls **digitalWrite** and **delay** functions that are provided by Arduino!

This is how your sketches should look. Breaking things up into functions makes it much easier to get your code working and makes it easier when you return to it after a period of not using it.

* * *

### Conclusion

In addition to looking at strings and arrays in this chapter, you have also built this more complex Morse translator that I hope will also reinforce the importance of building your code with functions.

In the next chapter, you learn about input and output, by which we mean input and output of analog and digital signals from the Arduino.

## 6

## Input and Output

The Arduino is about physical computing, and that means attaching electronics to the Arduino board. So you need to understand how to use the various options for your connection pins.

Outputs can be digital, which just means switched between being at 0V or at 5V, or analog, which allows you to set the voltage to any voltage between 0V and 5V—although it’s not quite as simple as that, as we shall see.

Likewise, inputs can either be digital (for example, determining whether a button is pressed or not) or analog (such as from a light sensor).

In a book that is essentially about software rather than hardware, we are going to try and avoid being dragged into too much discussion of electronics. However, it will help you to understand what is happening in this chapter if you can find yourself a multimeter and a short length of solid core wire.

If you are interested in learning more about electronics, then you might like to look at my book *Hacking Electronics* (TAB/McGraw-Hill, 2013).

* * *

### Digital Outputs

In earlier chapters, you have made use of the LED attached to digital pin 13 of the Arduino board. For example, in [Chapter 5](#14_Chapter_05.xhtml), you used it as a Morse code signaler. The Arduino board has a whole load of digital pins available.

Let’s experiment with one of the other pins on the Arduino. You will use digital pin 4, and to see what is going on, you will fix some wire to your multimeter leads and attach them to your Arduino. [Figure 6-1](#15_Chapter_06.xhtml_fig-ch6-1) shows the arrangement. If your multimeter has crocodile clips, strip the insulation off the ends of some short lengths of solid core wire and attach the clip to one end, fitting the other end into the Arduino socket. If your multimeter does not have crocodile clips, then wrap one of the stripped wire ends around the probe as shown in [Figure 6-1](#15_Chapter_06.xhtml_fig-ch6-1).

![image](images/fig-ch6-1.jpg)

Figure 6.1 *Measuring outputs with a multimeter*.

The multimeter needs to be set to its 0–20V direct current (DC) range. The negative lead (black) should be connected to the ground (GND) pin and the positive to D3\. The wire is just connected to the probe lead and poked into the socket headers on the Arduino board.

Load sketch 6-01:

```
//sketch 6-01

const int outPin = 3;

void setup()
{
  pinMode(outPin, OUTPUT);
  Serial.begin(9600);
  Serial.println("Enter 1 or 0");
}

void loop()
{
  if (Serial.available() > 0)
  {
    char ch = Serial.read();
    if (ch == '1')
    {
      digitalWrite(outPin, HIGH);
    }
    else if (ch == '0')
    {
      digitalWrite(outPin, LOW);
    }
  }
}
```

At the top of the sketch, you can see the command **pinMode**. You should use this command for every pin that you are using in a project so that Arduino can configure the electronics connected to that pin to be either an input or an output, as in the following example:

```
pinMode(outPin, OUTPUT);
```

As you might have guessed, **pinMode** is a built-in function. Its first argument is the pin number in question (an **int**), and the second argument is the mode, which must be either **INPUT, INPUT_PULLUP** or **OUTPUT**. Note that the mode name must be all uppercase.

This **loop** waits for a command of either **1** or **0** to come from the Serial Monitor on your computer. It it’s a **1**, then pin 3 will be turned on; otherwise, it will be turned off.

Upload the sketch to your Arduino and then open the Serial Monitor (shown in [Figure 6-2](#15_Chapter_06.xhtml_fig-ch6-2)).

![image](images/fig-ch6-2.jpg)

Figure 6.2 *The Serial Monitor*.

So, with the multimeter turned on and plugged into the Arduino, you should be able to see its reading change between 0V and about 5V as you send commands to the board from the Serial Monitor by either pressing 1 and then ENTER or pressing 0 and then ENTER. [Figure 6-3](#15_Chapter_06.xhtml_fig-ch6-3) shows the multimeter reading after a 1 has been sent from the Serial Monitor.

![image](images/fig-ch6-3.jpg)

Figure 6.3 *Setting the output to High*.

If there are not enough pins labeled “D” for your project, you can actually use the pins labeled “A” (for analog) as digital outputs too. To do this, just use the letter A in front of the analog pin name, for example, A0\. You could try this out by modifying the first line in sketch 6-01 to use pin A0 and moving your positive multimeter lead to pin A0 on the Arduino.

That is really all there is to digital outputs, so let’s move on swiftly to digital inputs.

* * *

### Digital Inputs

The most common use of digital inputs is to detect when a switch has been closed. A digital input can either be on or off. If the voltage at the input is less than 2.5V (halfway to 5V), it will be 0 (off), and if it is above 2.5V, it will be 1 (on).

Disconnect your multimeter and upload sketch 6-02 onto your Arduino board:

```
//sketch 6-02

const int inputPin = 5;

void setup()
{
  pinMode(inputPin, INPUT);
  Serial.begin(9600);
}

void loop()
{
  int reading = digitalRead(inputPin);
  Serial.println(reading);
  delay(1000);
}
```

As with using an output, you need to tell the Arduino in the **setup** function that you are going to use a pin as an input. You get the value of a digital input using the **digitalRead** function. This returns 0 or 1.

#### Pull-Up Resistors

The sketch reads the input pin and writes its value to the Serial Monitor once per second. So upload the sketch and open the Serial Monitor. You should see a value appear once per second. Push one end of your bit of wire into the socket for D5 and pinch the end of the wire between your fingers, as shown in [Figure 6-4](#15_Chapter_06.xhtml_fig-ch6-4).

![image](images/fig-ch6-4.jpg)

Figure 6.4 *A digital input with a human antenna*.

Continue pinching for a few seconds and watch the text appear on the Serial Monitor. You should see a mixture of ones and zeros appear in the Serial Monitor. The reason for this is that the inputs to the Arduino board are very sensitive. You are acting as an antenna, picking up electrical interference.

Take the end of the wire that you were holding and push it into the socket for +5V as shown in [Figure 6-5](#15_Chapter_06.xhtml_fig-ch6-5). The stream of text in the Serial Monitor should change to ones.

![image](images/fig-ch6-5.jpg)

Figure 6.5 *Pin 5 connected to +5V*.

Now take the end that was in +5V and put it into one of the GND connections on the Arduino. As you would expect, the Serial Monitor should now display zeros.

A typical use for an input pin is to connect a switch to it. [Figure 6-6](#15_Chapter_06.xhtml_fig-ch6-6) shows how you might connect your switch.

![image](images/fig-ch6-6.jpg)

Figure 6.6 *Connecting a switch to an Arduino board*.

The problem with this is that if the switch is not closed, then the input pin is not connected to anything. It is said to be floating, and could easily give you a false reading. You need your input to be more predictable, and the way to do this is with what is called a pull-up resistor. You will see later how you can enable the Arduino’s built-in series resistors and avoid having to use separate resistors. [Figure 6-7](#15_Chapter_06.xhtml_fig-ch6-7) shows the standard use of a pull-up resistor. It has the effect that if the switch is open, then the resistor pulls up the floating input to 5V. When you press the switch and close the contact, the switch overrides the effect of the resistor, forcing the input to 0V. One side-effect of this is, while the switch is closed, 5V will be across the resistor, causing a current to flow. So, the value of the resistor is selected to be low enough to make it immune from any electrical interference, but at the same time high enough to prevent excessive current drain when the switch is closed.

![image](images/fig-ch6-7.jpg)

Figure 6.7 *Switch with a pull-up resistor*.

#### Internal Pull-Up Resistors

Fortunately, the Arduino board has software-configurable pull-up resistors built into the digital pins. By default, they are turned off. So all you need to do to enable the pull-up resistor on pin 5 for sketch 6-02 is to change the pin mode from INPUT to INPUT_PULLUP.

Sketch 6-03 is the modified version. Upload it to your Arduino board and test it by acting like an antenna again. You should find that this time the input stays at 1 in the Serial Monitor.

```
//sketch 6-03

const int inputPin = 5;

void setup()
{
  pinMode(inputPin, INPUT_PULLUP);
  Serial.begin(9600);
}

void loop()
{
  int reading = digitalRead(inputPin);
  Serial.println(reading);
  delay(1000);
}
```

#### Debouncing

When you press a pushbutton, you would expect that you would just get a single change from 1 (with a pull-up resistor) to 0 as the button is depressed. [Figure 6-8](#15_Chapter_06.xhtml_fig-ch6-8) shows what can happen when you press a button. The metal contacts in the button bounce. So a single button press becomes a series of presses that eventually stabilize.

![image](images/fig-ch6-8.jpg)

Figure 6.8 *Oscilloscope trace of a button press*.

All this happens very quickly; the total time span of the button press on the oscilloscope trace is only 200 milliseconds. This is a very “ropey” old switch. A new tactile, click-type button may not even bounce at all.

Sometimes bouncing does not matter. For instance, sketch 6-04 will light the LED while the button is pressed. In reality, you would not use an Arduino to do this; we are firmly in the realms of theory rather than practice here.

```
//sketch 6-04

const int inputPin = 5;
const int ledPin = 13;

void setup()
{
  pinMode(ledPin, OUTPUT);
  pinMode(inputPin, INPUT_PULLUP);
}

void loop()
{
  int switchOpen = digitalRead(inputPin);
  digitalWrite(ledPin, ! switchOpen);
}
```

Looking at the **loop** function of sketch 6-04, the function reads the digital input and assigns its value to a variable **switchOpen**. This is a 0 if the button is pressed and a 1 if it isn’t (remember that the pin is pulled up to 1 when the button is not pressed).

When you program **digitalWrite** to turn the LED on or off, you need to reverse this value. You do this using the **!** or **not** operator.

If you upload this sketch and connect your wire between D5 and GND (see [Figure 6-9](#15_Chapter_06.xhtml_fig-ch6-9)), you should see the LED light. Bouncing may be going on here, but it is probably too fast for you to see and does not matter.

![image](images/fig-ch6-9.jpg)

Figure 6.9 *Using a wire as a switch*.

One situation where key bouncing would matter is if you were making your switch toggle the LED on and off. That is, if you press the button, the LED comes on and stays on, and when you press the button again, it turns off. If you had a button that bounced, then whether the LED was on or off would just depend on whether you had an odd or even number of bounces.

Sketch 6-05 just toggles the LED without any attempt at “debouncing.” Try it out using your wire as a switch between pin D5 and GND (or use a real switch if you have one):

```
// sketch 6-05
```

```
const int inputPin = 5;
const int ledPin = 13;
int ledValue = LOW;

void setup() 
{
  pinMode(inputPin, INPUT_PULLUP);
  pinMode(ledPin, OUTPUT);
}

void loop() 
{
  if (digitalRead(inputPin) == LOW)
  {
     ledValue = ! ledValue;
     digitalWrite(ledPin, ledValue);
  }
}
```

You will probably find that sometimes the LED toggles, but other times it appears not to toggle. This is bouncing in action!

A simple way to tackle this problem is simply to add a delay after you detect the first button press, as shown in sketch 6-06:

```
// sketch 6-06
const int inputPin = 5;
const int ledPin = 13;
int ledValue = LOW;

void setup() 
{
  pinMode(inputPin, INPUT_PULLUP);
  pinMode(ledPin, OUTPUT);
}

void loop() 
{
  if (digitalRead(inputPin) == LOW)
  {
     ledValue = ! ledValue;
     digitalWrite(ledPin, ledValue);
     delay(500);
  }
}
```

By putting a delay here, nothing else can happen for 500 milliseconds, by which time any bouncing will have subsided. You should find that this makes the toggling much more reliable. An interesting side-effect is that if you hold the button down, the LED just keeps flashing.

If that is all there is to the sketch, then this delay is not a problem. However, if you do more in the **loop**, then using a delay can be a problem; for example, the program would be unable to detect the press of any other button during that 500 milliseconds.

So, this approach is sometimes not good enough and you will need to be a bit more sophisticated. You can write your own advanced debouncing code by hand, but doing so gets complicated and fortunately some fine folks have done all the work for you.

To make use of their work, you must add a library to your Arduino application. To do this, you must download the library itself as a zip file from here: [http://www.arduino.cc/playground/Code/Bounce](http://www.arduino.cc/playground/Code/Bounce). Download the file using the link to GitHub. Once downloaded, the file will be called Bounce2-master.zip. To install it into your Arduino IDE, select the option Add .ZIP Library… from the Sketch menu ([Figure 6-10](#15_Chapter_06.xhtml_fig-ch6-10)).

![image](images/fig-ch6-10.jpg)

Figure 6.10 *Installing the Bounce library*.

Sketch 6-07 shows how you can use the Bounce library. Upload it to your board and see how reliable the LED toggling has become.

```
//sketch 06-07
```

```
 #include <Bounce2.h>

const int inputPin = 5;
const int ledPin = 13;

int ledValue = LOW;
Bounce bouncer = Bounce(); 

void setup() 
{
  pinMode(inputPin, INPUT_PULLUP);
  pinMode(ledPin, OUTPUT);
  bouncer.attach(inputPin);
}

void loop() 
{
  if (bouncer.update() && bouncer.read() == LOW) 
  {
   ledValue = ! ledValue;
   digitalWrite(ledPin, ledValue);
  }
}
```

Using the library is pretty straightforward. The first thing that you will notice is this line:

```
#include <Bounce2.h>
```

This is necessary to tell the compiler to use the Bounce library.

You then have the following line:

```
Bounce bouncer = Bounce();
```

Do not worry about the syntax of this line at the moment; it is actually C++ rather than C syntax, and you will not be meeting C++ until [Chapter 11](#20_Chapter_11.xhtml). For now, you will just have to be content to know that this sets up a **bouncer** object.

The new line in setup links **bouncer** to the **inputPin** using the attach function. From now on, you use that **bouncer** object to find out what the switch is doing rather than reading the digital input directly. It has put a kind of debouncing wrapper around your input pin. So, deciding whether a button has been pressed is wrapped up in this line:

```
if (bouncer.update() && bouncer.read() == LOW)
```

The function **update** returns true if something has changed with the **bouncer** object and the second part of the condition checks whether the button went **LOW**.

* * *

### Analog Outputs

A few of the digital pins—namely digital pins 3, 5, 6, 9, 10, and 11—can provide variable output other than just 5V or nothing. These are the pins on the board with a ~ or “PWM” next to them. PWM stands for Pulse Width Modulation, which refers to the means of controlling the amount of power at the output. It does so by rapidly turning the output on and off.

The pulses are always delivered at the same rate (roughly 500 per second on all the pins except pins 5 and 6, which provide 980 pulses per second), but the length of the pulses is varied. If you were to use PWM to control the brightness of an LED, then if the pulse were long, your LED would be on all the time. If, however, the pulses are short, then the LED is actually lit only for a small portion of the time. This happens too fast for the observer even to tell that the LED is flickering, and it just appears that the LED is lighter or dimmer.

Before you try using an LED, you can test this out with your multimeter. Set the multimeter up to measure the voltage between GND and pin D3 (see [Figure 6-11](#15_Chapter_06.xhtml_fig-ch6-11)).

![image](images/fig-ch6-11.jpg)

Figure 6.11 *Measuring the analog output*.

Now upload sketch 6-08 to your board and open the Serial Monitor (see [Figure 6-12](#15_Chapter_06.xhtml_fig-ch6-12)). Enter **3** and press ENTER. You should see your volt meter register about 3V. You can then try any other voltage between 0 and 5.

![image](images/fig-ch6-12.jpg)

Figure 6.12 *Setting the voltage at an analog output*.

```
//sketch 06-08

const int outputPin = 3;

void setup()
{
  pinMode(outputPin, OUTPUT);
  Serial.begin(9600);
  Serial.println("Enter Volts 0 to 5");
}

void loop()
{
  if (Serial.available() > 0)
  {
    float volts = Serial.parseFloat();
    int pwmValue = volts * 255.0 / 5.0;
    analogWrite(outputPin, pwmValue);
  }
}
```

The program determines the value of PWM output between 0 and 255 by multiplying the desired voltage (0 to 5) by 255/5\. (Readers may wish to refer to Wikipedia for a fuller description of PWM.)

You can set the value of the output by using the function **analogWrite**, which requires an output value between 0 and 255, where 0 is off and 255 is full power. This is actually a great way to control the brightness of an LED. If you were to try to control the brightness by varying the voltage across the LED, you would find that nothing would happen until you got to about 2V; then the LED would very quickly get quite bright. By controlling the brightness using PWM and varying the average amount of time that the LED is on, you achieve much more linear control of the brightness.

* * *

### Analog Input

Digital inputs just give you an on/off answer as to what is happening at a particular pin on the Arduino board. Analog inputs, however, give you a value between 0 and 1023 depending on the voltage at the analog input pin.

The program reads the analog input using the **analogRead** function. Sketch 6-09 displays the reading and actual voltage at the analog pin A0 in the Serial Monitor every half second, so open the Serial Monitor and watch the readings appear, as shown in [Figure 6-13](#15_Chapter_06.xhtml_fig-ch6-13).

![image](images/fig-ch6-13.jpg)

Figure 6.13 *Measuring voltage with an Arduino Uno*.

```
//sketch 6-09

const int analogPin = 0;

void setup()
{
  Serial.begin(9600);
}

void loop()
{
  int reading = analogRead(analogPin);
  float voltage = reading / 204.6;
  Serial.print("Reading=");
  Serial.print(reading);
  Serial.print("\t\tVolts=");
  Serial.println(voltage);
  delay(500);
}
```

When you run this sketch, you will notice that the readings change quite a bit. As with the digital inputs, this is because the input is floating.

Take one end of the wire and put it into a GND socket so that A0 is connected to GND. Your readings should now stay at 0\. Move the end of the lead that was in GND and put it into 5V and you should get a reading of around 1023, which is the maximum reading. So, if you were to connect A0 to the 3.3V socket on the Arduino board, the Arduino volt meter should tell you that you have about 3.3V.

The value of 204.6 is 1023 (the maximum analog reading) divided by 5 (the maximum voltage). **Serial.print** is used to send messages to the serial monitor without beginning a new line, which only happens when **Serial.println** is used. The \t in the messages is used to represent one tab stop so that the numbers line up.

* * *

### Conclusion

This concludes our chapter on the basics of getting signals into and out of the Arduino. In the next chapter, we will look at some of the features provided in the standard Arduino library.

## 7

## The Standard Arduino Library

This library is where all the goodies live. You can only get so far with the core C language; what you really need is a big collection of functions that you can use in your sketches.

You have already met a fair few of these, such as **pinMode, digitalWrite**, and **analogWrite**. But actually, there are many more. There are functions that you can use for doing math, making random numbers, manipulating bits, detecting pulses on an input pin, and using something called interrupts.

The Arduino language is based on an earlier library called Wiring and it complements another library called Processing. The Processing library is very similar to Wiring, but it is based on the Java language rather than C and is used on your computer to link to your Arduino over USB. In fact, the Arduino IDE application that you run on your computer is based on Processing. If you find yourself wanting to write some fancy interface on your computer to talk to an Arduino, then take a look at Processing ([www.processing.org](http://www.processing.org)).

* * *

### Random Numbers

Despite the experience of anyone using a PC, computers are in actual fact very predictable. Occasionally it is useful to be able to deliberately make your Arduino unpredictable. For example, you might want to make a robot take a “random” path around a room, heading for a random amount of time in one direction, turning a random number of degrees, and then setting off again. Or, you might be contemplating making an Arduino-based die that gives you a random number between one and six.

The Arduino standard library provides you with a feature to do just this. It is the function called **random. random** returns an **int** and it can take either one argument or two. If it just takes one argument, then it will return a random number between zero and the argument minus one.

The two-argument version produces a random number between the first argument (inclusive) and the second argument minus one. Thus **random(1, 10)** produces a random number between one and nine.

Sketch 7-01 pumps out numbers between one and six to the Serial Monitor.

```
//sketch 7-01

void setup()
{
  Serial.begin(9600);
}

void loop()
{
  int number = random(1, 7);
  Serial.println(number);
  delay(500); 
}
```

If you upload this sketch to your Arduino and open the Serial Monitor, you will see something like [Figure 7-1](#16_Chapter_07.xhtml_fig-ch7-1).

![image](images/fig-ch7-1.jpg)

Figure 7.1 *Random numbers*.

If you run this a few times you will probably be surprised to see that every time you run the sketch, you get the same series of “random” numbers.

The output is not really random; the numbers are called *pseudo-random* numbers because they have a random distribution. That is, if you ran this sketch and collected a million numbers, you would get pretty much the same number of ones, twos, threes, and so on. The numbers are not random in the sense of being unpredictable. In fact, it is so against the workings of a microcontroller to be random that it just plain can’t do it without some intervention from the real world.

You can provide this intervention to make your sequence of numbers less predictable by *seeding* the random number generator. This basically just gives it a starting point for the sequence. But, if you think about it, you cannot just use **random** to seed the random number generator. A commonly used trick is to use the fact that (as discussed in the previous chapter) an analog input will float. So you can use the value read from an analog input to seed the random number generator.

The function that does this is called **randomSeed**. Sketch 7-02 shows how you can add a bit more randomness to your random number generator.

```
//sketch 7-02

void setup()
{
  Serial.begin(9600);
  randomSeed(analogRead(0));
}

void loop()
{
  int number = random(1, 7);
  Serial.println(number);
  delay(500); 
}
```

Try pressing the Reset button a few times. You should now see that your random sequence is different every time.

This type of random number generation could not be used for any kind of lottery. For much better random number generation, you would need hardware random number generation, which is sometimes based on random occurrences, such as cosmic ray events.

* * *

### Math Functions

On rare occasions, you will need to do a lot of math on an Arduino, over and above the odd bit of arithmetic. But, should you need to, there is a big library of math functions available to you. The most useful of these functions are summarized in the following table:

| **Function** | **Description** | **Example** |
| --- | --- | --- |
| **abs** | Returns the unsigned value of its argument. | **abs(12) returns 12****abs(-12) returns 12** |
| **constrain** | Constrains a number to stop it from exceeding a range. The first argument is the number to constrain, the second is the start of the range, and the third is the end of the allowed range of numbers. | **constrain(8, 1, 10) returns 8****constrain(11, 1, 10) returns 10****constrain(0, 1, 10) returns 1** |
| **map** | Maps a number in one range into another range. The first argument is the number to map, the second and third are the “from” range (or source range), and the last two are the “to” range (or destination range). The function is useful for remapping analog input values. | **map(x, 0, 1023, 0, 5000)** |
| **max** | Returns the larger of its two arguments. | **max(10, 11) returns 11** |
| **min** | Returns the smaller of its two arguments. | **min(10, 11) returns 10** |
| **pow** | Returns the first argument raised to the power of the second argument. | **pow(2, 5) returns 32** |
| **sqrt** | Returns the square root of a number. | **sqrt(16) returns 4** |
| **sin, cos, tan** | Perform trigonometric functions. They are not often used. |  |
| **log** | Calculates the temperature from a logarithmic thermistor (for example). |  |

* * *

### Bit Manipulation

A bit is a single digit of binary information, that is, either 0 or 1\. The word *bit* is a contraction of *binary digit.* Most of the time, you use **int** variables that actually comprise 16 bits. This is a bit wasteful if you only need to store a simple true/false value (1 or 0). Actually, unless you are running short of memory, being wasteful is less of a problem than creating difficult-to-understand code, but sometimes it is useful to be able to pack your data tightly.

Each bit in the **int** can be thought of as having a decimal value, and you can find the decimal value of the **int** by adding up the values of all the bits that are a 1\. So in [Figure 7-2](#16_Chapter_07.xhtml_fig-ch7-2), the decimal value of the **int** would be 38\. Actually, it gets more complicated to deal with negative numbers, but that only happens when the leftmost bit becomes a 1.

![image](images/fig-ch7-2.jpg)

Figure 7.2 *An **int***.

When you are thinking about individual bits, decimal values do not really work very well. It is very difficult to visualize which bits are set in a decimal number such as 123\. For that reason, programmers often use something called *hexadecimal*, or, more commonly, just *hex*. Hex is number base 16\. So instead of having digits 0 to 9, you have six extra digits, A to F. This means that each hex digit represents four bits. The following table shows the relationship among decimal, hex, and binary with the numbers 0 to 15:

| **Decimal** | **Hex** | **Binary (Four Digit)** |
| --- | --- | --- |
| 0 | 0 | 0000 |
| 1 | 1 | 0001 |
| 2 | 2 | 0010 |
| 3 | 3 | 0011 |
| 4 | 4 | 0100 |
| 5 | 5 | 0101 |
| 6 | 6 | 0110 |
| 7 | 7 | 0111 |
| 8 | 8 | 1000 |
| 9 | 9 | 1001 |
| 10 | A | 1010 |
| 11 | B | 1011 |
| 12 | C | 1100 |
| 13 | D | 1101 |
| 14 | E | 1110 |
| 15 | F | 1111 |

So, in hex, any **int** can be represented as a four-digit hex number. Thus, the binary number 10001100 would in hex be 8C. The C language has a special syntax for using hex numbers. You can assign a hex value to an **int** as follows:

```
int x = 0x8C;
```

As well as using hex notation for numbers, you can also use binary notation directly using the prefix ‘0b’. For example, the binary used in the hex example of 0x8C could be written directly in binary as:

```
0b10001100
```

The Arduino standard library provides some functions that let you manipulate the 16 bits within an **int** individually. The function **bitRead** returns the value of a particular bit in an **int**; so, for the following example would assign the value 0 to the variable called **bit**:

```
int x = 0b10001100;
int bit = bitRead(x, 0);
```

In the second argument, the bit position starts at 0 and goes up to 15\. It starts with the least significant bit. So the rightmost bit is bit 0, the next bit to the left is bit 1, and so on.

As you would expect, the counterpart to **bitRead** is **bitWrite**, which takes three arguments. The first is the number to manipulate, the second is the bit position, and the third is the bit value. The following example changes the value of the **int** from 2 to 3 (in decimal or hex):

```
int x = 0b10;
bitWrite(x, 0, 1);
```

* * *

### Advanced I/O

There are some useful little functions that you can use to make your life easier when performing various input/output tasks.

#### Generating Tones

The **tone** function allows you to generate a square-wave signal (see [Figure 7-3](#16_Chapter_07.xhtml_fig-ch7-3)) on one of the digital output pins. The most common reason to do this is to generate an audible tone using a loudspeaker or buzzer.

![image](images/fig-ch7-3.jpg)

Figure 7.3 *A square-wave signal*.

The function takes either two or three arguments. The first argument is always the pin number on which the tone is to be generated, the second argument is the frequency of the tone in hertz (Hz), and the optional final argument is the duration of the tone. If no duration is specified, then the tone will continue playing indefinitely, as is the case in sketch 7-03\. This is why we have put the **tone** function call in **setup** rather than in the **loop** function.

```
//sketch 7-03

void setup()
{
  tone(4, 500);
}

void loop() {}
```

To stop a tone that is playing, you use the function **noTone**. This function has just one argument, which is the pin on which the tone is playing.

#### Feeding Shift Registers

Sometimes the Arduino Uno just doesn’t have enough pins. When driving a large number of LEDs, for example, a common technique is to use a shift register chip. This chip reads data one bit at a time, and then when it has enough, it latches all those bits onto a set of outputs (one per bit).

To help you use this technique, there is a handy function called **shiftOut**. This function takes four arguments:

♦ The number of the pin on which the bit to be sent will appear.

♦ The number of the pin to be used as a clock pin. This toggles every time a bit is sent.

♦ A flag to determine whether the bits will be sent starting with the least significant bit or the most significant. This should be one of the constants **MSBFIRST** or **LSBFIRST**.

♦ The byte of data to be sent.

* * *

### Interrupts

One of the things that tend to frustrate programmers used to “programming in the large” is that the Arduino can do only one thing at a time. If you like to have lots of threads of execution all running at the same time in your programs, then you are out of luck. Although a few people have developed projects that can execute multiple threads in this way, generally this capability is unnecessary for the type of uses that an Arduino is normally put to. The closest an Arduino usually gets to such execution is the use of interrupts.

Two of the pins on the Arduino Uno (D2 and D3) can have interrupts attached to them. That is, these pins act as inputs that, if the pins receive a signal in a specified way, the Arduino’s processor will suspend whatever it was doing and run a function attached to that interrupt.

Sketch 7-04 blinks an LED, but then changes the blink period when an interrupt is received. You can simulate an interrupt by connecting your wire between pin D2 and GND and using the internal pull-up resistor to keep the interrupt high most of the time.

```
//sketch 7-04

const int interruptPin = 2;
const int ledPin = 13;
int period = 500;

void setup()
{
  pinMode(ledPin, OUTPUT);
  pinMode(interruptPin, INPUT_PULLUP);
  attachInterrupt(0, goFast, FALLING);
}

void loop() 
{
  digitalWrite(ledPin, HIGH);
  delay(period);
  digitalWrite(ledPin, LOW);
  delay(period);  
}

void goFast()
{
  period = 100;
}
```

The following is the key line in the **setup** function of this sketch:

```
attachInterrupt(0, goFast, FALLING);
```

The first argument specifies which of the two interrupts you want to use. Rather confusingly, a 0 here means you are using pin 2, while a 1 means you are using pin 3.

The next argument is the name of the function that is to be called when there is an interrupt, and the final argument is a constant that will be one of **CHANGE, RISING**, or **FALLING**. [Figure 7-4](#16_Chapter_07.xhtml_fig-ch7-4) summarizes these options.

![image](images/fig-ch7-4.jpg)

Figure 7.4 *Types of interrupt signals*.

If the interrupt mode is **CHANGE**, then either a **RISING** from 0 to 1 or a **FALLING** from 1 to 0 will both trigger an interrupt.

You can disable interrupts using the function **noInterrupts**. This stops all interrupts from both interrupt channels. You can resume using interrupts again by calling the function **interrupts**.

Different Arduino boards have different interrupt names for different pins so if you are not using an Arduino Uno, check the documentation for your board on [http://www.arduino.cc](http://www.arduino.cc).

* * *

### Conclusion

In this chapter, you have looked at some of the handy features that the Arduino standard library provides. These features will save you some programming effort, and if there is one thing that a good programmer likes, it is being able to use high-quality work done by other people.

In the next chapter, we will extend what we learned about data structures in [Chapter 5](#14_Chapter_05.xhtml) and look at how you go about remembering data on the Arduino after the power goes off.

## 8

## Data Storage

When you give values to variables, the Arduino board will remember those values only as long as the power is on. The moment that you turn the power off or reset the board, all that data is lost.

In this chapter, we look at some ways to hang on to that data.

* * *

### Constants

If the data that you want to store does not change, then you can just set the data up each time that the Arduino starts. An example of this approach is the case in the letters array in your Morse code translator of [Chapter 5](#14_Chapter_05.xhtml) (sketch 5-05).

You used the following code to define a variable of the correct size and fill it with the data that you needed:

```
char* letters[] = {
  ".-", "-...", "-.-.", "-..", ".", 
     "..-.", "--.", "....", "..",    // A-I
  ".---", "-.-", ".-..", "--", "-.", 
     "---", ".--.", "--.-", ".-.",  // J-R
  "...", "-", "..-", "...-", ".--", 
     "-..-", "-.--", "--.."          // S-Z
};
```

You may remember that you did the calculation and decided that you had plenty of your meager 2K to spare. However, if memory was a bit tight, it would be far better to be able to store this data in the 32K of flash memory used to store programs, rather than the 2K of RAM. There is a means of doing this. It is a directive called **PROGMEM;** it lives in a library and is a bit awkward to use.

* * *

### Storing Data in Flash Memory

To store your data in flash memory, you have to include the **PROGMEM** library as follows:

```
#include <avr/pgmspace.h>
```

The purpose of this command is to tell the compiler to use the **pgmspace** library for this sketch. In this case, a library is a set of functions that someone else has written and that you can use in your sketches without having to understand all the details of how those functions work.

Because you are using this library, the **PROGMEM** keyword and the **pgm_read_word** function are available. You will use both in the sketches that follow.

This library is included as part of the Arduino software and is an officially supported Arduino library. A good collection of such official libraries is available, and many unofficial libraries, developed by people like you and made for others to use, are also available on the Internet. Such unofficial libraries must be installed into your Arduino environment. You will learn more about these libraries, as well as how to write your own libraries, in [Chapter 11](#20_Chapter_11.xhtml).

When using **PROGMEM**, you have to make sure that you use special **PROGMEM**-friendly data types. Unfortunately, that does *not* include an array of variable length **char** arrays. However, it does include access to an array of **char** arrays if those **char** arrays are of fixed size. The full program is very similar to that of sketch 5-05 in [chapter 5](#14_Chapter_05.xhtml). You may like to open sketch 8-01 in the IDE while I highlight the differences.

There is a new constant called maxLen that contains the maximum length of a single character’s dots and dashes plus one for the null character on the end.

The structure to contain the letters now looks like this:

```
PROGMEM const char letters[26][maxLen] = {
  ".-", "-...", "-.-.", "-..", ".", "..-.", "--.", "....", "..",    // A-I
  ".---", "-.-", ".-..", "--", "-.", "---", ".--.", "--.-", ".-.",  // J-R
  "...", "-", "..-", "...-", ".--", "-..-", "-.--", "--.."          // S-Z
};
```

The **PROGMEM** keyword indicates that the data structure is to be stored in flash. You can only store constants like this; once in the flash, the data structure cannot be changed, hence the use of **const**. The size of the array also has to be fully specified as 26 letters by **maxLen** (minus 1) dots and dashes.

The loop function is also slightly different from sketch 5-05.

```
void loop()                    
{
  char ch;
  char sequence[maxLen];
  if (Serial.available() > 0)
  {
    ch = Serial.read();
    if (ch >= 'a' && ch <= 'z')
    {
      memcpy_P(&sequence, letters[ch - 'a'], maxLen);
      flashSequence(sequence);
    }
    else if (ch >= 'A' && ch <= 'Z')
    {
      memcpy_P(&sequence, letters[ch - 'A'], maxLen);
      flashSequence(sequence);
    }
    else if (ch >= '0' && ch <= '9')
    {
      memcpy_P(&sequence, numbers[ch - '0'], maxLen);
      flashSequence(sequence);
    }
    else if (ch == ' ')
    {
      delay(dotDelay * 4);  // gap between words  
    }
  }
}
```

The data may look like an array of strings, but actually internally it is stored in flash in a way that can only be accessed by the special function **memcp_P**, which copies the flash data into a **char** array called **sequence** that is initialized to **maxSize** characters in length.

The & character before **sequence** allows **memcpy_P** to modify the data inside the sequence character array.

I have not listed sketch 8-01 here, as it is a little lengthy, but you may wish to load it and verify that it works the same way as the RAM-based version.

In addition to creating the data in a special way, you also have to read the data back a special way. Your code to get the code string for a Morse letter from the array has to be modified to look like this:

```
strcpy_P(buffer, (char*)pgm_read_word(&(letters[ch - 'a'])));
```

This uses a **buffer** variable into which the **PROGMEM** string is copied, so that it can be used as a regular **char** array. This needs to be defined as a global variable as follows:

```
char buffer[6];
```

This approach works only if the data is constant—that is, you are not going to change it while the sketch is running. In the next section, you will learn about using the EEPROM memory that is intended for storing persistent data that can be changed.

If you have individual strings that are perhaps formatted for messages to be displayed on the serial monitor, then Arduino C provides a handy shortcut. You can just enclose the string in F() as shown in the example below:

```
Serial.println(F("Hello World"));
```

The string will then be stored in flash memory, rather than use up RAM.

* * *

### EEPROM

The ATMega328 at the heart of an Arduino Uno has a kilobyte of electrically erasable read-only memory (EEPROM). EEPROM is designed to remember its contents for many years. Despite its name, it is not really read-only. You can write to it.

The official Arduino commands for reading and writing to EEPROM are just as awkward to use as the ones for using **PROGMEM**. You have to read and write to and from EEPROM one byte at a time.

The example of sketch 8-02 allows you to enter a single-digit letter code from the Serial Monitor. The sketch then remembers the digit and repeatedly writes it out on the Serial Monitor.

```
// sketch 8-02
#include <EEPROM.h>

int addr = 0;
char ch;

void setup()
{
  Serial.begin(9600);
  ch = EEPROM.read(addr);
}

void loop()
{
  if (Serial.available() > 0)
  {
    ch = Serial.read();
    EEPROM.write(0, ch);
    Serial.println(ch);
  }
  Serial.println(ch);
  delay(1000);
}
```

To try this sketch, open the Serial Monitor and enter a new character. Then unplug the Arduino and plug it back in. When you reopen the Serial Monitor, you will see that the letter has been remembered.

The function **EEPROM.write** takes two arguments. The first is the address, which is the memory location in EEPROM and should be between 0 and 1023\. The second argument is the data to write at that location. This must be a single byte. A character is represented as eight bits, so this is fine, but you cannot directly store a 16-bit **int**.

#### Storing an int in EEPROM

To store a two-byte **int** in locations 0 and 1 of the EEPROM, you could do this:

```
 int x = 1234; 
  EEPROM.write(0, highByte(x));
  EEPROM.write(1, lowByte(x));
```

The functions **highByte** and **lowByte** are useful for separating an **int** into two bytes. [Figure 8-1](#17_Chapter_08.xhtml_fig-ch8-1) shows how this **int** is actually stored in the EEPROM.

![image](images/fig-ch8-1.jpg)

Figure 8.1 *Storing a 16-bit integer in EEPROM*.

To read the **int** back out of EEPROM, you need to read the two bytes from the EEPROM and reconstruct the **int**, as follows:

```
byte high = EEPROM.read(0);
byte low = EEPROM.read(1);
int x = (high << 8) + low;
```

The **<<** operator is a bit shift operator that moves the eight high bytes to the top of the **int** and then adds in the low byte.

#### Using the AVR EEPROM Library

The official Arduino way of using EEPROM is just fine if you are only using single bytes. However, as you saw with **ints**, this becomes more complicated for larger data types. It’s even worse for floats (4 bytes). Fortunately, there is an alternative method that uses one of the libraries that Arduino itself uses called the AVR EEPROM library. This allows you to read and write as much data as will fit into your EEPROM with single commands.

The example of sketch 8-03 uses this library to write and then read an **int**.

```
// sketch 08-03

#include <avr/eeprom.h>

void setup() 
{
  Serial.begin(9600);
  int i1 = 123;
  eeprom_write_block(&i1, 0, 2);
  int i2 = 0;
  eeprom_read_block(&i2, 0, 2);
  Serial.println(i2);
}

void loop() 
{
}
```

The library is actually included in the Arduino IDE, so you do not need to install anything, just include the library. The function that writes to EEPROM is called **eeprom_write_block** and, as the name suggests, it writes a block of memory into EEPROM. Its first parameter is a reference to the variable. In this case, this is to **i1** that has been given a value of 123\. There is an & in front of **i1** as the function expects the parameter to be a reference to the variable’s address in memory rather than the variable’s value. The second parameter is the starting byte in EEPROM where the block should be written and the final parameter is the number of bytes to write (2 for an **int**).

Reading the value from EEPROM back into a RAM variable (**i2**) is a mirror of the writing process with the same parameters.

#### Storing a float in EEPROM

Storing a float in EEPROM using the AVR EEPROM library is very similar to storing an **int** as sketch 8-04 illustrates.

```
// sketch 08-04

#include <avr/eeprom.h>

void setup() 
{
  Serial.begin(9600);
  float f1 = 1.23;
  eeprom_write_block(&f1, 0, 4);
  float f2 = 0;
  eeprom_read_block(&f2, 0, 4);
  Serial.println(f2);
}

void loop() 
{
}
```

The main difference is that this time the final parameter to **eeprom_write_block** and **eeprom_read_block** is 4 (4 bytes) rather than 2.

#### Storing a String in EEPROM

Writing and reading character strings into the EEPROM is also best accomplished using the AVR EEPROM library. Sketch 8-05 illustrates this with an example that reads and writes passwords from EEPROM. The sketch first displays this password read from EEPROM and then prompts you to enter a new password ([Figure 8-2](#17_Chapter_08.xhtml_fig-ch8-2)). Having set the password, you can unplug the Arduino to power it down and when you plug it back in again and open the Serial Monitor, the old password will still be there.

![image](images/fig-ch8-2.jpg)

Figure 8.2 *Missing figure caption*.

```
// sketch 08-05

#include <avr/eeprom.h>

const int maxPasswordSize = 20;

char password[maxPasswordSize];

void setup() 
{
  eeprom_read_block(&password, 0, maxPasswordSize);
  Serial.begin(9600);
}

void loop() 
{
  Serial.print("Your password is:");
  Serial.println(password);
  Serial.println("Enter a NEW password");     
  while (!Serial.available()) {};
  int n = Serial.readBytesUntil('\n', password, 
    maxPasswordSize);
  password[n] = '\0';
  eeprom_write_block(password, 0, maxPasswordSize);  
  Serial.print("Saved Password: ");
  Serial.println(password);
}
```

The character array **password** has a fixed size of 20 characters that must also include the ‘\0’ end marker. In the **startup** function the contents of EEPROM starting at location 0 are read into **password**.

The **loop** function displays the necessary messages and then the **while** loop does nothing until serial communication arrives, indicated by **Serial.available** returning more than 0\. The **readBytesUntil** function will then keep reading characters until the end of line character ‘\n’ is encountered. The bytes being read will be put straight into the **password char** array.

Because you don’t know how long a password will be entered, the result of reading the bytes is stored in **n** and then element **n** of the password is set to ‘\0’ to mark the end of the string. Finally, the new password is printed to the Serial Monitor to confirm the change in password.

#### Clearing the Contents of EEPROM

When writing to EEPROM, remember that even uploading a new sketch will not clear the EEPROM, so you may have leftover values in there from a previous project. Sketch 8-06 resets all the contents of EEPROM to zeros:

```
// sketch 8-06
#include <EEPROM.h>

void setup()                 
{
  Serial.begin(9600);
  Serial.println("Clearing EEPROM")a;
  for (int i = 0; i < 1024; i++)
  {
    EEPROM.write(i, 0);
  }
  Serial.println("EEPROM Cleared");
}

void loop()                    
{
}
```

Also be aware that you can write to an EEPROM location only about 100,000 times before it will become unreliable. So only write a value back to EEPROM when you really need to. EEPROM is also quite slow, taking about 3 milliseconds to write a byte.

* * *

### Compression

When saving data to EEPROM or when using **PROGMEM**, you will sometimes find that you have more to save than you have room to save it. When this happens, it is worth finding the most efficient way of representing the data.

#### Range Compression

You may have a value for which on the face of it you need an **int** or a **float** that is 16-bit. For example, to represent a temperature in degrees Celsius, you might use a **float** value such as 20.25\. When you are storing that into EEPROM, life would be so much easier if you could fit it into a single byte, and you could store twice as much as if you used a **float**.

One way that you can do this is to change the data before you store it. Remember that a byte will allow you to store a positive number between 0 and 255\. So if you only cared about the temperature to the nearest degree Celsius, then you could simply convert the **float** to an **int** and discard the part after the decimal point. The following example shows how to do this:

```
int tempInt = (int)tempFloat;
```

The variable **tempFloat** contains the floating point value. The **(int)** command is called a *type cast* and is used to convert a variable from one type to another compatible type. In this case, the type cast converts the **float** of (for example) 20.25 to an **int** that will simply truncate the number to 20.

If you know that the highest temperature that you care about is 60 degrees Celsius and that the lowest is 0 degrees Celsius, then you could multiply every temperature by 4 before converting it to a byte and saving it. Then when you read the data back from EEPROM, you can divide by 4 to get a value that has a precision of 0.25 of a degree.

The following code example (sketch 8-07) saves such a temperature into EEPROM, then reads it back and displays it in the Serial Monitor as proof:

```
//sketch 8-07

#include <EEPROM.h>

void setup()
{
  float tempFloat = 20.75;
  byte tempByte = (int)(tempFloat * 4);
  EEPROM.write(0, tempByte);

  byte tempByte2 = EEPROM.read(0);
  float temp2 = (float)(tempByte2) / 4;
  Serial.begin(9600);
  Serial.println("\n\n\n");
  Serial.println(temp2);
}

void loop(){}
```

There are other means of compressing data. For instance, if you are taking readings that change slowly—again, changes in temperature are a good example of this—then you can record the first temperature at full resolution and then just record the changes in temperature from the previous reading. This change will generally be small and occupy fewer bytes.

* * *

### Conclusion

You now know a little about how to make your data hang around after the power has gone off. In the next chapter, you will look at displays.

## 9

## Displays

In this chapter, you look at how to write software to control displays. [Figure 9-1](#18_Chapter_09.xhtml_fig-ch9-1) shows the two types of display that you will use. The first is an alphanumeric LCD display shield. The second is a 128- × 64-pixel OLED (organic light-emitting diode) graphical display. These two types of display are very popular for the Arduino.

![image](images/fig-ch9-1.jpg)

Figure 9.1 *An alphanumeric LCD shield (left) and OLED display (right)*.

This is a book about software, not hardware, but in this chapter, we will have to explain a little about how the electronics of these displays work so that you understand how to drive them.

* * *

### Alphanumeric LCD Displays

The LCD module that we use is an Arduino shield that can just be plugged on top of an Arduino board. In addition to its display, it also has some buttons. There are a number of different shields, but nearly all of them use the same LCD controller chip (the HD44780), so look for a shield that uses this controller chip.

I used the DFRobot LCD Keypad Shield for Arduino. This module supplied by DFRobot ([www.robotshop.com](http://www.robotshop.com)) is inexpensive and provides an LCD display that is 16 characters by 2 rows and also has 6 pushbuttons.

The shield comes assembled, so no soldering is required; you just plug it on top of your Arduino board (see [Figure 9-2](#18_Chapter_09.xhtml_fig-ch9-2)).

![image](images/fig-ch9-2.jpg)

Figure 9.2 *LCD shield attached to an Arduino board*.

The LCD shield uses seven of the Arduino pins to control the LCD display and one analog pin for the buttons. So we cannot use these Arduino pins for any other purpose.

* * *

### A USB Message Board

For a simple example of a simple use of the display, we are going to make a USB message board. This will display messages sent from the Serial Monitor.

The Arduino IDE comes with an LCD library. This greatly simplifies the process of using an LCD display. The library gives you useful functions that you can call:

♦ **clear** clears the display of any text.

♦ **setCursor** sets the position in row and column where the next thing that you print will appear.

♦ **print** writes a string at that position.

This example is listed in sketch 9-01:

```
// sketch 9-01 USB Message Board

#include <LiquidCrystal.h>

// lcd(RS, E, D4, D5, D6, D7)
LiquidCrystal lcd(8, 9, 4, 5, 6, 7);
int numRows = 2;
int numCols = 16;

void setup()
{
  Serial.begin(9600);
  lcd.begin(numRows, numCols);
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("Arduino");
  lcd.setCursor(0,1);
  lcd.print("Rules");
}

void loop()
{
  if (Serial.available() > 0) 
  {
    char ch = Serial.read();
    if (ch == '#')
    {
      lcd.clear();
    }
    else if (ch == '/')
    {
      // new line
      lcd.setCursor(0, 1);
    }
    else
    {
      lcd.write(ch);
    }
  }
}
```

As with all Arduino libraries, you have to start by including the library to make the compiler aware of it.

The next line defines which Arduino pins are used by the shield and for what purpose. If you are using a different shield, then you may well find that the pin allocations are different, so check in the documentation for the shield.

In this case, the six pins used to control the display are D4, D5, D6, D7, D8, and D9\. The purpose of each of these pins is described in [Table 9-1](#18_Chapter_09.xhtml_tab-ch9-1).

| **Parameter to LCD()** | **Arduino Pin** | **Purpose** |
| --- | --- | --- |
| RS | 8 | Register Select; this is set to 1 or 0 depending on whether the Arduino is sending data for characters or an instruction. An instruction might make the cursor flash, for example. |
| E | 9 | Enable; this gets toggled to tell the LCD controller chip that the data on the following four pins is ready to be read. |
| Data 4 | 4 | These four pins are used to transfer data. The LCD controller chip used by the shield can use eight-bit or four-bit data. This shield uses four bits, in which case the bits 4–7 are used rather than 0–7. |
| Data 5 | 5 |
| Data 6 | 6 |
| Data 7 | 7 |

Table 9-1 *LCD Shield Pin Assignments*

The **setup** function is straightforward. You start serial communications so that the Serial Monitor can send commands and initialize the LCD library with the dimensions of the display being used. You also display the message “Arduino Rules” on two lines by setting the cursor to top-left, printing “Arduino,” then moving the cursor to the start of the second row and printing “Rules.”

Most of the action takes place in the **loop** function, which checks for any incoming characters from the Serial Monitor. The sketch deals with characters one at a time.

Apart from ordinary characters that the sketch will simply display, there are also a couple of special characters. If the character is a **#**, then the sketch clears the whole display, and if the character is a **/**, the sketch moves to the second line. Otherwise, the sketch simply displays the character at the current cursor position using **write**. The function **write** is like **print**, but it prints only a single character rather than a string of characters.

* * *

### Using the Display

Try out sketch 9-01 by uploading it to the board and then attaching the shield. Note that you should always unplug the Arduino board so that it is off before you plug in a shield.

Open up the Serial Monitor and try typing in the text shown in [Figure 9-3](#18_Chapter_09.xhtml_fig-ch9-3).

![image](images/fig-ch9-3.jpg)

Figure 9.3 *Sending commands to the display*.

* * *

### Other LCD Library Functions

In addition to the functions that you have used in this example, there are a number of other functions that you can use:

♦ **home** is the same as **setCursor(0,0)**: it moves the cursor to top-left.

♦ **cursor** displays a cursor.

♦ **noCursor** specifies not to display a cursor.

♦ **blink** makes the cursor blink.

♦ **noBlink** stops the cursor from blinking.

♦ **noDisplay** turns off the display without removing the content.

♦ **display** turns the display back on after **noDisplay**.

♦ **scrollDisplayLeft** moves all the text on the display one character position to the left.

♦ **scrollDisplayRight** moves all the text on the display one character position to the right.

♦ **autoscroll** activates a mode in which, as new characters are added at the cursor, the existing text is pushed in the direction determined by the functions **leftToRight** and **rightToLeft.**

♦ **noAutoscroll** turns **autoscroll** mode off.

* * *

### OLED Graphic Displays

OLED (organic light-emitting diode) displays are bright and crisp and are fast replacing LCD displays in consumer appliances. The type of OLED described here uses an interface bus called I2C and has a driver chip called the SD1306\. These can be bought on eBay, Adafruit, and many other suppliers around the Internet. Look for a device with just four interface pins as these are easiest to work with.

[Figure 9-4](#18_Chapter_09.xhtml_fig-ch9-4) shows an Arduino Uno connected to a 0.96-inch OLED display. These boards have a resolution of 128 × 64 pixels and are monochrome—in this case, blue.

![image](images/fig-ch9-4.jpg)

Figure 9.4 *An Arduino Uno and OLED display*.

* * *

### Connecting an OLED Display

You can connect your OLED display to your Arduino using female-to-male jumper wires. You can buy these from many sources including Adafruit (product 825). You will need to make the following connections:

♦ GND on the display to GND on the Arduino.

♦ VCC on the display to 5V on the Arduino.

♦ SCL on the display to the SCL pin of the Arduino. This is not labeled on the Arduino Uno itself but is indicated in [Figure 9-5](#18_Chapter_09.xhtml_fig-ch9-5).

♦ SDA on the display to the SDA pin of the Arduino (also see [Figure 9-5](#18_Chapter_09.xhtml_fig-ch9-5)).

![image](images/fig-ch9-5.jpg)

Figure 9.5 *Identifying the SCL and SDA pins of an Arduino Uno*.

I2C (pronounced *I squared C*) is a serial bus standard commonly used to connect sensors and displays to microcontrollers like the Arduino. As well as the GND and positive power pins, it uses a data pin (SDA) and clock pin (SCK) to communicate with the microcontroller by sending serial data 1 bit at a time.

* * *

### Software

Sketch 9-02 will count in seconds up to 9999 and then reset to 0. Before uploading it to your Arduino, you need to find out the I2C address of the display. This will be a hexadecimal number and may be written on the back of the OLED display. Many low-cost eBay OLED displays use 0x3c.

You will also need to install some libraries before the sketch will compile. These can both be imported directly from the Arduino IDE’s Library Manager. Open the Library Manager by selecting the menu option Sketch → Include Library → Manage Libraries…. Then scroll down to “Adafruit GFX Library” and click Install ([Figure 9-6](#18_Chapter_09.xhtml_fig-ch9-6)). Then do the same for the “Adafruit SSD1306” library. The SPI and Wire libraries that the sketch needs are both installed by default in the Arduino IDE.

![image](images/fig-ch9-6.jpg)

Figure 9.6 *Installing the Adafruit libraries*.

```
// sketch 09_02

#include <SPI.h>
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

Adafruit_SSD1306 display(4); // pick an unused pin

void setup()   
{                
  display.begin(SSD1306_SWITCHCAPVCC, 0x3c);  // may need to change this
  display.setTextSize(4);
  display.setTextColor(WHITE);
}

void loop() 
{
  static int count = 0;
  display.clearDisplay();
  display.drawRoundRect(0, 0, 127, 63, 8, WHITE);
  display.setCursor(20,20);
  display.print(count);
  display.display();
  count ++;
  if (count > 9999)
  {
    count = 0;
  }
  delay(1000);
}
```

The sketch starts by importing the libraries that it needs and then a **display** variable initialized. The parameter supplied is that of the optional “reset” pin that some OLED displays (including those supplied by Adafruit) have. If your display does not have a reset pin, then set this value to a pin that is not being connected to anything. In this case I chose pin 4.

The **setup** function initializes the display and you may need to change the I2C address supplied as the second parameter from 0x3c to a different value. **setup** then sets the font size to 4 (large) and the text color to white (anything but black will display in the LED color).

The **loop** function clears the display, draws a round-cornered rectangle, sets the cursor position, and then prints the value of count. The display will not actually be updated until the command **display.display()** is run. The variable **count** is then incremented and there is a delay of one second.

The Adafruit GFX library provides all sorts of fancy drawing routines that you can use with the graphical display. For documentation on this library see [https://learn.adafruit.com/adafruit-gfx-graphics-library](https://learn.adafruit.com/adafruit-gfx-graphics-library).

* * *

### Conclusion

You can see that programming shields is not hard, particularly when there is a library that can do a lot of the work.

In the next chapter, you will use an Arduino to connect to your network and the Internet.

## 10

## Arduino Internet of Things Programming

The Internet of Things (IoT) is the concept that more and more devices will become connected to the Internet. That doesn’t just mean more and more computers using browsers, but actual appliances and wearable and portable technology. This includes all sorts of home automation from smart appliances and lighting, to security systems and even Internet-operated pet feeders as well as lots of less practical but fun projects.

Arduinos are used a lot to create IoT projects, but require either a specialized Arduino or shields to provide the network capabilities that will allow you to measure and control things over your local network and the Internet. The network interface might be in the form of a cabled Ethernet connection or a WiFi connection.

In this chapter we will explore the use of an Arduino with an Ethernet shield, or a combined device like the EtherTen from Freetronics, as well as the increasingly popular ESP8266 WiFi boards that can be programmed in Arduino C and are wonderfully low cost, starting at $5 or less ([Figure 10-1](#19_Chapter_10.xhtml_fig-ch10-1)).

![image](images/fig-ch10-1.jpg)

Figure 10.1 *Left to right: Arduino Uno + Ethernet shield, EtherTen, and Node MCU ESP8266 boards*.

You will learn how to run a local Web server and also make outgoing Web requests to Internet services using both of these types of board. Finally, some other options like the Particle Photon and Arduino Yun will be briefly described.

* * *

### Communicating with Web Servers

Before looking at how the Arduino deals with communication between a browser and the Web server that it uses, you need some understanding of the Hypertext Transfer Protocol (HTTP) and the Hypertext Markup Language (HTML).

#### HTTP

The Hypertext Transport Protocol is the method by which Web browsers communicate with a Web server.

When you go to a page using a Web browser, the browser sends a request to the server hosting that page, saying what it wants. What the browser asks for may be simply the contents of a page in HTML. The Web server is always listening for such requests, and when it receives one, it processes it. In this simple case, processing the request just means sending back HTML that you have specified in the Arduino sketch.

#### HTML

The Hypertext Markup Language is a way of adding formatting to ordinary text so that it looks good when the browser displays it. For example, the following code is HTML that displays on a browser page as shown in [Figure 10-2](#19_Chapter_10.xhtml_fig-ch10-2):

![image](images/fig-ch10-2.jpg)

Figure 10.2 *An HTML example*.

```
<html>
<body>
<h1>Programming Arduino</h1>
<p>A book about programming Arduino</p>
</body>
</html>
```

The HTML contains tags. Tags have a start and an end and usually contain other tags. The start of a tag has a **<** and then the tag name, and then a **>**; for example, **<html>**. The end of a tag is similar except that it has a **/** after the **<**. In the preceding example, the outermost tag is **<html>** that contains a tab called **<body>**. All webpages should start with such tags, and you can see the corresponding ends for those tags at the end of the file. Note that you have to put the end tags in the right order, so the **body** tag must be closed before the **html** tag.

Now we get to the interesting bit in the middle, the **h1** and **p** tags. These are the parts of the example that are actually displayed.

The **h1** tag indicates a level 1 header. This has the effect of displaying the text that it contains in a large bold font. The **p** tag is a paragraph tag, and so all the text contained within it is displayed as a paragraph.

This really just scratches the surface of HTML. Many books and Internet resources are available for learning about HTML.

* * *

### Arduino Uno as a Web Server

The first example sketch simply uses the Arduino and Ethernet shield to make a small Web server. It’s definitely not a Google server farm, but it will allow you to send a Web request to your Arduino and view the results in a browser on your computer. An alternative to Arduino Uno and Ethernet Shield is to use the EtherTen board from Freetronics that combines both Uno and shield into one board that is compatible with the Uno and shield.

Before uploading sketch 10-01, you may want to make a change to the code. If you look at the top of the sketch, you will see the following line:

```
byte mac[] = { 0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED };
```

The **mac** address must be unique among all the devices connected to your network.

Attach the Arduino to your computer using the USB lead and upload the sketch. You can now disconnect the USB lead and attach the power supply to the Arduino and the Ethernet lead.

Open the Serial Monitor of the Arduino IDE and you should see something like [Figure 10-3](#19_Chapter_10.xhtml_fig-ch10-3) telling you the IP address that has been allocated to your Arduino by your network. Navigate to that IP address using your browser and you should see a webpage like the one shown in [Figure 10-4](#19_Chapter_10.xhtml_fig-ch10-4).

![image](images/fig-ch10-3.jpg)

Figure 10.3 *Finding the IP address of your Arduino*.

![image](images/fig-ch10-4.jpg)

Figure 10.4 *A simple Arduino server example*.

The listing for sketch 10-01 is as follows:

```
// sketch 10-01 Simple Server Example
#include <SPI.h>
#include <Ethernet.h>

// MAC address just has to be unique. This should work
byte mac[] = { 0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED };

EthernetServer server(80);

void setup()
{
  Serial.begin(9600);
  Ethernet.begin(mac);
  server.begin();
  Serial.print("Server started on: ");
  Serial.println(Ethernet.localIP());
}

void loop()
{
  // listen for incoming clients
  EthernetClient client = server.available();
  if (client) 
  {
    while (client.connected()) 
    {
      // send a standard http response header
      client.println("HTTP/1.1 200 OK");
      client.println("Content-Type: text/html");
      client.println();

      // send the body
      client.println("<html><body>");
      client.println("<h1>Arduino Server</h1>");
      client.print("<p>A0="); 
      client.print(analogRead(0)); 
      client.println("</p>"); 
      client.print("<p>millis="); 
      client.print(millis()); 
      client.println("</p>"); 
      client.println("</body></html>");
      client.stop();
    }
    delay(1);
  }
}
```

As with the LCD library discussed in [Chapter 9](#18_Chapter_09.xhtml), a standard Arduino library takes care of interfacing with the Ethernet shield.

The **setup** function initializes the Ethernet library using the **mac** address that you set earlier. Once the connection has been established and your network has been allocated an IP address, that is displayed in the Serial Monitor as shown in [Figure 10-3](#19_Chapter_10.xhtml_fig-ch10-3) so that you know where to point your browser.

The **loop** function is responsible for servicing any requests that come to the Web server from a browser. If a request is waiting for a response, then calling **server.available** will return a client. A client is an object; you will learn a bit more about what this means in [Chapter 11](#20_Chapter_11.xhtml). But for now, all that you need to know is that if a client exists (tested by the first **if** statement); you can then determine if it is connected to the Web server by calling **client.connected**.

The next three lines of code print out a return header. This just tells the browser what type of content to display. In this case, the browser is to display HTML content.

Once the header has been written, all that remains is to write the remaining HTML back to the browser. This must include the usual **<html>** and **<body>** tags, and also includes a **<h1>** header tag and two **<p>** tags that will display the value on the analog input A0 and the value returned by the **millis** function; that value is the number of milliseconds since the Arduino was last reset.

Finally, **client.stop** tells the browser that the message is complete. The browser then displays the page.

In a later section in this chapter, this example will be repeated, but using WiFi and an ESP8266 board rather than Ethernet.

* * *

### Web-Controlled Arduino

This second example of using an Ethernet shield allows you to turn the Arduino pins D3 to D7 on and off using a Web form.

Unlike the simple server example, you are going to have to find a way to pass the pin settings to the Arduino.

The method for doing this is called *posting data* and is part of the HTTP standard. For this method to work, you have to build the posting mechanism into the HTML so that the Arduino returns HTML to the browser, which renders a form. This form (shown in [Figure 10-5](#19_Chapter_10.xhtml_fig-ch10-5)) has a selection of On and Off for each pin and an Update button that will send the pin settings to the Arduino.

![image](images/fig-ch10-5.jpg)

Figure 10.5 *A Web interface to Arduino pins*.

When the Update button is pressed, a second request is sent to the Arduino. This will be just like the first request, except that the request will contain request parameters that will contain the values of the pins.

A request parameter is similar in concept to a function parameter. A function parameter enables you to get information to a function, such as the number of times to blink, and a request parameter enables you to pass data to the Arduino that is going to handle the Web request. When the Arduino receives the Web request, it can extract the pin settings from the request parameter and change the actual pins.

The code for the second example sketch follows:

```
// sketch 10-02 Internet Pins

#include <SPI.h>
#include <Ethernet.h>

// MAC address just has to be unique. This should work
byte mac[] = { 0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED };

EthernetServer server(80);

int numPins = 5;
int pins[] = {3, 4, 5, 6, 7};
int pinState[] = {0, 0, 0, 0, 0};
char line1[100];

void setup()
{
  for (int i = 0; i < numPins; i++)
  {
     pinMode(pins[i], OUTPUT);
  }
  Serial.begin(9600);
  Ethernet.begin(mac);
  server.begin();
  Serial.print("Server started on: ");
  Serial.println(Ethernet.localIP());
}

void loop()
{
  EthernetClient client = server.available();
  if (client) 
  {
    while (client.connected()) 
    {
      readHeader(client);
      if (! pageNameIs("/"))
      {
        client.stop();  
        return;
      }
      client.println("HTTP/1.1 200 OK");
      client.println("Content-Type: text/html");
      client.println();

      // send the body
      client.println("<html><body>");
      client.println("<h1>Output Pins</h1>");
      client.println("<form method='GET'>");  
      setValuesFromParams();
      setPinStates();
      for (int i = 0; i < numPins; i++)
      {
         writeHTMLforPin(client, i);
      }
      client.println("<input type='submit' 
        value='Update'/>");
      client.println("</form>");
      client.println("</body></html>");

      client.stop();            
    }
  }
}

void writeHTMLforPin(EthernetClient client, int i)
{
  client.print("<p>D");
  client.print(pins[i]);  
  client.print(" <select name='");
  client.print(i);
  client.println("'>");
  client.print("<option value='0'");
  if (pinState[i] == 0)
  {
    client.print(" selected");
  }
  client.println(">Off</option>");
  client.print("<option value='1'");
  if (pinState[i] == 1)
  {
    client.print(" selected");
  }
  client.println(">On</option>");
  client.println("</select></p>");  
}

void setPinStates()
{
  for (int i = 0; i < numPins; i++)
  {
     digitalWrite(pins[i], pinState[i]);
  }
}

void setValuesFromParams()
{
  for (int i = 0; i < numPins; i++)
  {
    pinState[i] = valueOfParam(i + '0');
  }
}

void readHeader(EthernetClient client)
{
  // read first line of header
  char ch;
  int i = 0;
  while (ch != '\n')
  {
    if (client.available())
    {
      ch = client.read();
      line1[i] = ch;
      i ++;
    }
  }
  line1[i] = '\0'; 
  Serial.println(line1);
}

boolean pageNameIs(char* name)
{
   // page name starts at char pos 4
   // ends with space
   int i = 4;
   char ch = line1[i];
   while (ch != ' ' && ch != '\n' && ch != '?')
   {
     if (name[i-4] != line1[i])
     {
       return false;
     }
     i++;
     ch = line1[i];
   }
   return true;
}

int valueOfParam(char param)
{
  for (int i = 0; i < strlen(line1); i++)
  {
    if (line1[i] == param && line1[i+1] == '=')
    {
      return (line1[i+2] - '0');
    }
  }
  return 0;
}
```

The sketch uses two arrays to control the pins. The first, **pins**, just specifies which pins are to be used. The **pinState** array holds the state of each pin: either 0 or 1.

To get the information coming from the browser form about which pins should be on and which should be off, it is necessary to read the header coming from the browser. In fact, all you need is contained in the first line of the header. You will use a character array **line1** to contain the first line of the header.

When the user clicks on the Update button and submits the form from the browser, the URL for the page will look something like this:

```
http://192.168.1.17/?0=1&1=1&2=0&3=0&4=0
```

The request parameters come after the **?** and are each separated by an **&**. Looking at the first parameter (**0=1**), this means that the first pin in the array (**pins[0]**) should have the value 1\. If you were to look at the first line of the header, you would see those same request parameters there:

```
GET /?0=1&1=1&2=0&3=0&4=0 HTTP/1.1
```

Before the parameters, there is the text **GET /.** This specifies the page requested by the browser. In this case, **/** indicates the root page.

In the loop of the sketch, you call the **readHeader** function to read the first line of the header. You then use the **pageNameIs** function to check that the page request is for the root page **/**.

The sketch then generates the header and the start of the HTML form that is to be displayed. Before writing the HTML for each of the pins, the sketch calls the **setValuesFromParams** function to read each of the request parameters and set the appropriate values in the **pinStates** array. This array is then used to set the values of the pin outputs before the **writeHTMLforPin** function is called for each of the pins. This function generates a selection list for each pin. It has to build this list part by part. The **if** statements ensure that the appropriate options are selected.

The functions **readHeader, pageNameIs**, and **valueOfParam** are useful general-purpose functions that you can make use of in your own sketches.

You can use your multimeter as you did in [Chapter 6](#15_Chapter_06.xhtml) to verify that the pins are indeed turning on and off. If you are feeling more adventurous, you could attach LEDs or relays to the pins to control things.

* * *

### Node MCU Web Server

The ESP8266 is a WiFi System on a Chip. That is, it’s a single chip that pretty much does everything that an Arduino Uno equipped with a WiFi shield could do. It includes a few GPIO pins and an analog input and can be programmed from the Arduino IDE as if it were an official Arduino board.

The two most common boards that use the ESP8266 are shown in [Figure 10-6](#19_Chapter_10.xhtml_fig-ch10-6).

![image](images/fig-ch10-6.jpg)

Figure 10.6 *ESP01 (left) and Node MCU (right) ESP8266 boards*.

The ESP01 board is extremely minimal and only has two GPIO pins and requires a separate USB to serial programmer in order to program it. However, the Node MCU board on the right of [Figure 10-6](#19_Chapter_10.xhtml_fig-ch10-6) includes an Arduino Uno-style USB-to–serial interface chip to program the board as well as a decent selection of GPIO pins. The Node MCU board is the better board to get started with.

The ESP8266 has around 36kB of memory available for us in sketches (far more than the Arduino Uno’s 2kB). The ESP8266 does not have any built-in flash memory, but rather the board it is on, such as the Node MCU, has a separate flash memory chip that, in the case of the Node MCU, provides 4MB of program storage.

None of the ESP8266 boards are official Arduino boards; in fact, the Node MCU board actually comes with its own firmware that uses the Lua programming language rather than Arduino C. However, thanks to the efforts of Sandeep Mistry, this firmware can be replaced and the board programmed almost like any other Arduino board. All ESP8266 boards can also be wired up to the serial port of an Arduino and just used to provide a WiFi interface to a regular Arduino. But, given that the boards are capable of filling in for an Arduino, it makes sense to make full use of their capabilities.

The first step in using a Node MCU is to update your Arduino IDE so that it is aware of this new type of board. You must be using Arduino 1.6 or later for the following instructions to work.

First, open the Arduino IDE Preferences window from the File menu and add the address [http://arduino.esp8266.com/stable/package_esp8266com_index.json](http://arduino.esp8266.com/stable/package_esp8266com_index.json) to the Additional Board Manager URLs field ([Figure 10-7](#19_Chapter_10.xhtml_fig-ch10-7)).

![image](images/fig-ch10-7.jpg)

Figure 10.7 *Adding a Board Manager URL for ESP8288 boards*.

Open the Arduino IDE’s Boards Manager window, which you will find under the Tools → Boards menu option. Scroll down to the bottom of the list and click on the Install button next to the “esp8266 by ESP8266 Community” item.

Close the Boards Manager and now, when you look at the list of possible boards, you will find some new board options for ESP8266-related boards, in particular “Node MCU0.9” and “NodeMCU 1.0”. When you buy your ESP8266 board you will need to check which of these two types it is.

Before you can start programming your Node MCU board, you will need to install drivers for the USB-to-serial chip. This is not the same chip as is used for an Arduino Uno’s USB-to-serial interface, so you will need to download and install the drivers for your platform from [https://github.com/nodemcu/nodemcu-devkit/tree/master/Drivers](https://github.com/nodemcu/nodemcu-devkit/tree/master/Drivers) and then run the installer.

Select the board type and port as you would any other Arduino and you should now be able to program the ESP8266\. There are, however, a few differences that you should be aware of:

♦ Sometimes (not always) you will need to hold down the Flash button on the board before you power it up, and only release the button a few seconds after the board has been powered up. Do this if your sketch fails to upload.

♦ The named pins D0 to D8 on the board must always be used with the D in front of them, for example, pinMode(D0, OUTPUT). This “D” is optional for the official Arduino boards.

♦ The Mode MCU has a built-in LED like the Arduino Uno’s L LED, but it is on pin D0 rather than pin 13, so you will need to modify your blink sketch to use pin D0.

♦ When using an official Arduino board, it does not matter in which order you define your functions. When using a Node MCU board, you must define functions before the first place where they are called.

The node MCU library is a little different from the standard Arduino Ethernet library. Sketch 10-03 replicates the simple Web server shown in [Figure 10-4](#19_Chapter_10.xhtml_fig-ch10-4) but using a Node MCU and WiFi rather than an Arduino and Ethernet.

```
// sketch 10-03\. Node MCU Basic Web Server

#include <ESP8266WiFi.h>
#include <WiFiClient.h>
#include <ESP8266WebServer.h>
#include <ESP8266mDNS.h>

const char* ssid = "my-network-name";
const char* password = "my_password";

ESP8266WebServer server(80);

void handleRoot()
{
  String message = "<html><body>\n";
  message += "<h1>Arduino Server</h1>\n";
  message += "<p>A0="; 
  message += analogRead(A0); 
  message += "</p>"; 
  message += "<p>millis="; 
  message += millis(); 
  message += "</p>"; 
  message += "</html></body>\n";
  server.send(200, "text/html", message);
}

void connectToWiFi()
{
  Serial.print("\n\nConnecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\nWiFi connected");  
  Serial.print("IP address: ");
  Serial.println(WiFi.localIP());
}

void setup()
{
  Serial.begin(115200);
  connectToWiFi();

  server.on("/", handleRoot);

  server.begin();
  Serial.println("HTTP server started");
}

void loop()
{
  server.handleClient();
}
```

The code for the Node MCU is actually structured quite differently from the code for an Arduino and Ethernet shield that you saw in sketch 10-01\. In this sketch, in place of the MAC address there are constants for the **ssid** (wireless network name) and **password**. Instead of creating a server variable of type **Ethernet**, one of type **ESP8266WebServer** is created.

The **handleRoot** function demonstrates a nice feature of the ESP8266 library. That is, the ability to define handlers for different pages that the server is serving. So if you jump down to the setup function, you will see the command **server.on(“/”, handleRoot)**. This tells the server that whenever there is a request for the root page (/) the function **handleRoot** should be called to generate the necessary HTML for that page and send it back to the browser.

This function uses the Arduino **String** class to construct the HTML a line at a time. Note that the **String** class can be quite memory hungry, so if you start to get unexpected errors in your code, then it may be that the **String** class is to blame. For small string construction like this example, it is fine, but for longer strings it can be better to use a character buffer as shown later in sketch 10-04.

The process of creating the WiFi connection, along with code to display the IP address of the server in the Serial Monitor is all contained in the **connectToWiFi** function. Note that the baud rate for this sketch is set to 115200 so you will need to set the rate to the same on the drop-down list in the right-hand bottom corner of the Serial Monitor to be able to see the messages.

The **setup** function just calls **connectToWiFi**, links up the root handler and starts the server running. The loop function just calls **handleClient** on the server, which waits for incoming requests and then services them.

* * *

### Web-Controlled Node MCU

The Web-controlled Arduino of sketch 10-02 can be adapted to work using a Node MCU. The resulting sketch is sketch 10-04\. To test the sketch, you will need to attach LEDs to the pins used, or measure their voltage using a multimeter.

```
// sketch 10-04 Web Controlled Node MCU

#include <ESP8266WiFi.h>
#include <WiFiClient.h>
#include <ESP8266WebServer.h>
#include <ESP8266mDNS.h>

const char* ssid = "my-network-name";
const char* password = "my_password";

int numPins = 5;
char* pinNames[] = {"D5", "D6", "D7", "D8", "D9"};
int pins[] = {D5, D6, D7, D8, D9};
int pinState[] = {0, 0, 0, 0, 0};

ESP8266WebServer server(80);

void setPinStates()
{
  for (int i = 0; i < numPins; i++)
  {
     digitalWrite(pins[i], pinState[i]);
  }
}

void setValuesFromParams()
{
  for (int i = 0; i < numPins; i++)
  {
    pinState[i] = server.arg(i).toInt();
  }
}

void connectToWiFi()
{
  Serial.print("\n\nConnecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\nWiFi connected");  
  Serial.print("IP address: ");
  Serial.println(WiFi.localIP());
}

void handleRoot()
{
  char buff[1000];
  Serial.println("Got a Request");
  setValuesFromParams();
  setPinStates();

  strcat(buff, "<html><body>\n");
  strcat(buff, "<h1>Output Pins</h1>\n");
  strcat(buff, "<form method='GET'>\n"); 
  for (int i = 0; i < numPins; i++)
  {
    strcat(buff, "<p>");
    strcat(buff, pinNames[i]);
    strcat(buff, " <select name='");
    char indexStr[10];
    sprintf(indexStr, "%d", i);
    strcat(buff, indexStr);
    strcat(buff, "'><option value='0'");
    if (pinState[i] == 0)
    {
      strcat(buff, " selected");
    }
    strcat(buff, ">Off</option>");
    strcat(buff, "<option value='1'");
    if (pinState[i] == 1)
    {
      strcat(buff, " selected");
    }
    strcat(buff, ">On</option></select></p>\n");
  }
  strcat(buff, "<input type='submit' value='Update'/>");
  strcat(buff, "</form></html></body>\n");
  server.send(200, "text/html", buff);
}

void setup()
{
  for (int i = 0; i < numPins; i++)
  {
     pinMode(pins[i], OUTPUT);
  }
  Serial.begin(115200);
  connectToWiFi();
  server.on("/", handleRoot);

  server.begin();
  Serial.println("HTTP server started");
}

void loop()
{
  server.handleClient();
}
```

This sketch is structured in much the same way as its Arduino counterpart (sketch 10-02). However, it uses a different set of pins and also has an array of strings holding the names of those pins for use in the generated webpage. The utility functions **pageNameIs** and **valueOfParam**, which were written to check the page being accessed and split parameters out of the request, are not needed in the ESP8266 version as the library handles requests by page name using the **server.on** mechanism and allows direct access to parameter values using **server.arg(i)** where **i** is the index position of the parameter. The **arg** function actually has options to retrieve named parameters too. You can find out more about this in the documentation that you can find here: [http://links2004.github.io/Arduino/d3/d58/class_e_s_p8266_web_server.html](http://links2004.github.io/Arduino/d3/d58/class_e_s_p8266_web_server.html)

In this case, the **handleRoot** function has to construct a much bigger string to contain the HTML to be sent back to the client. Rather than use the **String** class, this illustrates a different approach that uses a string buffer (**buff**) that uses the **strcat** C function to concatenate a series of small strings to an ever-increasing main string (terminated with a \0). This works okay until you get to adding a number such as the pin value. Then a second string buffer (**indexStr**) is used. The number is then written into this buffer using the **sprintf** C function that “prints” the number into the buffer that is then concatenated into **buff**.

All this buffer writing is unnecessary in the Arduino Ethernet library as that allows writing of the response to the browser a line at a time, which removes the need to construct the whole message before sending it back to the browser.

* * *

### Calling Web Services

All the examples so far in this chapter have used the Arduino or Node MCU as a Web server, but what if you want the board to act more like a Web browser and send requests to a Web server somewhere else on the Internet?

For example, you could have your board take temperature readings at regular intervals and then post those readings to a Web service. In the next two sections you will learn how to use both a regular Arduino and a Node MCU to send requests to the popular IFTTT (If This Then That) Web service. When the service receives the request (its trigger) it will perform an action that, in this case, will be to send you an e-mail that contains the reading from pin A0.

Whether you are using an Arduino or a Node MCU, you will first need to create for yourself an account on [ifttt.com](http://ifttt.com) and then create a new “recipe”. IFTTT has a very easy to use Web interface that is for the most part self-explanatory. So after clicking the button to create a new recipe, click on the “this” hyperlink in the heading “if this then that”. You will then be prompted for a trigger channel. Type **maker** into the search box to find the Maker channel (the logo looks like a colorful letter *M*). Select the Maker channel and then “Receive a web request” as the trigger. You will then need to supply an event name ([Figure 10-8](#19_Chapter_10.xhtml_fig-ch10-8)).

![image](images/fig-ch10-8.jpg)

Figure 10.8 *Completing the trigger fields*.

Enter the text **arduino_spoke** into the Event Name field and then click Create Trigger.

The next step is to define the action. That is, to specify what will happen when the recipe is triggered. For this example we will have IFTTT send us an e-mail, but you could choose a different action channel and have IFTTT send a Tweet, update a Facebook status, or many other possible actions. After you have the basic recipe working, you might like to experiment with other actions. Click on the “that” link in the heading “if this then that” and find the “e-mail” action channel. Select the only action available: “Send me an e-mail.” This will open up the form shown in [Figure 10-9](#19_Chapter_10.xhtml_fig-ch10-9).

![image](images/fig-ch10-9.jpg)

Figure 10.9 *Completing the action fields*.

You can leave the fields as they are and just click Create Action, or you can use the form to customize the e-mail that you will receive. You can always come back and modify the action later. Click the final Create Recipe button and your new recipe will go live waiting for a message from your Arduino or Node MCU.

One final step that you need to take is to fetch the key for your trigger event so that only you can use it. To do this, click on the “Channels” link at the top of the [ifttt.com](http://ifttt.com) home page and search for the Maker channel. You will then see details like the ones shown in [Figure 10-10](#19_Chapter_10.xhtml_fig-ch10-10).

![image](images/fig-ch10-10.jpg)

Figure 10.10 *Finding the Maker channel key*.

The important information here is the text that says “Your key is:”. Later on you will need to paste this key into your sketch.

* * *

### Arduino Uno and IFTTT

Let’s start with the Arduino and Ethernet shield sketch to send messages to IFTTT. This is in sketch 10-05.

```
// sketch 10-05 IFTTT
#include <SPI.h>
#include <Ethernet.h>

// MAC address just has to be unique. This should work
byte mac[] = { 0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED };
const char* key = "c1AsQq_qsQVTSO5-6NASqg";
const char* host = "maker.ifttt.com";
const int httpPort = 80;
const long sendPeriod = 60000L; // 1 minute
EthernetClient client;

void setup()
{
  Serial.begin(9600);
  Ethernet.begin(mac);
}

void sendToIFTTT(int reading)
{
  client.stop(); // for second time around the loop
  Serial.print("connecting to ");
  Serial.println(host);
  if (!client.connect(host, httpPort)) {
    Serial.println("connection failed");
    return;
  }

  String url = "/trigger/arduino_spoke/with/key/";
  url += key;
  url += "?value1=" + String(reading);

  String req = String("GET ") + url + " HTTP/1.1\r\n" +  
               "Host: " + host + "\r\n" +
               "Connection: close\r\n\r\n";
  Serial.println(req);
  client.print(req);
}

void loop() 
{
  static long lastReadingTime = 0;
  long now = millis();
  if (now > lastReadingTime + sendPeriod)
  {
    int reading = analogRead(A0);
    sendToIFTTT(reading);
    lastReadingTime = now;
  }
  if (client.available())
  {
    Serial.write(client.read());
  }
}
```

Change the constant **key** to contain your key from the Maker channel in IFTTT that you found earlier (see [Figure 10-10](#19_Chapter_10.xhtml_fig-ch10-10)). The **sendPeriod** constant sets the time between successive sends of Web requests to IFTTT.

The variable **client** refers to the **EthernetClient** class rather than the **EthernetServer** class that we used in previous examples because the Arduino is acting as a Web client in this example.

The loop function calls the function **sendToIFTTT** every minute, passing the value read from A0 as a parameter. **loop** then checks to see if there is any response from the server and if there is, it displays it. This isn’t strictly necessary but does give valuable feedback in the Serial Monitor so that you know if anything is going wrong.

The **sendToIFTTT** function first calls **client.stop()** to end any previous transaction before connecting to the host server and constructing a **String url** to send to the server that includes the **reading** parameter as one of the request parameters. The URL also includes the **key** and the **arduino_spoke** event name that you specified on IFTTT.

* * *

### Node MCU ESP8266 Board and IFTTT

The node MCU variant for sending triggers to IFTTT is listed in sketch 10-06.

```
// sketch 10_06

#include <ESP8266WiFi.h>

const char* ssid = "my-network-name";
const char* password = "my_password";
const char* key = "c1AsQq_qsQVTSO5-6NASqg";
const char* host = "maker.ifttt.com";
const int httpPort = 80;
const long sendPeriod = 10000L; // 1 minute

WiFiClient client;

void connectToWiFi()
{
  Serial.print("\n\nConnecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\nWiFi connected");  
  Serial.print("IP address: ");
  Serial.println(WiFi.localIP());
}

void sendToIFTTT(int reading)
{
  Serial.print("connecting to ");
  Serial.println(host);

  if (!client.connect(host, httpPort)) {
    Serial.println("connection failed");
    return;
  }

  String url = "/trigger/arduino_spoke/with/key/";
  url += key;
  url += "?value1=" + String(reading);

  String req = String("GET ") + url + " HTTP/1.1\r\n" +  
               "Host: " + host + "\r\n" +
               "Connection: close\r\n\r\n";
  Serial.println(req);
  client.print(req);
}

void setup() 
{
  Serial.begin(115200);
  connectToWiFi();
}

void loop() 
{
  static long lastReadingTime = 0;
  long now = millis();
  if (now > lastReadingTime + sendPeriod)
  {
    int reading = analogRead(A0);
    sendToIFTTT(reading);
    lastReadingTime = now;
  }
  if (client.available())
  {
    Serial.write(client.read());
  }
}
```

Aside from the code to connect to WiFi rather than to Ethernet and the use of the **WiFiClient** class rather than **EthernetClient**, the code is almost identical.

* * *

### Other IoT Options

The Arduino Yun and Particle Photon ([Figure 10-11](#19_Chapter_10.xhtml_fig-ch10-11)) offer alternative platforms for making Internet of Things projects.

![image](images/fig-ch10-11.jpg)

Figure 10.11 *The Arduino Yun (left) and Particle Photon (right)*.

#### Arduino Yun

The Arduino Yun is the official Arduino approach to an IoT board. It’s a very full-featured board that includes both a separate WiFi module and wired Ethernet and USB host sockets. Effectively, it’s a bit like an Arduino Uno combined with an ESP8266-style WiFi module. Communication between the Arduino and WiFi module sides of the board is accomplished using software called “bridge.”

The first step when using a Yun is to connect it to your WiFi network. After you have done this you can program it using the Arduino IDE without having a physical wire connecting it to the computer doing the programming. The board can then be programmed over the WiFi connection.

The board also has USB host, but all these features come at a cost, making the board prohibitively expensive for many IoT projects, especially when put next to an ESP8266-based board.

#### Particle Photon

The Photon and its predecessor the Spark Core are a third-party Arduino-like platform for the IoT. It is WiFi only and also allows over-the-air programming using a Web-based IDE that is not actually the Arduino IDE, but looks rather like it.

The Photon is programmed in Arduino C with some extensions that link it seamlessly into Particle.io’s IoT framework, removing a lot of the potentially tricky network programming that you have seen in this chapter.

The Photon is a little more expensive than ESP8266-based boards but its built-in IoT framework and over-the-air programming capabilities make it a good choice for WiFi IoT projects.

If you want to learn more about the Photon, then you might like to look at my book *Getting Started with the Photon* (Maker Media, 2015).

* * *

### Conclusion

Having used shields and associated libraries in the last two chapters, it is now time to investigate the features that enable libraries to be written and learn how to write libraries of your own.

## 11

## C++ and Libraries

Arduinos are simple microcontrollers. Most of the time, Arduino sketches are quite small, so using the C programming language works just fine. However, the programming language for Arduino is actually C++ rather than C. C++ is an extension to the C programming language that adds something called *object orientation.*

* * *

### Object Orientation

This is only a short book, so an in-depth explanation of the C++ programming language is beyond its scope. The book can, however, cover the basics of C++ and object orientation. But the main goal is to increase the *encapsulation* of your programs. Encapsulation keeps relevant things together, something that makes C++ very suitable for writing libraries such as those that you have used for the Ethernet and LCD sketches in earlier chapters.

There are many good books on the topics of C++ and object-oriented programming. Look for the higher-rated books on the topic in your favorite online bookstore.

#### Classes and Methods

Object orientation uses a concept called *classes* to aid encapsulation. Generally, a class is like a section of a program that includes both variables—called *member variables*—and *methods*, which are like functions but apply to the class. These functions can either be *public*, in which case the methods and functions may be used by other classes, or *private*, in which case the methods can be called only by other methods within the same class.

Whereas an Arduino sketch is contained in a single file, when you are working in C++, you tend to use more than one file. In fact, there are generally two files for every class: A *header file*, which has the extension .h, and the *implementation file*, which has the extension .cpp.

* * *

### Built-In Library Example

The LCD library has been used in the two previous chapters, so let’s look more closely and see what is going on in a little more detail.

Referring back to sketch 9-01 (open this in your Arduino IDE), you can see that the **include** command includes the file LiquidCrystal.h:

```
#include <LiquidCrystal.h>
```

This file is the header file for the class called **LiquidCrystal**. This file tells the Arduino sketch what it needs to know to be able to use the library. You can actually retrieve this file if you go to your Arduino installation folder and file and find the file libraries/LiquidCrystal. You will need to open the file in a text editor. If you are using a Mac, then right-click on the Arduino app itself and select the menu option Show Package Contents. Then navigate to Contents/Resources/Java/libraries/LiquidCrystal.

The file LiquidCrystal.h contains lots of code, as this is a fairly large library class. The code for the actual class itself, where the nuts and bolts of displaying a message actually reside, is in the file LiquidCrystal.cpp.

In the next section, a simple example library will be created that should put the concepts behind a library into context.

* * *

### Writing Libraries

Creating an Arduino library might seem like the kind of thing that only a seasoned Arduino veteran should attempt, but actually it is pretty straightforward to make a library. For example, you can convert into a library the **flash** function from [Chapter 4](#13_Chapter_04.xhtml) that causes an LED to flash for a specified number of times.

To create the C++ files that are needed to do this, you will need a text editor for your computer—something like TextPad on Windows or TextMate on Mac.

#### The Header File

Start by creating a folder to contain all the library files. You should create this folder inside the libraries folder of your Arduino documents folder. In Windows, your libraries folder will be in My Documents\Arduino. On the Mac, you will find it in your home directory, Documents/Arduino/, and on Linux, it will be in the sketchbook directory of your home directory. If there is no libraries folder in your Arduino, then create one.

This libraries folder is where any libraries you write yourself, or any “unofficial” contributed libraries, must be installed.

Call the folder ‘Flasher’. Start the text editor and type the following into it:

```
// LED Flashing library

#include "Arduino.h"

class Flasher
{
  public:
    Flasher(int pin, int duration);
    void flash(int times);
  private:
    int _pin;
    int _d;
};
```

Save this file in the Flasher folder with the name Flasher.h. This is the header file for the library class. This file specifies the different parts of the class. As you can see, it is divided into public and private parts.

The public part contains what looks like the start of two functions. These are called methods and differ from functions only insofar as they are associated with a class. They can be used only as part of the class. Unlike functions, they cannot be used on their own.

The first method, **Flasher**, begins with an uppercase letter, which is something you would not use with a function name. It also has the same name as the class. This method is called a *constructor*, which you can apply to create a new **Flasher** object to use in a sketch.

For example, you could put the following in a sketch:

```
Flasher slowFlasher(13, 500);
```

This would create a new **Flasher** called **slowFlasher** that would flash on pin D13 with a duration of 500 milliseconds.

The second method in the class is called **flash**. This method takes a single argument of the number of times to flash. Because it is associated with a class, when you want to call it, you have to refer to the object that you created earlier, as follows:

```
slowFlasher.flash(10);
```

This would cause the LED to flash ten times at the period that you specified in the constructor to the **Flasher** object.

The private section of the class contains two variable definitions: one for the pin, and one for the duration, which is simply called **d**. Every time that you create an object of class **Flasher**, it will have these two variables. This enables it to remember the pin and duration when a new **Flasher** object is created.

These variables are called member variables because they are members of the class. Their names generally are unusual in that they start with an underscore character; however, this is just a common convention, not a programming necessity. Another commonly used naming convention is to use a lowercase *m* (for *member*) as the first letter of the variable name.

#### The Implementation File

The header file has just defined what the class looks like. You now need a separate file that actually does the work. This is called the implementation file and has the extension .cpp.

So, create a new file containing the following and save it as Flasher.cpp in the Flasher folder:

```
#include "Flasher.h"

Flasher::Flasher(int pin, int duration)
{
  pinMode(pin, OUTPUT);
  _pin = pin;
  _d = duration / 2;
}

void Flasher::flash(int times)
{
  for (int i = 0; i < times; i++)
  {
    digitalWrite(_pin, HIGH);
    delay(_d);
    digitalWrite(_pin, LOW);
    delay(_d);
  }  
}
```

There is some unfamiliar syntax in this file. The method names are both prefixed by **Flasher::**. This indicates that the methods belong to the **Flasher** class.

The constructor method (**Flasher**) just assigns each of its parameters to the appropriate private member variable. The **duration** parameter is divided by two before being assigned to the member variable **_d**. This is because the delay is called twice, and it seems more logical for the duration to be the total duration of the flash and the gap between flashes.

The **flash** function actually carries out the business of flashing; it loops for the appropriate number of times, turning the LED on and off for the appropriate delay.

#### Completing Your Library

You have now seen all of the essentials for completing the library. You could now deploy this library and it would work just fine. However, there are two further steps that you should take to complete your library. One is to define the keywords used in the library so that the Arduino IDE can show them in the appropriate color when users are editing code. The other is to include some examples of how to use the library.

##### *Keywords*

To define the keywords, you have to create a file called keywords.txt, which goes into the Flasher directory. This file contains just the two following lines:

```
Flasher   KEYWORD1
flash     KEYWORD2
```

This is essentially a two-column table in a text file. The left column is the keyword and the right column an indication of the type of keyword it is. Class names should be a **KEYWORD1** and methods should be **KEYWORD2**. It does not matter how many spaces or tabs you put between the columns, but each keyword should start on a new line.

##### *Examples*

The other thing that you, as a good Arduino citizen, should include as part of the library is a folder of examples. In this case, the library is so simple that a single example will suffice.

The examples must all be placed in a folder called examples inside the Flasher folder. The example is in fact just an Arduino sketch, so you can create the example using the Arduino IDE. But first, you have to quit and then reopen the Arduino IDE to make it aware of the new library.

After restarting the Arduino IDE, from the Arduino IDE’s menu, select File and then New to create a new sketch window. Then from the menu, select Sketch and the Include Library option. The options should look something like [Figure 11-1](#20_Chapter_11.xhtml_fig-ch11-1).

![image](images/fig-ch11-1.jpg)

Figure 11.1 *Importing the Flasher library*.

The libraries above the line in the submenu are the official libraries; below this line are the “unofficial” contributed libraries. If all has gone well, you should see Flasher in the list.

If Flasher is not in the list, it is very likely that the Flasher folder is not in the libraries folder of your sketches folder, so go back and check.

Type the following into the sketch window that has just been created:

```
#include <Flasher.h>

const int ledPin = 13;
const int slowDuration = 300;
const int fastDuration = 100;

Flasher slowFlasher(ledPin, slowDuration);
Flasher fastFlasher(ledPin, fastDuration);

void setup(){}

void loop()
{
   slowFlasher.flash(5);
   delay(1000);
   fastFlasher.flash(10);
   delay(2000);
}
```

The Arduino IDE will not allow you to save the example sketch directly into the libraries folder, so save it somewhere else under the name Simple_Flasher_Example and then move the whole Simple_Flasher_Example folder that you just saved into the ‘examples’ folder in your library.

If you restart your Arduino IDE, you should now see that you are able to open the example sketch from the menu as shown in [Figure 11-2](#20_Chapter_11.xhtml_fig-ch11-2).

![image](images/fig-ch11-2.jpg)

Figure 11.2 *Opening the example sketch*.

* * *

### Conclusion

There is more to C++ and to writing libraries, but this chapter should get you started. It should also be sufficient for most of what you are likely to do with an Arduino. These Arduinos are small devices and the temptation is often to over-engineer solutions that could otherwise be very simple and straightforward.

That concludes the main body of this book. For further information on Arduino and where to go next, a good starting point is always the official Arduino website at [www.arduino.cc](http://www.arduino.cc). Also, please refer to this book’s website at [www.arduinobook.com](http://www.arduinobook.com), where you will find errata and other useful resources.

If you are looking for help or advice, the Arduino community on [www.arduino.com/forum](http://www.arduino.com/forum) is extremely helpful. You will also find the author on there with the username Si.

## INDEX

### Symbols

>= (greater than or equal to), comparison operators, [43](#12_Chapter_03.xhtml_page43)

<= (less than or equal to), comparison operators, [43](#12_Chapter_03.xhtml_page43)

− (minus), as arithmetic operator, [41](#12_Chapter_03.xhtml_page41)

!= (not equal to), comparison operators, [43](#12_Chapter_03.xhtml_page43)

/*.*/, coding style for comments, [61](#13_Chapter_04.xhtml_page61)

/ (slash), as division operator, [41](#12_Chapter_03.xhtml_page41)

// (slashes), coding style for comments, [61](#13_Chapter_04.xhtml_page61)

|| (`or` operator), use of booleans in truth tables, [57–58](#13_Chapter_04.xhtml_page57)

+ (plus), as arithmetic operator, [41](#12_Chapter_03.xhtml_page41)

= (assignment operator), using numeric variables in C, [39](#12_Chapter_03.xhtml_page39)

== (equal to), comparison operators, [43](#12_Chapter_03.xhtml_page43)

! (`not` operator), use of booleans in truth tables, [58](#13_Chapter_04.xhtml_page58)

&& (`and` operator), use of booleans in truth tables, [57–58](#13_Chapter_04.xhtml_page57)

* (asterisk), as multiplication operator, [41](#12_Chapter_03.xhtml_page41)

{} (curly braces)

in function syntax, [33](#12_Chapter_03.xhtml_page33)

opening braces in C language coding style, [60](#13_Chapter_04.xhtml_page60)

< (less than), comparison operators, [43](#12_Chapter_03.xhtml_page43)

> (greater than), comparison operators, [43](#12_Chapter_03.xhtml_page43)

### A

`abs` function, in Arduino library, [100](#16_Chapter_07.xhtml_page100)

Adafruit

connecting to OLED display, [125](#18_Chapter_09.xhtml_page125)

display libraries, [126–128](#18_Chapter_09.xhtml_page126)

Adafruit Trinket, Arduino clones/variants, [13](#10_Chapter_01.xhtml_page13)

Advanced I/O

feeding shift registers, [104](#16_Chapter_07.xhtml_page104)

in standard Arduino library, [102](#16_Chapter_07.xhtml_page102)

tone generation, [102–103](#16_Chapter_07.xhtml_page102)

*Algorithms + Data Structures = Programs* (Wirth), [63](#14_Chapter_05.xhtml_page63)

Alphanumeric LCDs, [120](#18_Chapter_09.xhtml_page120)

Analog inputs

in Arduino microcontroller, [2](#10_Chapter_01.xhtml_page2), [4](#10_Chapter_01.xhtml_page4)

overview of, [94–96](#15_Chapter_06.xhtml_page94)

Analog outputs

in Arduino microcontroller, [2](#10_Chapter_01.xhtml_page2)

using PWM to control brightness of LEDs, [92–94](#15_Chapter_06.xhtml_page92)

`analogRead` function, [94](#15_Chapter_06.xhtml_page94)

`and` operator (&&), use of booleans in truth tables, [57–58](#13_Chapter_04.xhtml_page57)

Antenna, digital input with human antenna, [84](#15_Chapter_06.xhtml_page84)

Applications. *See* Sketches

Arduino family

Arduino Lilypad, [11](#10_Chapter_01.xhtml_page11)

Arduino Mega and Due, [9](#10_Chapter_01.xhtml_page9)

Arduino Micro and small boards, [10](#10_Chapter_01.xhtml_page10)

Arduino Uno and Leonardo, [8](#10_Chapter_01.xhtml_page8)

Arduino Yun, [10–11](#10_Chapter_01.xhtml_page10)

clones/variants, [12–13](#10_Chapter_01.xhtml_page12)

overview of, [8](#10_Chapter_01.xhtml_page8)

Arduino history, [6–7](#10_Chapter_01.xhtml_page6)

Arduino Uno

28-pin chip on, [5](#10_Chapter_01.xhtml_page5)

Arduino family, [8](#10_Chapter_01.xhtml_page8)

as development board, [2–3](#10_Chapter_01.xhtml_page2)

microcontroller on, [2](#10_Chapter_01.xhtml_page2)

sending messages to IFTTT, [151–153](#19_Chapter_10.xhtml_page151)

as Web servers, [132–135](#19_Chapter_10.xhtml_page132)

Arduino Yun

in Arduino family, [10–11](#10_Chapter_01.xhtml_page10)

IoT (Internet of Things) programming, [155](#19_Chapter_10.xhtml_page155)

Arguments

C language, [28](#12_Chapter_03.xhtml_page28)

interrupts, [105–106](#16_Chapter_07.xhtml_page105)

for loops, [45](#12_Chapter_03.xhtml_page45)

`tone` function, [103](#16_Chapter_07.xhtml_page103)

Arithmetic functions

C language, [39–41](#12_Chapter_03.xhtml_page39)

math functions in Arduino library, [100](#16_Chapter_07.xhtml_page100)

performing arithmetic in Arduino, [37](#12_Chapter_03.xhtml_page37)

Arrays

data structure for Morse code translator, [70–71](#14_Chapter_05.xhtml_page70)

`flashDotOrDash` function for Morse code translator, [75–76](#14_Chapter_05.xhtml_page75)

`flashSequence` function for Morse code translator, [75](#14_Chapter_05.xhtml_page75)

globals and setup for Morse code translator, [70–71](#14_Chapter_05.xhtml_page70)

`loop` function for Morse code translator, [72–74](#14_Chapter_05.xhtml_page72)

Morse code SOS example, [66–67](#14_Chapter_05.xhtml_page66)

Morse code translator, [69–70](#14_Chapter_05.xhtml_page69)

Morse code translator listing, [76–78](#14_Chapter_05.xhtml_page76)

overview of, [63–66](#14_Chapter_05.xhtml_page63)

string arrays, [67](#14_Chapter_05.xhtml_page67)

ASCII character codes, [68](#14_Chapter_05.xhtml_page68)

Assignment operator (=), using numeric variables in C, [39](#12_Chapter_03.xhtml_page39)

Asterisk (*), as multiplication operator, [41](#12_Chapter_03.xhtml_page41)

ATMega328 microcontroller

in Arduino Mega, [9](#10_Chapter_01.xhtml_page9)

in Arduino Uno, [3](#10_Chapter_01.xhtml_page3)

EEPROM and, [110](#17_Chapter_08.xhtml_page110)

Atmel, manufacturer of microcontrollers, [2–3](#10_Chapter_01.xhtml_page2)

AVR EEPROM library

overview of, [112–113](#17_Chapter_08.xhtml_page112)

storing floats in EEPROM, [113](#17_Chapter_08.xhtml_page113)

storing strings in EEPROM, [113–115](#17_Chapter_08.xhtml_page113)

### B

Banzi, Massimo, [6](#10_Chapter_01.xhtml_page6)

Binary

bit manipulation, [100–102](#16_Chapter_07.xhtml_page100)

comparing with hex and decimal, [101–102](#16_Chapter_07.xhtml_page101)

machine code compiled as, [30–31](#12_Chapter_03.xhtml_page30)

Bit manipulation, in standard Arduino library, [100–102](#16_Chapter_07.xhtml_page100)

Blink sketch

changing blink rate, [20–22](#11_Chapter_02.xhtml_page20)

saving, [23](#11_Chapter_02.xhtml_page23)

uploading first sketch, [17–20](#11_Chapter_02.xhtml_page17)

Boards

development boards, [2–3](#10_Chapter_01.xhtml_page2)

selecting board type, [18](#11_Chapter_02.xhtml_page18)

shield boards, [7](#10_Chapter_01.xhtml_page7)

tour of Arduino board, [3](#10_Chapter_01.xhtml_page3)

Boole, George, [57](#13_Chapter_04.xhtml_page57)

Booleans

data types in C, [58](#13_Chapter_04.xhtml_page58)

types of variables, [57–58](#13_Chapter_04.xhtml_page57)

Bounce library, installing/using, [91–92](#15_Chapter_06.xhtml_page91)

Buttons, debouncing, [87–88](#15_Chapter_06.xhtml_page87)

Bytes, separating int into two bytes, [111](#17_Chapter_08.xhtml_page111)

### C

C language

applying `setup` and `loop` functions to Blink sketch, [34–35](#12_Chapter_03.xhtml_page34)

for command, [43–46](#12_Chapter_03.xhtml_page43)

commands, [41–43](#12_Chapter_03.xhtml_page41)

constants, [47](#12_Chapter_03.xhtml_page47)

data types, [58–59](#13_Chapter_04.xhtml_page58)

defining variables, [36–37](#12_Chapter_03.xhtml_page36)

extending with functions from standard Arduino library, [97](#16_Chapter_07.xhtml_page97)

numeric variables and arithmetic functions, [39–41](#12_Chapter_03.xhtml_page39)

overview of, [27](#12_Chapter_03.xhtml_page27)

programming in, [27–29](#12_Chapter_03.xhtml_page27)

testing experiments, [37–39](#12_Chapter_03.xhtml_page37)

while command, [46–47](#12_Chapter_03.xhtml_page46)

C++ language

built-in and written libraries, [158](#20_Chapter_11.xhtml_page158)

classes and methods, [157–158](#20_Chapter_11.xhtml_page157)

defining keywords for new library, [161–162](#20_Chapter_11.xhtml_page161)

header file for written library, [159–160](#20_Chapter_11.xhtml_page159)

implementation file for written library, [160–161](#20_Chapter_11.xhtml_page160)

including examples in newly written library, [162–164](#20_Chapter_11.xhtml_page162)

object orientation, [157](#20_Chapter_11.xhtml_page157)

overview of, [157](#20_Chapter_11.xhtml_page157)

Calling functions, [28](#12_Chapter_03.xhtml_page28)

Central processing unit (CPU), at heart of Arduino chip, [6](#10_Chapter_01.xhtml_page6)

`char` data type

ASCII codes, [68](#14_Chapter_05.xhtml_page68)

in C, [58](#13_Chapter_04.xhtml_page58)

data structure for Morse code translator, [71](#14_Chapter_05.xhtml_page71)

Chip, in Arduino controller, [5–6](#10_Chapter_01.xhtml_page5)

Classes

C++ implementation and, [161](#20_Chapter_11.xhtml_page161)

C++ keywords and, [162](#20_Chapter_11.xhtml_page162)

in C++ language, [157–158](#20_Chapter_11.xhtml_page157)

methods associated with, [159–160](#20_Chapter_11.xhtml_page159)

Clones/variants, of Arduino family, [12–13](#10_Chapter_01.xhtml_page12)

Coding style, for functions

comments, [61–62](#13_Chapter_04.xhtml_page61)

indentation, [59–60](#13_Chapter_04.xhtml_page59)

opening braces, [60](#13_Chapter_04.xhtml_page60)

overview of, [59](#13_Chapter_04.xhtml_page59)

whitespace, [60–61](#13_Chapter_04.xhtml_page60)

COM port, selecting serial port on Windows computers, [19](#11_Chapter_02.xhtml_page19)

Commands, C language. *See also* Functions

for, [43–46](#12_Chapter_03.xhtml_page43)

if, [41–43](#12_Chapter_03.xhtml_page41)

overview of, [41](#12_Chapter_03.xhtml_page41)

sending to displays, [123](#18_Chapter_09.xhtml_page123)

while, [46–47](#12_Chapter_03.xhtml_page46)

Comments, coding style for, [61–62](#13_Chapter_04.xhtml_page61)

Comparison operators, [43](#12_Chapter_03.xhtml_page43)

Compilation, into machine code, [30–31](#12_Chapter_03.xhtml_page30)

Conditions

for command, [45](#12_Chapter_03.xhtml_page45)

if command, [42](#12_Chapter_03.xhtml_page42)

Connections, digital, [5](#10_Chapter_01.xhtml_page5)

Constants

in C language, [47](#12_Chapter_03.xhtml_page47)

storing, [107](#17_Chapter_08.xhtml_page107)

string literals as, [67](#14_Chapter_05.xhtml_page67)

using const keyword with arrays, [65](#14_Chapter_05.xhtml_page65)

Constrain function, math functions in Arduino library, [100](#16_Chapter_07.xhtml_page100)

Constructor method

in C++ header, [159](#20_Chapter_11.xhtml_page159)

in C++ implementation, [161](#20_Chapter_11.xhtml_page161)

`cos` function, math functions in Arduino library, [100](#16_Chapter_07.xhtml_page100)

CPU (central processing unit), at heart of Arduino chip, [6](#10_Chapter_01.xhtml_page6)

Creative Common license, Arduino available under, [7](#10_Chapter_01.xhtml_page7)

Cuartielles, David, [6](#10_Chapter_01.xhtml_page6)

Curly braces ({})

in function syntax, [33](#12_Chapter_03.xhtml_page33)

opening braces in C language coding style, [60](#13_Chapter_04.xhtml_page60)

### D

Data storage

clearing EEPROM contents, [115–116](#17_Chapter_08.xhtml_page115)

compression and, [116–117](#17_Chapter_08.xhtml_page116)

constants, [107](#17_Chapter_08.xhtml_page107)

EEPROM and, [110–111](#17_Chapter_08.xhtml_page110)

in flash memory, [108–110](#17_Chapter_08.xhtml_page108)

storing floats in EEPROM, [113](#17_Chapter_08.xhtml_page113)

storing int in EEPROM, [111–112](#17_Chapter_08.xhtml_page111)

storing strings in EEPROM, [113–115](#17_Chapter_08.xhtml_page113)

using AVR EEPROM library, [112–113](#17_Chapter_08.xhtml_page112)

Data structure, for Morse code translator, [70–71](#14_Chapter_05.xhtml_page70)

Data types, in C, [58–59](#13_Chapter_04.xhtml_page58)

Debouncing, in digital input, [87–92](#15_Chapter_06.xhtml_page87)

Decimals, comparing with binary and hex, [101–102](#16_Chapter_07.xhtml_page101)

`delay` function

applying `setup` and `loop` functions to Blink sketch, [35](#12_Chapter_03.xhtml_page35)

as built in function, [32](#12_Chapter_03.xhtml_page32), [49](#13_Chapter_04.xhtml_page49)

Development boards, [2–3](#10_Chapter_01.xhtml_page2). *See also* Microcontroller, Arduino

DFRobot LCD Keypad Shield, [120](#18_Chapter_09.xhtml_page120)

Digital connections, in Arduino microcontroller, [5](#10_Chapter_01.xhtml_page5)

Digital inputs

in Arduino microcontroller, [2](#10_Chapter_01.xhtml_page2)

debouncing, [87–92](#15_Chapter_06.xhtml_page87)

internal pull-up resistors in digital input, [86–87](#15_Chapter_06.xhtml_page86)

overview of, [83](#15_Chapter_06.xhtml_page83)

pull-up resistors in, [83–86](#15_Chapter_06.xhtml_page83)

Digital outputs

in Arduino microcontroller, [2](#10_Chapter_01.xhtml_page2)

overview of, [79–82](#15_Chapter_06.xhtml_page79)

`digitalWrite` function

arguments, [28](#12_Chapter_03.xhtml_page28)

predefined functions, [32](#12_Chapter_03.xhtml_page32), [34](#12_Chapter_03.xhtml_page34)

DIL (dual in-line) socket, for microcontroller chip, [5](#10_Chapter_01.xhtml_page5)

Displays

alphanumeric LCDs, [120](#18_Chapter_09.xhtml_page120)

connecting OLED display, [125–126](#18_Chapter_09.xhtml_page125)

LCD library functions, [124](#18_Chapter_09.xhtml_page124)

OLED (organic light-emitting diode), [124–125](#18_Chapter_09.xhtml_page124)

overview of, [119](#18_Chapter_09.xhtml_page119)

sending commands to, [123](#18_Chapter_09.xhtml_page123)

software for, [126–128](#18_Chapter_09.xhtml_page126)

USB message board, [121–123](#18_Chapter_09.xhtml_page121)

Division operator, [41](#12_Chapter_03.xhtml_page41)

`double` data type, in C, [58](#13_Chapter_04.xhtml_page58)

Dual in-line (DIL) socket, for microcontroller chip, [5](#10_Chapter_01.xhtml_page5)

Durations, example of use of arrays, [66–67](#14_Chapter_05.xhtml_page66)

### E

EEPROM (electrically erasable read-only memory)

clearing contents, [115–116](#17_Chapter_08.xhtml_page115)

compression and, [116–117](#17_Chapter_08.xhtml_page116)

overview of, [110–111](#17_Chapter_08.xhtml_page110)

storing floats in, [113](#17_Chapter_08.xhtml_page113)

storing int in, [111–112](#17_Chapter_08.xhtml_page111)

storing strings in, [113–115](#17_Chapter_08.xhtml_page113)

using AVR EEPROM library, [112–113](#17_Chapter_08.xhtml_page112)

Encapsulation

benefits of C++, [157](#20_Chapter_11.xhtml_page157)

global variables and, [53](#13_Chapter_04.xhtml_page53)

EPROM (erasable programmable memory)

components of microcontrollers, [1](#10_Chapter_01.xhtml_page1)

data storage in flash memory, [108–110](#17_Chapter_08.xhtml_page108)

how Arduino chip works, [6](#10_Chapter_01.xhtml_page6)

Equal to (==), comparison operators, [43](#12_Chapter_03.xhtml_page43)

ESP8266 WiFi System on a Chip

IFTTT and, [153–155](#19_Chapter_10.xhtml_page153)

Node MCU Web server, [140–145](#19_Chapter_10.xhtml_page140)

Ethernet shield

types of shield boards, [7](#10_Chapter_01.xhtml_page7)

using Arduino as Ethernet shield, [129](#19_Chapter_10.xhtml_page129), [132–135](#19_Chapter_10.xhtml_page132)

Web-controlled Arduino, [135–140](#19_Chapter_10.xhtml_page135)

Examples, including in new C++ library, [162–164](#20_Chapter_11.xhtml_page162)

### F

File menu

opening Blink sketch, [17](#11_Chapter_02.xhtml_page17)

options for working with Arduino applications, [22–23](#11_Chapter_02.xhtml_page22)

Flash memory. *See* EPROM (erasable programmable memory)

`flashDotOrDash` function, for Morse code translator, [75–76](#14_Chapter_05.xhtml_page75)

`flashSequence` function, for Morse code translator, [75](#14_Chapter_05.xhtml_page75)

`float`

data types in C, [58](#13_Chapter_04.xhtml_page58)

range compression, [116–117](#17_Chapter_08.xhtml_page116)

storing in EEPROM, [113](#17_Chapter_08.xhtml_page113)

types of variables, [56](#13_Chapter_04.xhtml_page56)

`for` command, C language, [43–46](#12_Chapter_03.xhtml_page43)

Freetronics EtherTen, Arduino clones/variants, [13](#10_Chapter_01.xhtml_page13)

Functions

applying `setup` and `loop` functions to Blink sketch, [34–35](#12_Chapter_03.xhtml_page34)

boolean, [57–58](#13_Chapter_04.xhtml_page57)

C language, [58–59](#13_Chapter_04.xhtml_page58)

C++ language, [157–158](#20_Chapter_11.xhtml_page157)

calling, [28](#12_Chapter_03.xhtml_page28)

coding style, [59–61](#13_Chapter_04.xhtml_page59)

comments in C language coding style, [61–62](#13_Chapter_04.xhtml_page61)

defining `setup` and `loop` functions for every sketch, [32–33](#12_Chapter_03.xhtml_page32)

`float`, [56](#13_Chapter_04.xhtml_page56)

global, local, and static variables in, [52–54](#13_Chapter_04.xhtml_page52)

LCD library functions, [124](#18_Chapter_09.xhtml_page124)

`loop`. *See* `loop` function

needed in Arduino “boilerplate” code, [31–32](#12_Chapter_03.xhtml_page31)

overview of, [49](#13_Chapter_04.xhtml_page49)

parameters, [50–51](#13_Chapter_04.xhtml_page50)

return values, [55](#13_Chapter_04.xhtml_page55)

`setup`. *See* `setup` function

syntax, [33](#12_Chapter_03.xhtml_page33)

what they are, [49–50](#13_Chapter_04.xhtml_page49)

working with LCD displays, [121](#18_Chapter_09.xhtml_page121)

### G

Getting started

installing software, [16](#11_Chapter_02.xhtml_page16)

powering up, [15](#11_Chapter_02.xhtml_page15)

uploading first sketch, [17–22](#11_Chapter_02.xhtml_page17)

working with Arduino application, [22–25](#11_Chapter_02.xhtml_page22)

Global variables

in functions, [52–54](#13_Chapter_04.xhtml_page52)

for Morse code translator, [70–71](#14_Chapter_05.xhtml_page70)

Greater than (>), comparison operators, [43](#12_Chapter_03.xhtml_page43)

Greater than or equal to (>=), comparison operators, [43](#12_Chapter_03.xhtml_page43)

### H

*Hacking Electronics* (Monk), [79](#15_Chapter_06.xhtml_page79)

Header file, creating new C++ library, [159–160](#20_Chapter_11.xhtml_page159)

Hexadecimal (hex), comparing with binary and decimal, [101–102](#16_Chapter_07.xhtml_page101)

HTML (Hypertext Markup Language), [131–132](#19_Chapter_10.xhtml_page131)

HTTP (Hypertext Transport Protocol)

communicating with Web servers, [130](#19_Chapter_10.xhtml_page130)

posting data, [135](#19_Chapter_10.xhtml_page135)

### I

I/O (input/output)

advanced I/O in standard Arduino library, [102](#16_Chapter_07.xhtml_page102)

analog inputs, [4](#10_Chapter_01.xhtml_page4), [94–96](#15_Chapter_06.xhtml_page94)

analog outputs, [92–94](#15_Chapter_06.xhtml_page92)

debouncing in digital input, [87–92](#15_Chapter_06.xhtml_page87)

digital and analog, [2](#10_Chapter_01.xhtml_page2)

digital connections for output, [5](#10_Chapter_01.xhtml_page5)

digital inputs, [83](#15_Chapter_06.xhtml_page83)

digital outputs, [79–82](#15_Chapter_06.xhtml_page79)

internal pull-up resistors in digital input, [86–87](#15_Chapter_06.xhtml_page86)

overview of, [79](#15_Chapter_06.xhtml_page79)

pull-up resistors in digital input, [83–86](#15_Chapter_06.xhtml_page83)

I/O (input/output) pins, [1–2](#10_Chapter_01.xhtml_page1)

I2C, serial bus standard, [125](#18_Chapter_09.xhtml_page125)

IDE (integrated development environment)

compilation and, [32](#12_Chapter_03.xhtml_page32)

programming languages and, [29](#12_Chapter_03.xhtml_page29)

`if` command

C language, [41–43](#12_Chapter_03.xhtml_page41)

indentation coding style, [60](#13_Chapter_04.xhtml_page60)

IFTTT (If This Then That)

calling Web services, [148–151](#19_Chapter_10.xhtml_page148)

Node MCU ESP8266 board and, [153–155](#19_Chapter_10.xhtml_page153)

sending messages to Arduino Uno, [151–153](#19_Chapter_10.xhtml_page151)

Implementation file, C++, [160–161](#20_Chapter_11.xhtml_page160)

Indentation, function coding style, [59–60](#13_Chapter_04.xhtml_page59)

Inputs. *See* I/O (input/output)

`int` variables

16-bit size of, [100–101](#16_Chapter_07.xhtml_page100)

data types in C, [58–59](#13_Chapter_04.xhtml_page58)

declaring, [40–41](#12_Chapter_03.xhtml_page40)

defining, [36](#12_Chapter_03.xhtml_page36), [51](#13_Chapter_04.xhtml_page51)

hex representation of, [102](#16_Chapter_07.xhtml_page102)

range compression, [116–117](#17_Chapter_08.xhtml_page116)

return values and, [55](#13_Chapter_04.xhtml_page55)

storing in EEPROM, [111–112](#17_Chapter_08.xhtml_page111)

Integrated development environment (IDE)

compilation and, [32](#12_Chapter_03.xhtml_page32)

programming languages and, [29](#12_Chapter_03.xhtml_page29)

Interrupts, in standard Arduino library, [104–106](#16_Chapter_07.xhtml_page104)

IoT (Internet of Things) programming

Arduino Yun and, [155](#19_Chapter_10.xhtml_page155)

calling Web services, [148–151](#19_Chapter_10.xhtml_page148)

communicating with Web servers, [130](#19_Chapter_10.xhtml_page130)

HTML and, [131–132](#19_Chapter_10.xhtml_page131)

HTTP and, [130](#19_Chapter_10.xhtml_page130)

Node MCU ESP8266 board and IFTTT, [153–155](#19_Chapter_10.xhtml_page153)

Node MCU Web server, [140–145](#19_Chapter_10.xhtml_page140)

overview of, [129–130](#19_Chapter_10.xhtml_page129)

sending messages to IFTTT, [151–153](#19_Chapter_10.xhtml_page151)

using Arduino Uno as Web server, [132–135](#19_Chapter_10.xhtml_page132)

Web-controlled Arduino, [135–140](#19_Chapter_10.xhtml_page135)

Web-controlled Node MCU, [145–148](#19_Chapter_10.xhtml_page145)

IP addresses, finding for Arduino Uno, [132–134](#19_Chapter_10.xhtml_page132)

### K

Keywords, defining for new C++ library, [161–162](#20_Chapter_11.xhtml_page161)

### L

LCDs (liquid crystal displays)

alphanumeric LCDs, [120](#18_Chapter_09.xhtml_page120)

comparing with OLED, [119](#18_Chapter_09.xhtml_page119)

library functions, [124](#18_Chapter_09.xhtml_page124)

USB message board, [121–123](#18_Chapter_09.xhtml_page121)

LED (light-emitting diode)

creating flash function for, [50](#13_Chapter_04.xhtml_page50)

`flashDotOrDash` function for Morse code translator, [75–76](#14_Chapter_05.xhtml_page75)

powering up and, [15](#11_Chapter_02.xhtml_page15)

using PWM to control brightness of, [92–94](#15_Chapter_06.xhtml_page92)

Less than (<), comparison operators, [43](#12_Chapter_03.xhtml_page43)

Less than or equal to (<=), comparison operators, [43](#12_Chapter_03.xhtml_page43)

Libraries. *See also* Standard Arduino library

Adafruit display libraries, [126–128](#18_Chapter_09.xhtml_page126)

AVR EEPROM library, [112–113](#17_Chapter_08.xhtml_page112)

installing/using Bounce library, [91–92](#15_Chapter_06.xhtml_page91)

LCD library functions, [124](#18_Chapter_09.xhtml_page124)

USB message board, [121–123](#18_Chapter_09.xhtml_page121)

Libraries, C++

built-in and written, [158](#20_Chapter_11.xhtml_page158)

defining keywords for new library, [161–162](#20_Chapter_11.xhtml_page161)

header file for written library, [159–160](#20_Chapter_11.xhtml_page159)

implementation file for written library, [160–161](#20_Chapter_11.xhtml_page160)

including examples in newly written library, [162–164](#20_Chapter_11.xhtml_page162)

Licensing, Creative Common license, [7](#10_Chapter_01.xhtml_page7)

Light-emitting diode. *See* LED (light-emitting diode)

Linux computers

installing Arduino software on, [16](#11_Chapter_02.xhtml_page16)

selecting serial port, [19](#11_Chapter_02.xhtml_page19)

Liquid crystal displays. *See* LCDs (liquid crystal displays)

Local variables, in functions, [52–54](#13_Chapter_04.xhtml_page52)

`log` function, math functions in Arduino library, [100](#16_Chapter_07.xhtml_page100)

`long` data type, in C, [58](#13_Chapter_04.xhtml_page58)

`loop` function

adding display software, [128](#18_Chapter_09.xhtml_page128)

applying to Blink sketch, [34–35](#12_Chapter_03.xhtml_page34)

count as local variable, [53–54](#13_Chapter_04.xhtml_page53)

defining for every sketch, [32–33](#12_Chapter_03.xhtml_page32)

for loops, [43–46](#12_Chapter_03.xhtml_page43)

Morse code translator, [72–74](#14_Chapter_05.xhtml_page72)

needed in Arduino “boilerplate” code, [31–32](#12_Chapter_03.xhtml_page31)

parameters, [51](#13_Chapter_04.xhtml_page51)

performing arithmetic in Arduino, [37](#12_Chapter_03.xhtml_page37)

using Arduino Uno as Web server, [134](#19_Chapter_10.xhtml_page134)

while loops, [46–47](#12_Chapter_03.xhtml_page46)

### M

MAC address, finding for Arduino Uno, [132–134](#19_Chapter_10.xhtml_page132)

Mac computers

installing Arduino software on, [16](#11_Chapter_02.xhtml_page16)

selecting serial port, [19](#11_Chapter_02.xhtml_page19)

Machine code, compilation into, [30–31](#12_Chapter_03.xhtml_page30)

`map` function, math functions in Arduino library, [100](#16_Chapter_07.xhtml_page100)

Math functions, in standard Arduino library, [100](#16_Chapter_07.xhtml_page100)

`max` function, math functions in Arduino library, [100](#16_Chapter_07.xhtml_page100)

Member variables, C++ language, [157](#20_Chapter_11.xhtml_page157)

Memory, storing variables and array data in, [65](#14_Chapter_05.xhtml_page65)

Message board displays, USB message board, [121–123](#18_Chapter_09.xhtml_page121)

Methods, C++

in header file, [159–160](#20_Chapter_11.xhtml_page159)

in implementation file, [161](#20_Chapter_11.xhtml_page161)

keywords and, [162](#20_Chapter_11.xhtml_page162)

overview of, [157–158](#20_Chapter_11.xhtml_page157)

Microcontroller, Arduino

analog inputs, [4](#10_Chapter_01.xhtml_page4)

Arduino family. *See* Arduino family

chip, [5–6](#10_Chapter_01.xhtml_page5)

development boards, [2–3](#10_Chapter_01.xhtml_page2)

digital connections, [5](#10_Chapter_01.xhtml_page5)

other components, [6](#10_Chapter_01.xhtml_page6)

overview of, [1–2](#10_Chapter_01.xhtml_page1)

power connections, [4](#10_Chapter_01.xhtml_page4)

power supply, [4](#10_Chapter_01.xhtml_page4)

tour of Arduino board, [3](#10_Chapter_01.xhtml_page3)

`min` function, math functions in Arduino library, [100](#16_Chapter_07.xhtml_page100)

Minus (−), as arithmetic operator, [41](#12_Chapter_03.xhtml_page41)

Monitors. *See* Displays

Morse code

data structure for translator, [70–71](#14_Chapter_05.xhtml_page70)

`flashDotOrDash` function for translator, [75–76](#14_Chapter_05.xhtml_page75)

`flashSequence` function for translator, [75](#14_Chapter_05.xhtml_page75)

globals and setup for translator, [70–71](#14_Chapter_05.xhtml_page70)

`loop` function for translator, [72–74](#14_Chapter_05.xhtml_page72)

SOS example, [66–67](#14_Chapter_05.xhtml_page66)

translator application, [69–70](#14_Chapter_05.xhtml_page69)

translator listing, [76–78](#14_Chapter_05.xhtml_page76)

Motor, types of shield boards, [7](#10_Chapter_01.xhtml_page7)

Multimeter

testing/measuring output with, [80–81](#15_Chapter_06.xhtml_page80)

testing voltage, [92–93](#15_Chapter_06.xhtml_page92)

Multiplication operator, [41](#12_Chapter_03.xhtml_page41)

### N

Naming conventions, C++, [160](#20_Chapter_11.xhtml_page160)

Node MCU board

Arduino clones/variants, [13](#10_Chapter_01.xhtml_page13)

IFTTT and ESP8266, [153–155](#19_Chapter_10.xhtml_page153)

Web-controlled, [145–148](#19_Chapter_10.xhtml_page145)

as Web servers, [140–145](#19_Chapter_10.xhtml_page140)

Not equal to (!=), comparison operators, [43](#12_Chapter_03.xhtml_page43)

`not` operator (!), use of booleans in truth tables, [58](#13_Chapter_04.xhtml_page58)

Numeric variables, C language, [39–41](#12_Chapter_03.xhtml_page39)

### O

Object orientation, C++, [157](#20_Chapter_11.xhtml_page157)

Objects, in C++ header, [159–160](#20_Chapter_11.xhtml_page159)

OLED (organic light-emitting diode)

comparing with LCDs, [119](#18_Chapter_09.xhtml_page119)

connecting, [125–126](#18_Chapter_09.xhtml_page125)

overview of, [124–125](#18_Chapter_09.xhtml_page124)

software for, [126–128](#18_Chapter_09.xhtml_page126)

Operators

boolean, [57–58](#13_Chapter_04.xhtml_page57)

comparison, [43](#12_Chapter_03.xhtml_page43)

`or` operator (||), use of booleans in truth tables, [57–58](#13_Chapter_04.xhtml_page57)

Oscilloscope, tracing button press with, [87–88](#15_Chapter_06.xhtml_page87)

Outputs. *See* I/O (input/output)

### P

Parameters

of arguments, [28](#12_Chapter_03.xhtml_page28)

defining global, local, and static variables, [52](#13_Chapter_04.xhtml_page52)

function, [50–51](#13_Chapter_04.xhtml_page50)

Particle Photon

Arduino clones/variants, [13](#10_Chapter_01.xhtml_page13)

IoT programming, [156](#19_Chapter_10.xhtml_page156)

Passing arguments, [28](#12_Chapter_03.xhtml_page28)

PCB (printed circuit board), public availability of design, [2–3](#10_Chapter_01.xhtml_page2)

Physical computing, Arduino as, [1](#10_Chapter_01.xhtml_page1)

`pinMode` function, built in to setup function, [34](#12_Chapter_03.xhtml_page34), [81](#15_Chapter_06.xhtml_page81)

Pins

connecting to OLED display, [125–126](#18_Chapter_09.xhtml_page125)

controlling, [139](#19_Chapter_10.xhtml_page139)

feeding shift registers, [104](#16_Chapter_07.xhtml_page104)

interrupts, [104–106](#16_Chapter_07.xhtml_page104)

LCD Shield pin assignments, [122](#18_Chapter_09.xhtml_page122)

Plus (+), as arithmetic operator, [41](#12_Chapter_03.xhtml_page41)

Posting data, HTTP, [135](#19_Chapter_10.xhtml_page135)

`pow` function, math functions in Arduino library, [100](#16_Chapter_07.xhtml_page100)

Power connections, [4](#10_Chapter_01.xhtml_page4)

Power supply, [4](#10_Chapter_01.xhtml_page4)

Powering up, getting started with Arduino, [15](#11_Chapter_02.xhtml_page15)

`print` function, working with LCD displays, [121](#18_Chapter_09.xhtml_page121)

Printed circuit board (PCB), public availability of design, [2–3](#10_Chapter_01.xhtml_page2)

Private functions, C++, [158](#20_Chapter_11.xhtml_page158), [159–160](#20_Chapter_11.xhtml_page159)

Processing library, [97](#16_Chapter_07.xhtml_page97)

PROGMEM

storing constants, [107–108](#17_Chapter_08.xhtml_page107)

storing data in flash memory, [108–110](#17_Chapter_08.xhtml_page108)

Programming

in C language, [27–29](#12_Chapter_03.xhtml_page27)

for Internet of Things. *See* IoT (Internet of Things) programming

programming by intention, [72](#14_Chapter_05.xhtml_page72)

Programming languages

C. *See* C language

C++. *See* C++ language

what they are, [29–33](#12_Chapter_03.xhtml_page29)

Programs. *See* Sketches

Pseudo-random numbers, [99](#16_Chapter_07.xhtml_page99)

Public functions, C++, [157](#20_Chapter_11.xhtml_page157), [159](#20_Chapter_11.xhtml_page159)

Pull-up resistors

digital input, [83–86](#15_Chapter_06.xhtml_page83)

internal, [86–87](#15_Chapter_06.xhtml_page86)

Punctuation, C language syntax, [28](#12_Chapter_03.xhtml_page28)

PWM (Pulse Width Modulation), analog outputs and, [92–94](#15_Chapter_06.xhtml_page92)

### Q

Quartz crystal oscillator, components of microcontrollers, [6](#10_Chapter_01.xhtml_page6)

### R

RAM (random access memory), [1](#10_Chapter_01.xhtml_page1)

`random` function, in standard Arduino library, [97–99](#16_Chapter_07.xhtml_page97)

Range compression, [116–117](#17_Chapter_08.xhtml_page116)

Register, shift register chips, [104](#16_Chapter_07.xhtml_page104)

Relays, types of shield boards, [7](#10_Chapter_01.xhtml_page7)

Reset button

components of microcontrollers, [6](#10_Chapter_01.xhtml_page6)

power connections and, [4](#10_Chapter_01.xhtml_page4)

Resistors

internal pull-up resistors in digital input, [86–87](#15_Chapter_06.xhtml_page86)

pull-up resistors in digital input, [83–86](#15_Chapter_06.xhtml_page83)

`return` statement, functions and, [55](#13_Chapter_04.xhtml_page55)

### S

SCK (clock pin), connecting to OLED display, [125–126](#18_Chapter_09.xhtml_page125)

Screens. *See* Displays

SDA (data pin), connecting to OLED display, [125–126](#18_Chapter_09.xhtml_page125)

Serial bus standard, I2C, [125](#18_Chapter_09.xhtml_page125)

Serial Monitor

digital outputs and, [81–82](#15_Chapter_06.xhtml_page81)

internal pull-up resistors in digital input, [86–87](#15_Chapter_06.xhtml_page86)

printing out array values to, [64–65](#14_Chapter_05.xhtml_page64)

pull-up resistors in digital input, [83–86](#15_Chapter_06.xhtml_page83)

reading/writing to EEPROM, [110–111](#17_Chapter_08.xhtml_page110)

sending commands to LCD display, [123](#18_Chapter_09.xhtml_page123)

sending text to, [64–65](#14_Chapter_05.xhtml_page64)

testing experiments in C, [37–39](#12_Chapter_03.xhtml_page37)

viewing analog input, [94–95](#15_Chapter_06.xhtml_page94)

viewing numeric variable, [39–41](#12_Chapter_03.xhtml_page39)

viewing random numbers, [98–99](#16_Chapter_07.xhtml_page98)

Serial port, selecting, [19](#11_Chapter_02.xhtml_page19)

Serial Programming Connector, components of microcontrollers, [6](#10_Chapter_01.xhtml_page6)

`serial.available()`, serial communication with Arduino via USB, [73](#14_Chapter_05.xhtml_page73)

`setCursor` function, working with LCD displays, [121](#18_Chapter_09.xhtml_page121)

`setup` function

adding display software, [128](#18_Chapter_09.xhtml_page128)

applying to Blink sketch, [34–35](#12_Chapter_03.xhtml_page34)

defining for every sketch, [32–33](#12_Chapter_03.xhtml_page32)

for Morse code translator, [70–71](#14_Chapter_05.xhtml_page70)

needed in Arduino “boilerplate” code, [31–32](#12_Chapter_03.xhtml_page31)

testing experiments in C, [37–39](#12_Chapter_03.xhtml_page37)

USB message board, [123](#18_Chapter_09.xhtml_page123)

using Arduino Uno as Web server, [134](#19_Chapter_10.xhtml_page134)

Shield boards

ESP8266 WiFi System on a Chip, [140–145](#19_Chapter_10.xhtml_page140)

Ethernet shield for Web-controlled Arduino, [135–140](#19_Chapter_10.xhtml_page135)

LCD module, [120](#18_Chapter_09.xhtml_page120)

LCD pin assignments, [122](#18_Chapter_09.xhtml_page122)

overview of, [7](#10_Chapter_01.xhtml_page7)

using Arduino as Ethernet shield, [129](#19_Chapter_10.xhtml_page129), [132–135](#19_Chapter_10.xhtml_page132)

Shift register chips, standard Arduino library, [104](#16_Chapter_07.xhtml_page104)

ShiftOut function, [104](#16_Chapter_07.xhtml_page104)

`sin` function, math functions in Arduino library, [100](#16_Chapter_07.xhtml_page100)

Sketchbook, for folder organization of sketches, [22–25](#11_Chapter_02.xhtml_page22)

Sketches. *See also* Software

defining setup and loop functions for, [32–33](#12_Chapter_03.xhtml_page32)

installing software, [16](#11_Chapter_02.xhtml_page16)

uploading first sketch, [17–22](#11_Chapter_02.xhtml_page17)

working with Arduino application, [22–25](#11_Chapter_02.xhtml_page22)

Slash(/), as division operator, [41](#12_Chapter_03.xhtml_page41)

Slashes (//), coding style for comments, [61](#13_Chapter_04.xhtml_page61)

Software. *See also* Sketches

for displays, [126–128](#18_Chapter_09.xhtml_page126)

installing, [16](#11_Chapter_02.xhtml_page16)

uploading first sketch, [17–22](#11_Chapter_02.xhtml_page17)

working with Arduino application, [22–25](#11_Chapter_02.xhtml_page22)

Spaces

coding style for whitespace, [60–61](#13_Chapter_04.xhtml_page60)

in syntax of C language, [28](#12_Chapter_03.xhtml_page28)

`sqrt` function, math functions in Arduino library, [100](#16_Chapter_07.xhtml_page100)

Square-wave signal, generating, [102–103](#16_Chapter_07.xhtml_page102)

Standard Arduino library

advanced I/O, [102](#16_Chapter_07.xhtml_page102)

bit manipulation, [100–102](#16_Chapter_07.xhtml_page100)

interrupts, [104–106](#16_Chapter_07.xhtml_page104)

math functions, [100](#16_Chapter_07.xhtml_page100)

overview of, [97](#16_Chapter_07.xhtml_page97)

random numbers, [97–99](#16_Chapter_07.xhtml_page97)

shift register chips, [104](#16_Chapter_07.xhtml_page104)

`tone` function, [102–103](#16_Chapter_07.xhtml_page102)

Static variables, in functions, [52–54](#13_Chapter_04.xhtml_page52)

Strings

storing in EEPROM, [113–115](#17_Chapter_08.xhtml_page113)

string arrays, [67](#14_Chapter_05.xhtml_page67)

string literals, [67–68](#14_Chapter_05.xhtml_page67), [71](#14_Chapter_05.xhtml_page71)

string variables, [68](#14_Chapter_05.xhtml_page68)

Switches

connecting to Arduino board, [85–86](#15_Chapter_06.xhtml_page85)

using wire as, [89](#15_Chapter_06.xhtml_page89)

Syntax

C language, [28](#12_Chapter_03.xhtml_page28)

of for loops, [45](#12_Chapter_03.xhtml_page45)

### T

Tags, HTML syntax, [131](#19_Chapter_10.xhtml_page131)

`tan` function, math functions in Arduino library, [100](#16_Chapter_07.xhtml_page100)

Testing experiments, C language, [37–39](#12_Chapter_03.xhtml_page37)

Text, [67](#14_Chapter_05.xhtml_page67). *See also* Strings

Todos, adding to code, [62](#13_Chapter_04.xhtml_page62)

`tone` function, [102–103](#16_Chapter_07.xhtml_page102)

Tools menu, selecting board type, [18](#11_Chapter_02.xhtml_page18)

Triggers, calling Web services, [149](#19_Chapter_10.xhtml_page149)

True/false logic, [57–58](#13_Chapter_04.xhtml_page57)

Truth tables, use of booleans in, [57](#13_Chapter_04.xhtml_page57)

### U

UART (Universal Asynchronous Receiver/Transmitter), [73](#14_Chapter_05.xhtml_page73)

USB (universal serial bus)

connecting Arduino to computer with, [1](#10_Chapter_01.xhtml_page1)

powering up Arduino via, [15](#11_Chapter_02.xhtml_page15)

serial communication with Arduino, [73](#14_Chapter_05.xhtml_page73)

USB interface chip on microcontroller, [6](#10_Chapter_01.xhtml_page6)

USB message board, [121–123](#18_Chapter_09.xhtml_page121)

USB Host, types of shield boards, [7](#10_Chapter_01.xhtml_page7)

### V

Variables

boolean, [57–58](#13_Chapter_04.xhtml_page57)

in C++ header, [160](#20_Chapter_11.xhtml_page160)

constants, [47](#12_Chapter_03.xhtml_page47)

declaring in for loops, [45](#12_Chapter_03.xhtml_page45)

defining for Blink sketch, [36–37](#12_Chapter_03.xhtml_page36)

`float`, [56](#13_Chapter_04.xhtml_page56)

numeric variables, [39–41](#12_Chapter_03.xhtml_page39)

storing data, [65](#14_Chapter_05.xhtml_page65)

string variables, [68](#14_Chapter_05.xhtml_page68)

`void` keyword

defining setup and loop functions for every sketch, [32–33](#12_Chapter_03.xhtml_page32)

return values and, [55](#13_Chapter_04.xhtml_page55)

Voltage

measuring with Arduino Uno, [95–96](#15_Chapter_06.xhtml_page95)

testing with multimeter, [92–93](#15_Chapter_06.xhtml_page92)

Voltage regulator, components of microcontrollers, [4](#10_Chapter_01.xhtml_page4)

### W

Web browsers, using HTTP, [130](#19_Chapter_10.xhtml_page130)

Web-controlled Arduino, [135–140](#19_Chapter_10.xhtml_page135)

Web servers

calling Web services, [148–151](#19_Chapter_10.xhtml_page148)

communicating with, [130](#19_Chapter_10.xhtml_page130)

HTML and, [131–132](#19_Chapter_10.xhtml_page131)

HTTP and, [130](#19_Chapter_10.xhtml_page130)

Node MCU Web server, [140–145](#19_Chapter_10.xhtml_page140)

using Arduino Uno as, [132–135](#19_Chapter_10.xhtml_page132)

Web-controlled Arduino, [135–140](#19_Chapter_10.xhtml_page135)

Web-controlled Node MCU, [145–148](#19_Chapter_10.xhtml_page145)

Web services, calling, [148–151](#19_Chapter_10.xhtml_page148)

`while` command, C language, [46–47](#12_Chapter_03.xhtml_page46)

Whitespace, coding style for functions, [60–61](#13_Chapter_04.xhtml_page60)

WiFi System on a Chip. *See* ESP8266 WiFi System on a Chip

Windows computers

installing Arduino software on, [16](#11_Chapter_02.xhtml_page16)

selecting serial port, [19](#11_Chapter_02.xhtml_page19)

Wiring library, [97](#16_Chapter_07.xhtml_page97)

Wirth, Niklaus, [63](#14_Chapter_05.xhtml_page63)