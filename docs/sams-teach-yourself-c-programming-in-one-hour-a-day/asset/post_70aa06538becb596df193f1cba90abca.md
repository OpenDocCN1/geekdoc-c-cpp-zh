
string. You must allocate enough space for str to hold the resulting string. The function returns a pointer to str. Listing 18.5 uses strcat() to produce the same output as Listing 18.4.

## Input
LISTING 18.5 stringcat2.c: Using the strcat() Function to Concatenate Strings

```c
1: // stringcat2.c--The strcat() function.
2:
3: #include <stdio.h>
4: #include <string.h>
5:
6: char str2[] = "abcdefghijklmnopqrstuvwxyz";
7:
8: int main(void )
9: {
10:    char str[27];
11:    int n;
12:
13:    for (n=1; n< 27; n++)
14:    {
15:        strcpy(str, "");
16:        strcat(str, str2, n);
17:        puts(str);
18:    }
19:
20:    return 0;
21: }
```

## Output

a
ab
abc
abcd
abcde
ababcdef
ababcdefg
ababcdefgh
ababcdefghi
ababcdefghij
ababcdefghijk
ababcdefghijkl
ababcdefghijklij
ababcdefghijklm
ababcdefghijklklmn
ababcdefghijklmno
ababcdefghijklmnop
ababcdefghijklklmnopq
ababcdefghijklmmnopqr
abcdefghijklmnopqr
ababcdefghijklmnopqrt
ababcdefghijklmnopstu
ababcdefghijklmnopqrstuv
ababcdefghijklmnopqrstuvw
ababcdefghijklmnopqrstuvwx
ababcdefghijklmnopqrstxy
ababcdefghijklmnopqrstuvwxyz

## LESSON 18 Manipulating Strings

### Analysis

You might wonder about the purpose of line 15, `strcpy(str1, "");`. This line copies an empty string consisting of only a single null character. The result is that character in `str1`—`str1[0]`—is set to 0 (the null character). The same thing could have been accomplished with the statements `str1[0] = 0;` `str1[0] = '\0';`

### Comparing Strings

Strings are compared to determine whether they are equal or unequal. If they are unequal, one string is "greater than" or "less than the other". Determinations of "greater" and "less" are made with the ASCII codes of the characters. For letters, this is equivalent to alphabetical order, with the one seemingly strange exception that all uppercase letters are "less than" the lowercase a–z are represented by 97–122. Thus, "ZEBRA" would be considered to be less than "apple" evaluating by these C functions.
The ANSI C library contains functions for two types of string comparisons: comparing two strings and comparing a certain number of characters in two strings.

### Comparing Two Entire Strings

The function `strcmp` compares two strings, by character. Its prototype is `int strcmp(const char *str1, const char *str2);`
The arguments `str1` and `str2` are pointers to the strings being compared. The function's return values are given in Table 18.1. You should notice that both strings are passed as constants because neither is changed. Listing 18.6 demonstrates `strcmp()`.

TABLE 18.1 The Values Returned by `strcmp()`

| Return Value | Meaning |
|---|---|
| < 0 | str1 is less than str2. |
| 0 | str1 is equal to str2. |
| > 0 | str1 is greater than str2. |

### Comparing Strings

LISTING 18.6 stringcompare.c: Using strcmp() to Compare Strings

```c
1: // stringcompare.c--The strcmp() function.
2:
3: #include <stdio.h>
4: #include <string.h>
5:
6: int main(void )
7: {
8:     char str1[80], str2[80];
9:     int x;
10:    while (1)
11:    {
12:
13:        /* Input two strings. */
14:
15:        printf("\nInput the first string, a blank to exit: %s");
16:        gets(str1);
17:
18:
19:        if ( strlen(str1) == 0 )
20:            break;
21:
22:        printf("\nInput the second string: %s");
23:        gets(str2);
24:
25:        /* Compare them and display the result. */
26:
27:        x = strcmp(str1, str2);
28:
29:        printf("\nstrcmp(%s,%s) returns %d", str1, str2, x);
30:    }
31:    return(0);
32: }
```

## Output

Input the first string, a blank to exit: **First string**

Input the second string: **Second string**

strcmp(First string,Second string) returns -1

Input the first string, a blank to exit: **test string**

Input the second string: **test string**

strcmp(test string,test string) returns 0

Input the first string, a blank to exit: zebra

Input the second string: aardark

strcmp(zebra,aardark) returns 1

Input the first string, a blank to exit:

### NOTE
Some UNIX systems, string comparison functions’t necessarily return -1 when the strings aren’t the same. They do, however, always return a nonzero value for unequal strings. The ANSI Standard states that only the return value is less than, equal to, or greater than zero.

### Analysis
This program demonstrates strcmp(), prompting the user for two strings (lines 16, 17, 22), and displays the result returned by strcmp() on line 29. Experiment with this program to get a feel how strcmp() compares strings. Try entering two strings that are identical for case, such as Smith and SMITH. You learn that strcmp() is case-sensitive, meaning that the program considers uppercase and lowercase letters to be different.

### Partial Strings

The library function strncmp() compares a number of characters of one string to another. Its prototype is

```c
int strncmp(const char *str1, const char *str2, size_t n);
```

The function strncmp() compares n characters of str2 to str1. The comparison proceeds until n characters have been compared or the end of str1 has been reached. The method of comparison and return values are the same as strcmp(). The comparison is case-sensitive. Listing 18 demonstrates strncmp().

## Input
LISTING 18.7 stringcompare2.c: Comparing Parts of Strings with strncmp()

```c
1: // stringcompare2.c--The strncmp() function.
2:
3: #include <stdio.h>
4: #include <string.h>
5:
6: char str[] = "The first string.";
7: char str2[] = "The second string.";
8:
9: int main(void )
10: {
11:     size_t n, x;
12:
13:     puts(str);
14:     puts(str2);
15:
16:     while (1)
17:     {
18:         puts("Enter number of characters to compare, 0 to exit.");
19:         scanf("%d", &n);
20:
21:         if (n <= 0)
22:             break;
23:
24:             x = strncmp(str, str2, n);
25:
26:             printf("Comparing %d characters, strcmp() returns %d.", n, x);
27:     }
28:     return(0);
29: }
```

## Output

The first string.
The second string.

Enter number of characters to compare, 0 to exit.
Comparing 3 characters, strcmp() returns 0.

Enter number of characters to compare, 0 to exit.
Comparing 6 characters, strcmp() returns -1.

Enter number of characters to compare, 0 to exit.

### Analysis
This program compares two strings defined on lines 6 and 7. Lines 13 and 14 print the strings to the screen that the user can see what they are. The program executes while loop on lines 16-27 so that multiple compares can be done. If the user asks to compare zero characters on lines 18 and 19, the program breaks on line 22; otherwise, the strncmp executes on line 24, and the result is printed on line 26.

### Searching Strings
The C library contains a number of functions that search strings. To put it another way, these functions determine whether one string occurs within another, and so you can choose from string searching functions, all of which require the header file string.h:

- strchr()
- strcspn()
- strspn()
- strpbrk()
- strstr()

### The strchr() Function

The strchr() function finds the first occurrence of a specified character in a string. The prototype is

```c
char *strchr(const char *str, int ch);
```

The function strchr() searches string from left to right until the character ch is found or the terminating null character is found. If ch is found, a pointer to it is returned. If not, NULL is returned.

When strchr() finds the character, it returns a pointer to that. Knowing that str is a pointer to the first character in the string, you can obtain the position of the found character by subtracting str from the pointer returned by strchr(). Listing the first character in a string is at position 0. Like many of C's string functions, strchr() is case-sensitive and, therefore, reports that the character "F" isn't found in the string "raffle".

## Input
LISTING 18.8 stringchar1.c: Using strchr() to Search a String for a Single Character

```c
1: // stringchar1.c--Searching for a single character with strchr()
2:
3:   #include <stdio.h>
4:   #include <string.h>
5:
6:   int main(void )
7:   {
8:       char *loc, buf[80];
9:       int ch;
10:
11:      // Input the string and the character.
12:
13:      printf("Enter the string to be searched: ");
14:      gets(buf);
15:      printf("Enter the character to search for: ");
16:      ch = getchar();
17:
18:      // Perform the search.
19:
20:      loc = strchr(buf, ch);
21:
22:      if ( loc == NULL )
23:          printf("The character %c was not found.", ch);
24:      else
25:          printf("The character %c was found at position %d.\n",
26:              ch, loc-buf);
27:      return(0);
28: }
```

## Output

Enter the string to be searched: How now Brown Cow.
Enter the character to search for: C
The character C was found at position 14.

### Analysis
This program uses strchr() on line 20 to search for a character within a string. strchr() returns a pointer to the location where the character is first found or NULL if the character isn’t found. Line 22 checks whether the value of loc is NULL and prints an appropriate message. As described in the section “strchr() Function,” the position of the character within the string is determined by subtracting the string pointer from the value returned by the function.
