```
decimal interestPaid;
interestPaid = principal * (interest / 100);
// Now calculate the total.
decimal total = principal + interestPaid;
```

The first equation multiplies the principal times the interest interest to produce the interest to be paid — interestPaid. (You divide by 100 because interest is usually calculated by entering a percentage amount.) The interest to be paid is then added back into the principal, resulting in a new principal, which is stored in the variable total.

The program must anticipate almost anything when dealing with human input. For example, you don't want your program to accept a negative principal or interest amount (well, maybe a negative interest). The following CalculateInterest program includes checks to ensure that neither of these entries happens:

![](bbox=[0.15, 0.55, 0.25, 0.7])

```
// CalculateInterest -- Calculate the interest amount paid
// on a given principal. If either the principal or the
// interest rate is negative, generate an error message.
using System;
namespace CalculateInterest
{
public class Program
{
public static void Main(string[] args)
{
// Prompt user to enter source principal.
Console.Write("Enter principal: ");
string principalInput = Console.ReadLine();
decimal principal = Convert.ToDecimal(principalInput);
// Make sure that the principal is not negative.
if (principal < 0)
{
Console.WriteLine("Principal cannot be negative");
principal = 0;
}
// Enter the interest rate.
Console.Write("Enter interest: ");
string interestInput = Console.ReadLine();
decimal interest = Convert.ToDecimal(interestInput);
// Make sure that the interest is not negative either.
if (interest < 0)
{
Console.WriteLine("Interest cannot be negative");
interest = 0;
}
// Calculate the value of the principal plus interest.
decimal interestPaid = principal * (interest / 100);
// Now calculate the total.
decimal total = principal + interestPaid;
// Output the result.
Console.WriteLine();
Console.WriteLine("Principal = " + principal);
Console.WriteLine("Interest = " + interest + "%");
Console.WriteLine();
Console.WriteLine("Interest paid = " + interestPaid);
Console.WriteLine("Total = " + total);
}
}
}
```