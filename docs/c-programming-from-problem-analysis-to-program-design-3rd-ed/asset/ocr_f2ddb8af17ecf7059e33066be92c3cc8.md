```
```csharp
public static void DisplayInstructions( )
{
    Console.WriteLine("This program will "
                    + "determine how much "
                    + "carpet to purchase.");
    Console.WriteLine( );
    Console.WriteLine("You will be asked to "
                    + "enter the size of "
                    + "the room");
    Console.WriteLine("and the price of the "
                    + "carpet, in price per"
                    + " square yds.");
    Console.WriteLine( );
}

public static double GetDimension(string side )
{
    string inputValue;       // local variables
    int feet,                // needed only by this
        inches;              // method

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

public static double GetPrice( )
{
    string inputValue;       // local variables
    double price;

    Console.Write("Enter the price per Square"
                + "Yard: ");
    inputValue = Console.ReadLine( );
    price = double.Parse(inputValue);
    return price;
}
```
```