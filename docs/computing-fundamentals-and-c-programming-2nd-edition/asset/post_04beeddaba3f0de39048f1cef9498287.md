
```text
? New York
Strings are not equal
s1 = NewYork     length = 7 characters
s2 = York        length = 4 characters
s3 = NewYork     length = 7 characters
Enter two string constants
? London London
Strings are equal
s1 = London      length = 6 characters
s2 = London      length = 6 characters
s3 = London      length = 6 characters
```

**Fig. 10.10** *Illustration of string handling functions*

### WORKED-OUT PROBLEM 10.10

The program in Fig. 10.11 shows how to write a C program that reads a string and prints if it is a palindrome or not.

Program

```c
#include <stdio.h>
#include <conio.h>
#include <string.h>
void main()
{
char chk='t', str[30];
int len, left, right;
printf("\nEnter a string:");
scanf("%s", &str);
len=strlen(str);
left=0;
right=len-1;
while(left < right && chk=='t')
  {
  if(str[left] == str[right])
    ;
  else
  chk='f';
  left++;
  right--;
  }
if(chk=='t')
    printf("\nThe string %s is a palindrome",str);
else
    printf("\nThe string %s is not a palindrome",str);
getch();
}
```

Output

```text
    Enter a string: nitin
    The string nitin is a palindrome
```

**Fig. 10.11** *Program to check if a string is palindrome or not*

## Other String Functions

The header file **<string.h>** contains many more string manipulation functions. They might be useful in certain situations.

### strncpy

In addition to the function **strcpy** that copies one string to another, we have another function **strncpy** that copies only the left-most *n* characters of the source string to the target string variable. This is a three-parameter function and is invoked as follows:

```c
strncpy(s1, s2, 5);
```

This statement copies the first 5 characters of the source string **s2** into the target string **s1**. Since the first 5 characters may not include the terminating null character, we have to place it explicitly in the 6th position of **s1** as shown below:

```c
s1[6] = '\0';
```

Now, the string **s1** contains a proper string.

### strncmp

A variation of the function **strcmp** is the function **strncmp**. This function has three parameters as illustrated in the function call below:

```c
strncmp (s1, s2, n);
```

This compares the left-most *n* characters of **s1** to **s2** and returns:

- (a) 0 if they are equal;
- (b) negative number, if s1 sub-string is less than s2; and
- (c) positive number, otherwise.

### strncat

This is another concatenation function that takes three parameters as shown below:

```c
strncat (s1, s2, n);
```

This call will concatenate the left-most *n* characters of **s2** to the end of **s1**. Example:

![](img/11b034a94fc590add0a7808250a38792_373_0.png)

![](img/11b034a94fc590add0a7808250a38792_373_1.png)

After **strncat (s1, s2, 4);** execution:

![](img/11b034a94fc590add0a7808250a38792_373_2.png)

### strstr

It is a two-parameter function that can be used to locate a sub-string in a string. This takes the following forms:

```text
strstr (s1, s2);
strstr (s1, "ABC");
```

The function **strstr** searches the string **s1** to see whether the string **s2** is contained in **s1**. If yes, the function returns the position of the first occurrence of the sub-string. Otherwise, it returns a NULL pointer.

Example:

```c
if (strstr (s1, s2) == NULL)
    printf("substring is not found");
else
    printf("s2 is a substring of s1");
```

We also have functions to determine the existence of a character in a string. The function call

```c
strchr(s1, 'm');
```

will locate the first occurrence of the character 'm' and the call

```c
strrchr(s1, 'm');
```

will locate the last occurrence of the character 'm' in the string **s1**.

### Warning

- When allocating space for a string during declaration, remember to count the terminating null character.
- When creating an array to hold a copy of a string variable of unknown size, we can compute the size required using the expression
  ```c
  strlen(stringname) + 1
  ```
- When copying or concatenating one string to another, we must ensure that the target (destination) string has enough space to hold the incoming characters. Remember that no error message will be available even if this condition is not satisfied. The copying may overwrite the memory and the program may fail in an unpredictable way.
- When we use **strncpy** to copy a specific number of characters from a source string, we must ensure to append the null character to the target string, in case the number of characters is less than or equal to the source string.

## 10.9 TABLE OF STRINGS

LO 10.4

We often use lists of character strings, such as a list of the names of students in a class, list of the names of employees in an organization, list of places, etc. A list of names can be treated as a table of strings and a two-dimensional character array can be used to store the entire list. For example, a character array `student[30][15]` may be used to store a list of 30 names, each of length not more than 15 characters. Shown below is a table of five cities:

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|
| C | h | a | n | d | i | g | a | r | h |
| M | a | d | r | a | s |   |   |   |   |
| A | h | m | e | d | a | b | a | d |   |
| H | y | d | e | r | a | b | a | d |   |
| B | o | m | b | a | y |   |   |   |   |

This table can be conveniently stored in a character array `city` by using the following declaration:

```c
char city[5][11] =
{
    "Chandigarh",
    "Madras",
    "Ahmedabad",
    "Hyderabad",
    "Bombay"
};
```

To access the name of the ith city in the list, we write

```c
city[i-1]
```

and therefore, `city[0]` denotes “Chandigarh”, `city[1]` denotes “Madras” and so on. This shows that once an array is declared as two-dimensional, it can be used like a one-dimensional array in further manipulations. That is, the table can be treated as a column of strings.

### WORKED-OUT PROBLEM 10.11

H

Write a program that would sort a list of names in alphabetical order.

A program to sort the list of strings in alphabetical order is given in Fig. 10.12. It employs the method of bubble sorting described in Case Study 1 in Chapter 9.

Program

```c
#define ITEMS 5
#define MAXCHAR 20
main( )
{
    char string[ITEMS][MAXCHAR], dummy[MAXCHAR];
    int i = 0, j = 0;
/* Reading the list */
printf ("Enter names of %d items \n ",ITEMS);
while (i < ITEMS)
    scanf ("%s", string[i++]);
/* Sorting begins */
for (i=1; i < ITEMS; i++) /* Outer loop begins */
{
    for (j=1; j <= ITEMS-i ; j++) /*Inner loop begins*/
    {
        if (strcmp (string[j-1], string[j]) > 0)
        { /* Exchange of contents */
            strcpy (dummy, string[j-1]);
            strcpy (string[j-1], string[j]);
            strcpy (string[j], dummy );
        }
    } /* Inner loop ends */
} /* Outer loop ends */
/* Sorting completed */
printf ("\nAlphabetical list \n\n");
for (i=0; i < ITEMS ; i++)
    printf ("%s", string[i]);
}
```

Output

```text
Enter names of 5 items
London Manchester Delhi Paris Moscow
Alphabetical list
Delhi
London
Manchester
Moscow
Paris
```

**Fig. 10.12** Sorting of strings in alphabetical order

Note that a two-dimensional array is used to store the list of strings. Each string is read using a **scanf** function with **%s** format. Remember, if any string contains a white space, then the part of the string after the white space will be treated as another item in the list by the **scanf**. In such cases, we should read the entire line as a string using a suitable algorithm. For example, we can use **gets** function to read a line of text containing a series of words. We may also use **puts** function in place of **scanf** for output.
