Program 18.3 displays the following output:
Division by zero
y = 1

Note that the program did not stop at the point of exceptional condition. It catches the error condition, prints the error message and then continues the execution as if nothing has happened. Compare this with the execution of Program 18.2 which did not give the value of y.

Most often, exceptions are thrown by methods that are invoked from within the try blocks. The point at which an exception is thrown is called the throw point. Once an exception is thrown to the catch block, control cannot return to the throw point. This kind of relationship is shown in Fig. 18.2.

![](bbox=[0.6, 0.12, 0.95, 0.33])

# 18.6 MULTIPLE CATCH STATEMENTS

It is possible to have more than one catch statement in the catch block as illustrated below:

```
try
{
    statement ;        // generates an exception
}
catch (Exception-Type-1 e)
{
    statement;         // processes exception type 1
}
catch (Exception-Type-2 e)
{
    statement;         // processes exception type 2
}
...
catch (Exception-type-N e)
{
    statement ;        // processes exception type N
}
```

When an exception in a try block is generated, the C# treats the multiple catch statements like cases in a switch statement. The first statement whose parameter matches with the exception object will be executed, and the remaining statements will be skipped.

Note that C# does not require any processing of the exception at all. We can simply have a catch statement with an empty block to avoid program abortion.

Example:

```
catch (Exception e){ }
```

This statement will catch an exception and then ignore it.