```
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

This program file is a little more complicated than the one you created earlier, although it does exactly the same thing. Program.cs file defines a class called Program that contains a method called Main. In C#, every executable code must be defined within a method, and all methods must belong to a class or a struct. You'll learn more about classes in Chapter 7, "Creating managing classes and objects," and about structs in Chapter 9, "Creating value types with enumerations and structures."

The Main method designates the program's entry point. This method should be defined in the method specified in the Program class as a static method; otherwise, the .NET Framework might not recognize it as the starting point for your application when you run it. (You'll learn about methods in detail in Chapter 3, "Writing methods and applying scope.") Chapter 7 provides more information on static methods.

At this point, you're probably thinking, "I didn't create a Program class or a Main method" in the previous exercise. In the latest version of C#, if you have a simple application as shown in the first exercise, the C# compiler will create its own Main method, as its name is actually Main.) (You can think of this as a compiler-synthesized Main method, which can save you unnecessary boilerplate code in many cases; just compare the code to the program you wrote in the previous exercise to see what I mean. However, the console application template provided with the .NET always creates a Program class and a Main method. Additionally, other types of applications use a different way of marking the entry point for a program that doesn't utilize a Main method. The templates for these types of applications generate the appropriate startup code. You'll see an example later in this section "Creating a graphical application."

As for the using statement and the namespace definition, you'll learn about these items later in this chapter.