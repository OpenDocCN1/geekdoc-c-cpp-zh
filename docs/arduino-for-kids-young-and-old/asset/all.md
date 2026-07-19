![](cover.jpeg)

# Copyright

## From legal to ISBN

Arduino® for Kids Young and Old ©2014 Daniel W. Milligan

All content is copyright 2014, Daniel Milligan. All rights reserved. No part of this publication or the files that it is comprised of shall be legally produced, reproduced, or transmitted by any form or any means without the express permission of the publisher.

Published by Daniel Milligan 2014, all photo's and images are copyright Milligan Photography unless otherwise noted.

Limit of Liability and Disclaimer of Warranty: The publisher has made every effort in preparing this book to ensure that the content is accurate however the information provided herein is provided "as is" and without warranty. Daniel Milligan et al makes no representation or warranties with respect to the accuracy or completeness of the contents of this book and specifically disclaims any implied warranties of merchantability or fitness for any particular purpose and shall in no event be liable for any loss of profit or any other commercial damage, including but not limited to special, incidental, consequential, or other damages.

Trademarks: This book identifies product names and services known or suspected to be trademarks, registered trademarks, or service marks of their respective holders. They are used throughout this book in an editorial fashion only. While great care has been taken to appropriately identify these items, there is potential that some may have not been identified as such and Daniel Milligan cannot vouch for the accuracy of this information. Use of a term in this book should not be regarded as affecting the validity of any trademark, registered trademark, or service mark. Daniel Milligan is not associated with any product or vendor mentioned in this book other then being the primary of Milligan Photography.

```
 First edition 2014

 ISBN-10: 0985855630
 ISBN-13: 978-0-9858556-3-5 
```

Thanks go out to all of my friends and family, and especially my wife Sylvine for all of the support and love through the years.

The resources linked to at the end of this eBook were valid as of the time of the writing of this eBook and include links to various tools helpful to those getting started with open source hardware and hobby programming / engineering.

![chapter end graphic](images/00001.jpeg)

# Introduction

## Getting started with Ardunio®

First I am going to make some assumptions both knowingly and unknowingly. I work with a lot of this technology on a regular basis and may inadvertently leave something out. It's not that I don't feel it's important or needed but more that I might not think it needs explaining or requires additional detail. With that, if you should have any questions please do not hesitate to email me at [Email Dan](mailto:books@afmsoftware.com?subject=Arduino%20Starter).

This book is intended for those wanting to start working with open source hardware and software in order to build their own creations using tools and components readily available. While I will point you to specific links to learn more about various software and/or hardware modules, I am not going to get into too much of programming skills 101 or hardware design 101\. My assumption is that you either have some knowledge in this area or are willing to go and learn it as you go. I will try to cover everything in enough detail that you won't have to dig too far to get additional information however it will vary depending on the individual. As the title of the book states, this book is focused on developing with the Arduino® platform. While a number of the examples and overall concepts will be applicable to a number of micro-controllers, I will be focusing on the Arduino® family of modules and specifically those built around the Atmel® AVR family of devices.

The following are some basic terms I will be using that you should be aware of.

Prototype

An experimental design (software/hardware) used to prove a theory or realize an idea

Arduino®

An open source hardware/software solution used for prototyping

Shield

An add on card i.e. expander board to be used in conjunction with an Arduino®. This may also be called a daughter board.

DC

Direct Current which is what most prototyping boards utilize

AC

Alternating Current which is the standard current coming into a house and delivered to each outlet within the house *

Java™

A high level programming language and environment originally designed by Sun® Computer and now owned by Oracle®

C

A high level programming language designed at Bell Labs[[1](#part0012_split_001.html_Ref1)]

Sketch

An Arduino® term for describing the code to be executed on the Arduino®

USB

Universal Serial Bus - standard connection for peripherals such as mice, keyboards, card readers, etc.

LED

Light Emitting Diode

Compiler

A software application which generates executable code from a source file such as a sketch.

Variable

A data type found in a sketch which can be assigned a value. Variables can be of different types to represent different data types such as integers, characters, and floating point numbers

Signed value

A value that can represent both positive and negative numbers

Unsigned value

A value that can only represent positive numbers

Parameter

A value passed into a method during program execution

Return Value

A value returned by a method once it has finished processing

Object

A software construct utilized in high level programming languages such as Java™ and C++

Baud, Baud Rate

The speed at which a communication device operates at

* As I am based in the United States, a typical AC current coming into each house would be in the 120V range while in Europe, the typical value would be in the 240V range. [[2](#part0012_split_001.html_Ref2)]. While most items purchased operate via 120V's AC, in actuality they operate on a DC voltage and have transformers inside or as part of the power cord to convert from AC to DC.

Having the right tool is always beneficial when working on any kind of project. The same is true when working with both software and hardware. Before you get started you will want to make sure you have the following items:

*   a functioning computer (Macintosh® OSX, Windows® based PC, or Linux®)
*   an available USB host port. The port should be of the type A which will look something like this: ![USB Port image](images/00002.jpeg)
*   a clean area to work in and spread out a bit
*   internet access to look up information
*   the Java Runtime Environment which can be downloaded: [here](http://java.com/en/download/index.jsp)
*   the Arduino® development environment which can be downloaded: [here](http://arduino.cc/en/Main/Software)
*   ** an Arduino® kit such as this one from [MakerSHED](http://www.makershed.com/Getting_Started_with_Arduino_Kit_V3_0_p/msgsa.htm)
*   *** a breadboard for prototyping circuits
*   *** jumper wires for connecting the various parts of your circuits together and to the Arduino®
*   A +5v power supply able to deliver 2 Amps of current such as: [5v 2A Supply](http://www.adafruit.com/products/276).
*   and a comfortable chair

** Electronic components are very susceptible to static electricity. This means that any static electricity that builds up on yourself could damage the component, like the micro-controller, when you touch it and transfer that energy from yourself to the component. In some cases, this damage cannot be detected and the component will work most of the time but not always. Consider it like a crack in a bowl. It may be fine most of the time however once in a while, some liquid may spill. And then if it happens to be hot, you will get burned.

*** If you happen to purchase the Arduino® kit as specified above then there will be a breadboard and jumpers included with it.

The following list are some additional items which are not required however I regularly use during development.

*   a soldering iron for building circuits
*   a solder sucker for removing the excess solder applied with the soldering iron
*   solid strand wire in the 22 gauge (AWG) area of thickness
*   wire strippers
*   wire cutters
*   small pliers
*   a multimeter for measuring the voltage at a given point and checking continuity within a circuit. ![Multimeter image](images/00003.jpeg)

Finally a list of some items that you will probably not need however knowing they exist is always good.

*   a logic analyzer for debugging protocol issues such as those that might come up when using serial peripheral interfaces (SPI) among other things
*   an oscilloscope for debugging issues related to communication signals or Pulse Width Modulation (PWM) output![Oscilloscope image](images/00004.jpeg)

Most if these items are available at your local [Radio Shack](http://www.radioshack.com) , [Fry's](http://www.frys.com), or whichever local electronics store catering to hobbyists in your corner of the world. In some cases, the devices used will only be available from on-line merchants which I will attempt to provide various links to companies I have dealt with successfully.

All circuit diagrams included in this book are provided using the creative commons license for Attribution - Share Alike 3.0 Unported[[3](#part0012_split_001.html_Ref3)]. The complete set of circuit diagrams can be found here: [Circuit Diagrams](http://book.afmsoftware.com/resources/CircuitDiagrams.zip). Each of the circuit diagrams were created using the Fritzing development tool which can be found on the web at [Fritzing.org](http://fritzing.org/). For each image that is bound by the creative commons license, the following icon will be associated with it: ![Creative Commons - Attribution - Share Alike](images/00005.jpeg). In addition, I have followed standard practice in coloring the wires at least in terms of +5v (red) and GND (black). For the schematics, opposed to using traditional schematics, I have chosen to use the breadboard images out of Fritzing as I feel they better convey the required information in this context.

With all of that said, lets dive into it and have some fun!

![chapter end graphic](images/00001.jpeg)

# Setup

## Getting ready to develop

Setting up your computer for development can be a challenge depending on the tools and the support available. Hopefully that will not be the case with the Arduino® toolset. However, just in case, I will walk you through the process. If you are already up and going then please skip over this chapter and proceed to developing your first sketch in the [Arduino® Platform](#part0003_split_000.html_Arduino) chapter.

While you may already have Java™ installed on your computer, it wouldn't hurt to ensure you have the latest version so please download the following package from Oracle® [here](http://java.com/en/download/index.jsp). This page should detect your current system and give you a download button to start. Once downloaded, follow the directions provided by Oracle® to install this on your system.

Now that Java™ is ready to go, you can download the Arduino® environment for development. This software can be found [here](http://arduino.cc/en/Main/Software). For this package, there isn't an installer* per se however you do need to unzip it. Navigate to your download folder or the destination that you selected when downloading the package to get access to the application. If you are on a Macintosh OSX® platform than it will unzip the package for you. If you are on a Windows® platform than the Explorer application will be able to unzip it for you. For the Linux® platform, when you download it, I expect it will ask you if it should open it with the archive manager which you can choose to or from the terminal you can utilize the unzip application. For my own development, I moved the package to my Development folder which is located on my desktop. I than unzipped it in that location so it will be centrally located with other things I am working on.

* As of the 1.05 version of the Arduino™ software for Windows® there is an installer available to assist with installing the Arduino™ software. I have left this chapter in for reference and for those not on a Windows® based platform.

The following sequence is the platform extraction and placement on my Windows® based machine and the initial loading of the platform. The first image shows the file once it has been downloaded from the Arduino™ website.

![Download file of Arduino](images/00006.jpeg)

This image shows the Windows® wizard for extracting a zipped file. I have selected my Development folder on my desktop for the placement of the platform.

![Extracting the Arduino platform](images/00007.jpeg)

This image shows the Windows® extraction in progress which on my system is fairly slow as it is not the fastest system in the world.

![Extracting the Arduino platform in progress](images/00008.jpeg)

This image shows the extracted file folder which has inside it the actual Arduino® folder. Because I didn't want to have to go too deep into the folder hierarchy, I elected to move it up one.

![Showing the extracted folder once extraction has completed](images/00009.jpeg)

This image shows the extracted folder once I moved it up one level, removing the arduino-1.0.3-windows folder.

![Moving the folder up a level so as to keep it clean](images/00010.jpeg)

In this image, I have elected to display everything as large icons. At this point you will be ready to launch the development platform.

![Showing the contents of the Arduino folder as large icons](images/00011.jpeg)

When you first launch the application, you will most likely see the following security warning. This is expected and is just noting to you, the end user, that the file was downloaded and the publisher is unknown. While I don't expect you to have any issues running this software, I do advise that you take the necessary precautions with your system and ensure that you have up to date virus protection installed and running. Also note the checkbox which will allow you to skip the security warning the next time you open the application.

![Standard security warning resulting from the downloaded file](images/00012.jpeg)

At this point, you should see the following main screen for the Arduino® environment.

![The main file of the Arduino platform](images/00013.jpeg)![chapter end graphic](images/00001.jpeg)

# The Arduino® Platform

## What it is

The Arduino® package is a cost effective, easy to use, prototyping board which can be enhanced to do many tasks. The micro-controller that this board utilizes has been created with a number of general purpose input and output (GPIO) pins. These GPIO pins have many functions that you can utilize to create a number of designs. While the controller and overall design are fairly simple in todays terms, the community that has developed around the platform is where it really shines. With a simple internet search you can find a number of forums and stores promoting and selling various products to enhance your Arduino®, from Ethernet port shields to LCD shields to a number of other's in between.[[4](#part0012_split_001.html_Ref4)] Considering all of these expansion options are readily available, the Arduino® becomes a very useful micro-controller. In this book I will focus on the abilities of one of the Arduino® boards, the Arduino® UNO. It does everything that we need and is based on a 5 volt system which can be used with a variety of external devices. This will also limit the discussion to one of the more popular Atmel® AVR micro-controllers, the ATmega328.

## What it isn't

This is not a full fledged computer with monitor, keyboard, and mouse as you have probably already noticed. While it is fast doing simple tasks, it will not break any super computer processing speeds. With today's processors running at 100x or 200x the speed of this little controller, it isn't surprising that it isn't as fast as a full fledged computer. The overall Arduino® environment is based on approachable and easy to use tools. The environment does it's best to prevent mishaps when using it and the target devices. With this extra security comes limitations and potential speed losses. There is also potential for conflicting devices due to the overloading of processor pins to internal functions. However for the kinds of projects that we will want to do, it is more than capable.

### Getting Started

So where do we start? Assuming you have already purchased an Arduino® and have the development environment installed, our first order of business is to make sure everything is working ok. If you haven't already downloaded and configured your system, take a look at the chapter entitled [Setup](#part0002_split_000.html_Setup) for information regarding setting up your development environment. When ready, open up the development platform and you should see something like this:

![Ardunio main view](images/00013.jpeg)

Now we need to make sure your Arduino® is properly registered with your development environment. If you have not connected your Arduino® to your development system than you may need to load the drivers in order for the board to communicate with your system. On the Windows™ platform, you can find the necessary drivers in the drivers folder under the Arduino® software folder. If you are running on the Macintosh® or Linux® then you will want to visit the USB chip manufacturer web page to download the drivers for your particular system. They can be found [here](http://www.ftdichip.com/Drivers/VCP.htm). You will also find the latest Windows® drivers there.

The first thing to notice in the previous image is the currently selected board and communication port i.e. COM port. This is shown in the lower right hand side of the image. This development board is an Arduino® UNO connected to COM3\. In order to work with your Arduino® you will need to ensure the correct COM port is selected along with the correct hardware board. To do this, select the tools menu item on the menu bar.

Note: the menu can take some time to actually pop up depending upon the user's environment.

From the tools menu, select board and then select the type of board that you have. The following image shows the board selection where I have selected the Arduino® UNO as my board.

![Selection of the board from drop down tool menu](images/00016.jpeg)

Once the proper board has been selected, the corresponding COM port that the operating system has assigned to the development board can be selected. The following image shows the selection of the COM port for the attached Arduino® board.

![Selection of the comm port from drop down tool menu](images/00017.jpeg)

Before we go any further, it will be good to look at some of the different variable types that you may find within an Arduino® sketch. The following are some of the more common variable types you may come across:

char

a signed value representing the values from -128 to 127\. Char's are stored using 8 bits of data

unsigned char

an unsigned value representing the values from 0 to 255\. Like a char, an unsigned char is stored using 8 bits of data

byte

Analogous to an unsigned char and used within Arduino® sketches

int

a signed integer type representing the values from -32,768 to 32,767. Int's are stored using 16 bits of data*

unsigned int

an unsigned integer type representing the values from 0 to 65,535\. Int's are stored using 16 bits of data*

long

a signed value representing the values from -2,147,483,648 to 2,147,483,647\. Long's are stored using 32 bits of data.*

unsigned long

an unsigned value representing the values from 0 to 4,294,967,295. Unsigned long's are stored using 32 bits of data.*

float

a float value represents a wide range of signed values in decimal notation and is primarily used to represent fractions and other non integer values. Float's are stored as 32 bits of data.**

double

For the Arduino® platform, the double is analogous to a float.

void

the void type typically indicates a non-value however is dependent on its usage. For method definitions, a return value of void indicates that no value will be returned by the method.

* the size of an int or long may be different based on the processor in use. For the Atmel® micro-controller we are using an integer will be 16 bits i.e. 2 bytes while the long will be 32 bits i.e. 4 bytes. Other micro-controller's may have larger integer sizes. You should verify the sizes of the data types of your target hardware to ensure you do not make any false assumptions.

** floats are stored as 32 bits of data which represents the mantissa and the exponent. Floats have about 7 decimal digits of precision which should be considered when processing data.

Every Arduino® sketch will consist of two functions i.e. methods, setup and loop. As you can probably imagine, setup is where you will configure your Arduino® for operation such as specifying the direction of data flow on a certain pin etc. The loop function is where all of the processing is done and will be executed basically as fast as the micro-controller can go. Let's take a look at each of these methods in some detail and see how they work.

### Setup

As mentioned above, this is where the configuration of the micro-controller is performed. This isn't to say that the micro-controller configuration cannot be changed outside of this method however for consistency it is best to do any configuration here. There will be exceptions to this rule but for now this will be good advice to follow. So what kind of things should be configured when you start executing code on your Arduino®? Primarily it will be proper to configure your digital pins as either input or output and start any sub-systems that may need to be started such as the serial communications port. The main reason is that this method is only called once while the loop is called every pass through the code. It wouldn't be very productive to keep initializing the serial communications and the like every time through the main loop. Consider the following code snippet from this [sketch](http://book.afmsoftware.com/resources/SkeletonSketch.zip):

```
 /*
  * Setup - main configuration point of our sketch to configure
  *         the Arduino for operation
  *
  * Params - none
  *
  * Returns - nothing
  */

 void setup()
 {
   Serial.begin(9600);

   pinMode(13, OUTPUT);
 } 
```

The first portion are the comments describing what the intention of the method is. I say intention as with all things, they start as good intentions and then veer off from there. For Arduino® sketches, there are two acceptable types of comments, the block as shown above and the single line [[5](#part0012_split_001.html_Ref5)]. The block comment is everything between the opening token /* and the closing token */ which indicates to the Arduino® compiler that what lies between the tokens including the tokens themselves can be ignored. While the above example shows a block comment spanning multiple lines, there is nothing preventing it from being a set of single line comments such as:

```
 //
// Setup - main configuration point of our sketch to configure
//         the Arduino for operation
//
// Params - none
//
// Returns - nothing
// 
```

I would be reluctant to put the whole thing on one line as I prefer to have some whitespace i.e. blank area around the comments for readability. You could do something like the following:

```
 // Setup - main configuration point of our sketch to configure the Arduino for operation 
```

The other things of note inside of the comment block is the Params and Returns lines. The first tells the viewer of your code what parameters need to be passed into the method. As shown above, not all methods require parameters. The second line indicates what values one might expect to be returned from the method when it finishes. In this case, nothing is returned. Later on we will explore methods that take both parameters and return values to the calling application. This convention is something I tend to use most often and part of the reason why I don't use a single line comment at the beginning of functions i.e. methods. Even though nothing is passed in as a parameter nor returned, have it spelled out never hurts.

Following the comment block is the name of the method which declares what the return value type will be, if any, and also details any parameters that need to be supplied when the application calls the method. In this case, the method does not take any parameters and does not return any value. This is indicated by the word void. Next comes the opening brace, { which indicates the start of the method definition. There is also a closing brace, } which indicates the end of the method definition. The opening and closing braces are not limited to method definitions and will be used in additional constructs which will be explored later on. Now we get to the actual code. The first line is as follows:

```
 Serial.begin(9600); 
```

This code, which is part of the standard Arduino® platform, calls the begin method which is part of the Serial object. An object is a collection of related methods and variables that work together to perform a task. The C++ term for an object is a class which is fundamental to C++ and object oriented programming in general. We will be looking at various objects and constructs as we progress through this book. As you can see, the begin method takes a single parameter which in this case is a value of 9600. This value represents the speed at which the serial port of the Arduino® will operate at. While the speed can be a number of values [[6](#part0012_split_001.html_Ref6)], 9600 is one that I remember easily and typically use. In terms of speed, this value is typically given as a baud rate which is the number of symbols transmitted per second. This value happens to be the same as the bit rate resulting in 9600 bits per second in transmission speed. The end data rate however will be somewhat less due to some of the bits being used to indicate the start and ending of each packet. The main thing to note is that when you open up a serial monitor application such as the one included with the Arduino® software, you will need to ensure that it is set for the same speed that was specified in the sketch. So why would we want to start the serial port? In general this is the simplest way to debug your application. You upload your code, it executes and you monitor the results. It can be real useful when things are not working as expected and you need to dig in and figure out what the issue is. If application speed is a concern, than once you have completed your project, you can remove all of this code resulting in a smaller package and faster execution time. A few things to be careful of though is that for time sensitive applications, the inclusion or exclusion of this code could change your results. Also care should be taken when placing any types of debug lines as you may end up with more information than you can use.

```
 pinMode(13, OUTPUT); 
```

The second line of code, also a standard part of the Arduino® platform, is where the digital pin, 13, is configured as an output. On the Arduino®, there is a LED connected to the digital pin number 13 which can be used as a visual indicator of sorts. The first parameter is the pin that will be configured while the second parameter is the mode which in this case is OUTPUT. The word OUTPUT is a constant value defined by the Arduino® platform. Typically it is good practice to create a constant value to specify what the particular pin will be doing opposed to a raw number. In this case, I left the number in the code to highlight what pin I was using and to keep the sketch simple. In the future examples, I will use more meaningful identifiers for these types of values.

### Loop

Loop is where all of the main processing of your sketch will be done. This method will be executed soon after the Setup method has completed and will continue to be executed for the life of your application that is to say until you power down your Arduino®. While this keeps the complexity of your code down, there are a few things to be careful of when writing code for the loop. The first thing to remember is that the speed at which loop is called can be variable based on the speed of the micro-controller and how much work is being done inside of your loop. Another thing to note is that if you need to receive input from the user, you may need to do that over multiple passes of the loop opposed to waiting until the input arrives otherwise you will prevent other activities from happening. Building upon the above code, I will demonstrate the basic sketch of turning the pin 13 LED on and off periodically causing it to flash. This is also included in the sketch noted previously.

```
 /*
  * loop - main method which will be called each time the
  *        Arduino goes through its main loop
  *
  * Params - none
  *
  * Returns - nothing
 */

 void loop()
 {
   digitalWrite(13, HIGH);
   delay(500);
   digitalWrite(13, LOW);
   delay(500);
   Serial.println("Led 13 has been toggled on and off.");
 } 
```

Again the method starts with a comment block describing what the method is intended to do along with the name of the method declaration indicating that no parameters are passed to the method and the method doesn't return any value.

```
 digitalWrite(13, HIGH); 
```

This first line of code calls the method digitalWrite which instructs the micro-controller to set the output value on pin 13 to HIGH. The word HIGH is another predefined value which you can use throughout your sketch as needed. Because we are writing a digital value out to this pin, it can only be one of two values, LOW or HIGH. These values correspond to 0 volts when set to LOW and 5* volts when set to HIGH. With this, the LED connected to pin 13 will turn on as there is now a positive voltage emitting from the given pin. When set to LOW, the voltage is set to 0 volts resulting in the LED turning off.

* the Arduino® UNO runs on 5 volts hence the value when set to HIGH will be 5 volts. Other boards, such as the [Arduino Due](http://arduino.cc/en/Main/ArduinoBoardDue), run at a lower voltage such as 3.3v so the output voltage when set to HIGH will be equivalent to that lower voltage.

When using a board with a lower overall voltage, care must be taken that the resistors and other components recommended in this book are adjusted accordingly. Because of the smaller voltage, less current will be generated as the current is equal to the voltage divided by the resistance. While this may be alright in most cases, you should also verify the maximum amount of current that each output pin can supply as they may differ across micro-controller devices.

```
 delay(500); 
```

The delay method is used to stop execution for a period of time. When I say stop execution, I really mean stopping execution of your code. The micro-controller is still processing data however your code will be paused until the delay method is finished. For this example, using delay is fine however later on we will explore better approaches to handle this. So why would I want a delay in my code anyways? Remember that the loop method is executed quite frequently and we want to be able to see the LED turn on an off. The delay that is specified is 500. This value is expressed in milliseconds which is to say how many 1/1000's (0.001) of a second the micro-controller should pause. For the above example, we are pausing for 500 milliseconds which is 1/2 second. The end result is the LED will turn on for 1/2 second and then back off for another 1/2 second or so. I say so because I have an additional line of code after the second delay which will take some time to execute and will skew the time. I could try and compensate by reducing the second delay to 499 milliseconds however that would be a guess unless I knew for sure how long the last line of code would take to execute. I would also have to factor in which micro-controller was executing the code along with the speed of that micro-controller. All in all it would be a significant challenge to do correctly. And while were are speaking of the last line of code, it's purpose is to just give us feedback that the loop is working properly and our board is functional. Typically I wouldn't do this as it will just fill up the communications buffer and if I didn't have the delay(s), we would quickly fill our monitor buffer with the same not so helpful information. This is an example of where you would want to be careful with where you place your debugging i.e. informational output data.

```
 Serial.println("Led 13 has been toggled on and off."); 
```

The serial class has a number of methods of which one of them is shown in the above code snippet. This particular version is for printing out a full line of text including the line feed so the next line will start on a new line. There is a related method Serial.print that will print out text much the same way however will not include a line feed. It is useful when you want to print out a number of items all on one line such as:

```
 Serial.print("Led: ");
   Serial.print(13);
   Serial.println(" has been toggled on and off."); 
```

The above code will result in the same output however I could have easily replaced the number 13 with a variable in order to use this code for any pin.

### Summary

So pulling it all together, an Arduino® sketch consists of two methods, the setup and loop methods. The setup method is used to configure your Arduino® for how it should operate while the loop method is where all of the work will be done for the life of the application. In addition, there are built in constants and classes such as the Serial class which can be used to assist with debugging or relaying information to the user.

![chapter end graphic](images/00001.jpeg)

# Input

## Monitoring our surroundings

Now that we have the Ardunio® setup and ready, we can dig into more interesting topics. The first of these is the input system that allows us to monitor our surroundings utilizing various analog and digital devices. In the following sections we will look at analog and digital inputs from a variety of devices which allow us to interpret our surroundings and act upon the various events when they happen.

### Analog Input

The Arduino® has several analog pins that can be used to read in the voltage level of a particular device to determine its value. The actual number of pins available to you will be dependent upon which AVR micro-controller is built into the board you have purchased. Regardless though, the basic operation will be the same. The analog input pins have a 10 bit resolution which is to say that each pin can detect up to 1024 levels of voltage. The values are based on ground as being the bottom i.e. no voltage coming in and up to five (5)* volts which is the maximum voltage for the micro-controller. You can also limit the top of the voltage range to a value less then 5 volts however for the following examples that will not be necessary. When the analog input is read in, it is actually using a scale much like a balance scale to determine the value. Imagine you have a basement that is flooding and there is a staircase coming up to the first floor. One thing you might want to know is how deep the water is and how fast is it rising? For the depth of the water it would be very easy if you happened to know how far apart each step on the staircase is. In this case, you could simply count how many steps were covered in water and do some simple arithmetic to determine the waters depth. Oddly enough the Arduino® is doing something very similar. It has a built in scale that compares its internal value with the value coming in on the analog pin. Each cycle, the device will increase the voltage and compare it to the incoming voltage. It knows how many cycles it has been since it started the comparison so once they are equal, the micro-controller knows the value of the external voltage. The micro-controller has 10 bits of resolution which means that it can count all the way from zero (0) to 1023 to find a value matching that which is being read at the analog input pin. Using the above analogy, it is like the micro-controller has a staircase with 1024 steps counting the floor as step number one (1). In the case, step number one is equal to zero (0) volts and step number 1024 is equal to five (5) volts. This corresponds to a voltage of 0 volts being equivalent to a digital value of 0 and a voltage of 5 volts being equivalent to a digital value of 1023\. As you can see, there is a fair amount of precision when using the 10 bit analog to digital converter. The downside to this type of converter is that it takes time to count from zero (0) up to the value that represents the incoming analog voltage. Just like the rate that the water rises in the basement, the comparison of each voltage value to the next highest value takes time as the micro-controller determines the equivalent voltage to the input voltage. The worst case of course is for 5 volts which is at the top of the range resulting in the micro-controller having to count 1024 times to get to a comparative value. In terms of computing time, this can be quite slow and could be as much as 260 microseconds for the given device. In human time, this is about 1/4 of a millisecond which in turn is 1/1000's (0.001) of one second. When looked at in this way, it is plenty fast enough for what we want to do. Speaking of what we want to do, the first thing is to determine what the temperature in the room is.

* For the Arduino UNO and MEGA, the maximum voltage that can be read in is 5 volts however on some systems, the maximum may be lower such as 3.3 volts or even 1.8 volts.

#### Temperature Reading

The first thing we will look at is how to read in a temperature value and then be able to react to it based on its value and/or delta from it's initial value. Luckily there are specific devices available that will increase in voltage as the surrounding temperature rises. Knowing this, we can connect one of these devices to our Arduino® and read in the value to determine the current temperature.

##### Required Components

*   Arduino® Board
*   4.7K Ohm Resistor
*   LM335 temperature sensor[[7](#part0012_split_001.html_Ref7)] or similar such as the NTE7225[[8](#part0012_split_001.html_Ref8)]

##### Tools

*   breadboard
*   jumper wires
*   voltage meter

##### Schematic

For this circuit, you will need to run 5 volts from the Arduino® to the first lead of the 4.7K Ohm resistor. The second lead of the 4.7K Ohm resistor is connected to pin two (2) of the LM335\. The third pin of the LM335 is connected to ground from the Arduino®. The final wire is connected from pin two (2) of the LM335 back to analog input zero (0) of the Arduino® in order to read the voltage drop across the LM335 as it pertains to the current temperature.![LM335 Temperature sensor circuit](images/00018.jpeg)

![Creative Commons - Attribution - Share Alike](images/00005.jpeg) Image created using: [Fritzing](http://fritzing.org/)

##### Software

The following is the code that is necessary to read in the analog voltage across the LM335 and display it to the serial port for review. Once we have our circuit working and the temperature values available, we will be able to further enhance the software and hardware to perform some useful functions.

For this sketch, I am using the well known formulas to convert from Celsius to Fahrenheit and from Fahrenheit to Celsius. These formulas are as follows:

```
 Celsius = ((Fahrenheit - 32) x 5) / 9
 Fahrenheit = ((Celsius x 9) / 5) + 32 
```

```
 /*
  * The temperature pin is where the input from the LM335 will be read from.
  * The base voltage is what the device (LM335) will measure at 0°C
  * The voltage reference is the max voltage that can be read in on the
  * analog input pin
  * The max sample count is the highest value that could be read in on the
  * analog input pin which will equal the voltage reference
  * The c to f conversion is the well known formula of multiplying the
  * C temp by 9 then dividing by 5
  * The f to c conversion is the well known formula of multiplying the
  * F temp by 5 then dividing by 9
  * The c to f delta is the difference between C and F at the freezing temperature
  */        
 const int temperaturePin = 0;
 const float baseVoltage = 2.730f; /* 2.730V at 0°C */
 const float voltageReference = 5.0f;
 const float maxSampleCount = 1023.0f;
 const float CtoFConversion = 9.0f / 5.0f;
 const float FtoCConversion = 5.0f / 9.0f;
 const float CtoFDelta = 32.0f;

 /*
  * Method declarations
  */

 float getTemperature(float temperatureVoltage);
 float convertTemperatureToF(float temperatureInCelsius);
 float convertTemperatureToC(float temperatureInFahrenheit);

 /*
  * getTemperature - determines the temperature in celsius based on the
  *         incoming voltage value assuming 2.73v equals 0°C
  *
  * Params - temperatureVoltage - the incoming voltage representing the temperature
  *
  * Returns - float - the actual temperature in celsius based on the incoming voltage
  */

 float getTemperature(float temperatureVoltage)
 {
   float currentTemperature = 0.0f;

   // From the datasheet, every 10 mv is equal to 1 °K - 0°C is 273°K equal to 2.73v
   // Temperature is scaled by 100 to bring it into the celsius scale from kelvin
   currentTemperature = (temperatureVoltage - baseVoltage) * 100;

   return currentTemperature;
 }

 /*
  * convertTemperatureToF - converts the temperature from Celsius to Fahrenheit
  *
  * Params - temperatureInCelsius - the incoming temperature in Celsius
  *
  * Returns - float - the temperature expressed in Fahrenheit
  */

 float convertTemperatureToF(float temperatureInCelsius)
 {
   float convertedTemperature = 0.0f;

   convertedTemperature = (temperatureInCelsius * CtoFConversion) + CtoFDelta;

   return convertedTemperature;
 }

 /*
  * convertTemperatureToC - converts the temperature from Fahrenheit to Celsius
  *
  * Params - temperatureInCelsius - the incoming temperature in Fahrenheit
  *
  * Returns - float - the temperature expressed in Celsius
  */

 float convertTemperatureToC(float temperatureInFahrenheit)
 {
   float convertedTemperature = 0.0f;

   convertedTemperature = (temperatureInFahrenheit - CtoFDelta) * FtoCConversion;

   return convertedTemperature;
 }

 /*
  * Setup - main configuration point of our sketch to configure
  *         the Arduino for analog input
  *
  * Params - none
  *
  * Returns - nothing
  */

 void setup()
 {
   analogReference(DEFAULT);
   Serial.begin(9600);
 }

 /*
  * loop - main method which will be called each time the
  *        Arduino goes through its main loop to read the
  *        current temperature value
  *
  * Params - none
  *
  * Returns - nothing
  */

 void loop()
 {
   int    temperatureValue = 0;
   float  currentTempVoltage = 0.0f;
   float  currentTemperature = 0.0f;

   // Read in the temperature value which will be in a range from 0 to 1023
   temperatureValue = analogRead(temperaturePin);

   // Convert our incoming voltage representation to a value we can utilize
   currentTempVoltage = ((float)temperatureValue * voltageReference) / maxSampleCount;

   // We now have the current temperature expressed in celsius
   currentTemperature = getTemperature(currentTempVoltage);

   // Print out the current temperature in both C and F
   Serial.print("The current temperature is: ");
   Serial.print(currentTemperature);
   Serial.print("°C which is ");
   Serial.print(convertTemperatureToF(currentTemperature));
   Serial.println("°F");

   // Rest for a second and check again
   delay(1000);
 } 
```

###### Constants

In the beginning of this sketch I have declared some constant values which I will use later on in my code. As I mentioned previously, it is better to declare these values as constant that way you get the benefit of meaningful names in your code which helps in the overall readability of your sketch along with the ability to change the value as needed later on without trying to find everywhere it is used in your code. It should be noted that you could also declare these values as defines which act as constants and are replaced in your code by the [Pre-processor](http://en.wikipedia.org/wiki/C_preprocessor) when you compile the code.

```
 const int temperaturePin = 0;
 const float baseVoltage = 2.730f; /* 2.730V at 0°C */
 const float voltageReference = 5.0f;
 const float maxSampleCount = 1023.0f;
 const float CtoFConversion = 9.0f / 5.0f;
 const float FtoCConversion = 5.0f / 9.0f;
 const float CtoFDelta = 32.0f;

 #define temperaturePin 	0
 #define baseVoltage 		2.730f /* 2.730V at 0°C */
 #define voltageReference 	5.0f
 #define maxSampleCount 	1023.0f
 #define CtoFConversion 	9.0f / 5.0f
 #define FtoCConversion 	5.0f / 9.0f
 #define CtoFDelta 			32.0f 
```

In the above code snippet, I have declared each variable as const indicating that the value will remain constant for the life of the application. Basically I am telling the compiler that I want to be able to read the value stored in the variable however I never want to change it during the lifetime of my application by writing to it. Given the type of values I am using, there is no reason to change them while the application is being executed. My main goal with these variables is to have human readable names assigned to the values so that my application is easier to understand. As shown in the second section, I could have also declared these constants using the #define pre-processor directive which would also make my code readable and maintainable. In doing so, however, I lose the type information of each of the values which may or may not be of interest to you the developer. On the flip side, the use of #define could reduce the amount of RAM that is used for your sketch.

Another thing you may have noticed is that for every variable of type float, I added an f to the end of the declaration. This is called a suffix which I tend to use on any value I assign to a float. By default, the compiler will consider a decimal value of type double and therefore convert the value from double to float when it builds the application from the sketch. For the Arduino® this isn't really a problem given float's and double's are the same thing. On systems where the double is indeed different, the compiler may generate a compilation error as it will appear that you are trying to assign a double value to a float variable. That would be the best case as you will at least get a chance to look at it and determine if there is a mistake in your code or not. Some compilers may automatically convert the value to float for you resulting in the possibility of a loss of precision.

###### Method Declarations

The next portion of my sketch consists of the method declarations or function prototypes as they would be named in the C language. These declarations inform the compiler of what methods will be available for use along with what types of variables are passed into the method when it is called along with the type of value that is returned if any. While technically you do not have to give the variables i.e. parameters names in the method declaration, it is good practice to do so in order for someone looking at the code to better understand the values being passed into the method. The only exception to this is the setup and loop methods which are declared for you outside of your sketch.

```
 float getTemperature(float temperatureVoltage);
 float convertTemperatureToF(float temperatureInCelsius);
 float convertTemperatureToC(float temperatureInFahrenheit); 
```

In this sketch, I have declared three methods that I may want to use. In the end I am only going to use two of them however I declared all three for completeness. Because I am going to be looking at values that change in the order of micro-volts, I will need a data type that can represent a decimal value such as a float. The first will convert the raw voltage reading into a temperature in celsius while the other two will convert temperatures between Fahrenheit and Celsius.

###### User Methods

The methods are declared above now appear in the code and this is where I will define what each method actually does. My end goal is that this code has enough comments to make it clear as to what its intended behavior is.

```
 /*
  * getTemperature - determines the temperature in celsius based on the
  *         incoming voltage value assuming 2.73v equals 0°C
  *
  * Params - temperatureVoltage - the incoming voltage representing the temperature
  *
  * Returns - float - the actual temperature in celsius based on the incoming voltage
  */

 float getTemperature(float temperatureVoltage)
 {
   float currentTemperature = 0.0f;

   // From the datasheet, every 10 mv is equal to 1 °K - 0°C is 273°K equal to 2.73v
   // Temperature is scaled by 100 to bring it into the celsius scale from kelvin
   currentTemperature = (temperatureVoltage - baseVoltage) * 100;

   return currentTemperature;
 } 
```

In the above code, I have a method, getTemperature which takes a temperature reading in volts and converts it to a temperature value in degrees celsius. I could just convert the value read in directly to Fahrenheit but not everyone is familiar with the Fahrenheit scale and Celsius is closer to the original value making debugging easier if the values look odd from the expected values. The raw temperature value is the value I will be reading from the analog input pin of the Arduino®. While I could keep it as a voltage reading, it will be easier to for me to relate to the value if it is in unit of measure that I am familiar with. In this case having it in a temperature unit is much easier then a raw voltage value.

```
 /*
  * convertTemperatureToF - converts the temperature from Celsius to Fahrenheit
  *
  * Params - temperatureInCelsius - the incoming temperature in Celsius
  *
  * Returns - float - the temperature expressed in Fahrenheit
  */

 float convertTemperatureToF(float temperatureInCelsius)
 {
   float convertedTemperature = 0.0f;

   convertedTemperature = (temperatureInCelsius * CtoFConversion) + CtoFDelta;

   return convertedTemperature;
 } 
```

This method converts a temperature in Celsius to Fahrenheit.

```
 /*
  * convertTemperatureToC - converts the temperature from Fahrenheit to Celsius
  *
  * Params - temperatureInCelsius - the incoming temperature in Fahrenheit
  *
  * Returns - float - the temperature expressed in Celsius
  */

 float convertTemperatureToC(float temperatureInFahrenheit)
 {
   float convertedTemperature = 0.0f;

   convertedTemperature = (temperatureInFahrenheit - CtoFDelta) * FtoCConversion;

   return convertedTemperature;
 } 
```

This method converts a temperature in Fahrenheit to Celsius.

###### Setup

Again, the setup method is where I will configure my Arduino® to operate as I need. In this case I will want to set the analog reference voltage to the default which in the case of the Arduino® UNO or the Arduino® MEGA, will be 5.0v. This informs the micro-controller I want to measure voltages in the range of 0v to 5.0v. For our purposes, this resolution will be fine.

```
 void setup()
 {
   analogReference(DEFAULT);
   Serial.begin(9600);
 } 
```

So what do I mean regarding resolution? Well the analog to digital converter in the Atmel® micro-controller has 10 bits of data for precision. For a 5.0v voltage range, this means that there will be 5.0v / 1024 or 0.0048828125 volts per step of the analog to digital converter. For each increment of the analog to digital converter, the voltage that it represents increases by 0.0048828125 volts. I have also configured my serial port here so I can write sample data out to my development system to verify that the data looks appropriate.

###### Loop

The loop method once again is where all of the real work is done. Here I am also using comments in the code to explain what everything is doing so the next person looking at this code can understand it without any assistance from me.

```
 void loop()
 {
   int    temperatureValue = 0;
   float  currentTempVoltage = 0.0f;
   float  currentTemperature = 0.0f;

   // Read in the temperature value which will be in a range from 0 to 1023
   temperatureValue = analogRead(temperaturePin);

   // Convert our incoming voltage representation to a value we can utilize
   currentTempVoltage = ((float)temperatureValue * voltageReference) / maxSampleCount;

   // We now have the current temperature expressed in celsius
   currentTemperature = getTemperature(currentTempVoltage);

   // Print out the current temperature in both C and F
   Serial.print("The current temperature is: ");
   Serial.print(currentTemperature);
   Serial.print("°C which is ");
   Serial.print(convertTemperatureToF(currentTemperature));
   Serial.println("°F");

   // Rest for a second and check again
   delay(1000);
 } 
```

The first thing that is done is to read in the current temperature value in volts as a digital representation. Once a value has been read, it can then be converted for display to the end user. In the above code, I first convert the temperature from a digital representation to an actual temperature. Given the LM335 is designed to be sensitive to 1°Kelvin which represents 10 milli-volts (mV) for each one degree Kelvin of change, I will convert from the digital representation to a Celsius temperature value. So how did I go from Kelvin to Celsius? Kelvin has the same scale as Celsius however it starts at absolute zero and continues up on the same scale. With absolute zero being -273.0°C, I simply use this value to convert from Kelvin to Celsius. Once I have done that, I can then use one of my methods I declared above to convert from the Celsius value to Fahrenheit. Once I have my values in the units of measure that I want, I can then print them to the serial port for verification on my development system.

A sample of the output generated by this sketch is as follows:

```
 The current temperature is: 26.61C which is 79.90F
 The current temperature is: 26.12C which is 79.02F
 The current temperature is: 26.12C which is 79.02F
 The current temperature is: 26.12C which is 79.02F
 The current temperature is: 28.08C which is 82.54F
 The current temperature is: 29.05C which is 84.30F
 The current temperature is: 29.54C which is 85.17F
 The current temperature is: 28.56C which is 83.42F
 The current temperature is: 28.08C which is 82.54F
 The current temperature is: 27.59C which is 81.66F 
```

As you can see in the above data, my temperature readings are in the expected range i.e. room temperature or close to it depending on the room etc. Also you should note that I placed my finger on the device during the output display which is why the temperature started to rise and then began to fall once I removed my finger from the device. I did this to ensure that the circuit and code were working as expected. The only thing I have not done is to calibrate my temperature device to ensure it is reading the correct value. This is done by connecting the ADJ pin of the temperature sensor to a potentiometer and than fine tuning the input to the current room temperature.

![LM335 Temperature sensor circuit](images/00019.jpeg)

![Creative Commons - Attribution - Share Alike](images/00005.jpeg) Image created using: [Fritzing](http://fritzing.org/)

In the above circuit diagram you can see where I have placed a potentiometer attached to the ADJ input of the temperature sensor to allow me to calibrate it to the current room temperature. While not overly critical for what we are doing, having the ability to do this will be crucial when we want to use the same basic circuit to monitor temperatures with a suitable level of accuracy.

For analog inputs, that covers it for the most part. There are more fine details that could be discussed such as over voltage prevention, static electricity, etc. however as an introduction, I think we have the basics covered. One thing you may have noticed is that under tools, I mentioned a voltage meter however did not mention when it should be used. The voltage meter is one of those tools that I have handy whenever something doesn't look right. For sanity sake, I can use the voltage meter to ensure that I have wired my LM335 correctly and it is measuring a voltage in the general range I expect. Typical voltage meters are actually multimeters which can measure in addition to voltage, current and resistance. One such feature on my multimeter is the continuity check where I can ensure that I have wired things properly by checking two points and audibly verifying that I have continuity between them. So while I may mention that a voltage meter or multimeter is one of the tools recommended, I may not indicate when I use it. Basically it is one of those tools that you should have for whatever circumstances come up.

### Digital Input

For digital inputs, the Arduino® has a number of pins available to accomplish this. When we say digital input, we are referring to the micro-controller being able to recognize an incoming signal as either HIGH or LOW. For the devices we are looking at, this would be equivalent to zero (0) volts representing a LOW value and five (5) volts representing a HIGH* value. The main thing to remember with digital inputs is that the value to trigger either a HIGH or LOW is not exact. There is a range of values that will cause the input to be HIGH or LOW. The datasheet indicates that a LOW signal is anything from -0.5v through 1.5v when the micro-controller is powered by 5v. The datasheet also indicates that a HIGH signal is anything from 3.0v through 5.5v when the micro-controller is powered by 5v. The main thing to note is that any voltage between 1.5v and 3.0v will be undefined and should be avoided to prevent unexpected application execution. Using our last example, I am now going to create a circuit and sketch that will only trigger when the temperature reaches a certain value such as 80°F which would be 26.67°C.

* the Arduino® UNO runs on 5 volts hence the value when set to HIGH will be 5 volts. Other boards, such as the [Arduino Due](http://arduino.cc/en/Main/ArduinoBoardDue), run at a lower voltage such as 3.3v so the output voltage when set to HIGH will be equivalent to that lower voltage.

#### Temperature Comparison

First we will develop a circuit that will trigger when a certain temperature is reached. For this circuit, we will want it to trigger at 80°F which would be 26.67°C. Using what we know about the LM335, 0°C is equal to 2.73v and each 1°C increases the voltage by 10mV. If we divide the 26.67°C by 100 to get it into the 10mV range, we will see that we need a voltage increase from 0°C of 0.2667v. So our target voltage across the LM335 will be 2.9967v. Oddly enough this is almost enough voltage to trigger our digital input however due to the variations found in components, doing this would be problematic and result in flaky operation of our program and circuit. To overcome this, we will create a comparison circuit that will trigger the digital HIGH value in the required range which is above 3.0v.

##### Required Components

*   Arduino® Board
*   4.7K Ohm Resistor
*   (2) 10K Trim potentiometers
*   LM335 temperature sensor[[7](#part0012_split_001.html_Ref7)] or similar such as the NTE7225[[8](#part0012_split_001.html_Ref8)]
*   LM311 voltage comparator[[9](#part0012_split_001.html_Ref9)] or similar such as the NTE943M[[10](#part0012_split_001.html_Ref10)]

##### Tools

*   breadboard
*   jumper wires
*   voltage meter

##### Schematic

For this schematic we will be using the circuit from before however this time we will be using a voltage comparator to compare our temperature voltage with our target voltage. As noted above, our target is 2.9967v. First we will need to wire up a voltage dividing circuit. We will want to use a 4.7K Ohm resistor in series with a 10K potentiometer. This will allow us to adjust the voltage across the potentiometer to our target voltage. In order to fine tune the target voltage, we can do one of two things. First we can use the analog pin of our Arduino® to read in the voltage drop across our trim potentiometer. This will require a little coding but will work fine. The other option is to use a multimeter to monitor the voltage across the potentiometer and fine tune it using that reading. Either is fine depending on what tools you have available. This connection will be wired into the voltage comparator. For the second half of our circuit, will be connecting the LM335 temperature sensor into the other input of the voltage comparator which will trigger an input of HIGH when our target voltage is reached. It will drop back to LOW once the temperature cools down.![LM335 Temperature triggering circuit](images/00020.jpeg)

![Creative Commons - Attribution - Share Alike](images/00005.jpeg) Image created using: [Fritzing](http://fritzing.org/)

##### Software

The following is the code that is necessary to monitor the input signal to determine if our temperature reading is greater than our set point, and if so, take an appropriate action such as turning a fan on.

```
 /*
  * This circuit is designed to toggle between a HIGH signal and a LOW
  * based on the current temperature in the room.  The potentiometer
  * and the resistor are used to divide the 5v signal into two values
  * giving us the comparison we need to trigger the comparator output.
  * 2.73v is 0°C so to get the comparator to trigger we will want
  * to ensure that there is 2.73v + X across the potentiometer where
  * X is the temperature we want to toggle on.
  * The temperaturePin (now called setPointPin) will again read in the 
  * temperature however it will actually be the voltage across the 
  * potentiometer so we can use that as our setpoint.
  * The temperatureTogglePin will be used to determine if we are above
  * or below our target temperature.
  */        
 const int setPointPin = 0;
 const int temperatureTogglePin = 7;
 const float baseVoltage = 2.730f; /* 2.730V at 0°C */
 const float voltageReference = 5.0f;
 const float maxSampleCount = 1023.0f;
 const float CtoFConversion = 9.0f / 5.0f;
 const float FtoCConversion = 5.0f / 9.0f;
 const float CtoFDelta = 32.0f;

 /*
  * Method declarations
  */

 float getTemperature(float temperatureVoltage);
 float convertTemperatureToF(float temperatureInCelsius);
 float convertTemperatureToC(float temperatureInFahrenheit);

 /*
  * getTemperature - determines the temperature in celsius based on the
  *         incoming voltage value assuming 2.73v equals 0°C
  *
  * Params - temperatureVoltage - the incoming voltage representing the temperature
  *
  * Returns - float - the actual temperature in celsius based on the incoming voltage
  */

 float getTemperature(float temperatureVoltage)
 {
   float currentTemperature = 0.0f;

   // From the datasheet, every 10 mv is equal to 1 °K - 0°C is 273°K equal to 2.73v
   // Temperature is scaled by 100 to bring it into the celsius scale from kelvin
   currentTemperature = (temperatureVoltage - baseVoltage) * 100;

   return currentTemperature;
 }

 /*
  * convertTemperatureToF - converts the temperature from Celsius to Fahrenheit
  *
  * Params - temperatureInCelsius - the incoming temperature in Celsius
  *
  * Returns - float - the temperature expressed in Fahrenheit
  */

 float convertTemperatureToF(float temperatureInCelsius)
 {
   float convertedTemperature = 0.0f;

   convertedTemperature = (temperatureInCelsius * CtoFConversion) + CtoFDelta;

   return convertedTemperature;
 }

 /*
  * convertTemperatureToC - converts the temperature from Fahrenheit to Celsius
  *
  * Params - temperatureInCelsius - the incoming temperature in Fahrenheit
  *
  * Returns - float - the temperature expressed in Celsius
  */

 float convertTemperatureToC(float temperatureInFahrenheit)
 {
   float convertedTemperature = 0.0f;

   convertedTemperature = (temperatureInFahrenheit - CtoFDelta) * FtoCConversion;

   return convertedTemperature;
 }

 /*
  * Setup - main configuration point of our sketch to configure
  *         the Arduino for analog input
  *
  * Params - none
  *
  * Returns - nothing
  */

 void setup()
 {
   pinMode(temperatureTogglePin, INPUT);
   analogReference(DEFAULT);
   Serial.begin(9600);
 }

 /*
  * loop - main method which will be called each time the
  *        Arduino goes through its main loop to read the
  *        setPoint temperature value and check our digital
  *        input pin to see if it is high or not.
  *
  * Params - none
  *
  * Returns - nothing
  */

 void loop()
 {
    int    rawSetPointValue = 0;
    float  setPointVoltage = 0.0f;
    float  temperatureSetPoint = 0.0f;

    // Read in the temperature value which will be in a range from 0 to 1023
    rawSetPointValue = analogRead(setPointPin);

    // Convert our incoming voltage representation to a value we can utilize
    setPointVoltage = ((float)rawSetPointValue * voltageReference) / maxSampleCount;

    // We now have the current temperature expressed in celsius
    temperatureSetPoint = getTemperature(setPointVoltage);

    // Print out the current temperature in both C and F
    Serial.print("The temperature set point is: ");
    Serial.print(temperatureSetPoint);
    Serial.print("C which is ");
    Serial.print(convertTemperatureToF(temperatureSetPoint));
    Serial.println("F");

   if (digitalRead(temperatureTogglePin) == HIGH)
   {
    Serial.println("We have reached our set point.");
   }
   else
   {
    Serial.println("Set point has not been reached.");
   }
   // Rest for a second and check again
   delay(1000);
 } 
```

A significant amount of the code above is straight from the earlier example which will now be used to monitor the set point temperature and allow us to tweak the value as the program is executing. Once we have the set point established we can than vary the temperature that our LM335 is reading by holding our finger on it to warm it up or using a fan to cool it off. While I won't rehash everything that was done before, I will highlight the main differences that were made.

```
 const int setPointPin = 0;
 const int temperatureTogglePin = 7; 
```

I changed the the temperaturePin variable name to setPointPin which better describes what this constant variable is doing i.e. defining the pin on the Arduino® that we will read for the set point temperature. The second constant variable is temperatureTogglePin which is the pin on the Arduino® which we will monitor to detect if the LM335 has reached the setPoint or not.

```
 /*
  * Setup - main configuration point of our sketch to configure
  *         the Arduino for analog input
  *
  * Params - none
  *
  * Returns - nothing
  */

 void setup()
 {
   pinMode(temperatureTogglePin, INPUT);
   analogReference(DEFAULT);
   Serial.begin(9600);
 } 
```

The next major change is in the setup method where I am now configuring the temperature toggle pin to be a digital input pin. The method, pinMode, instructs the Arduino® to configure this pin for digital input data. Remember that most pins on the Atmel® micro-controller, which is what the Arduino® utilizes, can be configured to perform a number of disparate functions. In order to use these functions, we must ensure the micro-controller is configured properly before we start running our code.

```
 /*
  * loop - main method which will be called each time the
  *        Arduino goes through its main loop to read the
  *        setPoint temperature value and check our digital
  *        input pin to see if it is high or not.
  *
  * Params - none
  *
  * Returns - nothing
  */

 void loop()
 {
    int    rawSetPointValue = 0;
    float  setPointVoltage = 0.0f;
    float  temperatureSetPoint = 0.0f;

    // Read in the temperature value which will be in a range from 0 to 1023
    rawSetPointValue = analogRead(setPointPin);

    // Convert our incoming voltage representation to a value we can utilize
    setPointVoltage = ((float)rawSetPointValue * voltageReference) / maxSampleCount;

    // We now have the current temperature expressed in celsius
    temperatureSetPoint = getTemperature(setPointVoltage);

    // Print out the current temperature in both C and F
    Serial.print("The temperature set point is: ");
    Serial.print(temperatureSetPoint);
    Serial.print("C which is ");
    Serial.print(convertTemperatureToF(temperatureSetPoint));
    Serial.println("F");

  if (digitalRead(temperatureTogglePin) == HIGH)
   {
    Serial.println("We have reached our set point.");
   }
   else
   {
    Serial.println("Set point has not been reached.");
   }
   // Rest for a second and check again
   delay(1000);
 } 
```

In the main loop of our sketch, I have changed the name of a number of variables to better describe their function. I have also added in code to read the state of the temperature toggle pin to determine if we have reached our set point or not. This is done by calling the aptly named digitalRead method. This method takes one argument which is the value of the pin to be read. It will return either a HIGH or LOW value depending upon the voltage being read at the input pin of the device. For now I am simply displaying that I have either reached the set point or not. Later on we can take additional actions to do something a little more useful with this information. We will also look at another form of digital input when working with [interrupts](#part0006_split_001.html_temptrigger) later on.

### Summary

The Arduino® provides pins to read in both analog and digital data. The analog data can be any signal such as a temperature reading, photo-resistor, or any other such item that provides a range of values based on an environmental stimulus. Digital inputs can be used to determine button presses, on and off states, and other binary types of data. Together, both of these types of inputs can be used to monitor the world around us and allow us to react to events when they occur.

![chapter end graphic](images/00001.jpeg)

# Output

## what goes in must come out

Previously we looked at some of the inputs that the Arduino® can process. Now we will look at the other side which is outputs. So what kind of signals can the Arduino® output? Here is a summary of them.

Analog *

A variable value based on how the output is configured within the micro-controller

Digital

A signal that can be either HIGH or LOW

Timer

A signal, HIGH or LOW, is generated when a timer reaches a certain point

* The Atmel® micro-controller that we are using on the Arduino® doesn't actually output a true analog signal but instead uses a feature called pulse width modulation (PWM) to create an analog output value. For a true analog output, we would need to wire up a digital to analog converter [DAC](http://en.wikipedia.org/wiki/Digital-to-analog_converter) to do the conversion for us. Also note that while the micro-controller that we are using doesn't have a DAC built into it, there are other micro-controllers that do have this functionality such as the micro-controller found on the Arduin® Due.

### Analog Output

The Arduino® UNO supports analog outputs in the form of PWM. This is not a true analog output but more a percentage of a signal that remains HIGH for a portion of a period of time and LOW for the remainder. For the Atmel® chip found on the Arduino® UNO, there are two forms of PWM, Fast PWM and Phase correct PWM. In general, the fast PWM will look like a sawtooth where the output rises from the starting value, zero (0), up to the top value and then dropping abruptly back to zero (0). The phase correct PWM will rise up like the fast PWM however it will then count back down from the top value back to zero (0) opposed to the abrupt drop resulting in a better output waveform. This output is passed through a comparator circuit to make it more of a square wave on the output. For a lot of the devices we will encounter, this type of output will be fine however it is good to note that it isn't a true analog output such as that a DAC would bring.

The Arduino® combines the analog outputs on the some of the same pins as the digital outputs which is why it is a very good idea to plan your designs accordingly up front to minimize potential issues later on in your design. The reason behind this, is that the Atmel® micro-controller packs a significant amount functionality into a small package. The resulting package only has so many physical pins to the outside world resulting in overlap between certain functions. For the most part, if you are using your micro-controller to do a specific task, this will not be an issue. When you start getting into more complicated designs then you may find that this overlapping of features becomes an obstacle that you will have to overcome one way or another.

So what good is this type of analog output? In general, this is a fine output which can be used to drive the brightness of LED's, motors, servos's and a number of other items. For LED's, the length of time that the output signal remains HIGH correlates to the brightness of the LED in some implementations. The same would hold true for basic motors where the length of time that the output signal is HIGH translates to the speed of that the motor runs at. For servo's, the length of time that the output signal remains HIGH may correlate to the direction that the servo turns. All of these are useful applications which we will look into in more detail as we proceed.

#### Pulse Width Modulation - LED's

The first project will be to read in a temperature value and then turn on a tricolor LED to represent the temperature visually. To do this we will need to re-use our circuit from before with the LM335 to measure the current temperature and then will add to it a tricolor LED to represent that temperature value. For the tricolor LED that we are going to utilize, it doesn't come with any PWM support so we will use some of our Arduino® PWM outputs to accomplish this. There are some lengthy strips of LED's that can be found on the internet that have PWM support built into them. These can be interfaced through other means such as SPI which we will cover in the [Communications](#part0007_split_000.html_Communications) chapter.

##### Required Components*

*   Arduino® Board
*   (4) 4.7K Ohm Resistor
*   (3) 470 Ohm Resistors
*   (3) 2N2222(A) PNP Transistor
*   LM335 temperature sensor[[7](#part0012_split_001.html_Ref7)] or similar such as the NTE7225[[8](#part0012_split_001.html_Ref8)]
*   Tricolor LED

* The part list includes those parts required for the temperature reading circuit along with the parts for the additional components used in this circuit.

##### Tools

*   breadboard
*   jumper wires
*   voltage meter
*   Canned air *
*   hair dryer or heat gun *

* I added canned air and hair dryer to the tools portion of the above list as they can be used to quickly cool down or heat up the temperature sensor. They are not required, just convenient.

##### Schematic

In this circuit, you will need to connect the ground and +5v signals from the Arduino® over to the TRI-Color LED. Each of the LED connections will utilize a NPN transistor in line to control current flow through the LED. Each transistor consists of a base, collector, and emitter. The collector for each transistor will be connected to the LED pin for each individual color. The base of each transistor will be connected to a PWM output of the Arduino® which will be used to vary the intensity of the LED it is connected to. A 4.7K resistor will be used inline between the Arduino® outputs and the base of each transistor. Finally the emitter of each transistor will be connected to ground through a 470 Ohm resistor. For the temperature input side of this we will again utilize the circuit we created in the previous chapter, [Temperature Reading](#part0004_split_001.html_TempReading), using an analog input to read the temperature.

![Tri-color LED circuit](images/00021.jpeg)

![Creative Commons - Attribution - Share Alike](images/00005.jpeg) Image created using: [Fritzing](http://fritzing.org/)

##### Software

The following code incorporates the analog reading for the temperature sensor and adds in the code to drive the LED.

```
 /*
 * The temperature pin is where the input from the LM335 will be read from.
 *
 * The redLedPin is the where the PWM output of the Arduino will connect to
 * the circuit.
 *
 * The greenLedPin is the where the PWM output of the Arduino will connect to
 * the circuit.
 *
 * The blueLedPin is the where the PWM output of the Arduino will connect to
 * the circuit.
 *
 * The base voltage is what the device (LM335) will measure at 0°C
 * The voltage reference is the max voltage that can be read in on the
 * analog input pin
 * The max sample count is the highest value that could be read in on the
 * analog input pin which will equal the voltage reference
 *
 */        
const int temperaturePin = 0;
const int redLedPin = 9;
const int greenLedPin = 10;
const int blueLedPin = 11;
const float baseVoltage = 2.730f; /* 2.730V at 0°C */
const float voltageReference = 5.0f;
const int maxSampleCount = 1023;

/*
 * Method declarations
 */

     /* No additional methods in this sketch */

/*
 * Setup - main configuration point of our sketch to configure
 *         the Arduino for analog input and PWM output
 *
 * Params - none
 *
 * Returns - nothing
 */ 

void setup()
{
  analogReference(DEFAULT);

  // Because we are using digital pins as analog outputs i.e. PWM
  // we do not need to configure them using pinMode.
}

 /*
 * loop - main method which will be called each time the
 *        Arduino goes through its main loop to read the
 *        current temperature value and then turn on the
 *        three LED's based on the value of said temperature
 *
 * Params - none
 *
 * Returns - nothing
 */
void loop()
{
  int temperatureValue = 0;
  int red = 0;
  int green = 0;
  int blue = 0;
  float colorPercent = 0.0f;

  // Read in the temperature value which will be in a range from 0 to 1023
  temperatureValue = analogRead(temperaturePin);

  // The closer we are to 0, the bluer it will be
  colorPercent = 100.0f - (((float)temperatureValue / (float)maxSampleCount) * 100.0f);
  blue = (int)(colorPercent * 255.0f);

  // The closer to 1023 i.e. max of device, the redder it will be
  colorPercent = ((float)temperatureValue / (float)maxSampleCount) * 100.0f;
  red = (int)(colorPercent * 255.0f);

  // And green will vary accordingly peeking @ midpoint
  if (temperatureValue > (maxSampleCount / 2))
  {
    colorPercent = (float)(maxSampleCount - temperatureValue) * 100.0f;
  }
  else
  {
    colorPercent = ((float)temperatureValue / (float)(maxSampleCount / 2)) * 100.0f;
  }
  green = (int)(colorPercent * 255.0f);

  analogWrite(redLedPin, red);
  analogWrite(greenLedPin, green);
  analogWrite(blueLedPin, blue);

  // Rest for a second and check again
  delay(1000);
} 
```

###### Constants

In the beginning of this sketch I have declared some constant values which I will use later on in my code. As I mentioned previously, it is better to declare these values as constant that way you get the benefit of meaningful names in your code which helps in the overall readability of your sketch along with the ability to change the value as needed later on without trying to find everywhere it is used in your code.

###### Method Declarations

For this sketch, we do not have any user specific methods to declare.

###### User Methods

Given we do not have any user method declarations, we also do not have any user method implementations to look at.

###### Setup

The setup method is where I will configure my Arduino® to operate as I need. In this case I will want to set the analog reference voltage to the default which in the case of the Arduino® UNO or the Arduino® MEGA, will be 5.0v. This informs the micro-controller I want to measure voltages in the range of 0v to 5.0v. For our purposes, this resolution will be fine.

```
 void setup()
 {
   analogReference(DEFAULT);

   // Because we are using digital pins as analog outputs i.e. PWM
   // we do not need to configure them using pinMode.
 } 
```

###### Loop

The loop method once again is where all of the real work is done. It is here that I will read the temperature value periodically and update the color of the TriColored LED to match the temperature that was read in. As noted in the code above, we do not have to call pinMode for each of the analog output pins.

```
 void loop()
{
  int temperatureValue = 0;
  int red = 0;
  int green = 0;
  int blue = 0;
  float colorPercent = 0.0f;

  // Read in the temperature value which will be in a range from 0 to 1023
  temperatureValue = analogRead(temperaturePin);

  // The closer we are to 0, the bluer it will be
  colorPercent = 100.0f - (((float)temperatureValue / (float)maxSampleCount) * 100.0f);
  blue = (int)(colorPercent * 255.0f);

  // The closer to 1023 i.e. max of device, the redder it will be
  colorPercent = ((float)temperatureValue / (float)maxSampleCount) * 100.0f;
  red = (int)(colorPercent * 255.0f);

  // And green will vary accordingly peeking @ midpoint
  if (temperatureValue > (maxSampleCount / 2))
  {
    colorPercent = (float)(maxSampleCount - temperatureValue) * 100.0f;
  }
  else
  {
    colorPercent = ((float)temperatureValue / (float)(maxSampleCount / 2)) * 100.0f;
  }
  green = (int)(colorPercent * 255.0f);

  analogWrite(redLedPin, red);
  analogWrite(greenLedPin, green);
  analogWrite(blueLedPin, blue);

  // Rest for a second and check again
  delay(1000);
} 
```

The first thing we do in the loop method is to declare some variables to be used during the operation of the loop. The first one is the temperature value which will be read from the analog to digital converter pin. Following that is our potential color values based on the read in temperature value. Finally we have the color percentage variable which is of type float to handle the percentage calculations for each color.

```
 // Read in the temperature value which will be in a range from 0 to 1023
  temperatureValue = analogRead(temperaturePin); 
```

In the above code, we are reading in the current temperature value from the pin we have defined as temperaturePin. Once we know what the current temperature is, we can then calculate how much of the three colors we want to turn on.

```
 // The closer we are to 0, the bluer it will be
  colorPercent = 100.0f - (((float)temperatureValue / (float)maxSampleCount) * 100.0f);
  blue = (int)(colorPercent * 255.0f);

  // The closer to 1023 i.e. max of device, the redder it will be
  colorPercent = ((float)temperatureValue / (float)maxSampleCount) * 100.0f;
  red = (int)(colorPercent * 255.0f);

  // And green will vary accordingly peeking @ midpoint
  if (temperatureValue > (maxSampleCount / 2))
  {
    colorPercent = (float)(maxSampleCount - temperatureValue) * 100.0f;
  }
  else
  {
    colorPercent = ((float)temperatureValue / (float)(maxSampleCount / 2)) * 100.0f;
  }
  green = (int)(colorPercent * 255.0f); 
```

In the above code we determine what percentage of the color should be shown i.e. how intense the color should be. For this sketch, I have decided to make the color more blue as we get closer to a zero (0) reading and more red as we get closer to the maximum value of the analog to digital converter (ADC). For the green channel I am increasing the intensity as the value goes from 0 to the midpoint of the total range of the ADC. Once the midpoint of the total range has been hit, I will then decrease the percentage. Finally after I have calculated how intense each of the LED's should be, I will write out the values to each of the PWM pins that connect to the corresponding LED's.

```
 analogWrite(redLedPin, red);
  analogWrite(greenLedPin, green);
  analogWrite(blueLedPin, blue); 
```

This code is fairly straight forward in that each value for red, blue, and green is written out to the corresponding pins which results in turning on the transistor connected to the LED channel for that given color. The value we write out is the amount of time during the time period of the PWM signal that it will be HIGH with the remainder of the time with the signal being LOW. What I haven't mentioned so far is how long is this time overall? From the Arduino® documentation, we can see that the overall frequency of the PWM signal is approximately 490 Hz. The Hz acronym stands for hertz which is the frequency of the signal i.e. the number of times the signal varies from low to high for one complete second. Basically a single hertz is equal to one second. The overall time of the signal is one (1) second divided by the number of hertz. In our case this is 1 divided by 490, resulting in 0.00204081632653 seconds per cycle. In normalized terms, the cycle of the PWM signal is approximately 2 milliseconds. If you were to write a value of 127 out to the analog output pin, you would get a near perfect square wave out of the pin with it being HIGH half the time i.e. for 1 millisecond and then LOW for the remainder of the period i.e. the second millisecond. A value of 64 which is one quarter of the total value for the PWM signal would result in a HIGH signal for 500 microseconds followed by 1500 microseconds of a LOW signal.

Once you have your circuit built and ready to test with the provided sketch, you can heat and/or cool the LM335 to see the TriColor LED change. Given the space between each pixel of the TriColor LED being as small as it is, when we look at the LED as a whole, we will see the combined color of each individual segment opposed to three distinct colors. This is also due in part to the opaque housing around the LED causing the colors to blend. The final part of the code is the delay method which is again being utilized to let things happen before checking the analog input for a new temperature reading. Later on, when looking at [Interrupts](#part0006_split_000.html_Interupt), we will see how we can remove the delay and be more reactive to outside stimuli opposed to continuously monitoring the values.

#### Pulse Width Modulation - Fans

Now that we have a handle on PWM, I will look at other ways to utilize it. For this circuit, I will use a potentiometer connected to an analog input which will control the speed of the fan connected to a PWM output. The goal is to adjust the speed of the fan based on the analog input read in from the potentiometer. For practical uses, I would most likely put a temperature sensor on the analog input in order to adjust the fan based on the current temperature. However for this example, I will simply utilize the potentiometer to better exercise the fan from off to full on.

*   Arduino® Board
*   10K potentiometer
*   2N2222(A) Transistor
*   100 Ohm Resistor
*   1K Ohm Resistor
*   150 Ohm Resistor
*   Fan, +12v, 200mAmp

##### Tools

*   breadboard
*   jumper wires
*   voltage meter

##### Schematic

The fan connects to the board using a four (4) pin header. A three (3) pin fan can also be used however it will not have the ability to be controlled via a PWM output pin unless you hook this value up to a transistor such as Q1 in the diagram below. The voltage for the fan should be applied to the resistor on the top of the board to flow into the transistor. This assumes of course that the fan you are using is designed to run off of +12v. If you are using the four (4) pin fan type then you will want to change the yellow wire from the transistor to connect to the +12v voltage input for the fan, bypassing the transistor all together. The main thing to note is to not connect the fan power to the Arduino® as it may overload the Arduino® circuit board and damage it. You will also need to consider the current draw, Ic, to ensure it doesn't overload the transistor. For the transistor specified, the maximum current, Ic, is 1.0 Amps.

![Fan control circuit](images/00022.jpeg)

![Creative Commons - Attribution - Share Alike](images/00005.jpeg) Image created using: [Fritzing](http://fritzing.org/)

##### Software

The following code is used to read in the voltage across the potentiometer and in turn write out to the PWM pin in order to control the speed of the fan.

```
 /*
 * FanPWM - the purpose of this sketch is to read in a value from a potentiometer and then
 *          use that value to determine how fast the fan should be spinning.
 *
 * The fan control pin is where the input from the potentiometer will be read from.
 *
 * fanTachPin is connected to read in the current speed of the fan
 *
 * The fan speed pin is the where the PWM output of the Arduino will connect to
 * the interface circuit in order to drive the fan.
 *
 * The voltage reference is the max voltage that can be read in on the
 * analog input pin
 *
 * The max sample count is the highest value that could be read in on the
 * analog input pin which will equal the voltage reference
 */

const int fanControlPin = 0;
const int fanTachPin = 7;
const int fanSpeedPin = 9;
const float voltageReference = 5.0f;
const int maxSampleCount = 1023;

/*
 * Method declarations
 */

/* No additional methods in this sketch */

/*
 * Setup - main configuration point of our sketch to configure
 *         the Arduino for analog input and PWM output
 *         also set up the tach pin for input along with
 *         enabling the serial port to monitor fan speed
 *
 * Params - none
 *
 * Returns - nothing
 */

void setup()
{
  analogReference(DEFAULT);

  pinMode(fanTachPin, INPUT);

  Serial.begin(9600);
}

/*
 * loop - main method which will be called each time the
 *        Arduino goes through its main loop to read the
 *        current fan control value and then turn on the
 *        fan based on the voltage across the potentiometer
 *
 * Params - none
 *
 * Returns - nothing
 */

void loop()
{
  int fanControlValue = 0;
  int fanSpeed = 0;
  int fanTach = 0;

  // Read in the temperature value which will be in a range from 0 to 1023
  fanControlValue = analogRead(fanControlPin);

  // Our range for output for PWM is 0 to 255 so we will divide by
  // 4 in order to get the read in value into the proper range
  // the output pin expects.
  fanSpeed = fanControlValue / 4;

  analogWrite(fanSpeedPin, fanSpeed);

  // Read in the fan tachometer value which will be a high signal
  // for a period X
  fanTach = pulseIn(fanTachPin, HIGH);

  char buffer[256];
  int rpm = 1000000 / fanTach; // 1 Million as the value is in microseconds

  // Target and tach shouldn't be expected to be the same
  sprintf(buffer, "Target: %d, Tach: %d", fanSpeed, rpm);

  Serial.println(buffer);

  // Rest for a second and check again
  delay(1000);
} 
```

###### Constants

In the beginning of this sketch I have declared some constant values which I will use later on in my code. As I mentioned previously, it is better to declare these values as constant that way you get the benefit of meaningful names in your code which helps in the overall readability of your sketch along with the ability to change the value as needed later on without trying to find everywhere it is used in your code. The constants in this sketch define which pins are being used as analog and digital input, and which pin is being used for analog out i.e. PWM output.

###### Method Declarations

There are not any additional methods declared for this sketch.

###### Setup

The setup method is where I will configure my Arduino® to operate as I need. For this sketch we will ensure that our analog reference voltage is five (5) volts.

```
 void setup()
{
  analogReference(DEFAULT);

  pinMode(fanTachPin, INPUT);

  Serial.begin(9600);
} 
```

In addition to the analog reference we will also set the fanTachPin as a digital input which is much like we have done before however there will be a slight twist in how we use it. Finally the serial port is started and set for 9600 baud. This will allow us to observe the speed of the fan that is being read.

###### Loop

As before, the loop method is where all of the work is done. In this case we will be reading in a value from a potentiometer and writing out a value to the fan which represents how fast the fan should be spinning. In addition we will be reading in the pulse width of the fan tachometer pin and presenting that as a speed to the serial port interface.

```
 void loop()
{
  int fanControlValue = 0;
  int fanSpeed = 0;
  int fanTach = 0;

  // Read in the temperature value which will be in a range from 0 to 1023
  fanControlValue = analogRead(fanControlPin);

  // Our range for output for PWM is 0 to 255 so we will divide by
  // 4 in order to get the read in value into the proper range
  // the output pin expects.
  fanSpeed = fanControlValue / 4;

  analogWrite(fanSpeedPin, fanSpeed);

  // Read in the fan tachometer value which will be a high signal
  // for a period X
  fanTach = pulseIn(fanTachPin, HIGH);

  char buffer[256];
  int rpm = 1000000 / fanTach; // 1 Million as the value is in microseconds

  // Target and tach shouldn't be expected to be the same
  sprintf(buffer, "Target: %d, Tach: %d", fanSpeed, rpm);

  Serial.println(buffer);

  // Rest for a second and check again
  delay(1000);
} 
```

The voltage is read in from the fan control pin and converted to a value that is proper for our PWM output. The input range is from 0 to 1023 while the output can only be from 0 to 255\. Because of this, I will scale the incoming value by dividing the value read by four (4). Once we have converted our value, we will then write that speed out to set the fan for that speed. Note that the actual value written will not be an actual speed but a value from 0 to 255\. The fan most likely will turn off well before we reach the lowest value i.e. 0 and will turn on when not zero (0). The reason for this is that it takes a bit of voltage in order to actually switch on the transistor and depending on what components that you use along with which fan and what voltage you select. Once the value has been written to the fan speed pin, I will read in the value from the tachometer in order to determine the speed that the fan is rotating.

```
 // Read in the fan tachometer value which will be a high signal
  // for a period X
  fanTach = pulseIn(fanTachPin, HIGH); 
```

For this sketch, I have included a new input method for digital pins. This is the pulseIn method which is designed to read in the length of either a HIGH or LOW signal. This method will return a value representing the amount of time a pulse was either HIGH or LOW. This value will represent the number of microseconds that the pulse endured. In the above example, I am measuring how long the pulse is HIGH in order to determine the rotational speed of the fan. The return value from the pulseIn method is in microseconds. So our rotations will be one divided by the number of microseconds. I was reading around 500 microseconds on my display which puts us at an RPM of around 2000 which is inline with what I would expect based on the documentation for the fan.

Once we know what the rotational speed is of the fan, we will display the target speed and tachometer value to the user. Following this we will sleep for one (1) second before checking the potentiometer again and adjusting the fan speed accordingly. You might notice that the fan tach is not stable and can rise and fall quite significantly. We will rectify this in the chapter regarding [Interrupts](#part0006_split_001.html_fantach).

This type of circuit would be similar to what your mother board in your computer might do in terms of controlling the CPU temperature. Basically the system will want to measure the current temperature of the CPU and increase the fan speed if it is getting above a certain point and decrease it when it drops back down to a certain threshold. If we were to take our circuit from the chapter on [Inputs](#part0004_split_002.html_temptrigger) and add the fan interface to that circuit, we could turn the fan on whenever the temperature reached our set point.

#### Pulse Width Modulation - Servos

The last area we will look at is a servo which we can control to perform some type of work. Servos are used for controlling robotic arms and can also be used for steering remote controlled cars among other things.

*   Arduino® Board
*   4.7K Ohm Resistor
*   LED
*   +5v DC power supply
*   5v servo such as this [LS-3006](http://www.frys.com/product/7027261)

##### Tools

*   breadboard
*   jumper wires
*   voltage meter

##### Schematic

![Motor circuit](images/00023.jpeg)

![Creative Commons - Attribution - Share Alike](images/00005.jpeg) Image created using: [Fritzing](http://fritzing.org/)

The above drawing shows the servo attached to the Arduino® with the control signal connected to pin 11 which is a PWM output pin. The main thing to note is that I am connecting the servo to the Arduino® Vin pin. It is very important to connect the servo to this pin and NOT the +5v pin. This also requires that you connect a +5v DC power supply to the Arduino®. The reason for this is that the servo will draw more current then is safe for the Arduino® pins to supply. By connecting it to the Vin pin, you will be using the DC power supply to provide current to the servo and protecting your Arduino® from potential harm. This also means that you shouldn't use just the USB port as your power supply as it will supply around 500 milliamps maximum which will probably not be enough for both the servo and the Arduino® board.

##### Software

The following code is used to control the servo. The main goal is to be able to turn the servo both forward and backward. Another thing to note is that servo's come in a variety of formats. Some will turn full circle while others may only turn a certain amount. The one I have, the LS-3006, is able to turn a full 360 degrees.

```
 /*
 * ServoPWM - the purpose of this sketch is to control a servo in order to do some work.
 *            the led is used to indicate which direction the servo is going with it being
 *            off when the servo is going forward and on when it is going backward.
 *
 * The ledPin is used to drive the LED to turn it on or off.
 *
 * The servoPin is used to drive the servo motor.
 *
 */	        
const int ledPin = 8;
const int servoPin = 11;

/*
 *  The frequency of the arduino PWM signal is around 490 Hz
 *  This translates into 2 milliseconds per cycle.
 */

const int pwmFrequency = 490;

typedef enum
{
  FORWARD = 0,
  BACKWARD = 1
} eDirection;

eDirection servoDirection = FORWARD;

/*
 * Motor speeds for the LS-3006
 * which are defined in microseconds.
 */

typedef enum
{
  FORWARD_SPEED = 128,  // (1000 microseconds) which is equal to half of our cycle
  BACKWARD_SPEED = 250, // (2000) microseconds which is basically the full cycle
  NEUTRAL_SPEED = 192,  // (1500 microseconds) which is equal to three quarters of the cycle
} eMotorSpeed;

eMotorSpeed motorSpeed = FORWARD_SPEED;

/*
 * Method declarations
 */

/* No additional methods in this sketch */

/*
 * Setup - main configuration point of our sketch to configure
 *         the Arduino for PWM output
 *
 * Params - none
 *
 * Returns - nothing
 */

void setup()
{
  pinMode(ledPin, OUTPUT);  
}

/*
 * loop - main method which will be called each time the
 *        Arduino goes through its main loop to change the
 *        direction of the servo
 *
 * Params - none
 *
 * Returns - nothing
 */

void loop()
{
  // Set our LED to the proper state based on the direction
  if (servoDirection == FORWARD)
  {
    motorSpeed = FORWARD_SPEED;
    digitalWrite(ledPin, LOW);
    servoDirection = BACKWARD;  // set it for next time
  }
  else
  {
    motorSpeed = BACKWARD_SPEED;
    digitalWrite(ledPin, HIGH);
    servoDirection = FORWARD;  // set it for next time
  }

  analogWrite(servoPin, motorSpeed);

  // Rest for a second and then change directions
  delay(1000);
} 
```

###### Constants

Constants. What would we do without them? So I have again declared a few as follows:

```
 const int ledPin = 8;
const int servoPin = 11; 
```

This just defines the pin which the LED is to be connected to along with the pin which will drive the signal (PWM) to the servo.

```
 const int pwmFrequency = 490;

typedef enum
{
  FORWARD = 0,
  BACKWARD = 1
} eDirection;

eDirection servoDirection = FORWARD; 
```

In this section I have declared what the frequency of the PWM signal will be i.e. how often it will cycle from on to off. I have also defined an [enumeration](http://en.wikipedia.org/wiki/Enumerated_type) to indicate when the servo is moving forward or backward i.e. clockwise or counter-clockwise.

```
 typedef enum
{
  FORWARD_SPEED = 128,  // (1000 microseconds) which is equal to half of our cycle
  BACKWARD_SPEED = 250, // (2000) microseconds which is basically the full cycle
  NEUTRAL_SPEED = 192,  // (1500 microseconds) which is equal to three quarters of the cycle
} eMotorSpeed;

eMotorSpeed motorSpeed = FORWARD_SPEED; 
```

The above definitions are the most important in this sketch as they define the values to be sent to the PWM control pin to represent the signals to control the direction of the servo.

###### Method Declarations

There are not any additional methods declared for this sketch.

###### Setup

The setup method is where I will configure my Arduino® to operate as I need. For this sketch the only pin to configure is the pin connected to the onboard LED which will be declared as an output.

```
 void setup()
{
  pinMode(ledPin, OUTPUT);  
} 
```

This code will set the ledPin to act as an output signal. This will allow us to control the LED to indicate the direction of the servo.

###### Loop

As before, the loop method is where all of the work is done. For this sketch we are toggling the direction of the servo every second from forward to backward. While this code isn't really useful, the idea is to show how it could be used. The applications for this type of circuit are endless however it would be a really good fit for a robotic arm or perhaps a conveyor belt where you need a little more torque and not necessarily the speed.

```
 void loop()
{
  // Set our LED to the proper state based on the direction
  if (servoDirection == FORWARD)
  {
    motorSpeed = FORWARD_SPEED;
    digitalWrite(ledPin, LOW);
    servoDirection = BACKWARD;  // set it for next time
  }
  else
  {
    motorSpeed = BACKWARD_SPEED;
    digitalWrite(ledPin, HIGH);
    servoDirection = FORWARD;  // set it for next time
  }

  analogWrite(servoPin, motorSpeed);

  // Rest for a second and then change directions
  delay(1000);
} 
```

For this circuit, we are just moving the servo forward and backward using the PWM signals from the Arduino®. The LED pin is used to indicate which direction the servo should be moving in i.e. forward or backward. This is useful to ensure that the device is operating as expected as it is sometimes difficult to see which direction the servo is going depending on its speed. To make this really useful, I would use an input to trigger an action such as a proximity sensor where I would stop the servo from moving when the proximity sensor was triggered.

### Digital Output

The Arduino® supports a number of digital outputs that are capable of producing either a HIGH or LOW signals representing five (5) volts and zero (0) volts accordingly. So where are digital output's used? In one case you could use them as an electronic switch to activate an external circuit such as an LED to indicate something is currently active such as a power on LED. Of course it could also be used for the reverse where the LED comes on when the power to the main board is lost or the like. When a number of the digital outputs are used in conjunction with each other, they can be used to interface with external devices such as LCD's and other wide data path devices.

#### Power On LED

For our first look at digital outputs, we will create a simple power on circuit that will light up a LED when the system has reached an operating state. I am going to utilize a tricolor LED in order to have state information. The LED will be red when the board is powered down, yellow when the board is booting up, and finally green when the board is functional.

*   Arduino® Board
*   (3) 470 Ohm Resistor
*   (2) 4.7K Ohm Resistor
*   (2) 2N2222(A) Transistor
*   tricolor LED
*   3.0 v battery

##### Tools

*   breadboard
*   jumper wires
*   voltage meter

##### Schematic

In this circuit, I am going to utilize an external battery that will turn on the RED channel of the tricolor LED when there isn't any power to the Arduino®. Once the board starts powering up, we will turn the LED to YELLOW, and then finally we will turn it to GREEN once we enter our LOOP method. The main thing to note is that we need to connect the battery ground terminal to the ground pin on our Arduino® in order to establish a common ground amongst our components. For this circuit, the lack of signal coming from the Arduino® digital output pin will result in the LED being lit up RED. I am going to utilize the two transistors to act like switches in order to prevent the GREEN and BLUE channels from lighting up when the Arduino® isn't powered on. Once we have power, the transistors, will allow the Arduino® to apply voltage to the base of each transistor turning the switch on to allow the flow of electricity through the LED.

![Power Indicator Tri-color LED circuit](images/00024.jpeg)

![Creative Commons - Attribution - Share Alike](images/00005.jpeg) Image created using: [Fritzing](http://fritzing.org/)

##### Software

The following code is used to manage the power indicator circuit to give a visual representation of the state of the circuit.

```
 /*
 * Power Indicator - the purpose of this script/circuit is to visually display
 *                   the health of the system via a tricolor RGB LED.
 *
 * The redPin will be used to control the red portion of the LED.
 *     Note: this pin will act different then the other two as
 *           we will be turning this pin high to turn off the LED.
 *           To make the code cleaner, this change is only
 *           handled in the LightLed routine.
 * The greenPin will be used to control the green portion of the LED.
 * The bluePin will be used to control the blue portion of the LED.
 *
 * For this circuit, there will not be any additional inputs or outputs as this circuit is
 * intended as the basis for a project opposed to a complete project.
 */

/*
 * Enumeration of values to turn on/off the 3 channels of the tricolor LED
 */

typedef enum
{
  RED_ON = 0x1,
  GREEN_ON = 0x2,
  BLUE_ON = 0x4
} eLedSettings;

/*
 * Constants used in this sketch
 */

const int redPin = 9;
const int greenPin = 10;
const int bluePin = 11;

const int POWER_OFF = RED_ON;
const int POWER_ON = GREEN_ON;
const int SETUP = GREEN_ON | RED_ON;  // Turn both red and green on to get yellow
const int BLANK = 0; // no lED's lit

/*
 * Method declarations
 */

void LightLed(int colors);

/*
 *  LightLed
 *
 * This method checks the passed in value to determine which parts of the LED should be on and
 * which ones shouldn't be.  Only the lower 3 bits are used to indicate the colors starting with
 * red as the LSB (least significant bit) and blue the MSB (most significant bit)
 *
 * Params - colors - a set of bits (bit mask) indicating which LED colors should be on and
 *                   which ones should not be.
 *
 * Returns - none
 */

void LightLed(int colors)
{
  /*
   *  Red acts differently where a HIGH output turns off the LED and a LOW output
   *  turns it on.
   */
  if (colors & RED_ON)
  {
    digitalWrite(redPin, LOW);
  }
  else
  {
    digitalWrite(redPin, HIGH);
  }

  if (colors & GREEN_ON)
  {
    digitalWrite(greenPin, HIGH);
  }
  else
  {
    digitalWrite(greenPin, LOW);
  }

  if (colors & BLUE_ON)
  {
    digitalWrite(bluePin, HIGH);
  }
  else
  {
    digitalWrite(bluePin, LOW);
  }
} 

/*
 * Setup - main configuration point of our sketch to configure
 *         the Arduino for writing digital values out on the defined pins
 *
 * Params - none
 *
 * Returns - nothing
 */

void setup()
{
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);

  LightLed(SETUP);
  delay(1000);
}

/*
 * loop - main method which will be called each time the
 *        Arduino goes through its main loop to turn the
 *        LED on to green and then off blinking every
 *        half second
 *
 * Params - none
 *
 * Returns - nothing
 */
void loop()
{
  LightLed(POWER_ON);
  delay(500);

  LightLed(BLANK);
  delay(500);
} 
```

###### Enumerations

In this sketch I have used a new feature of the C programming language which is called an enumeration i.e. enum. Much like a const integer or a definition such as #define VARIABLE, an enumeration allows the developer to assign certain values to names which makes our code easier to read. For this enumeration, I have defined three values indicating if each of the parts of the LED are on or off. I have assigned values for each of the enumerations such that each one is a specific bit out of the total bytes. Consider the following:

```
 const int myValue       = 42;         // decimal representation (base 10)
const int myValueHex    = 0x2A;       // hexadecimal representation (base 16)
const int myValueBinary = 0b00101010; // binary representation (base 2) 
```

Each of the constants are the same value however I have shown them in various formats. As you can see, the decimal version is probably the easiest to understand while the binary version is cumbersome but explicit in terms of what bits are on and off. Binary numbers are the heart of computer computation. I am using this feature of computer numbers to indicate if an LED should be on or off. What makes this nice is that I can use one variable to indicate which parts of the LED is on or off opposed to a separate value for each of the colors. You may have noticed that each value assigned in my enumeration has unique bits to represent it. The reason is that I can combine them to create additional colors such as red and green creating yellow.

###### Constants

In the beginning of this sketch I have declared some constant values which I will use later on in my code. As I mentioned previously, it is better to declare these values as constant that way you get the benefit of meaningful names in your code which helps in the overall readability of your sketch along with the ability to change the value as needed later on without trying to find everywhere it is used in your code. The constants in this sketch define which pins are being used as digital outputs and assign values to certain states such as POWER_OFF, SETUP, and POWER_ON.

```
 const int POWER_OFF = RED_ON;
const int POWER_ON = GREEN_ON;
const int SETUP = GREEN_ON | RED_ON;  // Turn both red and green on to get yellow
const int BLANK = 0; // no lED's lit 
```

In the above four lines I have declared each of my color states as either a single or combination of values from my enumeration. In the enumeration I defined the values as:

```
 typedef enum
{
  RED_ON = 0x1,
  GREEN_ON = 0x2,
  BLUE_ON = 0x4
} eLedSettings; 
```

In the above enumeration, I have RED_ON assigned the hexadecimal value, 0x01. This becomes 0b0001 in binary. For the second value, GREEN_ON, I have assigned it the hexadecimal value 0x02. This becomes 0b0010 in binary. You might notice that each one sets a different bit to on. Finally I have assigned the third value, BLUE_ON the hexadecimal value 0x04 which is 0b0100 in binary. If I want to create a yellow light, I can simply combine the value for GREEN_ON with the value for RED_ON which will equal the hexadecimal value 0x03 which will be the binary value 0b0011. When I pass this combined value to my function LightLed it will check each bit and turn on the proper portion of the LED corresponding to the set bits.

###### Method Declarations

I declared one method in this sketch to light up the LED based on the color passed into the method which can be any combination of the three colors. This allows for up to eight (8) total colors with all colors on representing WHITE and all colors off indicating BLACK. While there isn't a true black, the lack of light i.e. the LED in the off state will represent black.

###### User Methods

As mentioned above, I have created one method which will turn on each of the parts of the LED based on the incoming color value. The color value is called a bit mask which indicates which colors are on and which ones are off. The passed in color value is anded i.e. & with each of my constants, RED_ON, GREEN_ON, and BLUE_ON, to determine if that part of the LED should be on or off. The AND operation is a fundamental operation of binary numbers. This will allow us to test if a color should be lit or not.

###### Setup

The setup method is where I will configure my Arduino® to operate as I need. In this case I will enable each of the pins being used as digital outputs prior to using them which is done when I call the method LightLed.

```
 void setup()
{
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);

  LightLed(SETUP);
  delay(1000);
} 
```

The main thing of note in this setup code is that I am delaying for one (1) second to allow the user to see the yellow LED before changing it to green.

###### Loop

Normally the loop method is where all of the work is done however since this is only a partial sketch i.e. I am showing how to use a digital output and not much more, it is fairly limited in its functionality.

```
 void loop()
{
  LightLed(POWER_ON);
  delay(500);

  LightLed(BLANK);
  delay(500);
} 
```

In this loop, the LED is turned on to show GREEN for 500 milliseconds and then turn off for another 500 milliseconds.

### Summary

In this chapter we looked at various ways to output data from our Arduino® to control the world around us. This ranges from simple visual indicators to alert us when an issue arises, to automated control systems that can keep a device cool based on the surrounding temperature. We also looked at servo's which could be used for simple movement or could as part of a system to control a robotic arm or other sophisticated machinery. Overall, the number of possibilities are only limited by the imagination of the developer.

![chapter end graphic](images/00001.jpeg)

# Program Interrupted

## Stop! Stop! Wait

Interrupts are a very important aspect of program implementation and can be leveraged to provide clarity to an application. Interrupts allow you to focus on the task at hand while knowing that other operations are going to happen when they should. They can also be the source of all sorts of trouble and make it difficult to determine what is happening in your application. With proper planning and good coding practices though, you can keep them under control.

I imagine your first question is what is an interrupt? An interrupt is a signal to your micro-controller indicating that an event has occurred. The reason this is beneficial is that it tells the micro-controller that there is something to be done opposed to having it waiting around checking periodically for something to do. Consider if you had a pet dog that you needed to take outside during the day to do their business. Your first option is to jump up and check every five (5) minutes or so to see if he/she needs to go out. While this would be a successful approach, it does waste a lot of time. The other option is to train your pet to notify you when it needs to go out. With this approach you can go about your business, and when needed, take your pet outside to do theirs. Your day remains productive while your pet gets relief when they need it. Sort of a win/win situation. An interrupt is the same thing overall. Instead of checking to see if something needs to be done, the interrupt notifies your micro-controller that something needs attention and then allows it to handle the distraction when needed in the way it should be done. Once the interrupt has been satisfied, the micro-controller can go back to doing whatever else it needs to do and not waste time continuously checking input pins.

In one of the previous chapters we looked at various types of inputs such as analog signals and digital values. For one circuit we carefully set up the circuit to provide an input when the temperature reached a certain point. For our purposes, this worked well and we were able to determine when an action should be taken such as turning a fan on. While that did the trick and worked decent enough, we wasted a lot of time monitoring the input pin to see if it was time to take action. That was a lot of wasted effort and we can do better. Imagine having a tropical fish tank where the fish have to be kept at 78°F exactly. When the temperature gets too cold, the fish get chilled and die. When the temperature gets to warm, the oxygen in the water goes down and the fish die. So what do we do? We can use the circuit from before however we wasted a lot of effort checking to see if the temperature was above a certain level. Now we want to also check if it is below a certain level. And what happens if we check for it to be above 78°F and its actually below that temperature? We end up standing around the toilet in the bathroom saying good bye to our fish. Not good. What we need is a way to signal the micro-controller at anytime that there is an important action that needs to take place. This is where interrupts come in.

In the example below, I will build a circuit that will trigger off of one temperature circuit. The second half of the circuit to detect the temperature dropping below a specific point can be added and wired to a second interrupt pin to be handled accordingly.

The Arduino® and most importantly, the Atmel® micro-controller, is designed to allow external events to signal the micro-controller that there is an important action to be taken. The Ardunio® provides a number of pins that can be used for external interrupts. The following table details which pins of the Arduino® can be used for external interrupts.

| Arduino® Board | Interrupt 0 | Interrupt 1 | Interrupt 2 | Interrupt 3 | Interrupt 4 | Interrupt 5 |
| NANO | Pin 2 | Pin 3 | N/A | N/A | N/A | N/A |
| UNO | Pin 2 | Pin 3 | N/A | N/A | N/A | N/A |
| MEGA 2560 | Pin 2 | Pin 3 | Pin 21 | Pin 20 | Pin 19 | Pin 18 |
| Due | * | * | * | * | * | * |
| Yun | Pin 3 | Pin 2 | Pin 0 | Pin 1 | Pin 7 | N/A |

* The Arduino® Due can have interrupts mapped to all available pins. When using this particular board, you will have to specify the pin number opposed to interrupt number;

For these examples, I will only be using pins two (2) and three (3) as they are consistent across most of the various boards** I have been working with and will make the examples easier to follow.

** The Yun appears to have the interrupts, 0 and 1, swapped in terms of pins based on the documentation that I could find.

### Temperature Trigger

The first thing we will do is to take our temperature circuit ([Temperature Trigger](#part0004_split_002.html_temptrigger)) and put the input on pin 2 which will correlate with Interrupt 0. Next we will have to instruct the Arduino® to expect an interrupt on that pin.

#### Required Components

*   Arduino® Board
*   (2) 4.7K Ohm Resistor
*   (2) 10K Trim potentiometers
*   LM335 temperature sensor[[7](#part0012_split_001.html_Ref7)] or similar such as the NTE7225[[8](#part0012_split_001.html_Ref8)]
*   LM311 voltage comparator[[9](#part0012_split_001.html_Ref9)] or similar such as the NTE943M[[10](#part0012_split_001.html_Ref10)]

#### Tools

*   breadboard
*   jumper wires
*   voltage meter

#### Schematic

![LM335 Temperature triggering circuit](images/00025.jpeg)

![Creative Commons - Attribution - Share Alike](images/00005.jpeg) Image created using: [Fritzing](http://fritzing.org/)

#### Software

The following code incorporates the analog reading for the temperature set point that we wish to trigger off of. Prior to connecting the analog pin zero (0) to the LM311 comparator input, you may want to place it on pin two (2) of the LM335 to adjust the temperature sensor to the current room temperature.

```
 /*
  * This circuit is designed to toggle between a HIGH signal and a LOW
  * based on the current temperature in the room.  The potentiometer
  * and the resistor are used to divide the 5v signal into two values
  * giving us the comparison we need to trigger the comparator output.
  * 2.73v is 0°C so to get the comparator to trigger we will want
  * to ensure that there is 2.73v + X across the potentiometer where
  * X is the temperature we want to toggle on.
  * The temperaturePin (now called setPointPin) will again read in the 
  * temperature however it will actually be the voltage across the 
  * potentiometer so we can use that as our setpoint.
  * The temperatureTogglePin will be used to determine if we are above
  * or below our target temperature.
  */        
 const int setPointPin = 0;
 const int temperatureTogglePin = 2;  // Use the interrupt attached to digital pin 2
 const float baseVoltage = 2.730f; /* 2.730V at 0°C */
 const float voltageReference = 5.0f;
 const float maxSampleCount = 1023.0f;
 const float CtoFConversion = 9.0f / 5.0f;
 const float FtoCConversion = 5.0f / 9.0f;
 const float CtoFDelta = 32.0f;
 volatile boolean setPointReached = false;

 /*
  * Method declarations
  */

  float getTemperature(float temperatureVoltage);
  float convertTemperatureToF(float temperatureInCelsius);
  float convertTemperatureToC(float temperatureInFahrenheit);

 /*
  * Interrupt declarations
  */

  void TemperatureTrigger();

 /*
  * getTemperature - determines the temperature in celsius based on the
  *         incoming voltage value assuming 2.73v equals 0°C
  *
  * Params - temperatureVoltage - the incoming voltage representing the temperature
  *
  * Returns - float - the actual temperature in celsius based on the incoming voltage
  */

 float getTemperature(float temperatureVoltage)
 {
   float currentTemperature = 0.0f;

   // From the datasheet, every 10 mv is equal to 1 °K - 0°C is 273°K equal to 2.73v
   // Temperature is scaled by 100 to bring it into the celsius scale from kelvin
   currentTemperature = (temperatureVoltage - baseVoltage) * 100;

   return currentTemperature;
 }

 /*
  * convertTemperatureToF - converts the tempertature from celsius to fahrenheit
  *
  * Params - temperatureInCelsius - the incoming temperature in celsius
  *
  * Returns - float - the temperature expressed in fahrenheit
  */

 float convertTemperatureToF(float temperatureInCelsius)
 {
   float convertedTemperature = 0.0f;

   convertedTemperature = (temperatureInCelsius * CtoFConversion) + CtoFDelta;

   return convertedTemperature;
 }

 /*
  * convertTemperatureToC - converts the tempertature from fahrenheit to celsius
  *
  * Params - temperatureInCelsius - the incoming temperature in fahrenheit
  *
  * Returns - float - the temperature expressed in celsius
  */

 float convertTemperatureToC(float temperatureInFahrenheit)
 {
   float convertedTemperature = 0.0f;

   convertedTemperature = (temperatureInFahrenheit - CtoFDelta) * FtoCConversion;

   return convertedTemperature;
 }

 /*
  * TemperatureTrigger - is triggered by an interrupt when
  *                      the temperature setpoint is reached.
  *
  * Params - none
  *
  * Returns - none
  */

void TemperatureTrigger()
{
  setPointReached = true;
}

 /*
  * Setup - main configuration point of our sketch to configure
  *         the Arduino for serial communications and interrupt usage.
  *
  * Note:  We will be using the rising edge of the interrupt to trigger
  *
  * Params - none
  *
  * Returns - nothing
  */

 void setup()
 {
   attachInterrupt(0, TemperatureTrigger, RISING);
   Serial.begin(9600);
 }

 /*
  * loop - main method which will be called each time the
  *        Arduino goes through its main loop to read the
  *        setPoint temperature value abd check our digital
  *        input pin to see if it is high or not.
  *
  * Params - none
  *
  * Returns - nothing
  */

 void loop()
 {
   int    rawSetPointValue = 0;
   float  setPointVoltage = 0.0f;
   float  temperatureSetPoint = 0.0f;

   // Read in the temperature value which will be in a range from 0 to 1023
   rawSetPointValue = analogRead(setPointPin);

   // Convert our incoming voltage representation to a value we can utilize
   setPointVoltage = ((float)rawSetPointValue * voltageReference) / maxSampleCount;

   // We now have the current temperature expressed in celsius
   temperatureSetPoint = getTemperature(setPointVoltage);

   // Print out the current setpoint temperature in both C and F
   Serial.print("The temperature set point is: ");
   Serial.print(temperatureSetPoint);
   Serial.print("C which is ");
   Serial.print(convertTemperatureToF(temperatureSetPoint));
   Serial.println("F");

   if (setPointReached == true)
   {
     Serial.println("We have reached our set point.");
     setPointReached = false;
   }
   // Rest for a second and read the current setpoint temperature
   delay(1000);
 } 
```

As I mentioned before, this code is not a lot different from the earlier code so I won't go into great detail regarding it, however I will point out the highlighted pieces.

The first difference is the use of a volatile boolean type. Volatile is a hint to the compiler that the variable it is used in conjunction with could change by means other than directly by the program.

```
 volatile boolean setPointReached = false; 
```

Because the interrupt routine is what causes the boolean variable setPointReached to change from false to true, we must give the compiler a hint that even though no one is calling the method TemperatureTrigger directly the boolean variable can still be changed via the interrupt routine which calls TemperatureTrigger.

The next part of the code is the interrupt declaration. While it is just like the other method declarations, I kept it separate in order to point out that the interrupt routine doesn't return any values and does not take any parameters.

```
 /*
  * Interrupt declarations
  */

 void TemperatureTrigger(); 
```

Next is the definition of the TemperatureTrigger code where we set the setPointReached flag to true indicating to the main loop that the interrupt has been triggered.

```
 /*
  * TemperatureTrigger - is triggered by an interrupt when
  *                      the temperature setpoint is reached.
  *
  * Params - none
  *
  * Returns - none
  */

void TemperatureTrigger()
{
  setPointReached = true;
} 
```

Following this is our setup routine where we enable the interrupt and assign it to the appropriate pin. In this case I am using the Arduino® digital pin two (2). The call to the attachInterrupt routine enables the interrupt zero (0). Also note that we are triggering the interrupt on the rising edge. This indicates that when the signal coming in goes from low to high i.e. rises then the interrupt triggers. It can also trigger off any of the following values:

LOW

triggers when the input is LOW.

CHANGE

triggers whenever a change occurs on the input pin.

RISING

triggers when the input rises from low to high.

FALLING

triggers when the input falls from high to low.

HIGH

triggers when the input is HIGH.**

** The HIGH value is only available on the Arduino® Due platform.

```
 attachInterrupt(0, TemperatureTrigger, RISING); 
```

In this example, the main goal was to simply be able to detect the input trigger, the interrupt, indicating that our set point was reached. We could go a little further in cleaning up the code by not doing any work unless the interrupt was triggered. However for testing, I wanted to monitor the values being read to ensure things were working as expected. As mentioned above, I didn't build the second half of the circuit which would trigger when a temperature fell below a certain value. To do this, you could use the same circuit as shown however in this case you would calibrate it for the lower temperature and change the interrupt routine to trigger off of the FALLING edge. In general the input to the interrupt would be high and would go low once the temperature dropped below the target value.

### Rotary Encoder

For this project we will be looking at rotary encoders to determine the amount of distance a user wants to traverse in relation to a signal. For instance, I may want to use the rotary encoder to brighten or dim an LED. I can use a potentiometer for this however a rotary encoder might do the job better given its behavior. In addition to this I store my current setting in the onboard EEPROM in order to return to that value at start up. This also prevents any potential issues with the brightness changing during movement and such while the device is turned off. This could happen with a potentiometer as it has a fixed length of travel i.e. it can only go so far in either direction and can be turned while the device is not powered on. A rotary encoder, however, is designed to spin continuously in either direction so it will not matter if it is turned while the device is powered off. The Arduino® will only act upon it when it is powered on. I will configure my Arduino® to trigger off of inputs from the rotary encoder to determine how bright the LED should be.

#### Required Components

*   Arduino® Board
*   (4) 10K Ohm Resistors
*   (2) 0.01uF capacitors
*   ALPS STE1207 Rotary Encoder
*   Red LED

#### Tools

*   breadboard
*   jumper wires
*   voltage meter

#### Schematic

![Rotary encoder trigger circuit](images/00026.jpeg)

![Creative Commons - Attribution - Share Alike](images/00005.jpeg) Image created using: [Fritzing](http://fritzing.org/)

#### Software

For this code, we will configure our interrupt to trigger when one signal of the rotary encoder is active. When that happens we will read the value on the secondary pin to see which direction the encoder is being turned. The decoder is designed such that one signal will trigger and at the trigger time the other signal will be either high or low depending on the direction it is being turned. So the one input triggers our software to indicate movement while the other input gives us the direction. We will then have to determine how many signals we have received to determine the number of turns the user has made. Extra circuitry, resistors and capacitors, have been added to the rotary encoder to allow for better signal integrity. This information is provided by the manufacturer of the rotary encoder and can be found usually on their website. Typically, I will download the manufacturer's data sheet when a component is unfamiliar to me as they will usually have sample circuits that you can utilize when creating your own circuits.

```
 /*
 * RotaryEncoder -  the purpose of this sketch is to handle the input of
 *                  a rotary encoder to adjust the brightness of an LED.
 *
 * The rotary encoder output will be tied to one interupt and one normal input
 * line in order to detect movement and determine which direction.
 *
 * One output line will be connected to the LED and we will use PWM
 * to adjust the brightness based on the amount the rotary encoder is
 * turned.
 *
 * We will store the current brightness of the LED (0 - 255) so that we can
 * restore it after a reboot.
 */

const int ledOutput = 3;
const int directionPin = 4;
const long signature = 0xFACE; // some non-arbritary value

/* Module includes */

#include <EEPROM.h>

/* Structures used in this sketch */

typedef struct
{
  long signature;
  int brightness;
} EE_Structure;

/*
 * Variables used by this sketch
 */

volatile EE_Structure StoredData;

/*
 * Method declarations 
 */

int ReadInteger(int offset);
void WriteInteger(int offset, int value);
long ReadLong(int offset);
void WriteLong(int offset, long value);
void HandleDecoderTrigger();

/*
 * ReadInteger - a helper function to read in an integer from the nonvolatile storage
 *
 * Params - offset - the offset into the EEPROM where data is stored
 *
 * Returns - int - the value read from the specified location
 */

int ReadInteger(int offset)
{
  int returnValue = 0;

  // Read in EEPROM
  for (int count = 0; count < sizeof(int); count++)
  {
    returnValue |= EEPROM.read(offset + count) << (count * 8); // read in a byte from eeprom and shift it x to build up an integer of data
  }

  return returnValue;
}

/*
 * WriteInteger - a helper function to write in an integer to the nonvolatile storage
 *
 * Params - offset - the offset into the EEPROM where data is to be stored
 *        - value - the value to be stored
 *
 * Returns - none
 */

void WriteInteger(int offset, int value)
{
  byte dataValue = 0;
  byte intSize = sizeof(int);

  for (int count = 0; count < intSize; count++)
  {
    dataValue = value >> ((intSize - 1 - count) * 8); // We need to shift from left to right so upper first then on down
    EEPROM.write(offset + count, dataValue);
  }
}

/*
 * ReadLong - a helper function to read in a long from the nonvolatile storage
 *
 * Params - offset - the offset into the EEPROM where data is stored
 *
 * Returns - long - the value read from the specified location
 */

long ReadLong(int offset)
{
  long value = 0;

  int storedValue = ReadInteger(offset);

  value = (storedValue << 16);

  storedValue = ReadInteger(offset + 2);

  value += storedValue;

  return value;
}

/*
 * WriteInteger - a helper function to write in a long to the nonvolatile storage
 *
 * Params - offset - the offset into the EEPROM where data is to be stored
 *        - value - the value to be stored
 *
 * Returns - none
 */

void WriteLong(int offset, long value)
{
  int upperValue = (value >> 16);
  int lowerValue = value && 0xFFFF;

  WriteInteger(offset, upperValue);
  WriteInteger(offset + 2, lowerValue);
}

/*
 * HandleDecoderTrigger - called when the encoder is turned
 *
 * Params - none
 *
 * Returns - nothing
 */

void HandleDecoderTrigger(void)
{
  byte directionData = 0;

  noInterrupts();

  directionData = digitalRead(directionPin);

  if (directionData == HIGH)
  {
    // clockwise
    if (StoredData.brightness < 256)
    {
      StoredData.brightness++;
    }
  }
  else
  {
    // counter clockwise
    if (StoredData.brightness > 0)
    {
      StoredData.brightness--;
    }
  }

  interrupts();
}

/*
 * Setup - main configuration point of our sketch to configure
 *         the Arduino for reading signals from a rotary encoder
 *         and setting the brightness of the LED based on the
 *         amount the rotary encoder is turned and which direction.
 *
 * Params - none
 *
 * Returns - nothing
 */

void setup()
{
  StoredData.signature = ReadLong(0); 

  if (StoredData.signature == signature)
  {
    // Have we been here before?
    StoredData.brightness = ReadInteger((char *)&StoredData.brightness - (char *)&StoredData.signature);
  }
  else
  {
    // Store signature and default brightness of 0
    WriteLong(0, signature);
    WriteInteger((char *)&StoredData.brightness - (char *)&StoredData.signature, StoredData.brightness);
  }

  pinMode(directionPin, INPUT);

  attachInterrupt(0, HandleDecoderTrigger, FALLING);  // trigger on falling edge
}

/*
 * loop - main method which will be called each time the
 *        Arduino goes through its main loop to change the state
 *        of the headlights and update the 7 segment displays
 *
 * Params - none
 *
 * Returns - nothing
 */

void loop()
{
  static int lastBrightness = 0;
  static int brightnessOffset = (char *)&StoredData.brightness - (char *)&StoredData.signature;

  if (lastBrightness != StoredData.brightness)
  {
    analogWrite(ledOutput, StoredData.brightness);
    WriteInteger(brightnessOffset, StoredData.brightness);
  }

  // Pause for 500 milliseconds i.e. 1/2 second.
  delay(500);
} 
```

For this sketch we have introduced a number of new items which I will go over as they appear within the sketch. The first item is the signature that I am using. While it is the same as other constant variables I have used in the past, I am defining this one in hexadecimal format i.e. [base 16](#part0012_split_001.html_Ref14) format. Base 16 format allows the user to specify a number using 16 unique tokens which are typically the numbers zero (0) through nine (9) and the letters A through F. Because in hexadecimal we have this selection of letters to choose from, I opted to spell out a word that is easily recognizable. Also note that this is a long integer data variable which will be 4 bytes on this platform.

```
 const long signature = 0xFACE; // some non-arbritary value 
```

For this sketch, I chose the word FACE as it stands out. The likelihood of this particular letter order coming up randomly in memory is fairly low so I can be fairly certain that if I do find this sequence of letters in memory then my persistent storage i.e. the EEPROM is initialized. Speaking of EEPROM's, I should probably explain what they are and what the following line of code does.

```
 #include <EEPROM.h> 
```

An [EEPROM](#part0012_split_001.html_Ref15) is a special device that can store data even when the power to the system is turned off. This is called non-volatile memory or sometimes persistent memory. One of the special things about this memory is that it can be written to at runtime and is built into the micro-controller that we are using i.e. the Atmel® device. This allows us to store data between user sessions and restore that data at runtime in order to pick back up where we left off. In this case we will be storing the last known brightness level of the LED in order to restore the LED to the same brightness level when we turn the circuit back on. This can be very handy depending on your application. If this was a television and the encoder was used to set the volume of the television, you would want it to come back on at the same volume level as when you turned it off. While you could just leave the television running all of the time, that would be very wasteful. In this case, we can store the current volume in persistent memory and then restore it when we power back up making the television more user friendly. So now that we have an idea of what an EEPROM can be used for, we should look at that line of code that mentions it.

In this sketch, I am including a secondary file, which the Arduino® calls a library. This allows me to utilize functionality that other's have provided in order to access various features of the Arduino® that might not normally be readily accessible. In traditional C and C++, common functionality is provided in the form of libraries which are described in header files. The .H is the common file extension indicating that this is a header file. The header file will typically describe the functionality that is made available by the particular library without actually showing how it is done. This can be very useful to extend the functionality of sketches and allow user's to share their code with others. In order to take advantage of libraries inside of the Arduino® platform, select the Sketch menu item and then the Import library option which will show a selection of libraries that you can use. Select the EEPROM library to include it with the current sketch that you have open. While I will not go into detail regarding each of the libraries, it is good to know that they are there and ready to be used when you need them. So now back to that #include statement. This statement is a special keyword of the C language that is used to add functionality to an application.

![image showing library menu selection](images/00027.jpeg)

While you could retype everything in the file in order to make it available for use, this can be very error prone, tedious, and quite frankly a waste of time. The #include statement does this for you allowing you to build your sketches faster and more reliably. Note that the # character at the beginning of the include statement is required to indicate to the compiler that this is a special command. Once you have included the library that you need, in this case, the EEPROM library, you will be able to use the functionality that it provides in your sketch.

So we included some additional functionality in our code. That is pretty cool and something we will want to remember in the future to save time when creating more complex sketches. It is also good to note that you, as an end user, can make your own libraries of routines that you use a lot to limit the amount of coding that you need to do. The temperature conversion functions that we used previously would be good candidates for a library as we will probably use them again from time to time and we probably will not want to have to retype that information in again.

Now we come to the next new feature of the C programming language which is the structure. A structure allows the programmer to group a set of variables together into one container making it easier to pass around the data and to work with it. The following is our structure declaration which we will use in this sketch.

```
 typedef struct
{
  long signature;
  int brightness;
} EE_Structure; 
```

This structure is fairly simple and consists of the signature block and a brightness value. I have called it EE_Structure as this will be the structure of the data we will store in the EEPROM. It is important to note that this is the name of the structure definition and not the actual variable name I will use in my sketch. I am combining the brightness and a signature in the data so that I can determine if I have a valid value stored in the EEPROM when I look at it during future runs of my sketch. When I first run my sketch, I cannot guarantee what values will be in the EEPROM. The signature helps me determine if my sketch has ever been executed before. The second part of this structure is the brightness of the LED which will range from zero (0) to two hundred fifty five (255). This could fit into one unsigned character i.e. a byte however I reserved extra space in case I need it later on. So where does a structure come in handy when programming? Well, now I can use this structure just like I would a regular variable type such as an integer. I am now able to do the following:

```
 volatile EE_Structure StoredData; 
```

This allows me to declare both the signature and the brightness at the same time. It also keeps them together as one unit which I can pass around to methods as needed. I didn't take full advantage of all of the benefits of a structure however it still comes in handy to keep my data contained within one type. If I had multiple encoders with multiple ID's, I could create one of these structures for each of the LED's. I could also associate the output pin for each LED with the brightness to keep each data set together. This can be very useful when your data needs increase and the complexity of your sketches increase. This is also a fundamental premise of object oriented design and C++ which is an object oriented programming language. Keeping your data and the methods that work with that data combined allows you to create building blocks to work with in your later sketches.

The next few line of code are the function declarations and the various helper functions that I wrote to make my program easier to understand and to reduce the code size. I knew I would need to write data to the EEPROM and be able to restore it at a later time. With this in mind, I created a few functions, ReadInteger, WriteInteger, ReadLong, and WriteLong which will read and write an integer or long to a specific location within the EEPROM. The first one is the ReadInteger function which looks like this:

```
 int ReadInteger(int offset)
{
  int returnValue = 0;

  // Read in EEPROM
  for (int count = 0; count < sizeof(int); count++)
  {
    returnValue |= EEPROM.read(offset + count) << (count * 8); // read in a byte from eeprom and shift it x to build up an integer of data
  }

  return returnValue;
} 
```

This code reads in a series of bytes from the EEPROM and concatenates them into a single integer value. As I read each byte, I shift it over using the shift (<<) operator which shifts the bits in the supplied value the number of bits specified. In this case I am shifting the data 8 bits which is the equivalent of one byte.

When shifting data, the bits are moved down or up depending on the direction of the shift command. For instance, if I had the binary value 0b00000011 which is equal to the value of three (3), I could shift it one bit to the left which would then give me the value 0b00000110. When I shift the value left, the top most bit is lost and a zero is added to the end of the value preserving the proper number of bits that make up the variable. In this example, I am using 8 bits which represents one byte of data. If I was writing this in code it would be as follows:

```
 byte value = 0x03; 				// start with a value of 3
byte shiftedValue = value << 1;	// shift left by 1 bit resulting in 0x06 i.e. 0b00000110 
```

As you might have guessed, shifting it to the right would do the opposite and with the value 0x06 becoming 0x03\. If you were to shift it another single bit to the right, the value 0x03 would then become 0x01. Another thing to note, a one (1) bit shift is equivalent to multiplying or dividing by two (2). When speed is a concern, shifting can be an order of magnitude faster than a division operation.

One thing you will note is that I am using the sizeof(int) compile time unary operator. This is a very important operator which allows code to be more portable opposed to hard coding a size. For the Atmel® device used on a number of the Arduino® boards, the integer size is two (2) bytes. So when I store my integer value to EEPROM, I will be storing two bytes of data which represents that integer. On the Arduino® Due which is an ARM® based device, the size of an integer is four (4) bytes. By writing my code to utilize the sizeof operator, I am able to make it more portable then it otherwise would be. The downside is that the data I store in the EEPROM will typically only be read correctly by a device that shares the same integer size as that which wrote it. For our purposes this is a non-issue as the EEPROM is internal to the device and only this device will ever read and write to it. If this was a shared memory device then we would have to take precautions to ensure that one device didn't interpret the data incorrectly.

Following the ReadInteger function is the aptly named WriteInteger function. Basically it will do the reverse of the former function in that it will convert the integer passed in to a series of bytes based on the size of an integer for the platform the code is running on. This code is as follows:

```
 /*
 * WriteInteger - a helper function to write in an integer to the nonvolatile storage
 *
 * Params - offset - the offset into the EEPROM where data is to be stored
 *        - value - the value to be stored
 *
 * Returns - none
 */
void WriteInteger(int offset, int value)
{
  byte dataValue = 0;
  byte intSize = sizeof(int);

  for (int count = 0; count < intSize; count++)
  {
    dataValue = value >> ((intSize - 1 - count) * 8); // We need to shift from left to right so upper first then on down
    EEPROM.write(offset + count, dataValue);
  }
} 
```

This code writes a series of bytes to the EEPROM in the same order that the ReadInteger function will expect. This will allow me to store my data for future use when the micro-controller starts again. There is not anything remarkable with this function other than shifting the value down in order to store each part of the integer. The real key to this routine is the manipulation of the incoming integer to create a series of bytes.

```
 dataValue = value >> ((intSize - 1 - count) * 8); // We need to shift from left to right so upper first then on down
    EEPROM.write(offset + count, dataValue); 
```

The variable dataValue is of size one (1) byte. When I assign an integer to it, the integer will be truncated to match the size of the recipient. In this case the two byte integer will be converted to a single byte. Because of this fact, I can simply assign the data value to the integer and write out the first byte of data. The second time through the loop, I will shift the incoming integer value to the right by 8 bits which will then assign the upper byte to the variable dataValue and allow me to store the upper 8 bits of data associated with the integer that was passed in. This is assuming that the integer size is equivalent to two (2) bytes. I used the count variable to know how much I should shift the value in order to get the right value in my variable dataValue. You may also note that I took the liberty of assigning the sizeof value to a variable opposed to just using it throughout the code. This will actually make my code a little slower because I will have to read in the value from the memory location that I called intSize each time I want to reference it. If I had simply placed the sizeof operator wherever I needed to know the size of the integer, the calculation for the proper size value would have been done at compile time resulting in a constant value being placed in the code opposed to a variable representation. The net result is the code would be faster if I had used the sizeof operator consistently throughout. Of course if I had done that, I wouldn't have had anything to point out at this point in the book. The bottom line is that if you find that you need to call a particular function a number of times in order to retrieve a value which most likely isn't changing it is best to assign it to a variable opposed to calling the function repeatedly. This is assuming that the function to get said value is lengthy in nature or that the overhead to call the function based on your platform is high. For example, I now accessing the EEPROM is slower than accessing regular memory (RAM). Instead of reading in the brightness every time, I could read it in at the beginning of my sketch and keep it in a variable which I could access quite quickly. When the user changed the value of the brightness via the rotary encoder, I could update my variable and than write the new value to the EEPROM. However in the case of the sizeof operator, this is not a function call and in fact is an operator so the time used to evaluate it is a non-issue.

In addition to these two functions, there are two additional functions for storing long values which utilize the ReadInteger and WriteInteger functions we have just reviewed.

The next thing to look at is the call to EEPROM.read(offset + count). This call is part of the EEPROM class that I imported as the EEPROM library. The read function is a part of the class that knows how to read data from an EEPROM. In this case it is the EEPROM that is integral to the micro-controller that we are using. Overall the function isn't very difficult to understand. Pass in a valid offset between zero (0) and the maximum size of the EEPROM, minus one as the index is zero (0) based, and it will return the byte of data that is stored at the specified location. Pretty simple overall. The main thing is being able to convert the incoming bytes from the EEPROM into other data values. In this case I am converting them into integers which is why I will shift each value read in over eight (8) bits based on how many bytes I have read. This will work for any size integer as I am using the sizeof operator. Once I have finished reading the correct number of bytes, I return the complete value to the calling routine.

So once I am able to read and write values to my EEPROM, I now need to be able to respond to an interrupt whenever the rotary encoder is turned. I do that with the following code:

```
 void HandleDecoderTrigger(void)
{
  byte directionData = 0;

  noInterrupts();

  directionData = digitalRead(directionPin);

  if (directionData == HIGH)
  {
    // clockwise
    if (StoredData.brightness < 256)
    {
      StoredData.brightness++;
    }
  }
  else
  {
    // counter clockwise
    if (StoredData.brightness > 0)
    {
      StoredData.brightness--;
    }
  }

  interrupts();
} 
```

This code is written with the assumption that a turn of the rotary encoder will trigger it indicating it is time to read in the value on the secondary pin which I am calling directionPin. The rotary encoder that I am using outputs 2-bit quadrature code which consists of two (2) inputs to the Arduino®. The first input is used to detect movement of the device. This is mapped to the interrupt pin so I don't have to keep checking to see if the pin has changed. The signal is considered on when the trigger input reaches a LOW value. If the encoder is being turned clockwise, the other input will be a HIGH signal. If the encoder is being turned counter-clockwise then it will be a LOW signal. This allows me to both know that the encoder is being turned and to detect the its direction of travel. Based on the direction that the encoder is being turned, I will either increment or decrement the brightness of the LED. In order to be safe and not have multiple overlapping calls to my interrupt routine, I disable interrupts as I enter my decoder handler and re-enable them when I exit. The key here is to make sure that during the time interrupts are disabled, I take whatever necessary action there is to take, quickly. Generally it is not wise to keep interrupts turned off for any length of time. For our setup this is probably a moot point however it is best practice to keep interrupt routines short and to the point. As an interesting side note, key presses on a keyboard are typically processed as interrupts. During this time when determining which key was pressed, you can imagine it would be good to keep the routine short and simple. The main goal is to determine what key was pressed and pass that on to the application to handle. Typing would be very frustrating if you had to wait between each key press to have the computer determine what should be done with the key value.

### Fan Tachometer

For this project we will be utilizing an interrupt to determine the speed of a fan's rotation. There are a number of ways to detect the speed of the fan however for this project we will be using an infrared emitter and detector much like what would be found in a remote control device for a television or similar electronic device. In order to do this right, we will need to have the infrared emitter on one side of the fan and the detector on the other side such that the fan blades will cause the detector to change state as the blades block it from receiving the output of the transmitter. Because each fan blade will cause a pulse to occur on the detector, we will need to know how many fan blades are on the fan and use this number to determine how many interrupts we will be seeing for each revolution of the fan. For the fan, we can actually use anything that will break the connection between the emitter and the detector. A computer fan is convenient as a number of them can accept various voltages in order to change the speed at which it turns. However given the nature of the detection circuit, anything that breaks the line of site between the emitter and the detector will cause the interrupt to trigger. This can be useful in other applications such as motion detection or obstacle detection such as you might find with an automatic garage door opener.

#### Required Components

*   Arduino® Board
*   Infrared Emitter such as the [Model: 276-142](http://www.radioshack.com/product/index.jsp?productId=2049723)
*   Infrared Detector such as the one included with the emitter linked above
*   100 Ohm resistor
*   15K Ohm resistor
*   PC 5v fan

#### Tools

*   breadboard
*   jumper wires
*   voltage meter

#### Schematic

![Rotary encoder trigger circuit](images/00028.jpeg)

![Creative Commons - Attribution - Share Alike](images/00005.jpeg) Image created using: [Fritzing](http://fritzing.org/)

#### Software

For this code, we will configure our interrupt to trigger when the infrared detector is activated by a fan blade moving out of the way of the infrared transmitter. In the above image, the fan would sit between the two infrared devices. In order to see the connections clearly, I opted to not show the fan itself on the breadboard. When the blade of the fan stops blocking the infrared emitter, the detector is charged which then reduces the voltage drop across the detector resulting in a transition on the interrupt line. As the voltage across the detector drops, the voltage into the Arduino® drops from a high signal to a low signal. When the next fan blade again blocks the detector the voltage into the Arduino® rises triggering our interrupt which we will configure to trigger on a RISING edge.

```
 /*
 * Infrared RPM - the purpose of this sketch is to configure an interrupt to trigger
 *                when the infrared detector changes state.
 *
 * fanBlades is the number of blades that the fan being used has.  Each fan blade triggers
 *           the interrupt so to get an accurate reading we will need to divide the number
 *           we obtain by the number of blades.
 *
 * interruptId is the identifier of which interrupt we are using.  While the interrupt itself is attached to
 *             pin two (2) of the Arduino, the interrupt identifier is actually zero (0).
 *
 * updateFrequency is how often we update the display with our calculated RPM's
 *
 * speedCount is the number of times that the interrupt has been triggered since we last looked at.
 *
 * lastCycle is the value of millis() at the last cycle so we can accurately determine the speed based on a
 *           one second target
 */ 
```

```
 const int fanBlades = 7;
const int interruptId = 0;
const int updateFrequency = 1000;

volatile int speedCount = 0; // volatile as it will be changed by both the interrupt and the main loop
unsigned long lastCycle = 0; 
```

```
 /*
 * Method declarations
 */ 
```

```
 void infrared_trigger(); 
```

```
 /*
 * infrared_trigger - this method is short as it is handled during an interrupt
 *                    it's sole purpose is to update the speed counter
 *
 *
 * Params - none
 *
 * Returns - nothing
 */ 
```

```
 void infrared_trigger()
{
  speedCount++;
} 
```

```
 /*
 * Setup - main configuration point of our sketch to configure
 *         the Arduino for serial port reporting, setting our
 *         default values, and enabling our interrupt.
 *
 * Params - none
 *
 * Returns - nothing
 */ 
```

```
 void setup()
{
  // Setup the serial port to report our fan RPM value
  Serial.begin(9600);

  lastCycle = millis();  // get a starting value prior to turning the interrupt on

  // We will use the rising edge which correlates to the fan blade blocking the infrared detector
  attachInterrupt(interruptId, infrared_trigger, RISING);  
} 
```

```
 /*
 * loop - main method which will be called each time the
 *        Arduino goes through its main loop to check the
 *        amount of time since it last looked an if our
 *        update frequency has been exceeded, we will then
 *        report the rotations per minute scaled by 60
 *        since we are reporting the value every second.
 *
 * Params - none
 *
 * Returns - nothing
 */ 
```

```
 void loop()
{
  /*
   * Grab the current millis to see if our target delta has been reached
   */
  unsigned long currentCycle = millis(); 
  unsigned long delta = currentCycle - lastCycle;

  // If we have passed our update frequency, update and start again
  if (delta > updateFrequency)
  {
    //--------------------------------------------
    // Have my seconds (in milliseconds)
    // convert to RPM's i.e. rotations per minute
    //
    // I am using floats to be more accurate
    //--------------------------------------------
    float variableRate = ((float)delta / 1000.0f) * 60;

    unsigned long currentSpeed = (speedCount * (variableRate)) / fanBlades;

    // Reset our speed count and make our current cycle the last cycle
    lastCycle = currentCycle;
    speedCount = 0;

    //--------------------------------------------
    // Write out the current speed once we have reset our values above
    // this is because the interrupt will be still running while we
    // are taking care of calculating the RPM's
    //--------------------------------------------
    Serial.print("Current speed is: ");
    Serial.print(currentSpeed);
    Serial.print("\n");
  }
} 
```

This sketch is fairly straight forward with the primary feature being the interrupt routine. This routine is where we keep track of the number of times the fan blades have triggered the interrupt pin. The bulk of the work is done in the main loop where we determine the number of times the interrupt has been triggered per second and convert the values into an RPM value. To do this, I get the current millisecond count by calling the function millis(). This returns an unsigned long value representing the number of milliseconds that have elapsed since the Arduino® was powered on. I do this so that I can compare it withe value I read the previous time through the loop function. Once I reach a delta i.e. time span greater than my update frequency, I will determine the speed that the fan is rotating at by multiplying the number of times that the fan blocked the infrared emitter. Because the fan has multiple blades, I must factor that into my equation. While I tried to ensure that I only did this once per second, I can never be sure how often my loop function will be called. Given that, I assigned the variable, variableRate a value representing my actual time delta divided by 1000.0f which is how many milliseconds in one second. I then multiplied by sixty (60) in order to convert the value to minutes from seconds. Once done with that I could take the total times that the fan blocked the infrared emitter and multiple it by amount of time that passed along with dividing the value by the number of blades on the fan to get a final rotations per minute (RPM) value. In converting the value from floating point to unsigned long integer, I will be losing some precision however for the purpose of this sketch it should be fine.

### Summary

In this chapter I looked at interrupts and how to be more reactive to external events opposed to polling. Polling is very time consuming and depending on what is going on, could result in missed events. Interrupts alleviate this by making your design able to react when an event occurs. The downside is that you must be careful that what you do in the interrupt doesn't conflict with what you are doing in your main application loop. It is also wise to ensure that the actual interrupt routine be fairly quick and not prevent the system from doing what it needs to do.

![chapter end graphic](images/00001.jpeg)

# Communications

## Talking to the outside world one protocol at a time

Communication can take a number of forms, from simple speech, to visual indications such as traffic lights, to complex protocols between sophisticated devices. In this chapter we are going to explore the protocols used to communicate between sophisticated devices. Our Arduino® will be one end of the communication channel while various devices and machines will be the other end communicating with the Arduino®.

### Serial Port (RS-232)

In past chapters, we have looked at the initial communications between the Arduino® and a host computer using the COMM Port. This port has been used for a number of different applications, from keyboards to mice to a whole array of disparate devices. A typical RS-232 communication port will utilize the following signals:

| Signal Name | Purpose | DB-9 Pinout | DB-25 Pinout |
| Rx | Receive data from the sending device | 2 | 2 |
| Tx | Transmit data to the sending device | 3 | 3 |
| Gnd | Common ground between the two devices | 5 | 7 |

While the standard communications between the Arduino® and the host computer is a valid use case and important in order for us to debug our sketches, I want to explore other applications for which it can be used for. In this case, I happen to have a Bluetooth® shield that uses serial communications between the Arduino® and itself. Depending on which Arduino® module that you are using, you can use either a hardware serial port or a software serial port. The software serial port is designed to mimic the real hardware serial ports allowing you more flexibility as to which pins of your Arduino® are used. The downside is that it is an emulation and can be subject to anomalies and can be somewhat slower. Overall though, using a software serial port should be transparent to your sketch and the micro-controller for the most part. The shield I am using is from [Seeed Studio](http://www.seeedstudio.com/depot/Bluetooth-Shield-p-866.html?cPath=19_21) and is flexible in that it can act as both a master device or a slave device. The other nice feature is that it can use any digital pins between zero (0) and seven (7) for its serial interface. In addition to this, it also has two [Grove Ports](http://www.seeedstudio.com/wiki/GROVE_System) to allow the system to interface using mainstream connectors to external components which can be useful for remote monitoring and the like.

Care has to be taken when using the hardware communication port(s) in your own projects as the first serial port is also used for the USB communication port to your computer system. When you utilize the Serial class of functionality, the data sent and received travels over this hardware communication port to your host system. It is also the communication port which is used to program your micro-controller.

| Arduino® | Serial 0 | Serial 1 | Serial 2 | Serial 3 |
| UNO R3 | 0 (RX), 1 (TX) | N/A | N/A | N/A |
| Leonardo | USB (CDC) | 0 (RX), 1 (TX) | N/A | N/A |
| DUE | 0 (RX), 1 (TX) | 19 (RX), 18 (TX) | 17 (RX), 16 (TX) | 15 (RX), 14 (TX) |
| YUN | USB (CDC) | 0 (RX), 1 (TX) | N/A | N/A |
| MEGA 2560 | 0 (RX), 1 (TX) | 19 (RX), 18 (TX) | 17 (RX), 16 (TX) | 15 (RX), 14 (TX) |

There are a number of other Arduino® or compatible boards available not listed above however most of them are based off of one of the above listed boards and, in most cases, will have very similar features i.e. the number of serial ports and the pins they are found on.

With that all out of the way, lets look at some code to communicate with the Bluetooth® shield. For this sketch, I will be communicating with the shield using pins six (6) and seven (7). The Bluetooth® shield will be acting as the master device and connecting to another device which will be the slave. For this example, I will be communicating with an [OBDII Interface](http://en.wikipedia.org/wiki/On-board_diagnostics) to look at diagnostic codes on my vehicle.

#### Required Components

*   Arduino® Board
*   Seeed Studio Bluetooth® shield[[16](#part0012_split_001.html_Ref16)]
*   Generic OBDII Connector[[17](#part0012_split_001.html_Ref17)]

#### Tools

None.

#### Software

The following code demonstrates communicating with a Bluetooth® shield and then using that device to communicate with a remote device to send and receive data.

```
 /*
  * This sketch is designed to establish a connection over Bluetooth to transfer
  * data between a host system and a target microcontroller.
  */

#include <stdio.h>            // sprintf
#include <EEPROM.h>           // storage of connection data
#include <SoftwareSerial.h>   // communication between BT module and arduino
#include <btmodule.h>         // arduino library for communicating with the SeeedStudio BT module

// Status pin for onboard led

#define BT_CONNECTED_STATUS_PIN  13

// The BT shield can use two digital pins for the serial communications from D0 - D7

#define BT_COMM_SPEED 38400
#define BT_PIN_CODE 1234
#define BT_RX_PIN 6
#define BT_TX_PIN 7

#define BT_CONNECTED_PIN 1 // analog pin

// EEPROM SIGNATURE

const long signature = 0xACED; // some non-arbritary value

#define MAX_BT_ADDRESS 32

/* Structures used in this sketch */

typedef struct
{
  long signature;                  // data is only valid when 0xACED is stored here.
  int valid;                       // 0 if not valid, non-zero if valid
  byte bt_address[MAX_BT_ADDRESS]; // bluetooth address of previously discovered device(s)
} EE_Structure;

// State machine for bluetooth communications

enum StateMachine
{
  Initialize = 0, // if we store the device addr, we can jump to connecting
  RestoreDeviceAddress,
  DiscoveringDevice,
  DeviceDiscovered, // once discovered, we can reconnect without all of the setup
  ConnectingToDevice,
  ActiveCommunications,
  ErrorState,
  EndStates
};

/*
 * Method declarations
 */

int ReadInteger(int offset);
void WriteInteger(int offset, int value);
long ReadLong(int offset);
void WriteLong(int offset, long value);
void ReadBytes(int offset, byte *data);
void WriteBytes(int offset, byte *data);

/*
 * ReadInteger - a helper function to read in an integer from the nonvolatile storage
 *
 * Params - offset - the offset into the EEPROM where data is stored
 *
 * Returns - int - the value read from the specified location
 */

int ReadInteger(int offset)
{
  int returnValue = 0;

  // Read in EEPROM
  for (int count = 0; count < sizeof(int); count++)
  {
    returnValue |= EEPROM.read(offset + count) << (count * 8); // read in a byte from eeprom and shift it x to build up an integer of data
  }

  return returnValue;
}

/*
 * WriteInteger - a helper function to write in an integer to the nonvolatile storage
 *
 * Params - offset - the offset into the EEPROM where data is to be stored
 *        - value - the value to be stored
 *
 * Returns - none
 */

void WriteInteger(int offset, int value)
{
  byte dataValue = 0;
  byte intSize = sizeof(int);

  for (int count = 0; count < intSize; count++)
  {
    dataValue = value >> ((intSize - 1 - count) * 8); // We need to shift from left to right so upper first then on down
    EEPROM.write(offset + count, dataValue);
  }
}

/*
 * ReadLong - a helper function to read in a long from the nonvolatile storage
 *
 * Params - offset - the offset into the EEPROM where data is stored
 *
 * Returns - long - the value read from the specified location
 */

long ReadLong(int offset)
{
  long value = 0;

  int storedValue = ReadInteger(offset);

  value = (storedValue << 16);

  storedValue = ReadInteger(offset + 2);

  value += storedValue;

  return value;
}

/*
 * WriteInteger - a helper function to write in a long to the nonvolatile storage
 *
 * Params - offset - the offset into the EEPROM where data is to be stored
 *        - value - the value to be stored
 *
 * Returns - none
 */

void WriteLong(int offset, long value)
{
  int upperValue = (value >> 16);
  int lowerValue = value & 0xFFFF;

  WriteInteger(offset, upperValue);
  WriteInteger(offset + 2, lowerValue);
}

/*
 * ReadBytes - a helper function to read in a number of bytes from the nonvolatile storage
 *
 * Params - offset - the offset into the EEPROM where data is stored
 *        - data - the array to hold the data being read in
 *        - maxLength - the maximum length to read
 *
 * Returns - none
 */

void ReadBytes(int offset, byte *data, int maxLength)
{
  if (data != NULL)
  {
    for (int index = 0; index < maxLength; index++)
    {
      data[index] = EEPROM.read(offset + index);
    }
  }
}

/*
 * WriteBytes - a helper function to write out a number of bytes to the nonvolatile storage
 *
 * Params - offset - the offset into the EEPROM where data is to be stored
 *        - data - the array of bytes to be stored
 *        - length - the length of the data to write
 * Returns - none
 */

void WriteBytes(int offset, byte *data, int length)
{
  if (data != NULL)
  {
    for (int index = 0; index < length; index++)
    {
      EEPROM.write(offset + index, data[index]);
    }
  }
}

/*
 * Variables used by this sketch
 */

volatile EE_Structure StoredData;
BTModule *g_pBTModule = NULL; // Our interface to the Bluetooth module
StateMachine g_connectionState = Initialize;

/*
 * Setup - main configuration point of our sketch to configure
 *         the Arduino for setting up the bluetooth module
 *         and restoring the connection data if present
 *
 * Params - none
 *
 * Returns - nothing
 */

void setup()
{
  Serial.begin(9600); // for monitoring

  Serial.println("Starting setup...\n");

  g_pBTModule = BTModule::GetInstance(BT_RX_PIN, BT_TX_PIN);

  pinMode(BT_CONNECTED_STATUS_PIN, OUTPUT);

  StoredData.signature = ReadLong(0); 

  // Have we been here before?
  if (StoredData.signature == signature)
  {
    StoredData.valid = ReadInteger((char *)&StoredData.valid - (char *)&StoredData.signature);

    if (StoredData.valid != 0)
    {
      ReadBytes((char *)&StoredData.bt_address[0] - (char *)&StoredData.signature, (byte *)&StoredData.bt_address[0], MAX_BT_ADDRESS);
    }
  }
  else
  {
    // Store signature and default valid as 0 to indicate the address isn't valid
    WriteLong(0, signature);
    WriteInteger((char *)&StoredData.valid - (char *)&StoredData.signature, 0); // default to 0
  }

  // If we are still connected then jump right in
  if (analogRead(BT_CONNECTED_PIN) != 0)
  {
    g_connectionState = ActiveCommunications;
  }

  Serial.println("Setup Completed.");
}

/*
 * Loop   - the main loop which runs our state machine and progresses
 *          through each state establishing a connection with the remote
 *          device and then sending data to the device and receiving data back
 *          from it.
 *
 * Params - none
 *
 * Returns - nothing
 */

void loop()
{
  char *pRemoteAddress = NULL;

  switch (g_connectionState)
  {
    case Initialize:
    {
      Serial.println("Initializing device...");
      digitalWrite(BT_CONNECTED_STATUS_PIN, LOW); // turn off when not connected

      g_pBTModule->begin(BT_COMM_SPEED, true, "ArduinoBT", BT_PIN_CODE); // do we need to block on this?

      g_connectionState = RestoreDeviceAddress;
    }
    break;

    case RestoreDeviceAddress:
    {
      if (StoredData.valid != 0)
      {
        pRemoteAddress = (char *)&StoredData.bt_address[0];
        g_connectionState = DeviceDiscovered;
      }
      else
      {
        pRemoteAddress = NULL;
        g_connectionState = DiscoveringDevice;
      }
    }
    break;

    case DiscoveringDevice:
    {
      Serial.println("Discovering devices...");

      // discover our device, do not block, we will come back to try again
      if (g_pBTModule->discoverDevice(false) == true)
      {
        g_connectionState = DeviceDiscovered;
      }
    }
    break;

    case DeviceDiscovered:
    {
      Serial.println("Connecting to device...");
      if (g_pBTModule->connectToDevice(pRemoteAddress, true) == true)
      {
        g_connectionState = ActiveCommunications;
        digitalWrite(BT_CONNECTED_STATUS_PIN, HIGH); // we have a connection

        // Update eeprom data
        if (StoredData.valid == 0)
        {
            WriteInteger((char *)&StoredData.valid - (char *)&StoredData.signature, 1); // it is now valid
            g_pBTModule->getRemoteAddress((char *)&StoredData.bt_address[0]);
            WriteBytes((char *)&StoredData.bt_address[0] - (char *)&StoredData.signature, (byte *)&StoredData.bt_address[0], MAX_BT_ADDRESS);
        }  
      }
    }
    break;

    case ActiveCommunications:
    {
      char dataValue = 0;

      if (Serial.available())
      {
        g_pBTModule->sendByte(Serial.read());
      }

      if (g_pBTModule->readByte(&dataValue) == true)
      {
        Serial.print(dataValue);
      }
    }
    break;

    case ErrorState:
    {
      // Reset and come back up
      g_connectionState = DeviceDiscovered;
    }
    break;
  }
} 
```

A lot of this code, such as the [EEPROM](#part0006_split_001.html_eeprom) library, has already been covered in previous chapters. There are two key items to look at here. The first is the inclusion of a library that I wrote to work with the Bluetooth® module by Seeed Studio which can be found on [GitHub](https://github.com/milligan22963/Arduion-BT-Module). This library is available for free on github for other's to use and to improve upon. The second key item is the State Machine which I created to track the state of my Bluetooth® connection. This allows the software developer to create a list of instructions i.e. states to follow as the system is processing in order to accomplish a complete task. Basically each step of the state machine is a task which cannot be done in most cases until the previous task is done. The beauty of the state machine is the ability to jump from one state to another in order to redo something or handle error cases and the like. It also fits in nicely with the Arduino® loop function. Given the loop is called continuously, it is quite easy to create a state machine that can progress from one state to the next as the loop is run. In general, the serial communications library has been covered with the Serial functions which stay the same for the software serial port that we are using with this sketch. In particular we will be setting the starting baud rate with the begin function and then sending data using the print function. Likewise, we will be receiving data using the read function.

```
 g_pBTModule = BTModule::GetInstance(BT_RX_PIN, BT_TX_PIN); 
```

The above line of code initializes my Bluetooth® module and returns a pointer that I can use in my code. While this isn't rocket science, I did want to explain a little in more detail the pointer concept and usage. So far we have covered a number of variables such as integers (int), characters (char), and others. A pointer is a little different. It is not so much a data type in itself but more a link to a data type. Imagine a row of mail boxes for a group of houses each with a name on it. The actual mailbox isn't as important as the name beside it since your mail will be placed in the box where your name is. The pointer is similar in that it points to a specific mailbox i.e. memory location that holds the data you are interested in. The beauty of the mailboxes is that if another person builds a house between you and your neighbor, you can simply move the names on the mailboxes around so that the new person's mailbox is in the right spot. It may have been the one you used previously however now your name has been moved over one and points to a new mailbox. This is the same idea behind a pointer in programming. This variable points to a specific spot in memory however you can have multiple spots in memory containing the same type of data. The pointer can point to any of them as needed. To continue the example, imagine each mailbox is actually a Bluetooth® module as defined above. I could have the one pointer variable which could be assigned to any of the Bluetooth® modules and be able to access all of its functionality. This is done by simply changing which module the pointer points to. For example I could do the following (not working code):

```
 BTModule g_BTModule1(3, 4); // Our interface to the Bluetooth module 1
BTModule g_BTModule2(5, 6); // Our interface to the Bluetooth module 2
BTModule g_BTModule3(7, 8); // Our interface to the Bluetooth module 3
BTModule g_BTModule4(9, 10); // Our interface to the Bluetooth module 4
  ...

byte nextChar = Serial.read();

g_BTModule1.sendByte(nextChar);
g_BTModule2.sendByte(nextChar);
g_BTModule3.sendByte(nextChar);
g_BTModule4.sendByte(nextChar); 
```

This works but is a little tedious in that for every specific instance you have to access it directly and if you add or remove an instance then you have to go down through the code to determine every where it has been used and remove it. There is a better way and that way is with a pointer. Again this is just a code snippet and not a complete sketch.

```
 #define BT_MODULE_COUNT 4

// receive and transmit pin assignments
int g_btModulePins[BT_MODULE_COUNT][2] =
{
  {3, 4},
  {5, 6},
  {7, 8},
  {9, 10}
};

// Array of pointers to my modules
BTModule *g_pBTModules[BT_MODULE_COUNT] = {0};

void setup()
{
	for (int index = 0; index < BT_MODULE_COUNT; index++)
	{
		g_pBTModules[index] = BTModule::GetInstance(g_btModulePins[index][0], g_btModulePins[index][1]);
	}

	// Verify that each instance is valid i.e. not NULL.
}

void loop()
{
  ...

  byte nextChar = Serial.read();

  // Blast the value out to every instance
  for (int index = 0; index < BT_MODULE_COUNT; index++)
  {
	g_pBTModules[index]->sendByte(nextChar);
  }

  ...

} 
```

Granted I could still define my number of modules and create the module pin array and utilize it in the first example however the main thing here is that in the first example I had four specific instances of my Bluetooth® module which is rigid in that to add or remove an instance, I have to go back through my sketch and locate all of the places it is used and make the changes which takes time and is error prone. In the above example, I have to make two changes. The first change is to update the definition of BT_MODULE_COUNT to another positive value i.e. something greater than zero (0). The second change is to add or remove pin assignments to match the BT_MODULE_COUNT change. The compiler will warn you if the number of pin declarations doesn't match the value of BT_MODULE_COUNT because I use BT_MODULE_COUNT as part of my pin array definition. Once everything is defined, I can process each instance of the Bluetooth® module to configure it in the for loop. In the main loop function when I read in a value, instead of having to send it to each individual instance, I can simply walk my array of pointers and send to each instance of the Bluetooth® module. This reduces the amount of code that is needed and also makes it quite expandable as only a few changes are required in order to increase or decrease the number of modules to use.

The following is my state machine values which the sketch will progress through in order to initialize and utilize the Bluetooth® module. By default I always start at the Initialize state unless the BT_CONNECTED_PIN indicates the module is already connected. If that is the case then I can jump right to the ActiveCommunications state.

```
 enum StateMachine
{
  Initialize = 0, // if we store the device addr, we can jump to connecting
  RestoreDeviceAddress,
  DiscoveringDevice,
  DeviceDiscovered, // once discovered, we can reconnect without all of the setup
  ConnectingToDevice,
  ActiveCommunications,
  ErrorState,
  EndStates
}; 
```

Each of the above states should be fairly self explanatory. You might notice there is one state which I do not use which is the EndStates. This is really just a habit of mine in that for every enumeration I add a final state indicating the end of the defined states. The main reason for this is so I can do something like the following:

```
 for (int state = Initialize; state < EndStates; state++)
{
  ...

  // do something fabulous

  ...
} 
```

Again this isn't rocket science by any means. I find it useful in that if I add or remove a state, I do not have to go back through my code changing any loops to reflect the added or removed state. The exception of course would be a switch statement where each state is declared so a removal or addition would have to be updated. In this sketch I transition through my states until I reach the ActiveCommunications state. Once in active communications I can read in commands from the USB serial port and send them to the Bluetooth® module for transmission to the OBDII connector. Then when a response is sent back, I can display it back on my computer. For a list of commands that can be used with an ELM based OBDII adapter, see the following link: [ELM Data Sheet](http://elmelectronics.com/DSheets/ELM327DS.pdf).

### SPI

Serial Peripheral Interface, (SPI), is a high speed serial interface used to communicate between devices. This is a full duplex interface meaning that it can transmit and receive at the same time in a number of configurations. A nice feature of SPI is that it can be connected to a number of devices where a chip select is used to select the recipient and/or source of the data. The chip select signal activates the desired device allowing multiple devices to share the same bus. The SPI interface consists of the following connections:

| Signal Name | Alternate Names | Purpose |
| SCLK | None | The clock signal to synchronize the SPI devices |
| SDO | MOSI, DO, SO, etc. | Serial data out from the primary device to the subordinate recipients |
| SDI | MISO, DI, SI, etc. | Serial data in to the primary device from the subordinate devices |
| CS | SS, STE, etc. | Chip select from the primary device which enables i.e. directs the subordinate device(s) to accept the data |

In general usage, you will find SPI referred to as a four (4) wire interface given all of the signals above. In some cases, SPI may be used in a three (3) wire configuration where the SDO and SDI lines are combined. In addition there will be the chip select (CS) line indicating the direction of data flow along with the clock signal to keep everything aligned. And in some cases, i.e. the three (3) wire mode, the two data lines are integrated together at the device and on the host system i.e. the Arduino® in this case, a resistor is used to connect the input and output pins. The data flows according to commands issued on the SPI bus. In this case, the host controller will issue a read or a write command and will then expect the data to flow back based on the command written. And finally in some cases, there is never any data coming back from the recipient device(s) resulting in only three (3) wires needed to perform communications.

In addition to the signal names defined above, there are different modes of operation of the SPI bus. In particular you can set the speed of the communications, the polarity of the clock signal in respect to the data along with the phase of the clock in respect to the data. These may sound complicated however it basically means when to capture the data i.e. trigger the reading of the data on the rising edge of the clock signal or the falling edge. This is defined as the phase and it will be dependent upon the polarity of the clock signal which is to say trigger when the clock is either low or the clock is high. For complete details visit: [SPI Wiki](http://en.wikipedia.org/wiki/Serial_Peripheral_Interface_Bus).

The following table details the configurations per the Arduino® documentation.

| Mode | Clock Polarity | Clock Phase |
| 0 | with 0 indicating a low value as the base of the clock and data valid during its high value state | with 0 indicating data is captured when the clock transitions from low to high which is at the beginning of the clock high value state |
| 1 | with 0 indicating a low value as the base of the clock and data valid during its high value state | with 1 indicating data is captured when the clock transitions from high to low which is at the end of the clock high value state |
| 2 | with 0 indicating a high value as the base of the clock and data valid during its low value state | with 0 indicating data is captured when the clock transitions from low to high which is at the beginning of the clock low value state |
| 3 | with 0 indicating a high value as the base of the clock and data valid during its low value state | with 1 indicating data is captured when the clock transitions from high to low which is at the end of the clock low value state |

Note: This table is valid for Atmel® micro-controllers and some others but may be different depending on what micro-controller you are using.

Another consideration to take into account is the ordering of the data bits going along the SPI bus. Because it is serial, the bits will have to flow in order and the order can be important. When looking at a byte of data, there is a significant bit i.e. the high bit (most significant bit) and a low bit i.e. the least significant bit. The SPI bus can transfer data in most significant bit order where the largest bit is sent first or it can send it in least significant bit order where the lowest significant bit is sent first. Typically you will be sending data most significant bit first however you will want to be aware of the order of any devices that you communicate with over SPI. In some cases it can be difficult to determine the proper order and some trial and error will have to be done to determine the proper settings.

The last configurable piece of the SPI puzzle is the speed at which the clock transitions from low to high. This is the frequency of the device and can be as fast as 25 MHz and perhaps more depending on the device. The speed of the SPI bus in terms of the Arduino® is flexible to allow interfacing with a variety of devices. Again, you will need to look at the documentation for the device that you are connecting to in order to configure your Arduino® for the correct speed. The following are the valid clock dividers for the SPI bus and the bus speeds assuming a 16 Mhz clock.

| Name* | Value | Speed |
| SPI_CLOCK_DIV2 | 2 | 8 Mhz |
| SPI_CLOCK_DIV4 (default value) | 4 | 4 Mhz |
| SPI_CLOCK_DIV8 | 8 | 2 Mhz |
| SPI_CLOCK_DIV16 | 16 | 1 Mhz |
| SPI_CLOCK_DIV32 | 32 | 500 Khz |
| SPI_CLOCK_DIV64 | 64 | 250 Khz |
| SPI_CLOCK_DIV128 | 128 | 125 Khz |

The Arduino® DUE is a little different in that you specify the slave select pin and the divider value which is any value between 0 and 255. The default value for the DUE is 21 which sets the speed to 4 Mhz which is the default of the other Arduino® boards.

So SPI seems to be fairly straight forward in terms of a small number of wires to connect along with a ready to use library to interface with it. However, where would we use it? There are any number of uses for the SPI bus and any number of devices that support it which can be beneficial when the number of data lines on your micro-controller is limited. For our use case, we will be interfacing to a digital potentiometer which will allow us to control the intensity of light being displayed by our tricolor LED's. A lot of LED's that are available control brightness by using Pulse Width Modulation (PWM) however that is a simulation by pulsing the LED on and off real quickly to trick your eye into seeing a dimmer color. Using a potentiometer will limit the amount of voltage being dropped across the LED therefore reducing the amount of current flowing through the LED resulting in a lower intensity glow. Typically you will not be able to see the difference however if you were to use a camera you might catch the LED in the off state and if taking video of an LED most likely will catch it both on and off.

#### Required Components

*   Arduino® Board
*   (2) 150 Ohm Resistor
*   270 Ohm Resistor
*   2N2222A Transistor
*   Standard 5mm red light emitting diode (LED)
*   10K digital potentiometer [[18](#part0012_split_001.html_Ref18)]

#### Tools

*   breadboard
*   jumper wires
*   voltage meter

#### Schematic

![SPI Digital potentiometer](images/00029.jpeg)

![Creative Commons - Attribution - Share Alike](images/00005.jpeg) Image created using: [Fritzing](http://fritzing.org/)

#### Software

For this sketch we will be utilizing the SPI bus to communicate with a digital potentiometer in order to control the brightness of an LED. We will use a transistor to control the current through the LED and will wire the digital potentiometer such that it will control the saturation of the transistor based on its voltage level which will be programmed. This method of control is a little more complicated then using PWM however you have the ability of controlling a number of different devices with the same communication bus.

```
 /*
 * SpiDigitalPot - the purpose of this sketch is control the brightness of an LED
 *                 by configuring a digital potentiometer to set the brightness.
 *
 * potCS pin is the pin I am using as the chip select for the potentiometer.
 *
 * spi
 *    - spClk - is the pin that the SPI clock is configured for
 *    - spiMosi - is the pin that the master device (Arduino) transmits data to the slave device
 *    - spiMiso - is the pin that the slave device sends data to the master device (Arduino)
 *    - spiCS - is the chip select for the SPI circuit in the Arduino
 *            - I could use the spiCS chip select also for my POT given I only
 *              I only have one SPI device in use at this time.  Various shields will
 *              use specific pins as the chip select which most likely will not be pin 10
 *
 * tested with MCP4261 digital potentiometer from Microchip
 */

// include the SPI library:

#include <SPI.h>

/* constant defines */

const int potCS = 6;
const int spiClk = 13;
const int spiMosi = 11;
const int spiMiso = 12;
const int spiCS = 10;

/* Variables for this sketch */

byte g_potValue = 0;

/*
 * Data structures to send commands to
 * the digital potentiometer
 */

 /* The command Byte is the main address/data bits to send to the pot */

typedef struct _CommandByte
{
  byte Address:4;  /* the address to select */
  byte Command:2;  /* the actual command to send */
  byte DataBits:2; /* the upper data bits */
} CommandByte;

/* The combination command byte with data to send */

typedef struct _CommandData
{
  union
  {
  	/* The command byte as defined above */
    CommandByte cmd;

     /* The cmd byte in standard byte format for easy access */
    byte cmdByte;
  } command;

  /* The data to be sent with the command as needed. */
  byte        data;
} CommandData;

/*
 * Method declarations
 */

void UpdatePot(int selectPin, struct _CommandData *pData);
int ReadPot(int selectPin, struct _CommandData *pData);

/*
 * UpdatePot - sends commands and data to the potentiometer
 *             which is activated by the specified chip select
 *
 * Params
 *  selectPin - the pin to use as the select pin
 *  pData     - pointer to the command data stucture to be sent
 *
 * Return
 *  none
 */

void UpdatePot(int selectPin, struct _CommandData *pData)
{  
  digitalWrite(selectPin, LOW);

  delay(100); // required delay

  SPI.transfer(pData->command.cmdByte);
  SPI.transfer(pData->data);

  digitalWrite(selectPin, HIGH);
}

/*
 * ReadPot   - sends commands and data to the potentiometer
 *             which is activated by the specified chip select
 *
 * Params
 *  selectPin - the pin to use as the select pin
 *  pData     - pointer to the command data stucture to be sent
 *
 * Return
 *  int       - the value read back from the pot
 */

int ReadPot(int selectPin, struct _CommandData *pData)
{
  int dataRead = 0;

  digitalWrite(selectPin, LOW);
  delay(100);

  dataRead = SPI.transfer(pData->command.cmdByte) << 8;
  dataRead |= SPI.transfer(pData->data);
  digitalWrite(selectPin, HIGH);

  dataRead &= 0x1FF;

  return dataRead;
}

/*
 * Enumerations for clarity of code
 */

/*
 *  This enum is a definition of each address that can
 *  be accessed on the potentiometer
 */

typedef enum
{
  Wiper0 = 0,
  Wiper1,
  NVWiper0,
  NVWiper1,
  TConReg,
  StatusReg,
  Data0,
  Data1,
  Data2,
  Data3,
  Data4,
  Data5,
  Data6,
  Data7,
  Data8,
  Data9,
} Addresses;

/*
 *  This enum is a definition of each command that can
 *  be sent to the potentiometer
 */

typedef enum
{
  WriteData = 0,
  Increment,
  Decrement,
  ReadData
} Commands;

/*
 * Setup - main configuration point of our sketch to configure
 *         the Arduino for SPI communications with the potentiometer
 *
 * Params - none
 *
 * Returns - nothing
 */

void setup()
{
  Serial.begin(9600);

  pinMode(spiCS, OUTPUT);
  pinMode(potCS, OUTPUT);

  digitalWrite(potCS, HIGH);

  /* Configure SPI */
  SPI.begin();

  SPI.setBitOrder(MSBFIRST);
  SPI.setDataMode(SPI_MODE0);
  SPI.setClockDivider(SPI_CLOCK_DIV128);

  // Configure pot outputs
  CommandData command;

  command.command.cmd.Command = WriteData;
  command.command.cmd.Address = TConReg;
  command.command.cmd.DataBits = 0;
  command.data = 0xFF;

  // Configure the pot to enable each output
  UpdatePot(potCS, &command);

  command.command.cmd.Command = ReadData;

  // Read back in the tcon register
  int tconValue = ReadPot(potCS, &command);

  Serial.print("TCON: ");
  Serial.println(tconValue);
  Serial.println("Setup completed");
}

/*
 * loop - main method which will be called each time the
 *        Arduino goes through its main loop which will set
 *        the value of the digital potentiometer which
 *        will vary the intensity of the LED based on the
 *        value written to the potentiometer.  The larger
 *        the value written to the potentiometer, the dimmer
 *        the LED as the transistor saturation is lower.
 *
 * Params - none
 *
 * Returns - nothing
 *
 * Note:  The pot is 9 bits but we are only using the lower 8
 */

void loop()
{
  CommandData command;

  command.command.cmd.Command = WriteData;
  command.command.cmd.Address = Wiper0;
  command.command.cmd.DataBits = 0; // clear the upper bit(s)
  command.data = g_potValue;

  // Send the command to the pot updating the value
  UpdatePot(potCS, &command);

  // Note the current value that was sent to the pot
  Serial.println(g_potValue);

  // Delay 250 ms so we can see the changes
  delay(250);    

  // let it roll
  g_potValue += 25;
} 
```

In this sketch we have introduced a few new things, namely the SPI bus. First I have defined two structures to assist in sending data to the potentiometer. The structures are as follows:

```
 /* The command Byte is the main address/data bits to send to the pot */

typedef struct _CommandByte
{
  byte Address:4;  /* the address to select */
  byte Command:2;  /* the actual command to send */
  byte DataBits:2; /* the upper data bits */
} CommandByte;

/* The combination command byte with data to send */

typedef struct _CommandData
{
  union
  {
      /* The command byte as defined above */
    CommandByte cmd;

    /* The cmd byte in standard byte format for easy access */
    byte cmdByte;
  } command;

  /* The data to be sent with the command as needed. */
  byte        data;
} CommandData; 
```

The first structure defines one byte which will consist of the address we are interested in accessing on the device, the command we are sending, and the upper two data bits of which the highest one is not used. Although I have defined what looks like three (3) bytes of data in this structure, CommandByte, I have actually only defined one (1) byte which is made up of the three defined fields. You will notice that the total bits defined is equal to the same size as a byte i.e. eight (8) bits. I could have written a macro of the like to set the value for the address and the command however it isn't very clear to someone coming along after what is happening. By using the power of the language and the compiler, I can write code that is clear and easy to work with. The second structure is basically two bytes, the first byte is the command byte which contains the address and the command. The second byte is the data byte to send to the device. I am also using a union to allow easy access to the CommandByte which also allows me to simply pass the cmdByte value to the SPI transfer routine. A union is programming construct that allows you to declare multiple ways of accessing the same data. In this case the command byte, CommandByte, can be accessed via the individual bit fields i.e. Address, Command, and DataBits or it can be accessed all at once via the cmdByte field. The union allows you, the developer, to access the value as needed.

The enumerations are provided for code clarity and being able to easily specify what command I want to issue and what address I want to issue it to. I could use simple integer values however the benefits of the enumerations are much easier to read and in some high level programming languages provide additional benefits such as compile time type validation.

The next thing to look at is the configuration of the SPI bus.

```
 pinMode(spiCS, OUTPUT);
  pinMode(potCS, OUTPUT);

  digitalWrite(potCS, HIGH);

  /* Configure SPI */
  SPI.begin();

  SPI.setBitOrder(MSBFIRST);
  SPI.setDataMode(SPI_MODE0);
  SPI.setClockDivider(SPI_CLOCK_DIV128); 
```

In the above code, the first thing we do is configure the SPI chip select line as an output. Regardless of whether you will be using spiCS pin itself or another pin, this pin must be configured as an OUTPUT pin otherwise the SPI bus will not work. I am also setting the potentiometer chip select to HIGH to ensure that nothing spurious on the SPI bus is transferred to the digital potentiometer. Once the selection pins are configured, I start the SPI communications and then configure it for use with my device. In this case, my device, the MCP4621, utilizes the most significant bit (MSB) data format. I have also configured the SPI bus to use data mode zero (0) which was defined in the table above. I then specify the clock divider to lower the speed of the SPI bus. In this case I am dividing my base system clock by 128 resulting in a 125KHz clock speed. I could push the device much faster, up to 10MHz however for what I am doing, speed isn't a great concern.

Finally, once I have configured the SPI bus, I can read and write data to it. The following code demonstrates transferring data via the SPI bus.

```
 void UpdatePot(int selectPin, struct _CommandData *pData)
{  
  digitalWrite(selectPin, LOW);

  delay(100); // required delay

  SPI.transfer(pData->command.cmdByte);
  SPI.transfer(pData->data);

  digitalWrite(selectPin, HIGH);
} 
```

The first thing we must do is select the proper device that will be receiving the data that we are going to write out on the SPI bus. I have added a delay after the selectPin has been driven to a low state i.e. selected. This delay, while not overly necessary, just ensures that the device to receive the data has time to prepare to receive it. Typically there will be a delay needed that is in the 10's of nanoseconds however the delay I am using is more than sufficient and for what we are doing here, not noticeable. If you were writing data to a strip of LED's which had to change color very rapidly, I would reduce this delay and would also raise the clock speed to as high as the LED strip could handle. Each application requires different configuration settings. Once I have the select pin in the proper state, I then transfer the command byte and the data to the digital potentiometer. Once the data has been transferred, I then place the select pin back to the HIGH state disabling the SPI interface of the recipient device. One thing to note, that each transfer of data on the SPI bus may result in data being read back in as part of the transfer. It will be up to the programmer to determine if this is the case or not based on what is being sent to the recipient device i.e. the digital potentiometer.

All in all, the digital potentiometer is a decent device to control the intensity of an LED among other things. In this particular case, the MCP4621 can also be used to store a small amount of data that could be associated with the device itself in order to persist values that could be used regardless of which micro-controller the component was connected to. In addition to it being a decent device, the fact that it can be accessed with the SPI bus makes it easy to interface with. So what happens when you don't have an SPI bus to interface with? You make your own! This will work with a number of SPI bus devices however if the particular device that you are using requires a high speed bus, than this method may not work properly. In highly technical terms, this method is fondly called Bit Banging. This is where you programmatically simulate the SPI bus using standard I/O pins.

```
 /*
 * TogglePin quickly toggles a pin from low to high back to low
 * Assumes the pin is starting off as low
 */

void TogglePin(int pinId)
{
	digitalWrite(pinId, HIGH);
	digitalWrite(pinId, LOW);
}

/*
 * SendData sends a byte of data out a specific pin.
 *
 * Params
 *  selectPin 	- the pin to select the device to receive the data
 *  dataPin 	- the pin which is where the data will be serialized out over
 *  clockPin 	- the pin which we will toggle to simulate the clock
 *  data		- the data to be sent out
 *
 * Returns
 *  None
 */

void SendData(int selectPin, int dataPin, int clockPin, byte data)
{
	// Select the device - assumes device is active low i.e.
	// it is listening when this pin is at a LOW state
	digitalWrite(selectPin, LOW);

	pinMode(dataPin, OUTPUT);

	// Send MSB first
	for (int index = 7; index >= 0; index--)
	{
		// Shift the 1 into position to see if that bit in the passed in data is high or low
		if (data & (1 << index))
		{
			digitalWrite(dataPin, HIGH);
		}
		else
		{
			digitalWrite(dataPin, LOW);
		}

		// Once the data pin is in the proper state, toggle the clock pin
		TogglePin(clockPin);
	}

	// Once done, de-select the device
	digitalWrite(selectPin, HIGH);
}

/*
 * SendData sends a byte of data out a specific pin.
 *
 * Params
 *  selectPin 	- the pin to select the device to receive the data
 *  dataPin 	- the pin which is where the data will be serialized out over
 *  clockPin 	- the pin which we will toggle to simulate the clock
 *  command		- the command to send for requesting data
 *
 * Returns
 *  byte		- representing the value read in from the remote device
 */

byte ReadData(int selectPin, int dataPin, int clockPin, byte command)
{
	byte response = 0;
	byte bitValue = 0;

	SendData(selectPin, dataPin, clockPin, command);

	pinMode(dataPin, INPUT);

	digitalWrite(selectPin, LOW);

	for (int index = 7; index >= 0; index--)
	{
		TogglePin(clockPin);

		bitValue = digitalRead(dataPin);

		if (bitValue == HIGH)
		{
			response |= (1 << index); // set the bit if the value was high
		}
	}

	digitalWrite(selectPin, HIGH);
	return response;
} 
```

This method can be a really quick way to simulate an SPI bus without actually using SPI. The major downside is that it is much slower than a true SPI BUS and is not as flexible. In particular, it is great for sending data to a device but not quite as convenient for reading data back in. Typically you will have to send out a command to the device in order to have it send back the response. While not a big issue if the target device multiplexes the MOSI pin with the MISO pin, than you will have to configure the data pin for output when sending the command and than reconfigure it for input when receiving the data back from the target device. Of course you can always have the data read back in via a different I/O pin of the Arduino® too. This can be considerably slower and prone to timing issues.

### I2C

Inter-integrated circuit, (I2C), is another serial data communication interface used between peripheral devices. I2C utilizes two signals which are as follows:

| Signal Name | Purpose |
| SCL | The clock signal to synchronize the I2C devices |
| SDA | Serial data line between the primary and subordinate devices |

In a lot of respects, I2C is very similar to SPI in three (3) wire mode where it consists of a synchronization clock and a data line used for both transmission and reception. The main difference is that I2C does not have a dedicated chip select line and instead relies on addressing within the data to indicate which device the data is intended for. I2C currently is not as fast as SPI however for most applications this will probably be a moot point. Because I2C only utilizes a clock and a data line i.e. it doesn't include a chip select, the data sent includes the address of the recipient. This address is typically 7 bits following the start bit. This allows the controlling device to select which recipient device will receive the command / data. It is good to note that while only one device may be the intended recipient of the sent data, any device on the same bus will see the same data that is sent. The devices that don't have the same address as the target device should simply ignore the data. There are other addressing schemes including 10 bit addressing and as much as 16 bit addressing. In all cases it is dependent upon the device(s) being used and the data sheet for the specific device should be consulted prior to use. On the Arduino®, the addressing used is seven (7) bits. It is recommended on the Arduino® website to shift an eight (8) bit address down by one (1) bit in order to convert it to a seven (7) bit address.

The following table identifies the pins which the various Arduino® modules utilize for I2C communications.

| Arduino® | SDA | SCL |
| UNO R3 | A4 | A5 |
| Leonardo | 2 | 3 |
| DUE | 20, SDA1 | 21, SCL1 |
| YUN | 2 | 3 |
| MEGA 2560 | 20 | 21 |

For our purposes, we will interface with an LCD panel that implements an I2C interface. This will allow us to write out status information to a screen other than the serial port connected to the programming computer. This will allow an easier time debugging your projects and will provide feedback regarding the activity of your device(s). The particular screen that I will be using is based off of the SH1106[[19]](#part0012_split_001.html_Ref19) controller chip.

#### Required Components

*   Arduino® Board
*   OLED LCD, 128x64 based on the SH1106 controller chip

#### Tools

*   breadboard
*   jumper wires
*   voltage meter

#### Schematic

![I2C display](images/00030.jpeg)

![Creative Commons - Attribution - Share Alike](images/00005.jpeg) Image created using: [Fritzing](http://fritzing.org/)

#### Software

For this sketch we will be utilizing the Wire library in order to communicate over the I2C bus. The first thing I found when programming this device is that the board is 128x64 pixels however a lot of the documentation I had seen indicated it supported 132x64\. After monkeying with some weird display issues I found it was indeed 128x64\. I created a library to work with the display which can be downloaded from the web [[20]](#part0012_split_001.html_Ref20). The main Arduino® sketch is fairly minimal mostly for testing out my library for proper operation. In the above graphic you can see that in terms of connections, there are not a lot. The bottom row of the image showing pins 1 through 20 are internal to the board. The board I have has four (4) pins that can plug into a breadboard and cover the voltage, ground, SCL, and SDA pins.

For the code, I will focus more on the Wire library opposed to the code I wrote to work with it. However I will go through a few of the routines that will interface with the Wire library.

```
 typedef enum
{
    StartSend = 0,
    MidSend,
    FinishSend,
    Complete
} SendState;

/*
 *  Send Command - used to send a command byte to the LCD
 *
 * Params
 *      command - the command to be sent
 *      state   - the state of the transmission
 *
 *  Returns
 *      byte - the return value from the transmission
 */

byte sh1106_lcd::SendCommand(byte command, SendState state)
{
    if (state == StartSend || state == Complete)
    {
        Wire.beginTransmission(SH1106_ADDR1);
        Wire.write(SH1106_COMMAND);
    }

    return SendByte(command, state);
}

/*
 *  Send Data - used to send a data byte to the LCD
 *
 * Params
 *      data - the data to be sent
 *      state   - the state of the transmission
 *
 *  Returns
 *      byte - the return value from the transmission
 */

byte sh1106_lcd::SendData(byte data, SendState state)
{
    if (state == StartSend || state == Complete)
    {
        Wire.beginTransmission(SH1106_ADDR1);
        Wire.write(SH1106_DATA);
    }

    return SendByte(data, state);
}

/*
 *  Send Byte - used to send a byte to the LCD
 *
 * Params
 *      data - the data to be sent
 *      state   - the state of the transmission
 *
 *  Returns
 *      byte - the return value from the transmission
 */

byte sh1106_lcd::SendByte(byte data, SendState state)
{
    Wire.write(data);

    byte transmissionStatus = 0;

    if (state == FinishSend || state == Complete)
    {
        transmissionStatus = Wire.endTransmission();
    }

    return transmissionStatus;
} 
```

In the above code, I have written two main methods to send commands and data to the LCD and a third method which will be utilized by each of the other two methods. Because we can send both data and commands to the controller chip, I have two separate methods to handle that with the only difference being the first value written out onto the I2C bus indicating whether the following byte is a command or is data. I am sure there other ways I could have done it to conserve space however I chose this way as it is clear in regard to my intent. I did create a third method, SendByte which is used by each of the other methods in order to reduce the code size when and after data is sent. The other item of interest in this code is the send state SendState enumeration which I am using to track what state I am in terms of sending data to the I2C device. I am doing this for potential speed savings when writing to the end device as some devices can accept a number of commands or data values in one transmission sequence. The Wire library can buffer up to thirty two (32) bytes of data in its transmission queue to send out at one time. As can be seen above, the starting of the send along with the finishing of the send adds overhead and for every single byte of data, this can add up to a lot of activity on the I2C bus unnecessarily. So to alleviate this, I created a simple enumeration in the code to track what state I am in and cut down on the number of bytes being sent over the bus to improve overall throughput.

So now that I have given you some of the background of how the Wire library is used, lets dig a little deeper. So how did I know how big the buffer inside of the Wire library was? I looked. Each of the libraries that you can import right out of the box reside on the local machine where the Arduino® application resides. On my Windows™ machine, I found it in the C:\Program Files (x86)\Arduino\libraries\Wire. For the Macintosh™ system it was located inside of the Arduino® package which you can view by Control - Clicking the mouse button and selecting the Show Package Contents option on the context menu that comes up. Doing this should then show a folder Contents which has inside it a number of folders. If you open the folder Resources you should find another folder entitled Java. Inside the Java folder is a file structure very similar to the PC based system including the libraries folder which contains the Wire folder. Inside of this folder, Wire, there is another folder called utility which contains support files for the Wire library. This code is the base two wire code, TWI which is the closest we get to the hardware.

While that was a lot of digging around, it is always good to know how the libraries that you are depending on work. In this case, one key issue I had was the amount of data I could queue up before sending. The standard serial library can queue up around 64 bytes however this library, Wire has a maximum buffer size of 32 bytes. Always a good thing to know when trying to send 1024 bytes of screen data over a slow bus. The 1024 bytes of data comes from my internal buffer that I use to track the state of each pixel on the LCD. If you look within the class I created for the sh1106, you will find the following:

```
 // 1024 bytes 8 pages of 128 bits

byte m_screen[MAX_PAGE_COUNT][SCREEN_WIDTH]; 
```

Not one of my longer comments for sure however it does sum things up in that there is 1024 bytes to cover the 8 pages of memory which are each 128 bits wide. This buffer allows me to queue up a number of higher level commands such as DrawPixel, DrawLine, etc. before sending the data down to the actual device. This saves some time however can lead to some mysterious bugs such as a figure being hidden by another figure due to the ordering of the drawing. In this case, user beware given the resource constraints of the system and the limitations in general of the environment.

Now the next thing to look at is the details of the Wire class. The first thing to do when using the library is to start the transmission by calling the method:Wire.beginTransmission(SH1106_ADDR1). This call includes the address of the device I want to communicate with making my Arduino® the master and the LCD the slave. Once I start transmission, I can then send the byte of data representing a command or data message that will follow. This is done with the simple Wire.write(SH1106_COMMAND) or Wire.write(SH1106_DATA) function call. Once I have done that I can then send a number of data bytes associated with the command or data flag. Once I have sent all of my data I will call the Wire.endTransmission() to finish the transmission of the data which will also return a status byte indicating if there were any errors. In general that is how easy it is to use the Wire library. In addition to the calls detailed above, there are a number of standard I/O style calls inherited from the Stream class like read, write, seek, etc. The last method I will highlight is the requestFrom(address, quantity) where the address which should provide the data and the quantity being the number of bytes that we expect to receive back from said device. This allows us to read data back from an I2C device.

### Summary

As can be seen, there are a number of ways to communicate with external devices including additional protocols not detailed above such as [SATA](http://en.wikipedia.org/wiki/Serial_ATA), [PCI Express](http://en.wikipedia.org/wiki/PCI_Express) and others. Most of these are standard in a PC type setting but not always found in an embedded micro-controller. In terms of an embedded micro-controller such as the Atmel® device used on the Arduino® the above communication methods will be the most common and easy to interface with. We also looked at both SPI and I2C which are quite similar to each other but do have various pro's and con's.

| Protocol | Pro's | Con's |
| Serial | Simple and quite ubiquitous. Has both standard and TTL interfaces. | Somewhat slow. Not good for any type of broadcasting i.e. sending data to multiple devices at the same time unless you have a special adapter. |
| SPI | Speed. Can run very fast and can use the same clock and data line to communicate with a number of devices. | Requires a dedicated select pin for each device participating on the SPI bus. |
| I2C | Can be faster than Serial but not up there with SPI. Only uses two wires as the target device address is part of the data that is transmitted. | Potential for conflicts when trying to send data when another device is already using the bus. Not as fast as SPI. |

![chapter end graphic](images/00001.jpeg)

# Storage

## Bits and Bytes

Storage is another area where the Arduino® and more importantly, the Atmel® micro-controller really shines. The main device on each of the boards has the capability to store program code, variables, and semi-permanent data.

### Flash Memory

Flash memory is where your application code will be stored and loaded from during program execution. This memory is persistent and can be reprogrammed numerous times. In order to program this memory, the device has to be configured appropriately and then programmed. Programming of the Arduino® boards is typically done directly through the Arduino® IDE using the USB port of your development computer attached to the board being programmed. Once programmed, the device will maintain this memory even when power is lost. This type of memory is fairly slow compared to other types of memory. This memory is split into two sections, a boot loader and then an application area. The size of each is configurable to accommodate the various needs of the boot loader and the application code. The main thing to be aware of is that the size of your end application has to be small enough to fit into the application code area taking into account the amount of size used by the boot loader.

#### Boot Loader

The boot loader is special software that allows the micro-controller to reprogram itself. You may see advertisements for Atmel® devices where it states that it has the Arduino® boot loader programmed in. This boot loader is what allows the Arduino® to be programmed from the IDE. While I wont go to deep into the details of everything that the boot loader does, the primary purpose is to check if a reprogram cycle is being requested and if not then to launch the application code that has been stored in the application section of the flash memory. Because the boot loader and application code share the same flash memory, keeping the size of the boot loader to a minimum is usually considered best practice. For your own projects, this may not be a requirement depending on the size of your application software. For more details of what goes into a boot loader for an Atmel® type micro-controller, take a look at the following [Design Note (32)](http://www.avrfreaks.net/modules/FreaksFiles/files/419/DN_032.pdf).

#### Application Code

The application code area is where all of the end user's application code is stored. It can be reprogrammed by the user via the IDE or other means such as from the command line using a program like avrdude[[13](#part0012_split_001.html_Ref13)]. This memory is persistent in nature where it will retain the programming for a number of years well beyond the typical life span of the product. The application code is called by the boot loader once the boot loader determines that the user does not want to reprogram the device. For our applications, this would be the setup and loop methods we created along with any additional libraries we may have used and the base Arduino® code.

### SRAM

The static random access memory, SRAM, is where all of the application data is stored during the execution of your application. Unlike the flash memory, it can be written to fairly fast and the device doesn't need to be configured in any specific way to do this. The down side of SRAM is that if power is lost, the memory contents are lost unless there is a battery installed in the system to preserve it. This makes it good for run time data however not so good for long term storage. Another thing to note regarding SRAM, and RAM in general, is that it will typically power on with arbitrary values contained within it. This is why it is always good idea to initialize your variables when they are first declared to ensure the value stored there is something reasonable given its purpose. While this memory is called static it is not persistent. The name static indicates that the memory does not have to be refreshed periodically to retain its data. The complimentary memory to static is dynamic memory. Dynamic memory requires that a memory controller refresh the data periodically in order to maintain its state. I won't get too deep into the details however it should be noted that dynamic memory, DRAM, circuits are smaller then their SRAM counterparts resulting in higher densities and thus cheaper memory. Typically you will find DRAM in computer systems as the main memory or used in conjunction with video cards or other peripherals.

The other downside to SRAM for the Atmel® micro-controllers is that is very limited in size. When developing your applications i.e. sketches, you will want to ensure that you keep your memory usage fairly conservative. In the chapter, [Communications](#part0007_split_002.html_i2c), I created a library for an LCD which uses 1024 bytes of SRAM to store the current screen image. For the Arduino® UNO, this was half of all the memory my board had!

### EEPROM

Electrically erasable programmable read only memory or EEPROM is a good compromise between flash memory and SRAM. Like flash memory, it is persistent and can be written to although is fairly slow. Unlike flash memory, the EEPROM cannot store program code as the micro-controller cannot directly execute code stored in EEPROM. You could load it from EEPROM and place it into SRAM however that is a bit beyond what I want to cover at this time. Like SRAM, it doesn't require any special configuration and can be directly written to by the application code. This makes the name somewhat a misnomer in that it isn't quite read only any longer however in general usage, it will be written to in order store configuration or other persistent data that is read more often then written to. Typically I would use EEPROM memory area for storing items such as a serial number, board configuration, or other somewhat static data. The Arduino® UNO™ micro-controller has 1K (1024 bytes) of EEPROM memory available to it. Given the various temperature circuits we have looked at, we could use this memory to store the high and low temperature for each day throughout a given year. Over time we could see the range of temperatures and could offload the data to a computer for further processing.

As seen in previous chapters, the Arduino™ has a rich set of libraries to work with various aspects of the micro-controller. For the EEPROM, the following library is included:

```
 #include <EEPROM.h> 
```

which allows us to simply write and read to and from the EEPROM like most any other memory using a couple of provided commands.

```
 byte dataValue = EEPROM.read(offset);
			EEPROM.write(offset, dataValue); 
```

The only downside with the EEPROM library is that you must manage the offset into the storage area yourself. This however isn't a major concern given the amount used is typically low and helper functions can be written as I have done in the chapter on [interrupts](#part0006_split_001.html_rotaryencoder).

### I/O Memory

This is memory or memory like data located external to the micro-controller and is accessed by mapping it through the I/O registers. This could be done for a number of devices such as an LCD panel or other device that has a data bus. Because we are using an Arduino®, I am not going to delve into this particular area other than to say it can be used with the Arduino® however the number of I/O pins required to operate it quickly grows limiting your options.

### External Memory

In addition to the memory that is internal to the micro-controller, additional memory can be utilized by the Arduino® using various communication interfaces such as SPI, I2C, etc. One example of this is the SD micro-card that can be accessed depending on what shield is being used in conjunction with the Arduino®. Previously we have utilized an SPI based digital potentiometer which also contained persistent memory. Another example would be a real time clock RTC where the system has an external battery and crystal to keep the time while the system is powered off.

### Summary

In this chapter we have looked at the various types of storage available to the Arduino® and how they are typically used. In general, the FLASH, SRAM, and EEPROM are the main types of memory you will use most often. Of the three, EEPROM is the one that will most likely be used the least however it will be very convenient when you need to persist data between application runs. SRAM will be the one that you wish you had more of while the FLASH memory will probably be sufficient for your application needs.

![chapter end graphic](images/00001.jpeg)

# I/O Expansion

## When one just isn't enough

Ensuring that you have identified all of the functions that you need up front is always a good idea when working with a micro-controller. Not having to go back and rework your complete design because you need another output line is best to say the least. Of course not having to buy more computing power than you need is always good too, especially if you plan on building a number of the same items. For the next project I have in mind, I want to add two, seven segment, displays to the pinewood derby car's my children are making. In order to do this, I will need two of the seven segment displays representing each digit along with an Arduino® to drive them. Because weight and size is a concern, I want to utilize the smallest Arduino® that I can while still having enough I/O's to drive the displays. For good measure, I also want to add two headlights because I can. I think this will also look very cool so there you go. With all of that, I need 14 digital outputs to drive each of the segments of the displays along with two additional outputs for the headlights. So overall I needed 16 digital outputs to drive all of the lights I have in mind. I also would like to flash the lights on and off and perhaps do some sequencing through the displays in order to catch the eye of the onlookers.

### Requirements

The first thing I need to do is ensure I capture all of my requirements so I know what I need up front. From there I can look at what pieces of hardware I will need. The following is my first pass at some requirements.

*   16 digital outputs
*   Interrupt to update the displays
*   Input to trigger the head lights
*   Input to set the display value from 00 to 99
*   Expansion board to mount the seven segment displays and the headlights

As mentioned before, the digital I/O pins will drive the individual segments of the displays and will also be used to turn on and off the headlights. I am thinking perhaps I could use a photodetector to determine when the headlights should be turned on. In addition, having a way to set the displays to a value dynamically would be very beneficial as I can then use the same code regardless of which car is adorned with the electronics. I can also change the assigned number to whatever the race officials assign to each child's car. Given all of the pieces I will need to do this, I had better plan on having an expansion board to hold the additional components given a bread board will not fit on the derby car and would likely push me over the maximum weight limit.

### Constraints

With all of the requirements captured, I now need to look at what constraints I have in order to meet all of my requirements but not exceed any of the constraints that I have.

*   Cost - I need to create 4 of these
*   Size - this needs to be mounted to a pine wood derby car which has a width of 1.75" and a length of 7.0"
*   Weight - a pinewood derby car is limited to 5 ounces
*   Reproducible - I need to make 4 of these and simplicity is always a good thing

So of the all of the constraints that I have, cost is the one that is the most flexible. The size and weight are hard and fast rules set by the derby regulations. While I could possibly do something with reproducibility in mind, I only need four (4) so in the long run that will not be as important to me.

### Design

With my requirements and constraints detailed, I can now start looking at a design that will meet my needs. The first thing is to decide which Arduino® will meet my needs while not breaking the bank in terms of cost. The most common choices are as follows:

| Board | Digital I/O | Interrupts | Analog Inputs | Length (In) | Width (In) | Cost * |
| NANO | 14 | 2 | 8 | 1.7 | 0.7 | $25.00 |
| UNO | 14 | 2 | 6 | 2.95 | 2.1 | $30.00 |
| MEGA | 54 | 6 | 16 | 4.25 | 2.1 | $60.00 |

* Cost is variable and will depend on when and where you purchase it. I am listing some average prices I have seen online however I expect that you can find better pricing if you shop around. There is also the Arduino® Pro Mini from Sparkfun Electronics however it requires an USB to FTDI cable negating some of the cost savings.

While the MEGA has more than enough digital I/O's, it also costs a significant amount more than the other options. In addition, it is also a good bit larger than the others with a dimension of 4.25" x 2.1". All things considered, the Arduino® NANO will be the best choice not only because it is the most inexpensive but also because it will fit nicely on the pinewood derby car. The biggest issue I am going to have is that it only has 14 digital I/O's and I need at least 16 not counting the interrupt and a sensor for the head lights. This was assuming I would use a simple on/off for each of the headlights. If I was to instead make that an analog input than I could turn the headlights on when a certain darkness was detected.

The best way I can see to handle the digital I/O issue is to add a couple of chips to expand my I/O pins. I can place these additional chips on the expansion board that will hold the 7 segment displays and the headlights which will be two LED's. The chips I have in mind are some that I have used in the past on other designs so I have good understanding of how they work and any limitations that they may have. The chip's that I have in mind are the SN74LS595[[11](#part0012_split_001.html_Ref11)] shift register. The beauty of this device is that it takes a serial input and converts it to a parallel output. I can shift in a value to represent my 7 segment display and use this device to drive the actual segments of the display. At a minimum, I only need two digital I/O lines to operate this device and I end up with 8 output lines. Not a bad trade off to go from 2 digital I/O's to 8\. Now granted, this is one way and I can only use it to expand my outputs however for my current project, this is perfect. For this particular device, it has two clock signals, one for the shift register and one for the storage register. The storage register is a buffer of sorts that allows you to build up the complete 8 bit data value before sending it to the output pins. The choice to make is whether you want to have a separate output for each of these clock lines which, if your output is better to turn on all at the same time, then the second clock line is what you need. I would like to be able to shift out the whole value at once to reduce flicker so I will utilize this additional clock line and use three digital I/O lines for each of my 7 segment displays. I am doing this so when I write a value to the SN74LS595, I will see a clean transition from one number to the next. I will also use two digital I/O's for my headlights so I can turn them on and off independently. So with this, I am now using 8 digital I/O's opposed to 16\. Not a bad savings overall and I have enough digital I/O's on the Arduino® NANO to do this. Of course I need to factor in the cost and space of two additional components however they will still be less than what an UNO or MEGA would cost.

Now that I have my design started I can see that some of my requirements are going to be impractical. In order to adjust the number for each car, I will either have to have a couple of switches which will increase the number of digital I/O's I need or I will need to use an analog input and convert the analog value to a digital equivalent. As for the photodetector, I think I will just pass on this. While it would be cool to have the lights come on when needed and turn off when not needed, I am going for the flashy look where I want them flashing all the time. Later on if I change my mind, I can always update my sketch to use photodetectors connected to the analog input pins however the devices themselves would have to be mounted separately. Another thing I was thinking about had been utilizing an interrupt to trigger when the lights should change. I can still do this as it will be simple to be done in code without any additional hardware however it isn't really necessary. I can simply have a loop do this given the actual micro-controller will not be doing much else in terms of work. I will however tie the input buttons to the interrupt pins so I can increase the number as required and reduce the potential of missing an input form the button. With the above design considerations my final requirements are as follows:

*   8 digital outputs
*   2 push buttons
*   Inputs to set the display value from 00 to 99
*   Expansion board to mount the seven segment displays and the headlights

### Implementation

Now that I have my main board selected and I have determined what additional major components I will need, I can start implementing my design. I have also refined my requirements to match my needs with the capabilities I have available or can easily obtain.

My first task is to design my expansion card and identify any possible issues that might come up due to that. I could look into the software I will need but given my hardware is currently just a good idea and not a concrete design, it would be a waste of time writing any software at this point.

#### Hardware

I know I will need two SN74LS595 devices to run each of the seven segment displays. I will also need a way to drive the LED's without overpowering the Arduino® output pins. The SN74LS595's can handle 24 milliamps. While the Radio Shack™ 7 segment displays have limited information posted regarding them, I found that they are similar or the same as the Everlight[[12](#part0012_split_001.html_Ref12)] 7 segment display which indicates that each segment requires a maximum of 15 milliamps. In order to ensure I don't over power any of my devices, I will place pull-up resistors inline with the various LED lights. This will allow me to drive the LED's while not over powering my devices. Given the number of LED's I will look into resistor arrays to minimize the amount of space required on my final board.

The first thing I am going to do is create a simplified circuit on my breadboard in order to test out what I believe will work. Right now there has been a lot of theory however I need to verify the design before trying to move forward. In this prototype, I will connect up one of the SN74LS595, a resistor network, and a seven segment display to test out both the hardware and the software interface.

##### Prototype

![expansion IO breadboard prototype](images/00031.jpeg)

In my prototype I only wired up one of the SN74LS595 chips given they are both going to be doing the same thing. I didn't hook up the headlights as of yet as they are fairly simple to wire i.e. a voltage supply, a resistor, and the LED. I connected the Arduino® to my laptop via USB however also used an external six (6) volt supply to drive the circuits on the breadboard. While none of the components on the breadboard would overload my USB port, if I don't have to take chances, I won't.

##### Circuit

Now that I have verified my prototype, I can move forward with a full circuit for expanding my I/O and displaying the car's number. The circuit consists of two 74LS595 shift registers along with the 7 segment displays. I am also using a resistor network to conserve space on my circuit board. The main circuit of the expansion board looks like as follows.![expansion schematic](images/00032.gif)

##### PCB

The circuit board I created from the schematic looks as follows:![expansion printed circuit board](images/00033.gif)You will notice in both the schematic and the PCB I have not defined the input buttons to change the number of the car. This is because I am going to mount them outside of the PCB in order to prevent them being exposed at the derby. Once I configure the car for the right number, I don't want it to change inadvertently so having them away from sight will make it a little easier. For the buttons, I will configure two push buttons which will simply allow the user to increment each digit of the 7 seven segment display individually. Because this is a fairly simple design we will only increment the numbers. Perhaps this isn't the most user friendly design but given the numbers won't be changing very often it will suffice.

#### Software

For this sketch I need to assign two data pins, two shift clocks, two storage clocks, and two pins to drive the LED's being used as headlights. Once they are assigned I can then write out data to each of the shift registers in order to assign the proper number for the car display. I will also need to configure two interrupts to handle the increment of the 7 segment displays.

```
 /*
 * PinewoodDerby - the purpose of this sketch is to control two 7 segment displays and two leds
 *                  which will be used as headlights.  The 7 segment display will be the number
 *                  of the pinewood derby car that it is attached to.
 *
 *  JP1 is three pins representing the data pin, the shift clock, and the storage clock
 *  JP2 is three pins representing the data pin, the shift clock, and the storage clock
 *  JP3 is two pins representing each of the LED headlights.
 *  Because we are using pins 2 and 3 as interrupts, we do not need to declare them prior to use
 */        

/*
  JP1 - Pin1 - To D8
  JP1 - Pin2 - To D9
  JP1 - Pin3 - To D10
*/

const int dataPinA = 8;
const int shiftClockA = 9;
const int storageClockA = 10;

/*
  JP2 - Pin1 - To D5
  JP2 - Pin2 - To D6
  JP2 - Pin3 - To D7
*/

const int dataPinB = 5;
const int shiftClockB = 6;
const int storageClockB = 7;

/*
  JP3 - Pin1 - ledA
  JP3 - Pin1 - ledB
*/

const int ledA = 11;
const int ledB = 12;

/* Segments - to value representing each 7 segment display LED mapped to a binary value
  Decimal Point: 0x01
  Top:           0x02
  Upper Right:   0x04
  Lower Right:   0x08
  Bottom:        0x10
  Lower Left:    0x20
  Center:        0x40
  Upper Left:    0x80
*/

//--------------------------------------------------------------------------------------------
// The following are the hexadecimal value for each of the digits based on the segments above
//------------------------  0     1     2     3     4    5      6     7     8     9

const byte digits[10] = { 0xBE, 0x0C, 0x76, 0x5E, 0xCC, 0xDA, 0xFA, 0x0E, 0xFE, 0xDE};
const byte decimalPoint = 0x1; // defined however unused in this sketch

/*
 * Variables used by this sketch
 */

volatile int g_leftDigit = 0;  // the left digit of the display
volatile int g_rightDigit = 0; // the right digit of the display
boolean g_ledFlash = false;    // to track whether my led should be on or off

/*
 * Method declarations
 */

void togglePin(int pinId);
void writeValue(int value);
void HandleLeftDigitIncrement(void);
void HandleRightDigitIncrement(void);

/*
 * Setup - main configuration point of our sketch to configure
 *         the Arduino for writing data to our shift registers
 *         and to be able to turn the headlights on and off.
 *         In addition I will preset the shift clocks to a known
 *         state.
 *         Finally I will configure my interrupts to catch when
 *         the buttons indicate the numbers should be incremented.
 *
 * Params - none
 *
 * Returns - nothing
 */

void setup()
{
  pinMode(dataPinA, OUTPUT);
  pinMode(dataPinB, OUTPUT);
  pinMode(shiftClockA, OUTPUT);
  pinMode(shiftClockB, OUTPUT);
  pinMode(storageClockA, OUTPUT);
  pinMode(storageClockB, OUTPUT);
  pinMode(ledA, OUTPUT);
  pinMode(ledB, OUTPUT);

  // Set the initial values of my shift and storage clocks
  digitalWrite(shiftClockA, LOW);
  digitalWrite(shiftClockB, LOW);
  digitalWrite(storageClockA, LOW);
  digitalWrite(storageClockB, LOW);

  attachInterrupt(0, HandleLeftDigitIncrement, RISING);
  attachInterrupt(1, HandleRightDigitIncrement, RISING);
}

/*
 * togglePin - toggles the passed in pin value from HIGH
 *              to LOW
 *
 * Params - pinId - representing the pin to toggle
 *
 * Returns - nothing
 */

void togglePin(int pinId)
{
  digitalWrite(pinId, HIGH);
  digitalWrite(pinId, LOW);
}

/*
 * writeValue - writes the passed in value to the
 *              the two 7 segment displays
 *
 * Params - value - which is the decimal value to write out encoded
 *                  using the digits array defined above.
 *
 * Returns - nothing
 */

void writeValue(int value)
{
  // Separate the value into two digits
  byte aValue = (value >> 8);
  byte bValue = value & 0xFF;

  // For every bit in each value i.e. aValue and bValue
  // write out HIGH if it is set i.e. a '1' and write out
  // LOW if it is not set i.e. a '0'
  for (int bitIndex = 0; bitIndex < 8; bitIndex++)
  {
    if (aValue & (1 << bitIndex))
    {
      digitalWrite(dataPinA, HIGH);
    }
    else
    {
      digitalWrite(dataPinA, LOW);
    }
    if (bValue & (1 << bitIndex))
    {
      digitalWrite(dataPinB, HIGH);
    }
    else
    {
      digitalWrite(dataPinB, LOW);
    }

    // Toggle the two clocks which shift the bits
    // down the shift register
    togglePin(shiftClockA);
    togglePin(shiftClockB);
  }

  // Finally toggle the storage clocks in order to show
  // the newly set digits.
  togglePin(storageClockA);
  togglePin(storageClockB);
}

/*
 * HandleLeftDigitIncrement - called when the button to
 *                            increment the left digit is
 *                            pressed.
 *
 * Params - none
 *
 * Returns - nothing
 */

void HandleLeftDigitIncrement(void)
{
  g_leftDigit++;     // Increment to the next digit
  g_leftDigit %= 10; // roll at 10 so we have 0 - 9 total
}

/*
 * HandleRightDigitIncrement - called when the button to
 *                             increment the right digit is
 *                             pressed.
 *
 * Params - none
 *
 * Returns - nothing
 */

void HandleRightDigitIncrement(void)
{
  g_rightDigit++;     // Increment to the next digit
  g_rightDigit %= 10; // roll at 10 so we have 0 - 9 total
}

/*
 * loop - main method which will be called each time the
 *        Arduino goes through its main loop to change the state
 *        of the headlights and update the 7 segment displays
 *
 * Params - none
 *
 * Returns - nothing
 */

void loop()
{
  if (g_ledFlash)
  {
    digitalWrite(ledA, HIGH);
    digitalWrite(ledB, LOW);
  }
  else
  {
    digitalWrite(ledA, LOW);
    digitalWrite(ledB, HIGH);
  }

  //---------------------------------------------
  // If ledFlash is currently true
  // then set it to false otherwise make it true
  //---------------------------------------------
  g_ledFlash = g_ledFlash == false ? true : false;

  //---------------------------------------------
  // Concatenate two 8 bit values into one 16 bit
  // integer.  In order to ensure I knew what the
  // size of an integer was on this platform, I did
  // the following:
  // Serial.print("Size of int: ");
  // Serial.println(sizeof(int));
  //
  // I first shift the value 8 bits into the upper "byte"
  // of the integer and then "or" in the same value into
  // the lower 8 bits.  I could have also added the value
  // to the current value that was shifted resulting
  // in the same value to display however I prefer to
  // use the "or" so it is clear I am merging the two
  // values opposed to adding.
  //---------------------------------------------
  int valueToDisplay = (digits[g_leftDigit] << 8) | digits[g_rightDigit];
  writeValue(valueToDisplay);

  // Pause for 500 milliseconds i.e. 1/2 second.
  delay(500);
} 
```

In the above code I am using several of the concepts we have explored previously. I am using the digital I/O to drive the expansion devices. I am using interrupts to increment each of the digits of the seven segment display. One thing to note is that while what I have shown is one way to do this, it most certainly isn't the only way. For instance I could have used the analog inputs to drive a voltage to indicate the value that the seven segment display should show. I also could have just used a digital input to read the signal coming from the switch and bypassed the interrupts all together. I am sure there are a number of other ways to accomplish this too.

For this code, I will not dig too deeply into it as most of this has been covered in previous chapters. I will however point out a few items I think are important and should be noted. The first is the use of the keyword volatile which I have used in the previously. It is important to note this keyword and when it should be used. I used it when declaring the variables to be used for the digits to be displayed as they can be updated during the interrupt cycle.

```
 volatile int g_leftDigit = 0;  // the left digit of the display
volatile int g_rightDigit = 0; // the right digit of the display 
```

The volatile keyword is a way for the programmer i.e. you to tell the compiler that the variable is subject to change outside the normal flow of control so should not be optimized. Basically when a compiler creates a program, it will optimize the code to take advantage of any hardware capabilities that will allow the software to run faster. Because this variable can be changed by the interrupt, which the compiler may not be able to determine on its own, I want to ensure that the compiler doesn't try to optimize this portion of the code. For the rest of the code, I feel that it is somewhat self explanatory given everything that has been covered so far.

#### Final Board

I utilized an online PCB manufacturer to create a few boards that I could use to bring my circuit to fruition. Overall the cost for six (6) boards was around $50.00 shipped. Not bad overall. The final built PCB is shown below.

![final pcb in action](images/00034.jpeg)

As you can see in the image, I have my board running and doing what I want. You may also notice that I have a shield on my Arduino® in order to interface with my expansion board. This was for ease of testing where I wanted to expose the various pins I needed as true male pins. By default the connections on the Arduino® UNO are female and I needed male pins to connect over to the expansion board. I utilized my Arduino® UNO for the preliminary testing due to its convenience factor. On the pinewood derby car I will have male pins on my Arduino® NANO which will connect directly to the expansion board. When placing everything on the car for the final verification, I realized I never included a way to connect the 9V battery power source from the expansion board over to the Arduino®. Even when you think you have everything covered, something always seems to be left out. I will be tying down the wires close to the body and placing the Arduino® NANO in the front to look like an engine. The only other thing I have to do is raise the expansion board itself a little to ensure I clear the wheels. The final setup with the parts as they will be glued to the pinewood derby car can be seen in the following images.

![parts on the car](images/00035.jpeg)
![side view of parts on the car](images/00036.jpeg)

### Summary

In this chapter I explored the creation of an interface board to connect to an Arduino® in order to display numbers and head lights on a pinewood derby car. I started with an idea and worked it through to the end product which could be mounted to a pinewood derby car to show the car's numbers. In the end it is only eye candy however its cool eye candy.

![chapter end graphic](images/00001.jpeg)

# Shields

## Bringing it to 11

Shields bring new capabilities to your Arduino® platform. Shields allow you to add on functionality to your base micro-controller to do additional great things. While most of the functionality that a shield brings can be built by yourself, having it canned and straight out of the box with the potential of working code is a definite bonus. Some of the shields I have used include the Ethernet and Bluetooth® communication modules.

So what does a shield look like? For the most part they are very similar to what an Arduino® UNO looks like.

![image of a standard shield](images/00037.jpeg)

From a top down view such as above, it might even look like and Arduino® UNO. The main reason for this is that most shields, if not all, are designed to be compatible with the largest number of Arduino® and clone boards that are out there. Typically the shield will expose the same digital and analog pins that an Arduino® board would have available. In addition to those pins it is typical to have a reset button available on the shield to allow easy access to resetting the board given that the shield will most likely cover the reset button on the main board. In some cases, the standard LED's may also be present. While this is really cool, you will have to be careful when using a shield as some of the pins that would normally be available to you might not be if the shield itself is using it. For instance, the Ethernet shield shown above has the typical Arduino® UNO pin layout however if you look closely you will notice that pins ten (10) and four (4) are not labeled the same. Because both the Ethernet chip and the SD card slot use SPI for communications, these two pins are utilized by the default sketches to use these two pins as chip selects. You will still have access to the pins however you will want to ensure that you don't use them as it might interfere with the operation of the Ethernet module or the SD card. Beyond this it is as simple as including the proper libraries in your sketch, attaching the shield, and start programming. One thing to note is that the shield should never be installed or removed while there is power applied to the main board or the shield. Even if it is just connected to the computer via an USB cable. The installation or removal of the shield could damage the main board or the shield itself if power is currently active on either one.

### Ethernet

The [Ethernet Shield](http://arduino.cc/en/Main/ArduinoEthernetShield) is designed to allow easy connectivity to your local network for communication purposes. This brings up a number of possibilities such as remote monitoring, remote control, data collection, etc. This shield also includes a micro SD card slot for data storage which can also be beneficial for offline storage of data which can be uploaded later on once an internet connection is made. One of the main uses for this shield is to be able to communicate with the Arduino® over your local network and not require an LCD or other means to observer what is happening with the controller. It is also possible to reprogram you controller over the network connection which can be useful when the controller is installed in a location that isn't readily accessible.

### Bluetooth®

The Bluetooth® shield brings wireless technology to your micro-controller. This allows communication with your PC or other device which supports the Bluetooth® serial port profile (SPP). The shield I have used is the following: [BT Shield](http://www.seeedstudio.com/wiki/Bluetooth_Shield) which only supports the serial profile. Other modules such as the [Maker Shed BLE Shield](http://www.makershed.com/Bluetooth_Low_Energy_BLE_Shield_for_Arduino_2_0_p/mkrbl1.htm) supports Bluetooth® LE and may support other profiles such as the advanced audio distribution profile (A2DP) or hands free profile (HFP). My experience so far has been limited to the one shield using the serial profile for communications to control a motor connected to my Arduino® in addition to the OBDII connecter we looked at previously in the [Communications](#part0007_split_001.html_spp_bt) chapter. The possibilities are quite extensive such as controlling a robot using your smartphone or other Bluetooth® enabled device.

### General

In addition to pre-built shields, there are many kits on the market from a variety of sources which allow you to build your own shields to interface with whatever you have lying around. These prototyping shields are a great way to quickly build up a circuit to interface with external devices and prove out a design before developing a PCB and ordering populated boards. Most of the prototyping shields I have used come with a number of components to get the basics in place such as the 6 pin In-System Programming, ISP, header and the stacking headers so additional shields can be placed above the prototyping shield or below it as needed.

### Summary

In general, if there is a task you need to accomplish, there is probably a shield out there ready to go to do it. From communications, to motor controls, to sensor reading, there are shields that will accomplish what you need. When that doesn't work, the prototyping kits that are available are a nice and easy way to build up an interface circuit to try out your idea before developing a PCB. In addition to the shields that are out there, most of them come with sample code that you can use in your own projects as is or as a starting point for something bigger and better. The possibilities are really endless.

![chapter end graphic](images/00001.jpeg)

# Sketches

## setup and loop

The sketches that have been utilized in this book are available for download from my website. For each sketch, I have provided the chapter from which it came and a link to where you can download it from.

| Sketch | Chapter | Location |
| Skeleton Sketch | [Arduino Platform](#part0003_split_002.html_skeletonsketch) | [Download](http://book.afmsoftware.com/resources/SkeletonSketch.zip) |
| Temperature Reading (LM335) | [Input](#part0004_split_001.html_TempReading) | [Download](http://book.afmsoftware.com/resources/lm335reader.zip) |
| Temperature Comparison (LM335) | [Input](#part0004_split_002.html_temptrigger) | [Download](http://book.afmsoftware.com/resources/lm335comparator.zip) |
| Temperature Trigger (LM335) | [Program Interrupted](#part0006_split_001.html_temptrigger) | [Download](http://book.afmsoftware.com/resources/lm335comparator_interrupt.zip) |
| Rotary Encoder | [Program Interrupted](#part0006_split_001.html_rotaryencoder) | [Download](http://book.afmsoftware.com/resources/RotaryEncoder.zip) |
| Fan Tachometer | [Program Interrupted](#part0006_split_001.html_fantach) | [Download](http://book.afmsoftware.com/resources/infrared_trigger.zip) |
| PWM Output - LEDs | [Output](#part0005_split_001.html_ledpwm) | [Download](http://book.afmsoftware.com/resources/TriColorLEDTemperature.zip) |
| PWM Output - Fans | [Output](#part0005_split_001.html_pwmfan) | [Download](http://book.afmsoftware.com/resources/FanPWM.zip) |
| PWM Output - Servo's | [Output](#part0005_split_001.html_servopwm) | [Download](http://book.afmsoftware.com/resources/ServoPWM.zip) |
| Power On LED | [Output](#part0005_split_001.html_powonled) | [Download](http://book.afmsoftware.com/resources/PowerIndicator.zip) |
| Power Indicator | [I/O Expansion](#part0009_split_001.html_derby) | [Download](http://book.afmsoftware.com/resources/PowerIndicator.zip) |
| Bluetooth Serial Communications | [Communications](#part0007_split_001.html_serialbt) | [Download](http://book.afmsoftware.com/resources/BTTest.zip) |
| SPI Communications | [Communications](#part0007_split_001.html_spicomm) | [Download](http://book.afmsoftware.com/resources/SpiDigitalPot.zip) |
| I2C Communications | [Communications](#part0007_split_002.html_i2c) | [Download](http://book.afmsoftware.com/resources/SH1106.zip) |

# References

## Additional information

The following is a table of references found throughout the book.

| Number | Title | Description | Link |
| --- | --- | --- | --- |
| 1 | Bell Labs | Describes what Bell Labs is and its history | [Here](http://en.wikipedia.org/wiki/Bell_Labs) |
| 2 | AC/DC Power | Background history of why 120V's was chosen for the United States. | [Here](http://wiki.answers.com/Q/Why_was_120V_chosen_as_the_standard_voltage_of_homes_in_the_US_and_not_some_other_voltage) |
| 3 | Creative Commons License | Attribution-ShareAlike 3.0 | [Here](http://creativecommons.org/licenses/by-sa/3.0/) |
| 4 | Arduino® | Main site for the Arduino® platform | [Here](http://www.arduino.cc/) |
| 5 | C/C++ Comments | Comment rules | [Here](http://msdn.microsoft.com/en-us/library/k1dbk8bw.aspx) |
| 6 | Serial Ports | Information regarding standard serial port communications. | [Here](http://en.wikipedia.org/wiki/Serial_port) |
| 7 | LM335 Temperature Sensor | Device data sheet | [Here](http://www.ti.com/lit/ds/symlink/lm335.pdf) |
| 8 | NTE7225 Temperature Sensor | Device data sheet | [Here](http://www.nteinc.com/specs/7200to7299/pdf/nte7225.pdf) |
| 9 | LM311 Voltage Comparator | Device data sheet | [Here](http://www.ti.com/product/lm311) |
| 10 | NTE943M Voltage Comparator | Device data sheet | [Here](http://www.nteinc.com/specs/900to999/pdf/nte943.pdf) |
| 11 | SN74LS595 Shift Register | Device Data Sheet | [Here](http://www.ti.com/product/sn74ls595) |
| 12 | 7 Segment Display | Device Data Sheet | [Here](http://www.digchip.com/datasheets/download_datasheet.php?id=296385&part-number=ELS-321HDB&show=inline) |
| 13 | AVR Downloader/UploaDEr | Open source AVR device programmer | [Here](http://www.nongnu.org/avrdude/) |
| 14 | Base 16 | Definition | [Here](http://en.wikipedia.org/wiki/Hexadecimal) |
| 15 | EEPROM | Definition | [Here](http://en.wikipedia.org/wiki/EEPROM) |
| 16 | Seeed Studio Bluetooth® Shield | Device Information | [Here](http://www.seeedstudio.com/depot/Bluetooth-Shield-p-866.html?cPath=19_21) |
| 17 | Generic OBDII Adapter | Device Information | [Here](http://www.amazon.com/iSaddle-Bluetooth-CAN-BUS-Diagnostic-Windows/dp/B008U1MOM8/ref=pd_sim_sbs_auto_1?ie=UTF8&refRID=0C8GAXPR2GC4DCE4RRAV) |
| 18 | Microchip 10K SPI Digital Potentiometer (MCP4261) | Device Information | [Here](http://ww1.microchip.com/downloads/en/DeviceDoc/22059b.pdf) |
| 19 | SH1106 LCD Controller Chip | Device Information | [Here](http://www.sinowealth.com/en/softdown.asp?soft_id=298&class_id=,%20100,&cat_id=33&flag=1) 
[Here](http://wenku.baidu.com/view/43ebc40aba1aa8114431d940.html) |
| 20 | SH1106 LCD Arduino® Library | Code library | [Here](https://github.com/milligan22963/sh1106) |

![chapter end graphic](images/00001.jpeg)

# Vendors

## On-line Merchants

The following is a table of on-line merchants with whom I have dealt successfully with.

| Vendor | Description | Link |
| --- | --- | --- |
| Adafruit Industries | Various prototyping tools and components | [Here](http://www.adafruit.com) |
| Sparkfun Electronics | Various prototyping tools and components | [Here](http://www.sparkfun.com) |
| Mouser Electronics | Numerous components and tools | [Here](http://www.mouser.com) |
| Newark | Numerous components and tools | [Here](http://www.newark.com) |
| OshPark | PCB manufacturing that is economical. Do note that the turn around time can vary depending on project size. | [Here](http://oshpark.com//) |
| Amazon | Various third party vendors with economical parts. | [Here](http://www.amazon.com//) |
| eBay™ | Various third party vendors with economical parts. | [Here](http://www.ebay.com//) |
| Sain Smart | Various prototyping parts and tools | [Here](http://www.sainsmart.com) |
| Seeed Studio | Various prototyping parts and tools | [Here](http://www.seeedstudio.com/depot/) |

![chapter end graphic](images/00001.jpeg)

# D. W. Milligan

## From Programming to Photography

![D. W. Milligan - Author](images/00038.jpeg)

Born and raised in Maine, the author grew up in the great outdoors. The winter’s were long and the summer’s were brief however there was usually time for a good day of fishing. The author currently lives outside of Charlottesville, VA with his wife and children. He is a Software Architect with a keen interest in landscape photography and computers. Equipment used in this book is as follows: Macintosh Macbook Pro, iPad 3rd generation for previewing, coffee and other caffeinated drinks as required.

Photo credit - Colin Conrad

![chapter end graphic](images/00001.jpeg)

1.  [Copyright](#part0000_split_000.html_About)
2.  [Introduction](#part0001_split_000.html_Introduction)
3.  [Setup](#part0002_split_000.html_Setup)
4.  [Arduino Platform](#part0003_split_000.html_Arduino)
5.  [Input](#part0004_split_000.html_Input)
6.  [Output](#part0005_split_000.html_Output)
7.  [Interrupts](#part0006_split_000.html_Interupt)
8.  [Storage](#part0008_split_000.html_Storage)
9.  [Communications](#part0007_split_000.html_Communications)
10.  [I/O Expansion](#part0009_split_000.html_ioexpansion)
11.  [Shields](#part0010_split_000.html_Arduino)
12.  [Sketches](#part0011_split_000.html_Sketches)
13.  [Reference](#part0012_split_000.html_Reference)
14.  [Vendors](#part0013_split_000.html_Reference)
15.  [About](#part0014_split_000.html_About)