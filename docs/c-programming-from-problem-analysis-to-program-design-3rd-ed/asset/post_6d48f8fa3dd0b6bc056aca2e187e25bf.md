
```csharp
case "MT": Console.WriteLine("Michigan");
break;
case "OK": Console.WriteLine("Oklahoma");
break;
case "TX": Console.WriteLine("Texas");
break;
default: Console.WriteLine("No match");
break;
}
}
}
}
```

When stateAbbrev has a value of NV, no error message is issued; Nevada is not printed either. Instead, No match is displayed on the console screen. Also, notice that Alabama is not displayed when stateAbbrev has a value of al. The case value must match the characters exactly; otherwise, the default option executes.

Multiple case values can be associated with the same statement(s), and it is not necessary to repeat the statement(s) for each value. When more than one case is associated with the same statement(s), you group common cases together and follow the last case value with the executable statement(s) to be performed when any of the previous cases match. In Example 5–21, it would be useful to display Alabama for AL, al, Al, and maybe aL. All four of the cases could be associated with the same executable statement that displays Alabama, as shown here:

```csharp
case "AL":
case "al":
case "Al":
case "aL": Console.WriteLine("Alabama");
    break;
```

You can place the executable statements for that group with the last case value. When you do this, you have effectively created a logical OR situation. In Example 5–22, the result of the expression is compared against 1, 2, 3, 4, and 5. If it matches any of those values, Failing Grade is written. Notice that the break statement is required as soon as a case includes an executable statement. No fall through is permitted if the previous case label has code.

### Example 5-22

```csharp
switch(examScore / 10)
{
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:  Console.WriteLine("Failing Grade");
        break;
    case 6:
    case 7:
    case 8:  Console.WriteLine("Passing Grade");
          break;
    case 9:
    case 10: Console.WriteLine("Superior Grade");
          break;
    default:  Console.WriteLine("Problem Grade");
          break;
}
```

The preceding `case` statement could be replaced with the following compound multiway `if` statement:

```csharp
if (((examScore / 10) == 1) || ((examScore / 10) == 2) ||
    ((examScore / 10) == 3) || ((examScore / 10) == 4) ||
    ((examScore / 10) == 5))
    Console.WriteLine("Failing Grade");
else if (((examScore / 10) == 6) || ((examScore / 10) == 7)
         || ((examScore / 10) == 8))
    Console.WriteLine("Passing Grade");
else if (((examScore / 10) == 9) || ((examScore / 10) == 10))
    Console.WriteLine("Superior Grade");
else Console.WriteLine("Problem Grade");
```

Which do you find the most readable? A solution for this problem could also be written using 10 separate one-way `if` statements. When an expression can be designed using the equality operator and involves more than three comparisons, the `switch` statement is almost always the best choice.

You cannot use the `switch` statement to test for a range of values. The only way to do this is to list every value using the `case` keyword. Also, the `case` value must be a constant literal; it cannot be a variable. The following code segment creates a syntax error:

```csharp
int score, high = 90;
switch (score)
{
    case high:    // Syntax error. Case value must be a constant.
```

You could write `case 90:`, but not `case high`.

![](img/e33ae760e23d89eac66541252ad65de8_300_0.png)

You must ensure that the expression type is the same as the `case` value type. For example, you can use a `char` variable as the selector. Each character literal value used as the `case` value must be enclosed in single quotation marks.

## TERNARY OPERATOR ? :

Also called the conditional operator, the ternary operator ? : provides another way to express a simple if...else selection statement. The operator consists of a question mark ? and a colon :. The general format for this conditional expression is:

```csharp
expression1 ? expression2 : expression3;
```

The ? : operator is the only ternary operator in C#. The expression that comes before the question mark, expression1, is evaluated first. When expression1 evaluates to true, expression2, following the question mark, is executed; otherwise expression3, following the colon, is executed.

An example of a statement using the conditional operator is as follows:

```csharp
grade = examScore > 89 ? 'A' : 'C';
```

This reads if examScore is greater than 89, assign A to grade; otherwise, assign C to grade. When examScore has a value of 75, the first expression, examScore > 89, evaluates to false; thus, expression3, C, following the colon is executed, and C is assigned to the grade memory location.

It performs the same operation as:

```csharp
if (examScore > 89)
    grade = 'A';
else
    grade = 'C';
```

![](img/e33ae760e23d89eac66541252ad65de8_301_0.png)

The conditional operator is often used in an assignment statement.

Consider Example 5-23.

### Example 5-23

Most service companies have a minimum charge they use for making house calls. Take, for example, a washing machine repairperson. He may charge $50.00 per hour; however, his minimum charge for traveling to your home is $100.00. Thus, when it takes him less than two hours, the charge is $100. A conditional expression to calculate the charges follows:

```csharp
double charges,
       timeAtSite = 3.5;
charges = timeAtSite < 2.0 ? 100.00 : timeAtSite * 50.00;
```

The value stored in `charges` would be 175. The first expression (`timeAtSite < 2.0`) evaluates to `false`; thus, the last expression (`timeAtSite * 50.00`) is evaluated and 175 is stored in `charges`.

![](img/e33ae760e23d89eac66541252ad65de8_302_0.png)

The ternary conditional operator is not as readable as the `if` statement. The `if` statement is used more often than other forms of the selection statement.

## Order of Operations

When an expression contains multiple operators, the **precedence of the operators** controls the order in which the individual operators are evaluated. For example, you saw in Chapter 2 that an expression such as `value1 + value2 * value3` is evaluated as `value1 + (value2 * value3)` because the `*` operator has higher precedence than the `+` operator.

Generally speaking, the precedence of operators follows the following order:

- 1. Unary operators
- 2. Binary operators
    - 1. Arithmetic operators (`* / %` in front of `+ -`)
    - 2. Relational operators (`< > <= >=` in front of `== !=`)
    - 3. Logical operators (`&&` in front of `||`)
- 3. Ternary operator (`? :`)
- 4. Assignment operators (`=, *= /= %= += -=`)

In Table 3–1, the operators used primarily for arithmetic were presented. Table 5–7 adds the operators presented in this chapter.

### Table 5-7 Operator precedence

| Category | Operator | Precedence |
|---|---|---|
| Unary | + - ! ~ ++ -- | Highest |
| Multiplicative | * / % |  |
| Additive | + - |  |
| Relational | < > <= >= |  |
| Equality | == != |  |
| Logical AND | & |  |
| Logical OR | \| |  |
| Conditional AND | && |  |
| Conditional OR | \|\| |  |
| Conditional | ? : |  |
| Assignment | = *= /= %= += -= | Lowest |

The operators listed in Table 5-7 appear from highest to lowest precedence. Except for the assignment operators, all binary operators are left-associative, meaning that operations are performed from left to right. For example, aValue + bValue - cValue is evaluated as (aValue + bValue) - cValue.

The assignment operators and the conditional operator ? : are right-associative, meaning that operations are performed from right to left. For example, firstValue = secondValue = thirdValue is evaluated as firstValue = (secondValue = thirdValue). Precedence and associativity can be controlled using parentheses. It is not necessary to include the parentheses in the previous example because the order of operations of the language determines the order. Parentheses can certainly be added to increase readability, but they are not necessary.

Example 5-24 includes an example of a selection statement using many of the operators presented in this chapter. The actual order in which the operations are performed is given following the declaration and conditional expression.

### Example 5-24

```csharp
int value1 = 10, value2 = 20, value3 = 30, value4 = 40, value5 = 50;
if (value1 > value2 || value3 == 10 && value4 + 5 < value5)
    Console.WriteLine("The expression evaluates to true");
```

The preceding expression is evaluated in the following order:

- 1. (value4 + 5) → (40 + 5) → 45
- 2. (value1 > value2) → (10 > 20) → false
