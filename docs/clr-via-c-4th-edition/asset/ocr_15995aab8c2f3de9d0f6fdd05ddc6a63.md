# # Delegates

In this chapter:

+   - A First Look at Delegates . . . . . . . . . . . . . . . . . . . . . 391
+   - Using Delegates to Call Back Static Methods . . . . . . . . . 394
+   - Using Delegates to Call Back Instance Methods . . . . . . . . 395
+   - Demystifying Delegates . . . . . . . . . . . . . . . . . . . . . . . . . 396
+   - Using Delegates to Call Back Many Methods (Chaining) . . . 400
+   - Enough with the Delegate Definitions Already (Generic Delegates) . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 407
+   - C#'s Syntactical Sugar for Delegates . . . . . . . . . . . . . . . . 408
+   - Delegates and Reflection . . . . . . . . . . . . . . . . . . . . . . . . 416

In this chapter, I talk about callback functions. Callback functions are an extremely useful programming mechanism that has been around for years. The Microsoft .NET Framework exposes a callback function mechanism by using delegates. Unlike callback mechanisms used in other platforms, such as unmanaged C++, delegates offer much more functionality. For example, delegates ensure that the callback method is type-safe, in keeping with one of the most important goals of the common language runtime (CLR). Delegates also integrate the ability to call multiple methods sequentially and support the calling of static methods as well as instance methods.

# ## A First Look at Delegates

The C runtime's qsort function takes a pointer to a callback function to sort elements within an array. In Windows, callback functions are required for window procedures, hook procedures, asynchronous procedure calls, and more. In the .NET Framework, callback methods are used for a whole slew of things. For example, you can register callback methods to get a variety of notifications such as unhandled exceptions, window state changes, menu item selections, file system changes, form control events, and completed asynchronous operations.

In unmanaged C/C++, the address of a non-member function is just a memory address. This address doesn't carry any additional information such as the number of parameters the function expects, the types of these parameters, the function's return value type, and the function's calling convention. In short, unmanaged C/C++ callback functions are not type-safe (although they are a very lightweight mechanism).