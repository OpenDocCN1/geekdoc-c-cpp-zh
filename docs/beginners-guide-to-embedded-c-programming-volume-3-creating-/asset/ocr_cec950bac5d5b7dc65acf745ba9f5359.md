hexadecimal). This function is really useful for displaying numerical values on an LCD.

```
lcd_goto(0x40);    // Select second line
lcd_number (value);    // Display ADC reading on LCD
```

We add a pause (10) to the program to delay reading the voltage thus allowing the display to look a little more stable. The potentiometer voltage is pretty steady so this isn’t necessary but helps if you want to use this project to read any input voltage that is cycling between 0 volts to 5 volts. This pause function also ends the loop so we circle back and read the potentiometer again and do this continuously within the while-loop.

```
pause (10);    // Delay 10 millisecond between samples
}
```

# Next Steps

You could replace the LCD with LEDs to create a bar graph display of light that changes with the turning of the potentiometer. You could also add some other functions such as the PWM library function so the potentiometer controls a motor’s speed or an LED’s brightness and still show the value on the LCD. You could also replace the potentiometer with a light sensor to let the light change the resistance and thus the voltage. This would make a crude light meter. This project is easily adapted to many different analog sensors. Having the LCD readout makes it easy to see the sensor results.