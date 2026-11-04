
```csharp
5   // Main method begins app execution
6   static void Main()
7   {
8       // rectangular array of student grades
9       int[,] gradesArray = {{87, 95, 70},
10                           {68, 87, 90},
11                           {94, 100, 90},
12                           {100, 81, 82},
13                           {83, 65, 85},
14                           {78, 87, 65},
15                           {85, 75, 83},
16                           {91, 94, 100},
17                           {76, 72, 84},
18                           {87, 93, 73}};
19
20      GradeBook myGradeBook = new GradeBook(
21         "CS101 Introduction to C# Programming", gradesArray);
22      myGradeBook.DisplayMessage();
23      myGradeBook.ProcessGrades();
24  }
25 }
```

**Fig. 8.22** | Create a GradeBook object using a rectangular array of grades. (Part 2 of 2.)

## 8.11 Variable-Length Argument Lists

Variable-length argument lists allow you to create methods that receive an arbitrary number of arguments. A one-dimensional array-type argument preceded by the keyword *params* in a method's parameter list indicates that the method receives a variable number of arguments with the type of the array's elements. This use of a *params* modifier can occur only in the parameter list's last parameter. While you can use method overloading and array passing to accomplish much of what is accomplished with variable-length argument lists, using the *params* modifier is more concise.

Figure 8.23 demonstrates method Average (lines 8–19), which receives a variable-length sequence of doubles (line 8). C# treats the variable-length argument list as a one-dimensional array whose elements are all of the same type. Hence, the method body can manipulate the parameter numbers as an array of doubles. Lines 13–16 use the foreach loop to walk through the array and calculate the total of the doubles in the array. Line 18 accesses numbers.Length to obtain the size of the numbers array for use in the averaging calculation. Lines 30, 32 and 34 in Main call method Average with two, three and four arguments, respectively. Method Average has a variable-length argument list, so it can average as many double arguments as the caller passes. The output reveals that each call to method Average returns the correct value.

### Common Programming Error 8.7

The *params* modifier may be used only with the last parameter of the parameter list.

```csharp
// Fig. 8.23: ParamArrayTest.cs
// Using variable-length argument lists.
using System;

class ParamArrayTest
{
    // calculate average
    static double Average(params double[] numbers)
    {
        var total = 0.0; // initialize total

        // calculate total using the foreach statement
        foreach (var d in numbers)
        {
            total += d;
        }

        return numbers.Length != 0 ? total / numbers.Length : 0.0;
    }

    static void Main()
    {
        var d1 = 10.0;
        var d2 = 20.0;
        var d3 = 30.0;
        var d4 = 40.0;

        Console.WriteLine(
            $"d1 = {d1:F1}\nd2 = {d2:F1}\nd3 = {d3:F1}\nd4 = {d4:F1}");
        Console.WriteLine($"Average of d1 and d2 is {Average(d1, d2):F1}");
        Console.WriteLine(
            $"Average of d1, d2 and d3 is {Average(d1, d2, d3):F1}");
        Console.WriteLine(
            $"Average of d1, d2, d3 and d4 is {Average(d1, d2, d3, d4):F1}");
    }
}
```

```text
d1 = 10.0
d2 = 20.0
d3 = 30.0
d4 = 40.0

Average of d1 and d2 is 15.0
Average of d1, d2 and d3 is 20.0
Average of d1, d2, d3 and d4 is 25.0
```

Fig. 8.23 | Using variable-length argument lists.

## 8.12 Using Command-Line Arguments

On many systems, it’s possible to pass arguments from the command line (these are known as command-line arguments) to an app by including a parameter of type string[] (i.e., an array of strings) in the parameter list of Main. By convention, this parameter is named

args (Fig. 8.24, line 7). You can execute an app directly from the Command Prompt by changing to the directory containing the app's .exe file, typing the file's name (possibly followed by command-line arguments) and pressing Enter. When you do this, the execution environment passes any command-line arguments that appear after the app name to the app's Main method as strings in the one-dimensional array args. The number of arguments passed from the command line is obtained by accessing the array's Length property. For example, the command "MyApp a b" passes two command-line arguments to app MyApp. You must enter command-line arguments separated by whitespace, not commas. When the preceding command executes, the Main method entry point receives the two-element array args (i.e., args.Length is 2) in which args[0] contains the string "a" and args[1] contains the string "b". Common uses of command-line arguments include passing options and filenames to apps.

```csharp
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
            Console.WriteLine(
                "Error: Please re-enter the entire command, including\n" +
                "an array size, initial value and increment.");
        }
        else
        {
            // get array size from first command-line argument
            var arrayLength = int.Parse(args[0]);
            var array = new int[arrayLength]; // create array

            // get initial value and increment from command-line argument
            var initialValue = int.Parse(args[1]);
            var increment = int.Parse(args[2]);

            // calculate value for each array element
            for (var counter = 0; counter < arrayLength; ++counter)
            {
                array[counter] = initialValue + increment * counter;
            }

            Console.WriteLine($"{"Index"}{"Value",8}");

            // display array index and value
            for (int counter = 0; counter < array.Length; ++counter)
            {
                Console.WriteLine($"{counter,5}{array[counter],8}");
            }
        }
    }
}
```

C:\Users\PaulDeitel\Documents\examples\ch08\fig08_24\InitArray.exe
Error: Please re-enter the entire command, including
an array size, initial value and increment.

C:\Users\PaulDeitel\Documents\examples\ch08\fig08_24\InitArray.exe 5 0 4

| Index | Value |
|-------|-------|
| 0 | 0 |
| 1 | 4 |
| 2 | 8 |
| 3 | 12 |
| 4 | 16 |

C:\Users\PaulDeitel\Documents\examples\ch08\fig08_24\InitArray.exe 10 1 2

| Index | Value |
|-------|-------|
| 0 | 1 |
| 1 | 3 |
| 2 | 5 |
| 3 | 7 |
| 4 | 9 |
| 5 | 11 |
| 6 | 13 |
| 7 | 15 |
| 8 | 17 |
| 9 | 19 |

Fig. 8.24 | Using command-line arguments to initialize an array. (Part 2 of 2.)

Figure 8.24 uses three command-line arguments to initialize an array. When the app executes, if args.Length is not 3, the app displays an error message and terminates (lines 10–15). Otherwise, lines 16–39 initialize and display the array based on the values of the command-line arguments.

The command-line arguments become available to Main as strings in args. Line 19 gets args[0]—a string that specifies the array size—and converts it to an int value, which the app uses to create the array in line 20.

Lines 23–24 convert the args[1] and args[2] command-line arguments to int values and store them in initialValue and increment, respectively—as always, these lines could result in exceptions if the user does not enter valid integers. Line 29 calculates the value for each array element.

The first sample execution indicates that the app received an insufficient number of command-line arguments. The second sample execution uses command-line arguments 5, 0 and 4 to specify the size of the array (5), the value of the first element (0) and the increment of each value in the array (4), respectively. The corresponding output indicates that these values create an array containing the integers 0, 4, 8, 12 and 16. The output from the
