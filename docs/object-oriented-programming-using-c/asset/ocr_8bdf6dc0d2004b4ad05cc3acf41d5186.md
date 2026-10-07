# Object Oriented Programming C#

# Generic Collections and how to Serialize them

```
static void Main(string[] args)
{
    Bank b = new Bank();
    Account a;
    int an = // account number;

    a = new Account("Bert", "06/12/1963");
    b.AddAccount(1, a);
    a = new Account("Alice", "14/08/1990");
    b.AddAccount(2, a);
    a = new Account("Claire", "1/1/2000");
    b.AddAccount(3, a);

    Console.WriteLine("Stored data:");
    foreach (KeyValuePair<int, Account> kvp in b.Accounts)
    {
        int an = kvp.Key;
        Account a = kvp.Value;
        Console.WriteLine("Account number: " + an + "\naccount details: " + a.ToString());
    }

    FileStream outputFile = new FileStream("AccountData", FileMode.Create, FileAccess.Write);
    BinaryFormatter bformatter = new BinaryFormatter();
    bformatter.Serialize(outputFile, b);
    outputFile.Close();
    outputFile.Dispose();

    Bank b2 = new Bank();
    FileStream inFile = new FileStream("AccountData", FileMode.Open, FileAccess.Read);
    b2 = (Bank)bformatter.Deserialize(inFile);
    inFile.Close();
    inFile.Dispose();

    Console.WriteLine("nRetrieved data:");
    foreach (KeyValuePair<int, Account> kvp in b2.Accounts)
    {
        int an = kvp.Key;
        Account a = kvp.Value;
        Console.WriteLine("Account number: " + an + "\naccount details: " + a.ToString());
    }

    Console.ReadLine();
}
```

The code above performs the following steps -

+   - Firstly several bank accounts are created, added to the collection and the collection is displayed.
- Next an output file is created
- A binary formatter is created as this is used by the serialization process.

Download free ebooks at bookboom.com