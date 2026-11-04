```
Console.WriteLine("this won't be displayed");
}

class ExcDemo2 {
    static void Main() {
        try {
            ExcTest.GenException();
        }
        catch (IndexOutOfRangeException) {
            // Catch the exception.
            Console.WriteLine("Index out-of-bounds!");
        }
        Console.WriteLine("After catch block.");
    }
}
```

This program produces the following output, which is the same as that produced by the first version of the program shown earlier:

```
Before exception is generated.
nums[0]: 0
nums[1]: 1
nums[2]: 2
nums[3]: 3
Index out-of-bounds!
After catch block.
```

As explained, because GenException() is called from within a try block, the exception that it generates (and does not catch) is caught by the catch in Main(). Understand, however, that if GenException() had caught the exception, then it never would have been passed back to Main().

# The Consequences of an Uncaught Exception

Catching one of the standard exceptions, as the preceding program does, has a side benefit: It prevents abnormal program termination. When an exception is thrown, it must be caught by some piece of code, somewhere. In general, if your program does not catch an exception, it will be caught by the runtime system. The trouble is that the runtime system will report an error and terminate the program. For instance, in this example, the index out-of-bounds exception is not caught by the program:

```
// Let the C# runtime system handle the error.

using System;

class NotHandled {
    static void Main() {
        int[] nums = new int[4];
```