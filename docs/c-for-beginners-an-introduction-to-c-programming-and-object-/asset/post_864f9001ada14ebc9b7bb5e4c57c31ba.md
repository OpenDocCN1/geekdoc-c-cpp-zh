
```cpp
    return ;
}
```

![](img/cda5b023e23ffd0b87fc37b1da33973d_52_0.png)

*Note:* The `cin >>` statement can read all primitive data types without a problem. It can also read strings in some cases. However, it cannot be used to read strings with spaces. If a string with spaces is entered, each value after the space is going to be treated as a new input and each new input will go to the next variable if available. If no more variables are present, those values after the space will be just discarded. This shortfall of `cin >>` statement can lead to data type mismatch and can cause the program to behave differently. Let us execute the same program and demonstrate.

Instead of entering *Matthew (first name)* and *Johnson (last name)* as two different inputs, I will place them on a single line separated by a space. The output shows that the program behaves totally fine and *Matthew* and *Johnson* are fetched as *first name* and *last_name* correctly:

![](img/cda5b023e23ffd0b87fc37b1da33973d_53_0.png)

Now, let us do another run and try to introduce a space in the *address* variable. Instead of *Ottawa*, let us enter *New York*. Theoretically, “*New*” should go to the *address* variable and “*York*” will be treated as another input as there is a space after “*New*”. After reading address, we ask the user to enter age and weight. The program will try to extract “*York*” in the age variable which is of *integer* type. This will lead to a data mismatch situation and will cause the program to lose stability. Here is the output:

## 7. Operators

An operator in a programming language is a symbol that performs a specific task. Operators in C++ are used to perform mathematical, logical or comparison operations. The following types of operators are available:

- 1. Arithmetic Operators
- 2. Logical Operators
- 3. Bitwise Operators
- 4. Relational Operators
- 5. Assignment Operators

### 7.1 Arithmetic Operators

Arithmetic operators are used to perform arithmetic/mathematical operations such as addition, subtraction, division, etc.

| Operator | Description | Sample Usage | Explanation |
|---|---|---|---|
| + | Addition | a + b | Performs arithmetic addition, returns sum of the operands. |
| - | Subtraction | a - b | Performs arithmetic subtraction, returns difference of the operands. |
| * | Multiplication | a * b | Multiplies operands and returns the arithmetic product. |
| / | Division | a / b | Performs division and returns the arithmetic quotient. |
| % | Modulus | a % b | Performs division and returns the remainder. Usage is restricted to integer type operands only. |
| ++ | Increment | a ++ | Increments the value of an operand by 1. Two variations: Post increment (a ++) and Pre increment (++ a). This operator works only on integer variables. |
| -- | Decrement | a -- | Decrements the value of an operand by 1. Two variations: Post decrement (a --) and Pre decrement (-- a). This operator works only on integer variables. |

Note: Integer by Integer division will result in the quotient being an integer even if the arithmetic value of the quotient should be fractional. For example, the quotient resulting from this division - 5 / 2 will be 2 and not 2.5. To solve this, a float factor must be introduced. You can multiply 1.0 to either the numerator or the denominator. The expression 5 / 2 will now become 5 * 1.0 / 2 or 5 / 2 * 1.0. You can even use brackets just as you would in mathematics for convenience or when you want to carry out an operation first among an expression - 5 / (2 * 1.0).

```cpp
eg:
int x = 15, y = 4;
float quotient = (x * 1.0) / y;
```

### 7.2 Logical Operators

Logical operators are used to carry out logical AND, OR and NOT. These return 0 or 1. 0 (and negative numbers) is regarded as false, and 1 (and all positive numbers) is regarded as true.

| Operator | Description | Sample Usage | Explanation |
|---|---|---|---|
| && | Logical AND | a && b | Compares operands and returns 1 if all the values are non-zero, returns 0 otherwise. |
| \|\| | Logical OR | a \|\| b | Compares operands and returns 1 if any one of the values is non-zero, returns 0 otherwise. |
| ! | Logical NOT | !a | Returns inverted value of the operand. If the operand has a true value (non-zero), 0 will be returned and if the operand has false value (0 or negative), 1 will be returned. |

### 7.3 Bitwise Operators

Bitwise operators are used to perform bit-by-bit logical operation. That is, operations are carried out on each bit of the operands.

| Operator | Description | Sample Usage | Explanation |
|---|---|---|---|
| `&` | Bitwise Logical AND | `a & b` | Performs logical AND on each of the operands on a bit-by-bit basis. |
| `\|` | Bitwise Logical OR | `a \| b` | Performs logical OR on each of the operands on a bit-by-bit basis. |
| `~` | Bitwise Logical Inverter | `~a` | Inverts each bit of the operand. |
| `^` | Bitwise Logical XOR | `a ^ b` | Performs logical XOR on each of the operands on a bit-by-bit basis. |
| `<<` | Left Shift | `a << b` | Left shifts bits of the operand on the left by a number specified by the right operand. From *Sample Usage*, `a << b` will result in a’s bits left shifted b times. |
| `>>` | Right Shift | `a >> b` | Right shifts bits of the operand on the left by a number specified by the right operand. From *Sample Usage*, `a >> b` will result in a’s bits right shifted b times. |

```cpp
<operand 1> = <operand 2>
eg:
a = 70;
b = a * 2;
c = b;
```

Assignment operator, assigns the value of the operand on the right to the operand on the left. Operand on the left side of the assignment operator has to be a variable. Operand on the right side of the assignment operator can be a constant, variable or an expression. In case of an expression, it will be evaluated first and then the value will be assigned except when a post-increment operator is used as demonstrated in the code snippet below:

```cpp
int a, b, c = 100 ;
a = c * 100 ;
b = c++;
```

Before assigning a value to variable *a*, the expression *c * 100* will be evaluated first. Hence the variable *a* will now hold a value of *10000*. Whereas, the value of *c* will be assigned to variable *b* first and then *c* will be incremented. Hence variable *b* will now hold *100* and variable *c* will now hold *101*. If you want to increment first and then assign, pre-increment operator needs to be used: *b = ++c*.

#### 7.5.1 Compound Assignment Operators

Compound Assignment Operators are used to perform mathematical operations on operands first and then assign.

| Operator | Description | Sample Usage | Equivalent To |
| :---: | :--- | :---: | :---: |
| += | Perform arithmetic addition, then assign | a += b | a = a + b |
| -= | Perform arithmetic subtraction, then assign | a -= b | a = a - b |
| *= | Perform arithmetic multiplication, then assign | a *= b | a = a * b |
| /= | Perform arithmetic division, then assign | a /= b | a = a / b |
| %= | Calculate modulus, then assign | a %= b | a = a % b |
| &= | Perform Bitwise Logical AND, then assign | a &= b | a = a & b |
| \|= | Perform Bitwise Logical OR, then assign | a \|= b | a = a \| b |
| ^= | Perform Bitwise Logical XOR, then assign | a ^= b | a = a ^ b |
| <<= | Perform left shift, then assign | a <<= b | a = a << b |
| >>= | Perform right shift, then assign | a >>= b | a = a >> b |

To understand the working of bitwise operators, some knowledge of *Boolean Algebra* and *Binary Number System* is needed. For now, let us see how to represent an integer in a binary form. The *bitset* header provides an object called *bitset* (part of *std namespace*) which is used to work with binary representations. Usage of *bitset* will need **#include <bitset>** in your program. Syntax for representing an integer in binary form:

```cpp
bitset<number of bits>
(variable/constant/expression)
eg:
int a = 4;
```
