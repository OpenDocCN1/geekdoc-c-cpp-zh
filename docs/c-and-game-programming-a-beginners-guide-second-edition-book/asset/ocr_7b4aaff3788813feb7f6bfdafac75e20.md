```
```csharp
"<V> to view account");
input = char.Parse(Console.ReadLine());
if(Char.ToUpper(input) == 'C') {
    account.CreateFile(ref account);
} else if (Char.ToUpper (input) == 'V') {
    account.ReadFile(ref account);
} else {
    break;
}

account.ViewFile(account);
account.SaveFile(account, 0, 0);
}
}
}
```
```

# The Internal Access Modifier

An internal access modifier is a type member used to access class components. The advantage of the internal modifier is that it allows for limited access from within a single assembly. A key disadvantage is that it is only accessible from within that assembly. In addition to the basic internal modifier, we can also use the keyword internal in combination with protected to create a internal protected modifier (see Example 5.15).

# Example 5.15. Internals.

```
```csharp
using System;
using System.IO;

namespace Chapter5 {
    internal class BankAccount {
        internal protected string first_name;
        internal protected string last_name;
        internal protected long account_number;
        internal protected decimal Checking;
        internal protected decimal Savings;
        internal protected short pin_number;

        internal void ReadFiles (ref BankAccount acc) {
            StreamReader ReadFile = new StreamReader(@"C:\MyFile.txt");
```
```