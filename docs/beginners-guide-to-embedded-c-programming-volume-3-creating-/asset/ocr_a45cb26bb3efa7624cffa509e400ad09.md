function retrieves the data from the EEPROM at the address in the address parameter. The byte received is stored in the b0 variable.

```
char b0 = RD_BYTE( addr);   // Read from SEEPROM
```

Now that we have the data and already know the address, we position the LCD to the second line and then display the address value and the data value using separate lcd_symbol functions. The values are added to the constant “number” so the value sent to the LCD is the ASCII value for the value. This method works because all the values are single digit values.

```
lcd_goto(0x40);          // Select second line
lcd_symbol(addr + number);   // Display value read from
                           //EEPROM on LCD
lcd_text(" / ");
lcd_symbol(b0 + number);   // Display value read from
                           //EEPROM on LCD
```

A delay is added so we can easily read the values displayed on the LCD.

```
pause (250);          // Delay 250 msec to see count
} //End For
} //End While
} //End Main
```

# Next Steps

You can play with the first loop to change the data being stored and verify it works by monitoring the display. You can also expand the project to store more data but you’ll have to modify the way the data is displayed on the LCD because larger amounts of data mean address values larger than single digit.