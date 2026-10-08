# 382 Chapter 8 Arrays; Introduction to Exception Handling

```
d1 = 10.0
d2 = 20.0
d3 = 30.0
d4 = 40.0
```

Average of d1 and d2 is 15.0
Average of d1, d2 and d3 is 20.0
Average of d1, d2, d3 and d4 is 25.0

Fig. 8.23 Using variable-length argument lists. (Part 2 of 2.)

# 8.12 Using Command-Line Arguments

On many systems, it's possible to pass arguments from the command line (these are known as command-line arguments) to an app by including a parameter of type string[](i.e., an array of strings) in the parameter list of Main. By convention, this parameter is named args (Fig. 8.24, line 7). When you execute an app directly from the Command Prompt by changing to the directory containing the app.exe file, typing the file's name (followed by command-line arguments) and pressing Enter, the execution environment passes any command-line arguments that appear after the name of the app's Main method as strings in the one-dimensional array args. The number of arguments passed from the command line is obtained by accessing the app's length property. For example, the command "MyApp a b" passes two command-line arguments to app MyApp. When the preceding command executes, the Main method entry point receives the two-element array args (i.e., args.Length is 2) in which args[0] contains the string "a" and args[1] contains the string "b". Common uses of command-line arguments include passing parameters and options to apps.

```
// Fig. 8.24: InitArray.cs
// Using command-line arguments to initialize an array.
using System;

class InitArray
{
    static void Main(string[] args)
    {
        // check number of command-line arguments
        if (args.Length != 3)
        {
            Console.WriteLine("Error: Please re-enter the entire command, including\n" + "an array size, initial value and increment.");
        }
        else
        {
            // get array size from first command-line argument
            var arrayLength = int.Parse(args[0]);
        }
    }
```

Fig. 8.24 Using command-line arguments to initialize an array. (Part I of 2.)