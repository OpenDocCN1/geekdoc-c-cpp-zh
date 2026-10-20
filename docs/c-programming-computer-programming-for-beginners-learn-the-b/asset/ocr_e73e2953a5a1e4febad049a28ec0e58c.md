```
{
    tCode = c;
    date = d;
    amount = a;
}
public double getAmount()
{
    return amount;
}
public void showTransaction()
{
    Console.WriteLine("Transaction: {0}", tCode);
    Console.WriteLine("Date: {0}", date);
    Console.WriteLine("Amount: {0}", getAmount());
}
}
class Tester
{
```