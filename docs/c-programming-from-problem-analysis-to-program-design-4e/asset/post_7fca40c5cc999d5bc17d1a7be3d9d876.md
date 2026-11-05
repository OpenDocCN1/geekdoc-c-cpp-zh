
The other methods (`GetNumberStrides()`, `CalculateTime()`, `CalculateAvgSteps()`, and `CalculateDistance()`) all return values back to `Main()`. Instead of having `void` preceding the method name, a data type appears before the method name. This data type describes what will be returned when the method is finished. You also find a `return` statement as the last line in each of these four methods.

Also notice some of the methods have parameters, some do not. The `InputJoggingTime()` method has two special parameters. A method can only return one value through its name. There can also only be one value following a `return` statement. The `InputJoggingTime()` method needs to return hours and minutes both back to `Main()`. Two separate value-returning methods could have been written. Another option is to use the `out` reference type. This essentially gives the address of the hrs and mins to the method. Any changes, like inputting values into the memory location, will be available back in `Main()`. Without the `out` or `ref` parameter type, the values would be lost when control was returned back to `Main()`.

After the algorithm is developed, the design should be checked for correctness. When you desk check your algorithm, begin in `Main()`. When you encounter method calls, keep your location in that method, go to the called method, and perform the statements. When you finish with the called method, return back to your saved location.

Test your algorithm with the following data:

- Steps during 1st minute: 185
- Steps during last minute: 120
- Time spent jogging - Hrs: 1 Min: 12

Use a calculator and write down the results you obtain. After you implement your design, you can compare these results with those obtained from your program output.

## CODE THE SOLUTION

After you complete the design and verify the algorithm’s correctness, it is time to translate the design into source code.

The final application listing for the file appears here:

```csharp
/* JoggingDistance.cs
 * Author: Doyle
 * This application calculates the jogging distance.
 * Users are asked to enter the number of minutes
 * strides ran during the first and last minute
 * and the total jogging time. A 2.5 stride is used
 * for calculation.
 */
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace JoggingDistance
{
    class JoggingDistance
    {
        static void Main(string[] args)
        {
            int initialStrideCount,
                finalStrideCount,
                hrs,
                mins,
                totalMinutes;
            double numberOfStepsPerMin,
                distanceTraveled;

            DisplayInstructions();

            initialStrideCount = GetNumberStrides("first");
            finalStrideCount = GetNumberStrides("last");
            InputJoggingTime(out hrs, out mins);

            totalMinutes = CalculateTime(hrs, mins);
            numberOfStepsPerMin = CalculateAvgSteps(initialStrideCount,
                finalStrideCount);
            distanceTraveled = CalculateDistance(numberOfStepsPerMin,
                totalMinutes);
            DisplayResults(numberOfStepsPerMin, hrs, mins,
                distanceTraveled);
            Console.ReadKey();
        }

        public static void DisplayInstructions()
        {
            Console.WriteLine("How many miles did you jog?");
            Console.WriteLine("Distance (in miles) will be " +
                "calculated");
            Console.WriteLine("based on stride and number of steps");
            Console.WriteLine("taken per minute.\n");
            Console.WriteLine("You will be asked to enter ");
            Console.WriteLine("your initial and ending strides...");
            Console.WriteLine("OR how many steps you took the ");
            Console.WriteLine("first minute and how many ");
            Console.WriteLine("steps during the last minute.");
            Console.WriteLine("Average stride is calculated from ");
            Console.WriteLine("those entries.\n");
            Console.WriteLine("Calculations are based on a ");
            Console.WriteLine("2.5 feet stride-each step is 2.5 " +
                "feet long.");
            Console.WriteLine();
            Console.WriteLine("\nYou will also be asked to enter");
            Console.WriteLine("the length of time (hours and minutes)");
            Console.WriteLine("you jogged.");
            Console.WriteLine();
            Console.WriteLine("Press any key when you are ready " +
                "to begin!");
            Console.ReadKey();
            Console.Clear();
        }

        public static int GetNumberStrides(string when)
        {
            string inputValue;
            int numberOfSteps;
            Console.Write("*Enter number of steps taken " +
                "during {0} minute: ", when);
            inputValue = Console.ReadLine();
            numberOfSteps = int.Parse(inputValue);
            return numberOfSteps;
        }

        public static int CalculateTime(int hrs, int mins)
        {
            return hrs * 60 + mins;
        }

        public static double CalculateAvgSteps(int initialStrideCount,
            int finalStrideCount)
        {
            return (initialStrideCount + finalStrideCount) / 2.0;
        }

        public static void InputJoggingTime(out int hrs, out int mins)
        {
            string inputValue;
            Console.WriteLine("\nHow much time did you spend " +
                "jogging?");
            Console.Write("Hours: ");
            inputValue = Console.ReadLine();
            hrs = int.Parse(inputValue);
            Console.Write("Minutes: ");
            inputValue = Console.ReadLine();
            mins = int.Parse(inputValue);
        }

        public static double CalculateDistance(double numberOfStepsPerMin,
            int totalMinutes)
        {
            const double STRIDE = 2.5;
            const int FEET_PER_MILE = 5280;
            return numberOfStepsPerMin * STRIDE * totalMinutes / FEET_PER_MILE;
        }

        public static void DisplayResults(double numberOfStepsPerMin,
            int hrs, int mins,
            double distanceTraveled)
        {
            Console.Clear();
            Console.WriteLine("{0,35}", "Jogging Distance " +
                "Calculator");
            Console.WriteLine();
            Console.WriteLine("{0,-25} {1} Feet Per Step ",
                "Stride:", 2.5);
            Console.WriteLine("{0,-25} {1} Strides Per Minute:",
                "Strides:", numberOfStepsPerMin);
            Console.WriteLine("{0,-25} {1} Hour(s) and {2} Minute(s)",
                "Jogging Time:", hrs, mins);
            Console.WriteLine("{0,-25} {1:F2} Miles", "Distance " +
                "Traveled:", distanceTraveled);
        }
    }
}
```

## IMPLEMENT THE CODE

Compile the source code. If you have any rule violations, make corrections until no errors are present. Run the application entering the values indicated previously (185, 120, 1, 12).

## TEST AND DEBUG

During this final step, test the program and ensure you have the correct result. The output for the test values should match your prototype. Figure 3-15 shows the output generated from the preceding source code.

![Output from JoggingDistance example](img/36e48639a06772bcb0fa1ea2525b33a3_218_0.png)

FIGURE 3-15 Output from JoggingDistance example

## Coding Standards

It is important to establish and follow good coding standards. The intent of creating a set of coding standards is to have an acceptable list of guidelines that can be followed by all members of a team. The following list of standards are recommendations as they relate to methods.

### Naming Conventions

- Use Pascal Casing (first character of all words are uppercase; all other characters are lowercase) for method identifiers.
- Use Camel Casing (first character of all words, except the first word, are uppercase; all other characters are lowercase) for local variable identifiers and parameters.
- Use a verb or action clause to name a method. Do not use misleading names. Method names should tell what the method does. If you select a good method name, there is no need for additional documentation explaining what the method does.

### Spacing Conventions

- Align curly braces ( { } ) up with the method heading.
- Declare each local variable independently on separate lines. It is permissible to reuse the data type, but each variable should be on a separate line.
- There should be one and only one single blank line between each method inside the class.
- Avoid writing long methods. Consider refactoring when the method exceeds 25 lines of code.
- Avoid extremely large source code files. Consider refactoring when the file size exceeds 300–400 lines in a single class.

### Declaration Conventions

- Do not have more than one class in a single file.
- Declare and initialize local variables in the method where they are used.
- Try to initialize variables when they are declared.
- Avoid passing too many parameters to a method. If you have more than 4–5 parameters, it is a good idea to define a class or structure.
- A method should do only one thing: have a single theme.
