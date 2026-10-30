The tcsendbreak function transmits a continuous stream of zero bits for a specified duration. If the duration argument is 0, the transmission lasts between 0.25 second and 0.5 second. POSIX.1 specifies that if duration is nonzero, the transmission time is implementation dependent.

# 18.9 Terminal Identification

Historically, the name of the controlling terminal in most versions of the UNIX System has been /dev/tty. POSIX.1 provides a runtime function that we can call to determine the name of the controlling terminal.

```
#include <stdio.h>

char *ctermid(char *ptr);

Returns: pointer to name of controlling terminal on success, pointer to empty string on error
```

If ptr is non-null, it is assumed to point to an array of at least L_ctermid bytes, and the name of the controlling terminal of the process is stored in the array. The constant L_ctermid is defined in <stdio.h>. If ptr is a null pointer, the function allocates room for the array (usually as a static variable). Again, the name of the controlling terminal of the process is stored in the array.

In both cases, the starting address of the array is returned as the value of the function. Since most UNIX systems use /dev/tty as the name of the controlling terminal, this function is intended to aid portability to other operating systems.

All four platforms described in this text return the string /dev/tty when we call ctermid.

# Example — ctermid Function

Figure 18.12 shows an implementation of the POSIX.1 ctermid function.

```
#include <stdio.h>
#include <string.h>

static char ctermid_name[L_ctermid];

char *
ctermid(char *str)
{
    if (str == NULL)
        str = ctermid_name;
    return(strcpy(str, "/dev/tty"));    /* strcpy() returns str */
}
```

Figure 18.12 Implementation of POSIX.1 ctermid function