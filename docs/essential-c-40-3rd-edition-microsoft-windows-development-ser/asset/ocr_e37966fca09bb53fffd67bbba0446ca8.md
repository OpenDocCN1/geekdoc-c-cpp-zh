```
public static void Main()
{
    checked
    {
        // int.MaxValue equals 2147483647
        int n = int.MaxValue;
        n = n + 1;
        System.Console.WriteLine(n);
    }
}
}
```

If the calculation involves only constants, then the calculation will be checked by default. The results of Listing 10.7 appear in Output 10.2.

# OUTPUT 10.2:

```
Unhandled Exception: System.OverflowException: Arithmetic operation resulted in an overflow. at Program.Main() in ..\Program.cs:line 12
```

In addition, depending on the version of Windows and whether a debugger is installed, a dialog may appear prompting the user to send an error message to Microsoft, check for a solution, or debug the application. Also, the location information (Program.cs:line X) will appear only in debug compilations—compilations using the /Debug option of the Microsoft csc.exe compiler.

The result is that an exception is thrown if, within the checked block, an overflow assignment occurs at runtime.

The C# compiler provides a command-line option for changing the default checked behavior from unchecked to checked. C# also supports an unchecked block that truncates the data instead of throwing an exception for assignments within the block (see Listing 10.8).

# LISTING 10.8: An Unchecked Block Example

```
using System;

public class Program
{
    public static void Main()
    {
        unchecked
        {
```