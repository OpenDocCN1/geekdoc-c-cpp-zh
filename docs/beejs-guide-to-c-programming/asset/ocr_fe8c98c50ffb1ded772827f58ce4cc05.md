# Chapter 27. Unicode, Wide Characters, and All That

+   * wcrtomb()—wide character to multibyte
* mbstowcs()—multibyte string to wide character string
* wcstombs()—wide string to multibyte string

These are similar to their non-restartable counterparts, except they require you passing a pointer to your own mstate_t variable. And they they modify the source pointer (to help you out if invalid bytes are found), so it might be useful to save a copy of the original.

Here's the example from earlier in the chapter reworked to pass your own mstate_t.

```
#include <stdio.h>
#include <stdlib.h>
#include <stddef.h>
#include <wchar.h>
#include <string.h>
#include <locale.h>
```

```
int main(void)
{
    // Get out of the C locale to one likely has the euro symbol
    setlocale(LC_ALL, "");

    // Original multibyte string with a euro symbol (Unicode point 20ac)
    char *mbs_string = "The cost is \u20ac.23"; // €1.23
    size_t mb_len = strlen(mbs_string);
```

```


// Wide character array that will hold the converted string
wchar_t wc_string[128]; // Holds up to 128 wide characters
```

```
// Set up the conversion state
mbsstate_t mbs;
memset(&mbs, 0, sizeof(mbs)); // Initial state
```

```


// mbsrtowcs() modifies the input pointer point to the first
invalid character, or NULL if success. Let's make a copy of
// the pointer for mbsrtowcs() to mess with so our original is
unchanged.
```

```


// This will will be successful, but we check further
down to see.
const char *invalid = mbs_string;
```

```
// Convert the MB to WC; this returns the number of wide chars
size_t wc_len = mbstowcs(wc_string, invalid, 128, &mbs);
```

```

if (invalid == NULL) {
    printf("--No invalid characters found--\n");
```

```

    // Print result--the %ls for wide char strings
    printf("multibyte: \%%s (%%zu bytes)\%%\n", mbs_string, mb_len);
    printf("wide char: \%%ls (%%zu characters)\%%\n", wc_string, wc_len);
} else {
    ptrdiff_t offset = invalid - mbs_string;
    printf("Invalid character at offset %td\n", offset);
}
```