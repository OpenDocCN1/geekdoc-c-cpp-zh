```
```csharp
DisplayInstructions( );

// Call getDimension( ) to get the length
roomLength = GetDimension("Length");

// Call getDimension( ) again to get the width
roomWidth = GetDimension("Width");
berber.SetNoOfSqYards(roomLength, roomWidth);
berber.PricePerSqYard = 25.99;
Console.Clear( );
Console.Write(berber);
Console.ReadLine();
}

public static void DisplayInstructions( )
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

public static double GetDimension(string side)
{
    string inputValue;     // local variables
    int feet,              // needed only by this
        inches;            // method

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
```

![](bbox=[0.928, 0.273, 1.0, 0.383])