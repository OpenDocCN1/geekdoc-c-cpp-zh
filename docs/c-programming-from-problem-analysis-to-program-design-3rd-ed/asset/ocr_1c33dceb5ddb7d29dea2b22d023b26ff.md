Use a calculator and write down the results you obtain. After you implement your design, you can compare these results with those obtained from your program output.

# Code the Solution

After you complete the design and verify the algorithm's correctness, it is time to translate the design into source code. For this application, you are creating two separate files—one for each class. Only one of the classes will have a Main( ) method. If you create the RealEstateInvestment class first, delete the Main( ) method from that file. To add a second class, click Project, Add Class.

The final application listing for both files appears here:

```
```csharp
/* RealEstateApp.cs      Author:      Doyle
 * This class constructs an
 * object of the RealEstateInvestment
 * class. It tests several properties and
 * methods of the class.
 * A static method is used in
 * the application class to
 * input expenses.
 * */
using System;
namespace PropertyApplication
{
    public class RealEstateApp
    {
        public static void Main( )
        {
            const double RENTAL_AMOUNT = 1000.00;

            RealEstateInvestment invest1 = new
                RealEstateInvestment (2004, 150000,
                "65th Street");

            invest1.MonthlyExpense = GetExpenses( );
            invest1.IncomeFromRent = RENTAL_AMOUNT;
            Console.WriteLine( );
            Console.WriteLine("Property Location: {0}",
                invest1.StreetAddress);
            Console.WriteLine("Earnings For Month: {0:C}",
                invest1.DetermineMonthlyEarnings( ));
            Console.Read( );
        }

        public static double GetExpenses( )
        {
```
```