256

# Microcontroller Theory and Applications with the PIC18F

# TABLE 9.2 Typical LCD commands along with 8-bit codes in hex

| Hex | Command |
| :--- | :--- |
| 0x01 | Clear the screen |
| 0x02 | Return home |
| 0x04 | Shift cursor to left |
| 0x06 | Shift cursor to right |
| 0x05 | Shift display to right |
| 0x07 | Shift display to left |
| 0x08 | Display on, cursor off |
| 0x0A | Display off, cursor on |
| 0x0C | Display on, cursor off |
| 0x0E | Display on, cursor blinking |
| 0x10 | Shift cursor position to the left |
| 0x14 | Shift cursor position to the right |
| 0x80 | Move cursor to the start of the first line |

```
CALL LCDDATA
MOV LW 'a' ; Send ASCII a
CALL LCDDATA
MOV LW 'I' ; Send ASCII I
CALL LCDDATA
MOV LW 'u' ; Send ASCII u
CALL LCDDATA
MOV LW 'e' ; Send ASCII e
CALL LCDDATA
MOV LW ':' ; Send ASCII :
CALL LCDDATA
AGAIN MOVF PORTC, W ; Move switch value to WREG
ANDLW 0x0F ; Mask lower 4 bits
IORLW 0x30 ; Convert to ASCII data by ORing with 0x30
CALL LCDDATA ; Display switch value on screen
MOV LW 0x10 ; Shift cursor to left
CALL CMD
```

![](bbox=[0.11, 0.6, 0.82, 0.89])

# FIGURE 9.14 Figure for Example 9.4