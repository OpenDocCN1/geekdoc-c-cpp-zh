```
void delay_ms(unsigned int time)  //#25 2ms delay function
{
    unsigned int i, j;
    for(i=0; i<time; i++)
        for(j=0; j<255; j++);
}
```

In Figure 9.21, the four rows and four columns of the hex keyboard are connected to the PIC18F4321 via PORTC and PORTD respectively. The top row (row 0) of the keyboard is connected to RC0, next row (row 1) to RC1, next row (row 2) to RC2, and next row (row 3) to RC3. On the other hand, the rightmost column (column 0) is connected to RD3, next column to the left (column 1) to RD2, next column to the left (column 2) to RD1, and next column to the left (column 3) to RD0. In the figure, the columns of the keyboard connected to +5V, are normally HIGH. The key matrix at line #5 in the program is arranged differently than the Keyboard in Figure 9.21. For example, in the program Key ‘F’ is located at row 0 and column 0. Hence, key ‘F’ is located on the extreme right of the top row of the key matrix.

In order to detect a key actuation, 0’s are outputted on the four rows using “PORTC = 0x00;” (Line #13). If a key is pushed, that key will place a ‘0’ on the normally HIGH column connected to it. Thus, the pushed key will make one of the columns connected to it ‘0’, and the other three columns will be HIGH.

Line #18 clears a bit for row j, and line #19 outputs a LOW on that row. Line #20 detects if a key is pushed in column i connected to that row. Once the key is found, it is debounced (Line #21). With i and j, the key is obtained from the key matrix [j][i], and then outputted to PORTB on the seven segment display (Line #23).

![](bbox=[0.105, 0.58, 0.83, 0.885])

# **FIGURE 9.21**  PIC18F4321 interface to keyboard and display for the C-program