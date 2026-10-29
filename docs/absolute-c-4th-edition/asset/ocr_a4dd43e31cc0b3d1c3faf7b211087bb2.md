the function to another. There is seldom any other situation that can profitably benefit from throwing an exception.

+   If an exception is thrown in a function but not caught in that function, then the exception type should be listed in an exception specification for that function.

+   If an exception is thrown but never caught, then the default behavior is to end your program.

+   Do not overuse exceptions.

# ANSWERS TO SELF-TEST EXERCISES

1. Try block entered.
Exception thrown with
waitTime equal to 46
After catch block.

2. Try block entered.
Leaving try block.
After catch block.

3. throw waitTime;

Note that the following is an if statement, not a throw statement, even though it contains a throw statement:

```
if (waitTime > 30)
    throw waitTime;
```

4. When a throw statement is executed, that is the end of the enclosing try block. No other statements in the try block are executed, and control passes to the following catch block or blocks. When we say control passes to the following catch block, we mean that the value thrown is plugged in for the catch-block parameter (if any) and the code in the catch block is executed.

```
try
{
    cout << "Try block entered.";
    if (waitTime > 30)
        throw waitTime;
    cout << "Leaving try block.";
}
```

```
catch(int thrownValue)
{
    cout << "Exception thrown with\n"
         << "waitTime equal to" << thrownValue << endl;
}
```