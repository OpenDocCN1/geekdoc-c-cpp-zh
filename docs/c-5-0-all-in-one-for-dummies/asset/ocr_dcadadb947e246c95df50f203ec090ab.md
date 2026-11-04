# Book 1  
Chapter 9  
**Some Exceptional Exceptions**

What if `SomeOtherMethod()` had thrown a simple `Exception` or another non-`CustomException` type of exception? It would be like trying to catch a football with a baseball glove — the catch doesn’t match the throw.

Fortunately, C# enables the program to define numerous catch clauses, each designed for a different type of exception. Assuming that this is the right place to handle the other exceptions, you can tack on one after another.

Don’t be alarmed by my use of the word *numerous*. In practice, you don’t use many catch blocks in one place.

![](bbox=[0.121, 0.201, 0.205, 0.275])

Multiple catch clauses for different exception types must be lined up nose to tail after the try block. C# checks each catch block sequentially, comparing the object thrown with the catch clause’s argument type, as shown in this chunk of code:

```
public void SomeMethod()
{
    try
    {
        SomeOtherMethod();
    }
    catch(CustomException ce)   // Most specific exception type
    {
        // All CustomException objects are caught here.
        // You could insert other exception types between these two.
    }
    catch(Exception e)   // Most general exception type
    {
        // All otherwise uncaught exceptions are caught here.
        // Not that you should always do so -- but then it makes sense ...
    }
}
```

Were `SomeOtherMethod()` to throw an `Exception` object, it would pass over the `catch(CustomException)` because an `Exception` isn’t a type of `CustomException`. It would be caught by the next catch clause: the `catch(Exception)`.

![](bbox=[0.122, 0.695, 0.207, 0.765])

Always line up the catch clauses from most specific to most general. Never place the more general catch clause first, as in this fairly awful bit of code:

```
public void SomeMethod()
{
    try
    {
        SomeOtherMethod();
    }
    catch(Exception e)   // Most general first -- not good!
    {
        // All exceptions are caught here.
        // The dingo ate everything.
    }
    catch(CustomException ce)
```