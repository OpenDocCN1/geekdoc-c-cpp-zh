```
Dotnet/HelloWorld3.cs):
class Program
{
    static void Main()
    {
        System.Console.WriteLine("Hello, World!");
    }
}
```

After writing the source code, you need to compile the code to run it.

# Compiling with .NET 4.6

You can compile this program by simply running the C# command-line compiler (`csc.exe`) against the source file, like this:

```
csc HelloWorld.cs
```

If you want to compile code from the command line using the `csc` command, you should be aware that the .NET command-line tools, including `csc`, are available only if certain environment variables have been set up. Depending on how you installed .NET (and Visual Studio), this may or may not be the case on your machine.

> NOTE If you do not have the environment variables set up, you have three options: The first is to add the path to the call of the csc executable. It is located at %Program Files%\MsBuild\14.0\Bin\csc.exe With the dotnet tools installed, you can also find the csc at %ProgramFiles%\dotnet\bin\csc.exe. The second option is to run the batch file %Microsoft Visual Studio 2015%\Common7\Tools\vsvars32.bat from the command prompt before running csc, where %Microsoft Visual Studio 2015% is the folder to which Visual Studio 2015 has been installed. The third, and easiest, way is to use the Visual Studio 2015 command prompt instead of the Windows command prompt. To find the Visual Studio 2015 command prompt from the Start menu, select Programs ⇨ Microsoft Visual Studio 2015 ⇨ Visual Studio Tools. The Visual Studio 2015 command prompt is simply a command prompt window that automatically runs vsvars32.bat when it opens.

Compiling the code produces an executable file named HelloWorld.exe, which you can run from the command line. You can also run it from Windows Explorer as you would run any other executable. Give it a try:

```
> csc HelloWorld.cs
Microsoft (R) Visual C# Compiler version 1.1.0.51109
Copyright (C) Microsoft Corporation. All rights reserved.
> HelloWorld
Hello World!
```