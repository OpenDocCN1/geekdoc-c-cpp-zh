
example, when performing a Celsius-to-Fahrenheit temperature conversion, (c*9.0/5.0)+32.0 is easier to read than c*9.0/5.0+32.0, even though the parentheses are completely unnecessary.

# Guidelines

DO use parentheses to make code more readable, particularly if the operator precedence is not clear to the casual reader.

Clearly, operators of higher precedence must execute before adjoining operators of lower precedence: in x+y*z, the multiplication must be executed before the addition because the result of the multiplication is the right-hand operand of the addition. However, it is important to realize that precedence and associativity affect only the order in which the operators themselves are executed; they do not in any way affect the order in which the operands are evaluated.

Operands are always evaluated from left to right in C#. In an expression with three calls, such as A()+B()*C(), first A() is evaluated, then B(), then C(); then the multiplication operator determines the product; and finally the addition operator determines the sum. Just because C() is involved in a multiplication and A() is involved in a lower-precedence addition, does not imply that method invocation C() happens before method invocation A().

# Language Contrast: C++ Evaluation Order of Operands

In contrast to the rule mentioned here, the C++ specification allows implementation broad latitude to decide the evaluation order of operands. When given an expression such as A()+B()*C(), a C++ compiler can choose to evaluate the functions in any order, as long as the product is one of the summands. For example, a legal compiler could evaluate B(), then A(), then C(); then the product; and finally the sum.

# Using the Addition Operator with Strings

Operators can also work with non-numeric operands. For example, it is possible to use the addition operator to concatenate two or more strings, as shown in Listing 4.4 with Output 4.3.

Listing 4.4: Using Binary Operators with Non-numeric Types

```
public class FortyTwo {
    public static void Main() {
        short windSpeed = 42;
        Console.WriteLine("The original Tacoma Bridge in Washington" + Environment.NewLine + \
        " brought down by a " \
        windSpeed + " mile/hour wind.");
    }
}
```

OUTPUT 4.3

| The original Tacoma Bridge in Washington was brought down by a 42 mile/hour wind. |

Because sentence structure varies among different languages in different cultures, developers should be careful not to use the addition operator with strings that possibly will require localization. Similarly, although we can embed expressions within a string using string interpolation, localization to other languages still requires moving the string to a resource file, neutralizing the string interpolation. For this reason, you should use the addition operator sparsely, favoring composite formatting when localization is a possibility.

# Guidelines

DO favor composite formatting over use of the addition operator for concatenating strings when localization is a possibility.

# Using Characters in Arithmetic Operations

When introducing the char type in Chapter 2, we mentioned that even though it stores characters and numbers, the char type is an integral type (integral means it is based on an integer). It can participate in arithmetic operations with other types. However, interpretation of the value of char type is not based on the character stored within it but rather its underlying value. The digit 3, for example, is represented by the Unicode value 0x33 (hexadecimal), which in base 10 is 5. The digit 4 is represented by the Unicode value 0x34, or 4 in base 10. Adding 3 and 4 in Listing 4.5 results in a hexadecimal value of 0x37, or 7 in base 10, which is the Unicode value for g, as shown in Output 4.4.

LISTING 4.5: Using the Plus Operator with char Type

```
int n = '3' + '4';
char c = (char)n;
Console.WriteLine(c); // g
```

OUTPUT 4.4

g

You can use this trait of character types to determine how far two characters are from each other. For example, the letter f is three away from the letter c. You can determine this value by subtracting the letter c from the letter f, as Listing 4.6 with Output 4.5 demonstrates.

LISTING 4.6: Determining the Character Difference between Two Characters

```
int distance = 'f' - 'c';
Console.WriteLine(distance);
```

OUTPUT 4.5

3

# Special Floating-Point Characteristics

The binary floating-point types, float and double, have some special characteristics, such as the way they manage precision. This section looks at some examples, as well as some unique floating-point characteristics.

A float, with seven digits of precision, can hold the value 1.234567 and the value 0.1234567. However, if you add these two floats together, the result will be rounded to 1.234567 because the exact result requires more precision than the seven digits a float can hold. The error introduced by rounding off seven digits can become large, especially with repeated calculations. (See also “Advanced Topic: Unexpected Inequality with Floating-Point Types” later in this section.)

Internally, the binary floating-point types store a binary fraction, not a decimal fraction. Consequently, “representation error” can occur with a simple assignment, such as double = 14.6. The exact value of 140.6 is the fraction 703/5, but the denominator of that fraction is not a power of 2, so a binary floating-point number cannot represent it. Instead, the value represented is the closest fraction with a power of 2 that fits into the 32 bits of float.

Since the double can hold a more accurate value than the float can store, the C# compiler actually evaluates this expression to double = 14.600000103516 because 14.600000103516 is the closest binary fraction to 14.6 as a float. This fraction is slightly larger than 14.6 as represented as a double.

# Guidelines

AVOID binary floating-point types when exact decimal arithmetic is required; use the decimal floating-point type instead.

# Chapter 4: Operators and Control Flow

# ADVANCED TOPIC

Unexpected Inequality with Floating-Point Types

Because floating-point numbers can be unexpectedly rounded off to non-decimal fractions, comparing floating-point values for equality can be quite confusing. Consider Listing 4.7 with Output 4.6.

LISTING 4.7: Unexpected Inequality Due to Floating-Point Inaccuracies

```
decimal decimalNumber = 4.2M;
double doubleNumber1 = 0.1F * 42F;
double doubleNumber2 = 0.1D * 42D;
float floatNumber = 0.1F * 42F;

// 1. Displays: 4.2 != 4.2000002861023
Console.WriteLine(
  "${decimalNumber} != {doubleNumber1}");

// 2. Displays: 4.2 != 4.20000028610295
Console.WriteLine(
  "${decimalNumber} != {doubleNumber1}");

// 3. Displays: (float)4.2M != 4.2000003F
Console.WriteLine(
  "${decimalNumber}M != {floatNumber}F");

// 4. Displays: 4.20000028610295 != 4.2
Console.WriteLine(
  "${doubleNumber1} != {doubleNumber2}");

// 5. Displays: 4.2000003F != 4.2D
Console.WriteLine(
  "${floatNumber}F != {doubleNumber2}D}");

// 6. Displays: 4.19999980929265137 != 4.2
Console.WriteLine(
  "${4.2F} != {4.2D}");

// 7. Displays: 4.2F != 4.2D
Console.WriteLine(
  "${4.2F}F != {4.2D}");
```

# OUTPUT 4.6

```
4.2 != 4.2000002861023
4.2 != 4.20000028610295
(float)4.2M != 4.2000003F
4.20000028610295 != 4.2
4.2000003F != 4.2D
4.19999980929265137 != 4.2
4.2F != 4.2D
```
