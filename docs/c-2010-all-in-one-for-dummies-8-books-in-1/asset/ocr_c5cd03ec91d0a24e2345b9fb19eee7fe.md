# Having Arguments with Methods 239

```
// Wait for user to acknowledge.
Console.WriteLine("Press Enter to terminate...");
Console.Read();

// AverageAndDisplay - Average two numbers with their
// labels and display the results.
public static void AverageAndDisplay(string s1, double d1,
    string s2, double d2)

// var okay here, it's truly really.
var average = (d1 + d2) / 2;
Console.WriteLine("The average of " + s1 + " whose value is " + d1 + 
    " and " + s2 + " whose value is " + d2 + " is " + average");
```

C# can't match the type of each argument in the class to AverageAnd
Display() with the corresponding argument in the method definition. The
string "grade" matches the first string in the method definition: how-
ever, the method definition calls for a double as its second argument rather
t the string that's passed.

You can easily see that I simply transposed the second and third arguments.
(That's what I hate computers — they take me too literally. I know
what I said, but it's obvious what I meant!)

To fix the problem, swap the second and third arguments.

# Overloading a method doesn't mean giving it too much to do

You can give two methods within a given class the same name — known as
overloading the method name — as long as they differ.

This example demonstrates Overloaded:

```
// AverageAndDisplay -- This version demonstrates that
// the AverageAndDisplay method can be overloaded.
using System;
namespace AverageAndDisplayOverloaded
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Access the first version of the method.
            AverageAndDisplay("my GPA", 3.5, "your GPA", 4.0);
            Console.WriteLine();
            // Access the second version of the method.
        }
}
```

![](bbox=[0.135, 0.625, 0.205, 0.7])

![](bbox=[0.125, 0.73, 0.205, 0.805])

Book II Chapter 3

We Have Our Methods