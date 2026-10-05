
| To | Do this |
|---|---|
| Throw an exception | Use a `throw` statement. For example:<br><br>[Click here to view code image](#)\n```throw new FormatException(source);``` | |
| Catch all exceptions in a single `catch` handler | Write a `catch` handler that catches `Exception`. For example:\n```java\ntry {\n  ...\n} catch (Exception ex) {\n  ...\n}\n``` |
| Ensure that some code will always run, even if an exception is thrown | Write the code within a `finally` block. For example:\n```java\ntry {\n  ...\n} finally {\n  // always run\n}\n``` |

# Understanding the C# object model

CHAPTER 7 Creating and managing classes and objects
- 8 Understanding values and references
- CHAPTER 9 Creating value types with enumerations and structures
- CHAPTER 10 Using arrays
- CHAPTER 11 Understanding parameter arrays
- CHAPTER 12 Working with inheritance
- CHAPTER 13 Creating interfaces and defining abstract classes
- CHAPTER 14 Using garbage collection and resource management

In Part I, you learned how to declare variables, use operators to create values, methods, and write many of the statements when you need when to implement a method. You now know enough to progress to the next stage: combining methods and data into your own functional data structures. The chapters in Part II show you how to do this.

In Part II, you'll learn to model the entities and structures, the two fundamental types that use and other items that constitute a typical C# application. In particular, you'll see how C# creates objects and value types based on the definitions of classes and structures, and how .NET manages the life cycle of these items. You'll find out how to create families of classes by using inheritance, and you'll learn how to aggregate items by using arrays.

# Chapter 7

# Creating and managing classes and objects

After completing this chapter, you will be able to:

- Understand the concepts of classification and encapsulation.
- Define a class containing a related set of methods and data items.
- Control the accessibility of members using the `public` and `private` keywords.
- Write and call your own constructors.
- Create methods and data that can be shared by all instances of the same class by using the `static` keyword.
- Create anonymous classes.

Classes provide a convenient mechanism for modeling the entities manipulated by applications. An entity can represent a specific item, such as a customer, or something more abstract, such as a transaction. Part of the design process for any system focuses on determining the entities that are important to the processes that the system implements and then performing an analysis to see what information these entities need to hold and what operations they should perform. You store the information that a class holds as fields and use methods to implement the operations that a class can perform.

> Note
> .NET uses classes extensively. The .NET libraries contain thousands of classes. You have used several of them already, including `Console` and `Exception`.

# Understanding classification

Class is the root word of the term classification. When you design a class, you systematically arrange information and behavior into a meaningful entity. This arranging is an act of classification, and it's something everyone does—not just programmers. For example, all cars share common behaviors (they can be steered, stopped, accelerated, and so on) and common attributes (they have a steering wheel, an engine, and so on). People can use the word car to mean an object that shares these common behaviors and attributes. As long as everyone agrees on a word means, this system works well, and you can express complex but precise ideas in a concise format. Without classification, it's hard to imagine how people could think or communicate at all.

Given that classification is deeply ingrained in the way we think and communicate, it makes sense to write programs by classifying the different concepts inherent in a problem and its solution and modeling these classes in a programming language. This is exactly what you can do with object-oriented programming languages, including Microsoft Visual C#.

# The purpose of encapsulation

Encapsulation is an important principle when defining classes. The idea is that a program that uses a class should not account for how that class actually works internally; the program simply creates an instance of a class and calls the methods of that class. As long as those methods do what they are designed to do, the program doesn't need to know how they are implemented. For example, when you call the Console.WriteLine, you don't want to be bothered with all the intricate details of how the Console physically arranges data to be written to the screen. A class might need to maintain all sorts of internal state information to the program from using the class. This additional state information and activity is hidden. Therefore, encapsulation is sometimes referred to as information hiding. Encapsulation actually has two purposes:

- To combine methods and data within a class—in other words, to support classification
- To control the accessibility of the methods and data—in other words, to control the use of the class

# Defining and using a class

In C#, you use the class keyword to define a new class. The data and methods of the class occur in the body of the class between a pair of braces. Following is a C# class called Circle that contains one method (to calculate the circle's area) and one piece of data (the circle's radius):

Click here to view code image

```
class Circle
{
    int radius;
    double Area()
    {
        return Math.PI * radius * radius;
    }
}
```

> Note
> The Math class contains methods for performing mathematical calculations and fields containing mathematical constants. The Math.PI field contains the value 3.14159265358979, which approximates the value of pi.

The body of a class contains ordinary methods (such as Area) and fields (such as radius). Recall that variables in a class are called fields. Chapter 2, "Working with variables, operators, and expressions," showed how to declare variables, and Chapter 3, "Writing methods and applying scope," demonstrated how to write methods, so there's almost no new syntax here.

You can use the Circle class like you have used the other types you have already met. You can create a variable specifying Circle as its type, and you initialize the variable with some value data. Here is an example:

Click here to view code image

```
Circle c; // Create a Circle variable
c = new Circle(); // Initialize it
```

A point worth highlighting in this code is the use of the new keyword. Previously, when you initialized a variable such as an int or a float, you simply assigned it a value.

```
int i;
i = 42;
```

You cannot do the same with variables of class types. One reason for this is that C# just doesn't provide the syntax for assigning literal class values to variables.

You cannot write a statement such as this:

```
Circle c;
c = 42;
```

After all, what is the Circle equivalent of 42? Another reason concerns the way in which memory for variables of class types is allocated and managed by the runtime. This is discussed further in Chapter 8, “Understanding values and references.” For now, just accept that the new keyword creates a new instance of a class, more commonly called an object.

You can, however, directly assign instance of a class to another variable of the same type, like this:

```
Circle c;
c = new Circle();
Circle d;
d = c;
```

However, this is not as straightforward as it might first appear, for reasons are described in Chapter 8.

> **Important**
> Don't confuse the terms class and object. A class is the definition of a type. An object is an instance of that type created when the program runs. Several different objects can be instances of the same class.

# Type inference and the new operator

In the examples shown in the main body of the text, the class name, Circle, in the new expression is actually superfluous. You can simply write:

```
Circle c;
c = new();
```

The C compiler understands that c is a Circle variable, so it will create a new Circle object by default. Whether you include or omit the type new expression is often a matter of personal preference, but there will be times when you need to specify the type in the new expression. (You'll meet some examples later.)
