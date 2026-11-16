To see that arithmetic works, try adding 4 + 3:

```
410 = 001002
+ 310 = 000112
-------
710 = 001112
```

That was easy since involved no carries. Next we will try 3 + 1:

```
310 = 11
+ 110 = 000112
-------
410 = 001002
```

In the ones column (rightmost column), 12 + 12 = 102, so write a 0 and carry the 1 to the top of the next column to the left (that is, the twos column). In the twos column, 12 + 12 + 02 = 102, so we must carry a 1 into the fours column as well.

The next example illustrates a limitation of our finite representation. Consider the sum 8 + 28:

```
   11
810 = 010002
+ 2810 = 111002
-------
410 = 100102
```

In the this sum we have a carry of 1 from the eights column to the 16s column, and we have a carry from the 16s column to nowhere. We need a sixth column (a 32s column), another place value, but our **unsigned tiny** type is limited to five bits. That carry out from the 16s place is lost. The largest **unsigned tiny** value is 31, but 28 + 8 = 36. It is not possible to store the value 36 in an **unsigned tiny** just as it is impossible to store the value 5,000,000,000 in a C++ **unsigned** double variable.

Consider exceeding the capacity of the **unsigned tiny** type by just one:

```
   11111
3110 = 111112
+ 110 = 000012
-------
010 = 1000002
```

Adding one to the largest possible **unsigned tiny**, 31, results in the smallest possible value, 0! This mirrors the behavior of the actual C++ **unsigned** type, as Listing 4.13 (unsignedoverflow.cpp) demonstrates.

# Listing 4.13: unsignedoverflow.cpp

```
#include <iostream>

int main() {
    unsigned x = 4294967293; // Almost the largest possible unsigned value
    std::cout << x << " + 1 = " << x + 1 << " \n";
    std::cout << x << " + 2 = " << x + 2 << " \n";
    std::cout << x << " + 3 = " << x + 3 << " \n";
}
```

Listing 4.13 (unsignedoverflow.cpp) prints