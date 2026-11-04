+   - An initial input section in which the user inputs the principal, interest, and duration information
+   - A section mirroring the input data so that the user can verify the entry of the correct data
+   - A section that creates and outputs the table

Use this list to start looking for ways to refactor the program. In fact, if you further examine the input section of that program, you can see that the same basic code is used to input these amounts:

+   - Principal
+   - Interest
+   - Duration

Your observation gives you another good place to look. Alternatively, you can write empty methods for some of those comments and then fill them in one by one. That's programming by intention.

I used the techniques for planning a method to create the following version of the CalculateInterestTableWithMethods program:

![](bbox=[0.12, 0.7, 0.25, 0.85])

```
// CalculateInterestTableWithMethods -- Generate an interest table
// much like the other interest table programs, but this time using a
// reasonable division of labor among several methods.
using System;
namespace CalculateInterestTableWithMethods
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Section 1 -- Input the data you need to create the table.
            decimal principal = 0M;
            decimal interest = 0M;
            decimal duration = 0M;
            InputInterestData(ref principal, ref interest, ref duration);
            // Section 2 -- Verify the data by mirroring it back to the user.
            Console.WriteLine(); // Skip a line.
            Console.WriteLine("Principal   = " + principal);
            Console.WriteLine("Interest    = " + interest + "%");
            Console.WriteLine("Duration    = " + duration + " years");
            Console.WriteLine();
            // Section 3 -- Finally, output the interest table.
            OutputInterestTable(principal, interest, duration);
            // Allow the user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
        // InputInterestData -- Retrieve from the keyboard the
        // principal, interest, and duration information needed
        // to create the future value table. (Implements Section 1.)
        public static void InputInterestData(ref decimal principal,
            ref decimal interest,
            ref decimal duration)
        {
```