# Program 3.4 USE OF ALIASES FOR CLASSES

```
using A = System.Console; //A is alias for System.Console
class SampleFour
{
    public static void Main()
    {
        D.WriteLine("Hello!");
    }
}
```

# 3.7 PASSING STRING OBJECTS TO WRITELINE METHOD

So far, we have seen only constant string output to the Console. We can store string values in string objects and use these objects as parameters to the WriteLine method. We can use string data type to create a string variable and assign a string constant to it as below:

```
string s = "abc";
```

The content of s may be printed out using the WriteLine method.
System.Console.WriteLine(s); //s is string object
Program 3.5 illustrates the use of a string object as a parameter to the output method WriteLine.

# Program 3.5 USING STRING OBJECTS IN OUTPUT

```
using System;
class SampleFive
{
    public static void Main()
    {
        string name = "C sharp"; // name is assigned a string
        Console.WriteLine(name);
    }
}
```

# 3.8 COMMAND LINE ARGUMENTS

There may be occasions when we may like our program to behave in a particular way depending on the input provided at the time of execution. This is achieved in C# by using what are known as command line arguments. Command line arguments are parameters supplied to the Main method at the time of invoking it for execution. Program 3.6 accepts a name from the command line and writes it to the console.

# Program 3.6 COMMAND LINE ARGUMENTS

```
/*
This program uses command line arguments as input
*/
using System;
```