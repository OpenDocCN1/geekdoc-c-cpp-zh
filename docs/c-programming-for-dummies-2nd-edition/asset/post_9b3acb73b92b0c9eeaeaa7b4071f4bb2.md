
decimal value. The result of the operation is that the bits set to 1 in the set value are also set to 1 in the result value.

## Exercise 17-3: Type the source code from Listing 17-2 into your editor to create a new program. Build and run the program.

Here's the output I see for the value 65:

Type a value from 0 to 255: 65
0100001    65
| 0010000  32
= 0110001  97

You can see in the binary output how the sixth bit is set in the result.

*What does it mean?*

The bitwise | (OR) operator lets you manipulate values at the binary level. This control has interesting consequences for certain mathematical operations, as shown in Listing 17-3.

## LISTING 17-3: Up with That Text

```c
#include <stdio.h>

int main()
{
    char input[64];
    int ch;
    int x = 0;

    printf("Type in ALL CAPS: ");
    fgets(input,63,stdin);

    while(input[x] != '\n')
    {
        ch = input[x] | 32;
        putchar(ch);
        x++;
    }
    putchar('\n');

    return(0);
}
```

## Operating exclusively with XOR

XOR is the exclusive OR operator, yet another bitwise logical operator. And to answer your most pressing question, you pronounce XOR like “zor.” It’s the perfect evil name from bad science fiction.

The XOR operation is kind of weird, but it does have its charm. In this manipulation, bits are compared with one another, just like the & and | operators. When two bits are identical, XOR coughs up a 0. When the two bits are different, XOR spits out a 1. As usual, a program example helps explain things.

The C language XOR operator is the caret character: ^. You can find it put into action on Line 14 in Listing 17-4.

## LISTING 17-4: It's Exclusive or

```c
#include <stdio.h>

char *binbin(unsigned char n);

int main()
{
    int a,x,r;

    a = 73;
    x = 170;

    printf("%s %3d\n",
        binbin((unsigned char)a),a);
    printf("^ %s %3d\n",
        binbin((unsigned char)x),x);
    r = a ^ x;
    printf("= %s %3d\n",
        binbin((unsigned char)r),r);
    return(0);
}

char *binbin(unsigned char n)
{
    static char bin[9];
    int x;

    for(x=0;x<8;x++)
    {
        bin[x] = n & 0x80 ? '1' : '0';
        n <<= 1;
    }
    bin[x] = '\0';
    return(bin);
}
```

## Exercise 17-8: Type the source code from Listing 17-4 into your editor. Build and run to see how the XOR operation affects binary values.

The charming thing about the XOR operation is that if you use the same XOR value on a variable, you get back the variable’s original value.

## Exercise 17-9: Modify the source code from Listing 17-4 so that one more XOR operation takes place. Insert these three statements after line 18 (the two `printf()` statements are split between two lines):

```c
printf("^ %s %3d\n",
       bin((unsigned char)x),x);
a = r ^ x;
printf("= %s %3d\n",
       bin((unsigned char)a),a);
```

Save your update to the code. Build and run. The output looks like this:

```
  01001001  73
^ 10101110 170
= 11100011 227
^ 10101110 170
= 01001001  73
```

Using the same XOR value of 170 turns the value 73 first into 227 and then back to 73.

![](img/dcc0cd79d4a45cfce24fa49d85442884_273_0.png)

Because XOR is the exclusive OR operator, some programmers refer to the standard bitwise OR operator as the inclusive OR operator.

## Understanding the ~ and ! operators

Two infrequent binary operators are the unary ~ (or one's complement) and the ! (or NOT). They lack the charm of the logical bitwise operators, but I suppose that they have a place.

The one's complement operator flips all the bits in a value, turning a 1 into a 0 and a 0 into a 1. For example:

```
~01010111 = 10101100
```

The ! (NOT) operator affects the entire value — all the bits. It changes any non-zero value to 0 and the value 0 to 1:

```
10101011 = 00000000
10000000 = 00000001
```

> Zero and 1 are the only two results possible when using the bitwise ! operator.
> 
> Both the ~ and ! operators are unary operators — you prefix a value to get the results.

| Operator | Name | Type | Action |
| --- | --- | --- | --- |
| & | AND | Bitwise | Masks bits, resetting some bits to 0 and leaving the rest alone |
| \| | OR | Bitwise | Sets bits, changing specific bits from 0 to 1 |
| ^ | XOR | Bitwise | Changes bits to 0 when they match; otherwise, to 1 |
| ~ | 1's complement | Unary | Reverses all bits |
| ! | NOT | Unary | Changes nonzero values to 0; 0 values, to 1 |

## Shifting binary values

The C language features two binary operators that perform the equivalent operation of "Everyone move one step to the left (or right)." The << and >> operators shift bits in value, matching them to the left or right, respectively. Here's the format for the << operator:

```
v = int << count;
```

int is an integer value. count is the number of places to shift the value's bits to the left. The result of this operation is stored in variable v. Any bits that are shifted to the left beyond the width of the int variable x are lost. New bits shifted in from the right are always 0.

As with most binary nonsense, it helps to see what's going on in a value when its bits are shifted. Therefore, I present Listing 17-5.

## LISTING 17-5: Everyone Out of the Pool!

```c
#include <stdio.h>

char *binbin(unsigned char n);

int main()
{
    unsigned bshift,x;

    printf("Type a value 0 to 255: ");
    scanf("%u",&bshift);

    for(x=0;x<8;x++)
    {
        printf("%s\n",
            binbin((unsigned char)bshift));
        bshift = bshift << 1;
    }
    return(0);
}

char *binbin(unsigned char n)
{
    static char bin[9];
    int x;

    for(x=0;x<8;x++)
    {
        bin[x] = n & 0x80 ? '1' : '0';
        n <<= 1;
    }
    bin[x] = '\0';
    return(bin);
}
```

The shift operation takes place at Line 16 in Listing 17-5. The value in variable `bshift` is shifted to the left one bit.

## Exercise 17-10: Type the source code from Listing 17-5 into your editor and build a new program to see what it does.

Shifting a value one bit to the left doubles the value. This rule holds true to a certain point: Obviously, the farther left you shift, some bits get lost and the value ceases to double. Also, this trick works best for unsigned values.

## Exercise 17-11: Modify the source code from Listing 17-5 so that the `printf()` function at Line 14 also displays the decimal value of the `bshift` variable. You should also modify the `binbin()` function so that it displays 16 digits instead of 8. (Refer to Exercise 17-2 for the 16-bit `binbin()` solution.)

Here’s the output I see when using the value 12:

```
Type a value from 0 to 255: 12
000000000001100 12
000000000011000 24
000000000110000 48
000000001100000 96
000000011000000 192
000000110000000 384
000001100000000 768
000011000000000 1536
```

Try the value 800,000,000 (don’t type the commas) to see how the doubling rule fails as the values keep shifting to the left. Also see the nearby sidebar “Negative binary numbers.”

The >> shift operator works similarly to the << shift operator, though values are marched to the right instead of the left. Any bit that’s marched off the right end is discarded, and only zero bits slide in on the left. Here’s the format:

```
v = int >> count;
```

*int* is an integer value, and *count* is the number of places to shift the bits to the right. The result is stored in variable *v*.

## Exercise 17-12: Modify the source code from Exercise 17-11 so that the right shift operator is used instead of the left shift at Line 15. Build the program.

## NEGATIVE BINARY NUMBERS

Binary numbers are always positive, considering that the values of a bit can be only 1 or 0 and not –1 and 0. So how does the computer do signed integers? Easy: It cheats.

The leftmost bit in a signed binary value is known as the sign bit. When that bit is set (equal to 1), the value is negative for a signed int. Otherwise, the value is read as positive.

![](img/dcc0cd79d4a45cfce24fa49d85442884_277_0.png)

In this example, the sign bit is set for a signed char. The values expressed are negative, which is in the range of a signed char variable.

![](img/dcc0cd79d4a45cfce24fa49d85442884_277_1.png)

In this example, the sign bit is ignored because the value is an unsigned char. The values can only be positive, which is why the positive range for an unsigned variable is greater than for a signed variable.
