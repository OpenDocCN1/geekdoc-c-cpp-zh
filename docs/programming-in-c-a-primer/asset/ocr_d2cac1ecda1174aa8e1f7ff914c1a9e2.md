Consider another example as shown below:

```
```csharp
for (int x = 0; x < 10; x++)
average[x] = (float)x;
```
```

This loop initializes the array average to the values 0.0 to 9.0. Program 9.1 illustrates the use of an array for sorting a list of numbers.

# Program 9.1 | SORTING A LIST OF NUMBERS

```
```csharp
using System;
class NumberSorting
{
	public static void Main( )
	{
		int[] number = { 55, 40, 80, 65, 71 };
		int n = number.Length;
		Console.Write("Given list : ");
		for (int i = 0; i < n; i++)
		{
			Console.Write(" " + number[i]);
		}
		Console.WriteLine("\n");
		// Sorting begins
		for (int i = 0; i < n; i++)
		{
			for (int j = i+1; j < n; j++)
			{
				if(number[i] < number[j])
				{
					// Interchange values
					int temp = number[i];
					number[i] = number[j];
					number[j] = temp;
				}
			}
		}
		Console.Write("Sorted list : ");
		for (int i = 0; i < n; i++)
		{
			Console.Write(" " + number[i]);
		}
		Console.WriteLine(" ");
	}
}
```

Program 9.1 displays the following output:

Given list : 55 40 80 65 71

Sorted list : 80 71 65 55 40