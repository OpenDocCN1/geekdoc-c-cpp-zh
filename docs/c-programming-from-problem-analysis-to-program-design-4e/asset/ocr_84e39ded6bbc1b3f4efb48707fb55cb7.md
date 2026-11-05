The actual call to the method expecting an array as an argument simply includes the identifier. It does not include the size or the square brackets. A call to the `DisplayArrayContents( )` method shown in Example 7-11 would be as follows:

```
```
DisplayArrayContents(waterDepth);
```
```

Recall that `waterDepth` is a `double [ ]` array.

Example 7-12 illustrates how the output statements can be placed in a method and called three times with different arguments each time. The first call sends the `waterDepth` array. The last two calls send the `w` array.

# **EXAMPLE 7.12**

```
```csharp
/* StaticMethods.cs    Author: Doyle
 * Demonstrates use of methods from the
 * System.Array class.
 */

using System;
using System.Windows.Forms;

namespace StaticMethods
{
    class StaticMethods
    {
        private const string CAPTION = "System.Array Methods " +
                                      "Illustrated";

        static void Main( )
        {
            double [ ] waterDepth = {45, 19, 2, 16.8, 190, 0.8,
                                     510, 6, 18};
            double [ ] w = new double [20];

            DisplayOutput(waterDepth, "waterDepth Array\n\n");

            // Copies values from waterDepth to w
            Array.Copy(waterDepth, 2, w, 0, 5);

            // Sorts Array w in ascending order
            Array.Sort (w);
            DisplayOutput(w, "Array w Sorted\n\n");

            // Reverses the elements in Array w
            Array.Reverse(w);
            DisplayOutput(w, "Array w Reversed\n\n");
        }
    }
}
```
```