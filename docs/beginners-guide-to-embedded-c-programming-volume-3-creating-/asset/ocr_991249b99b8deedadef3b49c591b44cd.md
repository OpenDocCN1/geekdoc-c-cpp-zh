The screen of the LCD is cleared with the lcd_clear function. This clears the screen and positions the cursor at the home or first character block position.

```
lcd_clear();    // Clear LCD screen
```

Now we enter the main while loop that actually displays the count on the LCD. The while-loop contains a for-loop that creates and increments an 8-bit variable. When the variable equals 10, the for-loop ends.

```
while (1==1)
{
    for (char x=0;x<10;x=x+1)    // Create count of 0 thru 9
    {
```

The first SimpleC function in the for-loop is the lcd_goto function. This function has the parameter 0 so it positions the cursor at the first position of the LCD. This was already done when we cleared the screen but in the loop we need to reposition it each time.

```
lcd_goto(0);    // Select first line
```

The next SimpleC function we use is the lcd_symbol function. This sends the ASCII value in the parameter section to the LCD. In this case we send the loop variable value (0-9) to the LCD but first add the hex value 30 to create the proper ASCII value to send. The number 1 has the ASCII value 31 hex, 32 hex is for 2, etc.

```
lcd_symbol(0x30+x);    // Display decimal value
```

The program then uses the SimpleC pause function to delay 1000 milliseconds or 1 second before incrementing the variable. This makes the numbers change at a one second rate. From there the while-loop ends and so does the main-loop so this code runs over and over again.

```
pause(1000);    // Delay to read display
} //End While
} //End Main
```