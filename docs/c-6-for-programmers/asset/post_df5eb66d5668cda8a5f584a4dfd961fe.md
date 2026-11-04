
```csharp
// Fig. 6.12: AutoPolicyTest.cs
// Demonstrating strings in switch.
using System;

class AutoPolicyTest
{
    static void Main()
    {
        // create two AutoPolicy objects
        AutoPolicy policy1 = new AutoPolicy(11111111, "Toyota Camry", "NJ");
        AutoPolicy policy2 = new AutoPolicy(22222222, "Ford Fusion", "ME");

        // display whether each policy is in a no-fault state
        PolicyInNoFaultState(policy1);
        PolicyInNoFaultState(policy2);
    }

    // method that displays whether an AutoPolicy
    // is in a state with no-fault auto insurance
    public static void PolicyInNoFaultState(AutoPolicy policy)
    {
        Console.WriteLine("The auto policy:");
        Console.WriteLine($"Account #: {policy.AccountNumber}; ");
        Console.WriteLine($"Car: {policy.MakeAndModel};");
        Console.WriteLine($"State {policy.State}:");
        Console.WriteLine($"{(policy.IsNoFaultState ? "is" : "is not")}");
        Console.WriteLine(" a no-fault state\n");
    }
}
```

The auto policy:
Account #: 11111111; Car: Toyota Camry;
State NJ is a no-fault state

The auto policy:
Account #: 22222222; Car: Ford Fusion;
State ME is not a no-fault state

Fig. 6.12 | Demonstrating strings in switch.

## 6.9 break and continue Statements

In addition to selection and iteration statements, C# provides statements break and continue to alter the flow of control. The preceding section showed how break can be used to terminate a switch statement's execution. This section discusses how to use break to terminate any iteration statement.

### 6.9.1 break Statement

The break statement, when executed in a while, for, do...while, switch, or foreach, causes immediate exit from the loop or switch. Execution continues with the first statement after the control statement. Figure 6.13 demonstrates a break statement exiting a for. When the if nested at line 13 in the for statement (lines 11–19) determines that count is 5, the break statement at line 15 executes. This terminates the for statement, and the app proceeds to line 21 (immediately after the for statement), which displays a message indicating the value of the control variable when the loop terminated. The loop fully executes its body only four times instead of 10 because of the break.

```csharp
// Fig. 6.13: BreakTest.cs
// break statement exiting a for statement.
using System;

class BreakTest
{
    static void Main()
    {
        int count; // control variable also used after loop terminates

        for (count = 1; count <= 10; ++count) // loop 10 times
        {
            if (count == 5) // if count is 5,
            {
                break; // terminate loop
            }

            Console.Write($"{count} ");
        }

        Console.WriteLine($"\nBroke out of loop at count = {count}");
    }
}
```

```text
1 2 3 4
Broke out of loop at count = 5
```

**Fig. 6.13** | break statement exiting a for statement.

### 6.9.2 continue Statement

The **continue** statement, when executed in a while, for, do...while, or foreach, skips the remaining statements in the loop body and proceeds with the next iteration of the loop. In while and do...while statements, the app evaluates the loop-continuation test *immediately after* the continue statement executes. In a for statement, the increment expression normally executes next, then the app evaluates the loop-continuation test.

Figure 6.14 uses the continue statement in a for statement to skip the statement at line 16 when the nested if (line 11) determines that the value of count is 5. When the continue statement executes, program control continues with the increment of the control variable in the for statement (line 9).

![](img/3f5ef6be1748bb746e5f71a483bba4d0_177_0.png)

> **Software Engineering Observation 6.1**
> 
> *There's a tension between achieving quality software engineering and achieving the best-performing software. Often, one of these goals is achieved at the expense of the other. For all but the most performance-intensive situations, apply the following rule: First, make your code simple and correct; then make it fast, but only if necessary.*

which is true if and only if *both* simple conditions are true. Some programmers find that the preceding combined condition is more readable with redundant parentheses, as in

(gender == 'F') && (age >= 65)

The table in Fig. 6.15 summarizes the `&&` operator. The table shows all four possible combinations of false and true values for `expression1` and `expression2`. Such tables are called truth tables. C# evaluates all expressions that include relational operators, equality operators or logical operators to `bool` values—which are either `true` or `false`.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_179_0.png)

### 6.10.2 Conditional OR (||) Operator

Now suppose we wish to ensure that *either* or *both* of two conditions are true before we choose a certain path of execution. In this case, we use the `||` (conditional OR) operator, as in the following app segment:

```
if ((semesterAverage >= 90) || (finalExam >= 90))
{
    Console.WriteLine ("Student grade is A");
}
```

This statement also contains two simple conditions. The condition `semesterAverage >= 90` is evaluated to determine whether the student deserves an A in the course because of a solid performance throughout the semester. The condition `finalExam >= 90` is evaluated to determine whether the student deserves an A in the course because of an outstanding performance on the final exam. The `if` statement then considers the combined condition

(semesterAverage >= 90) || (finalExam >= 90)

and awards the student an A if either or both of the simple conditions are true. The only time the message `"Student grade is A"` is *not* displayed is when *both* of the simple conditions are *false*. Fig. 6.16 is a truth table for operator conditional OR (`||`). Operator `&&` has a higher precedence than operator `||`. Both operators associate from left to right.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_179_1.png)

### 6.10.3 Short-Circuit Evaluation of Complex Conditions

The parts of an expression containing && or || operators are evaluated only until it’s known whether the condition is true or false. Thus, evaluation of the expression

```
(gender == 'F') && (age >= 65)
```

stops immediately if gender is not equal to 'F' (i.e., at that point, it’s certain that the entire expression is false) and continues only if gender is equal to 'F' (i.e., the entire expression could still be true if the condition age >= 65 is true). This feature of conditional AND and conditional OR expressions is called short-circuit evaluation.

> > **Common Programming Error 6.3**
> >
> > In expressions using operator &&, a condition — known as the dependent condition — may require another condition to be true for the evaluation of the dependent condition to be meaningful. In this case, the dependent condition should be placed after the other one, or an error might occur. For example, in the expression `(i != 0) && (1/i == 1/2)`, the second condition must appear after the first condition, or a divide-by-zero error might occur.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_180_0.png)

### 6.10.4 Boolean Logical AND (&) and Boolean Logical OR (|) Operators

The boolean logical AND (&) and boolean logical inclusive OR (|) operators work identically to the && (conditional AND) and || (conditional OR) operators, with one exception—the boolean logical operators always evaluate both of their operands (i.e., they do not perform short-circuit evaluation). Therefore, the expression

```
(gender == 'F') & (age >= 65)
```

evaluates age >= 65 regardless of whether gender is equal to 'F'. This is useful if the right operand of the & or | operator has a required side effect—such as a modification of a variable’s value. For example, the expression

```
(birthday == true) | (++age >= 65)
```

guarantees that the condition ++age >= 65 will be evaluated. Thus, the variable age is incremented in the preceding expression, regardless of whether the overall expression is true or false.

> > **Error-Prevention Tip 6.3**
> >
> > For clarity, avoid expressions with side effects in conditions. The side effects may appear clever, but they can make it harder to understand code and can lead to subtle logic errors.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_180_1.png)

### 6.10.5 Boolean Logical Exclusive OR (^)

A complex condition containing the boolean logical exclusive OR (^) operator (also called the logical XOR operator) is true if and only if one of its operands is true and the other is false. If both operands are true or both are false, the entire condition is false. Figure 6.17 is a truth table for the boolean logical exclusive OR operator. This operator is also guaranteed to evaluate both of its operands.
