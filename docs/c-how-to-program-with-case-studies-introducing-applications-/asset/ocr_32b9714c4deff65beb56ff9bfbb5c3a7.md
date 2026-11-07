```
After s2 is copied into s1 with memcpy, s1 contains:
Copy this string
```

Fig. 8.21 | Using function memcpy. (Part 2 of 2.)

# 8.9.2 Function memmove

Like memcpy, function memmove copies a specified number of bytes from the object pointed to by its second argument into the object pointed to by its first argument. Copying is performed as if the bytes were copied from the second argument into a temporary array, then copied from the temporary array into the first argument. This allows bytes from one part of a string (or block of memory) to be copied into another part of the same string (or block of memory), even if the two portions overlap. Other than memmove, string-manipulation functions that copy characters have undefined results when copying between parts of the same string. Figure 8.22 uses memmove to copy the last 10 bytes of array x into the first 10 bytes of array x.

```
// fig08_22.c
// Using function memmove
#include <stdio.h>
#include <string.h>

int main(void) {
    char x[] = "Home Sweet Home"; // initialize char array x

    printf("The string in array x before memmove is: %s\n", x);
    printf("The string in array x after memmove is: %s\n",
        (char *) memmove(x, &x[5], 10));
}
```

```
The string in array x before memmove is: Home Sweet Home
The string in array x after memmove is: Sweet Home Home
```

Fig. 8.22 | Using function memmove.

# 8.9.3 Function memcmp

Function memcmp (Fig. 8.23) compares the specified number of bytes of its first argument with its second argument’s corresponding bytes. The function returns a value greater than 0 if the first argument is greater than the second, 0 if the arguments are equal or a value less than 0 if the first argument is less than the second.

```
// fig08_23.c
// Using function memcmp
#include <stdio.h>
#include <string.h>
```

Fig. 8.23 | Using function memcmp. (Part 1 of 2.)