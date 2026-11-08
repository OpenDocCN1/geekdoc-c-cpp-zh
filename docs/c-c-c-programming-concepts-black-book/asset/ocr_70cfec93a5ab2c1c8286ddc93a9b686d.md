# Listing 17.12: Showing the Usage of a Jagged Array

```
```csharp
using System;
class Program
{
    public static void Main()
    {
        Console.WriteLine("Enter the input to the jagged array...");
        int[][] jag = new int[4][];
        jag[0] = new int[4];
        jag[1] = new int[2];
        jag[2] = new int[3];
        jag[3] = new int[1];
        for (int i = 0; i < 4; i++)
        {
            Console.WriteLine("Enter the input for the column {0}...", i);
            for (int j = 0; j < jag[i].Length; j++)
            {
                jag[i][j] = int.Parse(Console.ReadLine());
            }
        }
        Console.WriteLine("The jagged array is...");
        for (int i = 0; i < 4; i++)
        {
            for (int j = 0; j < jag[i].Length; j++)
            {
                Console.Write(jag[i][j]);
            }
            Console.WriteLine();
        }
    }
}
```
```

In the preceding program, we have first declared a jagged array that holds other four arrays. After that, we have initialized these four arrays, where the first array holds the four integers, the second array holds the two integers, the third array holds the three integers, and the fourth array holds a single integer. This program reads the inputs given by a user from the console, stores them in the jagged array accordingly, and prints the stored value on the console. The output of the preceding program is as follows:

```
```
Enter the input to the jagged array...
Enter the input for the column 0...
1
2
3
4
Enter the input for the column 1...
5
6
Enter the input for the column 2...
7
8
9
Enter the input for the column 3...
10
The jagged array is...
1234
56
789
10
```
```

Next, let’s learn about strings in C#.