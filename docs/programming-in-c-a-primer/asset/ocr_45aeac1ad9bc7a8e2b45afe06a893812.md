```
TestClass test = new TestClass(); // creating test object
test.fun(); // calling fun () function
}
```

This program has two class declarations, one for the TestClass and another for the Main method. TestClass contains only one method to print a string "C# is modern". The Main method in SampleSeven class creates an object of TestClass and uses it to invoke the method fun () contained in TestClass as follows:

```
TestClass test = new TestClass();
test.fun();
```

The object test is used to invoke the method fun () of TestClass with the help of the dot operator. Execution of Program 3.8 will produce the following output:

C# is modern

If we want, we could include the TestClass declaration within the class SampleSeven. That would mean creation of 'nested' classes. Classes, methods and creation of objects are discussed in detail in later chapters.

# 3.10 PROVIDING INTERACTIVE INPUT

So far we have seen two approaches for giving values to string objects:

+   - Using an assignment statement
+   - Through command line arguments

It is also possible to give values to string variables interactively through the keyboard at the time of execution. Program 3.9 shows how to get specific information from the user and print a message using that information.

# Program 3.9 INTERACTIVE CONSOLE INPUT

```
using System;
class SampleEight
{
    public static void Main()
    {
        Console.Write("Enter your name: ");
        string name = Console.ReadLine();
        Console.WriteLine("Hello " + name);
    }
}
```

The method

```
Console.Write("Enter your name: ");
```

outputs the message "Enter your name:" and the method

```
Console.ReadLine();
```

causes the execution to wait for the user to enter his name. The moment the user types his name and presses the 'Enter' key, the input is read into the string variable name. The second output line (Write Line