# Executing Loop Iterations in Parallel

> >3.14159265358979323842643832795028841976193993751582097494445923070816
40662480998628034825432117096789214480861532823066470938446950558022321725
35950812488111467538470685210113385211055966462294859308196444288109756653
3959043326412854736817532687152521110916544866920346038416054326668213993
607700044911123325486877780000035118888111009968899224091715364378892590
36330011305348824665213844695114451161196430572703567599519530921861173
3813926112709311051185047844763976274956753158575274278931830194912

appended in the right order. Imagine what would happen if you could have all the iterations of this loop run concurrently: Each processor could take a single iteration and execute it in parallel with other processors executing iterations. Given the simultaneous execution of iterations, would decrease the execution time and more based on the number of processors.

The Task Parallel Library (TPL) provides a convenient method, Parallel .For(), which precisely does that. Listing 21.2 shows how to modify the sequential, single-threaded program in Listing 21.1 to use the helper method.

# Listing 21.2: For Loop Calculating Pi in Sections in Parallel

```
using System;
using System.Threading.Tasks;
using AddisonWesley.Michaelis.EssentialCSharp.Shared;
```

```
//
public class Program
{
    const int TotalDigits = 100;
    const int BatchSize = 10;

    public static void Main()
    {
        string pi = ""
        const int iterations = TotalDigits / BatchSize;
        string[] sections = new string[iterations];
        Parallel.For(0, i =>
        {
            sections[i] = PiCalculator.Calculate(
                BatchSize, i * BatchSize);
        });

        pi = string.Join("", sections);
        Console.WriteLine(pi);
```