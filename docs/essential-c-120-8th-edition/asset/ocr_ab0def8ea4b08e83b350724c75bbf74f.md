# Chapter 5: Parameters and Methods

the calling code a little more complex, because it would be necessary to construct an array to pass as an argument.

To make it easier for the callers of such a method, C# provides a keyword that enables the number of arguments to vary in the calling code instead of being set by the target method. Before we discuss the method declaration, observe the calling code declared within Main(), as shown in Listing 5.21 with Output 5.7.

Listing 5.21: Passing a Variable Parameter List

```
using System;
using System.IO;

public class Program
{
    public static void Main()
    {
        string fullName;

        // ...

        // Call Combine() with four parameters
        fullName = Combine(
            Directory.GetCurrentDirectory(),
            "bin", "config", "index.html");
        Console.WriteLine(fullName);

        // ...

        // Call Combine() with only three parameters
        fullName = Combine(
            Environment.SystemDirectory,
            "Temp", "index.html");
        Console.WriteLine(fullName);

        // ...

        // Call Combine() with an array
        fullName = Combine(
            new string[] {
                $Environment.GetFolderPath(Environment.SpecialFolder.UserProfile),
                "Documents",
                "Web", "index.html"
            });
        Console.WriteLine(fullName);
        // ...
    }
}
```