```
```c
char str1[] = "abc";
char str2[] = "efg";

str2[4] = 'w';
printf("%c\n", str1[0]);
return 0;
}
```
```

Answer: When str1 is declared, the compiler creates an array of four places, to store the 'a', 'b', 'c', and '\0' characters. Similarly, it creates the str2 array with four places, to store the 'e', 'f', 'g', and '\0' characters. The attempt to store the 'w' character in a position that exceeds the length of str2 is wrong. In particular, the assignment str2[4] = 'w' overwrites the data out of str2, which causes unpredictable behavior. For example, the program may display a, but it may also display w if str1 is stored right after str2 in memory.

# Writing Strings

The most common functions used to write strings are printf() and puts(). In a simple form, printf() uses the %s format and a pointer to the string. For example, the following program uses the name of the array as a pointer to the first character of the string.

```
```c
#include <stdio.h>
int main(void)
{
    char str[] = "This is text";
    printf("%s\n", str);
    return 0;
}
```
```

printf() displays the characters of the string beginning, from the character that the pointer points to until it encounters the null character. Therefore, the program outputs: This is text. If printf() does not encounter the null character, it continues past the end of the string until it finds a null character somewhere in the memory. Recall from Chapter 2 that if we want to output a specific number of characters, we write %.ns, where n specifies that number. To display a part of the string, we make the pointer point to the proper position. For example, to display the part beginning from the sixth character, that is, is text, we write printf("%s\n", str+5); or equivalently, printf("%s\n", &str[5]); If we want to split the string inside printf() in more than one lines, we use the \ character. Notice that the string will be displayed in the same line. For example:

```
```c
printf("This text is displayed \
in the same line\n");
```
```

Alternatively, because C allows the merging of two or more adjacent literal strings into a single string, we can write: