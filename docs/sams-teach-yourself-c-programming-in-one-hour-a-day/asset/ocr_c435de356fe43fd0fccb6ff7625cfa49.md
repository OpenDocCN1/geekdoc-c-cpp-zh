# Accepting Keyboard Input

# LISTING 14.4 getch.c: Using the getch() Function

```
1: /* Demonstrates the getch() function. */
2: /* Non-ANSI code */
3: #include <stdio.h>
4: #include <conio.h>
5:
6: int main( void )
7: {
8:     int ch;
9:
10:    while ((ch = getch()) != '\r')
11:        putchar(ch);
12:
13:    return 0;
14: }
```

# Output

Testing the getch() function

# Analysis

When this program runs, getch() returns each character as soon as you press a key—it doesn’t wait for you to press Enter. There’s the only reason that each character displays onscreen is the call to putchar(ch). To get a better understanding of how getch() works, add a semicolon to the end of line 10 and remove line 11 (putchar(ch)). When you rerun the program, you will see that nothing is echoed to the screen. The getch() function gets the characters without echoing them to the screen. You know the characters are received because the original listing using putchar() to display them.

Listing 14.5 uses getch() to input an entire line of text. Running this program clearly illustrates that getch() doesn’t echo its input. With the exception of substituting getch() with getchar(), this program is virtually identical to Listing 14.3.