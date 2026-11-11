# # BRIEF CASES

# ## 1. Counting Words in a Text [LO 10.1, 10.2 M]

One of the practical applications of string manipulations is counting the words in a text. We assume that a word is a sequence of any characters, except escape characters and blanks, and that two words are separated by one blank character. The algorithm for counting words is as follows:

+   1. Read a line of text.
+   2. Beginning from the first character in the line, look for a blank. If a blank is found, increment words by 1.
+   3. Continue steps 1 and 2 until the last line is completed.

The implementation of this algorithm is shown in Fig. 10.13. The first **while** loop will be executed once for each line of text. The end of text is indicated by pressing the 'Return' key an extra time after the entire text has been entered. The extra 'Return' key causes a newline character as input to the last line and as a result, the last line contains only the null character.

The program checks for this special line using the test

    if ( line[0] == '\0' )

and if the first (and only the first) character in the line is a null character, then counting is terminated. Note the difference between a null character and a blank character.

```
Program

```c
#include <stdio.h>
main()
{
    char line[81], ctr;
    int i, c,
        end = 0,
        characters = 0,
        words = 0,
        lines = 0;
    printf("KEY IN THE TEXT.\n");
    printf("GIVE ONE SPACE AFTER EACH WORD.\n");
    printf("WHEN COMPLETED, PRESS 'RETURN'.\n\n");
    while( end == 0)
    {
        /* Reading a line of text */
        c = 0;
        while((ctr=getchar()) != '\n')
            line[c++] = ctr;
        line[c] = '\0';
        /* counting the words in a line */
        if(line[0] == '\0')
            break ;
```
```