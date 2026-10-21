# Notes

+   1. A virtual destructor to a derived class also invokes the destructor of the base class as the base class subobject buried within the derived class needs it.
+   
+   2. If a base class contains a pure virtual function, all the other classes in the hierarchy must implement it. If a class does not implement it, it automatically becomes an abstract class, in which case it is not possible to have objects of that class.
+   
+   3. Pure virtual functions are doing what interfaces do in Java, that is, forcing descendents to implement the function exactly as specified in the base class.

# 10.9.1 Static Invocation of Virtual Function

Virtual functions can also be invoked statically. When a class name:ptr->virtual function mechanism is used, they are called statically. Consider the base class shape, virtual function draw(), and the derived class circle. Suppose one writes the statements

```
Shape *PtrShape = new Circle;
PtrShape->Shape::draw()
```

In this case, the second statement calls the draw() of Shape class and not of Circle class.

Exhibit 10.3 explains the static evaluation of virtual function content.

# Exhibit 10.3 Static evaluation of a virtual function content

> When we call a function by the syntax
> 
> PointerToBaseClass->BaseClassSubObject::FunctionName
> 
> it is known as the static invocation of the FunctionName.
> 
> For example,
> 
> PtrShape->Shape::draw()
> 
> is the static invocation of draw(). Irrespective of the function being virtual and of where ptrShape is pointing to, the function that belongs to the base class subobject will be called.

Let us now analyse the topic further with the help of an example. It is related to a problem where the classes are arranged using the type of error. Following is the class hierarchy that is to be modelled in the program.

Define a class Error. Should contain error code, description, and possible solutions for the error. Define two derived classes, SyntaxError and LogicalError, inheriting from the base class Error. Define CompilerError and LinkerError classes inheriting from SyntaxError class and LoopingError and InitializationError inheriting from LogicalError class. PossibleSolutions is a function that displays what to do if an error has occurred and is defined in all these classes. Define this function such that given any error, it should display all relevant actions to be performed. That is, if an error is an initialization error, it displays possible solutions for initialization errors as well as possible solutions for logical errors and also for generic errors. Figure 10.3 shows the hierarchy that is observed among the classes. Program 10.8 shows how the solution can be coded.