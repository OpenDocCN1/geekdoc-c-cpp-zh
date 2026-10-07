# # Chapter 9
# DS18B20 1-Wire Temperature Sensor

The 1-Wire bus is a proprietary bus that is very easy to use and has a lot of useful devices you can connect to it. Probably the most popular of all 1-wire devices is the DS18B20 temperature sensor - it is small, very cheap and very easy to use if the processor supports the 1-Wire bus protocol, the micro:bit doesn't. However, the protocol is easy enough to program in C and the micro:bit is fast enough to work with it without needing anything extra. We have to use C for this; Python, for example, just isn't fast enough.

The microbit has an onboard temperature sensor, but this measures the temperature of the CPU and only gives you the air temperature very approximately. The DS18B20 gives you an accurate temperature and you have multiple sensors.

# # The Hardware

The DS18B20 is available in a number of formats but the most common makes it look just like a standard BJT - which can sometimes be a problem when you are trying to find one. You can also get the DS18B20 made up into a waterproof sensor complete with cable. No matter how packaged, it will work at 3.3V or 5V.

![](bbox=[0.206, 0.655, 0.783, 0.803])