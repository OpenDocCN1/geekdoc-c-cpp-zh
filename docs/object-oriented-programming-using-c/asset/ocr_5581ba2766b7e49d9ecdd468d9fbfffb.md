When each individual account is created we will add it to the list of accounts and we will also allow an individual account to be retrieved so that the account holder can deposit money into their account.

We will demonstrate this with a Main method that runs through a fixed routine a) adding a few accounts, b) displaying these accounts and c) retrieving an account, adding money to this account and displaying the list of accounts again.

We will need an accessor method in Bank that the Main method can access the list of accounts to display them. In C# we will implement this using a public property.

The code for the Account class is shown below and should need no explanation.

```
class Account
{
    private String name;
    public String Name
    {
        get { return name; }
    }

    private String dateOfBirth;
    public String DateOfBirth
    {
        get { return dateOfBirth; }
    }

    private int balance;

    public Account(String name, String dob)
    {
        this.name = name;
        this.dateOfBirth = dob;
        balance = 0;
    }

    public void DepositMoney(int increase)
    {
        balance = balance + increase;
    }

    public override String ToString()
    {
        return "Name: " + name + "\nBalance: " + balance;
    }
}
```