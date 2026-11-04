> > **Note**
> >
> > As we examine this program, we'll find that the most important modification pertains to the dynamic instance. This change was necessary because classes are, in fact, referencing data types. You should also notice that the key methods, namely SaveFiles, CreateFiles, and ReadFiles did not need to be edited for use with this altered program. This adheres to the principles behind structured programming, wherein our functions are written as generic coding that can be reused by several applications; this is also the underlying principle of object-oriented program, as we will see in the next section.

# **Example 5.12. Storing and retrieving data with classes.**

```
```csharp
using System;
using System.IO;

namespace Chapter5 {
    class BankAccount {
        public string first_name;
        public string last_name;
        public long account_number;
        public decimal checking;
        public decimal savings;
        public short pin_number;
    }

    class Class1 {
        static void Main() {
            BankAccount account1 = new BankAccount();

            char input;

            while (true) {
                Console.WriteLine("Enter <C> to create new file or " +
                    "<V> to view account");
                input = char.Parse(Console.ReadLine());

                if (Char.ToUpper(input) == 'C') {
                    CreateFile(ref account1);
                } else if (Char.ToUpper(input) == 'V') {
                    ReadFile(ref account1);
                } else {
                    break;
                }
            }
```
```