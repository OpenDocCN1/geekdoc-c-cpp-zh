
class Printdata
{
    void print(int i)
    {
        Console.WriteLine("Printing int: {0}", i);
    }

    void print(double f)
    {
        Console.WriteLine("Printing float: {0}", f);
    }

    void print(string s)
    {
        Console.WriteLine("Printing string: {0}", s);
    }

    static void Main(string[] args)
    {
        Printdata p = new Printdata();
        // Call print to print integer
p.print(5);

// Call print to print float

p.print(500.263);

// Call print to print string

p.print("Hello C++");

Console.ReadKey();

}

}

}
On executing the code shown above, the following result is achieved.

Printing int: 5

Printing float: 500.263

Printing string: Hello C++

## Dynamic Polymorphism

In this kind of polymorphism, the decision will be taken at the run time. This is implemented by means of method overriding.

With method overriding, it is possible to have methods in the derived and base classes with the same parameters and the same name. As a result, it becomes possible to point to a derived class through a base class’s object at runtime.

The following example illustrates the use of dynamic polymorphism.

```
using System;
namespace PolymorphismApplication
{
	class Shape
	{
		protected int width, height;
		public Shape(int a=0, int b=0)
		{
			width = a;
			height = b;
		}
		public virtual int area()
		{
			Console.WriteLine("Parent class area :");
			return 0;
		}
	}
}
```
}
}

class Rectangle: Shape
{
    public Rectangle( int a=0, int b=0): base(a, b)
    {
    }

    public override int area ()
    {
        Console.WriteLine("Rectangle class area :");
        return (width * height);
    }
}

class Triangle: Shape
{
    public Triangle(int a = 0, int b = 0): base(a, b)
    {
    }

public override int area()
{
    Console.WriteLine("Triangle class area :");
    return (width * height / 2);
}
}
class Caller
{
    public void CallArea(Shape sh)
    {
        int a;
        a = sh.area();
        Console.WriteLine("Area: {0}", a);
    }
}
class Tester
{
    static void Main(string[] args)
{
    Caller c = new Caller();
    Rectangle r = new Rectangle(10, 7);
    Triangle t = new Triangle(10, 5);
    c.CallArea(r);
    c.CallArea(t);
    Console.ReadKey();
    }
    }
}
The result produced after compiling and executing the code shown above is given below.

Rectangle class area:

Area: 70

Triangle class area:

Area: 25

This concludes the chapter on interfaces and polymorphism. Do not worry about using them at the moment. Strengthen your base in C# first.

## Chapter 14

## Learning the Basics of Debugging

Even if you have but a slight idea about computer programming, you should have heard about debugging. This is a vital process for all kinds of software and application programming. You see, there can be errors present in a program. These errors can be as simple as a typing mistake or an incorrect statement. They are all termed as bugs, and they can prevent your program from executing correctly. Therefore these bugs need to be removed, and that is achieved through debugging.

When you are writing simple applications of a few lines such as the examples shown in this book, it is quite easy for you to recognize the errors. You can simply execute the program and find out the bugs. However, with time, you will surely start writing more complex codes that are around hundreds of lines long and filled with complicated statements. Due to the high level of complexity involved, it becomes very difficult to determine the bugs.

In these situations, debugging becomes an extremely useful tool. As a result, you must take your time to understand this tool to become a better programmer. Without it, it is nearly impossible to correct the bugs you can find in the complex code.

## Understanding Print Debugging

The most common type of debugging used is known as print debugging. Although it is the most basic kind of debugging, it is often used by advanced programmers due to its effectiveness in certain situations.

In print debugging, the application is made to print a number or text. This allows you to find out which sections of the code have been executed and what are contained in the variables. In C#, the Console.Write () method can be used for printing a status message or for displaying the contents of a specific variable on the console.

For a few situations, this will be enough. On the other hand, you will have much better tools to use when you are using a good IDE such as Visual Studio or even the Express versions. The good thing is that they are quite easy to use once know the basic principles.

## Introduction to the Breakpoint

The breakpoint is the first thing that you need to learn about debugging. As the name suggests, a breakpoint marks a specific point in the code where its execution will be taking a break. The

application will not be rendered useless. Instead, the breakpoint simply pause the execution of the application.

If you are using Visual Studio or even the Express version, it is quite easy to implement breakpoints. In those IDEs, you will notice that there is a gray area located on the left hand side of the code. This is known as the gutter, and a left click on this area will cause a red circle to appear. This will be the breakpoint, and the debugger will stop the execution of the application at this point.

These are just the basics of debugging. As you advance as a C# programmer, you will automatically come to know about the various other kinds of debugging tools and methods apart from the most complicated aspects of debugging.

C#. Therefore, you should not get fixated on a particular process or technique. It is certainly possible that there are other processes which work better.

## Strengthen Your Base

You may learn to write code, but you must also know how each concept or function comes together to make the code work. In other words, you need to understand the fundamentals and the basics thoroughly. This will enable to you understand why a piece of code works in the way it does and what possible bugs are leading to the problem in the execution. Therefore, you will become a better developer.

## Learn Some Advanced Ideas Extensively

Of course, you shouldn’t expect to master all the advanced techniques and ideas in C# within a few months of starting it. However, it will help your progress greatly if you take the time to learn a few concepts in detail. You should become really good in working with those few concepts. You are free to choose which concepts you want to concentrate on. They can be something that you come across more often during your work or something that interests you greatly. Trying to become an expert in few techniques is easier than trying to master all of them.

## Take a Look at Code Written By Senior Programmers

One of the best ways to learn the concepts and techniques in C# is looking at the codes written by more experienced programmers. If you are working somewhere, you can easily ask the senior programmers to show you their code. Don’t forget to understand why they used a particular technique and how they used it. Alternatively, you can browse through open source projects online. They may not necessarily be topnotch programmers, but you can still learn a lot. Of course, you must avoid blindly imitating what others are doing. Simply understand the idea and try to use it in your own code.

## Conclusion

This marks the end of the book. You now possess the knowledge of the fundamentals of the object oriented programming language known as C#. You have also learned how to write some basic programs in this language and also what you need to start writing.

You can now start using some basic statements and methods in your code. Of course, you have learned how you can declare and define variables. More importantly, you know how you can create classes and even implement inheritance in them to create a hierarchy of code blocks. If you want, you can also start implementing conditional logic in your codes to make it a bit more advanced especially with the help of loops and multiple classes.

The information that you have gleaned from this book will be enough to help you get started with C# programming. Of course, there is a lot more to know and learn. Being a popular programming language, it is continually updated on a regular basis. As such, there will always be something new and exciting to learn. After becoming good at this programming language,
