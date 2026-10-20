After swap, value of b :200

# Reference Parameters

This is a reference to a variable’s memory location. When using this mechanism, a new storage location will not be created for the parameters unlike what happens with value parameters. Reference parameters will represent the exact memory location of the actual parameters which have been supplied to the method. It is possible to declare the reference parameters with the help of the ref keyword.

Look at the following example.

```
using System;

namespace CalculatorApplication
{
    class NumberManipulator
    {
        public void swap(ref int x, ref int y)
        {
            int temp;
            temp = x; /* save the value of x */
            x = y;  /* put y into x */
```