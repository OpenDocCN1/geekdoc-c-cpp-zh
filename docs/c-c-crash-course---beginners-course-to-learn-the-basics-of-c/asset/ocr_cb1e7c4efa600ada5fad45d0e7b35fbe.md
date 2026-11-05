```
Console.WriteLine("a is equal to b");
}
}
```

# The Switch-Case Statement

Programmers use a switch-case statement in situations where the possible answers are numerous. Here’s the syntax of a switch-case statement:

```
switch (selector)
{
    case first_integer;
        statements;
        break;
    case second_integer:
        statements;
        break;
    default:
        statements;
        break;
}
```

Basically, selectors are expressions that return usable values (i.e. values that you can compare or process). The “switch” keyword compares the selector’s value against the “cases”. If the value of the selector matches that of a case, the statements assigned to that case will run. If there’s no match, however, the program will execute the default statement/s (if any). That means the program will analyze the selector first before running any statement.

Important Note: Make sure that the cases have unique values. If two or more cases share the same value, your program will produce undesirable results.

As you can see, each case has a “break” clause. The “break” clause terminates the body of the case to which it belongs. C# requires you to add this clause to all of your switch statements.