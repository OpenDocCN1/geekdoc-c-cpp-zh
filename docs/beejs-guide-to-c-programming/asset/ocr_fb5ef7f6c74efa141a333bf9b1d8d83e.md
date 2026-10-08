# Chapter 27. Unicode, Wide Characters, and All That

printf("%ls %lc\n", s, c);

Now—are those characters stored as Unicode code points, or not? Depends on the implementation. But you can test them if they are using the macro _STDC_ISO_10646__. If this is, the answer is, "It’s Unicode!"
More detailed, the value in macro is an integer in the year yyyym lets you know what Unicode standard you can rely on—whatever was in effect on that date.

How do you use them?

# 27.8.1 Multyte to wchar_t Conversions

So how do we get from the byte-oriented strings to the character-oriented wide strings and back?
We can use couple string conversion functions to make this happen.
First, some naming conventions you'll see in these functions:

+   - mb: multibyte
- wc: wide character
- mbs: multibyte string
- wcs: wide character string

So if we want to convert a multibyte string to a wide character, we can call the mbstowcs(). And the other way around: wcstombs().

| Conversion Function | Description |
|---|---|
| mbtowc() | Convert a multibyte character to a wide character. |
| wctow() | Convert a wide character to a multibyte character. |
| mbstowcs() | Convert a multibyte string to a wide string. |
| wcstombs() | Convert a wide string to a multibyte string. |

Let’s do a quick demo where we convert a multibyte string to a wide character, and compare the string lengths of the two using their respective functions.

```
#include <stdio.h>
#include <stdlib.h>
#include <wchar.h>
#include <string.h>
#include <locale.h>

int main(void)
{
    // Get out of the C locale to one likely has the euro symbol
    setlocale(LC_ALL, "");

    // Original multibyte string with a euro symbol (Unicode point 20ac)
    char *mb_string = "The cost is \u20ac1.23"; // €1.23
    size_t mb_len = strlen(mb_string);

    // Wide character array that will hold the converted string
    wchar_t wc_string[128]; // Holds up to 128 wide characters
```