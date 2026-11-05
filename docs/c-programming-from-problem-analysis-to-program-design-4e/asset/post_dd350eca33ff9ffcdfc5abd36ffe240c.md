
The actual call to the method expecting an array as an argument simply includes the identifier. It does not include the size or the square brackets. A call to the `DisplayArrayContents()` method shown in Example 7-11 would be as follows:

```csharp
DisplayArrayContents(waterDepth);
```

Recall that `waterDepth` is a `double[]` array.

Example 7-12 illustrates how the output statements can be placed in a method and called three times with different arguments each time. The first call sends the `waterDepth` array. The last two calls send the `w` array.

## EXAMPLE 7.12

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

        static void Main()
        {
            double[] waterDepth = {45, 19, 2, 16.8, 190, 0.8,
                                   510, 6, 18};
            double[] w = new double[20];

            DisplayOutput(waterDepth, "waterDepth Array\n\n");

            // Copies values from waterDepth to w
            Array.Copy(waterDepth, 2, w, 0, 5);

            // Sorts Array w in ascending order
            Array.Sort(w);
            DisplayOutput(w, "Array w Sorted\n\n");

            // Reverses the elements in Array w
            Array.Reverse(w);
            DisplayOutput(w, "Array w Reversed\n\n");
        }

        // Displays an array in a MessageBox
        public static void DisplayOutput(double[] anArray,
                                         string msg)
        {
            foreach(double wVal in anArray)
                if (wVal > 0)
                    msg += wVal + "\n";
            MessageBox.Show(msg, CAPTION);
        }
    }
}
```

Notice how CAPTION is defined as a constant data member in the StaticMethods class. The declaration appears above the Main() method in Example 7-12. Doing this enabled each of the method members to have access to the string of characters without having to pass a value for the CAPTION to each method.

The parameter identifier anArray in the DisplayOutput() method is used as a placeholder for an array argument. The arrays are of different lengths, but this does not create a problem. Every element in the array is being processed using the foreach statement in the method. When array w is sent into the method, it is necessary to use the selection statement (if (wVal > 0)); otherwise, 20 lines are displayed. The foreach loop traverses through every element in the array. Array w is dimensioned to have a length of 20. Without the if statement, a number of 0 values are displayed when no other initialization values are given.

> **NOTE** Zero is used as the default value by the constructor for integer arrays. That includes sbyte, byte, short, ushort, int, uint, long, and ulong; their default value is 0. The default constructor values for decimal, float, and double are 0.0M, 0.0F, and 0.0D, respectively. False is the default for bool.

Figure 7-6 shows output from Example 7-12. It is exactly the same as the output produced from Example 7-10. The last example, Example 7-12, is more streamlined. Because array parameters are automatically treated as pass by reference, no additional keywords such as ref or out are required with the argument or parameter list.

> **NOTE** Remember, when you pass by reference, or call by reference, you pass the address of the identifier. A call or pass by value sends the actual data. When you pass a single array element such as an integer, you are passing by value. A copy of the current contents of that array element is made and sent to the method.

Consider the following that allocates memory for five elements:

```csharp
int[] temperature = new int[5];
```

The following method could be used to input values into the temperature array:

```csharp
public static void InputValues(int[] temp)
{
    string inValue;

    for(int i = 0; i < temp.Length; i++)
    {
        Console.Write("Enter Temperature {0}: ", i + 1);
        inValue = Console.ReadLine();
        temp[i] = int.Parse(inValue);
    }
}
```

A call to the method to input values follows:

```csharp
InputValues(temperature);
```

Figure 7-7 shows the result of inputting 78, 82, 90, 87, and 85.

![](img/36e48639a06772bcb0fa1ea2525b33a3_443_0.png)

**FIGURE 7-7** Array contents after the InputValues() method is called

When the InputValues() method is called, a reference to temperature is sent.

In Chapter 3, you learned that when an argument is sent using call by value, a copy of the argument's contents is made. The copy of the values is stored in new memory locations accessible only within that method. Changes made to the values do not impact the variables in the calling module. On return from the called method, the original value of the argument is unchanged. It contains the same value it had before the execution of the method.

With call by reference, no copy is made of the contents. A copy is made of the reference (address) to the location in which the array is stored, and the copy is stored in a variable. As shown in Figure 7-7, the formal parameter, temp, references the same location in memory as temperature does. The values entered into the temp array in the InputValues() method are stored in the memory cells referenced by temperature.

## Array Assignment

The assignment operator = may not work as you would think it should when used with reference types such as arrays. If an additional array is defined and an assignment is made, the assignment operator and the array reference the same elements. Individual elements are not copied to another memory location. Consider the following statements that could be written after the temperature array is filled with values:

```csharp
int[] t = new int[5];
t = temperature;
t[1] = 44;
```

Figure 7-8 illustrates the result of the assignment statements. Any reference to temperature[1] accesses 44.

![](img/36e48639a06772bcb0fa1ea2525b33a3_444_0.png)

**FIGURE 7-8** Assignment of an array to reference another array

Example 7-13 includes the complete code listing from the program statements used in Figures 7-7 and 7-8, which illustrate the assignment and use of arrays as method parameters.

## EXAMPLE 7.13

```csharp
/* PassingArray.cs   Author: Doyle
 * Demonstrates passing arrays to methods - references
 */

using System;

namespace PassingArray
{
    class PassingArray
    {
        static void Main()
        {
            int[] temperature = new int[5];
            int[] t = new int[5];

            InputValues(temperature);

            //Array t will reference the same array
            //as the temperature array.
            t = temperature;
            t[1] = 44;
            Console.WriteLine(temperature[1]);
            Console.WriteLine("Value stored in temperature[1]: {0}", temperature[1]);
            Console.ReadKey();
        }

        public static void InputValues(int[] temp)
        {
            string inValue;

            for(int i = 0; i < temp.Length; i++)
            {
                Console.Write("Enter Temperature {0}: ", i + 1);
                inValue = Console.ReadLine();
                if (int.TryParse(inValue, out temp[i]) == false)
                    Console.WriteLine("Invalid data entered - " +
                        "0 stored in array element");
            }
        }
    }
}
```

## Params Parameters

In Chapter 3, you were briefly introduced to the params parameter type. When a method uses the params modifier, the parameter is considered a parameter array. It is used to indicate that the number of arguments to the method may vary.

> **NOTE** If you include the `params` argument in the method heading, the array identifier it is used with must be the last parameter listed in the method heading. The identifier cannot be defined as a `ref` or `out` parameter.

The keyword `params` appears only in the formal parameter list of the method heading. By including it, the method may be called one time with a single value. Another call to the same method could send 10 or 100 values or an array of values. A variable number of arguments are accepted when `params` is included. It makes the method very flexible. Example 7-14 shows how a method defined with a parameter array can be called with both simple value arguments and with an array.

## EXAMPLE 7.14

```csharp
/* VaryingArguments.cs    Author: Doyle
 * This example demonstrates the use
 * of the params keyword. A varying
 * number of arguments can be sent
 * to a method.
 */

using System;

namespace VaryingArguments
{
    class VaryingArguments
    {
        public static void Main()
        {
            DisplayItems(1, 2, 3, 5);
            int[] anArray = new int[5] {100, 200, 300, 400, 500};
            DisplayItems(anArray);
            DisplayItems(1500, anArray[1] * anArray[2]);
            Console.ReadKey();
        }

        public static void DisplayItems(params int[] item)
        {
            for (int i = 0; i < item.Length; i++)
            {
                Console.Write(item[i] + "\t");
            }
            Console.WriteLine();
        }
    }
}
```
