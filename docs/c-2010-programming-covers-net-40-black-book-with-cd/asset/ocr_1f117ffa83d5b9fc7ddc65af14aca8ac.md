```
element of the " +(j+1)+ " row");
    x[j],k]=int.Parse(Console.ReadLine());
}
}
for (int j = 0; j <= 2; j++)
{
    Console.WriteLine();
    for (int k = 0; k <= 2; k++)
    {
        Console.Write(x[j],k +"\t");
    }
}
Console.ReadLine();
}
}
```

The output of Listing 2.22 is shown in Figure 2.19:

![](bbox=[0.28, 0.32, 0.78, 0.6])

Figure 2.19: Showing the Output of the MultiDimensionArray Application

Now, let’s learn how to iterate through an array

# Iterating Through an Array

Now, let’s create a new C# 2010 Console application, named Arraysizeanddimension (also available on the CD-ROM) by performing the steps given in the heading, Declaring Variables, earlier in this chapter. In the Arraysizeanddimension application, you learn how to print an array of one dimension with an unknown number of columns in it and determine the number of dimensions of an array. Listing 2.23 shows the complete code for the Program.cs file of the Arraysizeanddimension application:

Listing 2.23: Showing the Code for the Program.cs File of the Arraysizeanddimension Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace Arraysizeanddimension
{
    class Program
    {
        public static void PrintArray(int[] arr)
        {
            for (int i = 0; i < arr.Length; ++i)
                Console.WriteLine("OneDArray Row {0} = {1}", i, arr[i]);
        }
        public static void PrintArrayRank(int[,] arr)
        {
```