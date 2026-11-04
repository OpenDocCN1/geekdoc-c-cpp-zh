those values are made specific to that instance's reference. Constructors, like standard member functions, are declared from within those classes, but constructors do not require a base data type. Constructors are defined using the same definition as their declaring class, while their actual functions are expressed as a combination of both definitions and a connecting binary scope resolution operator. Since constructors do not declare a data type, they are also incapable of returning values (see Example 5.21).

> Each declared instance is allocated a portion of system memory (commonly referred to as the heap). In native C++ it is also important to define the restoration of that memory (normally referenced by that classes destructor— see this chapter's section on destructors).

![](bbox=[0.78, 0.3, 0.92, 0.42])

# Example 5.21. Constructors.

```
```
using System;
using System.IO;

namespace Chapter5 {
    class BankAccount {
        public decimal InterestRate;
        public decimal LoanRate;

        // Default Constructor
        public BankAccount() {
            InterestRate = .03M; LoanRate = .13M;
        }
    }

    class Class1 {
        static void Main() {
            BankAccount account = new BankAccount();
        }
    }
}
```
```

1 While destructors are an important part of native C++, their importance is minimized in C#, where the process of destructing an object has become the primary concern of the compiler, normally occurring when the object is no longer referenced.