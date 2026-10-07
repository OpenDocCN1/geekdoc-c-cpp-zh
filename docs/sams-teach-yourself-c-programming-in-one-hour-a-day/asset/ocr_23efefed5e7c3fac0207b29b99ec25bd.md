# The strbrk() Function

The library function strbrk() is similar to strcspn(), searching one string for the first occurrence of any character contained in another string. It differs that it doesn't include the terminating null characters in the search. The function prototype is

```
char *strbrk(const char *str1, const char *str2);
```

The function strbrk() returns a pointer to the first character in str1 that matches any of the characters in str2. If it doesn't find, the function returns NULL. As previously explained for the function strchr(), you can obtain the offset of the match in str1 by subtracting the pointer str1 from the pointer returned by strbrk() (if it isn't NULL, of course). replace strcspn() on line 20 of Listing 18.9 with strbrk().

# The strstr() Function

The final, and perhaps, most useful C string function is strstr(). This function searches for the first occurrence of one string within another, and it searches for the entire string, not just individual characters within that. Its prototype is

```
char *strstr(const char *str1, const char *str2);
```

The function strstr() returns a pointer to the first occurrence of str2 within str1. If it finds no match, the function returns NULL. If the length of str2 is 0, the function returns str1. When strstr() finds a match, you can obtain the offset of str2 within str1 by pointer subtraction, as explained earlier for strchr(). The matching procedure that strstr() is case-sensitive. Listing 18.11 demonstrates how to use strstr().

# Input ▼

LISTING 18.11 stringsearch4.c--Using strstr() to Search for One String Within Another

```
// stringsearch4.c--Searching with strstr().

#include <stdio.h>
#include <string.h>

int main(void )
{
    char *loc, buf1[80], buf2[80];

    // Input the strings.

    printf("Enter the string to be searched: ");
    gets(buf1);
    printf("Enter the target string: ");
```