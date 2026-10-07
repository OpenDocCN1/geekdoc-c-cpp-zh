# Input ▼

# LISTING 13.2** contin:c--Demonstrates the continue Statement

```
1: // contin.c--Demonstrates the continue statement.\n2:
3: #include <stdio.h>
4:
5: int main(void )
6: {
7:     // Declare a buffer for input and a counter variable.
8:
9:     char buffer[81];
10:    int ctr;
11:
12:    // Input a line of text.
13:    puts("Enter a line of text:");
14:    gets(buffer);
15:
16:    // Go through the string, displaying only those
17:    characters that are not lowercase vowels.
18:
19:    for (ctr = 0; buffer[ctr] != '\0'; ctr++)
20:    {
21:        // If the character is a lowercase vowel, loop back
22:        // without displaying it.
23:
24:        if (buffer[ctr] == 'a' || buffer[ctr] == 'e'
25:            || buffer[ctr] == 'i' || buffer[ctr] == 'o'
26:            || buffer[ctr] == 'u')
27:            continue;
28:
29:        // If not a vowel, display it.
30:        putchar(buffer[ctr]);
31:    }
32:    return 0;
33: }
```

# Output ▼

Enter a line of text:

**This is a line of text**

This s ln f txt