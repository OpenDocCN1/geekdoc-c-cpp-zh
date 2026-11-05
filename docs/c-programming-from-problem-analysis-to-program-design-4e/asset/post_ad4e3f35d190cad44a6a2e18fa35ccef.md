
After the algorithm is developed, the design should be checked for correctness. You might develop a table now with test values using a standard calculator. Desk check the pseudo-code to ensure that you are getting the results expected. After your program is running, you can validate the correctness by comparing the results you produce with your program against values you produced with the calculator during your design walk-through.

## CODE THE SOLUTION

After you complete the design and verify the algorithm’s correctness, translate the design into source code. The final application listing follows:

```csharp
/* TempAgency.cs
 * This application is used by a temporary work agency to
 * set projections for sales for new hires. The program enables the
 * user to input salesmen's names and expected sales goals.
 * The sales figure is placed in a two-dimensional array
 * and expected sales figures for four months are added.
 * These projections are based on increasing sales at
 * least 5% each month over the four-month period.
 * for testing purposes, four salesman data are entered.
 */

using System;
using System.Collections.Generic;

namespace TempAgency
{
    public class TempAgency
    {
        public static void Main(string[] args)
        {
            double[,] sales = new double[4,5];
            string[] salesman = new string[4];

            DisplayInstructions();
            GetSalesData(salesman, sales);
            ProduceSalesProjectionTable(sales);
            DisplaySalesProjections(salesman, sales);

            Console.ReadKey();
        }

        public static void DisplayInstructions()
        {
            Console.WriteLine("You will be asked to enter data for " +
                              "four salesmen. \nFor their name, " +
                              "enter their first " +
                              "name followed \nby a space and then " +
                              "their last name." +
                              "\n\nNext you will enter the " +
                              "expected sales for the 1st month. " +
                              "\n\nFor testing purposes enter " +
                              "data for (4) salesmen.\n");
            Console.WriteLine();
        }

        public static void GetSalesData(string[] salesman,
                                        double[,] sales)
        {
            for (int row = 0; row < salesman.Length; row++)
            {
                string fullname;
                string[] name = new string[3];

                Console.Write("Name of the New Salesman: ");
                salesman[row] = Console.ReadLine();
                fullname = salesman[row];
                name = fullname.Split(' ');
                Console.Write("Please enter {0}'s Initial Sales " +
                              "Goal: ", name[0]);
                sales[row, 0] = double.Parse(Console.ReadLine());
                Console.Clear();
            }
        }

        public static void ProduceSalesProjectionTable(double[,] sales)
        {
            double salesIncrease;

            DisplayHeading(sales);
            for (int row = 0; row < sales.GetLength(0); row++)
            {
                salesIncrease = 0.05;
                for (int col = 1; col < sales.GetLength(1); col++)
                {
                    sales[row, col] = sales[row, col-1] *
                                      salesIncrease + sales[row, col-1];
                    salesIncrease += 0.05;
                }
            }
        }

        public static void DisplayHeading(double[,] sales)
        {
            double inc = 0.05;

            Console.Write("{0,-20}  {1,-10}", "Salesman",
                          "Initial");
            for (int col = 0; col < sales.GetLength(1) - 1; col++)
            {
                Console.Write("{0,-6}{1,-1}  ", "Month", col + 1);
            }

            Console.WriteLine();
            Console.Write("{0,-20} {1,-7}", " Name", " Sales ");
            for (int col = 0; col < sales.GetLength(1) - 1; col++)
            {
                Console.Write("{0, 8} ", inc.ToString("P0"));
                inc += 0.05;
            }
            Console.WriteLine();
        }

        public static void DisplaySalesProjections(string[] salesmen, double[,] sales)
        {
            string[] name = new string[3];
            Console.WriteLine();
            for (int row = 0; row < sales.GetLength(0); row++)
            {
                name = salesmen[row].Split(' ');
                Console.Write("{0,-20}", name[1] + ", " + name[0]);
                for (int col = 0; col < sales.GetLength(1); col++)
                {
                    Console.Write("{0, 11:N2}", sales[row, col]);
                }
                Console.WriteLine();
            }
        }
    }
}
```

The output from one test run is shown in Figure 8-12.

![](img/36e48639a06772bcb0fa1ea2525b33a3_517_0.png)

**FIGURE 8-12**  TempAgency application output

## Coding Standards

Each project you develop should follow agreed upon coding standards. They make your code more readable and help reduce the number of errors.

### Guidelines for Naming Collections

Use a singular noun as an identifier for collection objects.

Use the Camel case naming convention when instantiating objects of collections.

### Advanced Array Suggestions

If a method returns a collection and there are no values to return, return an empty collection instead of null.

As opposed to writing new code, use .NET predefined methods and properties whenever possible when working with collections.

### Resources

Additional sites you might want to explore:

- An Extensive Examination of Data Structures – http://msdn.microsoft.com/en-us/library/aa289148(VS.71).aspx
- MSDN C# Data Structures series – http://www.andrewconnell.com/blog/archive/2004/02/17/262.aspx
- C# String Tutorial – http://csharp.net-informations.com/string/csharp_string_tutorial.htm
- Multidimensional Arrays – http://www.functionx.com/csharp/Lesson23.htm

## QUICK REVIEW

- 1. Two-dimensional and multidimensional arrays may contain any number of variables of the same type. One common identifier names the entire structure.
- 2. Two-dimensional and multidimensional arrays should be named using singular nouns.
- 3. To access a two-dimensional or multidimensional array element, use the number of indexes included in the declaration. Indexes are separated by commas and enclosed in square brackets.
- 4. When you use a two-dimensional or multidimensional array as a method parameter, the array identifier and type are specified; however, the length or size of the array is not included. Opening, closing square brackets, and commas are required. The call to that method includes the name of the array only.
- 5. Two-dimensional and multidimensional arrays can be sent as arguments to methods, and in addition, a method can have a two-dimensional or multidimensional array as its return type. The square bracket that is included before the name of the method is empty with the exception of one or more commas. The comma separators identify the number of dimensions.
- 6. Two-dimensional and other multidimensional arrays follow the same guidelines as one-dimensional arrays.
- 7. A two-dimensional array is usually visualized as a table divided into rows and columns. The first index represents the number of rows.
- 8. When the number of columns in rows may need to differ, a jagged, or ragged array, can be used. It is called an “array of arrays.”
- 9. ArrayList class creates a listlike structure that can dynamically increase or decrease in length. Like traditional arrays, indexes of ArrayList objects are zero based. A number of predefined methods are included.
- 10. To create a multidimensional array, specify the type and the number of dimensions per rank. These values are separated by commas. A three-dimensional array would be defined with type [,,] identifier = new type[length_of_planes, length_of_rows, length_of_columns].
- 11. The string class stores an immutable series of characters. After you give a string a value, it cannot be modified.
- 12. The string type is an alias for the System.String class in the .NET Framework. You can access the individual characters using an index, with the first index being zero.
- 13. String variables are objects of the string class; thus, a number of predefined methods including the following can be used: Trim(), ToUpper(), ToLower(), Substring(), Split(), Replace(), Insert(), and Copy().
- 14. The Hashtable class represents a collection of key/value pairs that are organized based on the hash code of the key. Override the GetHashCode() method to provide a new algorithm for the hash function.
- 15. BitArrays are very useful for working with large data sets. They are most commonly used to represent a simple group of Boolean flags.
