
### EXAMPLE 8.6

```csharp
double[] dailyAverage = new double[7];

dailyAverage = CalculateAverageByDay(calories);
```

In Example 8.6, `CalculateAverageByDay()` passes the two-dimensional array, `calories`, in as an argument when it is invoked. Again notice there are no square brackets. The call sends the address of the first element of the array. When the method finishes and returns back to `Main()`, the address of the first element of the local array, `dailyAverage`, is sent back through the method call and is then assigned to the local one-dimensional array, `dailyAverage`, which is defined in the `Main()` method.

C# is a row-major language, which means you specify the row index first when you reference elements in the array. In the previous example, the `r` variable was placed in the outermost loop. It is also possible to process data one column at a time. If you wanted to calculate the average number of calories consumed during all breakfasts, or the average number during lunches or dinners, you add all rows for column zero. The nested loop shown in Example 8.7 illustrates placing the column variable in the outermost loop.

### EXAMPLE 8.7

```csharp
public static double[] CalculateAverageByMeal(int[,] calories)
{
    int sum = 0;
    double[] mealAverage = new double[3];
    for (int c = 0; c < calories.GetLength(1); c++)
    {
        for (int r = 0; r < calories.GetLength(0); r++)
            sum += calories[r, c];
        mealAverage[c] = (double)sum / calories.GetLength(0);
        sum = 0;
    }
    return mealAverage;
}
```

Notice in Example 8.7 that when the `calories` array is referenced in the statement `sum += calories[r, c]`, the row is still listed first. As with the previous example, the `CalculateAverageByMeal()` method returns a one-dimensional array. It is also possible for a method to return a two-dimensional array.

Sometimes it is more readable to use identifiers for row and column indexes that are more representative of the data. Since the row stores calories for a given day, the identifier `da` is used in Example 8.8, instead of `r`, to store the row number. Each column holds the calories for a given meal; thus, the identifier `ml` is used to store the column number. As with the last two examples, Example 8.8 uses a nested loop to add every element in the array. The variable `da` stores the row numbers while `ml` stores the column number.

### EXAMPLE 8.8

```csharp
public static void DisplayAverageCaloriesPerMeal(int[,] calories)
{
    double sum = 0;
    for (int da = 0; da < calories.GetLength(0); da++)
        for (int ml = 0; ml < calories.GetLength(1); ml++)
            sum += calories[da, ml];
    Console.WriteLine("\nCaloric Average Per Meal: {0:N0}",
                      sum / calories.Length);
}
```

In this example, `sum` is divided by the value returned from the `calories.Length` property. The `Length` property was used to return the total number of elements in all dimensions. For Example 8.8, `Length` returns 21.

Example 8.9 displays the entire application. It does a compile-time initialization of the two-dimensional array. The application displays the average number of calories consumed per day, average number consumed per meal type, and the overall average per meal.

> **NOTE**
>
> When you create your solutions in Visual Studio, the code generator adds additional `using` statements. To conserve space, unnecessary `using` statements were deleted from Example 8.9 and other examples.

### EXAMPLE 8.9

```csharp
/* CalorieCounter.cs       Author: Doyle
 * Demonstrates usage of a two-dimensional array
 * to calculate the average number of calories
 * intake per day, per meal type, and per meal.
 */

using System;

namespace WeeklyCalorieCounter
{
    public class WeeklyCalorieCounter
    {
        public static void Main()
        {
            int[,] calories = {{900, 750, 1020},
                               {300, 1000, 2700},
                               {500, 700, 2100},
                               {400, 900, 1780},
                               {600, 1200, 1100},
                               {575, 1150, 1900},
                               {600, 1020, 1700}};
            double[] dailyAverage = new double[7];
            double[] mealAverage = new double[3];

            dailyAverage = CalculateAverageByDay(calories);
            mealAverage = CalculateAverageByMeal(calories);

            DisplayDailyAverage(dailyAverage);
            DisplayMealAverage(mealAverage);
            DisplayAverageCaloriesPerMeal(calories);
            Console.ReadKey();
        }

        public static double[] CalculateAverageByDay(int[,] calories)
        {
            int sum = 0;
            double[] dailyAverage = new double[7];
            for (int r = 0; r < calories.GetLength(0); r++)
            {
                for (int c = 0; c < calories.GetLength(1); c++)
                    sum += calories[r, c];
                dailyAverage[r] = (double)sum / calories.GetLength(1);
                sum = 0;
            }
            return dailyAverage;
        }

        public static double[] CalculateAverageByMeal(int[,] calories)
        {
            int sum = 0;
            double[] mealAverage = new double[3];
            for (int c = 0; c < calories.GetLength(1); c++)
            {
                for (int r = 0; r < calories.GetLength(0); r++)
                    sum += calories[r, c];
                mealAverage[c] = (double)sum / calories.GetLength(0);
                sum = 0;
            }
            return mealAverage;
        }

        public static void DisplayDailyAverage(double[] dailyAverage)
        {
            int dayNumber = 1;
            Console.WriteLine("*Calorie Counter*");
            Console.WriteLine("Daily Averages");
            foreach (double avgCalorie in dailyAverage)
            {
                Console.WriteLine("Day {0}: {1,6:N0}", dayNumber, avgCalorie);
                dayNumber++;
            }
        }

        public static void DisplayMealAverage(double[] mealAverage)
        {
            string[] mealTime = {"Breakfast", "Lunch", "Dinner"};
            Console.WriteLine("\n\nCalorie Counter");
            Console.WriteLine("Meal Averages");
            for (int c = 0; c < mealAverage.Length; c++)
            {
                Console.WriteLine("{0,-10}: {1,6}", mealTime[c], mealAverage[c].ToString("N0"));
            }
        }

        public static void DisplayAverageCaloriesPerMeal(int[,] calories)
        {
            double sum = 0;
            for (int da = 0; da < calories.GetLength(0); da++)
                for (int ml = 0; ml < calories.GetLength(1); ml++)
                    sum += calories[da, ml];
            Console.WriteLine("\nCaloric Average Per Meal: {0:N0}", sum / calories.Length);
        }
    }
}
```

Example 8.9 includes three separate `Display` methods. The `DisplayDailyAverage()` method illustrates using the `foreach` loop. Since no index is included with this loop structure, a separate variable, `dayNumber`, was defined and incremented inside the loop body in order to print the day number. The output produced from this example is shown in Figure 8.3.

![](img/36e48639a06772bcb0fa1ea2525b33a3_488_0.png)

**FIGURE 8.3** Output from WeeklyCalorieCounter

As you review Figure 8.3, notice that the numbers are aligned properly. Review the format specifier shown in Example 8.10.

### EXAMPLE 8.10

```csharp
Console.WriteLine("{0,-10}: {1,6}", mealTime[c],
                  mealAverage[c].ToString("N0"));
```

A comma separates the placeholder index from the width specifier. The first argument (`{0,-10}`) indicates that the first argument should be displayed in a width of 10. The negative value in front of the 10 indicates that the value stored in `mealTime[c]` should be left justified. Right justification is the default. The one-dimensional array `mealTime` stores the type of meal (i.e., Breakfast, Lunch, Dinner). A colon follows the meal type and then the actual value is displayed in a width of 6 (`{1,6}`) character positions. Since the value 6 is positive, the numbers are right justified and aligned properly.

In Example 8.10, the `ToString()` method is called to convert the double value stored in `mealAverage[c]` to a string value. The format specifier `N` is used to convert it to a number with a comma separator. The zero following the `N` indicates that there should be no digits to the right of the decimal.

> **NOTE**
>
> C# initializes array elements to the null value when you create them with the `new` keyword. One way to test to see if a value has been stored is to test for `null`. The following returns true when no values have been referenced by the array.
>
> ```csharp
> string[] name = new string[10];
> if (name[0] == null)
> ```

## Jagged Array

When the number of columns in the rows must differ, a jagged, or ragged array, can be created. Jagged arrays differ from rectangular arrays in that rectangular arrays always have a rectangular shape, like a table. Jagged arrays are called "arrays of arrays." One row might have five columns; another row 50 columns. To create a jagged array, you can create a one-dimensional array of type `Array`, and initialize each of the one-dimensional arrays separately. Example 8.11 illustrates the creation of a jagged array.

### EXAMPLE 8.11

```csharp
int[][] anArray = new int[4][];
anArray[0] = new int[] {100, 200};
anArray[1] = new int[] {11, 22, 37};
anArray[2] = new int[] {16, 72, 83, 99, 106};
anArray[3] = new int[] {1, 2, 3, 4};
```

The `GetLength()`, `GetUpperBound()`, and `GetLowerBound()` methods can be used with jagged arrays. Jagged arrays are used exactly like rectangular arrays, except that rows may have a different number of elements.

## Multidimensional Arrays

You are really only limited by your imagination as far as the number of dimensions for which you can allocate arrays in C#. The major requirement is that all data values placed in an array must be of the same base type. A two-dimensional array is actually a multidimensional array; however, it is such a common type of structure that it often is put in its own category.

To declare a three-dimensional array, three integral values are used. They specify the number of planes, rows, and columns to set aside for the array. As with single-dimensional arrays, three-dimensional arrays are referenced by the identifier name.

The format for creating a three-dimensional array is:

```csharp
type[,,] identifier =
    new type[integral value, integral value, integral value];
```
