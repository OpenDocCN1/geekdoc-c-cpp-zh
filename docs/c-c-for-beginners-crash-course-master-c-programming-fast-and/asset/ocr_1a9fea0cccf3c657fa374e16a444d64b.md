An array can be initialized as:

```
int[][] marks = new int[3][] { new int[] {45,57,78}, new int[] { 60, 75, 86,45,35}};
```

The marks array is of two arrays of integers as marks[0] with 3 integers and marks[1] with 5 integers.

# Example:

```
Example 3.1:

using System;
namespace Jaggedarray
{
    class jagged
    {
        static void Main(string[] args)
        {
            int[][] x = new int[][] {
                new int[] {0,0},
                new int[] {2,2},
                new int[] {3,4},
                new int[] {4,2},
                new int[] {1,3}};

            int a,b;

            for(a = 0; a < 5; a++)
            {
                for(b = 0; b < 2; b++)
                {
                    Console.WriteLine("x[{0},{1}]={2}", a,b,x[a][b]);
                }
            }
            Console.ReadLine();
        }
    }
}
```

The code is compiled and executed, the output is:

```
x[0,0] = 0
```