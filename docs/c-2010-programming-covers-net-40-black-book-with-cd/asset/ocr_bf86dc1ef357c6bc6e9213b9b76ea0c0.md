```
}
public double AmountOfDebitorCredit()
{
    return Amount;
}
public delegate Boolean AccountEventHandler(object sender, MyEventArgs e);
public class Account
{
    private double Total;
    private AccountEventHandler ah = null;
    public Account()
    {
        Total = 0;
    }
    public double getTotal()
    {
        return Total;
    }
    // Method to add a new OnPost handler
    public void AddonPost(AccountEventHandler handler)
    {
        ah = (AccountEventHandler)Delegate.Combine(ah, handler);
    }
    // Method to remove an OnPost handler
    public void RemoveOnPost(AccountEventHandler handler)
    {
        ah = (AccountEventHandler)Delegate.Remove(ah, handler);
    }
    // Handle the debit case
    public void PostDebit(double amt)
    {
        // First, create an argument list
        MyEventArgs ev = new MyEventArgs(true, amt);
        // Fire the event, checking to see if the return is ok
        Boolean okToSubtract = true;
        if (ah != null)
            okToSubtract = ah(this, ev);
        if (okToSubtract)
        {
            Console.WriteLine("Debit ok!");
            Total -= amt;
        }
        else
        {
            Console.WriteLine("Debit NOT ok! Not posting");
        }
    }
    public void PostCredit(double amt)
    {
        // First, create an argument list
        MyEventArgs ev = new MyEventArgs(false, amt);
        // Fire the event, checking to see if the return is ok
        Boolean okToAdd = true;
        if (ah != null)
            okToAdd = ah(this, ev);
        if (okToAdd)
            Total += amt;
    }
}
class Program
{
    public static Boolean CheckPost(object o, MyEventArgs arg)
    {
        if (arg.IsADebit()
```