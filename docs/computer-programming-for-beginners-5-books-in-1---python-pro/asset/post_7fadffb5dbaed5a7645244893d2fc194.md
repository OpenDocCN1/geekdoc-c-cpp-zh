
Try to learn in that exact manner. It is important for you to not overwhelm yourself with too much content in a short period of time.

Conversely, don’t allow too much time to lapse before coming back to your work. You may forget subtle nuances that may drive you crazy. Allow yourself to have reasonable expectations, which this book is designed to do.

Lastly, enjoy yourself! Allow yourself to take pride in the new skill you are learning and get ready for a crash course in basic C# mastery!

## Chapter 2: Detailed Overview

Since you are a beginner, we want to focus on building a strong foundation that gives you a full picture of the basics of C#.

Essentially, by the end of the first week you will have a firm grasp on the environment in C#, the program structure, basic syntax and data types, type conversion, variables, constants and operators. If you are unfamiliar with the terminology or methodology used, I will try to give a quick, basic review of the terms. If this does not satisfy jogging your memory, you may need to find a quick refresher from Google or another resource. I would also like to recommend a free interactive shell program you can try out code on - https://www.tutorialspoint.com/compile_csharp_online.php, this should help you complete any training exercises included in the book.

### Environment

As seen, C# was designed to be integrated with Microsoft and .NET Framework by the developers. As one would guess, this is a large influence on the environment you find within C#. An important part of understanding C# comes from the understanding you have of how the two interact with each other. First, here is a brief synopsis of .NET Framework to help you better understand how the two interact.

As the latter part of the name framework suggests, the .NET Framework is a platform in which one can run applications. The .NET Framework is a platform for software development developed by Microsoft. The framework was created for development of applications that can run on the Windows platform. The first version was announced in 2002 and given the name .NET Framework 1.0. Since then, a lot of updates have been made on the framework up to date.

We can use the .NET Framework for creation of both web-based and form-based applications. We can also use it to develop web services. Other than C#, the .NET Framework also supports the Visual Basic programming language. This means that the programmer has the option of choosing the language in which to develop their application in.

There are three different types of applications that the framework can assist you with writing—web services, web applications and windows applications. When one is using the framework applications, it can actually be used by a variety of programming languages, as it is a multi-platform application. The multitude of languages, from Visual Basic, JScript, C++ and COBOL, also have the ability to communicate with each other within the framework. Another great attribute of this framework is the extensive code library that can be used by a language, for our purposes we will be talking about C#.

One of the great things about any language or framework is the potential for a library of codes you can utilize. For the .NET Framework and C#, there is a huge library that you can access and utilize for your coding projects. One advisory statement I always give people is that although these libraries are excellent resources, be sure you understand the hows and whys of the coding itself to ensure that you are able to fix an issue, should it arise.

Microsoft itself also offers a great tool for its users in order to assist their development in their C# programming projects.

There are two excellent ones that the company even offers for free, great resources for writing any kind of application, from simple to complex. The names of the two I would recommend (because of their free price!) are Visual C# 2010 Express and Visual Web Developer.

If these options are not something you feel comfortable with or enjoy using, you can always use a text editor in order to write the source code you may need. I recommend the other options because I find them to be a step up in helpfulness from a simple code editor. However, lots of people prefer that method—it’s really up to you and the comfort level you feel with a program. Test them out and see which methodology works better for you.

You can download the two Microsoft programs I spoke of from a website called Microsoft Visual Studio.

Finally, you can also run C# on Linux or Mac OS, which is a great ability to code across different platforms. However, in order to do so, you obviously need a non-Microsoft framework to do so on your different operating system. I recommend “Mono”—which is an open source option for use on both Linux and Mac.

With the basics of the environment, go download or open the programs you would like to get familiar with to start your coding process. Play around with the software—or you can sleep on your new knowledge and you can pick up your project for the next phase!

### IDE (Integrated Development Environment)

An IDE is a program that allows you to write your program. Most .NET developers prefer using Visual Studio Community as the IDE. It allows you to create, debug and run your applications. This IDE can be used for development of both web-based and form-based applications. To use this IDE, you must download and install it on your computer. You can find it in the URL given below:

https://www.visualstudio.com/downloads/

You are allowed to choose between the Visual Studio Community, which is free, and Visual Studio Professional Edition, which comes with a 30-day trial period, and after the expiry of that period, you must pay for it.

Once the download is complete, double click the setup file to begin the installation of Visual Studio. Follow the on-screen instructions until the installation of Visual Studio is complete.

After that, you will be ready to start creating your own C# applications.

### Program Structure and Basic Syntax

Now that we have established a little about how the environment was created for C#, let’s look at the actual structure and how you will interact with programs through the syntax of C#.

When we are looking at how C# is structured, we are looking at 7 basic components that make up the program. These are class methods and attributes, namespace declaration, a class, a main method, comments, and statements and expressions. Now, what do these look like for you in terms of your programming and coding? Why don’t we take this “Hello World” example and break it down into parts to see this in action.

```csharp
using System;

namespace HelloWorldApplication
```

The code begins with the *using* statement. What this statement does is that it adds the *System* namespace into the program. C# programs normally have multiple *using statements*.

In the next line, we have a *namespace* declaration. A namespace is simply a collection of many classes. Above, we have the *HelloWorld* namespace in which we have the *Hello* class.

In the next line, we have the class declaration. The *Hello* class has method and data definitions that the program will be using. A class normally has numerous methods. The purpose of a method is to state the behavior of a class. However, our *Hello* class above only has one method, the *Main* method.

In the next line of code, we have the definition of the *Main* method, which marks the entry point for all C# programs. It is the *Main* method that states what happens after execution of a class.

Next, we have the `/* ... */` line. This is a comment, and the C# compiler will ignore the line. The line is only meant to increase the readability of the code by human readers.

Next, we have the `Console.WriteLine(...)` line. `WriteLine` is a method that belongs to the `Console` class that is defined in the `System` namespace. This line will print the `Hello World!` message on the screen.

Lastly, we have the `Console.ReadKey();` statement. This line is for `VS.NET` users. The line will make the program wait for a key press and prevent the screen from running and then closing quickly once the program has been launched from Visual Studio .NET.

Other than running the program from Visual Studio, it is possible for you to run a C# program from the command prompt of the operating system. To do this, follow this sequence of steps:

- Open your text editor then add the code given above to it. An example of a text editor is Notepad.
- Save the file with the name *helloworld.cs*.
