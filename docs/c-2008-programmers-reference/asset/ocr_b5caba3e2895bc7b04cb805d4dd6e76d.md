# Part I: C# Fundamentals

A common mistake with the equal relational operator is omitting the second = sign. For example, the following statement prints out the numeric 5 instead of True:

```
Console.WriteLine(num = 5);
```

A single = is the assignment operator.

C programmers often make the following mistake of using a single = for testing equality of two numbers:

```
if (num = 5) //---use == for testing equality---
{
    Console.WriteLine("num is 5");
}
```

Fortunately, the C# compiler will check for this mistake and issue a “Cannot implicitly convert type ‘int’ to ‘bool’” error.

# Logical Operators

C# supports the use of logical operators so that you can evaluate multiple expressions. The following table lists the logical operators supported in C#.

| Operator | Description |
|---|---|
| && | And |
| || | Or |
| ! | Not |

For example, consider the following code example:

```
if (age < 12 || height < 120)
{
    Console.WriteLine("Student price applies");
}
```

In this case, student price applies if either the age is less than 12, or the height is less than 120cm. As long as at least one of the conditions evaluates to true, the statement is true. Following is the truth table for the Or (||) operator.

| Operand A | Operand B | Result |
|---|---|---|
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | true |