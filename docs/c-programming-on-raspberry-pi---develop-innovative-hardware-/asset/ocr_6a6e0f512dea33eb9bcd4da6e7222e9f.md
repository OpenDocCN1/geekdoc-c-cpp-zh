# 7.6 • Project 4 – I2C LCD

# Description:

In this project, we will be using an I2C based LCD with Raspberry Pi. The text Raspberry Pi will be displayed on the LCD.

# Aim:

This project aims to show how an I2C based LCD can be used with Raspberry Pi when programming in C.

# Circuit diagram:

I2C based LCDs usually consist of a PCF8574 type 8-bit I/O expander chip connected on the back of a standard HD44780 type parallel LCD. The LCD is controlled in 4-bit mode by the PCF8574 chip through standard SDA and SCL I2C lines. Figure 7.21 shows the front and back views of a PCF8574 based I2C LCD. A small pot is provided on the back for adjusting the contrast of the LCD.

![](bbox=[0.343, 0.455, 0.679, 0.68])

Figure 7.21 PCF8574 based I2C LCD

The circuit diagram of the LCD is shown in Figure 7.22. The connections between the LCD and PCF8574 chip are as follows: