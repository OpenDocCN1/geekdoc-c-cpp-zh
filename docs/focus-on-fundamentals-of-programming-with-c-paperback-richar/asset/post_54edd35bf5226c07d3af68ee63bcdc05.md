
The string.h library contains a variety of functions to manipulate strings. To use any of the functions, we must add the following declaration to our program:

```
#include <string.h>
```

We'll look closely at four string functions that appear in the string.h library, strlen(), strcpy(), strcat(), strcmp(). We'll write our own code for each of these string functions as well.

- strlen(s1)

Tells us the length of a string. It returns the number of characters in a string, not counting the null-terminating character.

Function prototype:
int strlen(char *s1);

For example:

```
strlen("Computer");
```

returns the value 8 and not 9.

We can actually write a simple function to calculate our own string lengths. Note that we use the location of the null character in the string to help us determine the end of the string:

```
// strlen1.c
int strlen(char s1[]) {
    int i = 0;
    while (s1[i] != '\0') {
        ++i;
    }
    return i;
}
```

The formal parameter s1 is not really a character array, but a variable that holds the address of the initial element of the array. This is called a character pointer, and the function could have been declared as:

```
int strlen(char *s1)
```

When strlen() runs through its loop, it will look successively at s1[0], s1[1], etc. Since s1 contains the initial address of the array, C understands that s1[0] means the character at that address.

- strcpy(s1, s2) Copies string s2 to string s1, stopping after the terminating null character has been moved.

Function prototype:
void strcpy(char *s1, char *s2);

For example:

```
strcpy(s, "Computer");
```

copies the string "Computer" into string variable s.

Again, we can write our own strcpy() function and we can use the location of the null character in the string to help us determine the end of the string:

```
// strcpy1.c
void strcpy(char s1[], char s2[]) {
    int i = 0;
    while (s2[i] != '\0') {
        s1[i] = s2[i];
        ++i;
    }
    s1[i] = '\0';
}
```

We can write this more concisely:

```
// strcpy.c

void strcpy(char s1[], char s2[]) {
    int i = 0;

    while ((s1[i] = s2[i]) != '\0') {
        ++i;
    }
}
```

- strcat(s1, s2) Copies string s2 onto the end of string s1.

Function prototype:
void strcat(char *s1, char *s2);

For example:

```
char buf[32] = "Hello,";
strcat(buf, " world.");
printf("%s\n", buf);
```

outputs the string:

```
Hello, world.
```

Once again, we can write our own code to perform a string concatenation:

```
// strcat1.c

void strcat(char s1[], char s2[]) {
    int i = 0, j = 0;

    while (s1[i] != '\0') {
        ++i;
    }
    while (s2[j] != '\0') {
        s1[i] = s2[j];
        ++i;
        ++j;
    }
    s1[i] = '\0';
}
```

We can simplify the code:

```
// strcat2.c

void strcat(char s1[], char s2[]) {
    int i = 0, j = 0;

    while (s1[i]) {
        ++i;
    }
    while (s2[j]) {
        s1[i++] = s2[j++];
    }
    s1[i] = '\0';
}
```

We can simplify the code even further:

```
// strcat3.c

void strcat(char s1[], char s2[]) {
    int i = 0, j = 0;

    while (s1[i]) {
        ++i;
    }
    while (s1[i++] = s2[j++]) {
        ;
    }
}
```

- strcmp(s1, s2) Performs a comparison of string s1 to string s2, starting with the first character in each string and continuing with subsequent characters until the corresponding characters differ or until the end of the strings is reached. The function returns a value that is:
  - < 0 if s1 is less than s2
  - == 0 if s1 is the same as s2
  - > 0 if s1 is greater than s2

Function prototype:
int strcmp(char *s1, char *s2);

We write our own code to perform a string comparison:

```
// strcmp1.c

int strcmp(char s1[], char s2[]) {
    int i = 0;

    while (s1[i] == s2[i] && s1[i] != '\0') {
        ++i;
    }
    return s1[i] - s2[i];
}
```

Here's an example of the use of the `strcmp()` function:

```
// compareStrings.c

#include <stdio.h>
#include <string.h>

int main(void) {
    int num;

    char s1[] = "red";
    char s2[] = "blue";
    num = strcmp(s1, s2);
    if (num < 0) {
        printf("%s is smaller.\n", s1);
    } else if (num > 0) {
        printf("%s is smaller.\n", s2);
    } else {
        printf("The strings are the same.");
    }
    return 0;
}
```

The output produced looks like this:

```
blue is smaller.
```

Note that C does not allow us to directly compare two strings for equality using the equality operator:

```
if (s1 == s2)
```

This is due to the fact that the equality operator can only be applied to simple variable types such as int, float, char, etc., but not to structures or arrays.

## Additional String Functions

Here are additional string manipulation functions located in the string library:

- strncpy(s1, s2, max)

Copies up to max characters from string s2 into string s1, truncating or null-padding s1. The target string s1 might not be null-terminated if the length of s2 is max or more.

Function prototype:
char *strncpy(char *s1, char *s2, int max);

- strncmp(s1, s2, max)

Makes the same comparison as strcmp(), but looks at no more than max characters. It starts with the first character in each string and continues with subsequent characters until the corresponding characters differ or until it has examined max characters. Returns an int value based on the result of comparing string s1 (or part of it) to string s2 (or part of it). The function returns a value that is:
< 0 if s1 is less than s2
== 0 if s1 is the same as s2
> 0 if s1 is greater than s2

Function prototype:
int strncmp(char *s1, char *s2, int max);

- strchr(s1, c)

Scans string s1 for the first occurrence of character c. Returns a pointer to the first occurrence of the character c in s1. If c does not occur in s, strchr() returns null.

Function prototype:
char *strchr(char *s1, int c);

- strrchr(s1, c)

Scans a string for the last occurrence of a given character. strrchr() scans string s1 in the reverse direction, looking for character c. Returns a pointer to the last occurrence of character c. If character c does not occur in string s1, strrchr() returns null.

Function prototype:
char *strrchr(char *s1, int c);

- strstr(s1, s2)

Scans string s1 for the first occurrence of the substring s2. Returns a pointer to the element in s1, where s2 begins (points to s2 in s1). If s2 does not occur in s1, strstr() returns null.

Function prototype:
char *strstr(char *s1, char *s2);

- strset(s1, c)

Sets all characters in string s1 to character c. It quits when the terminating null character is found. Returns s1.

Function prototype:
char *strset(char *s1, int c);

- strrev(s1)

Reverses a string. strrev() changes all characters in a string to reverse order, except the terminating null character. Returns a pointer to the reversed string.

Function prototype:
char *strrev(char *s1);

- strlwr(s1)

Converts uppercase letters in string s1 to lowercase. No other characters are changed. Returns s1.

Function prototype:
char *strlwr(char *s1);

- strupr(s1)

Converts lowercase letters in string s1 to uppercase.
No other characters are changed. Returns s1.

Function prototype:
char *strupr(char *s1);

## Two String Examples

Below are two string functions. See if you can figure out how they work.

```
// reverse.c
// Function to reverse a string in place
void reverse(char s[]) {
    int c, i, j;
    for (i = 0, j = (int)strlen(s)-1; i < j; ++i, --j) {
        c = s[i];
        s[i] = s[j];
        s[j] = c;
    }
}
```

```
// convert.c
// Function converts a string of digits into its numeric equivalent
int atoi(char buf[]) {
    int i, num;
    num = 0;
    for (i = 0; buf[i] >= '0' && buf[i] <= '9'; ++i) {
        num = 10 * num + buf[i] - 48;
    }
    return num;
}
```

## Strings and Pointers

Consider the following two declarations:

```
(1) char word[] = "Computer";
(2) char *word = "Computer";
```

In declaration (1) the compiler counts up the characters and sizes the array accordingly, for a total of 9 bytes (including the '\0' character). Here, the array name word is a constant pointer to the first element of the array:

```
word == &word[0]
```

and we can show the following equalities:

```
*word == 'C'
*(word + 1) == word[1] == 'o'
```

In declaration (2) pointer notation is used to set up a string. The compiler actually reserves 13 bytes of storage: 9 for the string and 4 for the pointer variable that will point to the string.

In each case word is a pointer to a string. In each case the string itself determines the amount of storage set aside for the string. But the forms are not identical. The array form sets up an array of 9 elements (including the '\0' character) in storage and the compiler recognizes the name word as a synonym for the address of the first array element, &word[0]. Note that word is a pointer constant that contains the base address of the array and that cannot change. You can reference word + 1 to identify the next element in the array, but ++word is not allowed.

The pointer form also causes 9 elements in storage to be set aside for the string. However, it also sets aside one more storage location for the pointer variable word. This variable initially points to the beginning of the string, but its value can change. Here, ++word would point to the second character, etc.
