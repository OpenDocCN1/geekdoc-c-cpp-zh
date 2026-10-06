# Compiling, Loading, and Executing C# Programs

Example 1 Complete Program in File Example001.cs
Almost all programs need the using System directive (section 29.1) but it is omitted in later examples.

```
using System;
public class Sum {
    static void Main(String[] args) {
        int sum = 0;
        for (int i=0; i<args.Length; i++)
            sum += int.Parse(args[i]);
        Console.WriteLine("The sum is " + sum);
    }
}
```

Example 2 Compiling and Running a Program from the Command Line
This example shows how to compile the file Example001.cs from the command line under Microsoft .Net (left) or Linux or Windows using the Mono system (right). In both cases the program outputs the text: The sum is 29.

+   csc Example001.cs mcs Example001.cs
Example001 7 9 13 mono Example001.exe 7 9 13

Example 3 Compiling an Executable with a Reference to a Library
First compile file Mod.cs into a module Mod.netmodule and compile Lib.cs into a library Lib.dll.
Then compile the file Prog.cs and create an executable program in Prog.exe that has an external module Mod and refers to the library Lib. Finally, run the executable.exe:

```
csc /target:module Mod.cs
csc /target:library.dll
csc /addmodule:Mod.netmodule /reference:Lib.dll Prog.cs

```

The resulting assembly consists of two files: the main file Prog.exe, and file Mod.exe which contains the external module. The assembly has a manifest with version number, other metadata, and references to two other assemblies: the Lib, and mscorlib which is included by default.

![](bbox=[0.118, 0.733, 0.839, 0.876])