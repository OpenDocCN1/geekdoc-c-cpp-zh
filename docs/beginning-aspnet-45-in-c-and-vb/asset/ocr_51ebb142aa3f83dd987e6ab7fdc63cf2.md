# OBJECT ORIENTATION BASICS

A chapter about writing code in ASP.NET wouldn't be complete without a section on *object orientation (OO)*. Object orientation, or object-oriented programming, is a highly popular style of programming where the software is modeled as a set of objects interacting with each other. Object orientation is at the heart of the .NET Framework. Literally everything inside the framework is an object, from simple things like integers to complex things like a DropDownList control, a connection to the database, or a data-driven control.

Because object orientation is such an important aspect of .NET, it's important to be familiar with the general concepts of object-oriented programming. At the same time, you don't have to be an expert on OO to be able to build websites with ASP.NET. This section gives you a 10,000-foot overview of the most important terms and concepts. This helps you get started with object orientation, so you can start building useful applications in the next chapter instead of keeping your nose in the books for the next three weeks.

# Important OO Terminology

In object orientation, everything revolves around the concept of objects. In OO everything *is*, in fact, an object. But what exactly is an object? And what do classes have to do with them?

# Objects

*Objects* are the basic building blocks of object-oriented programming languages. Just like in the real world, an object in OO-land is a thing, but stored in the computer's memory. It can be an integer holding someone's age or an open database connection to a SQL Server located on the other side of the world, but it can also be something more conceptual, like a web page. In your applications, you create a new object with the New (new in C#) keyword, as you saw with the calculator example. This process of creating new objects is called *instantiating* and the objects you create are called instances. You can instantiate complex or custom types like Calculator, as well as simple types like Integers and Strings:

```
VB.NET
Dim myCalculator As Calculator = New Calculator()

Dim age As Integer = New Integer()
```

```
C#
Calculator myCalculator = new Calculator();

int age = new int();
```

Because it's so common to create variables of simple types like Integer (int in C#) and String (string in C#), the compiler allows you to leave out the new keyword and the assignment. Therefore, the following code is functionally equivalent to the preceding age declaration:

```
VB.NET
Dim age As Integer
```

```
C#
int age;
```