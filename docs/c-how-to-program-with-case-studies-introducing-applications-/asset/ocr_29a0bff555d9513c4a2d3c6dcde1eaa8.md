```
6 int a = 7;
7 int *aPtr = &a; // set aPtr to the address of a
8
9 printf('Address of a is %p\nValue of aPtr is %p\n\n', &a, aPtr);
10 printf('Value of a is %d\nValue of *aPtr is %d\n\n', a, *aPtr);
11 printf('Showing that * and & are complements of each other\n');
12 printf('&*aPtr = %p\n*&aPtr = %p\n', &*aPtr, *&aPtr);
13 }
```

Address of a is 0x7ffe69386cc
Value of aPtr is 0x7ffe69386cc

Value of a is 7
Value of *aPtr is 7

Showing that * and & are complements of each other
&*aPtr = 0x7ffe69386cc
*&aPtr = 0x7ffe69386cc

Fig. 7.1 | Using the & and * pointer operators. (Part 2 of 2.)

The following table lists the precedence and grouping of the operators introduced to this point:

| Operators | Grouping | Type |
|---|---|---|
| () [] ++ (postfix) -- (postfix) | left to right | postfix |
| + - ++ -- ! * & (type) | right to left | unary |
| * / % | left to right | multiplicative |
| + - | left to right | additive |
| < <= > >= | left to right | relational |
| == != | left to right | equality |
| && | left to right | logical AND |
| || | left to right | logical OR |
| ?: | right to left | conditional |
| = += -= *= /= %= | right to left | assignment |
| , | left to right | comma |

# Self Check

(True/False) Assuming the definitions
double d = 98.6;
double *dPtr;

the following statement assigns variable d's address to the pointer variable dPtr:

dPtr = &d;

Variable dPtr is then said to "point to" d.
Answer: True.