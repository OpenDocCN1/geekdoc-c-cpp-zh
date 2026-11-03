Code three consecutive getchar() functions to read the characters. Format the result like this:

The three characters are 'a', 'b', and 'c'

where these characters — a, b, and c — would be replaced by the program’s input.

![](bbox=[0.02, 0.04, 0.07, 0.12])

The program you create in Exercise 7-4 waits for three characters. The Enter key is a character, so if you type A, Enter, B, Enter, the three characters are A, the Enter key character, and then B. This input is valid, but what you probably want to type is something like ABC or PIE or LOL and then press the Enter key.

![](bbox=[0.02, 0.27, 0.07, 0.12])

Standard input is stream-oriented. As I mention earlier in this chapter, don't expect your C programs to be interactive. Exercise 7-4 is an example of how stream input works; the Enter key doesn’t end stream input; it merely rides along in the stream, like any other character.

# Using the putchar() function

The output counterpart to getchar() is the putchar() function. It’s also prototyped in the stdio.h header file. The function serves the purpose of sending a single character to standard output. Here’s the format:

```
int putchar(int c);
```

The function’s single argument is an integer value, in the preceding line of code. The argument can be a variable or a literal character, as in

```
putchar('v');
```

The function returns the integer value of the character output, though this value need not be checked for simple character output, as shown in Listing 7-2.

# Putting putchar() to Work

```
#include <stdio.h>

int main()
{
    int ch;
    putchar('A');
    putchar('B');
    putchar('C');
    putchar('\n');
    return 0;
}
```