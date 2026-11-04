
## Chapter 6 • LCD Projects

### 6.1 • Overview

In microcontroller-based systems, we usually want to interact with the system: For example, to enter a parameter, change its value, or display the output of a measured variable. Data is usually entered into a system using a switch, small keypad, or keyboard. Data is usually displayed using an indicator such as one or more LEDs, 7-segment displays, or LCDs. LCDs have the advantage that they can display alphanumeric as well as graphical data. Some LCDs have 40 or more character lengths with the capability to display data in several lines. Other LCDs can be used to display graphical images (Graphical LCDs, or simply GLCDs), such as animation. Some displays are in single or in multi-colour, while some others incorporate backlighting and so can be viewed in dimly lit conditions.

LCDs can be connected to a microcontroller in parallel or through I2C. Parallel LCDs (e.g. Hitachi HD44780) are connected using more than one data line and several control lines. The data is transferred in parallel. It is common to use either 4 or 8 data lines and two or more control lines. Using a 4 wire connection saves I/O pins but is slower due to data being transferred in two stages. I2C based LCDs on the other hand are connected to a microcontroller using only 2 wires, data, and a clock. In general, I2C based LCDs are much easier to use and require less wiring. However, they cost more than parallel types. In this chapter, we will be using 4 wire connections to LCDs.

The programming of LCDs is a complex task and requires a good understanding of the internal operations of LCD controllers, including knowledge of their exact timing requirements. Fortunately, several libraries can be used to simplify the use of both parallel and serial LCDs. In this chapter, we will be developing projects using LCDs with Raspberry Pi. The C language will be used in all projects.

### 6.2 • HD44780 LCD module

Although there are several types of LCDs, the HD44780 is one of the most popular LCD modules currently used in industry and by hobbyists (Figure 6.1). This module is an alphanumeric monochrome display and comes in different sizes. Modules with 16 columns are popular in most small applications, but other modules with 8, 20, 24, 32, or 40 columns are also available. Although most LCDs have two lines (or rows) as standard, it is possible to purchase models with 1 or 4 lines. LCDs are available with standard 14-pin connectors, although 16-pin modules are also available, providing terminals for backlighting. Table 6.1 gives the pin configuration and corresponding functions of a 16-pin LCD module. A summary of the pin functions is given below:

| Pin no | Name | Function |
| --- | --- | --- |
| 1 | VSS | Ground |
| 2 | VDD | +ve supply |
| 3 | VEE | Contrast |
| 4 | RS | Register select |
| 5 | R/W | Read/write |
| 6 | E | Enable |
| 7 | D0 | Data bit 0 |
| 8 | D1 | Data bit 1 |
| 9 | D2 | Data bit 2 |
| 10 | D3 | Data bit 3 |
| 11 | D4 | Data bit 4 |
| 12 | D5 | Data bit 5 |
| 13 | D6 | Data bit 6 |
| 14 | D7 | Data bit 7 |
| 15 | A | Backlight anode (+) |
| 16 | K | Backlight cathode (GND) |

Table 6.1 Pin configuration of HD44780 LCD module

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_179_0.png)

Figure 6.1 HD44780 compatible parallel LCD

V<sub>SS</sub> (pin 1) and V<sub>DD</sub> (pin 2) are the ground and power supply pins. The power supply should be +5V.

V<sub>EE</sub> is pin 3 and this is the contrast control pin used to adjust the contrast of the display. The arm of a 10K potentiometer is normally connected to this pin and the other two terminals of the potentiometer are connected to the ground and power supply pins. The contrast of the display is adjusted by rotating the potentiometer arm.

Pin 4 is the Register Select (RS) and when this pin is LOW, data transferred to the display is treated as commands. When RS is HIGH, character data can be transferred to and from the display.

Pin 5 is the Read/Write (R/W) line. This pin is pulled LOW to write commands or character data to the LCD module. When the pin is HIGH, character data or status information can be read from the module. This pin is normally connected permanently LOW so commands and character data can be sent to the LCD module.

Enable (E) is pin 6 which is used to initiate the transfer of commands or data between the LCD module and microcontroller. When writing to the display, data is transferred only on the HIGH to LOW transition of this pin. When reading from the display, data becomes available after the LOW to HIGH transition of the enable pin and this data remains valid as long as the enable pin is at logic HIGH.

Pins 7 to 14 are the eight data bus lines (D0 to D7). Data can be transferred between the microcontroller and LCD module using either a single 8-bit byte or as two 4-bit nibbles. In the latter case, only the upper four data lines (D4 to D7) are used. 4-bit mode has the advantage that four fewer I/O lines are required to communicate with the LCD. 4-bit mode is slower however due to the data being transferred in two stages. In this book, we will use the 4-bit interface.

Pins 15 and 16 are for background brightness control. To enable background brightness, a 220 Ohm resistor should be connected from pin 15 to +5V supply. Pin 16 should be connected to ground.

In 4-bit mode, the following pins of the LCD are used. The R/W line is permanently connected to ground. This mode uses 6 GPIO port pins of the microcontroller:

```
V_SS, V_DD, V_EE, E, RS, D4, D5, D6, D7
```

The libraries allow the control of 1, 2, and 4-line LCDs that are based on the **Hitachi HD44780** or compatible controllers. More than one LCD can be connected to Raspberry Pi. LCDs usually operate with +5V. There is no problem connecting them to Raspberry Pi GPIO pins because the display never writes data back to the Raspberry Pi (R/W pin is tied to GND).

### 6.3 • Project 1 – Displaying text

#### Description:

In this project, an LCD is connected to Raspberry Pi. The program displays text **Raspberry Pi** at row 0 (first row), column 2 of the LCD. Also, text **Computer** is displayed at row 1 (second row), column 4 of the display.

#### Aim:

This project aims to show how an LCD can be connected to Raspberry Pi, and be programmed using C.

#### Circuit diagram:

Figure 6.2 shows the circuit diagram of the project. The LCD is connected in 4-bit mode as follows:

| Raspberry Pi GPIO pin | LCD pin |
|---|---|
| GPIO 2 | D4 |
| GPIO 3 | D5 |
| GPIO 17 | D6 |
| GPIO 27 | D7 |
| GPIO 22 | RS |
| GPIO 10 | E |
| GND | R/W |
| GND | VSS |
| +5V | VDD |

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_181_0.png)

Figure 6.2 Circuit diagram of the project

Contrast is adjusted using a 10K potentiometer. The LCD background is lit by connecting pin 16 to ground and pin 15 to +5V through a 180 Ohm resistor.

#### Program listing:

#### wiringPi

The following header files must be included at the beginning of the program (see link: http://wiringpi.com/dev-lib/lcd-library/):

```c
#include <wiringPi.h>
#include <lcd.h>
```

The connections between the Raspberry Pi and LCD must be defined using the following function (assuming 4-bit operation):

```c
lcd = lcdInit(rows, cols, 4, RS, E, D4, D5, D6, D7, 0, 0, 0, 0);
```

Where rows and cols are the number of rows and columns respectively, the next is the number of bits used for the data interface (4-bit in this project), the remaining are the pins of the LCD. Notice only 4 data pins (D4-D7) are used. The function returns a handle (e.g. lcd) which is used in reference to LCD functions.

Some commonly used LCD functions supported by the LCD library are:

- **lcdHome (handle)**: home the cursor
- **lcdClear (handle)**: clear the LCD
- **lcdDisplay(fd, state)**: turn the display ON or OFF (state)
- **lcdCursor(fd, state)**: turn the cursor ON or OFF (state)
- **lcdCursorBlink(fd, state)**: turn blinking ON or OFF (state)
- **lcdPosition(handle, x, y)**: position the cursor at column x, row y. (0, 0) is the top left-hand corner of the LCD
- **lcdCharDef(handle, index, char data[8])**: this function allows the user to define 8-byte custom characters to represent a 5x8 array of pixels. Up to 8 custom characters (pointed to by the index argument) can be stored in LCD memory. Only the lower 5 bits are used in the character definition. The custom character created can be displayed using the **lcdPutchar** function call. Examples are given in later sections of this chapter.
- **lcdPutchar(handle, char data)**: display ASCII character data
- **lcdPuts(handle, char *string)**: display string
- **lcdPrintf(handle, char *message,...)**: display using the usual **printf** format

Figure 6.3 shows the program listing (Program: **LCDText.c**). GPIO pin numbering is used in this program. At the beginning of the program, the connections between Raspberry Pi and the LCD are defined as in Figure 6.2. Inside the main program function, **wiringPiSetupGpio** is called to initialise wiringPi and also to set the pin numbering mode to GPIO. Function **lcdInit** is then called to initialise the LCD library with 2 rows, 16 columns, 4-bit mode, and the pin connections as required. The LCD is cleared, the cursor is positioned at row 0, column 2, and the text **Raspberry Pi** is displayed. The cursor is then positioned at row 1, column 4, and the text **Computer** is displayed.
