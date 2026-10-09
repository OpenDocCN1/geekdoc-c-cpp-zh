In this example, the *if* statement checks whether the radius is positive. If so, the area of the circle is calculated and displayed; otherwise, an invalid radius message is displayed.

Notice that in this example, two statements follow the first *if*. However, these two statements appear within curly braces. The curly braces combine the statements into a code block, which is itself a single statement.

If you omit the curly braces that create a code block in Listing 4.24, only the statement immediately following the Boolean expression executes conditionally. Subsequent statements will execute regardless of the *if* statement’s Boolean expression. The invalid code is shown in Listing 4.25.

# **LISTING 4.25:** Relying on Indentation, Resulting in Invalid Code

```
if(radius >= 0)
    area = Math.PI * radius * radius;
    System.Console.WriteLine(
        $"The area of the circle is: { area:0.00}");
```

In C#, indentation is used solely to enhance the code readability. The compiler ignores it, so the previous code is semantically equivalent to Listing 4.26.

# **LISTING 4.26:** Semantically Equivalent to Listing 4.25 with Curly Braces

```
if(radius >= 0)
{
    area = Math.PI * radius * radius;
}
System.Console.WriteLine(
    $"The area of the circle is:{ area:0.00}");
```

Programmers should take great care to avoid subtle bugs such as this, perhaps even going so far as to always include a code block after a control flow statement, even if there is only one statement. A widely accepted coding guideline is to avoid omitting braces, except possibly for the simplest of single-line *if* statements.

Although unusual, it is possible to have a code block that is not lexically a direct part of a control flow statement. In other words, placing curly braces on their own (e.g., without a conditional or loop) is legal syntax.