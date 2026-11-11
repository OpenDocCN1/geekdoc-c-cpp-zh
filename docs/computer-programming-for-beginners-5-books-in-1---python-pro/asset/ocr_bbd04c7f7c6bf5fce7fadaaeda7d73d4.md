# C Language Basics and Functions

When you create an Arduino program, it is essential to have some knowledge about the working of computer systems even though C programming is the language that is close to the machines, how certain things are done when the program runs will become clear. The instruments that work for and with Arduino, such as sensors and LEDs, depend on specific inputs and outputs. Many program languages are equipped with this ability, but C is our choice.

A primary system consists of the control device referred to as the CPU or microcontroller. There are a few differences when it comes to some of these. We shall dig deep into this later. Just to mention, microcontrollers may not be that powerful compared to the standard microprocessor. However, it still contains input, output ports, as well as hardware functions.

Microprocessors are connected to the external Memory. Generally, microcontrollers contain a sufficient amount of onboard memory. However, it should be noted that we are not referring to the large sizes; it is possible for a microcontroller to have only a few hundred bytes or so of memory for the simple applications. Don’t forget that a memory byte has 8 bits, and each bit can either be true or false, high or low and I/O.

The register is the only place where we can have logical mathematical operations carried out. For example, if you would like to carry out an addition of two variables, the value of the variables has to be moved over to the register.

# Memory Maps

Each memory byte in the computer system has a connected address. Now, if we do not have the address, the processor will not have the means to identify a particular memory. In general, the memory address begins from 0 as it increases. Even though we have specific addresses with a private or unique system, a particular address may not point to the input and output port of external communication.

Most of the time, you will find it necessary to map-out the memory. This is merely a massive array of memory slots. We have people who develop a memory map and have the address with the least value positioned at the top while others who