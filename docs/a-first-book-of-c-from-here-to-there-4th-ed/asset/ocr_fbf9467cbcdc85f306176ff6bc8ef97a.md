The general syntax of the code required to throw and catch an exception is as follows:

```
try
{
    // one or more statements,
    // at least one of which should
    // be capable of throwing an exception
}
catch(exceptionDataType parameterName)
{
    // one or more statements
}
```

This example uses two new keywords: try and catch. The try keyword identifies the start of an exception-handling block of code. At least one of the statements inside the braces defining this block of code should be capable of throwing an exception. As an example, examine the try block in the following section of code:

```
try
{
    cout << "Enter the numerator (whole numbers only): ";
    cin >> numerator;
    cout << "Enter the denominator (whole numbers only):";
    cin >> denominator;
    result = numerator/denominator;
}
```

The try block contains five statements, three of which might result in an error you want to catch. In particular, a professionally written program would make sure valid integers are entered in response to both prompts and the second entered value isn't a 0. For this example, you see how to ensure that the second value entered isn't 0.

Therefore, for the purposes of this example, only the value of the second number matters. The try block is altered to say "Try all the statements in me to see whether an exception, which in this case is a 0 second value, occurs." To check that the second value isn't 0, you add a throw statement in the try block, as follows:

```
try
{
    cout << "Enter the numerator: (whole number only): ";
    cin >> numerator;
    cout << "Enter the denominator: (whole number only): ";
    cin >> denominator;
    if (denominator == 0)
        throw denominator;
    else
        result = numerator/denominator;
}
```