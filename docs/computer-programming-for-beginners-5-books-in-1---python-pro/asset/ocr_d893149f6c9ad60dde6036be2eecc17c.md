```
```csharp
//declare an event of type delegate
public event BeforeDisplay beforeDisplayEvent;

public DisplayHelper()
{

}
public void DisplayNumber(int x)
{
    //call the delegate method before moving to display
    if (beforeDisplayEvent != null)
        beforeDisplayEvent();

    Console.WriteLine("Number: {0,-12:N0}", x);
}

public void PrintDecimal(int dec)
{
    if (beforeDisplayEvent != null)
        beforeDisplayEvent();

    Console.WriteLine("Decimal: {0:G}", dec);
}
public void DisplayMoney(int amount)
{
    if (beforeDisplayEvent != null)
        beforeDisplayEvent();

    Console.WriteLine("Money: {0:C}", amount);
}

public void DisplayTemperature(int x)
{
    if (beforeDisplayEvent != null)
        beforeDisplayEvent();
```
```