In C and C++ function pointers are variables that directly refer to the memory location (address) of a function, which can be invoked by a function pointer. Delegates, in C# are similar to function pointers. C# delegates are object-oriented, type-safe function pointers that refer to a static or an instance method. Delegates are reference types and can be used to hold references for more than one method.

Events in C# are used to notify the user that some action has occurred, such as a mouse button has been clicked or a keyboard key has been pressed. Whenever an event is fired, an event handler to handle the event is automatically invoked. This event handling is implemented through delegates in C#.

In this chapter, you learn to work with delegates and creating single-cast and multi-cast delegates. You also learn about the event-handling mechanism in C# and the lambda expression and anonymous methods. Now, let's first start discussing how to work with delegates in the next section.

# Working with C# Delegate Types

At times you may need to pass a method as a parameter to some other method. In such a situation, you can use a delegate, as it enables the developers to encapsulate a reference to a method within the delegate object. After you assign a method to a delegate, its behavior resembles that of the method. You declare a delegate in C# using the delegate keyword. The following is the syntax to declare a delegate:

```
delegate return_type delegate_name(parameter_list);
```

All delegate types are sealed and derived from the Delegate class. In other words you cannot define your own classes from the Delegate class. Following are the steps to use a delegate:

+   - Declare a delegate.
+   - Instantiate a delegate object by assigning it to a specific method.
+   - Invoke the delegate object by passing a single argument or a list of arguments in parenthesis.

# Note

> Delegates are type-safe because if you pass a method to a delegate whose signature does not match with the signature of the delegate, then, you get a compile-time error.

Now, let's learn to create a single-cast delegate in the next section.

# Creating Single-Cast Delegates

The delegates that refer to a single method are known as single-cast delegates. A single-cast delegate can be declared by using the keyword, delegate followed by the return type and name of the delegate. The syntax to define a single-cast delegate is as follows:

```
delegate return_type delegate_name();
```

You can prefix the delegate declaration with public and internal access modifiers. The following code snippet shows a single-cast delegate declaration using the public access modifier:

```
public delegate int MyDelegate(int a);
```