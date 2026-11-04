# About try blocks

Think of using the try block as putting the C# runtime on alert. If an exception pops up while executing any code within this block, hang a lantern in the old church tower (one if by land, two if by sea — or, call 911).

Then, if any line of code in the try block throws an exception — or if any method called within that method throws an exception, or any method called by those methods does, and so on — try to catch it.

Potentially, a try block may "cover" a lot of code, including all methods called by its contents. Exceptions can percolate up (sometimes a long way) from the depths of the execution tree. We show you examples.

# About catch blocks

A try block is usually followed immediately by the keyword catch, which is followed by the catch keyword's block. Control passes to the catch block in the event of an error anywhere within the try block. The argument to the catch block is an object of class Exception or, more likely, a subclass of Exception.

If your catch doesn't need to access any information from the exception object it catches, you can specify only the exception type:

```
```
catch(SomeException) // No object specified here (no 'Exception e')
{
  // Do something that doesn't require access to exception object.
}
```
```

However, a catch block doesn't have to have arguments: A bare catch catches any exception, equivalent to catch(Exception):

```
```
catch
{
}
```
```

![](bbox=[0.1, 0.75, 0.22, 0.85])

We have a lot more to say about what goes inside catch blocks in two articles on http://csharp102.info: "Creating your own exception class" and "Responding to exceptions."

![](bbox=[0.1, 0.85, 0.22, 0.95])

Unlike a C++ exception, in which the object in the catch argument can be any arbitrary object, a C# exception requires that the catch argument be a class that derives from Exception. (The Exception class and its numerous predefined subclasses are defined in the System namespace. Book II, Chapter 10 covers namespaces.)