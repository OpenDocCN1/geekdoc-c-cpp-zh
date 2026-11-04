The output from the program is shown here:

```
Here is a: 5, 6, 7
Here is b: 10, 10, 10
Here is c: 0, 0, 0

c is false.

a & b is true.
a & c is false.
a | b is true.
a | c is true.
```

In this approach, the &, |, and ! operator methods each return a bool result. This is necessary if the operators are to be used in their normal manner (that is, in places that expect a bool result). Recall that for all built-in types, the outcome of a logical operation is a value of type bool. Thus, having the overloaded versions of these operators return type bool is a rational approach. Unfortunately, this approach works only if you will not be needing the short-circuit operators.

# Enabling the Short-Circuit Operators

To enable the use of the && and || short-circuit operators, you must follow four rules.

First, the class must overload & and |. Second, the return type of the overloaded & and | methods must be the same as the class for which the operators are being overloaded. Third, each parameter must be a reference to an object of the class for which the operator is being overloaded. Fourth, the true and false operators must be overloaded for the class. When these conditions have been met, the short-circuit operators automatically become available for use.

The following program shows how to properly implement the & and | for the ThreeD class so that the short-circuit operators && and || are available.

```
/* A better way to overload !, |, and & for ThreeD.
This version automatically enables the && and || operators. */

using System;

// A three-dimensional coordinate class.
class ThreeD {
    int x, y, z; // 3-D coordinates

    public ThreeD() { x = y = z = 0; }
    public ThreeD(int i, int j, int k) { x = i; y = j; z = k; }

    // Overload ! for short-circuit evaluation.
    public static ThreeD operator & (ThreeD op1, ThreeD op2)
    {
        if( ((op1.x != 0) || (op1.y != 0) || (op1.z != 0)) ||
            ((op2.x != 0) || (op2.y != 0) || (op2.z != 0)) )
            return new ThreeD(1, 1, 1);
        else
            return new ThreeD(0, 0, 0);
    }
```