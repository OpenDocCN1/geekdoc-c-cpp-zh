The important thing to remember is that C treats enumeration variables and constants as integers.

For example, consider the following program:

```
#include <stdio.h>
int main(void)
{
    int next_seas;
    enum seasons {AUTUMN = 1, WINTER, SPRING, SUMMER} s;

    printf("Enter season [1-4]: ");
    scanf("%d", &s);

    if(s == SUMMER)
        next_seas = AUTUMN;
    else
        next_seas = s+1;
    printf("Next season = %d\n", next_seas);
    return 0;
}
```

The program reads an integer, stores it into the enumeration variable s, and displays the number that corresponds to the next season. Notice that the compiler need not check whether the value stored in an enumeration variable is a valid value for the enumeration. If a value other than its constants is assigned, it is common for a compiler to issue a warning.

Concerning our preference among enum and #define, we'd say that when we need a set of values to characterize an entity (e.g., seasons), the enum type is more representative. And if a function needs that set, it is preferable to pass an enumeration variable than a plain integer. For example:

```
void test(enum codes c); instead of void test(int c);
```

The first prototype tells the reader that the passed value should belong within a set. Therefore, it becomes easier for the reader to read and verify the code. On the other hand, the second prototype does not provide any information about the passed value. Moreover, the preprocessor removes the names defined with the #define directive, so they won't be available during debugging. In general, we use #define when the constants we want to define are unrelated, or few, or they don't represent integers.

# Bitwise Operators

Bitwise operators are used to access the individual bits of an integer variable or constant. A bit value is either 0 or 1. Bitwise operators are particularly useful in several applications; in our experience, we've used them in communication protocols, in data encryption algorithms, and in low-level applications that communicate with the hardware. We'll show you some examples later.