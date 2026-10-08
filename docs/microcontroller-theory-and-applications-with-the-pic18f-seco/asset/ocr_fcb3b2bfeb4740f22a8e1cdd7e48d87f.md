```
    }
void cmd(unsigned char value)
{
    PORTD = value; // command is sent to PORT D
    PORTB = 0x04; // rs=0 rw=0 en=1
    delay(DELAYTIME); // delay 10ms
    PORTB = 0x00; // rs=0 rw=0 en=0
}

void data(unsigned char value)
{
    PORTD = value; // data is sent to PORTD
    PORTB = 0x05; // rs=1 rw=0 en=1
    delay(DELAYTIME); // 10ms delay
    PORTB = 0x01;//rs=1 rw=0 en=0
}

void delay(unsigned int itime)
{
    unsigned int i,j; // 2 ms delay. Can be verified from the
    for(i=0; i<itime; i++); // PIC18F assenbly program for LCD
    for(j= 0; j<255;j++);}
}
```

# 9.4 Interfacing PIC18F4321 to a hexadecimal keyboard and a seven-segment display

In this section we describe the basics of interfacing the PIC18F4321 microcontroller to a hexadecimal keyboard and a seven-segment display.

# 9.4.1 Basics of Keyboard and Display Interface to a Microcontroller

A common method of entering programs into a microcontroller is via a keyboard. An inexpensive way of displaying microcontroller results is by using seven-segment displays. The main functions to be performed for interfacing a keyboard are:

+   - Detect a key actuation.
- Debounce the key.
- Decode the key.

Let us now elaborate on keyboard interfacing concepts. A keyboard is arranged in rows and columns. Figure 9.15 shows a 2 × 2 keyboard interfaced to a typical microcontroller such as the PIC18F4321. In Figure 9.15, the columns are normally at a HIGH level. A key actuation is sensed by sending a LOW (closing the diode switch) to each row one at a time via RC0 and RC1 of port C. The two columns can then be inputted via RD2 and RD3 of PORTD to see whether any of the normally HIGH columns are pulled LOW by a key actuation. If so, the rows can be checked individually to determine the row in which the key is down. The row and column code for the key pressed can thus be found.

The next step is to debounce the key. Key bounce occurs when a key is pressed or released; it bounces for a short time before making the contact. When the bounce occurs, it