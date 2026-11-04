
```csharp
*pointer1 = *pointer1 - 1;
Console.WriteLine ("{0}    {1}", number1, number2);

number1 = number1*2;     // Multiplication
*pointer1 = *pointer1*2;
Console.WriteLine ("{0}    {1}", number1, number2);

number1 = number1/2;     // Division
*pointer1 = *pointer1/2;
Console.WriteLine ("{0}    {1}", number1, number2);

number1 = number1%3;     // Remainders
*pointer1 = *pointer1%3;
Console.WriteLine ("{0}    {1}", number1, number2);
}
}
}
```

### Example 4.29. Shorthand notation and the incrementing and decrementing operators.

```csharp
using System;

namespace Chapter4 {
    class Class1 {
        static unsafe void Main() {
            int number1 = 0, number2 = 0;
            int* pointer1 = &number2;

            for (int index = 0; index < 10; index++) {
                number1 = number1++;
                *pointer1 = (*pointer1)++;
            }
            Console.WriteLine ("{0}    {1}", number1, number2);
            number1 = number1 - 1;
            *pointer1 = (*pointer1)--;
            Console.WriteLine ("{0}    {1}", number1, number2);

            // number1 = number1 + number1
            number1 = number1 += number1;
            // *pointer1 = *pointer1 + *pointer1
            *pointer1 = *pointer1 += *pointer1;
            Console.WriteLine ("{0}    {1}", number1, number2);
            // number1 = number1 - number1
            number1 = number1 -= number1;
            // *pointer1 = *pointer1 - *pointer1
            *pointer1 = *pointer1 -= *pointer1;
            Console.WriteLine ("{0}    {1}", number1, number2);

            number1 = 5;
            *pointer1 = 5;
            number1 = number1*=2;
            *pointer1 = *pointer1*=2;
            Console.WriteLine ("{0}    {1}", number1, number2);
            number1 = number1/=2;
            *pointer1 = *pointer1/=2;
            Console.WriteLine ("{0}    {1}", number1, number2);
            number1 = number1/=2;
            *pointer1 = *pointer1/=2;
            Console.WriteLine ("{0}    {1}", number1, number2);
            number1 = 5;
            *pointer1 = 5;
            number1 = number1%=2;
            *pointer1 = *pointer1%=2;
            Console.WriteLine ("{0}    {1}", number1, number2);
        }
    }
}
```

## String and Address Arithmetic

String arithmetic is also fairly simple, but it doesn't involve changing numeric values. Instead, we'll use arithmetic commands to move an array's index from address to address. This is possible because the strings are sequentially stored in memory locations. Since we cannot know the spatial difference between any two strings, this type of memory manipulation must be limited to arranged variables that are part of the same string (see memory mapping for further details).

### Example 4.30. Mapping Memory.

Computers allocate a certain amount of Random Access Memory (RAM) to each variable declared inside of a program. This memory is actually part of a computer's hardware, and is reused and/or overwritten every time we run a new program. The methods used to store variables and the exact locations in memory of those variables are irrelevant to us as programmers, and will be left to books related to computer operating systems and hardware. Our understanding of how and where data is placed will have to be on an abstract scale. This therefore includes an imaginary point of reference that we can build upon to access and alter any arrays or strings of data declared in our programs.

First off, let's assume that we've just declared and initialized a character array or string to the values A, B, C, D, and E. We know that the strings' positions will reflect our points (as in zero equals A, one equals B and two equals C, etc.), but we don't know how this will relate to the computer's placement of that data. If we then reason that the computer places the first component A in some arbitrary location (say memory location 1000), using the basic form of 1 byte per character, we can deduce that the location 1001 would hold the value B, location 1002 would hold C, and so on. From this, we can also graph a map of the locations:

| Memory Location | Referencing Array | Value in Memory |
|---|---|---|
| [1000] = | array[0] = | A |
| [1001] = | array[1] = | B |
| [1002] = | array[2] = | C |
| [1003] = | array[3] = | D |
| [1004] = | array[4] = | E |
| [1005] = | array[5] = | \0 |

If a character takes up 2 bytes per element, their memory locations would be listed as

| Memory Location | Referencing Array | Value in Memory |
|---|---|---|
| [1000 – 1001] = | array[0] = | 1 |
| [1002 – 1003] = | array[1] = | 2 |
| [1004 – 1005] = | array[2] = | 3 |
| [1006 – 1007] = | array[3] = | 4 |
| [1008 – 1009] = | array[4] = | 5 |

In addition, if a data type takes up 4 bytes per element, it would produce a larger span or cluster of data.

| Memory Location | Referencing Array | Value in Memory |
|---|---|---|
| [1000 – 1003] = | array[0] = | 1 |
| [1004 – 1007] = | array[1] = | 2 |
| [1008 – 1011] = | array[2] = | 3 |
| [1012 – 1015] = | array[3] = | 4 |
| [1016 – 1019] = | array[4] = | 5 |

Further, this could continue on and on at least up to 64 bits (the 128-bit machines are not quite ready yet). Data that takes up 8 bytes is equivalent to:

| Memory Location | Referencing Array | Value in Memory |
|---|---|---|
| [1000 – 1007] = | array[0] = | 1 |
| [1008 – 1015] = | array[1] = | 2 |
| [1016 – 1023] = | array[2] = | 3 |
| [1024 – 1031] = | array[3] = | 4 |
| [1032 – 1039] = | array[4] = | 5 |

Manipulating strings using arithmetic is fairly straightforward, but we'll still have to make a few tiny adjustments (see Example 4.31).

> You can also subtract one pointer location from another as long as they're referencing the same string. This special situation gives us an integer value equal to the distance between the two.
> 
> The program in Example 4.31 converts letters from uppercase to lowercase and back from lowercase to uppercase using string (address) arithmetic rather than the ToUpper and ToLower functions.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_275_0.png)

### Example 4.31. String arithmetic.

```csharp
using System;

namespace Chapter4 {
    class Class1 {
        static void Main() {
            char input;

            do {
                input = char.Parse(Console.ReadLine());
                input = MyToUpper(input);
                Console.WriteLine("{0}", input);
                input = MyToLower(input);
                Console.WriteLine(input);
            } while (input != 'z');
        }

        static char MyToUpper(char input) {
            string alpha =
                "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";

            for (int index = 0; index < 26; index++)
                if (input == (alpha[index]))
                    input = (alpha[index + 26]);

            return (input);
        }

        static char MyToLower(char input) {
            string alpha =
                "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";

            for (int index = 26; index < 52; index++)
                if (input == (alpha[index]))
                    input = (alpha[index - 26]);

            return (input);
        }
    }
}
}
```

## The void Pointer

The *void* data type can be used to declare generalized pointers, that is, pointers that do not, as yet, have a set data type. These all-purpose pointers can be reassigned to different data types with each function call or as part of an abstract subroutine. void pointers can be converted to any of the other data types and can be used as a sort of template, always changing to fit the needs of a program (see Example 4.32).

### Example 4.32. The void pointer.

```csharp
using System;

namespace Chapter4 {
    class Class1 {
        static unsafe void Main() {
            short variable1 = 20;
            int variable2 = 20;
            long variable3 = 100000;
            float variable4 = 6.0F;
            double variable5 = 123.456789;
            decimal variable6 = 321.123456M;

            Console.WriteLine("{0}\n{1}\n{2}\n{3}\n{4}\n{5}\n",
                variable1, variable2, variable3, variable4, variable5,
                variable6);

            MyFunction (&variable1,'s');   // s for short
            MyFunction (&variable2,'i');   // i for integer
            MyFunction (&variable3,'l');   // l for long
            MyFunction (&variable4,'f');   // f for float
            MyFunction (&variable5,'d');   // d for double
            MyFunction (&variable6,'e');   // e for decimal

            Console.WriteLine ("{0}\n {1}\n {2}\n {3}\n {4}\n {5}\n",
                variable1, variable2, variable3, variable4, variable5,
                variable6);
        }

        static unsafe void MyFunction (void *values, char data_type) {
            switch (data_type) {
                case 's': {
                    *((short *)values) += 1;
                    break;
                }

                case 'i': {
                    *((int *)values) -= 1;
                    break;
                }

                case 'l': {
                    *((long *)values) *= 2;
                    break;
                }

                case 'f': {
                    *((float *)values) /= 2;
                    break;
                }

                case 'd': {
                    *((double *)values) = *((double *)values) + 2;
                    break;
                }

                case 'e': {
                    *((decimal *)values) = *((decimal *)values) - 2;
                    break;
                }
            }
        }
    }
}
```
