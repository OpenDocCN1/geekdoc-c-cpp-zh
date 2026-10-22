
## Dynamic Keyword

Dynamic is an object type, but it bypasses compiler type checks. We can give anything to a dynamic variable and not be perplexed about the compiler or the type. It uses the power of DLR, which is an extension of CLR. Although bypassing compiler checks is simple, it could potentially lead to unexpected behavior if not used cautiously. We don’t need to cast dynamics before trying out different operations explicitly.

```csharp
dynamic testDynamic = 10;
testDynamic = testDynamic + 25;
```

RuntimeBinderException is the exception we could get at execution time if a dynamic type fails to sort out the operation we provided on a type that doesn’t support it.

To put it in simple terms, imagine you are trying to do something on a static type and that static type doesn’t implement that behavior.

Like trying to increment a string. Or calling .Split() on an integer.

It’s not that easy, though, and there is some problem that we must be aware of. For example, calling the Count() on a dynamic object that has been given ICollection:

```csharp
public static void
ExamplePrintCount(ICollection collection)
{
    dynamic d = collection;
    Console.WriteLine("Static typing: {0}",
        collection.Count);
    Console.WriteLine("Dynamic typing: {0}",
        d.Count);
}
```

If we run this example by giving it an int array:

```csharp
ExamplePrintCount(new int[20]);
```

What do you imagine about the result?

Suppose you guessed that the first Console.WriteLine() will output 20, and that we’ll get RuntimeBinderException in the second one, you thought correctly.

this book, but, as for now, you can think of object-oriented languages as languages that have properties and are able to perform actions. This book covers the concepts of object-oriented programming through a real-world example. Then you will dive into advanced-level concepts such as generics and collections and get acquainted with objects and LINQ. Toward the end, you will work with application components that illustrate all the concepts explained in this book.

This book takes a unique and practical approach to teach C# to absolute beginners. It begins by teaching you the basic fundamentals and gets you acquainted with C# programming by introducing important features and nuances of the language in a hands-on way, helping you grasp the concepts in a fluid manner.

We will start by examining primitive types and variables in C#—what they are and how to work with them. First, we will review all the data types—integer types, real floating-point types, Boolean, character types, strings, and object types. We will continue with variables, their characteristics, how to declare them, how they are assigned a value, and what variable initialization is. It is also important to familiarize oneself with the main categories of data types in C#—value and reference types. We shall also discuss literals, what they are and what kinds of literals there are.

After getting to know the basics of the language, you are expected to spend some time learning arrays as a means for operating on sequences of elements of the same type. This book explains what they are and how we can declare, create, and instantiate arrays to provide access to their elements. You will be able to examine one-dimensional and multidimensional arrays and learn the various ways for iterating through an array, reading from the standard input and writing to the standard output. Many exercises as examples, which can be solved using arrays, will be provided along the way, just to show you how useful these tools can be.

In addition, you will get to know in detail the subroutines in programming, which are called methods in C#. We will describe when and why methods are used; show how methods are declared and what a method signature is. You will learn how to create a custom method and how to invoke it subsequently, using parameters and some established practices when dealing with methods. Again, all of this will be backed up with examples explained in detail.

Going back to the principles of object-oriented programming, be prepared to look into notions of class inheritance, interfaces implementation, data and behavior abstraction, data encapsulation and hiding implementation details, polymorphism, and virtual methods. Not to mention the principles of cohesion and coupling. We will also briefly outline object-oriented modeling and object model creation based on a specific technical problem.

You will also be exposed to some of the more sophisticated capabilities of C#. To be more specific, we will pay special attention to clarifying how to make queries to collections using lambda expressions and LINQ. This book thoroughly explains how to add functionality to already created classes, using extension methods. We will familiarize ourselves with anonymous types and briefly describe their nature and usage. Moreover, we will also review lambda expressions and show in practice how most of the built-in lambda functions work.

This book also includes a section on the popular .NET technology Language Integrated Query (LINQ), which allows execution of various queries (such as searching, sorting, summation, and other group operations) on arrays, lists, and other objects. It is placed toward the end on purpose, after the essential chapters on data structures and algorithms complexity. The reason behind this is that the good programmer should know what happens when they sort a list or search in an array according to criteria and how many operations these actions take. If LINQ is applied, it is not obvious how a given query operates and how much time it takes. LINQ is a very powerful and widely used technology, but it has to be mastered at a later stage, after you are well familiar with the basics of programming, and the main algorithms. Otherwise, you risk learning how to write inefficient code without understanding how it works and how many operations it runs in the background.

As a beginner, there is no need to worry since it is pretty simple to learn C#. Yet, to know C#, you should have at least a basic idea of writing code, even if you have yet to build your first application or program. The learning curve for C# is relatively low when compared to more complex languages.

In case you are looking to start a career in the industry, try checking out a website with job offers for programmers, and you will see for yourself that the demand for C# and .NET specialists is very high. The demand for PHP, C++, and other technology specialists is far lower than that for C# and Java engineers. At the same time, for good, experienced programmers, the language they use is of no significant meaning because they know how to program. Whatever language and technology they might require for the task, they will be able to master it quickly. Therefore, your goal is not only to learn C#, but rather to gain an understanding of programming. After you master the fundamentals of programming and learn to think algorithmically, when you become acquainted with other programming languages, you will see for yourself how much in common they have with C# and how easy it will be to learn them.

Programming is built upon principles that almost never change over the years, and this book teaches you these very principles. You should realize that the essence of programming is to control the work of the computer on different levels. This is done with the help of “orders” and “commands” from the programmer, also known as programming instructions. To “program” means to coordinate the work of the computer through sequences of instructions. These commands are given in written form and are implicitly followed by the computer (respectively by the operating system, the CPU and the peripheral devices). Thus, to “program” means to be able to script multiple sequences of instructions in order to organize the work of the computer to achieve something as a result. These sequences of instructions are called “computer programs” or “scripts.”

A sequence of steps to achieve or complete some work, or get a certain result, is called an algorithm. This is how programming is related to algorithms.

To put it simply, programming involves describing what you want the computer to do by a sequence of steps. And programmers are the professionals who create these instructions, which control computers. These instructions
