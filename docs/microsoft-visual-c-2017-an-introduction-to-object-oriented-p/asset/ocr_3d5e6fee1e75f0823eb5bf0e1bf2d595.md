# Alternate Ways to Write a Main() Method Header

Throughout this book, you have written Main() methods with the following header:

```
static void Main()
```

Using the return type void and listing nothing between the parentheses that follows is just one way to write a Main() method header in a program. However, it is the first way listed in the C# documentation, and it is the convention used in this book. This section describes alternatives because you might see different Main() method headers in other books or in programs written by others.

# Writing a Main() Method with a Parameter

An alternate way to write a Main() method header is as follows:

```
static void Main(string[] args)
```

The phrase string[] args is a parameter to the Main() method. The variable args represents an array of strings that you can pass to Main(). You can use any identifier, args is conventional. In particular, Java programmers might prefer the C# version of Main() that includes the string[] args parameters because their convention is to write main methods with the same parameter.

Use this format for the Main() method header if you need to access command-line arguments passed to your application. For example, the program in Figure 7-22 displays an args array that is a parameter to its Main() method. shows how a program is executed from the command line arguments to Main().

```
using static System.Console;
class DisplayArgs
{
    static void Main(string[] args)
    {
        for (int x = 0; x < args.Length; ++x)
            WriteLine("Argument {0} is {1}", x, args[x]);
    }
}
```

**Figure 7-21** A Main() method with a string args parameter

```
C:\CSharp>DisplayArgs Alpha Beta Gamma Delta
Argument 0 is Alpha
Argument 1 is Beta
Argument 2 is Gamma
Argument 3 is Delta
C:\CSharp>
```

**Figure 7-22** Executing the DisplayArgs program with arguments