# Chapter 7

# Tinkering with the Wii Nunchuk

One of the most entertaining electronic activities is tinkering: taking an existing product and turning it into something different or using it for an unintended purpose. Sometimes you have to open the product and void its warranty; other times you can safely make it part of your own project.

In this chapter, you'll learn how to hijack a Nintendo Nunchuk controller. It's a perfect candidate for tinkering: it comes with a three-axis accelerometer, an analog joystick, and two buttons, and it is very cheap (less than $20 at the time of this writing). Even better: because of its good design and its easy-to-access connectors, you can integrate it into your own projects surprisingly easily.

We'll use an ordinary Nunchuk controller and transfer the data it emits to our computer using an Arduino. You'll learn how to wire it to the Arduino; how to write software that reads the controller's current state; and how to move, rotate, and scale a 3D cube on the screen using your Nunchuk. You don't even need a Nintendo Wii to do any of this—you only need a Nunchuk controller.

# 7.1 What You Need

+   - An Arduino board such as the Uno, Duemilanove, or Diecimila
+   - A USB cable to connect the Arduino to your computer
+   - A Nintendo Nunchuk controller
+   - Four wires