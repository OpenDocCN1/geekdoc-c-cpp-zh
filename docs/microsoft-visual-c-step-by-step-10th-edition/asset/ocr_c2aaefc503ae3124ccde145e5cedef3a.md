result generated is -2147483648.) The reason for this behavior is performance: integer arithmetic is a common operation in almost every program, and adding the overhead of overflow checking to each integer expression could lead to very poor performance. In many cases, the risk is acceptable you know (or hope!) that your int values won't reach their limits. If you don't like this approach, you can turn on overflow checking.

> > Tip
nYou turn overflow checking on and off in Visual Studio 2022 by setting the project properties. In Solution Explorer, select YourProject (where YourProject is the actual name of the project). On the Project menu, select YourProject Properties. In the Project Properties dialog, select the Build tab. Select the Advanced button in the lower-right corner of the page. Finally, select the Advanced Built Settings dialog, select or clear the For Arithmetic Overflow/Underflow checkbox.

Regardless of how you compile an application, you can use the checked and unchecked keywords to turn on and off integer overflow checking in parts of an application that you think need it (or don't). These keywords override the compiler option specified for the project.

# Writing checked statements

A checked statement is a block preceded by the checked keyword. All integer arithmetic in a checked statement always throws an OverflowException if an integer calculation in the block overflows, as shown in this example:

Click here to view image

```
int number = int.MaxValue;
checked{
    int intWillThrow = number++;
    Console.WriteLine("This will not be reached");
}
```

> > Important