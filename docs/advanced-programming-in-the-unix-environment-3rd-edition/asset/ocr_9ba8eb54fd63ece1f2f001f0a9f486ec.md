The four baud rate functions exist to insulate applications from differences in the way that implementations represent baud rates in the termios structure. Linux and BSD-derived platforms tend to store baud rates as numeric values equal to the rates (i.e., 9,600 baud is stored as the value 9,600), whereas System V-derived platforms (such as Solaris) tend to encode the baud rate in a bitmask. The speed values we get from the cfget functions and pass to the cfset functions are untranslated from their representation as they are stored in the termios structure.

# 18.8 Line Control Functions

The following four functions provide line control capability for terminal devices. All four require that fd refer to a terminal device; otherwise, -1 is returned with errno set to ENOTTY.

```
#include <termios.h>

int tcdrain(int fd);
int tcflow(int fd, int action);
int tcflush(int fd, int queue);
int tcsendbreak(int fd, int duration);

All four return: 0 if OK, -1 on error
```

The tcdrain function waits for all output to be transmitted. The tcflow function gives us control over both input and output flow control. The action argument must be one of the following four values:

+   TCOOFF Output is suspended.
+   TCOON Output that was previously suspended is restarted.
+   TCIOFF The system transmits a STOP character, which should cause the terminal device to stop sending data.
+   TCION The system transmits a START character, which should cause the terminal device to resume sending data.

The tcflush function lets us flush (throw away) either the input buffer (data that has been received by the terminal driver, which we have not read) or the output buffer (data that we have written, which has not yet been transmitted). The queue argument must be one of the following three constants:

+   TCIFLUSH The input queue is flushed.
+   TCOFLUSH The output queue is flushed.
+   TCIOFLUSH Both the input and the output queues are flushed.