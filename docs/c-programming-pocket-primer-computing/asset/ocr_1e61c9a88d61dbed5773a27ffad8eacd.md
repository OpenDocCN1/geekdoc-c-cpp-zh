```
```c
    printf("Original: %s\n", ptr1);
    printf("Reverse: %s\n", ptr2);
}
```
```

Listing 6.17 contains a main() function that initializes the character pointer `ptr1` to a hard-coded string, and declares the character pointer `ptr2`. The length of the character string at `ptr1` is assigned to the integer variable `len`, and `ptr2` is assigned the address of a block of memory that is as long as the string at location `ptr1`.

The next section of code is a loop that iterates through the characters of the string at the location of `ptr1`. During each left-to-right iteration through the string `ptr1`, the positions at the “far end” of `ptr2` are assigned the characters from left-to-right iteration through the characters in `ptr1`. If you read the code carefully you can see that the characters at `ptr2` are the reverse order of the characters at `ptr1`. The output from Listing 6.17 is here:

```
```text
Original: this is a string
Reverse: gnirts a si siht
```
```

# # FINDING UPPERCASE AND LOWERCASE LETTERS

Listing 6.18 displays the contents of UpperAndLowerCount.c that illustrates how to construct strings with only uppercase and only lowercase letters from a text string. This code has a subtle bug (can you find it?) that is explained in the discussion after the code listing.

# LISTING 6.18: UpperAndLowerCount.c

```
```c
#include <stdio.h>
```
```