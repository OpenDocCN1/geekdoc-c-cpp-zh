# 366 A Real-World Example

The partial keyword indicates that this line is only part of the class. The rest can be found in the Form1.Designer.cs file listed in Solution Explorer. (Take a look at it.) Later in this, I revisit it to show you a couple of things about "events". Partial classes, which were introduced in C# 2.0, let you split a class between two or more files. The compiler generates the Form1.Designer.cs file, so don't modify its code directly. You can modify it however, by changing elements on the form.
Form1.cs is your part.

# Tracking the delegate life cycle

Look at the example through the parts of the delegate life cycle:

+   1. You define the UpdateProgressCallback delegate near the top of the class:
```csharp
delegate void UpdateProgressCallback();
```

Methods that delegate can "point" to be void, with no parameters. After the delegate return, defines the signature of any method that the delegate can point to; its return type and the number. Delegates don't have to be void — you can write delegates that return any type and take any arguments.

Defining a delegate defines a type, just as class Student (...) does. You can declare the delegate public, internal, protected, or even private, as needed.

> It's considered good form to append the name Callback to the name of a delegate type that defines a callback method, though C# couldn't care less.

+   2. You instantiate the delegate and pass the instance to the button1_Click() method:
```csharp
UpdateProgressCallback callback = =
new UpdateProgressCallback(this.DoUpdate); // Instantiate the delegate.
DoSomethingLengthy(callback); // Pass the delegate instance to a method.
```

This delegate "points" to this class (and this is optional). To point to another class, you need an instance of that class (if the method is an instance method), and you pass the method like this:

```
SomeClass sc = new SomeClass();
UpdateProgressCallback callback =
new UpdateProgressCallback(sc.DoUpdate);
```

But if the method is a static method (anywhere), pass it like this:

```
UpdateProgressCallback callback =
new UpdateProgressCallback(SomeClass.DoUpdate);
```

![](bbox=[0.135, 0.565, 0.225, 0.795])