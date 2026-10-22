# Another Example

Let’s work through one more example. The goal this time is to write a function that inverts the last n bits in a value, with both n and the value being function arguments.

The ~ operator inverts bits, but it inverts all the bits in a byte, not just a select few. However, the ^ operator (EXCLUSIVE OR), as you have seen, can be used to toggle individual bits. Suppose you create a mask with the last n bits set to 1 and the remaining bits set to 0. Then applying ^ to that mask and a value toggles, or inverts, the last n bits, leaving the other bits unchanged. That’s the approach used here:

```
int invert_end(int num, int bits)
{
    int mask = 0;
    int bitval = 1;

    while (bits-- > 0)
    {
        mask |= bitval;
        bitval <<= 1;
    }
    return num ^ mask;
}
```

The while loop creates the mask. Initially, mask has all its bits set to 0. The first pass through the loop sets bit 0 to 1 and then increases the value of bitval to 2; that is, it sets bit 0 to 0 and bit 1 to 1. The next pass through then sets bit 1 of mask to 1, and so on. Finally, the num ^ mask operation produces the desired result.

To test the function, you can slip it into the preceding program, as shown in Listing 15.2.

# Listing 15.2 The invert4.c Program

```
/* invert4.c -- using bit operations to display binary */
#include <stdio.h>
#include <limits.h>
char * itobs(int, char *);
void show_bstr(const char *);
int invert_end(int num, int bits);

int main(void)
{
    char bin_str[CHAR_BIT * sizeof(int) + 1];

    int number;

    puts("Enter integers and see them in binary.");
    puts("Non-numeric input terminates program.");
```