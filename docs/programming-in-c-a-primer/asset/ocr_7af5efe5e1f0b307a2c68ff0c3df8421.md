```
taxAmount = taxAmount1 * taxRate;
    return taxAmount;
}
// This method also takes one argument: Tax Type (string) and returns
the tax rate
public double TaxCalculator(string taxType)
{
    double taxRate = 0;
    Console.WriteLine("-- Using TaxCalculator method containing 1 argument only of String type");
    if (taxType == "Personal")
        taxRate = 0.10;
        return taxRate;
}
}
class MethodOverload
{
    static void Main(string[] args)
    {
        string userResponse;
        bool flagHome = false;
        bool flagBusiness = false;
        double houseRate = 0;
        double houseValue = 0;
        double businessSales = 0;
        double taxRate = 0;
        double earning = 0;
        double totalTax = 0;
        TaxCalc tc=new TaxCalc();
        Console.WriteLine("Do you have a house registered in your name? (y/n)":
        userResponse = Console.ReadLine();
        if (userResponse == "y")
        {
            flagHome = true;
            Console.WriteLine("Enter the worth of the house in Rupees: ");
            userResponse = Console.ReadLine();
            houseValue = Convert.ToDouble(userResponse);
            Console.WriteLine("Enter the tax rate applicable for a house: ");
            userResponse = Console.ReadLine();
            houseRate = Convert.ToDouble(userResponse);
        }
        Console.WriteLine("Are you an owner of a business? (y/n)");
        userResponse = Console.ReadLine();
        if (userResponse == "y")
        {
            flagBusiness = true;
            Console.WriteLine("Enter the total sales for the year: ");
            userResponse = Console.ReadLine();
            businessSales = Convert.ToDouble(userResponse);
```