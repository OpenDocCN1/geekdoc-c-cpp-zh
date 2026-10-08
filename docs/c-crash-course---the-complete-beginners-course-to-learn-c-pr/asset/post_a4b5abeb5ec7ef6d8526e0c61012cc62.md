
```csharp
Console.WriteLine("Animals say Hello");
);
class Lion: Animal
{
    public Lion ()
    {
    }
    public override void Speak()
    {
        Console.WriteLine("A lion roars");
    }
    public override void Speak ( string gender)
    {
        if ( gender == "male")
        {
            Console.WriteLine("The female lion purrs.");
        } else {
            Console.WriteLine("The male lion roars.");
        }
    }
}
```

Notice that we have now added a second method in our Lion class. Notice that this method has the same name as our other Speak method, but the new method takes a gender parameter. This parameter makes a distinction between the main Speak method that takes no parameters and this new method takes a gender parameter. It is called overloading your method, and it's a completely legitimate way to create dynamic classes for your programs.

For basic programming, you know that you can name two methods with the same name, but the only thing you need to change is the number of parameters or the data types that are taken by the parameters. This makes a distinguishable difference that the compiler understands. Therefore, your code won't return an error when it tries to compile your code.

Let's take a look at the code that calls your new overloaded methods and the results that return after you call them.

```csharp
static void Main(string[] args)
{
    Lion l1 = new Lion();
    l1.Speak();
    l1.Speak("male");
}
```

The result from the above code results in the following output:

Animals say hello.
Male lions roar.

The compiler is able to understand and distinguish the difference because each method has a different number of used parameters. The first one has no parameters, and the second one has one string parameter.

# Abstract Classes

You've already seen abstract classes in many of our examples, but we haven't really discussed the differences between an abstract class and how it's significant in your programming projects. Abstract classes are usually the main, top classes for your programs. They contain the similarities among all child classes.

Let's use the Animal class as an example. We have an Animal class for our Lion and Bird classes.

An abstract class is always at the top of the class design. If you take the Animal class as an example, any animal that speaks can derive from the main abstract class.

Polymorphism is an important part of C# coding and OOP programming in general. You'll need to work with this type of coding in almost any major enterprise application. Once you get used to the way these programs work, you can design your own polymorphic coding designs that make your C# code more dynamic and easier to work with.

# Lab Questions

- 1. What type of class is useful as a main top-level class but cannot be instantiated by any other parts of your code?
  - a. private
  - b. abstract
  - c. private
  - d. sealed

**Explanation:** An abstract class is good for a top-level class that defines several child class methods and properties, but it cannot be instantiated by any other parts of your code. Instead, it can only be derived through child classes.

- 2. What type of function uses the same method name as another within a class, but passes different parameters to distinguish it from the main method?
  - a. overridden
  - **b. overloading**
  - c. private
  - d. void

**Explanation:** Function overloading is a way to use a method name that is the same as others in its class without causing errors from the compiler. Methods with the same name but different parameters won't create a compiler error.

- 3. What type of function is used in a child class that derives a parent class method but changes its functionality?
  - a. overridden
  - b. overloading
  - c. private
  - d. void

**Explanation:** Overridden classes change the way a parent class method...

# Chapter 15
# Error Handling

**Objective:** Before you deploy your application, you need to fix any bugs. This chapter focuses on debugging and how you can test your applications before you deploy them to your users and production.

It's always a priority to test an application before you promote it to a production server or deploy it to your users. You can still use a beta testing application before you actually deploy the full version, but even then you should debug your application. One part of debugging is through error handling. Error handling is a way to trap errors and “handle” them for the user. These error handling events display a user-friendly message to the user, so your code doesn't frustrate your users. This chapter discusses how you can manage this type of process within your code.

## Using the Visual Studio Debugger

As mentioned, you need the Visual Studio code editor to create and compile code in C#. Visual Studio includes a debugger that you can use to walk through your code. Is one advantage of working with C# over other languages that don't have a good IDE for programming. C# lets you walk through each of your lines of code, and then you can watch the value of a variable as you walk through these lines of code.

You can start the debugger menu using the F5 key or by using the debugger menu item in your Visual Studio main. You can also set stop points called breakpoints in your code. These breakpoints let pause the compiler and run processes to see what is happening in your code. For instance, suppose you have an error or bug in one of your modules. You're not sure what variable is being set to a value, and you think that this variable is causing the bug in your program. You can set a breakpoint at a certain part of your code to view the value of the variable at a certain point in the run process for your code.

The Visual Studio Watch List is important for this process because it gives you the ability to view variable values in real time. If it weren't for this tool, you would only be able to guess the value of a variable as you worked through your code. The Visual Studio Watch List lets you see the value of a variable as you walk through your code. It's an excellent way to identify if a variable has been given the wrong value, and it lets you identify if you have a logic error in your code. Because logic errors occur during run time, it's useful for your debugging process to consider if you have a logic error in an area such as a loop or an if statement.

## The Try Catch Statement in C#

For error handling, the main component in any .NET language (including C# and VB.NET) is the try catch statement. This statement lets you trap errors and perform a user-friendly function that handles the errors for your users. You don't want to create unfriendly, messy errors for your users. In some cases, these errors can cause security issues for your application. Poorly handled error messages can display information, and in some cases, they can show passwords and user information that can be used for hacking your server—which you don't want displayed to the Internet public. The solution to this issue is to trap your errors and display a user-friendly message that tells your user how to handle the errors without causing them frustration.

Let's first look at the template used to create a try catch statement. We have created a basic template for you to follow.

```csharp
try
{
  // statements causing exception
}
catch(ExceptionName e1)
{
  // error handling code
}
catch(ExceptionName e2)
{
  // error handling code
}
catch(ExceptionName eN)
{
  // error handling code
}
finally
{
  // statements to be executed
}
```

In the code above, we first declare the try statement. This indicates that you're starting the try catch statement.

Each catch statement in the try catch statement catches a different type of error. This part of the statement can be tricky if you don't know what type of errors you should expect, but you should create catch statements that trap any type of error. When the compiler catches these types of statements, then they move into the catch statement block, which is where you create your custom code that handles the errors that you weren't
