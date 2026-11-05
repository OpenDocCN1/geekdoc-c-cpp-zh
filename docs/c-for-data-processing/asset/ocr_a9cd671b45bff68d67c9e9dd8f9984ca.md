```
// structure
struct Account
{
    public AccountState State;
    public string Name ;
    public string Address ;
    public int AccountNumber ;
    public int Balance ;
    public int Overdraft ;
}
// program
class BankProgram
{
    public static void Main ()
    {
        Account RobsAccount;
        RobsAccount.State = AccountState.Active;
        RobsAccount.Name = "Rob Miles";
        RobsAccount.Address = "His house";
        RobsAccount.AccountNumber = 1234;
        RobsAccount.Balance = 0;
        RobsAccount.Overdraft = -1000;
        Console.WriteLine ( "Name is: " + RobsAccount.Name ) ;
        Console.WriteLine ( "Balance is: " + RobsAccount.Balance ) ;
    }
}
```

Note how the structure and enum are declared outside the BankProgram class. Once I have created my structure I can use it in the same way that I would use something like Int or Float.

This program doesn't create an array of structures, but it does show you how to access the various fields in a single structure variable.

# Initial values in structures

When a structure is created as a local variable (i.e. in a block) the values in it are undefined. This means that if you try to use them in your program you will get a compilation error. This is exactly the same as if you use a variable in a program before giving it a value. In other words:

```
Account RobsAccount;
Console.WriteLine ( "Name is: " + RobsAccount.Name );
```

- would produce a compilation error. It is your job as programmer to make sure that you always put a value into a variable before you try to get something out of it.

# Using Structure Types in Method Calls

A method can have parameters of structure type:

```
public void PrintAccount ( Account a )
{
    Console.WriteLine ( "Name: " + a.Name );
    Console.WriteLine ( "Address: " + a.Address );
    Console.WriteLine ( "Balance: " + a.Balance );
}
```

This method provides a quick way of printing out the contents of an account variable:

```
PrintAccount (RobsAccount);
```