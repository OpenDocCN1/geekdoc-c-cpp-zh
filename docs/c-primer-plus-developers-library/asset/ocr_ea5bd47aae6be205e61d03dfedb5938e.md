Each arithmetic operator has a corresponding assignment operator, as summarized in Table 5.1. Each operator works analogously to `+=`. Thus, for example, the following statement replaces the current value of k with a value 10 times greater:

```
k *= 10;
```

**Table 5.1. Combined Assignment Operators**

| Operator | Effect (L=left operand, R=right operand) |
|---|---|
| `+=` | Assigns L + R to L |
| `-=` | Assigns L - R to L |
| `*=` | Assigns L * R to L |
| `/=` | Assigns L / R to L |
| `%=` | Assigns L % R to L |

# Compound Statements, or Blocks

The format, or syntax, for writing a C++ `for` statement might seem restrictive to you because the body of the loop must be a single statement. That’s awkward if you want the loop body to contain several statements. Fortunately, C++ provides a syntax loophole through which you may stuff as many statements as you like into a loop body. The trick is to use paired braces to construct a compound statement, or block. The block consists of paired braces and the statements they enclose and, for the purposes of syntax, counts as a single statement. For example, the program in Listing 5.8 uses braces to combine three separate statements into a single block. This enables the body of the loop to prompt the user, read input, and do a calculation. The program calculates the running sum of the numbers you enter, and this provides a natural occasion for using the `+=` operator.

Listing 5.8  **block.cpp**

```
```cpp
// block.cpp -- use a block statement
#include <iostream>
int main()
{
    using namespace std;
    cout << "The Amazing Accounto will sum and average ";
    cout << "five numbers for you.\n";
    cout << "Please enter five values:\n";
    double number;
    double sum = 0.0;
    for (int i = 1; i <= 5; i++)
    {
                                      // block starts here
        cout << "Value " << i << " is: ";
        cin >> number;
        sum += number;
    }                                  // block ends here
```
```