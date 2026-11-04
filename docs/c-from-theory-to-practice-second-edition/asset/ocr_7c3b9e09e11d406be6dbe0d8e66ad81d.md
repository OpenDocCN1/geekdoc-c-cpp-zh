> A common error is to confuse the '\0' and '0' characters. The ASCII code of the null character is 0, while the ASCII code of the zero character is 48.

As with an ordinary array, if the number of the characters is less than the size of the array, the remaining elements are initialized to 0. If it is greater, it is an error. For example, with the declaration:

```
char str[8] = "me";
```

because the ASCII value of '\0' is 0, str[0] becomes 'm', str[1] becomes 'e' and the rest elements are initialized to 0, or equivalently to '\0'. Similarly, with the declaration:

```
char str[8] = {0};
```

all str elements are initialized to '\0'.

A flexible way to initialize the array is to omit its length and let the compiler compute it. For example, with the declaration:

```
char str[] = "message";
```

the compiler calculates the length of "message" and then allocates eight bytes for str to store the seven characters plus the null character. If we use sizeof(str) to output its length, we'll see that it is 8, indeed. Leaving the compiler to compute the length, it is easier and safer, since a careless programmer might make a calculation error or forget to add an extra place for the null character.

> When declaring an array of characters to store a string, don't forget to reserve an extra place for the null character.

If the null character is missing and the program uses a library function to handle the array, unpredictable results may arise because C functions assume that strings are null terminated. Some programmers prefer to emphasize the reservation by adding 1 in the declaration. For example:

```
char s[SIZE+1];
```

Therefore, be cautious, the declarations char s[] = "abc"; and char s[3] = "abc"; are different. In the first case the size of s is 4, the null character is stored and we've got a string, while in the second case the size of s is 3 and we've no string.

# Exercise

C.10.1 Is the following program error free?

```
#include <stdio.h>
int main(void)
{
```