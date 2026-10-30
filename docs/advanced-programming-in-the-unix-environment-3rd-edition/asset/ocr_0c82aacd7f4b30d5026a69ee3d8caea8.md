Option names preceded by a hyphen are disabled. The last four lines display the current settings for each of the terminal special characters (Section 18.3). The first line displays the number of rows and columns for the current terminal window; we discuss the terminal window size in Section 18.12.

The stty command uses its standard input to get and set the terminal option flags. Although some older implementations used standard output, POSIX.1 requires that the standard input be used. All four implementations discussed in this text provide versions of stty that operate on the standard input. This means that we can type

```
stty -a < /dev/tty1a
```

if we are interested in discovering the settings on the terminal named tty1a.

# 18.7 Baud Rate Functions

The term *baud rate* is a historical term that should be referred to today as “bits per second.” Although most terminal devices use the same baud rate for both input and output, the capability exists to set the two rates to different values, if the hardware allows this.

```
#include <termios.h>

speed_t cfgetispeed(const struct termios *termptr);

speed_t cfgetospeed(const struct termios *termptr);

                                      Both return: baud rate value

int cfsetispeed(struct termios *term_ptr, speed_t speed);

int cfsetospeed(struct termios *term_ptr, speed_t speed);

                                      Both return: 0 if OK, −1 on error
```

The return value from the two cfget functions and the *speed* argument to the two cfset functions are one of the following constants: B50, B75, B110, B134, B150, B200, B300, B600, B1200, B1800, B2400, B4800, B9600, B19200, or B38400. The constant B0 means “hang up.” If B0 is specified as the output baud rate when tcsetattr is called, the modem control lines are no longer asserted.

Most systems define additional baud rate values, such as B57600 and B115200.

To use these functions, we must realize that the input and output baud rates are stored in the device’s termios structure, as shown in Figure 18.8. Before calling either of the cfget functions, we first have to obtain the device’s termios structure using tcgetattr. Similarly, after calling either of the two cfset functions, all we’ve done is set the baud rate in a termios structure. For this change to affect the device, we have to call tcsetattr. If there is an error in either of the baud rates that we set, we may not find out about the error until we call tcsetattr.