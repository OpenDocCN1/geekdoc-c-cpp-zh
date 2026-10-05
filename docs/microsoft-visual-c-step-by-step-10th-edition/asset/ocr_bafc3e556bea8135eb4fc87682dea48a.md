Click here to view code image

```
static void doWork()
{
    // int i = 0;
    // Console.WriteLine(i);
    // Pass.Value(i);
    // Console.WriteLine(i);
    var wi = new WrappedInt();
    Console.WriteLine(wi.Number);
    Pass.Reference(wi);
    Console.WriteLine(wi.Number);
}
```

+   14. On the Debug menu, select Start Without Debugging to build and run the application.

This time, the two values displayed in the console window correspond to the value of wi.Number before and after the call to the Pass.Reference method. You should see that the values 0 and 42 are displayed.

+   15. Press Enter to close the application and return to Visual Studio 2022.

To explain what the previous exercise shows, the value of wi.Number is initialized to 0 by the compiler-generated default constructor. The wi variable contains a reference to the newly created WrappedInt object (which contains an int). The wi variable is then copied as an argument to the Pass.Reference method. Because WrappedInt is a class (a reference type), wi and param both refer to the same WrappedInt object. Any changes made to the contents of the object through the param variable in the Pass.Reference method are visible by using the wi variable when the method completes. The following diagram illustrates what happens when a WrappedInt object is passed as an argument to the Pass.Reference method.