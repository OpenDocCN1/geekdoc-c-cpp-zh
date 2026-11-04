The LCD can operate in either command or data mode, selected by pin **RS**. When **RS** is 0, command mode is selected and any data sent to the LCD is treated as a command. Examples of commands are: clearing the LCD, homing the cursor, and moving the cursor to the required column and row. Examples of data are displaying text or numbers on the LCD.

Figure 7.25 shows the program listing (Program: **I2CLCD.c**). GPIO pin numbering is used in this program. The main program simply calls function **lcd_puts** to display the text **Raspberry Pi**. At the beginning of the program, the connections between the LCD and the PCF8574 expander chip are defined. PCF is the index used here. **PCF+0** is set to index port pin P0 (LCD **RS** pin), **PCF+1** to index P1 (LCD **RW** pin), **PCF+2** to index P2 (LCD **E** pin), and so on.

The LCD program consists of several functions. Function **lcd_init** must be called before any other LCD function is used. This function initialises the LCD to operate with 4-bits of data mode. Function **lcd_strobe** sends a pulse to the LCD so the given command is accepted. This pulse consists of setting the **E** pin to logic 1 for a very short time and then setting it back to 0. Function **lcd_write** writes either a command or data to the LCD. The first argument is the command or data to be written. The second argument specifies whether this is a command (if 0), or data (if 1). The command or data byte is sent as two nibbles where the upper nibble is sent first, followed by the lower.

The other functions are used in command mode and have the following definitions:

+   - **lcd_clear**: clear the LCD.
+   - **lcd_home**: set the cursor to the home position (top left pixel).
+   - **lcd_cursor_blink_on**: set the cursor in blinking mode.
+   - **lcd_cursor_blink_off**: set the cursor in non-blinking mode.
+   - **lcd_cursor_on**: set the cursor to be visible.
+   - **lcd_cursor_off**: set the cursor to be invisible.
+   - **lcd_puts**: display string of data.
+   - **lcd_putch**: display a character.
+   - **lcd_goto**: move the cursor to the specified column, row. (0, 0) is the top-left pixel. The top row is 0, and the bottom row is 1. Column 0 is the first column at the left.