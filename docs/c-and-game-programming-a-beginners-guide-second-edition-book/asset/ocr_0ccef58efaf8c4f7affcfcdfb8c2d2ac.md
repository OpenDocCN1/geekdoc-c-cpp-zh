```
```csharp
Console.WriteLine("\nEnter Your Savings Balance: ");
this.savings = decimal.Parse(Console.ReadLine());
Console.WriteLine("\nEnter Your Checking Balance: ");
this.checking = decimal.Parse(Console.ReadLine());
this.SaveFile(0, 0);
}

private void SaveFile(short input1, short input2) {
    StreamWriter file = new StreamWriter(@"C:\MyFile.txt");
    file.WriteLine(this.pin_number);
    file.WriteLine(this.account_number);
    file.WriteLine(this.savings + input1);
    file.WriteLine(this.checking + input2);
    file.WriteLine(this.first_name);
    file.WriteLine(this.last_name);
    file.Close ();
}

public void ViewFile() {
    this.ReadFile();
    Console.WriteLine("Pin Number: {0}",
        this.pin_number);
    Console.WriteLine("Account Number: {0}",
        this.account_number);
    Console.WriteLine("Name: {0} {1}",
        this.first_name, this.last_name);
    Console.WriteLine("Savings Balance: {0}",
        this.savings);
    Console.WriteLine("Checking Balance: {0}",
        this.checking);
}

class Class1 {
    static void Main() {
        BankAccount account = new BankAccount();

        char input;
        while (true) {
            Console.WriteLine("Enter <C> to create new file or " +
                "<V> to view account");
            input = char.Parse(Console.ReadLine());

            if (Char.ToUpper(input) == 'C') {
                account.CreateFile();
```
```