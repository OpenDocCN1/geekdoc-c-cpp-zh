```
~~~csharp
        // . . . control will actually pass here . . .
        break;
    case 'Smith':
        // . . . do Smith stuff . . .
        break;
    case 'Jones':
        // . . . do Jones stuff . . .
        break;
    case 'Hvidsten':
        // . . . do Hvidsten stuff . . .
        break;
    default:
        // Goes here if it doesn't pass any cases.
        break;
}
~~~
```

![](bbox=[0.1, 0.26, 0.2, 0.36])

Using the switch statement involves these severe restrictions:

+   * The argument to the `switch()` must be one of the counting types (including `char`) or a string. Floating-point values are excluded.
+   * The various case values must refer to values of the same type as the switch expression.
+   * The case values must be constant in the sense that their value must be known at compile time. (A statement such as `case x` isn't legal unless `x` is a type of constant.)
+   * Each clause must end in a `break` statement (or another exit command, such as `return`). The break statement passes control out of the `switch`.

You can omit a break statement if two cases lead to the same actions: A single case clause may have more than one case label, as in this example:

```
~~~csharp
    string s = "Davis";
    switch(s)
    {
        case "Davis":
        case "Hvidsten":
            // Do the same thing whether s is Davis or Hvidsten
            // since they're related.
            break;
        case "Smith":
            // . . . do Smith stuff . . .
            break;
        default:
            // Goes here if it doesn't pass any cases.
            break;
    }
~~~
```

This approach enables the program to perform the same operation, whether the input is Davis or Hvidsten. The SwitchSyntaxTest example on the Web site illustrates a variety of advice about using switch. The final section of this chapter supplies a small addendum to the switch story. You can find the code at csharp102.info.

![](bbox=[0.1, 0.87, 0.2, 0.95])