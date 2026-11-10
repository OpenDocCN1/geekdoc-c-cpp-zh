
## Counting number of characters in a string

The first of these, strlen(), is particularly straightforward. Its single parameter is the address of the start of the string and its value is the number of characters in the string excluding the terminating NUL.

To demonstrate the use of strlen(), here is a simple program that reads in a string and prints it out reversed, a useful thing to do. The repeated operation of this program is terminated by the user by entering a string of length zero, i.e., by hitting the <Return> key immediately after the program prompt.

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char s[100];
    int len;    /* holds length of string */
    while(1)
    {
        printf("Enter a string");
        gets(s);
        len = strlen(s);    /* find length */
        if(len == 0) break; /* termination condition */
        while(len > 0)
        {
            len--;
            printf("%c",s[len]);
        }
        printf("\n");
    }
    return 0;
}
```

The program operates by printing the characters one by one, starting with the last non-NUL character of the string. Notice that 'len' will have been decremented before the output of the character. This is correct since the length returned by strlen() is the length excluding the NUL but the actual characters are aggregate members, 0, ..., length-1. The outputs of this program for different sample runs are

- (a) Enter a string 1234  
  4321
- (b) Enter a string manas  
  sanam
- (c) Enter a string abc def ghi  
  ihg fed cba

Look at the following program that reads a line of text, stores it in a string, and prints its length (excluding the new line at the end).

```c
#include <stdio.h>
int main()
{
    int n, c;
    char line[100];
    n = 0;
    while((c=getchar()) != '\n')
    {
        if(n < 100)
            line[n] = c;
        n++;
    }
    line[n]='\0';
    printf("length = %d\n", n);
    return 0;
}
```

Lastly, here is another version of strlen().

```c
int mystrlen(char str[])
{
    int i;
    for(i = 0; str[i] != '\0'; i++)
    {}
    return i;
}
```

In this case, all one has to do is find the \0 that terminates the string. It turns out that the three control expressions of the for loop do all the work; there is nothing left to do in the body. Therefore, an empty pair of braces {} are used as the loop body. Equivalently, a null statement could be used, which is simply a semicolon as shown.

```c
for(i = 0; str[i] != '\0'; i++);
```

Empty loop bodies can be a bit startling at first, but they are not unheard of.

## Copying a string into another

Since C never lets entire arrays to be assigned, the strcpy() function can be used to copy one string to another. strcpy() copies the string pointed to by the second parameter into the space pointed to by the first parameter. The entire string, including the terminating NUL, is copied and there is no check that the space indicated by the first parameter is big enough. The given code shows the use of the strcpy() function.

```c
#include <string.h>
int main()
{
    char s1[] = "Hello, world!";
    char s2[20];
    strcpy(s2, s1);
    puts(s2);
    return 0;
}
```

The destination string is strcpy()'s first argument, so that a call to strcpy mimics an assignment expression, with the destination on the left-hand side. Note that string s2 must be allocated sufficient memory so that it can hold the string that would be copied to it. Also, at the top of any source file, the following line must be included

```c
#include <string.h>
```

that contains external declarations for these functions.

Since a string is just an array of characters, all string-handling functions can be written quite simply, using no technique more complicated than the ones that are already known. In fact, it is quite instructive to look at how these functions might be implemented. Here is a version of `strcpy`.

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char src[30], dest[30];
    int i = 0;
    printf("\n Enter the source string: ");
    scanf("%[^\n]", src);
    while(src[i] != '\0')
    {
        dest[i] = src[i];
        i++;
    }
    dest[i] = '\0';
    printf("\n Source string is : %s\n", src);
    printf("\n Destination string is : %s\n", dest);
    return 0;
}
```

Its operation is simple. It looks at characters in the `src` string one at a time, and as long as they are not `\0`, assigns them, one by one, to the corresponding positions in the `dest` string. On completion, it terminates the `dest` string by placing a `\0`. After exiting the while loop, `i` is guaranteed to have a value one greater than the subscript of the last character in `src`. For comparison, here is a way of writing the same code, using a for loop instead of while loop.

```c
for(i = 0; src[i] != '\0'; i++)
    dest[i] = src[i];
dest[i] = '\0';
```

The above statements can be rewritten using the following expression:

`for(i=0;(dest[i] = src[i]) != '\0';i++);`

This is actually the same type of combined operation.

## Comparing strings

Another function, `strcmp()`, takes the start addresses of two strings as parameters and returns the value zero if the strings are equal. If the strings are unequal, it returns a negative or positive value. The returned value is positive if the first string is greater than the second string and negative if the first string is lesser than the second string. In this context, the relative value of strings refers to their relative values as determined by the host computer character set (or collating sequence).

It is important to realize that two strings cannot be compared by simply comparing their start addresses although this would be syntactically valid. The following program illustrates the comparison of two strings:

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char x[50], y[] = "a programming example";
    strcpy(x, "A Programming Example");
    if(strcmp(x, "A Programming Example") == 0)
        printf("Equal \n");
    else
        printf("Unequal \n");
    if(strcmp(y, x) == 0)
        printf("Equal \n");
    else
        printf("Unequal \n");
    return 0;
}
```

It produces the following output:

```
Equal
Unequal
```

## Putting strings together

Arithmetic addition cannot be applied for joining of two or more strings in the manner

```
string1 = string2 + string3; or
string1 = string2 + "RAJA";
```

For this, the standard library function, `strcat()`, that concatenates strings is needed. It does not concatenate two strings together and give a third, new string. What it really does is append one string at the end of another. Here is an example.

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char s[30] = "Hello,";
    char str[] = "world!";
    printf("%s\n", s);
    strcat(s, str);
    printf("%s\n", s);
    return 0;
}
```

The first call to `printf` prints “Hello,”, and the second one prints “Hello,world!”, indicating that the contents of `str` have been appended to the end of `s`. Notice that `s` was declared with extra space, to make room for the appended characters.

Note that in arithmetic, `char` variables can usually be treated like `int` variables. Arithmetic on characters is quite legal, and often makes sense.

```
c = c + 'A' - 'a';
```

converts a single, lower-case ASCII character stored in `c` to a capital letter, making use of the fact that corresponding ASCII letters are a fixed distance apart. The rule governing this arithmetic is that all `char`s are converted to `int` before the arithmetic is done. Be aware that conversion may involve a sign-extension; if the leftmost bit of a character is 1, the resulting integer might be negative.

Therefore, to convert a text into lower case, the following program can be used:

```c
#include <stdio.h>
int main()
{
    char c;
    while((c=getchar()) != '\n')
    if('A'<=c && c<='Z')
        putchar(c+'a'-'A');
        /* equivalent statement in putchar(c+32);*/
    else
        putchar(c);
    return 0;
}
```

Sample run:

```
TIMES OF INDIA
times of india
```

The following program will demonstrate the strncat() library function:

```c
#include <string.h>
#include <stdio.h>
int main()
{
    char aString1[80] = "RCC Institute of Information Technology",
    aString2[80] = "Oxford University Press";
    printf("\n Before the copy...\n");
    puts(aString1);
    puts(aString2);
    strncat(aString1, aString2, 6);
    printf("\nAfter the copy...\n");
    puts(aString1);
    puts(aString2);
    return 0;
}
```

**Output**

```
Before the copy...
RCC Institute of Information Technology
Oxford University Press
After the copy...
RCC Institute of Information Technology Oxford
Oxford University Press
```

**Note**

- Since C never lets entire arrays to be assigned, the strcpy() function can be used to copy one string to another.
- Strings can be compared with the help of strcmp() function.
- The arithmetic addition cannot be applied for joining two or more strings; this can be done by using the standard library function, strcat().

## Some sample programs

*One interesting thing: This program tries to prove that a string is really an array of characters. Note the explicit placement of the string terminator at the end of the string. Note the term &str[2]. Remember that str[2] is the third character, so &str[2] is the address of the third character. Since str is the address of the first character, &str[2] effectively is str but with the first two characters removed. Try replacing &str[2] with str+2. Does this work? Lastly, notice the use of the strcpy (string copy) function from the string.h library.*

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char str[30];
    str[0]='M';
    str[1]='A';
    str[2]='D';
    str[3]='A';
    str[4]='M';
    str[5]='\0'; /* terminate string with a null */
    printf("String is %s\n",str);
    printf("Part of string is %s\n",&str[2]);
    strcpy(str,"SIR");
    printf("String is %s\n",str);
    return(0);
}
```

Sample run:

```
String is MADAM
Part of string is DAM
String is SIR
```

To make sure that what is going on is understood, consider the following table:

| Code | Output |
|---|---|
| `printf("%s?", str);` | MADAM |
| `printf("%s?", str[1]);` | Error |
| `printf("%s?", &str[1]);` | ADAM |
| `printf("%s?", &str);` | MADAM |

Some of the following programs will illustrate the manipulation of strings. The following program toggles the case of every character in the input string.

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char istr[128]; /* input buffer */
    char tstr[128]; /* translated string here */
    int i;
    int slen; /* string length */
    while(1)
    {
```
