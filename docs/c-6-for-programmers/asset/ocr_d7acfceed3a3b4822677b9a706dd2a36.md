Figure 8.6 uses the foreach statement (lines 13–16) to calculate the sum of array's elements. The iteration variable number's type is declared as int (line 13), because array contains int values. The foreach statement iterates through successive int values in array one by one, starting with the first element. The foreach header can be read concisely as "for each iteration, assign array's next element to int variable number, then execute the following statement." Lines 13–16 are equivalent to the counter-controlled iteration used in lines 13–16 of Fig. 8.5.

> **Common Programming Error 8.4**
> Any attempt to change the iteration variable's value in the body of a foreach statement results in a compilation error.

```
```csharp
1 // Fig. 8.6: ForEachTest.cs
2 // Using the foreach statement to total integers in an array.
3 using System;
4
5 class ForEachTest
6 {
7     static void Main()
8     {
9         int[] array = {87, 68, 94, 100, 83, 78, 85, 91, 76, 87};
10         int total = 0;
11
12         // add each element's value to total
13         foreach (int number in array)
14         {
15             total += number;
16         }
17
18         Console.WriteLine($"Total of array elements: {total}");
19     }
20 }
```
```

Total of array elements: 849

Fig. 8.6 | Using the foreach statement to total integers in an array.

# foreach vs. for

The foreach statement can be used in place of the for statement whenever code looping through an array does not require access to the current array element's index. For example, totaling the integers in an array requires access only to the element values—each element's index is irrelevant. If an app must use a counter for some reason other than simply to loop through an array (e.g., to calculate an element's value based on the counter's value, as in Fig. 8.4), you should use the for statement.

> **Common Programming Error 8.5**
> Attempting to modify an array element's value using a foreach statement's iteration variable is a logic error—the iteration variable can be used only to access each array element's value, not modify it.