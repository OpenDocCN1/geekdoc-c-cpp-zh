The following expression and test for equality is correct and valid:

```
if (aVar == aValue);
```

If the two expressions are not equal, the parenthesized expression is 0, and the path qualified by the “if” expression is not taken. However, if a minor typing error occurs to create:

```
if (aVar = aValue);
```

first, aVar is assigned the value of aValue. Then, aVar is evaluated and returns aValue, which is typically not 0, and the qualified path is taken, which may create a problem.

Good coding style recommends writing such tests as follows.

```
if (aValue == aVar);
```

Now if one of the = operators is dropped, the attempt to assign aVar to aValue, which is an rvalue, will fail and be rejected by the compiler because an rvalue can only appear on the right hand side of an assignment. The value of an rvalue can be assigned but cannot be assigned to, that is, an rvalue cannot appear on the left hand side of an assignment statement. If the path is always taken, it may be taken at the wrong time or under the wrong conditions leading to a potentially serious problem.

Manage all data containers to ensure that data cannot be written beyond the bounds of the container. The starting and ending addresses of a container are known; thus, so is the size.

When working with arrays, remember that the starting index of a one dimension array is 0 and the ending index is N – 1, where N is the number of entries. Testing if an array index is that is <= N will go beyond the container is a problem as we illustrated in Figure 8.40.

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int i = 0;
    int anArray[5]; // array contains 5 elements

    for(i = 0; i <= 5; i++) // write to 6 elements, 1 past end
    {
        anArray[i]=i;
    }

    // prints 6 elements 0..5
    for(i = 0; i <= 5; i++)
    {
        printf("array value at index %d is %d\n", anArray[i], i);
    }

    return 0;
}
```

Figure 8.40 Write Beyond the End of an Array.

# 8.23.1.3 Third Steps

The strategy for testing the software for design flaws, oversights, or potential vulnerabilities mirrors that utilized for the hardware. Whether testing hardware or software, keep in mind that the critical objective in testing is to identify and correct problems with the design and not simply to show that it works. Tests should be designed for and applied to all boundary condition values for all variables and functions with the intent of finding problems with the code.