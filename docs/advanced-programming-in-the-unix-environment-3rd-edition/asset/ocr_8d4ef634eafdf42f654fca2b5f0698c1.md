All the terminal device characteristics that we can examine and change are contained in a termios structure. This structure is defined in the header <termios.h>, which we use throughout this chapter:

```
struct termios {
    tcflag_t c_iflag;    /* input flags */
    tcflag_t c_oflag;    /* output flags */
    tcflag_t c_cflag;    /* control flags */
    tcflag_t c_lflag;    /* local flags */
    cc_t     c_cc[NCCS]; /* control characters */
};
```

Roughly speaking, the input flags control the input of characters by the terminal device driver (e.g., strip eighth bit on input, enable input parity checking), the output flags control the driver output (e.g., perform output processing, map newline to CR/LF), the control flags affect the RS-232 serial lines (e.g., ignore modem status lines, one or two stop bits per character), and the local flags affect the interface between the driver and the user (e.g., echo on or off, visually erase characters, enable terminal-generated signals, job control stop signal for background output).

The type tcflag_t is big enough to hold each of the flag values and is often defined as an unsigned int or an unsigned long. The c_cc array contains all the special characters that we can change. NCCS is the number of elements in this array and is typically between 15 and 20 (since most implementations of the UNIX System support more than the 11 POSIX-defined special characters). The cc_t type is large enough to hold each special character and is typically an unsigned char.

> Versions of System V that predated the POSIX standard had a header named <termio.h> and a structure named termio. POSIX.1 added an s to the names, to differentiate them from their predecessors.

Figures 18.3 through 18.6 list all the terminal flags that we can change to affect the characteristics of a terminal device. Note that even though the Single UNIX Specification defines a common subset that all platforms start from, all the implementations have their own additions. Most of these additions come from the historical differences between the systems. We'll discuss each of these flag values in detail in Section 18.5.

Given all the options available, how do we examine and change these characteristics of a terminal device? Figure 18.7 summarizes the various functions defined by the Single UNIX Specification that operate on terminal devices. (All the functions listed are part of the base POSIX specification. We described tcgetpgrp, tcsetsid, and tcsetpgrp in Section 9.7.)