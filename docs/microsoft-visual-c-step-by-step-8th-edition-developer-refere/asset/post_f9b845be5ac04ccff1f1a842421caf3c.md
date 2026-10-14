
IDisposable interface, as shown here in bold:

Click here to view code image

```
class Calculator : IDisposable
{
    ...
}
```

3. Add to the end of the Calculator class the following method (named Dispose). This method is defined by the IDisposable interface:

Click here to view code image

```
class Calculator : IDisposable
{
    ...
    public void Dispose()
    {
        Console.WriteLine("Calculator being disposed");
    }
}
```

You would normally add code to the Dispose method that releases the resources held by the object. There are none in this case, and the purpose of the Console.WriteLine statement in this method is just to let you see when the Dispose method is run. However, you can see that in a real-world application, there would likely be some duplication of code between the destructor and the Dispose method. To remove this duplication, you would typically place this code in one place and call it from the other. But because you cannot explicitly invoke a destructor from the Dispose method, it makes sense instead to call the Dispose method from the destructor and place the logic that releases resources in the Dispose method.

4. Modify the destructor so that it calls the Dispose method, as shown in bold in the following code. (Leave the statement displaying the message in place in the finalizer so that you can see when it is being run by the garbage collector).

Click here to view code image

```
~Calculator()
{
    Console.WriteLine("Calculator being finalized");
    this.Dispose();
}
```

When you want to destroy a Calculator object in an application, the Dispose method does not run automatically; your code must either call it explicitly (with a statement such as calculator.Dispose()) or create the Calculator object within a using statement. In your program, you will adopt the latter approach.

## 5. Display the Program.cs file in the Code and Text Editor window. Modify the statements in the Main method that create the Calculator object and call the Divide method, as shown here in bold:

Click here to view code image

```
static void Main(string[] args)
{
    using (Calculator calculator = new Calculator())
    {
        Console.WriteLine($"120 / 15 = {calculator.Divide(120, 15)}");
    }

    Console.WriteLine("Program finishing");
}
```

## 6. On the Debug menu, click Start Without Debugging. Verify that the program now displays the following series of messages:

```
Calculator being created
120 / 15 = 8
Calculator being disposed
Program finishing
Calculator being finalized
Calculator being disposed
```

The using statement causes the Dispose method to run before the statement that displays the “Program finishing” message. However, you can see that the destructor for the Calculator object still runs when the application finishes, and it calls the Dispose method again. This is clearly a waste of processing.

## 7. In the console window, press the Enter key and return to Visual Studio 2015.

Disposing of the resources held by an object more than once might or might not be disastrous, but it is definitely not good practice. The recommended approach to resolving this problem is to add a private Boolean field to the class to indicate whether the Dispose method has already been invoked, and then examine this field in the Dispose method.

### Prevent an object from being disposed of more than once

- 1. Display the Calculator.cs file in the Code and Text Editor window.
- 2. Add to the Calculator class a private Boolean field called disposed, and initialize the value of this field to false, as shown in bold in the following:

Click here to view code image

```
class Calculator : IDisposable
{
    private bool disposed = false;
```

The purpose of this field is to track the state of this object and indicate whether the Dispose method has been invoked.

3. Modify the code in the Dispose method to display the message only if the disposed field is false. After displaying the message, set the disposed field to true, as demonstrated here in bold:

Click here to view code image

```
public void Dispose()
{
    if (!this.disposed)
    {
        Console.WriteLine("Calculator being disposed");
    }
    this.disposed = true;
}
```

4. On the Debug menu, click Start Without Debugging. Notice that the program displays the following series of messages:

```
Calculator being created
120 / 15 = 8
Calculator being disposed
Program finishing
Calculator being finalized
```

The Calculator object is now discarded only once, but the destructor is still running. Again, this is a waste; there is little point in running a destructor for an object that has already released its resources.

5. In the console window, press the Enter key and return to Visual Studio 2015.

6. In the Calculator class, add to the end of the Dispose method the following statement shown in bold:

Click here to view code image

```
public void Dispose()
{
    if (!this.disposed)
    {
        Console.WriteLine("Calculator being disposed");
    }
    this.disposed = true;
    GC.SuppressFinalize(this);
}
```

The GC class provides access to the garbage collector, and it implements several static methods with which you can control some of the actions it
performs. Using the SuppressFinalize method, you can indicate that the garbage collector should not perform finalization on the specified object, and this prevents the destructor from running.

### Important

The GC class exposes a number of methods with which you can configure the garbage collector. However, it is usually better to let the CLR manage the garbage collector itself because you can seriously impair the performance of your application if you call these methods injudiciously. You should treat the SuppressFinalize method with extreme caution because if you fail to dispose of an object, you run the risk of losing data (if you fail to close a file correctly, for example, any data buffered in memory but not yet written to disk could be lost). Call this method only in situations such as that shown in this exercise, when you know that an object has already been discarded.

7. On the Debug menu, click Start Without Debugging. Notice that the program displays the following series of messages:

```
Calculator being created
120 / 15 = 8
Calculator being disposed
Program finishing
```

You can see that the destructor is no longer running because the Calculator object has already been disposed of before the program finishes.

8. In the console window, press the Enter key and return to Visual Studio 2015.

### Thread safety and the Dispose method

The example of using the disposed field to prevent an object from being discarded multiple times works well in most cases, but keep in mind that you have no control over when the finalizer runs. In the exercises in this chapter, it has always executed as the program finishes, but this might not always be the case—it can run any time after the last reference to an object has disappeared. So it is possible that the finalizer might actually be invoked by the garbage collector on its own thread while the Dispose method is being run, especially if the Dispose method has to do a significant amount of work. You could reduce the possibility of resources being released multiple times by moving the statement that sets the disposed field to true closer to the start of the Dispose method, but in this case you run the risk of not freeing the resources at all if an exception
occurs after you have set this variable but before you have released them.

To completely eliminate the chances of two concurrent threads disposing of the same resources in the same object simultaneously, you can write your code in a thread-safe manner by embedding it in a C# lock statement, like this:

Click here to view code image

```
public void Dispose()
{
    lock(this)
    {
        if (!disposed)
        {
            Console.WriteLine("Calculator being disposed");
        }
        this.disposed = true;
        GC.SuppressFinalize(this);
    }
}
```

The purpose of the lock statement is to prevent the same block of code from being run at the same time on different threads. The argument to the lock statement (this in the preceding example) should be a reference to an object. The code between the curly braces defines the scope of the lock statement. When execution reaches the lock statement, if the specified object is currently locked, the thread requesting the lock is blocked and the code is suspended at this point. When the thread that currently holds the lock reaches the closing curly brace of the lock statement, the lock is released, enabling the blocked thread to acquire the lock itself and continue. However, by the time this happens, the disposed field will have been set to true, so the second thread will not attempt to perform the code in the if (!disposed) block.

Using locks in this manner is safe, but it can impair performance. An alternative approach is to use the strategy described earlier in this chapter, whereby only the repeated disposal of managed resources is suppressed. (It is not exception-safe to dispose of managed resources more than once; you will not compromise the security of your computer, but you might affect the logical integrity of your application if you attempt to dispose of a managed object that no longer exists.) This strategy implements overloaded versions of the Dispose method; the using statement calls Dispose(), which in turn runs the statement Dispose(true), while the destructor invokes Dispose(false). Managed resources are freed only if the parameter to the overloaded version of the Dispose method is true. For more information, refer back to the example in the section “Calling the dispose method from a destructor.”
