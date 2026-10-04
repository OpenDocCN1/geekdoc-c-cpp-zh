The partial keyword indicates that this line is only part of the full class. The rest can be found in the Form1.Designer.cs file listed in Solution Explorer. (Take a look at it.) Later in the “Stuff Happens — C# Events” section, I revisit that file to show you a couple of things about “events.” Partial classes, which were introduced in C# 2.0, let you split a class between two or more files. The compiler generates the Form1.Designer.cs file, so don’t modify its code directly. You can modify it indirectly, however, by changing elements on the form. Form1.cs is your part.

# Tracking the delegate life cycle

Look at the example through the parts of the delegate life cycle:

+   1. You define the UpdateProgressCallback delegate near the top of the class:

```
delegate void UpdateProgressCallback();
```

Methods that this delegate can “point” to will be void, with no parameters. After the delegate keyword, the rest defines the signature of any method that the delegate can point to: its return type and the number, order, and types of its parameters. Delegates don’t have to be void — you can write delegates that return any type and take any arguments.

Defining a delegate defines a type, just as class Student {...} does. You can declare your delegate public, internal, protected, or even private, as needed.

It’s considered good form to append the name Callback to the name of a delegate type that defines a callback method, though C# couldn’t care less.

![](bbox=[0.13, 0.58, 0.21, 0.68])

+   2. You instantiate the delegate and then pass the instance to the DoSomethingLengthy() method in the button1_Click() method:

```
UpdateProgressCallback callback =
    new UpdateProgressCallback(this.DoUpdate); // Instantiate the delegate.
DoSomethingLengthy(callback); // Pass the delegate instance to a method.
```

This delegate “points” to a method on this class (and this is optional). To point to a method on another class, you need an instance of that class (if the method is an instance method), and you pass the method like this:

```
SomeClass sc = new SomeClass();
UpdateProgressCallback callback =
    new UpdateProgressCallback(sc.DoUpdate);
```

![](bbox=[0.12, 0.75, 0.2, 0.85])

But if the method is a static method (located anywhere), pass it like this:

```
UpdateProgressCallback callback =
    new UpdateProgressCallback(SomeClass.DoUpdate);
```