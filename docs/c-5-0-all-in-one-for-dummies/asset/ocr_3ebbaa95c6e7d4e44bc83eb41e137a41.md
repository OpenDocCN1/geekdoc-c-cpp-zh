In this case, the only calling method potentially affected was Main(), but the effects could have extended to dozens of methods that accessed bank accounts, and those methods could have been spread over hundreds of assemblies. None of those methods would have had to change, because the fix was within the confines of the BankAccount class, whose public interface (its public methods) didn't outwardly change. This solution wouldn't have been possible if the internal members of the class had been exposed to external methods.

![](bbox=[0.124, 0.257, 0.199, 0.314])

Internal changes to a class still require some retesting of other code, even though you didn't have to modify that code.

# # Defining Class Properties

The GetX() and SetX() methods demonstrated in the BankAccount programs in the previous section are access methods, or simply accessors. Although they signify good programming habits in theory, access methods can become clumsy in practice. For example, the following code line is necessary to increment _accountNumber by 1:

```
```
SetAccountNumber(GetAccountNumber() + 1);
```
```

C# defines a construct known as a property, which makes using access methods much easier than making them methods. The following code snippet defines a read-write property, AccountNumber (it's both a getter and a setter):

```
```csharp
public int AccountNumber          // No parentheses here.
{
    get { return _accountNumber; }  // The "read" part. Curly braces and semicolon.
    set { _accountNumber = value; } // The "write" part. 'value' is a keyword.
}
```
```

The get section is called whenever the property is read, and the set section is invoked on the write. The following Balance property is read-only because only the get section is defined (using a less compact notation):

```
```csharp
public double Balance
{
    get
    {
        return (double)_balance;
    }
}
```
```

In use, these properties appear as follows:

```
```csharp
BankAccount ba = new BankAccount();
// Set the account number property.
ba.AccountNumber = 1001;
// Get both properties.
Console.WriteLine("#{0} = {1:C}", ba.AccountNumber, ba.Balance);
```
```