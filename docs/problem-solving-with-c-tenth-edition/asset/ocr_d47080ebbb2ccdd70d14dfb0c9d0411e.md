2. Try block entered.
Leaving try block.
After catch block.

3. `throw waitTime;`

Note that the following is an if statement, not a throw statement, even though it contains a throw statement:

```
if (waitTime> 30)
    throw waitTime;
```

4. When a throw statement is executed, that is the end of the enclosing try block. No other statements in the try block are executed, and control passes to the following catch block(s). When we say control passes to the following catch block, we mean that the value thrown is plugged in for the catch-block parameter (if any), and the code in the catch block is executed.

```
5. try
{
    cout << "Try block entered.";
    if (waitTime > 30)
        throw (waitTime);
    cout << "Leaving try block.";
}
```

```
6. catch(int thrownValue)
{
    cout << "Exception thrown with\n"
         << "waitTime equal to" << thrownValue << endl;
}
```

7. thrownValue is the catch-block parameter.

8. Trying.
Starting sampleFunction.
Catching.
End of program.

9. Trying.
Starting sampleFunction.
Trying after call.
End of program.

10. If an exception is not caught anywhere, then your program ends.

11. Yes, you can have a try block and corresponding catch blocks inside another larger try block. However, it would probably be better to place the inner try and catch blocks in a function definition and place an invocation of the function in the larger try block.