# 8.4.6 Using Bar Charts to Display Array Data Graphically; Introducing Type Inference with var

Many apps present data to users in a graphical manner. For example, numeric values are often displayed as bars in a bar chart. In such a chart, longer bars represent proportionally larger numeric values. One simple way to display numeric data graphically is with a bar chart that shows each numeric value as a bar of asterisks (*).

An instructor might graph the number of grades in each of several categories to visualize the grade distribution for an exam. Suppose the grades on an exam were 87, 68, 94, 100, 83, 78, 85, 91, 76 and 87. Included were one grade of 100, two grades in the 90s, four grades in the 80s, two grades in the 70s, one grade in the 60s and no grades below 60. Our next app (Fig. 8.7) stores this grade-distribution data in an array of 11 elements, each corresponding to a category of grades. For example, array[0] indicates the number of grades in the range 0-9, array[7] the number of grades in the range 70-79 and array[10] the number of 100 grades. The two versions of class GradeBook in Sections 8.8 and 8.10 contain code that calculates these grade frequencies based on a set of grades. For now, we manually create array and initialize it with the number of grades in each range (Fig. 8.7, line 9). We discuss the keyword var (lines 14 and 27) after we present the app’s logic.

```
1  // Fig. 8.7: BarChart.cs
2  // Bar chart displaying app.
3  using System;
4  
5  class BarChart
6  {
7      static void Main()
8      {
9          int[] array = {0, 0, 0, 0, 0, 0, 1, 2, 4, 2, 1}; // distribution
10 
11         Console.WriteLine("Grade distribution:");
12 
13         // for each array element, output a bar of the chart
14         for (var counter = 0; counter < array.Length; ++counter)
15         {
16             // output bar labels ("00-09: ", ..., "90-99: ", "100: ")
17             if (counter == 10)
18             {
19                 Console.Write("  100: ");
20             }
21             else
22             {
23                 Console.Write($"{counter * 10:D2}-{counter * 10 + 9:D2}: ");
24             }
25 
26             // display bar of asterisks
27             for (var stars = 0; stars < array[counter]; ++stars)
28             {
29                 Console.Write("*");
30             }
        }
```