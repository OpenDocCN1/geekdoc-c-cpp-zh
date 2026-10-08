
## Try It Yourself

### Arithmetic Operators

To examine how the assignment, addition, compound assignment, and increment and decrement operators behave, follow these steps. For the increment and decrement operators, you explore the difference in behavior between a prefix operation and a postfix operation.

- 1. Create a new Console application.
- 2. In the Main method of the Program.cs file, enter the following code:

```csharp
int i = 20;
Console.WriteLine("i = {0}", i);

i = i + 1;
Console.WriteLine("i = {0}", i);

i += 2;
Console.WriteLine("i = {0}", i);
Console.WriteLine("i = {0}.", --i);
Console.WriteLine("i was {0}, but now is {1} again.", i++, i);
```

- 3. Run the application by pressing Ctrl+F5; you should see the following lines in the console window, as shown in Figure 2.3.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_69_0.png)

FIGURE 2.3
Output of working with the arithmetic operators

- 4. Press any key to close the console and return to Visual Studio.

## Relational Operators

The relational operators, shown in Table 2.10, are used when comparing two values and result in a Boolean value.

In many programming languages, the assignment and equality operators are easily confused because they use the same symbol. This confusion can result in accidental assignments, which remains one of the more common programming mistakes today. To help minimize the possibility for confusion, C# defines a different operator for equality (==).

### HOUR 2: Understanding C# Types

### TABLE 2.10 Relational Operators in C#

| Name | Operator | Expression | Result |
|---|---|---|---|
| Equals | `==` | `x == 20` | `true` |
|  |  | `y == 30` | `false` |
| Not Equals | `!=` | `x != 20` | `false` |
|  |  | `y != 30` | `true` |
| Greater Than | `>` | `x > y` | `true` |
|  |  | `y > x` | `false` |
| Greater Than or Equals | `>=` | `x >= y` | `true` |
|  |  | `y >= x` | `false` |
| Less Than | `<` | `x < y` | `false` |
|  |  | `y < x` | `true` |
| Less Than or Equals | `<=` | `x <= y` | `false` |
|  |  | `y <= x` | `true` |

Assuming x = 20 and y = 10.

### Logical Operators

The logical operators, shown in Table 2.11, evaluate Boolean expressions that result in either **true** or **false**.

### TABLE 2.11 Logical Operators in C#

| Name | Operator | Expression | Result |
|---|---|---|---|
| And (Conditional) | `&&` | `(x == 20) &&`<br>`(y == 30)` | false, both expressions must be true |
| And (Logical) | `&` | `(x == 20) &`<br>`(y == 30)` | false, both expressions must be true |
| Or (Conditional) | `||` | `(x == 20) ||`<br>`(y == 30)` | true, either or both expressions must be true |
| Or (Logical) | `|` | `(x == 20) |`<br>`(y == 30)` | true, either or both expressions must be true |
| Or (Exclusive) | `^` | `(x == 20) ^`<br>`(y == 30)` | true, the expressions are both different |
| Not | `!` | `!(x == 30)` | true, the expression must be false |

Assuming x = 20 and y = 10.

The rules for the logical operators can be easily summarized, assuming an x and y that are Boolean expressions, as shown in Table 2.12.

### TABLE 2.12 Logical Operators Truth Table

| X | Y | X && Y | X \|\| Y | X ^ Y |
| :--- | :--- | :--- | :--- | :--- |
| true | true | true | true | false |
| true | false | false | true | true |
| false | true | false | true | true |
| false | false | false | false | false |

## Try It Yourself

### Relational and Logical Operators

By following these steps, you verify the expressions shown in Table 2.10 and Table 2.11.

- 1. Create a new Console application.
- 2. In the Main method, declare two integer variables named x and y and initialize them to 20 and 10, respectively.
- 3. Using the expressions from Table 2.10 and Table 2.11, write a series of Console.WriteLine statements using the following format, where expression is replaced with the correct expression from the tables:

`Console.WriteLine("expression: {0}", expression);`

- 4. Run the application by pressing Ctrl+F5, and observe that the results match what is shown in the results column of both tables.

## By the Way

### Short-Circuit Evaluation

In C#, the conditional logical operators perform short-circuit evaluation, or minimal evaluation, which means that additional expressions are evaluated only if the first expression would not result in the entire expression being false. The logical operators do not perform short-circuit evaluation.

When short-circuit evaluation is in effect, if the first expression of an AND operator is false, it is not necessary to evaluate any additional expressions because the entire expression will be false. Similarly, if the first expression of an OR operator is true, it is not necessary to evaluate any additional expressions because the entire expression will be true. It is only when the first expression is not sufficient to determine the result of the entire expression that the additional expressions will be evaluated.

### Conditional Operator

The conditional operator (also called a ternary operator, or ternary if, because it takes three terms) is useful for writing concise expressions and evaluates a condition returning one of two values depending on the result.

The conditional operator has the following form:

```
condition ? consequence : alternative
```

When condition is true, the consequence is evaluated and becomes the result. However, when condition is false, the alternative is evaluated and becomes the result instead.

## Watch Out!

### Common Problems with the Ternary Operator

This operator is right-associative, different from most of the other operators which are left-associative. This means an expression like

```
a ? b : c ? d : e
```

is evaluated as

```
a ? b : ( c ? d : e )
```

The type of the conditional expression is determined only from the types of the consequence and alternative, not from the type to which it is being assigned. Ultimately, this requires that the consequence and alternative be of the same type, which means an expression like

```
object x = b ? 0 : "hello";
```

won't compile because the types of the consequence and alternative are int and string.

Although this code isn't practical and should probably never be used outside of this example, the correct way to write this would be

```
object x = b ? (object)0 : (object)"hello";
```

### Default Values

You learned earlier that C# does not allow you to use an uninitialized variable, which means the variable must have a value before you use it. Although this idea of **definite assignment** helps reduce errors, because it is enforced by the compiler, it can be cumbersome if you have to explicitly provide a default value for every field.

To alleviate this burden, fields, or member variables, are always initially assigned with an appropriate default value. Table 2.13 shows the default value for the different predefined data types.

**TABLE 2.13 Default Values**

| Type | Default |
| :---- | :---- |
| sbyte, byte, short, ushort, int, uint, long, ulong | 0 |
| char | `'\u0000'` |
| float | 0.0f |
| double | 0.0d |
| decimal | 0.0m |
| bool | false |
| object | null |
| string | null |

As you can see, for the integral value types, the default value is zero. The default value for the `char` type is the character equivalent of zero and `false` for the `bool` type. The `object` and `string` types have a default value of `null`, representing a **null reference** that literally is one that does not refer to any object.

### Null and Nullable Types

These default values mean that a value-type cannot be null, which at first glance might seem reasonable. However, it presents certain limitations when you work with databases, other external data sources, or other data types that can contain elements that might not be assigned a value. A classic example of this is a numeric field in a database that can store any integer data or might be undefined.

Nullable types provide a solution to this problem. A **nullable type** is a value type that can represent the proper value range of its underlying type and a null value.

Nullable types are represented by the syntax `Nullable<T>` or `T?` where T is a value
