```
char input;
while (true) {
    Console.WriteLine("Enter <C> to create new file or " +
                      "<V> to view account");
    input = char.Parse(Console.ReadLine());

    if (Char.ToUpper(input) == 'C') {
        account.CreateFile();
    } else if (Char.ToUpper(input) == 'V') {
        account.ViewFile();
    } else {
        break;
    }

    account.ViewFile();
}
}
}
}

```

# Destructors

In addition to constructors, we can also use *destructors* to return the allocated portions of an object’s memory back to the heap. This destruction, or *deallocation*, of system resources is an extremely important systems saving technique, especially when dealing with thousands of class objects that continue to exist even after they are no longer referenced. Again, while Managed C++ and C# do handle these instances automatically, it is still important to understand the concept of creating a destructor. Destructors are also automatically referenced at the termination of a set of coding, but the exact internal structure will depend on the constructor’s applications and thus is user-defined. The correct way to define a destructor is to reproduce the class’ definition (as done for the constructor), but with the addition of the tilde operator (~). Destructors contain no arguments and do not require a data type. Classes should be written to include only one destructor. Destructors do not return values, nor can they be overloaded (see Example 5.27).

# Example 5.27. Overloaded constructors and a destructor.

```
using System;
using System.IO;
```