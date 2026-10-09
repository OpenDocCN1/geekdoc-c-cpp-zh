```
**LISTING 19.26:** For Loop Synchronously Calculating Pi in Sections
```csharp
using System;
using AddisonWesley.Michaelis.EssentialCSharp.Shared;

class Program
{
    const int TotalDigits = 100;
    const int BatchSize = 10;

    static void Main()
    {
        string pi = null;
        const int iterations = TotalDigits / BatchSize;
        for(int i = 0; i < iterations; i++)
        {
            pi += PiCalculator.Calculate(
                BatchSize, i * BatchSize);
        }

        Console.WriteLine(pi);
    }
}

using System;

class PiCalculator
{
    public static string Calculate(
        int digits, int startingAt)
    {
        // ...
    }

    // ...
}
```
```

```
**OUTPUT 19.9**
```
>3.1415926535897932384626433832795028841971693993751058209749445923078164062862089986280348253421170679821480865132823066470938446095505822317253594081284811174502841027019385211055596446229489549303819644288109756659334461284756482337867831652712019091456485669234603486104543266482133936072602491412737548207381687188836920972445941050481623885791367954
code
```
```

The for loop executes each iteration synchronously and sequentially.
However, because the pi calculation algorithm splits the pi calculation into independent pieces, it is not necessary to compute the pieces sequentially