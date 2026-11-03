from Section 4.7 that an integer is returned to support the end-of-file indicator. As you know, function puts takes a string as an argument and displays the string followed by a newline character. The program stops inputting characters either when 79 characters have been read or when getchar reads the newline character entered by the user to end the line of text. A null character is appended to array sentence (line 20) so that the array may be treated as a string. Then line 24 uses puts to display the string contained in sentence.

```
// Fig. 8.11: fig08_11.c
// Using function getchar.
#include <stdio.h>
#define SIZE 80

int main(void)
{
    int c; // variable to hold character input by user
    char sentence[SIZE]; // create char array
    int i = 0; // initialize counter i

    // prompt user to enter line of text
    puts("Enter a line of text:");

    // use getchar to read each character
    while ((i < SIZE - 1) && ((c = getchar()) != '\n')) {
        sentence[i++] = c;
    }

    sentence[i] = '\0'; // terminate string

    // use puts to display sentence
    puts("\nThe line entered was:");
    puts(sentence);
}
```

Enter a line of text:
This is a test.

The line entered was:
This is a test.

Fig. 8.11 | Using function getchar.

# 8.5.3 Function sprintf

Figure 8.12 uses function sprintf to print formatted data into array s—an array of characters. The function uses the same conversion specifiers as printf (see Chapter 9 for a detailed discussion of formatting). The program inputs an int value and a double value to be formatted and printed to array s. Array s is the first argument of sprintf. [Note: If your system supports C11's snprintf_s, then use that in preference to sprintf. If your system doesn't support snprintf_s but does support snprintf, then use that in preference to sprintf.]