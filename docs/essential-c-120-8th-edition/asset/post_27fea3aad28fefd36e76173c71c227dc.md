
## Chapter 4: Operators and Control Flow

In mathematics, certain mathematical operations are undefined, including dividing zero by itself. In C#, the result of dividing the float by zero results in a special Not A (NaN) value; all attempts to print the output of such a number will result in NaN. Similarly, the square root of a negative number with System.Sqrt(-1) will result in NaN.

A floating-point number could overflow its bounds as well. For example, the upper bound of the float type is approximately $3.4 \times 10^{38}$. Should the number overflow that bound, the result would be stored as **positive infinity**, and the output of printing the number would be Infinity. Similarly, the lower bound of a float type is $-3.4 \times 10^{38}$, and computing a value below that bound would result in **negative infinity**, which would be represented by the string -Infinity. Listing 4.9 produces negative and positive infinity, respectively, and Output 4.8 shows the results.

### Listing 4.9: Overflowing the Bounds of a float

```csharp
// Displays: -Infinity
Console.WriteLine(-1f / 0);
// Displays: Infinity
Console.WriteLine(3.402823E+38f * 2f);
```

### OUTPUT 4.8

```
-Infinity
Infinity
```

Further examination of the floating-point number reveals that it can contain a value close to zero without actually containing zero. If the value exceeds the lower threshold for the float or double type, the value of the number can be represented as **negative zero** or **positive zero**, depending on whether the number is negative or positive, and is represented in output as -0 or 0.

## Compound Mathematical Assignment Operators (+=, -=, *=, /=, %)

Chapter 1 discussed the simple assignment operator, which places the value of the right-hand side of the operator into the variable on the left-hand side. Compound mathematical assignment operators combine common binary operator calculations with the assignment operator. For example, consider Listing 4.10.

### Listing 4.10: Common Increment Calculation

```csharp
int x = 123;
x = x + 2;
```

In this assignment, first you calculate the value of x + 2, and then you assign the calculated value back to x. Since this type of operation is performed relatively frequently, an assignment operator exists to handle both the calculation and the assignment with one operator. The += operator increments the variable on the left-hand side of the operator with the value on the right-hand side of the operator, as shown in Listing 4.11.

### Listing 4.11: Using the += Operator

```csharp
int x = 123;
x += 2;
```

This code, therefore, is equivalent to Listing 4.10.
Numerous other compound assignment operators exist to provide similar functionality. You can also use the assignment operator with subtraction, multiplication, and remainder operators (as demonstrated in Listing 4.12).

### Listing 4.12: Other Assignment Operator

```csharp
x -= 2;
x /= 2;
x *= 2;
x %= 2;
```

## Increment and Decrement Operators (++, --)

C# includes unary operators for incrementing and decrementing. The increment operator, ++ increments a variable by one each time it is used. In other words, all of the code lines shown in Listing 4.13 are equivalent.

### Listing 4.13: Increment Operator

```csharp
spaceCount = spaceCount + 1;
spaceCount += 1;
spaceCount++;
```

Similarly, you can decrement a variable by 1 using the decrement operator, --. Therefore, all of the code lines shown in Listing 4.14 are equivalent.

### Listing 4.14: Decrement Operator

```csharp
lines = lines - 1;
lines--;
```

##```NERNERNERIC

: A Decrement Example in a Loop

The increment and decrement operators are especially prevalent in loops, such as the while loop described later in the chapter. For example, Listing 4.15 with Output 4.9 uses the decrement operator to iterate backward through each letter in the alphabet.

### Listing 4.15: Displaying Each Character's Unicode Value in Descending Order

```csharp
char current;
int unicodeValue;

// Set the initial value of current
current = 'z';

do {
  // Retrieve the Unicode value of current
  unicodeValue = current;
  Console.Write($"{current}={unicodeValue}\t");
  // Proceed to the previous letter in the alphabet
  current--;
} while(current >= 'a');
```

### Output 4.9

| Character | Unicode |
| :--- | :--- |
| z | 122 |
| y | 121 |
| w | 120 |
| v | 119 |
| u | 118 |
| t | 117 |
| s | 116 |
| r | 115 |
| q | 114 |
| p | 113 |
| o | 112 |
| n | 111 |
| m | 110 |
| l | 109 |
| k | 108 |
| j | 107 |
| i | 105 |
| h | 104 |
| g | 103 |
| f | 102 |
| e | 101 |
| d | 100 |
| c | 99 |
| b | 98 |
| a | 97 |

The increment and decrement operators many times a particular operation is performed. In this example, notice that the decrement operator acts on (char) data type. You can use increment and decrement operators on various types given some meaning to the concept of "next" or "previous" value for that data type. We saw that the assignment operator first computes the value and performs the assignment. The result of the assignment operator is the value that was assigned. The increment and decrement operators are similar: They compute the value, perform the assignment, and return a value. It is therefore possible to use the assignment operator with the increment or decrement operator, doing so carefully can be extremely confusing. See Listing 4.16 and Output 4.10 for an example.

### Listing 4.16: Using Post-increment Operator

```csharp
int count = 123;
int result;
result = count++;
Console.WriteLine($"{result} and {count}");
```

You might be surprised that result was assigned the value that was count before incremented. Where you place the increment or decrement operator determines whether the assigned value should be the value of the operand before or after the calculation. If you want the value of result to be the value assigned to count, you need to place the operator before the variable being incremented, as shown in Listing 4.17 with Output 4.11.

### Listing 4.17: Using Pre-increment Operator

```csharp
int count = 123;
int result;
result = ++count;
Console.WriteLine($"{result} and {count}");
```

### OUTPUT 4.10

```
result = 123 and count = 124
```

In this example, the increment operator appears before the operand, so the result of the expression is the value assigned to the variable after the increment. If count is 123, ++count assigns 124 to count and produces the result 124. By contrast, the postfix increment operator count++ assigns 124 to count and produces the value that count held before the increment: 123. Regardless of whether the operator is postfix or prefix, the variable count is incremented before the value is produced; the only difference is which value is produced. The difference between prefix and postfix behavior is illustrated in Listing 4.18. The resultant output is shown in Output 4.12.

### Listing 4.18: Comparing the Prefix and Postfix Increment Operators

```csharp
public class IncrementExample {
  public static void Main() {
    int x = 123;
    // Displays 123, 124, 125
    Console.WriteLine($"{x++}, {x++}, {x}");
    // x now contains the value 125

    // Displays 126, 127, 127
    Console.WriteLine("{++x}, {x}, {x}");
    // x now contains the value 127
  }
}
```

### OUTPUT 4.12

```
123, 124, 125
126, 127, 127
```

As Listing 4.18 demonstrates, where the increment and decrement operators appear relative to the operand can affect the result produced by the expression. The result of the prefix operators is the value that the variable had before incrementing or decrementing. The result of the postfix operators is the value that the variable had after incrementing or decrementing. Use caution when embedding these operators in the middle of a statement. When doing as to what will happen, use these operators independently, placing them within their own statements. This way, the code is also more readable and there is no mistake the intention.

## Language Contrast: C++—Implementation-Defined Behavior

Earlier we discussed how the operands in an expression can be evaluated in any order in C#, whereas they are evaluated from left to right in C#. Similarly, in C++ an implementation may legally perform the side effects of increments and decrements in any order. For example, in C++ a call of M(x++, x++), where x begins as 1, can legally call M(1,2) or M(2,1) of the compiler. In contrast, C# always calls M(1,2) because C# computes the arguments to a call from left to right, and (2) the assignment of the incremented value to the variable always happens before the value of the expression is used. C++ makes neither guarantee.

## Guidelines

AVOID confusing usage of the increment and decrement operators.
