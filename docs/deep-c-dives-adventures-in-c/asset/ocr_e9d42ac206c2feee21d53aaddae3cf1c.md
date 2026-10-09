# Swapping Values

Usually, if you want to swap two values, you need a third variable to hold the result while the swap occurs:

```
int temp = a;
a = b;
b = temp;
```

You can swap without a third variable using XOR:

```
a = a^b;
b = b^a;
a = a^b;
```

If you try it out you will find that a and b have swapped values. Seeing why it works takes a little longer!

# Overflow-Free Average

Consider finding the average of two integers. The simple straightforward way of doing the job is:

```
int average = (a+b)/2;
```

This has one problem – a+b can overflow even if the answer is representable in the number of bits available. At first it looks as if nothing can be done, but if a result can be represented then there is usually a bit-manipulation way of computing it without the threat of overflow.

In this case we need to notice that addition is a simple logical operation. If you add the two values, a and b together then the sum bits are:

```
a ^ b
```

and the carry bits are:

```
a & b
```

this is how a half-adder is implemented.

For example:


| a | 1 | 0 | 1 |
| b | 0 | 1 | 1 |
| sum | 1 | 1 | 0 |
| carry | 0 | 0 | 1 |