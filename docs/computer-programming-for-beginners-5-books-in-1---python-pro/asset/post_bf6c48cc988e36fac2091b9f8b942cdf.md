
This is just a basis for basic Arduino programming. In the rest of the book, we will be looking at how Arduinos can be programmed with respect to different functions. If you’re new to programming, don’t let the above codes frighten you. Coding takes practice, but it is relatively easy to learn, just like a new language.

After some issues with establishing the trademark for Arduino, which resulted in a split in the company for a few years, Arduino is now a single company that is committed to the development of hardware and software usable by the average person or hobbyist, but also flexible enough to be of interest to the professional engineer.

## But what is Arduino?

This history of Arduino might sound as convoluted as the technology itself seems to you. Full of many puzzling and confusing elements, you might feel overwhelmed by the language of “microcontrollers,” “environments,” and “languages.” However, this book is intended to demystify Arduino. We will start here, beginning with the definition of Arduino.

How it works is as follows: one purchases the hardware that is appropriate to his or her purposes and then, on a more powerful Windows, Macintosh OSX, or Linux computer, codes or writes instructions for the board and uploads the instructions via a cable. The code is then stored on the microcontroller, and it functions according to the instructions, such as activating a beeping sound when light filters in through an opening door. The light activates a sensor connected to the microcontroller, like an alarm.

## Who Uses Arduino?

A wide array of people uses Arduino for various projects and hobbies, as well as for professional uses. It is known for being simple and straightforward enough for beginners, deep and rich enough for the beginner to grow, and with enough potential for a more advanced user to utilize.

Teachers and students use Arduino, and indeed are the intended consumer base for the products, as Arduino offers a low-cost way to build scientific instruments. This allows teachers and students to practice and demonstrate chemistry and physics principles, as well as get started with programming and building robots.

Designers and architects might use Arduino technologies to build interactive models and prototypes of what they hope to develop on a full-scale. Musicians and artists also use Arduino microcontrollers to experiment with new instruments or techniques in their art. Just about anyone can use Arduino, including children who want to start tinkering with coding and computer hardware, as well as hobbyists who simply want to learn a bit about software and microcomputers.

## The 6 Advantages of Arduino

- The driving force behind creating Arduino microcontrollers was cost-efficiency. Rather than the $100 that some other boards cost, a pre-assembled Arduino board costs less than $50, and the boards that can be manually put together cost even less.
- The Arduino environment, IDE, works across different platforms. This means that you can use a Windows computer unlike any other microcontroller board would probably require, but you can also use a Macintosh OSX computer, or a computer running Linux and work just as easily with the Arduino software. This opens up the use of microcontrollers to the Apple user and the open-source Linux user.
- The software for Arduino is open-source. The tools, or strings of code that you use to instruct the microcontroller to accomplish certain functions, are accessible by anyone. You do not have to purchase a license to use these tools so that teachers can teach students about them and students can learn them without added cost.
- The open-source tools are also extendable by the C++ libraries and the AVR-C coding language, meaning that those with more in-depth knowledge of code would be able to benefit from using these technologies as well. There is depth to the software and programming features that allow the more dedicated person to go deeper while being enough of a straightforward coding language to allow the hobbyist to tinker as well.
- The environment in which a person codes for the microcontroller is simple and clear. This means that the computer program, IDE, which you would use to program the instructions for the microcontroller, is straightforward and easy to understand. This makes working with the software a smooth experience.
- The open-source hardware. Arduino board technologies are published under a Creative Commons license. Anyone who desires and has the knowledge to do so could find and create their own hardware to use with Arduino software programming in the IDE environment. Even those who are not experienced circuit designers can use a breadboard to create their own Arduino circuit board.

## Key Terms in Understanding Arduino

When working with Arduino technologies, it is helpful to understand the terminology of Arduino. You will need to understand the terminology to choose a board, write the coded instructions, set up the microcontroller for use, and finally use the Arduino board. In this chapter, you will find some key terms that will aid you greatly in your endeavor to become an Arduino user.

As mentioned earlier, Arduino is open-source, meaning you can use it and teach it to others without violating any copyright laws. It is based on easy-to-use hardware, which is the actual physical computer board with which you will be working, and straightforward software, the coded instructions with which you will direct the hardware to perform a task of your choosing. The software is also known as code, and the individual pieces of instructions are called tools.

## Anatomy of the Arduino Board

The board itself contains a good number of parts. The digital pins run along the edges of most Arduino microcontrollers and are used for input, or sensing of a condition, and output, the response that the controller makes to the input. For example, the input might be that the light sensor senses darkness, that is, a lack of light. It will then close a circuit lighting up a bulb as output: a nightlight for your child.

On most boards, there will be a Pin LED, associated with a specific pin, like Pin 13 on the Arduino Uno. This Pin LED is the only output possibility built into the board, and it will help you with your first project of a “blink sketch,” which will be explained later. The Pin LED is also used for debugging or fixing the code you have written so that it has no mistakes in it. The Power LED is what its name implies: it lights up when the board is receiving power or is “turned on.” This can also be helpful in debugging your code.

There exists on every board the microcontroller itself, called the ATmega microcontroller, which is the brain of the entire board. It receives your instructions and acts accordingly. Without this, the entire board would have no functionality.

Analog in pins exist on the opposite edge of the board from the digital pins on the Arduino Uno. They are inputs into the Arduino system. Analog means that the signal which is input is not constant but instead varies with time, such as audio input. In the example of audio input, the auditory input in a room varies with the people in the room talking and with the noises filtering in from outside the room.

GND and 5V pins are used to create additional power of 5V to the circuit and microcontroller. The power connector is most often on the edge of the Arduino board, and it is used to provide power to the microcontroller when it is not plugged into the USB. The USB port can be used as a power source as well, but its main function is to upload, or transfer, your sketch, or set of instructions that you have coded, from your computer to the Arduino.

TX and RX LEDs are used to indicate that there is a transfer of information occurring. This indication of communication will happen when you upload your sketches from your computer to the Arduino so that they will blink rapidly during the exchange.

The reset button as it sounds: it resets the microcontroller to factory settings and erases any information you have uploaded to the Arduino.

## Other Terms about Working with Arduino

There are three types of memory in an Arduino system. Memory is the space where information is stored.

Flash memory is where the code for the program that you have written is stored. It is also called the “program space,” because it is used for the program automatically when you upload it to the Arduino. This type of memory remains intact when the power is cut off, or when the Arduino is turned off.

SRAM (static random-access memory) is the space used by the sketch or program you have created to create, store, and work with information from the input
