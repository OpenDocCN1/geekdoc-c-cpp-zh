# Common Programming Error 7.5

![](bbox=[0.153, 0.114, 0.209, 0.163])

Declaring a method outside the body of a class declaration or inside the body of another method is a syntax error.

# Common Programming Error 7.6

![](bbox=[0.153, 0.19, 0.209, 0.239])

Redearing a method parameter as a local variable in the method's body is a compilation error.

# Common Programming Error 7.7

![](bbox=[0.153, 0.256, 0.209, 0.305])

Forgetting to return a value from a method that should return one is a compilation error. If a return type other than void is specified, the method must use a return statement to return a value, and that value must be consistent with the method's return type. Returning a value from a method whose return type has been declared void is a compilation error.

# static Members Can Only Access the Class Members Directly

A static method or property can call only static methods or properties of the class directly (i.e., using the method name itself) and can manipulate only static variables in the same class. To access a non-static member, a static method or property must use a reference to an object of that class. Recall that static methods relate to a class as a whole, whereas non-static methods are associated with a specific object (instance) of the class and may manipulate the instance variables of object (as well as the class's static members).

Many objects of a class, each with its own copies of instance variables, may exist at the same time. Suppose a static method were to invoke a non-static method directly. How would the method know which object's instance variables to manipulate? What would happen if no objects of the class existed at the time the non-static method was invoked?

# Software Engineering Observation 7.3

![](bbox=[0.153, 0.635, 0.209, 0.684])

A static method cannot access non-static members of the same class directly.

# 7.6 Argument Promotion and Casting

Another important feature of method calls is argument promotion—implicitly converting an argument's value to the type that the method expects to receive (if possible) in its responding parameter. For example, an app can call Math method Sqrt with an integer argument even though the method expects to receive a double argument. The statement

```
Console.WriteLine(Math.Sqrt(4));
```

correct evaluates Math.Sqrt(4) and displays the value 2.0. Sqrt's parameter list carries C# to convert the int value 4 to the double value 4.0 before passing the value to Sqrt. Such conversions may lead to compilation errors if C#'s promotion rules are not satisfied. The promotion rules specify which conversions are allowed—that is, which can be performed without losing data. In the Sqrt example above, an int is converted to a