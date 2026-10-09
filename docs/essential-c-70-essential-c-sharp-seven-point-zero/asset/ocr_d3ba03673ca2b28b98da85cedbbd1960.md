# TABLE 4.3: Conditional Values for the XOR Operator

| Left Operand | Right Operand | Result |
| :--- | :--- | :--- |
| True | True | False |
| True | False | True |
| False | True | True |
| False | False | False |

Unlike the Boolean AND and Boolean OR operators, the Boolean XOR operator does not short-circuit: It always checks both operands, because the result cannot be determined unless the values of both operands are known. Note that the XOR operator is exactly the same as the Boolean inequality operator.

# Logical Negation Operator (!)

The **logical negation operator**, or **NOT operator**, !, inverts a `bool` value. This operator is a unary operator, meaning it requires only one operand. Listing 4.34 demonstrates how it works, and Output 4.16 shows the result.

# LISTING 4.34: Using the Logical Negation Operator

```
```
 bool valid = false;
 bool result = !valid;
 // Displays "result = True"
 System.Console.WriteLine($"result = { result }");
```
```

# OUTPUT 4.16

```
```
 result = True
```
```

At the beginning of Listing 4.34, `valid` is set to `false`. You then use the negation operator on `valid` and assign the value to `result`.