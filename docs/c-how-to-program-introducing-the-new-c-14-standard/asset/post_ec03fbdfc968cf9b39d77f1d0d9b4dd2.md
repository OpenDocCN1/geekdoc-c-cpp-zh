
```c
c += 3;
```

The `+=` operator adds the value of the expression on its right to the value of the variable on its left and stores the result in the variable on the left of the operator. Thus, the assignment expression `c += 3` adds `3` to `c`. **Figure 4.15** shows the arithmetic compound assignment operators, sample expressions using the operators and explanations of what the operators do.

**Fig. 4.15 Arithmetic compound assignment operators.**

Assume: `int c = 3, d = 5, e = 4, f = 6, g = 12;`

| Assignment operator | Sample expression | Explanation | Assigns |
|---|---|---|---|
| `+=` | `c += 7` | `c = c + 7` | `10` to `c` |
| `-=` | `d -= 4` | `d = d - 4` | `1` to `d` |
| `*=` | `e *= 5` | `e = e * 5` | `20` to `e` |
| `/=` | `f /= 3` | `f = f / 3` | `2` to `f` |
| `%=` | `g %= 9` | `g = g % 9` | `3` to `g` |

## 4.13 Increment and Decrement Operators

C++ provides two unary operators (summarized in **Fig. 4.16**) for adding 1 to or subtracting 1 from the value of a numeric variable. These are the unary **increment operator**, `++`, and the unary **decrement operator**, `--`. A program can increment by 1 the value of a variable called `a` using the increment operator, `++`, rather than the expression `a = a + 1` or `a += 1`. An increment or decrement operator that's prefixed to (placed before) a variable is referred to as the **prefix increment** or **prefix decrement operator**, respectively. An increment or decrement operator that's postfixed to (placed after) a variable is referred to as the **postfix increment** or **postfix decrement operator**, respectively.

**Fig. 4.16 Increment and decrement operators.**

| Operator | Operator name | Sample expression | Explanation |
|---|---|---|---|
| `++` | prefix increment | `++a` | Increment `a` by `1`, then use the new value of `a` in the expression in which `a` resides. |
| `++` | postfix increment | `a++` | Use the current value of `a` in the expression in which `a` resides, then increment `a` by `1`. |
| `--` | prefix decrement | `--b` | Decrement `b` by `1`, then use the new value of `b` in the expression in which `b` resides. |
| `--` | postfix decrement | `b--` | Use the current value of `b` in the expression in which `b` resides, then decrement `b` by `1`. |

Using the prefix increment (or decrement) operator to add 1 to (or subtract 1 from) a variable is known as **preincrementing** (or **predecrementing**). This causes the variable to be incremented (decremented) by 1; then the new value of the variable is used in the expression in which it appears.

Using the postfix increment (or decrement) operator to add 1 to (or subtract 1 from) a variable is known as **postincrementing** (or **postdecrementing**). This causes the current value of the variable to be used in the expression in which it appears; then the variable's value is incremented (decremented) by 1.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_481_0.png)

**Good Programming Practice 4.4**

> Unlike binary operators, the unary increment and decrement operators as a matter of style should be placed next to their operands, with no intervening spaces.

### Difference Between Prefix Increment and Postfix Increment Operators

**Figure 4.17** demonstrates the difference between the prefix increment and postfix increment versions of the `++` increment operator. The decrement operator (`--`) works similarly.

```cpp
// Fig. 4.17: Increment.cpp
// Prefix increment and postfix increment operators.
#include <iostream>
using namespace std;

int main() {
    // demonstrate postfix increment operator
    unsigned int c{5}; // initializes c with the value 5
    cout << "c before postincrement: " << c << endl; // prints 5
    cout << "    postincrementing c: " << c++ << endl; // prints 5
    cout << "c after postincrement: " << c << endl; // prints 6

    cout << endl; // skip a line

    // demonstrate prefix increment operator
    c = 5; // assigns 5 to c
    cout << "c before preincrement: " << c << endl; // prints 5
    cout << "    preincrementing c: " << ++c << endl; // prints 6
    cout << "c after preincrement: " << c << endl; // prints 6
}
```

```text
c before postincrement: 5
    postincrementing c: 5
c after postincrement: 6

c before preincrement: 5
    preincrementing c: 6
c after preincrement: 6
```

**Fig. 4.17 Prefix increment and postfix increment operators.**

Line 8 initializes the variable `c` to `5`, and line 9 outputs `c`'s initial value. Line 10 outputs the value of the expression `c++`. This expression postincrements the variable `c`, so `c`'s *original* value (`5`) is output, then `c`'s value is incremented (to `6`). Thus, line 10 outputs `c`'s initial value (`5`) again. Line 11 outputs `c`'s new value (`6`) to prove that the variable's value was indeed incremented in line 10.

Line 16 resets `c`'s value to `5`, and line 17 outputs `c`'s value. Line 18 outputs the value of the expression `++c`. This expression preincrements `c`, so its value is incremented; then the *new value* (`6`) is output. Line 19 outputs `c`'s value again to show that the value of `c` is still `6` after line 18 executes.

### Simplifying Statements with the Arithmetic Compound Assignment, Increment and Decrement Operators

The arithmetic compound assignment operators and the increment and decrement operators can be used to simplify program statements. For example, the three assignment statements in **Fig. 4.14** (lines 21, 24 and 28)

```text
passes = passes + 1;
failures = failures + 1;
studentCounter = studentCounter + 1;
```

can be written more concisely with compound assignment operators as

```text
passes += 1;
failures += 1;
studentCounter += 1;
```

with prefix increment operators as

```text
++passes;
++failures;
++studentCounter;
```

or with postfix increment operators as

```text
passes++;
failures++;
studentCounter++;
```

When incrementing or decrementing a variable in a statement by itself, the prefix increment and postfix increment forms have the *same* effect, and the prefix decrement and postfix decrement forms have the same effect. It's only when a variable appears in the context of a larger expression that preincrementing and postincrementing the variable have different effects (and similarly for predecrementing and postdecrementing).

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_485_0.png)

**Common Programming Error 4.4**

> Attempting to use the increment or decrement operator on an expression other than one to which a value can be assigned is a syntax error. For example, writing `++(x + 1)` is a syntax error, because `(x + 1)` is not a variable.

### Operator Precedence and Associativity

**Figure 4.18** shows the precedence and associativity of the operators introduced to this point. The operators are shown top-to-bottom in decreasing order of precedence. The second column indicates the associativity of the operators at each level of precedence. Notice that the conditional operator (`?:`), the unary operators preincrement (`++`), predecrement (`--`), plus (`+`) and minus (`-`), and the assignment operators (`=`, `+=`, `-=`, `*=`, `/=`, and `%=`) associate from *right to left*. All other operators in **Fig. 4.18** associate from *left to right*. The third column names the various groups of operators.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_485_1.png)

**Good Programming Practice 4.5**

> Refer to the operator precedence and associativity chart **Appendix A** when writing expressions containing many operators. Confirm that the operators in the expression are performed in the order you expect. If you're uncertain about the order of evaluation in a complex expression, break the expression into smaller statements or use parentheses to force the order of evaluation, exactly as you'd do in an algebraic expression. Be sure to observe that some operators such as assignment (`=`) associate right to left rather than left to right.

**Fig. 4.18 Operator precedence for the operators encountered so far in the text.**

| Operators | Associativity | Type |
|---|---|---|
| `::` `()` | left to right [*See Fig. 2.10's caution regarding grouping parentheses.*] | primary |
| `++` `--` `static_cast<type>` `()` | left to right | postfix |
| `++` `--` `+` `-` | right to left | unary (prefix) |
| `*` `/` `%` | left to right | multiplicative |
| `+` `-` | left to right | additive |
| `<<` `>>` | left to right | insertion/extraction |
| `<` `<=` `>` `>=` | left to right | relational |
| `==` `!=` | left to right | equality |
