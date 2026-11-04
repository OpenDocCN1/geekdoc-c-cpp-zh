```
```csharp
for(i=1; i <= 10; i++) {
    sum = sum + i;
    prod = prod * i;
}
Console.WriteLine("Sum is " + sum);
Console.WriteLine("Product is " + prod);
}
```
```

The output is shown here:

```
```
Sum is 55
Product is 3628800
```
```

Here, the block enables one loop to compute both the sum and the product. Without the use of the block, two separate for loops would have been required.

One last point: Code blocks do not introduce any runtime inefficiencies. In other words, the { and } do not consume any extra time during the execution of a program. In fact, because of their ability to simplify (and clarify) the coding of certain algorithms, the use of code blocks generally results in increased speed and efficiency.

# Semicolons, Positioning, and Indentation

In C#, the semicolon signals the end of a statement. That is, each individual statement must end with a semicolon.

As you know, a block is a set of logically connected statements that are surrounded by opening and closing braces. A block is not terminated with a semicolon. Since a block is a group of statements, it makes sense that a block is not terminated by a semicolon; instead, the end of the block is indicated by the closing brace.

C# does not recognize the end of the line as the end of a statement—only a semicolon terminates a statement. For this reason, it does not matter where on a line you put a statement. For example, to C#,

```
```csharp
x = y;
y = y + 1;
Console.WriteLine(x + " " + y);
```
```

is the same as

```
```csharp
x = y;  y = y + 1;  Console.WriteLine(x + " " + y);
```
```

Furthermore, the individual elements of a statement can also be put on separate lines. For example, the following is perfectly acceptable:

```
```csharp
Console.WriteLine("This is a long line of output" +
    x + y + z +
    "more output");
```
```

Breaking long lines in this fashion is often used to make programs more readable. It can also help prevent excessively long lines from wrapping.