method is called twice. It is called first with the string argument of “Length” and second with “Width” as the argument. The value that is returned from the GetDimension( ) method each time is stored in different variables.

![](bbox=[0.22, 0.22, 0.28, 0.32])

> Whenever possible, you should write code that can be reused. Often, if you spend a little extra effort thinking through your design, you can write a generalized solution and reap the benefits later. A simple example of this is writing one method, GetDimension( ), to retrieve both the width and height. It is called two times with different messages or arguments.

# Example 3-17

```
/* CarpetExampleWithClassMethods.cs
 * Author: Doyle
 * Calculates the total cost of carpet. User
 * inputs room dimensions and carpet price.
 */
using System;
namespace CarpetExampleWithClassMethods
{
    public class CarpetWithClassMethods
    {
        public static void Main( )
        {
            double roomWidth;
            double roomLength;
            double pricePerSqYard;
            double noOfSqYards;

            DisplayInstructions( );

            // Call GetDimension( ) to get the length
            roomLength = GetDimension("Length");

            // Call GetDimension( ) again to get the
            // width
            roomWidth = GetDimension("Width");
            pricePerSqYard = GetPrice( );
            noOfSqYards =
                DetermineSqYards(roomWidth, roomLength);
            DisplayResults(noOfSqYards,
                pricePerSqYard);
        }
    }
}
```