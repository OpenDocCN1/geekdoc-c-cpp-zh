```
```csharp
file.WriteLine((acc.checking + input2));
file.WriteLine(acc.first_name);
file.WriteLine(acc.last_name);
file.Close();
}

public void CreateFile(ref BankAccount acc) {
    Console.WriteLine("Enter Your New Pin Number: ");
    acc.pin_number = short.Parse(Console.ReadLine());
    
    Random rnd = new Random();
    acc.account_number = rnd.Next(1, 100);
    
    Console.WriteLine("\nYour New Account Number is: {0}",
        acc.account_number);
    Console.WriteLine("\nEnter your first name: ");
    acc.first_name = Console.ReadLine();
    Console.WriteLine("\nEnter your last name: ");
    acc.last_name = Console.ReadLine();
    Console.WriteLine("\nEnter Your Savings Balance: ");
    acc.savings = decimal.Parse(Console.ReadLine());
    Console.WriteLine("\nEnter Your Checking Balance: ");
    acc.checking = decimal.Parse(Console.ReadLine());
    
    SaveFile(acc, 0, 0);
}

public void ViewFile(BankAccount acc) {
    Console.WriteLine("Pin Number: {0}", acc.pin_number);
    Console.WriteLine("Account Number: {0}", acc.account_number);
    Console.WriteLine("Name: {0} {1}", acc.first_name,
        acc.last_name);
    Console.WriteLine("Savings Balance: {0}", acc.savings);
    Console.WriteLine("Checking Balance: {0}", acc.checking);
}

}

class Class1 {
    static void Main() {
        BankAccount account = new BankAccount();
        
        char input;
        while (true) {
            Console.WriteLine("Enter <C> to create new file or " +
                "<V> to view account");
```
```