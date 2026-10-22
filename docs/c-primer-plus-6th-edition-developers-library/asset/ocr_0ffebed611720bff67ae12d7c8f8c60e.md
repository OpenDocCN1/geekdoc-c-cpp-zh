Perhaps you are wondering what’s the rationale for discarding the rest of a too-long line. The problem is that if the remainder of the line is left in place, it becomes the input for the next read statement. This can, for example, cause the program to crash if the next read statement is looking for a type double value. Discarding the rest of the line keeps the read statements synchronized with the keyboard input.

Our s_gets() function isn’t perfect. Its most serious flaw is that it is silent about encountering input that doesn’t fit. It discards the extra input with neither the program nor the user being informed, thus closing off other options, such as having the user try again or finding more storage space. Another flaw is that it doesn’t cope with misuse such as being passed a size of 1 or less. But it’s good enough to serve as a gets() substitute for our examples.

# The scanf() Function

Let’s visit scanf() again. We’ve used scanf() with the %s format before to read a string. The chief difference between scanf() and gets() or fgets() lies in how they decide when they have reached the end of the string: scanf() is more of a “get word” than a “get string” function. The gets() function, as you’ve seen, takes in all the characters up to the first newline, as does fgets(), if the string is short enough. The scanf() function has two choices for terminating input. For either choice, the string starts at the first non-whitespace character encountered. If you use the %s format, the string runs up to (but not including) the next whitespace character (blank, tab, or newline). If you specify a field width, as in %10s, the scanf() collects up to 10 characters or up to the first whitespace character, whichever comes first (see Figure 11.3).

| Input Statement | Original Input Queue* | Name Contents | Remaining Queue |
|---|---|---|---|
| scanf("%s", name); | Fleebert□Hup | Fleebert | □Hup |
| scanf("%5s", name); | Fleebert□Hup | Fleeb | ert□Hup |
| scanf("%5s", name); | Ann□Ular | Ann | □Ular |

*the □ represents the space character

Figure 11.3 Field widths and scanf().

Recall that the scanf() function returns an integer value that equals the number of items successfully read or returns EOF if it encounters the end of file.

Listing 11.11 illustrates how scanf() works when you specify a field width.

# Listing 11.11 The scan_str.c Program

```
/* scan_str.c -- using scanf() */
#include <stdio.h>
```