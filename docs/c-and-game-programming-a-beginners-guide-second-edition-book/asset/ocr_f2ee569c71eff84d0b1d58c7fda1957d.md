```
```csharp
Console.WriteLine("Name: {0} {1}",
    acc.First_name, acc.Last_name);
Console.WriteLine("Savings Balance: {0}",
    acc.Savings);
Console.WriteLine("Checking Balance: {0}",
    acc.Checking);
}
}
}

class Class1 {
    static void Main() {
        BankAccount account = new BankAccount();

        char input;
        while (true) {
            Console.WriteLine("Enter <C> to create new file or " +
                "<V> to view account");
            input = Char.Parse(Console.ReadLine());

            if(Char.ToUpper(input) == 'C') {
                account.CreateFiles(ref account);
            } else if (Char.ToUpper(input) == 'V') {
                account.ReadFiles(ref account);
            } else
                break;

            account.ViewFiles(account);
            account.SaveFiles(account, 0, 0);
        }
    }
}
```
```

# Arrays as Member Fields

Another key component to implement when dealing with a list of classes is the *array reference type*. This powerful, yet somewhat supplemental, string type is still a very useful data block, especially when dealing with the integral data types. Here, we'll want to examine the proper forms when working with arrays both as part of the class and as a component of its methods. Note also that while the array in our example was declared as a private value, its length is still left as a public reference, and thus will not cause an error (see Example 5.16).