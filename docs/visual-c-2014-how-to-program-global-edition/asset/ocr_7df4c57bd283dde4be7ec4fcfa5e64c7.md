# 8.4 Examples Using Arrays 349

index is irrelevant. If an app must use a counter for some reason other than simply loop through an array (e.g., to calculate an element's value based on the counter's value, as in Fig. 8.4), you should use the for the statement.

# Common Programming Error 8.5

Attempting to modify an array element's value using a foreach statement's iteration variable is a logic error—the iteration variable can be used only to access each array element's value, not modify it.

# 8.4.6 Using Bar Charts to Display Data Graphically; Introducing Type Inference with var

Many apps present data to users in a graphical manner. For example, numerical values are often displayed as bars in a bar chart. In such a chart, bars represent proportionally larger values. One simple way to display data graphically is with a bar chart that shows each numerical value as a bar of asterisks (*).

An instructor might graph the number of grades in several categories for an exam. Suppose the grades on an exam were 87, 68, 94, 100, 83, 78, 85, 91, 76 and 87. Included were one grade of 100, two grades in the 90s, four in the 80s, two grades in the 70s, one grade in the 60s and no grades below 60. Our next app (Fig. 8.7) shows this grade-distribution in an array of 11 elements, each responding to a category of grades. For example, array[0] indicates the number of grades in the range 0–9, array[7] the number of grades in the range 70–79 and array[10] the number of 100 grades. The two versions of class GradeBook in Sections 8.8 and 8.10 contain code that calculates these grade frequencies and initialize it with the number of grades in each range (Fig. 8.7, line 9). We decide the keyword var (lines 14 and 27) after we present the app's logic.

```
// Fig. 8.7: BarChart.cs
// Bar chart displaying app.
using System;
class BarChart
{
    static void Main()
    {
        int[] array = {0, 0, 0, 0, 0, 0, 1, 2, 4, 2, 1}; // distribution
        Console.WriteLine("Grade distribution:");

        // for each array element, output a bar of the chart
        for (var counter = 0; counter < array.Length; ++counter)
        {
            // output bar labels ("00-09 \ ", ..., "90-99": ", "100: ")
            if (counter == 10)
            {
                Console.Write(" 100: ");
            }
        }
    }
}
```

Fig. 8.7 | Bar chart displaying app. (Part 1 of 2).