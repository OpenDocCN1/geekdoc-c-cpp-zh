
By defining a scope, you are keeping it from being accessed or altered by code outside the scope. The scope rules provide the foundation for encapsulation.

Scopes can be nested. For instance, each time you create a block of code, you are creating another, nested scope. When this happens, the outer scope encloses the inner scope. This means that local variables declared in the outer scope will be visible to code inside the inner scope. However, the reverse is not true. Local variables declared inside the inner scope will not be visible outside it.

As the comments demonstrate, the variable `x` is declared at the beginning of `Main()`'s scope and is open to all subsequent code inside `Main()`. Inside the `if` block, `y` is declared. Since a block defines a scope, `y` is visible only to other code inside its block. This is why, outside of its block, the line `y = 100;` is commented out. If you remove the first comment symbol, a compile-time error will happen because `y` is not visible outside of its block. Inside the `if` block, `x` can be used because code inside a block (that is, a nested scope) has access to variables declared by an enclosing scope.

If you come from a C/C++ background, you know that there is no restriction on the names that you give variables declared in an inner scope. Thus, in C/C++, the declaration of `count` inside the block of the outer `for` loop is perfectly legal. However, in C/C++, such a declaration hides the outer `count`. The designers of C# felt that this kind of name hiding could easily lead to programming errors and outlawed it.

Before going into the mechanics of using `ref` and `out`, it is useful to understand why you should pass a value type by reference. In general, there are two reasons: to allow a method to modify the contents of its arguments or to enable a method to return more than one value. Let's take a look at each reason in detail. Often, you will want a method to be able to operate on the actual arguments that are passed to it. The quintessential case of this is a "swap" method that trades the values of its two arguments. Since value types are passed by

In the previous example, a parameterless constructor was used. While this is fine for some circumstances, often you will require a constructor that accepts one or more parameters. Parameters are added to a constructor in the same way that they are added to a method: just declare them inside the parentheses after the constructor's name. Since you know about classes and their constructors, let's investigate the `new` operator. It has this general structure:

```
new class-name(arg-list)
```

Here, `class-name` is the name of the class that is being instantiated. The class name followed by parentheses specifies the constructor for the class, as described in the preceding section. If a class doesn't define its own constructor, `new` will use the default constructor provided by C#. Since memory is limited, it is conceivable that `new` won't be able to allocate memory for an object because not enough memory exists. If this happens, a runtime exception will occur. For the example programs in this book, you won't have to worry about running out of memory, but you should think about this possibility.

The `Instance` property verifies whether the single instance of the `Broadcaster` has been created. If the `Singleton` doesn't exist, then one instance is created and assigned to the private field `instance`. The `Singleton` object is then returned. The result is that the `Broadcaster` contains a reference to an instance of itself.

If you add an `IListener` to the `ArrayList` of listeners, then each time the static method `Broadcast` is called, all listeners who are listening will get the string content. This method can be used to display internal status information, write to a log file, trace your distributed application, or perform a combination of these tasks. (It is recommended that you use `Debug` and `Trace` listeners in conjunction with the `Broadcaster` idiom.) Also, note that the `IEnumerator` is used to iterate the `ArrayList` of listeners.

### Defining the Interface

The `IListener` interface defines two methods: `Listening` and `Listen`. `Listening` is a function that returns a Boolean indicating whether the object implementing the `IListener` interface wants to receive messages. This enables the object to figuratively plug its ears without unregistering from the `Broadcaster`. The `Listen` method is the method that will receive the string content when listening.

You can use the `Broadcaster` by implementing the `IListener` interface. The `FormMain` class implements `IListener` to display broadcast messages in the status bar. In the case of the main form, you can add the form to the list of listeners in the Form's `Load` event. Another good place to add a control is in real programs that you write.

In C#, a variable of a value type contains its own value. Memory to hold this value is automatically allocated when the program is run. Therefore, there is no need to explicitly allocate this memory using `new`. On the other hand, a reference variable stores a reference to an object. The memory to hold this object is allocated dynamically during execution. Not making the essential types, such as `int` or `char`, into reference types significantly improves the performance of your program. When using a reference type, there is a layer of indirection that adds overhead to each object access. This overhead is avoided by a value type.

## Chapter 2: C# Assembly Viewer

This chapter demonstrates how to load assemblies dynamically and inspect those assemblies using Reflection. Working with assemblies and Reflection in just this second chapter is a truly difficult task, but the Assembly Viewer will help you with these topics as well as build Windows applications using controls in the Windows Forms namespace and GDI+.

### Demonstrated Topics:

This chapter's primary point is using dynamic discovery to inspect assemblies using Reflection. If you can dynamically load and use assemblies, you can take advantage of thin client programming by loading assemblies over HTTP connections, which supports automatic deployment and updates of Windows Forms–based applications. There will also be sufficient examples of the following topics:

- Working with value types
- Using the StringBuilder class
- Defining static methods
- Defining classes and inheritance
- Defining and implementing interfaces
- Using the IEnumerator interface
- Multithreading safely in Windows Forms
- Programming with the Graphics object
- Debugging with System.Diagnostics
- Loading data from a resource, which aids internationalization

### Using Statements:

There are two places you will see the `using` keyword. The `using` statement is used to import namespaces and as a block statement for disposing objects.

Listing 2-1 shows how to use namespaces. Consider a `using` statement as adding a reference to a DLL. Assemblies in the framework are actually contained in DLL files; as such, `using System.Reflection;` implies a DLL that starts with the word System.

You can examine assemblies in the .NET Framework by navigating to `C:\WINNT\Microsoft.NET\Framework\v1.0.3705\`.

### Making an Alias with the using Directive

You can create an alias for namespaces with the `using` directive. Changing `using System.Diagnostics;` to `using Diag = System.Diagnostics;` creates an alias named `Diag` for the `System.Diagnostics` namespace. Wherever you would use the fully qualified `System.Diagnostics` namespace, you can replace it with the alias `Diag`.

### Describing a using Scope

The second way `using` is used resembles the `Using` statement in VB.NET. When you use the `using` statement in code with an object, you are defining a scope that will automatically dispose of the object at the end of the `using` block. The object will be disposed of regardless of whether an exception is thrown before the end of the `using` block, as long as the object created in the `using` block implements the `IDisposable` interface.
