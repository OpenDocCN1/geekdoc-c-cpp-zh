selecting items and executing methods for them. In many dialog boxes, such as the Open dialog box, double-clicking a list entry selects that item and closes the dialog box as well (which is the same as selecting the item and clicking the OK button).

Let’s create a Console application, named FiringEvent (also available in the CD). Listing 6.18 shows the code of the Program.cs file of the FiringEvent application:

# Listing 6.18: Showing the Code of the Program.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
public delegate Boolean AccountEventHandler(object sender, double amt);
namespace FiringEvent
{
public class Account
{
    private double Total;
    public AccountEventHandler ah = null;
    public Account() {
        Total = 0;
    }
    public double getTotal() {
        return Total;
    }
    public void AddOnPost(AccountEventHandler handler)
    {
        ah = (AccountEventHandler)Delegate.Combine(ah, handler);
    }
    public void RemoveOnPost(AccountEventHandler handler)
    {
        ah = (AccountEventHandler)Delegate.Remove(ah, handler);
    }
    public Boolean OnPost(double amt) {
        if (ah != null)
            return ah(this, amt);
        return true;
    }
    public void PostDebit(double amt)
    {
        // Fire the event, checking to see if the return is ok
        Boolean okToSubtract = OnPost(amt);
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
        Total += amt;
    }
}
class Program
{
    public static Boolean CheckPost(object o, double d)
    {
        // See if it went negative
        Account a = (Account)o;
        if (d > a.getTotal())
            return false;
```