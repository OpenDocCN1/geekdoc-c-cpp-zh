
```
C6 to PICkit 2 pin 4
Vdd to PICkit 2 pin 2
Gnd to PICkit 2 pin 3
*******************************/
```

The simplec1.1.h file is included along with the usual init_micro function.

```
#include "simplec1.1.h"

void main(void){
    init_micro();    // Setup micro ports
```

The first SimpleC library function for the USART is the init_serial function that has a parameter of 2400 or 9600 that selects the baud rate. These are the only two supported so far.

```
init_serial(9600); // set up the USART baud rate (2400 or 9600)
```

Now the main loop of code begins and you’ll see some other functions used that are actually part of standard libraries within the HI-TECH C compiler. They work with the USART perfectly. The putch () sends one ASCII character as defined by the parameter. It can be the ASCII character or the ASCII character value. This first for-loop uses these to send a number and then a carriage return plus line feed.

```
// *** Serial Communication Main Loop
while(1)
{
// ********** Send a decimal numbers from 1 to 9 **********
for (char count = 0x31; count <= 0x39; count = count +1)
{
    putch(count);        // Send Count 1-9 in ASCII
    pause(100);          // Delay 100 msec
}
putch(0x0D);           // Send ASCII value for
                       // carriage return
putch(0x0A);           // Send ASCII value for new
                       // line
```

The second for-loop sends the alphabet A through Z as ASCII characters using the PUTCH function.

```
// *********** Send the alphabet from A to Z ************
for (char count = 0x41; count <= 0x5A; count = count +1)
{
```

serial communication easier as well. This makes a great debug tool as well if you just want to send some status data. The PICkit 2 software can also collect and store characters received.

### Next Steps

I first suggest you try both the PICkit 2 and a USB to TTL converter module method of communication. Even though I didn’t show how to use a USB converter method, I did test it and it worked quite well. There are many different USB converter boards available so I won’t single one out here.

Changing the messages sent is an easy next step but getting the PICkit 2 to collect data and then opening that file in EXCEL or any spreadsheet program can be a great use of this project. You could combine an analog sensor reading program with this to create a data logger application. This is very handy and that is why the serial port is still popular in the embedded world even though the PC world has decided to move on.

## Chapter 12 – SimpleC I2C Communication

We started the projects in this book with an I2C communication project.
We'll end it the same way only this time we'll use the SimpleC library to make the software much easier to write. The project hardware and operation will be the same as Chapter 2 but will demonstrate how the SimpleC library makes this same project much easier to implement in software.

### Hardware

If you happen to have the hardware still setup from Chapter 2 then you are ready for software. If not, the 24LC01B chip is connected to the CHIPINO pin 3 and 4 (RC4 and RC3) and the LEDs connected to pins 8 thru 11 (RB0 thru RB3). The rest is built into the CHIPINO.

![](img/910b145bee7ca8076318eafbe6d13997_180_0.png)

Figure 12-1: EEPROM Schematic

The breadboard layout and the CHIPINO module connections are shown in Figure 12-2 and 12-3 so you can choose your setup.

![](img/910b145bee7ca8076318eafbe6d13997_181_0.png)

Figure 12-2: I2C EEPROM Breadboard Layout

![](img/910b145bee7ca8076318eafbe6d13997_181_1.png)

Figure 12-3: I2C EEPROM CHIPINO Module Connections

```
} //End Main
```

### How it Works

The familiar header block has a description of the program. After the header is the #include for the simplec1.1.h file.

```
/*
 *  I2C External EEPROM example using SimpleC
 *  This code will write 10 bytes to the EEPROM and
 *  then read them back and display binary value on LEDs.
 *  Connections:
 *  Pin 8(B0) - LED Anode - LED Cathode - 1k ohm - Ground
 *  Pin 9(B1) - LED Anode - LED Cathode - 1k ohm - Ground
 *  Pin 10(B2) - LED Anode - LED Cathode - 1k ohm - Ground
 *  Pin 11(B3) - LED Anode - LED Cathode - 1k ohm - Ground
 *
 *  Pin 3(C4) - 24LC01B SDA - 10k pullup - 5v
 *  Pin 4(C3) - 24LC01B SCL - 10k pullup - 5v
 *  24LC01B Vss - Ground
 *  24LC01B Vdd - 5v
 */

#include "simplec1.1.h"
```

The main loop is next and contains the init_micro function and the i2c_init that sets the I2C pins up for communication.

```
void
main(void)
{
    init_micro();    // Initialize I/O
    i2c_init();      // Initialize i2c
```

The LED ports are setup to have all the LEDs off by driving the I/O pins low.

```
PORTB=0x00;    // All LEDs off
TRISB=0x00;     // All PORTB outputs
```

A variable cnt is created that will be used to count the number of times through a while loop. It is initialized to zero at this same point in time.

```
unsigned char cnt=0;
```

A while loop runs through ten loops and stores a downward count in the EEPROM. The LEDs show the value of the cnt variable in binary by making the whole port equal to the variable value. Since we are only using the lower four bits of PORTB (CHIPINO pins 8-11) this method of control also affects the state of the pin 12, 13, B6 and B7 of the modules. Since we have nothing hooked up to those pins this works fine but if you adapt this code you may want to change that setup to control each LED individually.

```
while(cnt<=10)    /* write 10 numbers to eeprom */
{
PORTB=cnt;        // The cnt value will display on the LEDs
```

The I2C_EEOUT function does all the EEPROM communication work. The first parameter is the address and the second is the data. In this case the variable cnt is the address and the data is the value 10 minus the value of the variable cnt. It stores 9 at location 1, 8 at location 2, etc.

```
I2C_EEOUT(cnt,10-cnt);// Store 9 at address 1, 8 at address 2, ...
cnt=cnt+1;           // Increment cnt variable
```

A pause command is added to allow enough time to see the value displayed on the LEDs.

```
pause(255);          // Delay 255 milliseconds
}
```

The variable cnt is reset to zero and then the data is read back with another while loop. This time the I2C_EEIN function is used to read back the data. The parameter is the address and the data read back is sent to a variable. In this case we use PORTB label as the variable. The HI-TECH compiler allows this because the register names are setup as volatile variables in the specific header file for the PIC16F886 automatically included by the compiler. This line makes the LED's display the value read back from the EEPROM in binary form.

```
cnt=0;
while(cnt<=10)
{
PORTB =I2C_EEIN(cnt); // Display data read from EEPROM on
                       // LEDs in binary
```

A pause function has the parameter 1000 to create a 1 second delay allowing you to read the binary value on the LED's. This is slower than the delay for writing to the EEPROM so you can easily tell when it's writing and when its reading by the speed of the LED changes.

```
pause (1000);    // Delay for 1 second to read LEDs
```

The cnt variable is incremented for the next test of the value in the while loop. When the count reaches 10, the loop is done and the program jumps back to the beginning of the main loop, which starts the whole process over again.

```
cnt=cnt + 1;    // Increment cnt variable
} 
} //End Main
```

### Next Steps

Replacing the LED's with an LCD is the most logical next step and I've already showed you how easy that is with SimpleC. You could also add an ADCIN function to read a sensor, average it against previous readings and then store the result in the EEPROM. This would create a simple data logger for just about anything you can measure with an analog sensor.

### Conclusion

If you worked through the projects in my Beginner’s Guide to Embedded C Programming Volume 2 book, then at this point you should really understand how much typing the Simple C library saves you. In this book I wanted to give you a starting point for using the most common functions people asked for via email responses to my first two books in this series.

SimpleC can now help you make projects faster or prove out a concept quicker. I can see where several of these projects could be combined to create more complex projects. Combining the LCD, EEPROM and RS232 communication projects make a great starting point to building a data logger. The ADC could be used to read a sensor and the measurements displayed on the LCD while also being stored in EEPROM. Later on you could retrieve that data with a computer by connecting the serial port to the Rx and Tx pins of the data logger module. All that could be done in a short list of SimpleC functions. This is just one example of how these can be combined or at least give you a starting point for building more complex projects.

One thing I’ve found in talking to people who program in C is many of them rely on libraries of functions to build the projects from. These could be functions they created or functions they “borrowed” from another programmer. I’ve also seen many code examples on the internet that you can easily modify to fit your needs. The whole point of this book and my previous embedded C books are to teach you enough of the basics so you can understand the functions at these various other sources. By no means is there a standard approach either, therefore one persons code may be very helpful while another on the same topic may be so hard to follow you would be better off writing a new function yourself. That is the decision you have to make as the programmer.

I want to thank all those who read my first two books on Embedded C and then continued on with this one. It’s that loyalty that makes this long process of writing books seem worth all the nights of typing and typing and typing… It’s a very long process.
