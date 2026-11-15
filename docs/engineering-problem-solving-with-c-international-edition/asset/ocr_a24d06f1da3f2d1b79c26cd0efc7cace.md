type to receive the value returned by the getchar function so that we can store the EOF and detect the end of data. The following statements cause one character to be read from the keyboard and printed on a new line:

```
int c;
...
putchar('\n');
c = getchar();
putchar(c);
putchar('\n');
```

The actual value of the EOF is system dependent. The EOF character is often represented by the control-z character. A control-z is entered from the keyboard by pressing the control (ctrl) key, and then pressing the z key while the control key is still pressed. This combination of characters is often written as ^z (control-z), but is not the same as pressing the ^ key with the z key. The use of EOF will be discussed in more detail in Chapter 3.

# Character Comparisons

Character functions

The Standard C library contains additional functions for use with characters. These character functions fall into two categories; one set of functions is used to convert characters between uppercase and lowercase, and the other set is used to perform character comparisons. The following preprocessor directive should be used in programs referencing these character functions:

```
#include <ctype.h>
```

The following statement converts the lowercase letter stored in the variable ch to an uppercase character and stores the result in the character variable upper:

```
upper = toupper(ch);
```

If ch is a lowercase letter, the function toupper returns the corresponding uppercase letter; otherwise, the function returns ch. Note that no change is made to the variable ch.

Each character function requires an integer argument, and each function returns an integer value. The character comparison functions return a nonzero value if the comparison is true; otherwise, they return a zero. We now list these functions with a brief explanation:

| tolower(ch) | If ch is an uppercase letter, this function returns the corresponding lowercase letter; otherwise, it returns ch. |
| toupper(ch) | If ch is a lowercase letter, this function returns the corresponding uppercase letter; otherwise, it returns ch. |
| isdigit(ch) | This function returns a nonzero value if ch is a decimal digit; otherwise, it returns zero. |
| islower(ch) | This function returns a nonzero value if ch is a lowercase letter; otherwise, it returns zero. |
| isupper(ch) | This function returns a nonzero value if ch is an uppercase letter; otherwise, it returns a zero. |
| isalpha(ch) | This function returns a nonzero value if ch is an uppercase letter or a lowercase letter; otherwise, it returns a zero. |
| isalnum(ch) | This function returns a nonzero value if ch is an alphabetic character or a numeric digit; otherwise, it returns a zero. |