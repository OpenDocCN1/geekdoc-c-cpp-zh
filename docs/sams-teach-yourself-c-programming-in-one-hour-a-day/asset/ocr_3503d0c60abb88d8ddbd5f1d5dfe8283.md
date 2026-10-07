# LESSON 14 Working with the Screen, Printer, and Keyboard

# Character Input

Character input functions read input from a stream one character at a time. When called, each of these functions returns the next character in the stream, or EOF if the end of the file has been reached or an error has occurred. EOF is a symbolic constant defined in stdin.h as -1. Character input functions differ in terms of buffering and echoing:

+   - Character input functions are buffered. This means the operating system holds all characters in a temporary storage space until you press Enter, and the system sends the characters to stdin stream. Others are unbuffered, meaning each character is sent to stdin as the key is pressed.

+   - Some input functions automatically echo each to stdout as it is received. Others don't echo; the character is sent to stdin and not stdout. Because stdout is assigned to the screen, where input is echoed.

The use of buffered, unbuffered, echoing, and nonechoing character input are explained in the following sections.

# The getchar() Function

The function getchar() obtains the next character from the stream stdin. It provides buffered input with echo, and its prototype is

```
int getchar(void);
```

The use of getchar() is demonstrated in Listing 14.2. Notice that the putchar() function, explained in detail later in the lesson, simply displays a single character onscreen.

# Input

LISTING 14.2 getchar.c: The getchar() Function

```
// // getchar.c--Demonstrates the getchar() function.
2:
3: #include <stdio.h>
4:
5: int main(void )
6: {
7:
    int ch;
8:
9:    while ((ch = getchar()) != '\n')
10:   putchar(ch);
11:
12:   return 0;
13: }
```