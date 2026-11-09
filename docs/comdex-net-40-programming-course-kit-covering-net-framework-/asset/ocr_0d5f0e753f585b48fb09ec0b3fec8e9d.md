8. Press the F5 key on the keyboard to run the application. The output of the application appears, as shown in Fig.C#-2.10:

![](bbox=[0.398, 0.171, 0.625, 0.281])

Fig.C#-2.10

You have learned how to work with interfaces in C#. Let’s now understand how C# implements the concept of polymorphism.

# Implementing Polymorphism

Polymorphism means one name, many forms. In other words, polymorphism can be explained as one entity having multiple forms. Polymorphism is an important feature of OOP. By using the feature of polymorphism, you can create multiple methods having the same name. For example, suppose you have to write a program that calculates the area of a circle, triangle, and rectangle. With the polymorphism feature, you can create three different methods with the same name, Area, to calculate the area of a circle, triangle, and rectangle. The number and types of parameters and the return types of the methods may be different. Polymorphism provides various advantages, which are as follows:

+   - Helps classes to provide different implementations for methods that are called using the same name
+   - Helps you to call a method of a class regardless of the specific implementation of the method
+   - Allows you to invoke methods of a derived class through the base class reference at run time

In C#, polymorphism is of the following two types:

+   - Compile-time polymorphism
+   - Run-time polymorphism

Let’s discuss each of these polymorphism types, one by one.

# Compile-Time Polymorphism

When a compiler compiles a program, the compiler has the information about the method arguments. Accordingly, the compiler binds the appropriate method to the respective object at the compile time itself. This process is called compile-time polymorphism or early binding. You can implement compile-time polymorphism through overloaded methods and operators. The arguments passed to the methods are matched in terms of number, type, and order; and then the overloaded methods are invoked.

Compile-time polymorphism can be implemented by using two methods:

+   - Method Overloading
+   - Operator Overloading

Let’s discuss each of these, one by one.

# Method Overloading

When the methods defined in a class behave according to the number and types of parameters passed to them, then they are called overloaded methods and this behavior of methods is called method overloading. When you overload a method, then the overloaded version of the method that is called by a method call at run time is determined by the signature with which the method is called. A method signature comprises the following attributes:

+   - The name of the method
+   - The number of parameters passed to the method