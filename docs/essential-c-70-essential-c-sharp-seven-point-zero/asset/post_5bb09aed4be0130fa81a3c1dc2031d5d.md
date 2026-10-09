
*becomes*, although, in those cases where the delegate is a predicate, it is common to read the lambda operator as *such that* or *where*. You might read the lambda in Listing 13.16 as “*first and second such that first is less than second.*”

Like the `null` literal, an anonymous function does not have any type associated with it; rather, its type is determined by the type it is being converted to. In other words, the lambda expressions we’ve seen so far are not intrinsically of the `Func<`int, int, bool>` (or `Comparer`) type, but they are compatible with that type and may be converted to it. As a result, you cannot use the `typeof()` operator on an anonymous method, and calling `GetType()` is possible only after you convert the anonymous method to a particular type.

Table 13.1 provides additional lambda expression characteristics.

## TABLE 13.1: Lambda Expression Notes and Examples

| Statement | Example |
| :---------- | :-------- |
| Lambda expressions themselves do not have a type. Therefore, there are no members that can be accessed directly from a lambda expression, not even the methods of object. | `// ERROR: Operator "." cannot be applied to // operand of type "lambda expression"`\n`string s = ((int x) => x).ToString();` |
| Lambda expressions do not have a type and so cannot appear to the left of an `is` operator. | `// ERROR: The first operand of an "is" or "as"`\n`// operator may not be a lambda expression or`\n`// anonymous method`\n`bool b = ((int x) => x) is Func<`int, int>;` |
| A lambda expression can be converted only to a compatible delegate type; here an `int`-returning lambda may not be converted to a delegate type that represents a `bool`-returning method. | `// ERROR: lambda expression is not compatible`\n`// with Func<`int, bool>` type`\n`Func<`int, bool>` f = (`int x) => x;` |
| A lambda expression does not have a type, so it cannot be used to infer the type of a local variable. | `// ERROR: Cannot assign lambda expression to`\n`// an implicitly typed local variable`\n`var v = x => x;` |
| Jump statements (break, goto, continue) inside lambda expressions cannot be used to jump to locations outside the lambda expression, and vice versa. Here the break statement inside the lambda would jump to the end of the switch statement outside the lambda. | `// ERROR: Control cannot leave the body of an anonymous method or lambda expression<br>string[] args;<br>Func<string> f;<br>switch(args[0])<br>{<br>&nbsp;&nbsp;&nbsp;&nbsp;case "File":<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;f = ( ) =><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if (!File.Exists(args[1]))<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;break;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return args[1];<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// ...<br>&nbsp;&nbsp;&nbsp;&nbsp;}` |
| Parameters and locals introduced by a lambda expression are in scope only within the lambda body. | `// ERROR: The name "first" does not exist in the current context<br>Func<int, int, bool> expression =<br>(first, second) => first > second;<br>first++;` |
| The compiler's definite assignment analysis is unable to detect initialization of “outer” local variables in lambda expressions. | `int number;<br>Func<string, bool> f =<br>text => int.TryParse(text, out number);<br>if (f("1"))<br>{<br>&nbsp;&nbsp;&nbsp;&nbsp;// ERROR: Use of unassigned local variable<br>&nbsp;&nbsp;&nbsp;&nbsp;System.Console.Write(number);<br>}` |
| The compiler's definite assignment analysis is unable to detect initialization of “outer” local variables in lambda expressions. | `int number;<br>Func<int, bool> isFortyTwo =<br>x => 42 == (number = x);<br>if (isFortyTwo(42))<br>{<br>&nbsp;&nbsp;&nbsp;&nbsp;// ERROR: Use of unassigned local variable<br>&nbsp;&nbsp;&nbsp;&nbsp;System.Console.Write(number);<br>}` |

## Anonymous Methods

Lambda expressions are not supported in C# 2.0. Instead, C# 2.0 uses a syntax called *anonymous methods*. An anonymous method is like a statement lambda, but without many of the features that make lambdas so compact. An anonymous method must explicitly type every parameter, and must have a statement block. Rather than using the lambda operator `->` between the parameter list and the code block, an anonymous method puts the keyword `delegate` before the parameter list, emphasizing that the anonymous method must be converted to a `delegate` type. Listing 13.17 shows the code from Listings 13.7, 13.12, and 13.15 rewritten to use an anonymous method.

### LISTING 13.17: Passing an Anonymous Method in C# 2.0

```
// ...
BubbleSort(items,
    delegate(int first, int second)
    {
        return first < second;
    }
);
// ...
```

It is unfortunate that there are two very similar ways to define an anonymous function in C# 3.0 and later.

- **Guidelines**
  - AVOID the anonymous method syntax in new code; prefer the more compact lambda expression syntax.

There is, however, one small feature that is supported in anonymous methods that is not supported in lambda expressions: Anonymous methods may omit their parameter list entirely in some circumstances.

## ADVANCED TOPIC

### Parameterless Anonymous Methods

Unlike lambda expressions, anonymous methods may omit the parameter list entirely provided that the anonymous method body does not use any parameter and the `delegate` type requires only “value” parameters (i.e., it does not require the parameters to be marked as `out` or `ref`). For example, the anonymous method expression `delegate { return Console.ReadLine() != ";"; }` is convertible to any delegate type that requires a return type of `bool` regardless of the number of parameters the delegate requires. This feature is not used frequently, but you might encounter it when reading legacy code.

![](img/ef6a8a417630b222bfb3f3b949facff0_593_0.png)

## ADVANCED TOPIC

### Why “Lambda” Expressions?

It is fairly obvious why anonymous methods are so named: They look very similar to method declarations but do not have a declared name associated with them. But where did the lambda in “lambda expressions” come from?

The idea of lambda expressions comes from the work of the logician Alonzo Church, who in the 1930s invented a technique called the lambda calculus for studying functions. In Church’s notation, a function that takes a parameter $x$ and results in an expression $y$ is notated by prefixing the entire expression with a small Greek letter lambda and separating the parameter from the value with a dot. The C# lambda expression `x=>y` would be notated $\lambda x.y$ in Church’s notation. Because it is inconvenient to use Greek letters in C# programs and because the dot already has many meanings in C#, the designers of C# chose to use the “fat arrow” notation rather than the original notation. The name lambda expression indicates that the theoretical underpinnings of the idea of anonymous functions are based on the lambda calculus, even though no letter lambda actually appears in the text.

## Delegates Do Not Have Structural Equality

Delegate types in .NET do not exhibit **structural equality**. That is, you cannot convert a reference to an object of one delegate type to an unrelated delegate type, even if the formal parameters and return types of both delegates are identical. For example, you cannot assign a reference to a `Comparer` to a variable of type `Func<int, int, bool>` even though both delegate types represent methods that take two int parameters and return a `bool`. Unfortunately, the only way to use a delegate of a given type when a delegate of a structurally identical but unrelated delegate type is
