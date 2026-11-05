# Guidelines for Placement of Curly Braces

Curly braces are required when the body following an if or else statement has more than one statement. Many developers use curly braces with all selection statements—even single if...else statements. In this book, curly braces are added when there are two or more executable statements. For single statements, curly braces were omitted. Whether you use curly braces with all cases or just for multi-statement executables, be consistent with your usage.

Open braces should always be at the beginning of the line after the statement that begins the block.

The contents of the brace should be indented by four spaces. For example:

```
if (someExpression)
{
    ExecuteMethod1( );
    ExecuteMethod2( );
}
else
{
    ExecuteMethod3( );
    ExecuteMethod4( );
}
```

# Guidelines for Placement of else with Nested if Statements

Many developers place an else...if on the same line when a nested if is written. In this book, the else is placed on a line by itself. The if statement appears on the line below as shown in the following example:

```
if (someExpression)
    DoSomething();
else
    if
    {
        DoSomethingElse(); // Curly braces are not needed here.
    }
```

# Guidelines for Use of White Space with a Switch Statement

Place curly braces on separate lines with a switch statement. Indent the case statements. Do not place curly braces around multiline executables as shown in the following example:

```
switch (someExpression)
{
    case 0:
        DoSomething();
        break;
    case 1:
        DoSomethingElse();
```