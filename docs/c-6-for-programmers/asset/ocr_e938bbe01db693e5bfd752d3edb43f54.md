```
```csharp
static void Main()
{
   // initializer list specifies the value of each element
   int[] array = {32, 27, 64, 18, 95};

   Console.WriteLine($"{ "Index",5}{"Value",8}"); // headings

   // output each array element's value
   for (int counter = 0; counter < array.Length; ++counter)
   {
      Console.WriteLine($"{counter,5}{array[counter],8}");
   }
}
```
```

| Index | Value |
| --- | --- |
| 0 | 32 |
| 1 | 27 |
| 2 | 64 |
| 3 | 18 |
| 4 | 95 |

**Fig. 8.3** | Initializing the elements of an array with an array initializer. (Part 2 of 2.)

# ### 8.4.3 Calculating a Value to Store in Each Array Element

Figure 8.4 creates a 5-element array and assigns to its elements the even integers from 2 to 10 (2, 4, 6, 8 and 10). Then the app displays the array in tabular format. Lines 13–16 calculate an array element’s value by multiplying the current value of the for loop’s control variable counter by 2, then adding 2.

```
```csharp
// Fig. 8.4: InitArray.cs
// Calculating values to be placed into the elements of an array.
using System;

class InitArray
{
   static void Main()
   {
      const int ArrayLength = 5; // create a named constant
      int[] array = new int[ArrayLength]; // create array

      // calculate value for each array element
      for (int counter = 0; counter < array.Length; ++counter)
      {
         array[counter] = 2 + 2 * counter;
      }

      Console.WriteLine($"{ "Index",5}{"Value",8}"); // headings
   }
```
```

**Fig. 8.4** | Calculating values to be placed into the elements of an array. (Part 1 of 2.)