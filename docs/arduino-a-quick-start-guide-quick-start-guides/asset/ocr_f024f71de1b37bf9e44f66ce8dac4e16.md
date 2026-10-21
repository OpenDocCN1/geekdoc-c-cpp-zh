![](bbox=[0.12, 0.07, 0.77, 0.29])

Figure 7.2: How to connect a Nunchuk to an Arduino

That’s really all you have to do to connect a Nunchuk controller to an Arduino. In the next section, you’ll see that the two wires connected to analog pins 4 and 5 are all we need to interface with the controller.

# 7.3 Talking to a Nunchuk

No official documentation shows how a Nunchuk works internally or how you can use it in a non-Wii environment. But some smart hackers and makers on the Internet invested a lot of time to reverse-engineer what’s happening inside the controller.¹

All in all, it’s really simple, because the Nunchuk uses the Two-Wire Interface (TWI), also known as I²C (Inter-Integrated Circuit) protocol.² It enables devices to communicate via a master/slave data bus using only two wires. You transmit data on one wire (DATA), while the other synchronizes the communication (CLOCK).

The Arduino IDE comes with a library named Wire that implements the I²C protocol. It expects the data line to be connected to analog pin 4 and the clock line to analog pin 5. We’ll use it shortly to communicate with the Nunchuk, but before that, we’ll have a look at the commands the controller understands.³

1. http://www.windmeadow.com/node/42
2. http://en.wikipedia.org/wiki/I2c
3. At http://todbot.com/blog/2010/09/25/softi2cmaster-add-i2c-to-any-arduino-pins/, you can find a library that allows you to use any pair of pins for I²C communication.