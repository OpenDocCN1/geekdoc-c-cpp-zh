# Step 2: Define the Data Processing Logic

Define the data processing logic that you want to perform in parallel. For this example, let's say you want to calculate the square of each number in a large dataset.

```
```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static void Main(string[] args)
    {
        // Create a large dataset
        int[] data = new int[1000000];
        for (int i = 0; i < data.Length; i++)
        {
            data[i] = i + 1;
        }

        // Process data in parallel
        Parallel.For(0, data.Length, i =>
        {
            data[i] = data[i] * data[i]; // Square each number
        });
        Console.WriteLine("Data processing completed.");
    }
}
```
```

# Step 3: Compile and Run

Build and run your C# console application in your development environment.

# Step 4: Observe Output

You should see the program processing the large dataset by squaring each number in parallel using the TPL.