```
public double DetermineTotalCost( )
{
    return (pricePerSqYard * noOfSqYards);
}
// One of the overloaded mutator methods
public void SetNoOfSqYards(double length,
                           double width)
{
    const int SQ_FT_PER_SQ_YARD = 9;

    noOfSqYards = length * width
                 / SQ_FT_PER_SQ_YARD;
}
// One of the overloaded mutator methods
public void SetNoOfSqYards
            (double squareYards)
{
    noOfSqYards = squareYards;
}
// Accessor method
public double GetNoOfSqYards( )
{
    return noOfSqYards;
}
public override string ToString( )
{
    return "Price Per Square Yard: " +
           pricePerSqYard.ToString("C") +
           "\nTotal Square Yards: " +
           noOfSqYards.ToString("F1") +
           "\nTotal Price: " +
           DetermineTotalCost().ToString("C");
}
}
```

The following file uses the CarpetCalculator class:

```
/* CarpetCalculatorApp.cs
 * Author: Doyle
 * This class instantiates an object
 * of the CarpetCalculator class. It
 * demonstrates how to access and use
 * the members of the class.
 */
using System;
namespace Carpet
```