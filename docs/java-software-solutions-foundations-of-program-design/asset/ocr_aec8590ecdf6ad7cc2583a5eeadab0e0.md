# 6.1 The switch Statement

Another conditional statement in Java is called the switch statement, which causes the executing program to follow one of several paths based on a single value. Similar logic could be constructed with multiple if statements, but in the cases where it is warranted, a switch statement usually makes code easier to read.

The switch statement evaluates an expression to determine a value and then matches that value with one of several possible cases. Each case has statements associated with it. After evaluating the expression, control jumps to the statement associated with the first case that matches the value. Consider the following example:

```
switch (idChar)
{
    case 'A':
        aCount = aCount + 1;
        break;
    case 'B':
        bCount = bCount + 1;
        break;
    case 'C':
        cCount = cCount + 1;
        break;
    default:
        System.out.println ("Error in Identification Character.");
}
```

First, the expression is evaluated. In this example, the expression is a simple char variable called idChar. Execution then transfers to the first statement after the case value that matches the result of the expression. Therefore, if idChar contains an 'A', the variable aCount is incremented. If it contains a 'B', the case for 'A' is skipped and processing continues where bCount is incremented. Likewise, if idChar contains a 'C', that case is processed.

KEY CONCEPT
A switch statement matches a character or integer value to one of several possible cases.

If no case value matches that of the expression, execution continues with the optional default case, indicated by the reserved word default. If no default case exists, no statements in the switch statement are executed and processing continues with the statement after the switch statement. It is often a good idea to include a default case, even if you don’t expect it to be executed.

When a break statement is encountered, processing jumps to the statement following the switch statement. A break statement is usually used to break out of each case of a switch statement. Without a break statement, processing continues into the next case of the switch. Therefore, if the break statement at the end of