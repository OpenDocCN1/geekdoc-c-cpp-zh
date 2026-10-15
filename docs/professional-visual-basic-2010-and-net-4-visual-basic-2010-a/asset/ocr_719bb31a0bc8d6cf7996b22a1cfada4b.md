This code creates a new instance of TheClass. You gain access to this new object via the obj variable. This variable holds a reference to the object. You might then do something like this:

```
Dim another As TheClass
another = obj
```

Now, you have a second variable, another, which also has a reference to the same object. You can use either variable interchangeably, as they both reference the exact same object. Remember that the variable you have is not the object itself but just a reference, or pointer, to the object.

# Dereferencing Objects

When you are done working with an object, you can indicate that you are through with it by *dereferencing* the object. To dereference an object, simply set the object reference to Nothing:

```
Dim obj As TheClass

obj = New TheClass()
obj = Nothing
```

After any or all variables that reference an object are set to Nothing, the .NET runtime knows that you no longer need that object. At some point, the runtime destroys the object and reclaims the memory and resources it consumed. You can find more information on the garbage collector in Chapter 4.

Between the time when you dereference the object and the time when the .NET Framework gets around to actually destroying it, the object simply sits in the memory, unaware that it has been dereferenced. Right before .NET destroys the object, the Finalize method is called on the object (if it has one).

# Early Binding versus Late Binding

One of the strengths of Visual Basic has long been that it provides access to both early and late binding when interacting with objects. *Early binding* means that code directly interacts with an object by directly calling its methods. Because the Visual Basic compiler knows the object’s data type ahead of time, it can directly compile code to invoke the methods on the object. Early binding also enables the IDE to use IntelliSense to aid development efforts by enabling the compiler to ensure that you are referencing methods that exist and are providing the proper parameter values.

*Late binding* means that your code interacts with an object dynamically at runtime. This provides a great deal of flexibility because the code doesn’t care what type of object it is interacting with as long as the object supports the methods you want to call. Because the type of the object is not known by the IDE or compiler, neither IntelliSense nor compile-time syntax checking is possible, but in exchange you get unprecedented flexibility.

If you enable strict type checking by using Option Strict On in the project’s Properties dialog or at the top of the code modules, then the IDE and compiler enforce early binding behavior. By default, Option Strict is turned off, so you have easy access to the use of late binding within the code. Chapter 1 discusses Option Strict. You can change this default directly in Visual Studio 2010 by selecting Tools ➜ Options from the VS menu. The Options dialog is shown in Figure 2-12. Expanding the Projects and Solutions node reveals the VB defaults. Feel free to change any of these default settings.

![](bbox=[0.525, 0.674, 0.932, 0.864])

**FIGURE 2-12**

# Implementing Late Binding

Late binding occurs when the compiler cannot determine the type of object that you’ll be calling. This level of ambiguity is achieved using the Object data type. A variable of data type Object can hold virtually any