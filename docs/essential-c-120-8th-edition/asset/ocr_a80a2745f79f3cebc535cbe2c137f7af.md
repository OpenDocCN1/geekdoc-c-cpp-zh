# LISTING 7.21: Type Checking with a switch Statement

```
public static TimeOnly GetTime(object input)
{
    switch (input)
    {
        case DateTime datetime:
            return TimeOnly.FromDateTime(datetime);
        case DateTimeOffset datetimeOffset:
            return TimeOnly.FromDateTime(datetimeOffset.DateTime);
        case string dateText:
            return TimeOnly.Parse(dateText);
        case null:
            throw new ArgumentNullException(nameof(input));
        default:
            throw new ArgumentException(\$Invalid type - {input.GetType().FullName}");
    }
}
```

Listing 7.21 includes a case for null, but if none of the cases matches, default provides a catch and throws an exception. Also, like with the operator, you can declare a variable simultaneously, providing access to an instance of the object that matches the case.

Starting in C# 8.0, the switch statement includes a more succinct expression that returns a value.

# Type Checking with switch Expressions

Like the switch statement, the switch expression (C# 8.0) provides multiple paths for each case—generically a match expression (for both switch expressions and statements). Unlike the switch statement, there are no labels, no break statements, and in fact, no enclosed statements at all. Most importantly, the switch expression returns a value (except when it throws an exception). This makes it a preferable option to the switch statement in Listing 7.21, which allows for a return only because the function of the embedded return statements. You couldn't, for example, assign the switch result to a variable. Listing 7.22 provides an example.

From Listing 7.22 you will notice that unlike a switch statement, the input operand for the switch statement appears before the switch keyword. Each