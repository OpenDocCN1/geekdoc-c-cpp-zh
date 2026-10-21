# Chapter 4

# Building a Morse Code Generator Library

You now know enough about the Arduino development environment and about blinking LEDs to start a bigger project. In this chapter, we’ll develop a Morse code generator that reads text from the serial port and outputs it as light signals using an LED.

By building this project, you’ll deepen your understanding of serial communication between the Arduino and your computer. You’ll also learn a lot about the typical Arduino development process: how to use existing libraries and how to structure bigger projects into your own libraries. At the end, you’ll be able to create a library that is ready for publishing on the Internet.

# 4.1 What You Need

+   - An Arduino board such as the Uno, Duemilanove, or Diecimila
+   - A USB cable to connect the Arduino to your computer
+   - An LED
+   - A speaker or a buzzer (they are optional)

# 4.2 Learning the Basics of Morse Code

Morse code was invented to turn text into sounds.¹ In principle, it works like a character set encoding such as ASCII. But while ASCII