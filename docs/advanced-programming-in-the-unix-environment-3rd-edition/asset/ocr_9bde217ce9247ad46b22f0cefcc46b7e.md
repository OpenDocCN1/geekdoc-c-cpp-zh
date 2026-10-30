IUTF8 (c_iflag, Linux, Mac OS X) Allow character erase processing to work with UTF-8 multibyte characters.

IXANY (c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) Enable any characters to restart output.

IXOFF (c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) If set, start-stop input control is enabled. When it notices that the input queue is getting full, the terminal driver outputs a STOP character. This character should be recognized by the device that is sending the data and cause the device to stop. Later, when the characters on the input queue have been processed, the terminal driver will output a START character. This should cause the device to resume sending data.

IXON (c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) If set, start-stop output control is enabled. When the terminal driver receives a STOP character, output stops. While the output is stopped, the next START character resumes the output. If this flag is not set, the START and STOP characters are read by the process as normal characters.

MDMBUF (c_cflag, FreeBSD, Mac OS X) Flow control the output according to the modem carrier flag. This is the old name for the CCAR_OFLOW flag.

NLDLY (c_oflag, XSI, Linux, Solaris) Newline delay mask. The values for the mask are NL0 or NL1.

NOFLSH (c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) By default, when the terminal driver generates the SIGINT and SIGQUIT signals, both the input and output queues are flushed. Also, when it generates the SIGSUSP signal, the input queue is flushed. If the NOFLSH flag is set, this normal flushing of the queues does not occur when these signals are generated.

NOKERNINFO (c_iflag, FreeBSD, Mac OS X) When set, this flag prevents the STATUS character from printing information on the foreground process group. Regardless of whether this flag is set, however, the STATUS character still causes the SIGINFO signal to be sent to the foreground process group.

OCRNL (c_oflag, XSI, FreeBSD, Linux, Solaris) If set, map CR to NL on output.

OFDEL (c_oflag, XSI, Linux, Solaris) If set, the output fill character is ASCII DEL; otherwise, it's ASCII NUL. See the OFILL flag.

OFILL (c_oflag, XSI, Linux, Solaris) If set, fill characters (either ASCII DEL or ASCII NUL; see the OFDEL flag) are transmitted for a delay, instead of using a timed delay. See the six delay masks: BSDLY, CRDLY, FFDLY, NLDLY, TABDLY, and VTDLY.

OLCUC (c_oflag, Linux, Solaris) If set, map lowercase characters to uppercase characters on output.