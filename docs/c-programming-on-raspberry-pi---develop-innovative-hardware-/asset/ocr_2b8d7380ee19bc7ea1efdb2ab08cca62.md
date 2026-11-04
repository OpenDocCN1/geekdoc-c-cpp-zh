![](bbox=[0.15, 0.08, 0.85, 0.42])

Figure 14.7 Block diagram of the project

# Circuit diagram:

The circuit diagram of the project is as shown in Figure 7.18. On-chip pull-up resistors are available on the TMP102 I2C bus lines. I2C bus lines SDA and SCL pins of the TMP102 are connected to GPIO 2 and 3 respectively.

# Program listing:

Figure 14.8 shows the program listing (Program: TMP102UDP.c). In this program, the wiringPi library and GPIO pin numbering is used. The program is in two parts: the function that reads the temperature from the TMP102 and the main program that sends the temperature reading to the Android smartphone. Function ReadTemperature reads the temperature from the TMP102 sensor module and returns it to the main program as a floating-point number (see Section 7.5 for details). The main program runs in a loop and waits to receive commands from the Android smartphone. If the received command is character x, the program terminates and the message End of program is sent to the smartphone. If the command is T, function ReadTemperature is then called. Temperature is converted into integer and stored in variable temperature. This is then converted into a string and stored in array msg. Character C (Centigrade) is then added to the end of msg and is sent and displayed on the Android smartphone. If the user command is anything other than x or T, the error message Error – expected T or x is sent and displayed on the Android screen. You can compile and run the program as follows:

```
gcc -o TMP102UDP TMP102UDP.c -lwiringPi
sudo ./TMP102UDP
```