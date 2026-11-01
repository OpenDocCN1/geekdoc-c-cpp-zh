```
char init_value = 0x3;
pause (15);    // wait 15mSec after power applied,
char temp = init_value;
LCD_DATA = LCD_DATA & 0xF0;
LCD_DATA = LCD_DATA + temp;
LCD_STROBE();
pause(10);
pause(10);
LCD_STROBE();
pause(10);
LCD_STROBE();
pause(10);
char temp = 2;  // Four bit mode
LCD_DATA = LCD_DATA & 0xF0;
LCD_DATA = LCD_DATA + temp;
LCD_STROBE();
// lcd_write(0x28); // Set interface length
// lcd_write(0x0C); // Display On, Cursor Off, Blink Off
// lcd_write(0x0F); // Display On, Cursor On, Cursor Blink
// lcd_clear(); // Clear screen
// lcd_write(0x06); // Set entry Mode
}
```

The next set of functions work on the hardware Universal Synchronous Asynchronous Receiver Transmitter (USART) peripheral. Using this feature can be very confusing to a beginner and sometimes even an experienced programmer so having a working library function to handle it is very useful. The first function I created for this is the initialization routine init_serial (). This function selects the baud rate (2400 or 9600) and defines the state of the Rx and Tx pins. There are a couple registers to set up; RXSTA and TXSTA, which the init_serial () routine does. All you have to do is select the baud rate and place it in the parameter section.

```
// *******************************************
// Initialize Hardware USART
// The serial commands all work with the hardware USART
// and is limited to 2400 baud or 9600 baud. Formula for
// baud rate calculation is FOSC/(64(SPBRG + 1)).
// *******************************************

void init_serial(int baud)
{
RX_PIN = 1;
TX_PIN = 0;
if (baud == 2400)
{SPBRG = 103;}          // 2400 Baud value
else                    // 9600 Baud value
{SPBRG = 25;}

//Continuous 8 bit asynchronous non inverted low speed communication
RCSTA = 0x90;           // SPEN and CREN bit = 1, RX9EN = 0
TXSTA = 0x20;           //TXEN = 1, BRGH = 0, SYNC = 0
BAUDCTL = 0;            //BRG16 = 0
}
```