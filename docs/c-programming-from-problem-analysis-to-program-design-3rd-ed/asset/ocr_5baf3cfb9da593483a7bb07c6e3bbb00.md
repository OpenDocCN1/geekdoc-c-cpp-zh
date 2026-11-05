```
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
        }
```