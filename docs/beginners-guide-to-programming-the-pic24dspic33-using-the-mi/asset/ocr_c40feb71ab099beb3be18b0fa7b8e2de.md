+   - LCD_Initialize () - initializes the LCD display and makes it ready for output. This needs to be called before any other LCD function is called. Keep in mind initialization is a two-step process, first the PIC24H must initialize it ports for output connection to the LCD and then once this is achieved it then executes the LCD initialization command sequence. Also keep in mind that the library is written specifically to support the connections illustrated in the schematic. Any deviation from this wiring will cause the LCD library not to work correctly.

The LCD requires specific initialization sequence for its proper operation. There is also a strict command set for PIC24H to interact with the LCD for writing command and data and also positioning the LCD cursor. These functions are performed by using the supplied 'C' library functions. Both an initialization sequence and command interface using elements of the 'C' library are shown for illustration. You are encouraged to review this code (in project under Graphics.c) and compare it against the LCD display data sheet that comes with the display (see Figure 5-4).

# Initialization Definitions in Graphics Library (Graphics.c)

```
//LCD Hardware Interface
#define LCDPORT LATB
#define E LATBbits.LATB11
#define RS LATBbits.LATB10
//Table for Initialization Instructions 8 bits 3.3V
#define FUNC1 0x20 // LCD 4bits 2 lines Table select 1
#define BIAS 0x15 // BIAS 1:3 / line LCD
#define PWRCNTRL 0x95 // Power control on, booster on, contrast 64
#define FOLLOW 0xC0 // Boost converter follower and pass
#define CONTRAST 0x72 // Set contrast 0x72
#define FUNC2 0x28 // Switch back to table
#define DISPLAY 0x0F // Display on/off - Display on, cursor on, cursor blink
#define CLEAR 0x01 // Clear display - return home
#define ENTRY 0x06 // Increment automatically
```

# Initialization Sequence in Graphics Library (Graphics.c)

```
//FUNC1
LCDWrite(FUNC1); // 0x20
// BIAS
LCDWrite(BIAS); // 0x15
//PWRCNTRL
LCDWrite(PWRCNTRL); // 0x95
//FOLLOW
LCDWrite(FOLLOW); // 0xC0
//CONTRAST
LCDWrite(CONTRAST); // 0x72
//FUNC2
LCDWrite(FUNC2); // 0x28
//DISPLAY
LCDWrite(DISPLAY); // 0x0F
//CLEAR
LCDWrite(CLEAR); // 0x01
//ENTRY
LCDWrite(ENTRY); // 0x06
```

Figure 5-4: LCD Code for Initialization