> **NOTE** *Errors and exceptions are explained in detail in Chapter 14, “Errors and Exceptions.”*

In such a scenario, you can avoid the problem by iterating the list on your own. The Delegate class defines the method GetInvocationList that returns an array of Delegate objects. You can now use this delegate to invoke the methods associated with them directly, catch exceptions, and continue with the next iteration:

```
static void Main()
{
    Action d1 = One;
    d1 += Two;

    Delegate[] delegates = d1.GetInvocationList();
    foreach (Action d in delegates)
    {
        try
        {
            d();
        }
        catch (Exception)
        {
            WriteLine("Exception caught");
        }
    }
}
```

When you run the application with the code changes, you can see that the iteration continues with the next method after the exception is caught:

```
One
Exception caught
Two
```

# Anonymous Methods

Up to this point, a method must already exist for the delegate to work (that is, the delegate is defined with the same signature as the method(s) it will be used with). However, there is another way to use delegates—with anonymous methods. An anonymous method is a block of code that is used as the parameter for the delegate.

The syntax for defining a delegate with an anonymous method doesn’t change. It’s when the delegate is instantiated that things change. The following simple console application shows how using an anonymous method can work (code file AnonymousMethods/Program.cs):

```
using static System.Console;
using System;

namespace Wrox.ProCSharp.Delegates
{
```