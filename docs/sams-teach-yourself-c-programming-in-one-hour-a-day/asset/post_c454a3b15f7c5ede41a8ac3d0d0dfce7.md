
# The rstrchr() Function

The library function rstrchr() is identical to strchr(), except that it searches a string for the last occurrence of a specified character in a string. Its prototype
`char *rstrchr(const char *str, int ch);`

The function rstrchr() returns a pointer to the last occurrence of ch in str and NULL if it finds no match. See how this function works, modify line 20 in Listing 18.8 to use rstrchr() instead of strchr().

# The strspn() Function

The library function strspn() searches one string for the first occurrence of any of the characters in a second string. Its prototype
`size_t strspn(const char *str1, const char *str2);`

The function strspn() starts searching at the first character of str1, looking for any of the individual characters in str2. This is important to remember. The function doesn't look for the specified character in str2, but only the characters it contains. If the function finds a match, it returns the offset from the beginning of str1 where the matching character is located. If it finds no match, strspn() returns the value of strlen(str1). This indicates that the first match was the null character terminating the string. Listing 18.9 shows you how to use strspn().

# Input

> LISTING 18.9 stringsearch2c: Searching for a Set of Characters with strspn()

```c
1: // stringsearch2c.-Searching with strspn()
2:
3: #include <stdio.h>
4: #include <string.h>
5:
6: int main(void )
7: {
8:     char buf1[80], buf2[80];
9:     size_t loc;
10:
11:     // Input the strings.
12:
13:     printf("Enter the string to be searched: ");
14:     gets(buf1);
15:     printf("Enter the string containing target characters: ");
16:     gets(buf2);
17:
18:     // Perform the search.
19: 
20:   loc = strcspn(buf1, buf2);
21:
22:   if ( loc == strlen(buf1) )
23:       printf("No match was found.");
24:   else
25:       printf("The first match was found at position %lu.\n", loc);
26:       return(0);
27: { }
```

# Output

Enter the string to be searched: How now Brown Cow?
Enter the string containing target characters: Cat
The first match was found at position 14.

# Analysis

This listing is similar to Listing 18. Instead of searching for the first occurrence of a single character, it searches for the first occurrence of any of the characters entered in the second string. The program calls strcspn() on line 20 with buf1 and buf2. If any of the characters in buf2 are in buf1, strcspn() returns the offset from the beginning of buf1 to the location of the first occurrence. Line 22 checks the return value to determine whether it is NULL. If the value is NULL, no characters were found, and an appropriate message displays on line 23. If a value is found, a message displays stating the character's position in the string.

# The strcspn() Function

This function is related to the previous one, strspn(), as the following paragraph explains. Its prototype is

```c
size_t strcspn(const char *str1, const char *str2);
```

The function strcspn() searches str1, character by character with the characters contained in str2. It returns the position of the first character in str1 that doesn't match a character in str2. In other words, strcspn() returns the length of the initial segment of str1 that consists entirely of characters found in str2. The return is 0 if no characters match. Listing 18 demonstrates strcspn().

# Input

LISTING 18.10 stringsearch3.c: Searching for the First Nonmatching Character with strspn()

```c
1: /* Searching with columnspan(). */
2:
3: #include <stdio.h>
4: #include <string.h>
5:
6: int main( void )
7: {
8:     char buf1[80], buf2[80];
9:     size_t loc;
10:
11:     /* Input the strings. */
12:
13:     printf("Enter the string to be searched: ");
14:     gets(buf1);
15:     printf("Enter the string containing target characters: ");
16:     gets(buf2);
17:
18:     /* Perform the search. */
19:
20:     loc = strcspn(buf1, buf2);
21:
22:     if ( loc == 0)
23:         printf("No match was found.\n");
24:
25:     else
26:         printf("Characters match up to position %d.\n", loc-1);
27: }
```

# Output

Enter the string to be searched: How now Brown Cow?
Enter the string containing target characters: How now what?
Characters match up to position 7.

# Analysis

This program is similar to the previous example, except that it calls columnspan() instead of strcspn() on line 20. The function returns the offset into buf1 where the first character that is not in buf2 is found. Lines 22–25 evaluate the return value and print an appropriate message.

# The strbrk() Function

The library function strbrk() is similar to strcspn(), searching one string for the first occurrence of any character contained in another string. It differs that it doesn't include the terminating null characters in the search. The function prototype is

```c
char *strbrk(const char *str1, const char *str2);
```

The function strbrk() returns a pointer to the first character in str1 that matches any of the characters in str2. If it doesn't find, the function returns NULL. As previously explained for the function strchr(), you can obtain the offset of the match in str1 by subtracting the pointer str1 from the pointer returned by strbrk() (if it isn't NULL, of course). replace strcspn() on line 20 of Listing 18.

# The strstr() Function

The final, and perhaps, most useful C string function is strstr(). This function searches for the first occurrence of a string within another. Its prototype is

```c
char *strstr(const char *str1, const char *str2);
```

The function strstr() returns a pointer to the first occurrence of str2 in str1. If it doesn't find, the function returns NULL. As previously explained for the function strchr(), you can obtain the offset of the match in str1 by subtracting the pointer str1 from the pointer returned by strstr() (if it isn't NULL, of course). Listing 18.11 demonstrates how to use strstr().

# Input

LISTING 18.11 stringsearch4.c: Using strstr() to Search for One String Within Another

```c
// stringsearch4.c--Using strstr().

#include <stdio.h>
#include <string.h>

int main(void )
{
    char *loc, buf1[80], buf2[80];

    // Input the strings.

    printf("Enter the string to be searched: ");
    gets(buf1);
    printf("Enter the target string: ");
    gets(buf2);

    // Perform the search.
    loc = strstr(buf1, buf2);

    if ( loc == NULL )
        printf("match was found.\n");
    else
        printf("%s was found at position %d.\n", buf2, loc-buf1);

    return(0);
}
```

# Output

Enter the string to be searched: How now brown cow?
Enter the target string: cow
cow was found at position 14.

# Analysis

This program is similar to the previous example, except that it calls strstr() instead of strcspn(). The function returns the offset into buf1 where the first occurrence of buf2 is found. Lines 21–24 evaluate the return value and print an appropriate message.
