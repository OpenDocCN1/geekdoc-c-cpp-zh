
| expression1 | expression2 | expression1 ^ expression2 |
|---|---|---|
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | false |

**Fig. 6.17** | ^ (boolean logical exclusive OR) operator truth table.

### 6.10.6 Logical Negation (!) Operator

The ! (logical negation or not) operator enables you to "reverse" the meaning of a condition. Unlike the logical operators &&, ||, & and ^, which are *binary* operators that combine two conditions, the logical negation operator is a *unary* operator that has only a single condition as an operand. The logical negation operator is placed before a condition to choose a path of execution if the original condition (without the logical negation operator) is false, as in the code segment

```csharp
if (!(grade == sentinelValue))
{
   Console.WriteLine($"The next grade is {grade}");
}
```

which executes the *WriteLine* call only if grade is not equal to `sentinelValue`. The parentheses around the condition `grade == sentinelValue` are needed because the logical negation operator has a higher precedence than the equality operator.

In most cases, you can avoid using logical negation by expressing the condition differently with an appropriate relational or equality operator. For example, the previous statement may also be written as

```csharp
if (grade != sentinelValue)
{
   Console.WriteLine($"The next grade is {grade}");
}
```

This flexibility can help you express a condition in a more convenient manner. Figure 6.18 is a truth table for the logical negation operator.

| expression | !expression |
|---|---|
| false | true |
| true | false |

**Fig. 6.18** | ! (logical negation) operator truth table.

### 6.10.7 Logical Operators Example

Figure 6.19 demonstrates the logical operators and boolean logical operators by producing their truth tables. The output shows the expression that was evaluated and the *bool* result of that expression. Lines 10–14 produce the truth table for && (conditional AND). Lines 17–21 produce the truth table for || (conditional OR). Lines 24–28 produce the truth table for & (boolean logical AND). Lines 31–35 produce the truth table for | (boolean logical inclusive OR). Lines 38–42 produce the truth table for ^ (boolean logical exclusive OR). Lines 45–47 produce the truth table for ! (logical negation).

```csharp
// Fig. 6.19: LogicalOperators.cs
// Logical operators.
using System;

class LogicalOperators
{
    static void Main()
    {
        // create truth table for && (conditional AND) operator
        Console.WriteLine("Conditional AND (&&)");
        Console.WriteLine($"false && false: {false && false}");
        Console.WriteLine($"false && true: {false && true}");
        Console.WriteLine($"true && false: {true && false}");
        Console.WriteLine($"true && true: {true && true}\n");

        // create truth table for || (conditional OR) operator
        Console.WriteLine("Conditional OR (||)");
        Console.WriteLine($"false || false: {false || false}");
        Console.WriteLine($"false || true: {false || true}");
        Console.WriteLine($"true || false: {true || false}");
        Console.WriteLine($"true || true: {true || true}\n");

        // create truth table for & (boolean logical AND) operator
        Console.WriteLine("Boolean logical AND (&)");
        Console.WriteLine($"false & false: {false & false}");
        Console.WriteLine($"false & true: {false & true}");
        Console.WriteLine($"true & false: {true & false}");
        Console.WriteLine($"true & true: {true & true}\n");

        // create truth table for | (boolean logical inclusive OR) operator
        Console.WriteLine("Boolean logical inclusive OR (|)");
        Console.WriteLine($"false | false: {false | false}");
        Console.WriteLine($"false | true: {false | true}");
        Console.WriteLine($"true | false: {true | false}");
        Console.WriteLine($"true | true: {true | true}\n");

        // create truth table for ^ (boolean logical exclusive OR) operator
        Console.WriteLine("Boolean logical exclusive OR (^)");
        Console.WriteLine($"false ^ false: {false ^ false}");
        Console.WriteLine($"false ^ true: {false ^ true}");
        Console.WriteLine($"true ^ false: {true ^ false}");
        Console.WriteLine($"true ^ true: {true ^ true}\n");

44  // create truth table for ! (logical negation) operator
45  Console.WriteLine("Logical negation (!)");
46  Console.WriteLine($"!false: {!false}");
47  Console.WriteLine($"!true: {!true}");
48  }
49  }
```

```text
Conditional AND (&&)
false && false: False
false && true: False
true && false: False
true && true: True

Conditional OR (||)
false || false: False
false || true: True
true || false: True
true || true: True

Boolean logical AND (&)
false & false: False
false & true: False
true & false: False
true & true: True

Boolean logical inclusive OR (|)
false | false: False
false | true: True
true | false: True
true | true: True

Boolean logical exclusive OR (^)
false ^ false: False
false ^ true: True
true ^ false: True
true ^ true: False

Logical negation (!)
!false: True
!true: False
```

Fig. 6.19 | Logical operators.

### Precedence and Associativity of the Operators Presented So Far

Figure 6.20 shows the precedence and associativity of the C# operators introduced so far. The operators are shown from top to bottom in decreasing order of precedence.

| Operators | Associativity | Type |
|---|---|---|
| . new ++(postfix) --(postfix) | left to right | highest precedence |
| ++ -- + - ! (type) | right to left | unary prefix |
| * / % | left to right | multiplicative |
| +  - | left to right | additive |
| <  <=  >  >= | left to right | relational |
| ==  != | left to right | equality |
| & | left to right | boolean logical AND |
| ^ | left to right | boolean logical exclusive OR |
| \| | left to right | boolean logical inclusive OR |
| && | left to right | conditional AND |
| \|\| | left to right | conditional OR |
| ?: | right to left | conditional |
| =  +=  -=  *=  /=  %= | right to left | assignment |

**Fig. 6.20** | Precedence/associativity of the operators discussed so far.

## 6.11 Wrap-Up

Chapter 5 discussed the `if`, `if…else` and `while` control statements. In Chapter 6, we discussed the `for`, `do…while` and `switch` control statements—we’ll discuss the `foreach` statement in Chapter 8. The `for` and `do…while` statements are simply more convenient ways to express certain types of iteration. The `switch` statement is in some situations a more convenient notation for multiple selection, rather than using nested `if…else` statements. You can use the `break` and `continue` statements to alter the flow of control in iteration statements. The logical operators enable you to use more complex conditional expressions in control statements. We used type `decimal` to represent monetary amounts precisely rather than incurring the representational errors associated with types `float` and `double`. In Chapter 7, we examine methods in greater depth.

# 7 Methods: A Deeper Look

## Objectives

In this chapter you'll:

- See that static methods and variables are associated with classes rather than objects.
- Use common Math class functions.
- Learn C#'s argument promotion rules for when argument types do not match parameter types exactly.
- Get a high-level overview of various namespaces from the .NET framework Class Library.
- Use random-number generation to implement game-playing apps.
- Understand how the visibility of identifiers is limited to specific regions of programs.
- See how the method call and return mechanism is supported by the method-call stack.
- Create overloaded methods.
- Use optional and named parameters.
- Use recursive methods.
- Understand what value types and reference types are.
- Pass method arguments by value and by reference.
