# 224 Defining and Using Method

WriteLine() are used in nearly every example in this book, and they're methods.

**Note:** The distinction between static and nonstatic members is important. I cover part that story in this minibook and continue with more detail in Chapter 4 of focus on nonstatic, or instance, methods.

![](bbox=[0.138, 0.246, 0.223, 0.335])

To invoke a nonstatic — method, you need an instance of the class. To invoke a static — class — method, you call the class name, or an instance. The following code snippet assigns a value to the object data anInt and the class, static member staticInt:

```
example = new Example(); // Create an instance of class Example.
example.anInt = i; // Initialize instance member through instance.
example.staticInt = 2; // Initialize class member through class.
```

The following snippet defines and accesses InstanceMethod() and ClassMethod() in the same way:

```
example = new Example(); // Create an instance.
example.InstanceMethod(); // Invoke the instance method
// with that instance.
example.ClassMethod(); // Invoke the class method with the class.
// The following lines won't compile:
example.ClassMethod(); // Can't access class methods via an instance.
example.InstanceMethod(); // Can't access instance methods via a class.
```

![](bbox=[0.138, 0.538, 0.223, 0.627])

Every instance of a class has its own, private copy of any instance members. But all instances of the same class share the same class members — both data members and methods — and values.

The expression.InstanceMethod() passes control to the code contained within the method. Example.ClassMethod(). Executing the line just shown (after commenting the last two lines, which don't compile) generates this output:

```
this is an instance method
this is a class method
```

![](bbox=[0.138, 0.74, 0.223, 0.829])

After a method completes execution, it returns to the point where it was called. That is, control moves to the next statement after the call.

The bit of C code used in the two sample methods does nothing more than writing a string to the console, but methods generally perform useful (sometimes complex) operations such as calculates concatenate two strings, sort an array of students, or surreptiously e-mail your URL to Microsoft (not really). A method can be as large and complex as you want, but to strive for shorter methods, using the approach described next.