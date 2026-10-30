| Function | Description |
|---|---|
| tcgetattr | fetch attributes (termios structure) |
| tcsetattr | set attributes (termios structure) |
| cfgetispeed | get input speed |
| cfgetospeed | get output speed |
| cfsetispeed | set input speed |
| cfsetospeed | set output speed |
| tcdrain | wait for all output to be transmitted |
| tcflow | suspend transmit or receive |
| tcflush | flush pending input and/or output |
| tcsendbreak | send BREAK character |
| tcgetpgrp | get foreground process group ID |
| tcsetpgrp | set foreground process group ID |
| tcgetsid | get process group ID of session leader for controlling TTY |

Figure 18.7 Summary of terminal I/O functions

The relationships among the 13 functions shown in Figure 18.7 are illustrated in Figure 18.8.

![](bbox=[0.15, 0.66, 0.92, 0.88])

Figure 18.8 Relationships among the terminal-related functions

POSIX.1 doesn't specify where in the termios structure the baud rate information is stored; that is an implementation detail. Some systems, such as Solaris, store this information in the c_cflag field. Linux and BSD-derived systems, such as FreeBSD and Mac OS X, have two separate fields in the structure: one for the input speed and one for the output speed.