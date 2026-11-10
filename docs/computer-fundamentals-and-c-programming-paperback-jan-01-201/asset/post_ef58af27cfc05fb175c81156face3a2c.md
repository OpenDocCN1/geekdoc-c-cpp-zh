
**Takeaway:** `scanf` returns 0 if it fails to match any item. But if `scanf` encounters EOF before reading the first item, it returns the value of EOF (usually -1). It is better to specify EOF (rather than -1) in your programs.

### 9.9.2 `scanf_retval.c`: Program to Extract Numbers from a String

Program 9.6 extracts integers embedded in an input character stream and adds them. It shows the skillful exploitation of the return value in handling every possible mismatch that may occur. As the output shows, as long as there are numerals embedded in a string, they will be extracted, converted and added. It just doesn’t matter what the other characters are.

This program which terminates when EOF is sent from the keyboard, checks for three possible return values: 1, 0 and EOF (-1). `scanf` returns 1 when it successfully separates an integer from the rest of the string. It successfully extracts 3 from 3-three and 5 from 5(five). When `scanf` meets the non-numeric characters, it returns 0. Because `getchar` runs in a loop, it has no problem in ridding the buffer of these troublemakers.

```c
/* scanf_retval.c: Uses scanf to add integers embedded in a string.
                 Employs the return value to handle mismatches. */
#include <stdio.h>
int main(void)
{
    short num, total = 0;
    int retval;

    printf("Enter integers to sum, EOF to quit: ");
    while ((retval = scanf("%hd", &num)) != EOF)
        if (retval == 1)                    /* Right input */
            total += num;
        else if (retval == 0)               /* Wrong input ... */
            getchar();                       /* ... so clear buffer */

    printf("Total: %d\n", total);
    return 0;
}
```

**PROGRAM 9.6: `scanf_retval.c`**

```text
Enter integers to sum, EOF to quit: 1 3 5 [Ctrl-d]
Total: 9
Enter integers to sum, EOF to quit: Add 3 to 5 and also 100. [Ctrl-d]
Total: 108
Enter integers to sum, EOF to quit: "1", 3-three & 5(five) [Ctrl-d]
Total: 9
Enter integers to sum, EOF to quit: 1.3.5 [Ctrl-d]
Total: 9
```

PROGRAM OUTPUT: `scanf_retval.c`

## 9.10 `scanf`: THE MAJOR FORMAT SPECIFIERS

**scanf** formats the input stream using format specifiers in the control string. A format specifier begins with a % followed by a *conversion code* (like the d in %d). The following generalized form also shows the optional components between the % and the conversion code:

```
% * field width modifier conversion code
```

The specifier `%*4hd` contains all optional components—the asterisk, field width (4) and modifier (h). These components have the following significance:

- The `*` flag is used for skipping a field.
- The *field width* specifies the *maximum* number of characters to be matched. Thus, `%4d` matches at most four digit-characters.
- A *modifier* changes the data type of the variable. You have used most of these modifiers on several occasions: h, l, L or ll.

An exhaustive list of format specifiers (including modifiers and a flag) used by **scanf** is shown in Table 9.1. We will now discuss the major format specifiers.

**TABLE 9.1** Format Specifiers Used by **scanf**

| Integer | short | int | long | long long |
|---|---|---|---|---|
| Signed Decimal | `%hd` | `%d` | `%ld` | `%lld` (C99) |
| Unsigned Decimal | `%hu` | `%u` | `%lu` | `%llu` (C99) |
| Octal | `%ho` | `%o` | `%lo` | `%llo` (C99) |
| Hex | `%hx` | `%x` | `%lx` | `%llx` (C99) |
| Decimal/Octal/Hex | `%hi` | `%i` | `%li` | `%lli` (C99) |

| Floating Point | float | double | long double |
|---|---|---|---|
| Normal or exponential | `%f`, `%e`, `%g` | `%lf`, `%le`, `%lg` | `%Lf`, `%Le`, `%Lg` |
| Synonyms | `%F`, `%E`, `%G` | `%lF`, `%lE`, `%lG` | `%LF`, `%LE`, `%LG` |

| Other Format Specifiers | Matches |
|---|---|
| `%c` | Character (char) |
| `%s` | Character string comprising a single word |
| `%p` | Pointer |
| `%n` | Nothing, but saves count of characters matched in a variable |
| `%%` | % |
| `%[...]` (*scan set*) | Any character in list |
| `%[^...]` (*scan set*) | Any character not in list |

| Flag | Significance |
|---|---|
| `*` | Skips a field |

### 9.10.1 Handling Numeric Data (%d and %f)

Integer and floating point data are represented by the conversion codes d and f, respectively, with or without modifiers. Note the following attributes of their format specifiers:

- `%d` matches 7, but it truncates 7.25 and leaves the string `.25` in the buffer.
- `%f` matches both an integer and a real number expressed in decimal or exponential notation. Thus, it matches 7, 713.5 and 7.135E2. In this respect, `%f` differs with its peer in `printf`.

A field width *n* matches up to *n* digits of an integer. For a floating point number, *n* includes the decimal point. So, when matching `%5f` with 3.14285, `scanf` selects 3.142 and returns 85 to the buffer. Unlike with `printf`, it is not possible to specify the width of the decimal portion by using, say, `%6.2f`.

![](img/d75612dcf3ab36327142238ab5bb21d8_305_0.png)

> **Caution:** Never use `scanf` with `%d` or `%u` to read a floating point number. `scanf` reads the integral part and returns the decimal portion to the buffer.

### 9.10.2 Handling Character Data (%c)

`scanf` uses `%c` to match a single character which can be a whitespace character. If you enter y and [Enter] in response to `scanf("%c", &x)`, the `\n` remains in the buffer. If the next `scanf` call uses `%d` or `%f`, the `\n` (which is now leading whitespace) will be ignored. But if the next `scanf` is another `%c`, then the second `scanf` call will match the `\n` and return without pausing. That’s why the buffer must be cleared between successive runs of `scanf` with `%c`.

While `%d%d%d` or `%f%f%f` ignores leading whitespace, `%c%c%c` does not. Surprisingly, `%c%c%c` matches three or more spaces, the string abc, but not a  b  c. However, `%c  %c  %c` matches abc, a  b  c, a□□b□c (two spaces separating the characters), but it doesn’t match only spaces. Table 9.2 shows the use of %c in matching one or more characters. The last three examples show the effect of using non-whitespace characters in the format specifier.

**TABLE 9.2** Matching char Data Type in scanf

| Format Specifier | Input String | Matches |
|---|---|---|
| `"%c"` | y | y (`\n` in buffer) |
| `"%c"` | yes | y (es`\n` in buffer) |
| `"%c%c%c"` | abc | abc |
| `"%c%c%c"` | a b c | a b (space, c`\n` in buffer) |
| `"%c %c %c"` | abc | abc |
| `"%c %c %c"` | a b c | a b c |
| `"%c:%c:%c"` | a:b:c | a:b:c |
| `"%c : %c : %c"` | a:b:c | a:b:c |
| `"%c : %c : %c"` | a : b : c | a : b : c |

### 9.10.3 Handling String Data (%s)

We know a string as an array of characters terminated by NUL (5.15), but that is not how scanf understands a string. To scanf, a string is simply a token or word, i.e. a set of one or more non-whitespace characters. scanf reads this word with the %s format specifier and the name of the array as its matching argument. Thus, if you have defined an array named stg as

```c
char stg[20];  // Array must be of type char
```

then you can fill up the array by using scanf like this:

```c
scanf("%s", stg);  // stg not &stg
```

scanf ignores leading whitespace and reads until it encounters a whitespace character or EOF. It saves the word in the array stg and tags a NUL character at the end. This means that the array must have an extra element for NUL. Note that scanf doesn't use the & prefix when %s is used. The name of the array itself provides the address that scanf needs.

The word-based approach used by scanf makes it unsuitable for reading a multi-word string. To match three words, scanf needs three %s specifiers (a single one for printf) and the addresses of three arrays. There are two solutions to this problem and one of them is discussed in Section 9.11.1.

> **Takeaway:** printf and scanf differ in their treatment of %s. This specifier matches a single word in scanf but one or more words in printf.

### 9.10.4 scanf_char_string.c: Characters and Strings as Input

Program 9.7 uses %c and %s to handle character and string input. It also uses the field width to split a string into three. The getchar sequence is used twice to clear the buffer, so it makes sense to use a macro (FLUSH_BUFFER) in this program.

Because whitespace in the control string ("%c %c %c") matches zero or more occurrences of leading whitespace in the data, we could key in both ABC and a b c. The final invocation of scanf uses "%3s%3s%3s" to split the string septenov into three separate strings. Each array has an extra byte to let scanf append the NUL at the end.

## 9.11 scanf: OTHER FEATURES

Our coverage of the scanf function would not be complete without a discussion on the (i) the scan set, (ii) the only flag supported by it, and (iii) some more format specifiers. These topics are examined in the following sections.

### 9.11.1 The Scan Set Specifier

The scan set specifier comprises one or more characters enclosed by [ and ]. For instance, %[aeiou] represents a scan set that matches only vowel characters. However, a caret at the beginning of the
