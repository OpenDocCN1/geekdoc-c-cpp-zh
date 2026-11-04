However, if the condition is changed such that student price applies only if a person is less than 12 years old and with height less than 120cm, the statement would be rewritten as:

```
if (age < 12 && height < 120)
{
    Console.WriteLine("Student price applies");
}
```

The truth table for the And (&&) operator follows.

| Operand A | Operand B | Result |
|---|---|---|
| false | false | false |
| false | true | false |
| true | false | false |
| true | true | true |

The Not operator (!) negates the result of an expression. For example, if student price does not apply to those more than 12 years old, you could write the expression like this:

```
if (!(age <= 12))
    Console.WriteLine("Student price does not apply");
```

Following is the truth table for the Not operator.

| Operand A | Result |
|---|---|
| false | true |
| true | false |

# Short-Circuit Evaluation

C# uses short-circuiting when evaluating logical operators. In short-circuiting, the second argument in a condition is evaluated only when the first argument is not sufficient to determine the value of the entire condition. Consider the following example:

```
int div = 0;
int num = 5;
if ((div == 0) || (num / div == 1))
{
    Console.WriteLine(num); //---5---
}
```

Here the first expression evaluates to true, so there is no need to evaluate the second expression (because an Or expression evaluates to true as long as at least one expression evaluates to true). The second expression, if evaluated, will result in a division-by-zero error. In this case, it won't, and the number 5 is printed.