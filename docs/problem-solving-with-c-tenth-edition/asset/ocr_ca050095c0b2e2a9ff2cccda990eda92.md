# catch-Block Parameter

The catch-block parameter is an identifier in the heading of a catch block that serves as a placeholder for an exception (a value) that might be thrown. When a (suitable) value is thrown in the preceding try block, that value is plugged in for the catch-block parameter. You can use any legal (nonreserved word) identifier for a catch-block parameter.

# EXAMPLE

```
catch(int e)
{
    cout << e << " donuts, and No Milk!\n"
        << "Go buy some milk.\n";
}
```

e is the catch-block parameter.

as the user enters a nonpositive number, the try block stops and the catch block is executed. For now, we will assume that every try block is followed by an appropriate catch block. We will later discuss what happens when there is no appropriate catch block.

Next, we summarize what happens when no exception is thrown in a try block. If no exception (no value) is thrown in the try block, then after the try block is completed, program execution continues with the code after the catch block. In other words, if no exception is thrown, then the catch block is ignored. Most of the time when the program is executed, the throw statement will not be executed, and so in most cases, the code in the try block will run to completion and the code in the catch block will be ignored completely.

# try-throw-catch

This is the basic mechanism for throwing and catching exceptions. The throw statement throws the exception (a value). The catch block catches the exception (the value). When an exception is thrown, the try block ends and then the code in the catch block is executed. After the catch block is completed, the code after the catch block(s) is executed (provided the catch block has not ended the program or performed some other special action).

If no exception is thrown in the try block, then after the try block is completed, program execution continues with the code after the catch block(s). (In other words, if no exception is thrown, then the catch block(s) are ignored.)