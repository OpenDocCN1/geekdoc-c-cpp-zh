```
double insurance;
 double taxes;
 double utilities;
 string inValue;
 Console.Write("Yearly Insurance: ");
 inValue = Console.ReadLine( );
 insurance = double.Parse(inValue);
 Console.Write("Yearly Tax: ");
 inValue = Console.ReadLine( );
 taxes = double.Parse(inValue);
 Console.Write("Monthly Utilities: ");
 inValue = Console.ReadLine( );
 utilities = double.Parse(inValue);
 return (insurance / 12 + taxes / 12 + utilities);
 }
 }
}

/* RealEstateInvestment.cs
 * Author: Doyle
 * This class defines a template
 * for a real estate object to
 * include instance data members,
 * public properties,
 * constructors, and a method to
 * determine the monthly earnings.
 */
using System;
namespace PropertyApplication
{
    class RealEstateInvestment
    {
        private string streetAddress;
        private int yearBuilt;
        private double purchasePrice;
        private double monthlyExpense;
        private double incomeFromRent;

        // Read-only property
        public double YearBuilt
        {
            get
            {
                return yearBuilt;
            }
        }

        // Read-only property
        public string StreetAddress
```