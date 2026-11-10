
```c
/* dos2unix.c: Converts an MSDOS file to UNIX.
                Removes the CR character before every newline. */
#include <stdio.h>
int main(void)
{
    int c;
    while ((c = getc(stdin)) != EOF) {
        if (c == '\r')          /* If \r, then ... */
            if ((c = getc(stdin)) != '\n')  /* ... check next character */
                ungetc(c, stdin);            /* Put it back if not \n */
            else
                putc('\n', stdout);
        else
            putc(c, stdout);
    }
    return 0;
}
```

PROGRAM 9.4: dos2unix.c

Since we are using *stdin* and *stdout*, we need to adopt the redirection technique discussed previously to execute the program:

```
a.out < foo1 > foo2                a.out for Linux
```

After you have read Chapter 15, you should be able to modify this program and its inverse counterpart (*unix2dos.c*) to handle disk files directly without using the < and > symbols. Unlike *stdin* and *stdout*, disk files have to be opened explicitly to be read or written. You'll find these programs useful for moving files across diverse platforms.

The functions and macros that we have discussed so far read and write data as *characters*. They cannot identify or handle specific data types in the character stream. The rest of this chapter examines the **scanf** and **printf** functions that convert character data into specific data types and vice versa. Though both functions have been used extensively in previous chapters, there's a lot that we still need to know about them.

## 9.8 FORMATTED INPUT: THE **scanf** FUNCTION

| | |
|---|---|
| Prototype: | `int scanf (cstring, &var1, &var2, ...);` |
| Header file: | `stdio.h` |
| Return value: | Number of items successfully matched or EOF if end of input is encountered before conversion of first item. |

**scanf** is the main member of a family of input functions that includes **fscanf** and **sscanf**. Unlike most functions, **scanf** uses a *variable* number of arguments. The first argument (*cstring*) is a *control string* containing one or more *format specifiers* (like `%d`). The remaining arguments (*&var1*, *&var2*, etc.) represent—not variables—but their *addresses*. The number of variable addresses must equal the number of format specifiers. Figure 9.2 shows a **scanf** statement used with three format specifiers and three variable addresses.

![](img/d75612dcf3ab36327142238ab5bb21d8_300_0.png)

**scanf** uses the information in the control string to divide the input into one or more *fields*. Thus, if the control string is “%c %d %f” and **scanf** encounters the string M 1986 37.4, it performs the following tasks:

- Saves the character M (`%c`) to the variable *gender* without performing any conversion.
- Converts the string 1986 to the integer 1986 (`%d`) and saves it in the variable *year*.
- Converts the four-character string 37.4 to the floating point value 37.4 (`%f`) and saves it in the variable *amount*.

If **scanf** encounters a mismatch between the type specified in the format specifier and that found in the data, it stops further processing. **scanf** then returns the number of items that were successfully read (if at all). The remaining characters, including the one that failed to match, are left in the buffer. The next invocation of **scanf** or any other input function will fetch these characters. It is often necessary to run **getchar** in a loop for clearing this “unclean” buffer.

> **Caution:** If you use x instead of &x as a **scanf** argument, **scanf** will interpret the current value of x as an address and will overwrite the contents of memory at that address. The behavior of the program then becomes unpredictable; it can even crash.

Program 9.5 runs **scanf** in a loop to accept a char, int and float value from standard input. **scanf** successfully matches the input in the first two loop iterations but fails in the next two. The buffer is cleared before the next iteration using a technique that was discussed in Section 8.4.2.

**scanf** can easily frustrate a user if its data-matching rules are not fully understood, so let’s examine each invocation separately:

Invocation 1—Matching is perfect.

Invocation 2—**scanf** successfully matches the integer 4096 with `%f`.

Invocation 3—**scanf** truncates 3.142 when matching it with `%d`. 3 is wrongly assigned to *i* and 0.142 to *f*.

```c
/* intro2scanf.c: Accepts a char, int and float.
     Shows how easy it is for scanf to fail. */
#include <stdio.h>
int main(void)
{
    char c; int i = 1; float f;
    while (i) {                 /* Loop terminates when i = 0 */
        printf("Enter a character, int and float: ");
        scanf("%c %d %f", &c, &i, &f);
        printf("You input %c, %d, %f\n", c, i, f);
        while (getchar() != '\n')    /* Clears the buffer */
            ;
    }
    return 0;
}
```

| PROGRAM 9.5: `intro2scanf.c` |
|---|
| Enter a character, int and float: **Y 12 3.142**<br>You input Y, 12, 3.142000 |
| Enter a character, int and float: **Y 15 4096**<br>You input Y, 15, 4096.000000 |
| Enter a character, int and float: **N 3.142 12.75**<br>You input N, 3, 0.142000 |
| Enter a character, int and float: **Yes 4096 15.75**<br>You input Y, 3, 0.142000 *(Prints previous values of i and f)* |
| Enter a character, int and float: **0 0 0**<br>You input 0, 0, 0.000000 |

PROGRAM OUTPUT: `intro2scanf.c`

Invocation 4—**scanf** assigns Y to c all right, but it is unable to match the remainder of the string (es) with %d. **scanf** thus returns after matching only one item and leaves the values in the variables i and f unchanged.

The inner **while** loop having a null body clears the buffer at the end of each iteration, so **scanf** always operates with an empty buffer. Why not comment these two lines and then run the program?

> **Takeaway:** **scanf** truncates a real number when matching it with %d even though it can match an integer with %f. Also, **scanf** can’t match multiple characters with %c.

## 9.9 `scanf`: THE MATCHING RULES

A number of rules determine the way `scanf` matches input values with format specifiers. Most of the rules also have exceptions. By default, `scanf` splits input on whitespace (space, tab and newline) even if the control string doesn’t contain whitespace. Before doing anything else, you must commit the following rule to memory:

> Whitespace in the control string matches zero or more leading whitespace characters in the input.

The emphasis here is on the word “leading.” This means that both `%d%d` and `%d %d` match the strings `12 45` and `12 45`. However, this rule doesn’t apply to `%c`, whose matching techniques are discussed in Section 9.10.2.

There are two more issues that impact matching. First, if the control string contains non-whitespace characters, the same characters must be present in the input. For instance, `%d:%d` matches `12:30:45` and `12: 30: 45` but not `12 :30 :45` because two values contain trailing whitespace.

Second, if a field width is specified (as in `%2d`), `scanf` tries to match two characters of the specified data type. Thus, `%2d%2d%2d` splits the string `311214` into the values 31, 12 and 14 and saves them in three `int` variables. That’s how one can extract the components of a date from a six-character string containing digit-characters.

**Tip:** For easier matching, provide whitespace on both sides of the non-whitespace character in the control string. Thus, `%d : %d` matches `12:34`, `12 :34`, `12: 34` as well as `12 : 34`. The same is true for `%c` and `%f`.

### 9.9.1 Mismatches and Return Value

`scanf` returns the number of items successfully matched and assigned to variables. For example, if the control string `%4d%c` successfully matches the input, `scanf` returns the value 3. If a mismatch occurs, `scanf` returns the number of items successfully matched until the occurrence of the mismatch. However, if EOF (the condition) occurs before the first item is matched, `scanf` returns EOF (the value—usually -1).

Mismatches can also occur for other reasons. If `scanf` finds a letter when a digit was expected, it returns the character to the buffer before the function itself returns to the caller. Wrong field width is also a possible cause of mismatch. When using `%4d` to match a six-digit number, `scanf` will only match the first four digits. Even if a subsequent call can read the remaining two digits, it would be reading the wrong item. Both of these situations are demonstrated in the following examples:

Control string: `%4d %d`

| Input String | Matches | Return Value | Remarks |
|---|---|---:|---|
| 1234 5678 | 1234 5678 | 2 | Nothing in buffer |
| 123456 789 | 1234 56 | 2 | 789 remains in buffer |
| 123r 5678 | 123 | 1 | r 5678 remains in buffer |
| r123 5678 | Nothing | 0 | Entire string remains in buffer |
