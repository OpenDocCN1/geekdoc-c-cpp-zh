

options available from Microsoft, the best of which is Visual Studio. This program can be used for working on all the aspects of the .NET framework. This is certainly a highly advanced program and is available in a range of editions. The complete Visual Studio does cost quite a bit and may be too advanced even for hobbyists.

On the release of the .NET framework, Express versions of the product were introduced by Microsoft. These versions are meant for hobby programmers and those who are just starting with the .NET framework. The Express versions will only work for a single language. They may not have the most advanced features of Visual Studio, but they are free. They are also quite easy to use for learning the language of your choice which is C# in this case.

There are some other third-party editors available in the market. However, for this book, we will be using Visual C# Express for writing the code. You must remember that the codes will remain the same irrespective of the editor you are using.

## Chapter 2

### Hello World: Writing Your First C# Program

If you have learned or dabbled in any programming language previous to C#, you will be familiar with “Hello, world!” This is a basic example that demonstrates the programming language in action. This is exactly what you will be learning in this chapter.

This programming example will illustrate the fundamentals of the programming language. You will come across a few functions and classes that you will surely be using later while writing more advanced codes.

### Starting a New Project

To start a new C# project, you should first open Visual C# Express. In the File menu, select the New Project option. The project dialog will open where you should choose the Console application. This will be the most basic application type that you can find on a system running Windows. Click on the Ok option so that Visual C# Express can create the new project for you.

You will also notice the creation of a file that has been named as Program.cs. This will be the application file where you will be writing the code. You will notice that the file already has a few lines of code as shown below.

```
using System;

using System.Collections.Generic;

using System.Text;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

These lines of code will most certainly work, but the end result is nothing at all. You can run the application if you want by pressing the F5 key. This will cause Visual C# Express to compile and then execute your code. On execution, a black

window will be launched which will then close again. This is simply because the application does not have any other functions to perform.

In order to make this program actually do something, you need to insert a couple of lines of code. You should enter the following two lines inside the last set of {}.

```
Console.WriteLine ("Hello, world!");
```

```
Console.ReadLine ();
```

On entering the lines, your entire program should resemble the following.

```
using System;
using System.Collections.Generic;
using System.Text;
namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
```

```
Console.WriteLine("Hello, world!");
Console.ReadLine();
}
}
}
```

In order to run this program, you should press F5 again. If there are no mistakes, you will notice that the black window remains instead of closing. In the window, you will notice the message “Hello, world!” displayed. Of course, this is the phrase that you entered into the application.

There is a reason why C# is considered to be a very user-friendly programming language. That reason is that it is easy to understand much of the code even if you have never written programs in it before. You will easily notice this in the program that you just wrote.

### Understanding the ‘Hello, world!’ Program

The previous application was just an example of how you can write a program in C#. Of course, you need to understand as to how it actually worked and what does the code actually mean. This is what you will be learning in this section.

To understand the program, consider the ‘{’ and ‘}’ first. After all, they are repeated multiple times in the program. They are known as curly braces. In C#, these braces signify the start and

the end of a logical section of code. You will notice that these braces are often used in a range of other programming languages such as Java and C++ among others. As the example demonstrates, their main function is to bring together several lines of code that belong together.

```
using System;
```

```
using System.Collections.Generic;
```

```
using System.Text;
```

If you are using Visual C# Express, you will notice that the term ‘using’ has been highlighted in blue. This is actually a keyword, and its function is to import a namespace. A collection of classes is known as the namespace. It is the job of Classes to provide you with certain functionalities automatically.

When you are working on an advanced IDE such as Visual C# Express, the keyword, ‘using’ will end up creating parts of the trivial code in your stead. In this example, it was used for creating a class for you. It also imported the namespaces that are necessary or are expected to be used.

In this example, three namespaces have been imported into the program. Each of these namespaces contains some useful classes. The Console class has been used in this program, and it belongs to the System namespace.

You will also notice that the application gets its very own namespace as shown below.

### 'Namespace' ConsoleApplication1

This is now the primary namespace for this application. By default, any new classes created will become a part of it. It is possible to modify this and create other classes under another namespace. If you want to do so, you need to import this namespace into your application with the help of the ‘using’ statement.

For the next step, the class has to be defined. C# is an objected oriented language. As a result, all lines of code which actually performs something will have to be kept inside a class. For this example, the class has been named Program as shown below.

### 'Class' Program

It is possible to increase the number of classes in the same application. However, that was not necessary for this program. A class is capable of containing a number of methods, properties, and variables. However, that will be discussed later. In this program, there is only a single method which is declared as follows.

### 'Static void Main' (string [] args)

The first word of this line is static, and it is a keyword. It instructs the program to keep the method accessible without causing the class to instantiate. The void keyword tells the

program what should be returned by the program which in this case is nothing.

The word, Main, is simply the name given to this method. In this case, it serves as what is known as the entry-point of the application. In other words, this will be the first section of the code that will be executed in the program.

After the name of the method has been declared, it is possible to specify a set of arguments with the help of parentheses. In this example, args is the only argument used by the method.

The next two lines are the actual program. In the first line, the Console class is used to deliver the text as output by means of the ‘WriteLine’ command. Of course, the text is, in this case, ‘Hello, world!’ The second line reads the line of text shown in the console through the ‘ReadLine’ command.

The ReadLine command is essential as it allows the window to remain open. Without it, the application would simply run and end. The window will be closed before you can see the output. The main function of this command is to make the application wait for some input from the user. In this example, you will find that you can enter text after the text has been displayed. On pressing Enter, the window will close and, thereby, bring an end to the program.

