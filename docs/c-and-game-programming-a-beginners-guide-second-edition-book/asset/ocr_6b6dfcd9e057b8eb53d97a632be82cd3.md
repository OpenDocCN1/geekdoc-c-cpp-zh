# *private and protected Member Functions*

Private and protected member functions (also known as predicate or utility functions) are specialized member functions used only for that class' internal reference. These functions can be used to read or display data, and are generally used to support the operations of that class' public member function. Private/protected member functions are not intended for use by outside references, but are generally written without any specific notation. To convert our previous program into one that uses private member functions, we simply need to revise our class' internal definition (see Examples 5.19 and 5.20).

# Example 5.19. Private member functions (methods).

```
```csharp
using System;
using System.IO;

namespace Chapters5 {
    class BankAccount {
        protected string first_name;
        protected string last_name;
        protected long account_number;
        protected decimal checking;
        protected decimal savings;
        protected short pin_number;

        private void ReadFile(ref BankAccount acc) {
            StreamReader file = new StreamReader(@"C:\MyFile.txt");
            acc.pin_number = short.Parse(file.ReadLine());
            acc.account_number = long.Parse(file.ReadLine());
            acc.savings = decimal.Parse(file.ReadLine());
            acc.checking = decimal.Parse(file.ReadLine());
            acc.first_name = file.ReadLine();
            acc.last_name = file.ReadLine();
            file.Close();
        }

        private void SaveFile(BankAccount acc, short input1,
            short input2) {
            StreamWriter file = new StreamWriter(@"C:\MyFile.txt");
            file.WriteLine(acc.pin_number);
            file.WriteLine(acc.account_number);
            file.WriteLine((acc.savings + input1));
        }
```
```