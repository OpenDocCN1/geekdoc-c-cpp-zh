WZXGNUVCL
ADSN
Output of strings:
AXBCLNMT
PRSTLM
GGBGCHTN K
WZXGNUVCL
ADSN

The array strname is two-dimensional, therefore each row can be used to store a string. Only the row index is needed to identify a string. For instance, strname[0] is the first string, strname[1] is the second string, and so forth.

In these codes using the array index, the input character strings contain nine characters and a line character. The nine characters are stored in locations zero through eight and the new line character '\n' is stored in the tenth location. The reason for this is that when the scanf() function is used for string input, the entire string and the new line character must be read, the results are unpredictable. The input statement "%10c" is used to read the strings, all of which must be nine characters followed by a new line. A terminator is written to replace the new line so that they are recognizable as strings. In Section 9.7, a sample program is coded and executed to show the application of such smooth arrays. Strings of unequal length can also be stored in a smooth array. However, each string must then be scanned to replace the new line character '\n' with the string terminator '\\0'.

# 9.2.3 Input/Output of Character Strings

Character strings may be input and output using the scanf() and printf() function with a "%s" string field. The following example shows this.

```
#include <stdio.h>
int main ()
{
    char strname[15];
    printf("Enter the string:\n");
    scanf("%s", strname);
    printf("\ntThe string entered is: %s\n", strname);
    return 0;
}
```