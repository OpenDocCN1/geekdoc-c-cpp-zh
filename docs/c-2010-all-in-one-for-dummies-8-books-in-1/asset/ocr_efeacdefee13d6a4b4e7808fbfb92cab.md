# 96 Here We Go Loop-Loop

You can use the while loop to create the CalculateInterestTable
program, a looping version of the CalculateInterestTable program.
CalculateInterestTable calculates a table of principals showing accu-
mulated payments:

![](bbox=[0.143, 0.215, 0.213, 0.298])

```
// CalculateInterestTable -- Calculate the interest paid on a given
// principal over a period of years.
using System;
namespace CalculateInterestTable
{
    using System;
    public class Program
    {
        public static void Main(string[] args)
        {
            // Define a maximum interest rate.
            int maximumInterest = 50;
            // Prompt user to enter source principal.
            Console.Write("Enter principal: ");
            string input = Console.ReadLine();
            decimal principal = Convert.ToDecimal(input);
            // If the principal is negative
            if (principal < 0)
            {
                // generate an error message
                Console.WriteLine("Principal cannot be negative");
            }
            else // here only if principal was > 0: thus valid.
{
                // otherwise, enter the interest rate.
                Console.Write("Enter interest: ");
                string input = Console.ReadLine();
                decimal interest = Convert.ToDecimal(input);
                // If the interest is negative or too large
                if (interest < 0 || interest > maximumInterest)
                {
                    // generate an error message well.
                    Console.WriteLine("Interest cannot be negative " + "or greater than " + maximumInterest);
                    interest = 0;
                }
                else // Reach this point only if all is valid.
{
                    // Both the principal and interest appear to be
                    // legal; input the number of years.
                    Console.Write("Enter number of years: ");
                    string input = Console.ReadLine();
                    int duration = Convert.ToInt32(input);
                    // Verify the input.
                    Console.WriteLine("Principal = " + principal);
                    Console.WriteLine("Interest = " + interest + "%%");
                    Console.WriteLine("Duration = " + duration + " years");
                    Console.WriteLine();
                }
            }
}
            // Now loop through the specified number of years.
            int year = 1;
            while(year < duration)
{
                // Calculate the value of the principal plus interest.
                decimal interestPaid;
                interestPaid = principal * (interest / 100);
```