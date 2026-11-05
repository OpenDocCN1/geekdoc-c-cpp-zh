
```csharp
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
    Console.WriteLine("Calorie Counter");
    Console.WriteLine("Daily Averages");
    foreach (double avgCalorie in dailyAverage)
    {
        Console.WriteLine("Day {0}: {1,6:N0}", dayNumber,
                          avgCalorie);
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
        Console.WriteLine("{0,-10}: {1,6}", mealTime[c],
                          mealAverage[c].ToString("N0"));
    }
}

public static void DisplayAverageCaloriesPerMeal(int[,] calories)
{
    double sum = 0;
    for (int da = 0; da < calories.GetLength(0); da++)
        for (int ml = 0; ml < calories.GetLength(1); ml++)
            sum += calories[da, ml];
    Console.WriteLine("\nCaloric Average Per Meal: {0:N0}",
                      sum / calories.Length);
}
}
```

Example 8-9 includes three separate Display methods. The DisplayDailyAverage() method illustrates using the foreach loop. Since no index is included with this loop structure, a separate variable, dayNumber, was defined and incremented inside the loop body in order to print the day number. The output produced from this example is shown in Figure 8-3.

![](img/e33ae760e23d89eac66541252ad65de8_456_0.png)

Figure 8-3 Output from WeeklyCalorieCounter

As you review Figure 8-3, notice that the numbers are aligned properly. Review the format specifier shown in Example 8-10.

### Example 8-10

```csharp
Console.WriteLine("{0,-10}: {1,6}", mealTime[c],
                  mealAverage[c].ToString("N0"));
```

A comma separates the placeholder index from the width specifier. The first argument ({0,-10}) indicates that the first argument should be displayed in a width of 10. The negative value in front of the 10 indicates that the value stored in mealTime[c] should be left justified. Right justification is the default. The one-dimensional array mealTime stores the type of meal (i.e., Breakfast, Lunch, Dinner). A colon follows the meal type and then the actual value is displayed in a width of 6 ({1,6}) character positions. Since the value 6 is positive, the numbers are right justified and aligned properly.

In Example 8-10 the ToString() method is called to convert the double value stored in mealAverage[c] to a string value. The format specifier N is used to convert it to a number with a comma separator. The zero following the N indicates that there should be no digits to the right of the decimal.

## Jagged Array

When the number of columns in the rows must differ, a jagged, or **ragged array**, can be created. **Jagged arrays** differ from rectangular arrays in that rectangular arrays always have a rectangular shape, like a table. Jagged arrays are called “**arrays of arrays**.” One row might have five columns; another row 50 columns. To create a jagged array, you can create a one-dimensional array of type `Array`, and initialize each of the one-dimensional arrays separately. Example 8-11 illustrates the creation of a jagged array.

### Example 8-11

```csharp
int[][] anArray = new int[4][];
anArray[0] = new int[] {100, 200};
anArray[1] = new int[] {11, 22, 37};
anArray[2] = new int[] {16, 72, 83, 99, 106};
anArray[3] = new int[] {1, 2, 3, 4};
```

The GetLength(), GetUpperBound(), and GetLowerBound() methods can be used with jagged arrays. Jagged arrays are used exactly like rectangular arrays, except that rows may have a different number of elements.

## Multidimensional Arrays

You are really only limited by your imagination as far as the number of dimensions for which you can allocate arrays in C#. The major requirement is the fact that all data values placed in an array must be of the same base type. A two-dimensional array is actually a multidimensional array; however, it is such a common type of structure that it often is put in its own category.

To declare a three-dimensional array, three integral values are used. They specify the number of planes, rows, and columns to set aside for the array. As with single-dimensional arrays, three-dimensional arrays are referenced by the identifier name.

The format for creating a three-dimensional array is:

```
type[,,] identifier =
    new type[integral value, integral value, integral value];
```

What if you wanted to create the calories table to hold four weeks of statistics? A three-dimensional array could be defined to hold the data. The first dimension could represent the number of weeks, the second number of days, and the third number of meals. To create the array in C# to hold that extra data, you write:

```csharp
int[,,] calories = new int[4, 7, 3];
```

![](img/e33ae760e23d89eac66541252ad65de8_458_0.png)

Figure 8-4 Three-dimensional array

This allocates storage for 84 elements (4 * 7 * 3). You will notice that the upper bounds on the indexes are 3, 6, and 2; the lower bound is 0 for all three.

An additional column could be added to the array to hold the total calories for each day by dimensioning the array as shown in Example 8-12. The code in Example 8-12 adds the first 3 columns and places the sum in the new fourth column.

### Example 8-12

```csharp
int[,,] calories = new int[4, 7, 4];
// Loop to place the row total in the last column, indexed by 3
for (int wk = 0; wk < calories.GetLength(0); wk++)
{
    for (int da = 0; da < calories.GetLength(1); da++)
    {
        for (int ml = 0; ml < calories.GetLength(2) - 1; ml++)
        {
            calories[wk, da, 3] += calories[wk, da, ml];
        }
    }
}
```

![](img/e33ae760e23d89eac66541252ad65de8_459_0.png)

Reexamine the first line in Example 8-12 and note that the dimension representing the number of columns was changed from 3 to 4. This enables the total calories for each row to be stored in this column.

The length integral value of the last dimension was changed from 3 to 4 to hold the total per day. Now each row has the meal count for breakfast, lunch, and dinner and the total count.

The nested loop adds columns indexed with 0 through 2 of each row and stores the result in the column indexed by 3. The conditional expression of the innermost loop uses (calories.GetLength(2) - 1) for the evaluation. GetLength(2) returns the length of the third dimension, or rank. This returns 4 because there are now four columns in the row. But notice that 1 is subtracted from that value, because the last column should not be added. It is holding the total. Therefore, the loop is executed for ml = 0, ml = 1, and ml = 2. When ml is equal to 3, ml is no longer less than 3 (ml < calories.GetLength(2) - 1), and the inner loop is complete for that iteration.

calories.GetLength(0) returns the dimension for the number of planes or weeks. It returns 4. GetLength(1) returns the dimension for the number of rows per plane or days per week. It returns 7. As was noted, GetLength(2) returns the dimension for the number of columns per row or meals per day. It returns 4. The program listing for the calorie counter application is included as Example 8-13.
