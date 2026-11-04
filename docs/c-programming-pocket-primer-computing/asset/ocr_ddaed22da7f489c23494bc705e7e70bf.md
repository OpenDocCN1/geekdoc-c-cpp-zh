block of code consists of six printf() statements the display the values of the variables x1 through x6 in hexadecimal, decimal, and octal format. The output from Listing 7.2 is here:

```
```
x1 = c8 200 310
x2 = b8 184 270
x3 = 88 136 210
x4 = f8 248 248
x5 = 70 112 160
x6 = 320 800 1440
```
```

Unfortunately, C does not provide a mechanism for displaying binary numbers in the printf() command. However, Listing 7.3 displays the contents of ShowBits.c (borrowed from Wikipedia) that illustrates how to display the digits of a binary number.

# **LISTING 7.3: ShowBits.c**

```
```c
#include <stdio.h>

void showbits(unsigned int x)
{
    int i;

    for(i=(sizeof(int)*8)-1; i>=0; i--)
    {
        (x&(1u<<i)) ? putchar('1'): putchar('0');
    }

    printf("\n");
}

int main()
{
    int j = 5225, m, n;
    printf("%d in binary \t\t ", j);
    showbits(j);
```
```