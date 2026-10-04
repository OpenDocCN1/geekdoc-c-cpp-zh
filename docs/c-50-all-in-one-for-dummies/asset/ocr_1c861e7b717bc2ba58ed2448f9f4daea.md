The following chunk of code continues the previous code listing. This one adds a new project with one class that contains a Main() method, and you can write code to exercise your library inside Main():

```
// ClassLibrary driver program

// In a separate Console Application project:

// File: Program.cs in ClassLibraryDriver project
using System;
using ClassLibrary;
namespace ClassLibraryExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a library object and use its methods.
            MyLibrary ml = new MyLibrary();
            ml.LibraryFunction1();
            // Call its static methods through the class.
            int result = MyLibrary.LibraryFunction2(27);
            Console.WriteLine(result.ToString());
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
}
```

To run and test the library through the driver, add a reference to the library in the driver project references, mark the driver project as the start-up project (as described earlier, in the “Executables” section), and run the program the same as you run all console applications in this book.

You can test your library in another, even better way, too — using the unit testing features of Visual Studio. Book V has some examples of unit testing, and you can find out more about NUnit at http://csharp102.info.

Here’s the output from the test driver:

```
This is LibraryMethod1()
This is LibraryMethod2(), returning 27
27
Press Enter to terminate...
```

Libraries often provide only static methods. In that case, you don’t need to instantiate the library object. Just call the methods through the class.

# Using a class library from a program

From any program you ever write, just include using directives for your class library’s namespaces and add a reference to the .DLL file that contains the library (providing a path to wherever it lives). Then use the classes in