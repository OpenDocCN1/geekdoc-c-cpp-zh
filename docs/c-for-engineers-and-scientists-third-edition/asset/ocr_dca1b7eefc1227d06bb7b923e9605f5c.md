# 15.1 The AND Operator

The AND operator, &, carries a bit-by-bit AND comparison between its two operands. The result of each bit-by-bit comparison is a 1 when both bits being compared are 1; otherwise, the result of the AND operation is a 0. For example, the following two 8-numbers are to be ANDed:

```
1 0 1 0 0 0 1 1
1 1 0 1 0 1 0 1
----------------
```

To perform an AND operation, each bit in one operand is compared to the bit occupying the same position in the other operand. This sample AND operation illustrates the correspondence between these bits for these operands:

```
1 0 1 0 0 0 1 1
& 1 1 0 1 0 1 0 1
----------------
```

As shown, both bits being compared are 1s, the result is a 1; otherwise, the result is a 0. The result of each comparison is, of course, independent of any other bit comparison. Program 15.1 shows the use of an AND operation. In this program, the variable op1 is initialized to the octal value 325, which is the octal equivalent of the binary number 1 0 1 0 1 1, and the variable op2 is initialized to the octal value 263, which is the octal representation of the binary number 1 0 1 0 0 1. They are the same binary numbers used in the preceding example.

![](bbox=[0.107, 0.545, 0.183, 0.593])

# Program 15.1

```
#include <iostream>
using namespace std;

int main() {
    int op1 = 0325, op2 = 0263;

    int op3 = op1 & op2;
    cout << oct << op1 << " ANDed with " << op2 << " is " << op3 << endl;

    return 0;
}
```

Program 15.1 produces the following output:

325 ANDed with 263 is 221