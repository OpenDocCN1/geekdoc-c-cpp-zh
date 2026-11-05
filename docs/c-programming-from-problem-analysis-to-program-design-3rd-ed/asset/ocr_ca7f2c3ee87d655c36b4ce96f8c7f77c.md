```
using System;
namespace AgeExample
{
    public class AgeIncrementer
    {
        public static void Main()
        {
            int age;
            string aValue;

            Console.Write("Enter your age: ");
            aValue = Console.ReadLine();
            age = int.Parse(aValue);
            Console.WriteLine("Your age next year"
                + " will be {0}", ++age);
            Console.Read();
        }
    }
}
```

# ReadKey( ) Method

The ReadKey( ) method obtains the next character or function key pressed by the user. This method can be called if you want the user to press some key to continue processing. It could also be placed as the last line of executable code in the Main( ) method.

# Parse( ) Method

Another predefined static method you will use often is the Parse( ) method. As stated previously, Parse( ) returns the number representation of its string argument. All numeric types have a Parse( ) method. In Example 3-9, an int value is returned when the Parse( ) method finishes. Parse( ) can also be called with a double object, as illustrated in Example 3-10.

# Example 3-10

```
/* *****************************************
 * SquareInputValue.cs              Author: Doyle
 * Allows an integer value to be input.
 * Computes and displays the square of the
 * value inputted.
 *
 *****************************************/
using System;
namespace Square
{
    class SquareInputValue
    {
```