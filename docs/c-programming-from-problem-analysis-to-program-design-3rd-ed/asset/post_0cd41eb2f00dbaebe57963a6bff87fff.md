
```
public double DetermineTotalCost( )
{
    return (pricePerSqYard * noOfSqYards);
}
// One of the overloaded mutator methods
public void SetNoOfSqYards(double length,
                           double width)
{
    const int SQ_FT_PER_SQ_YARD = 9;

    noOfSqYards = length * width
                 / SQ_FT_PER_SQ_YARD;
}
// One of the overloaded mutator methods
public void SetNoOfSqYards
            (double squareYards)
{
    noOfSqYards = squareYards;
}
// Accessor method
public double GetNoOfSqYards( )
{
    return noOfSqYards;
}
public override string ToString( )
{
    return "Price Per Square Yard: " +
           pricePerSqYard.ToString("C") +
           "\nTotal Square Yards: " +
           noOfSqYards.ToString("F1") +
           "\nTotal Price: " +
           DetermineTotalCost().ToString("C");
}
}
```

The following file uses the CarpetCalculator class:

```
/* CarpetCalculatorApp.cs
 * Author: Doyle
 * This class instantiates an object
 * of the CarpetCalculator class. It
 * demonstrates how to access and use
 * the members of the class.
 */
using System;
namespace Carpet
{
    public class CarpetCalculatorApp
    {
        public static void Main( )
        {
            CarpetCalculator berber =
                new CarpetCalculator(17.95);
            double roomWidth;
            double roomLength;
            DisplayInstructions( );
            // Call GetDimension( ) to get the length
            roomLength = GetDimension("Length");
            // Call GetDimension( ) again to get the width
            roomWidth = GetDimension("Width");
            berber.SetNoOfSqYards
                (roomLength, roomWidth);
            berber.PricePerSqYard = 25.99;
            Console.Clear( );
            Console.Write(berber);
            Console.ReadLine();
        }
        static void DisplayInstructions( )
        {
            Console.WriteLine("This program will"
                + " determine how much "
                + "carpet to purchase.");
            Console.WriteLine( );
            Console.WriteLine("You will be asked to "
                + "enter the size of the "
                + "room and the price of the");
            Console.WriteLine("carpet, in price per "
                + "square yds.");
            Console.WriteLine( );
        }
        static double GetDimension(string side)
        {
            string inputValue;    // local variables
            int feet,             // needed only by this
                inches;           // method
            Console.Write("Enter the {0} in feet: ",
                side);
            inputValue = Console.ReadLine( );
            feet = int.Parse(inputValue);
            Console.Write("Enter the {0} in inches: ",
                side);
            inputValue = Console.ReadLine( );
            inches = int.Parse(inputValue);

            // Note: cast required to avoid int division
            return (feet + (double) inches / 12);
        }
    }
}
```

As you review Example 4-18, notice that a property was defined in the CarpetCalculator class called PricePerSqYard. This property is tied to the pricePerSqYard data member, which was defined with an access mode of private. Recall that data members are named using camel case, while property identifiers follow the Pascal case convention; thus, the only difference in their names was the first character. pricePerSqYard can be referenced in the class where it is defined, but because it is defined with an access mode of private, it cannot be referenced outside of the defining class.

In the second class, CarpetCalculatorApp, an object of the CarpetCalculator class is instantiated. The object identifier is berber. The object is instantiated with the new operator as shown here:

~~~
CarpetCalculator berber = new CarpetCalculator(17.95);
~~~

Since a double value, 17.95, is sent in as an argument to the constructor, the one argument constructor is used. 17.95 goes into price and that value is placed in the private data member pricePerSqYard as shown here in the constructor:

~~~
public CarpetCalculator(double price)
{
    pricePerSqYard = price;
}
~~~

In order to change berber's pricePerSqYard in the CarpetCalculatorApp class, you must use the property PricePerSqYard. The private pricePerSqYard data member is not accessible in the second class. The pricePerSqYard was changed to 25.99 with the statement shown below:

~~~
berber.PricePerSqYard = 25.99;
~~~

The PricePerSqYard property has get and set clauses. In order for classes that instantiate objects of the CarpetCalculator class to change the object's PricePerSqYard, they use the set clause associated with the public property. The object's private data member's value (i.e., pricePerSqYard) is retrieved through the public property's get clause.

Next, in the Main( ) method of the CarpetCalculatorApp class, the mutator method SetNoOfSqYards( ) was invoked. Notice that this method, like the property reference above had to be invoked with an object. It too also offers a public access mode; thus, it is available in classes instantiating objects of the CarpetCalculator class. The object was berber for this example. A public property could have been defined for noOfSqYards instead of a mutator method. The public property NoOfSqYards would have been tied to the private noOfSqYards data member.

The last interesting statement in Main( ) for Example 4–18 is the Console.Write (berber) statement. Here the ToString ( ) method, defined in the CarpetCalculator class, is automatically invoked with the berber object. The CarpetCalculator class provided a new definition for the object’s ToString ( ) method. The keyword override was used on the method heading in the CarpetCalculator class.

Figure 4–7 shows the output for the preceding application when the user enters a room measurement of 17 feet, 10 inches for length, and 14 feet, 6 inches for the width.

![](img/e33ae760e23d89eac66541252ad65de8_246_0.png)

**Figure 4–7**  Output from Carpet example using instance methods

Much material is presented in this chapter. The programming example that follows makes use of most of these new concepts.

## PROGRAMMING EXAMPLE: REALESTATEINVESTMENT

This example demonstrates the use of methods in a program. Both static and instance methods are used. Properties that are new to C# are included in the solution. The problem specification is shown in Figure 4-8.

How much cash flow profit is a rental investment generating? Create an application to determine what the cash flow is for a real estate investment used as a rental.

Design an object-oriented solution. Use two classes.

For the real estate property class, characteristics such as the year the home was built, purchase price, and street address will help identify the current state of an object. The real estate object also has a monthly income amount from rent and a monthly expense characteristic. Include a method to determine what the monthly earnings, or cash flow, is based on deducting the total monthly expenses from the monthly rental income.

In the second class, instantiate an object of the real estate property class. Call the constructor that creates an object using year built, purchase price, and street address. Allow the user to input the yearly taxes and insurance expenses. The monthly utilities costs should also be considered. In this application class, calculate a monthly expense based on the inputted values. Set the appropriate data field in the real estate property object.

Write code in the application class to display the property address and the expected cash flow for a given month.

Figure 4-8 Problem specification for RealEstateInvestment example

## Analyze the Problem

You should review the problem specification in Figure 4-8 and make sure you understand the problem definition. Several values must be entered into the program. These values must be entered as `string` variables and then parsed into numeric fields, so that arithmetic can be performed.

Two separate classes are to be developed. Creating a separate `class` for the real estate `object` enables this `class` to be used by many different applications. One application is to produce a listing showing the cash flow from the investment. Other applications might include determining total investment dollar amounts or locations of investments. If the characteristics of real estate objects are abstracted out, many applications can reuse the `class`.

## Variables

Tables 4-2 and 4-3 list the data items needed for the RealEstateInvestment problem.

### Table 4-2 Instance variables for the RealEstateInvestment class

| Data item description | Type | Identifier |
|---|---|---|
| Year the home was built | `int` | yearBuilt |
| Location of the home | `string` | streetAddress |
| Original purchase price | `double` | purchasePrice |
| Total expenses for average month | `double` | monthlyExpense |
| Rental premium per month | `double` | incomeFromRent |

The `class` that is using the RealEstateInvestment `class` also needs data. As noted in the problem specification, the application `class` allows the user to enter values for expenses. Table 4-3 identifies some of the local variables needed by the application `class`.

### Table 4-3 Local variables for the property application class

| Data item description | Type | Identifier |
|---|---|---|
| Cost of insurance per year | `double` | insurance |
| Amount of taxes per year | `double` | taxes |
| Estimated monthly utility costs | `double` | utilities |
| String value for inputting values | `string` | inValue |

## Constants

The rental rate is set as a constant value. The identifier and preset constant value will be `RENTAL_AMOUNT = 1000.00`.
