but also defines a method to transfer money directly to a different account (code file UsingInterfaces/ITransferBankAccount):

```
namespace Wrox.ProCSharp
{
    public interface ITransferBankAccount: IBankAccount
    {
        bool TransferTo(IBankAccount destination, decimal amount);
    }
}
```

Because ITransferBankAccount is derived from IBankAccount, it gets all the members of IBankAccount as well as its own. That means that any class that implements (derives from) ITransferBankAccount must implement all the methods of IBankAccount, as well as the new TransferTo method defined in ITransferBankAccount. Failure to implement all these methods results in a compilation error.

Note that the TransferTo method uses an IBankAccount interface reference for the destination account. This illustrates the usefulness of interfaces: When implementing and then invoking this method, you don’t need to know anything about what type of object you are transferring money to—all you need to know is that this object implements IBankAccount.

To illustrate ITransferBankAccount, assume that the Planetary Bank of Jupiter also offers a current account. Most of the implementation of the CurrentAccount class is identical to implementations of SaverAccount and GoldAccount (again, this is just to keep this example simple—that won’t normally be the case), so in the following code only the differences are highlighted (code file UsingInterfaces/JupiterBank.cs):

```
public class CurrentAccount: ITransferBankAccount
{
    private decimal _balance;

    public void PayIn(decimal amount) => _balance += amount;

    public bool Withdraw(decimal amount)
    {
        if (_balance >= amount)
        {
            _balance -= amount;
            return true;
        }
        WriteLine("Withdrawal attempt failed.");
        return false;
    }

    public decimal Balance => _balance;

    public bool TransferTo(IBankAccount destination, decimal amount)
    {
        bool result = Withdraw(amount);
        if (result)
        {
```