The SimpleC lcd_text function does the work for us. The parameters of this function are placed between quotes so it knows this is a string. Each letter is then sent as an ASCII value to the LCD module. This displays the message “Simple C Makes” on the first line of the LCD.

```
```c
lcd_text("Simple C Makes");    // Display Hello World
```
```

Now the LCD cursor is positioned on the second line with a hex value 40 as the parameter. This is the value for the beginning of the second line. The lcd_goto handles the code that indicates this is a command character. After this function runs, the cursor will be at the beginning of the second line.

```
```c
lcd_goto(0x40);                 // Select second line
```
```

Now the lcd_text function is used to write the second message, which is “Programming Easy”.

```
```c
lcd_text("Programming Easy");
```
```

We pause a second and then loop back to write the message again.

```
```c
pause (10000);           // Delay for 1 second to read display
```
```

```
```c
} //End While
```
```

```
```c
} //End Main
```
```

# Next Steps

You can change the message in the second project and even play with the lcd_goto functions to move the message around. The first project can count through the whole ASCII library if you want by increasing the loop count and starting at a lower value. You can combine the two and display a message on the first line and then a number on the second line. In fact that is what the next chapter does with another of the SimpleC LCD functions. Let’s move on to the next chapter and use the same hardware with a few additional connections.