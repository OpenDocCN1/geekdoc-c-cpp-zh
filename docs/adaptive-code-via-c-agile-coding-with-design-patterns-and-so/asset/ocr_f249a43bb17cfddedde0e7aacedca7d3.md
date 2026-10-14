![](bbox=[0.23, 0.007, 0.76, 0.39])

# FIGURE 2-3 The referenced assemblies for any project are listed under its References node.

The bin directory contains the SimpleDependency.exe file, but it also contains the MessagePrinter.dll file. This was copied into the bin directory by the Visual Studio build process because it was referenced as a dependency by the executable. I want to show you an experiment, but first a slight modification to the code is needed. Because this is a console application that does nothing, it will initialize and shut down before you have any time to react. Open the console application’s Program.cs file.

Listing 2-1 shows the addition (in bold) inside the Main method. This is the entry point to the application that currently does nothing and exits quickly. By inserting a call to Console.ReadKey(), you ensure that the application waits for the user to press a key before it terminates.

# LISTING 2-1 The call to ReadKey prevents the console application from exiting immediately.

Click here to view code image

```
namespace SimpleDependency
{
    class Program
    {
        static void Main()
        {
            Console.ReadKey();
        }
    }
}
```