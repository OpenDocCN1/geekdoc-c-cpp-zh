The OUTSET and OUTCLR registers can be used to set or clear any GPIO
lines without changing the state of the others. If you write to either register
then the lines that correspond to one bits are set or cleared according
which register you write to. For example, suppose you want to set GPIO P0_0
a to 1 you can write 0x01 to the OUT register. However, this sets all of
the 31 pins to 0. If you write 0x01 to the OUTSET register then you set
P0_0 high and leave all of the others in their current state. Similarly, writing
0x01 to OUTCLR sets P0_0 and leaves the other in their current state.

There is a 32-bit DIR register which can be used to set any combination
pins to input or output depending on whether you write a 0 or a 1 to the
corresponding bit location.

The DIR and DIRCLR registers set the GPIO line to output or input
when you write a 1 to the corresponding bit location and make it easier for
to set lines to input or output without altering the remaining lines
set. Writing 0x01 to DIR sets P0_0 to output but all of the remaining
31 pins to input. Writing 0x01 to DIRSET will set only P0_0 to output and
writing it to DIRCLR will set only P0_0 to input.

To summarize, the registers controlling the bank of GPIO lines:

+   * 32 PIN[n] configuration registers, for each GPIO line
* OUT sets any combination of GPIO lines high or low
* OUTSET sets any combination of GPIO lines high
* OUTCLR sets any combination of GPIO lines low
* IN reads the state of all GPIO lines
* DIR sets the I/O direction of any combination of GPIO lines
* DIRSET sets any combination of GPIO lines to output
* DIRCLR sets any combination of GPIO lines to input

Of course, need to know which bits in the configuration register controls
what aspect of the GPIO line.

| Bits | DIR |
|---|---|
| 0 | DIR 0 = input, 1 = output |
| 1 | INPUT 0 = disconnect input, 1 = connect |
| 3,2 | PULL 00 = No Pull, 01 = Pull-Down, 11 = Pull-Up |
| 10,9,8 | DRIVE 000 S01, 001 H0S1, 010 S0H1, 011 H0H1, 100 D0S1, 101 D0H1, 110 S0D1, 111 H0D1 |
| 17,16 | SENSE 00 = disabled, 01 = High, 11 = Low |