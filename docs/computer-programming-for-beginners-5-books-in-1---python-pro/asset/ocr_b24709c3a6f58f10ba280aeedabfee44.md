# The For Loop¹¹⁵

In general, “for” loops are more complex than do-while and while loops. However, for loops can help you perform difficult tasks using fewer C# codes. The syntax of a “for” loop is:

```
`for (initializer; Boolean_expression; update)`
```

```
```text
{
    the_loop’s_body;
}
```
```

A “for” loop has an initializer (i.e. the initial value of the counter), a Boolean expression, a C# statement that updates the counter, and the loop’s body.

The “counter” (i.e. the initial value assigned to the loop) serves as a “for” loop’s most distinctive feature. In most cases, the counter’s value increases until it reaches the final value (e.g. 1 to 10). Also, programmers usually know how many times the “for” loop will iterate.

You may include one or more variables in your “for” loops. These variables may move in descending or ascending order. When writing programs, you may combine ascending and descending variables in a single “for” loop. In addition, an ascending variable can go from 1 to 1024 because “for” loops support arithmetic operations (e.g. addition, multiplication, etc.).

Important Note: All of the parts of a “for” loop are optional. You can create an infinite “for” loop by leaving blank spaces on the syntax. Here’s an example: