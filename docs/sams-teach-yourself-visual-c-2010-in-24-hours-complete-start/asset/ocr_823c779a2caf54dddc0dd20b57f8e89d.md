You should perform argument checking to prevent an `IndexOutOfRangeException` or `NullReferenceException` from occuring.

# # Throwing Exceptions

You throw an exception using the `throw` keyword. Because `Exception` is a class, you must create an instance of it using the `new` keyword. The following code throws a new `Exception` object:

```
```csharp
throw new System.Exception();
```
```

When an exception is thrown, program execution immediately halts while the exception propagates up the call stack, looking for an appropriate handler. If no handlers are found, one of three things happens:

+   * If the exception occured within a destructor, that destructor is aborted, and if present, the destructor of the base class is called.
* If a static constructor or static field initializer is contained in the call stack, a `TypeInitializationException` is thrown containing the original exception in the `InnerException` property.
* If the start of the thread is reached, the thread is terminated. In most cases, this means that if the exception reaches all the way to the `Main()` method without finding a compatible handler, the application is terminated. This happens no matter which thread the exception originated from.

Knowing when an exception should be thrown requires understanding the difference between coding errors and execution errors. Coding errors can be avoided by changing your code, and there is no reason to handle these using exceptions. Coding errors can be fixed at compile-time, and you can take steps to ensure they never occur at runtime.

![](bbox=[0.11, 0.76, 0.79, 0.91])

> Did you know?