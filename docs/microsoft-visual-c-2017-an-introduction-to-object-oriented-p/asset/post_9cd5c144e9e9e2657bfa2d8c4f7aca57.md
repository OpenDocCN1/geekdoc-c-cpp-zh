
# Writing a C# Program that Produces Output

At first glance, the simplest C# program involves a fair amount of confusing syntax. Consider the simple program in Figure 1-2. This program is written on seven lines, and its only task is to display *This is my first C# program* on the screen.

```csharp
class FirstClass
{
    static void Main()
    {
        System.Console.WriteLine("This is my first C# program");
    }
}
```

**Figure 1-2** FirstClass console application

The statement that does the work in this program is in the middle of the figure:
System.Console.WriteLine("This is my first C# program");
The statement ends with a semicolon because all C# statements do.

The text "This is my first C# program" is *literal string* of characters—that is, a series of characters that will be used exactly as entered. Any literal string in C# appears between quotation marks.

The string "This is my first C# program" appears within parentheses because the string is an argument to a method, and arguments to methods always appear within parentheses. Arguments represent information that a method needs to perform. For example, making an appointment with a dentist’s office was a C# method, you would write the following:
MakeAppointment("September 10", "2 p.m.");

Accepting and processing dental appointment is a method that consists of a set of standard procedures. However, each appointment requires different information—the date and time—and this information can be considered the arguments of the MakeAppointment() method. If you make an appointment for September 10 at 2 p.m., you expect different results than if you make one for September 9 at 8 a.m. or December 25 at midnight. Likewise, if you pass the argument "This is my first C# program", you will expect different results than if you pass the argument

Although an argument to a method may be a string, not all arguments are strings. In this book, you will write and methods that accept many other types of data.

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_37_0.png)

Within the following statement, the method to which you are passing the argument string named WriteLine():

```csharp
System.Console.WriteLine("This is my first C# program");
```

The WriteLine() method is a built-in method that is part of the C# language, and it displays out on the screen and positions the cursor on the next line, where additional output might subsequently be displayed. The Write() method is very similar to the WriteLine() method.

With Write(), the cursor moves to the following line after the message is displayed. Write(), the cursor does not advance to a new line; it remains on the same line as the output. Within the following statement Console is a class that contains the WriteLine() method:

```csharp
System.Console.WriteLine("This is my first C# program");
```

Of course, not all classes have a WriteLine() method (for instance, you can't write line to a computer's mouse, an Automobile, or a Dog), by the creators of C# assumed that you frequently wanted to display output on the screen at your terminal. The Console class created was endowed with the method named WriteLine(). When you use the WriteLine() method, programmers say you can call or invoke it. Soon, you will create your C# classes and endow them with your own callable methods. Within the following statement, System is a namespace:

```csharp
System.Console.WriteLine("This is my first C# program");
```

A namespace is a construct that acts like a container to provide a way to group similar classes. You organize your classes, and (will) create your own namespaces. The System namespace, an advantage is built into your C# compiler, holds commonly used classes.

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_38_0.png)

> Visual Studio that all of its languages use the same namespaces. In other words, every you learn about any namespace in C# is knowledge you can transfer to Visual C++ and Visual Basic.

The dots (periods) in the phrase System.Console.WriteLine are used to separate the names to the namespace, class, and method. You will use this namespace-dot-class-dot-method format repeatedly in your C# programs.

In the FirstClass in 1-2, the WriteLine() statement appears within a method named Main(). Every executable C# application must contain a Main() method because that is the starting point for every program. As you continue to learn C# from this, you will write applications that contain additional methods. You will create classes that are not programs, and do not need a Main() method. For example, a Dog or Automobile class would not be program. Rather would you use classes from which objects are created, and in turn, those objects would be used in programs with a Main() method.

# Writing a C# Program that Produces Output

Every method in C# contains a header and a body. A **method header** includes the method name and information what will pass into and be returned from a method. **A method body** is contained within a pair of curly braces { } and includes all the instructions executed by the method. The program in Figure 1-2 contains only one statement between the curly braces of the Main() method. Soon, you will write methods with many statements.

In Figure 1-2, the `WriteLine()` statement in the `Main()` method is indented between the curly braces. Soon, you will write methods with many statements.

In Figure 1-2, the `WriteLine()` statement in the `Main()` method is indented within the curly braces. Soon, you will write methods with many statements.

In Figure 1-2, the `WriteLine()` statement in the `Main()` method is indented within the curly braces. Soon, you will write methods with many statements.

For opening curly brace { } that encapsulates a method in C#, there must be a corresponding closing brace }. The precision of the opening and closing braces is not important to the compiler. In general, **whitespace** is any combination of spaces, tabs, and carriage returns (blank lines). You use whitespace to organize your program and make it easier to read; it does not affect your program's execution. Usually, you vertically align each pair of opening and closing braces and indent the contents between them, as shown in Figure 1-2.

The method header for the Main() method contains two words. These words are are keywords. In this book, keywords appear in blue. A complete list of keywords appears in Table 1-1 later in this. The method header static void indicates that the method will be executed by a class—not by objects. It means that you do not need to create an object of type `FirstClass` to use the Main() method defined within `FirstClass`. Later in this book, you will create other methods that are nonstatic and are executed by objects.

The second word in the method header in Figure 1-2 is void. In English, the word **void** means empty or having no effect. When the method **void** is used in the Main() method header, it does not return any value, but that the method does not return any value when called. You will learn more about methods that return values (and do affect other methods) when you study methods in greater detail. In the method header, the name of the method is Main(). Main() is not a C# keyword, but all C# applications must include a method named Main(), with additional methods. Recall that when you execute a C# application, the Main() method always executes first. Classes that contain a Main() method are **application classes**. Applications are executable or **runnable**. Classes that do not contain a Main() method are **non-application classes**, and are not runnable. Non-application classes provide support for other classes.

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_39_0.png)
