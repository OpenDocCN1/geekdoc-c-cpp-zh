
The focus is on writing *what needs to be done*. Figure 2–18 shows the Structured English design for the CarpetCalculator example.

![](img/36e48639a06772bcb0fa1ea2525b33a3_154_0.png)

**FIGURE 2-18**  Structured English for the CarpetCalculator example

Structured English is one of the more common tools used with the object-oriented approach to document the process logic. Decision trees and tables are sometimes used in conjunction with Structured English, especially when the solution requires that a number of alternate paths be developed as part of the solution. Chapter 5 introduces you to these tools.

The object-oriented approach focuses on the objects (persons, places, and things) that exist in our world. Class diagrams help design and document the data items and behaviors of the objects. Figure 2–19 shows the class diagram for the CarpetCalculator example.

![](img/36e48639a06772bcb0fa1ea2525b33a3_154_1.png)

**FIGURE 2-19**  Class diagram for the CarpetCalculator example

Figure 2–19 includes methods. In this chapter, you learned about the data items. The middle section in the class diagram includes the identifiers and their data types. Methods are included in the bottom portion of the class diagram. **Methods** are procedures for implementing the behaviors of objects in C#. In Chapter 3, you will learn how to write methods. Figure 2–20 shows a class diagram solution without methods. For now this will be how the application is designed. Notice Figure 2-20 includes three additional data members and no methods.

![](img/36e48639a06772bcb0fa1ea2525b33a3_155_0.png)

**FIGURE 2-20**  Revised class diagram without methods

After the algorithm is developed, the design should be checked for correctness. When you desk check your algorithm, use a calculator and write down the results you obtain. After you implement your design, you can compare the results obtained from the program with the calculator results.

At this point, it might seem that it would be easier simply to perform the calculations using a calculator. Remember that the power of the computer comes into play when you write a set of instructions that can be used with many different data sets. In the next chapter, you will learn to call methods that allow you to input data interactively, such as the carpet price and room sizes. This will add much more functionality to your program.

## CODE THE SOLUTION

After you have completed the design and verified the algorithm’s correctness, it is time to translate the design into source code. If you are creating your application in Visual Studio, you might want to glance back at Figure 1-26 to review the suggested changes. They included the following:

- After launching Visual Studio, click **File** on the menu bar, click **New Project**. In the **New Project** window, select **Visual C#**; and in the middle window, select **Console Application**. Type an appropriate name, such as `CarpetExample`.
- You may remove the `using System.Collections.Generic; using System.Linq;` and `using System.Text;` statements. These namespaces are not needed for this application.
- Modify the `Main()` method’s signature. You can remove “string[] args” from within the parentheses.
- Change the name of the `.cs` filename from `Program.cs` to a name more representative of the application’s operation, such as `CarpetCalculator.cs`. Answer Yes when asked if you would “like to perform a rename in this project of all references to the code element Program.”

The final program listing appears as follows:

```csharp
/* CarpetCalculator.cs Author: Doyle
* Calculates the total cost of carpet, given
* room dimensions in feet and inches and carpet
* price in price per square yard.
*/
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace CarpetExample
{
    class CarpetCalculator
    {
        static void Main()
        {
            const int SQ_FT_PER_SQ_YARD = 9;
            const int INCHES_PER_FOOT = 12;
            const string BEST_CARPET = "Berber";
            const string ECONOMY_CARPET = "Pile";

            int roomLengthFeet = 12,
                roomLengthInches = 2,
                roomWidthFeet = 14,
                roomWidthInches = 7;

            double roomLength,
                   roomWidth,
                   carpetPrice,
                   numOfSquareFeet,
                   numOfSquareYards,
                   totalCost;

            roomLength = roomLengthFeet +
                (double)roomLengthInches / INCHES_PER_FOOT;
            roomWidth = roomWidthFeet +
                (double)roomWidthInches / INCHES_PER_FOOT;
            numOfSquareFeet = roomLength * roomWidth;
            numOfSquareYards = numOfSquareFeet /
                SQ_FT_PER_SQ_YARD;
            carpetPrice = 27.95;
            totalCost = numOfSquareYards * carpetPrice;
            Console.WriteLine("The cost of " +
                BEST_CARPET +
                " is {0:C}", totalCost);
            Console.WriteLine();
            carpetPrice = 15.95;
            totalCost = numOfSquareYards * carpetPrice;
            Console.WriteLine("The cost of " +
                ECONOMY_CARPET +
                " is " + "{0:C}",
                totalCost);

            Console.ReadKey();
        }
    }
}
```

> **NOTE** Readability is important. Notice how the second lines of statements are indented to indicate that the statement has not been completed.

## IMPLEMENT THE CODE

During implementation, the source code is compiled to check to see if any rule violations have been made. To compile the project, click **Build Solution** from the **Build** menu if you are using Visual Studio. To run the application, use the **Start Without Debugging** option available on the **Debug** menu.

## TEST AND DEBUG

During this final step, test the program and ensure you have the correct result. The output should match your prototype. Is your spacing correct? Figure 2–21 shows the output generated from displaying the results of the calculations.

![](img/36e48639a06772bcb0fa1ea2525b33a3_157_0.png)

**FIGURE 2-21**  Output for the CarpetCalculator program

In conclusion, this chapter concentrated on using data. You will use the concepts you learned in this chapter for the remainder of your software development. In Chapter 3, you will learn how to write methods that describe the behavior of the data.

## Coding Standards

As you read in Chapter 1, coding or programming style is a term used to describe acceptable conventions for writing source code. It goes beyond the rules of the language and provides guidelines or suggestions that should be followed to ensure consistency among programmers working toward a common goal. Following the guidelines reduces the number of errors or bugs introduced into programming projects. It saves time, increases program maintainability, and helps ensure reliability of code. Naming Conventions, which were discussed earlier in this chapter, are highlighted next.

### Naming Conventions

- Use meaningful, descriptive words as identifiers.
- Do not use abbreviations for identifiers unless it is a well-known abbreviation.
- With the exception of variables used as iterators for loops, do not use single character identifiers.
- Use Pascal Casing (first character of all words are uppercase; all other characters are lowercase) for the following:
  - Class and type identifiers
  - Method names
  - Namespace identifiers
  - Property names
- Use Camel Casing (first character of all words, except the first word, are uppercase; all other characters are lowercase) for the following:
  - Local variable identifiers
  - Object identifiers
  - Private data members
  - Parameters
- Filename should match class name.
- Use all uppercase characters to name constants.
- Do not use an underscore in identifiers.
- Use a noun or a noun phrase to name a class.

### Spacing Conventions

- Use tabs instead of spaces for indentation.
- Use white space (one blank line) to separate and organize logical groups of code.
- Place curly braces { } at the same level as the code outside the braces.
