# Chapter 13
Getting On WiFi

The micro:bit has a radio that has two modes, Bluetooth LE and ad-hoc point-to-point ad-hoc but it lacks WiFi connectivity. One solution is to use the low cost ESP8266 to make the connection via the micro-bit's serial port. As we will make a lot of use of the micro:bit's serial port it is assumed that you know roughly how it works. In particular, it is assumed that you are familiar with the material in the previous chapter. Before we get on to the details of using the ESP8266 need to find out what makes it special.

# The Amazing ESP8266

The ESP8266 is a very odd and amazing device. It is remarkably low cost, $5 or less, it is a full microprocessor with GPIOS inline, RAM and built in WiFi. It is built by a Chinese company Espressif Systems but there are a number of copies on the market. The proliferation of devices and software revisions makes it difficult to work with, but it is well worth the effort.

The module used in this chapter is the ESP8266 ESP-01 which is widely available from many different sources but they all look alike:

![](bbox=[0.368, 0.574, 0.631, 0.755])

Another version, the ESP-07, which comes with a screened RF stage and other advantages, should also work.