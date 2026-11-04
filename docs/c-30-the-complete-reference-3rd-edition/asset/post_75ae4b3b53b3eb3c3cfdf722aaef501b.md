
Object-oriented programming took the best ideas of structured programming and combined them with several new concepts. The result was a different and better way of organizing a program. In the most general sense, a program can be organized in one of two ways: around its code (what is happening) or around its data (what is being affected). Using only structured programming techniques, programs are typically organized around code. This approach can be thought of as “code acting on data.”

Object-oriented programs work the other way around. They are organized around data, with the key principle being “data controlling access to code.” In an object-oriented language, you define the data and the code that is permitted to act on that data. Thus, a data type defines precisely the operations that can be applied to that data.

To support the principles of object-oriented programming, all OOP languages, including C#, have three traits in common: encapsulation, polymorphism, and inheritance. Let’s examine each.

## Encapsulation

Encapsulation is a programming mechanism that binds together code and the data it manipulates, and that keeps both safe from outside interference and misuse. In an object-oriented language, code and data can be bound together in such a way that a self-contained black box is created. Within the box are all necessary data and code. When code and data are linked together in this fashion, an object is created. In other words, an object is the device that supports encapsulation.

Within an object, the code, data, or both may be private to that object or public. Private code or data is known to and accessible by only another part of the object. That is, private code or data cannot be accessed by a piece of the program that exists outside the object. When code or data is public, other parts of your program can access it even though it is defined within an object. Typically, the public parts of an object are used to provide a controlled interface to the private elements.

C#’s basic unit of encapsulation is the class. A class defines the form of an object. It specifies both the data and the code that will operate on that data. C# uses a class specification to construct objects. Objects are instances of a class. Thus, a class is essentially a set of plans that specify how to build an object.

Collectively, the code and data that constitute a class are called its members. The data defined by the class is referred to as fields. The terms member variables and instance variables also are used. The code that operates on that data is contained within function members, of which the most common is the method. Method is C#’s term for a subroutine. (Other function members include properties, events, and constructors.) Thus, the methods of a class contain code that acts on the fields defined by that class.

## Polymorphism

Polymorphism (from Greek, meaning “many forms”) is the quality that allows one interface to access a general class of actions. A simple example of polymorphism is found in the steering wheel of an automobile. The steering wheel (the interface) is the same no matter what type of actual steering mechanism is used. That is, the steering wheel works the same whether your car has manual steering, power steering, or rack-and-pinion steering. Thus, turning the steering wheel left causes the car to go left no matter what type of steering is used. The benefit of the uniform interface is, of course, that once you know how to operate the steering wheel, you can drive any type of car.

The same principle can also apply to programming. For example, consider a stack (which is a first-in, last-out list). You might have a program that requires three different types of stacks. One stack is used for integer values, one for floating-point values, and one for characters. In this case, the algorithm that implements each stack is the same, even though the data being stored differs. In a non-object-oriented language, you would be required to create three different sets of stack routines, with each set using different names. However, because of polymorphism, in C# you can create one general set of stack routines that works for all three specific situations. This way, once you know how to use one stack, you can use them all.

More generally, the concept of polymorphism is often expressed by the phrase “one interface, multiple methods.” This means that it is possible to design a generic interface to a group of related activities. Polymorphism helps reduce complexity by allowing the same interface to be used to specify a general class of action. It is the compiler’s job to select the specific action (that is, method) as it applies to each situation. You, the programmer, don’t need to do this selection manually. You need only remember and utilize the general interface.

## Inheritance

Inheritance is the process by which one object can acquire the properties of another object. This is important because it supports the concept of hierarchical classification. If you think about it, most knowledge is made manageable by hierarchical (that is, top-down) classifications. For example, a Red Delicious apple is part of the classification apple, which in turn is part of the fruit class, which is under the larger class food. That is, the food class possesses certain qualities (edible, nutritious, and so on) which also, logically, apply to its subclass, fruit. In addition to these qualities, the fruit class has specific characteristics (juicy, sweet, and so on) that distinguish it from other food. The apple class defines those qualities specific to an apple (grows on trees, not tropical, and so on). A Red Delicious apple would, in turn, inherit all the qualities of all preceding classes and would define only those qualities that make it unique.

Without the use of hierarchies, each object would have to explicitly define all of its characteristics. Using inheritance, an object need only define those qualities that make it unique within its class. It can inherit its general attributes from its parent. Thus, the inheritance mechanism makes it possible for one object to be a specific instance of a more general case.

## A First Simple Program

It is now time to look at an actual C# program. We will begin by compiling and running the short program shown here:

/*
    This is a simple C# program.
    Call this program Example.cs.
*/

using System;

class Example {
// A C# program begins with a call to Main().
static void Main() {
    Console.WriteLine("A simple C# program.");
}
}

The primary development environment for C# is Microsoft’s Visual Studio. To compile all of the programs in this book, including those that use the new C# 3.0 features, you will need to use a version of Visual Studio 2008 (or later) that supports C#. A good choice for learning C# 3.0 is Visual C# 2008 Express Edition because (at the time of this writing) it is available free of charge from Microsoft. Visual C# 2008 Express Edition contains a full-featured compiler that supports all of C# 3.0 and is, therefore, able to compile all of the code in this book. It also includes Visual Studio, which is Microsoft’s integrated programming environment (IDE). Although the Express Edition does not supply all of the tools that a commercial developer will want, it is perfect for learning C#. At the time of this writing, Visual C# 2008 Express Edition can be downloaded from microsoft.com/express/. All of the code in this book has been tested against this compiler.

Using Visual C#, there are two general approaches that you can take to creating, compiling, and running a C# program. First, you can use the Visual Studio IDE. Second, you can use the command-line compiler, csc.exe. Both methods are described here.

## Using csc.exe, the C# Command-Line Compiler

Although the Visual Studio IDE is what you will probably be using for your commercial projects, some readers will find the C# command-line compiler more convenient, especially for compiling and running the sample programs shown in this book. The reason is that you don’t have to create a project for the program. You can simply create the program and then compile it and run it—all from the command line. Therefore, if you know how to use the Command Prompt window and its command-line interface, using the command-line compiler will be faster and easier than using the IDE.

> > **CAUTION** If you are not familiar with the Command Prompt window, then it is probably better to use the Visual Studio IDE. Although its commands are not difficult to learn, trying to learn both the Command Prompt and C# at the same time will be a challenging experience.

To create and run programs using the C# command-line compiler, follow these three steps:

- 1. Enter the program using a text editor.
- 2. Compile the program using csc.exe.
- 3. Run the program.

## Entering the Program

The source code for programs shown in this book are available at www.mhprofessional.com. However, if you want to enter the programs by hand, you are free to do so. In this case, you must enter the program into your computer using a text editor, such as Notepad. Remember,
