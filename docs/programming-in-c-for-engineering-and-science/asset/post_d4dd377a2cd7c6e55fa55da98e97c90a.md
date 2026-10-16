
- iii. Compute energy from mass.
- iv. Output a numeric value (energy) and a string (descriptive label) on the screen.

C++ provides operations for each of these operations except for the third one. For this we must use Einstein’s familiar equation

e = m × c²

where m is the mass, c is the speed-of-light constant, and e is the energy produced. Performing this operation thus requires the following operations:

- Exponentiation (c²)
- Multiplication of reals (m × c²)
- Storage of a real (e = m × c²)

This refinement adds two additional objects to our object list:

| Problem Objects | Type | Kind | C++ Identifier |
|---|---|---|---|
| Software Objects |  |  |  |
| screen | output device | variable | cout |
| prompt | text string | constant | none |
| quantity of matter | double | variable | mass |
| keyboard | input device | variable | cin |
| quantity of energy | double | variable | energy |
| descriptive label | string | constant | none |
| speed of light | double | constant | SPEED_OF_LIGHT |
| 2 | int | constant | none |

### 4.1.2.4 Algorithm

Next, we organize these objects and operations into an algorithm:

- 1. Define the constant SPEED_OF_LIGHT.
- 2. Display to cout a prompt for the mass.
- 3. Read a non-negative real number from cin into mass.
- 4. Compute energy = mass × SPEED_OF_LIGHT².
- 5. Output to cout a descriptive label and energy.

### 4.1.2.5 Coding, Execution, and Testing

The program in Example 4.1 implements the preceding algorithm. Two of the sample runs use test data for which the output can be easily checked and the third uses “real” data.

### Example 4.1 Mass-to-Energy Conversion

```
/* This program computes energy from a given mass using Einstein's mass-to-energy conversion equation.

Input: the mass (in kilograms) being converted to energy
Output: the amount of energy (in kilojoules) corresponding to mass
--------------------------------------------------------------------------*/

#include <iostream>      // cin, cout, <<, >>
#include <cmath>         // pow()
using namespace std;

int main()
{
    const double SPEED_OF_LIGHT = 2.997925e8; // meters/sec

    double mass;
    cout << "To find the amount of energy obtained from a given mass,\n" 
         "enter a mass (in kilograms): ";
    cin >> mass;            // get mass

                        // compute energy
    double energy = mass * pow(SPEED_OF_LIGHT, 2);

                        // display energy
    cout << mass << " kilograms of matter will release\n"
         << energy << " kilojoules of energy.\n";
}
```

### SAMPLE RUNS:

```
To find the amount of energy obtained from a given mass,
enter a mass (in kilograms): 1
1 kilograms of matter will release
8.98755e+16 kilojoules of energy.

To find the amount of energy obtained from a given mass,
enter a mass (in kilograms): .5
0.5 kilograms of matter will release
4.49378e+16 kilojoules of energy.

To find the amount of energy obtained from a given mass,
enter a mass (in kilograms): 155.5
155.5 kilograms of matter will release
1.39756e+19 kilojoules of energy.
```

Any fractional parts are dropped and the resulting integer is the result; no rounding occurs. In the other expressions involving division, at least one of the operands is real, so real division is performed, producing the real result 2.25. A common difficulty for beginning programmers is to remember that the value of m/n is 0 if m and n are integers with |m| < |n|; for example, each of 1/2, 1/3, 9/10, −99/100 produces the value 0.

In the case of integer division, C++ provides one operator (/) that gives the integer quotient and another operator (%) that gives the remainder from an integer division.² The following are some examples:

```
6 / 4 → 1      6 % 4 → 2
83 / 10 → 8     83 % 10 → 3
148 / 10 → 14   148 % 10 → 8
```

For real values, / performs real division and produces a real quotient whose precision is machine dependent. The % operator cannot be used with real values.

### 4.2.1.1 Operator Priority

The order in which operators in an expression are applied is determined by a characteristic known as operator priority (or precedence). For the arithmetic operators, *, / and % have higher priority than + and −.

Operators with higher priority are applied before those with lower priority. For example, in the expression 3 + 4 * 5, the multiplication is performed before the addition because * has higher priority than +, so the value of this expression is 23. Appendix C gives the precedence levels for all of the C++ operators.

### 4.2.1.2 Operator Associativity

The operators +, −, *, /, and % are all said to be left-associative, which means that in an expression having two operators with the same priority, the left operator is applied first. Thus,

```
9 - 4 - 3
```

is evaluated as

```
(9 - 4) - 3 → 5 - 3 → 2
```

In a later section, we will see that some C++ operators are right-associative.

Associativity is also used in more complex expressions containing different operators of the same priority. For example, consider

```
9 * 10 - 8 % 3 * 4 + 5
```

Now the division is performed, giving

```
1 + 9
```

and the addition produces the final result

```
10
```

Even though parentheses may not be required, they should be used freely in expressions containing several operations to make the intended order of evaluation clear and to write complicated expressions in terms of simpler expressions. Be sure, however, that the parentheses balance—each left parenthesis has a matching right parenthesis later in the expression—or a compilation error will result.

### 4.2.1.4 Unary Operators

When + and − are used as **unary operators** (i.e., applied to a single operand) as in −x + 5 and −2 * x, they have higher priority than the corresponding binary operations. Thus, if the value of x is −1, the values of these expressions will be 6 and 2, respectively.

### 4.2.1.5 Summary

The following rules summarize the evaluation of arithmetic expressions.

### OPERATOR PRIORITIES

Higher: unary +, unary -

*, /, %

Lower: binary +, binary -

- 1. Higher-priority operations are performed before lower-priority ones.
- 2. Operators with the same priority are applied left to right if they are left-associative and right to left if they are right-associative.
- 3. If an expression contains parenthesized subexpressions, they are evaluated first, using the order specified in rules 1 and 2. For nested parentheses, the innermost subexpressions are evaluated first.

### 4.2.1.6 Bitwise Operators

C++ also provides operations that can be used to manipulate the individual bits in the stored binary representations of integers: ~ (negation), & (bitwise and), | (bitwise or), ^ (bitwise exclusive or), << (bitshift left), and >> (bitshift right). They are sometimes used in low-level graphics or operating system programs that must check memory or interact directly with a computer’s hardware. More information about these operations can be found on the text’s website described in the Preface.

### 4.2.2 Type Coercion

As noted earlier, in the mixed-type expression 6.0 / 4 that involves both integer and real operands, C++ performs real division and produces the real value 1.5. This is because the compiler automatically converts the integer value 4 to a real value 4.0, and then performs the real division operation 6.0 / 4.0. This automatic type conversion by the compiler is known as type coercion. It also occurs in mixed-type expressions involving characters and integers or reals; the character values are automatically replaced by their numeric codes (see Section 3.3). For example, if characters are represented in ASCII, the value of the expression 'a' + 3 is 100 because 'a' is replaced by 97, its numeric code.

In general, these type conversions take place automatically in any mixed-type expression with “narrow” values—those stored in a smaller number of bits—being converted to “wider” values that occupy a larger number of bits. This automatic widening of a narrower value to the size of a wider value in an expression is known as promotion of the narrower value. It is what permits character, integer, and real values to be freely intermixed in C++ expressions. Two values are said to be compatible if (i) they have the same type, (ii) one can be promoted to the type of the other, or (iii) both can be promoted to the same type. For example, int and double are compatible, because int can be promoted to double.

### 4.2.2.1 Explicit Type Conversions

In addition to automatic type conversions, explicit conversions are also possible. For example, if intVal is an integer value, then either of the expressions double(intVal) or (double)intVal produces the double value equivalent to intVal. Similarly, if doubleVal is of type double, either of int(doubleVal) or (int)doubleVal will truncate the fractional part of doubleVal and produce its integer part.

In general, an expression of the form

```
type(expression)
```

or

```
(type)expression
```

where type is a valid C++ type can be used to convert the type of expression to type (if possible). The first form is sometimes referred to as functional notation and the last form as (C-style) cast notation.

### 4.3 ASSIGNMENT EXPRESSIONS

An assignment expression uses the assignment operator (=) to assign a value to a variable.

### ASSIGNMENT EXPRESSION

**Form:**

```
variable = expression
```
