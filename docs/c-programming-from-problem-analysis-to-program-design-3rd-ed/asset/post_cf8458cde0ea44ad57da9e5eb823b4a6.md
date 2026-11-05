
### Example 7-8

```csharp
int total = 0;
double avg;
foreach(int val in score)
{
    total += val;
}
Console.WriteLine("Total: " + total);
avg = (double)total / scoreCnt;
Console.WriteLine("Average: " + avg);
```

The identifier, val, is the iteration variable. It represents a different array element with each loop iteration. Remember that the type used in the foreach expression should match the array type. Because the score array contains int elements, val is declared of that type. During the first iteration through the loop, val references score[0]. A compile-time error occurs if one of the statements in the foreach loop body attempts to change the iteration variable or pass the iteration variable as a ref or out parameter. Example 7-9 displays red, blue, and green on separate lines.

### Example 7-9

```csharp
string[] color = {"red", "green", "blue"};
foreach(string val in color)
    Console.WriteLine(val);
```

## ARRAY CLASS

Through access to the elements using indexed values, C# supports the easy handling of arrays that other languages provide. But you get more than just indexed access. All arrays, of any type, inherit characteristics from the Array class, which includes a number of predefined methods and properties. Table 7-1 lists some of these predefined methods from the System.Array class. The third column gives examples of the use of each method. You will want to explore methods, especially those that are overloaded, using the online Help features in Visual Studio. Much of the information in Table 7-1 came from that documentation. As you explore the Array class methods, you will find a number of other members not listed in Table 7-1. The Array class serves as the base array class for all languages that target the common language runtime. Having its properties and methods available across languages provides power to each of the .NET languages, and this power is available with minimal programming. For example, an entire collection of data can be sorted with a call to one of the Array class member methods.

### Table 7-1 System.Array class methods

| Method | Description | Examples |
|---|---|---|
| `BinarySearch (System.Array array, object value)` | Class method. Overloaded. Searches a one-dimensional sorted array for a value, using a binary search algorithm. Returns index location or negative value if not found. | `double[] waterDepth = {2.4, 3.5, 6.8};`<br>`double x = 6.8;`<br>`int myIndex = Array.BinarySearch (waterDepth, x);`<br>`Console.WriteLine (myIndex);`<br>`//Displays 2 (This is the index of 6.8.)` |
| `Clear (System.Array array, int firstIndex, int length)` | Class method. Sets elements in the array to zero, to false, or to a null reference depending on the element type. Start at `firstIndex`, go `length` positions. | `double[] waterDepth = {2.4, 3.5, 6.8};`<br>`Array.Clear (waterDepth, 1, 1);`<br>`//Sets a range of array elements`<br>`//beginning at index 1, for a`<br>`//length of 1, to zero`<br>`Console.WriteLine (waterDepth[1]);`<br>`//Displays 0` |
| `Clone()` | Creates a copy of the array. Returns an object. | `double[] waterDepth = {2.4, 3.5, 6.8};`<br>`double[] w = new Double[3];`<br>`object o = waterDepth.Clone ();`<br>`w = (double[]) o;`<br>`//object cast as an array` |
| `Copy (System.Array sourceArray, int firstIndexSource, System.Array targetArray, int firstIndexTarget, int lengthToCopy)` | Class method. Overloaded. Copies a section of one array to another array. | `double[] waterDepth = {2.4, 3.5, 6.8};`<br>`double[] w = new Double[3];`<br>`Array.Copy (waterDepth, 0, w, 0, 3);`<br>`//Copies three elements from waterDepth`<br>`//to w`<br>`//Begins copy at index 0 in waterDepth;`<br>`//begins place at index 0`<br>`//index 0 in w array.` |
| `CopyTo (System.Array targetArray, int targetArrayStartLocation)` | Copies elements of a one-dimensional array to another one-dimensional array starting at the specified destination array index. (Destination must be large enough to hold elements.) | `double[] waterDepth = {2.4, 3.5, 6.8};`<br>`double[] w = new Double[5];`<br>`waterDepth.CopyTo (w, 2);`<br>`Console.WriteLine (w[3]);`<br>`//Displays 3.5 (copy started at w[2])`<br>`//w[0] = 0, w[1] = 0, w[2] = 2.4, w[4] = 6.8` |
| `GetValue(int index)` | Overloaded. Gets the value of the specified element in the current array. | `double[] waterDepth = {2.4, 3.5, 6.8};`<br>`Console.WriteLine`<br>`    (waterDepth.GetValue(1));`<br>`//Displays 3.5` |
| `IndexOf(System.Array array, object value)` | Class method. Overloaded. Returns the index of the first occurrence of a value in a one-dimensional array or in a portion of the array. | `double[] waterDepth = {2.4, 3.5, 6.8};`<br>`int i = Array.IndexOf(waterDepth, 3.5);`<br>`Console.WriteLine(i);`<br>`//Displays 1`<br>`//Returns -1 when the value is not found in the array` |
| `LastIndexOf(System.Array array, object value)` | Class method. Overloaded. Returns the index of the last occurrence of a value in a one-dimensional array or in a portion of the array. | `double[] waterDepth = {2.4, 3.5, 6.8, 2.4};`<br>`int i = Array.LastIndexOf(waterDepth, 2.4);`<br>`Console.WriteLine(i);`<br>`//Displays 3` |
| `Reverse(System.Array array)` | Class method. Overloaded. Reverses the order of the elements in a one-dimensional array or in a portion of the array. | `double[] waterDepth = {2.4, 3.5, 6.8};`<br>`Array.Reverse(waterDepth);`<br>`foreach (double wVal in waterDepth)`<br>`    Console.Write(wVal + "\t");`<br>`//Displays 6.8  3.5  2.4` |
| `SetValue(object value, int indexLocation)` | Overloaded. Sets the specified element in the current array to the specified value. | `double[] waterDepth = {2.4, 3.5, 6.8};`<br>`waterDepth.SetValue(55, 0);`<br>`foreach (double wVal in waterDepth)`<br>`    Console.Write(wVal + "\t");`<br>`//Displays 55  3.5  6.8` |
| `Sort(System.Array array)` | Class method. Overloaded. Sorts the elements in one-dimensional array objects. | `double[] waterDepth = {12.4, 3.5, 6.8};`<br>`Array.Sort(waterDepth);`<br>`foreach (double wVal in waterDepth)`<br>`    Console.Write(wVal + "\t");`<br>`//Displays 3.5  6.8  12.4` |

Some of the descriptions listed in the second column of Table 7-1 indicate “Class method.” You have used `class` methods from the `Math` class. To call a `class` method, you prefix the method name with the `class` name. As you review the examples in the third column, notice that these `class` method calls require `Array` to be listed before the method name.

Example 7-10 demonstrates the use of `Sort()`, `Reverse()`, and `Copy()` methods. Values are concatenated onto a `string` inside a `foreach` loop structure. On the outside of the loop, the `string` is displayed with one call to the `MessageBox.Show()` method.

### Example 7-10

```csharp
/* UsePredefinedMethods.cs   Author: Doyle
 * Demonstrates use of methods from the
 * System.Array class.
 */
using System;
using System.Windows.Forms;
namespace UsePredefinedMethods
{
    class UsePredefinedMethods
    {
        static void Main( )
        {
            double[] waterDepth = {45, 19, 2, 16.8,
                                    190, 0.8, 510, 6, 18 };
            string outputMsg = "";
            string caption = "System.Array Methods Illustrated";
            double[] w = new double[20];

            // Displays contents of Array waterDepth
            outputMsg += "waterDepth Array\n\n";
            foreach(double wVal in waterDepth)
                outputMsg += wVal
                    + "\n";
            MessageBox.Show(outputMsg, caption);

            // Copies 5 values from waterDepth,
            // beginning at indexed location 2.
            // Place values in Array w, starting
            // at index location 0.
            Array.Copy(waterDepth, 2, w, 0, 5);

            // Sorts Array w in ascending order
            Array.Sort (w);

            // Displays Array w sorted
            outputMsg = "Array w Sorted\n\n";
            foreach(double wVal in w)
            {
                if (wVal > 0)
                    outputMsg += wVal
                        + "\n";
            }
            MessageBox.Show(outputMsg, caption);

            // Reverses the elements in Array w
            Array.Reverse(w);
        }
    }
}
```
