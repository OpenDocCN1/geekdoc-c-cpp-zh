```
```csharp
Console.Write("Please enter a number: ");
int num = int.Parse(Console.ReadLine());
int sum = 0;
for (int i = 1; i <= num; i++)
{
    //---sum up all odd numbers---
    if (i % 2 == 1)
    {
        sum += i;
#if DEBUG
        Console.WriteLine("i={0}, sum={1}", i, sum);
#endif
    }
    Console.WriteLine(
        "Sum of all odd numbers from 1 to {0} is {1}",
        num, sum);
    Console.ReadLine();
}
```
```

*DEBUG is a common symbol that developers use to indicate debugging statements, which is why most books use it in examples. However, you can define any symbol you want using the #define preprocessor directive.*

Before compilation, the preprocessor will evaluate the #if preprocessor directive to see if the DEBUG symbol has been defined. If it has, the statement(s) wrapped within the #if and #endif preprocessor directives will be included for compilation. If the DEBUG symbol has not been defined, the statement — the statement(s) wrapped within the #if and #endif preprocessor — will be omitted from the compilation.

To test out the TestDefine program, follow these steps:

+   1. Launch the Visual Studio 2008 command prompt (Start ⇨ Programs ⇨ Microsoft Visual Studio 2008 ⇨ Visual Studio Tools ⇨ Visual Studio 2008 Command Prompt).
+   2. Change to the path containing the program (C:\TestDefine).
+   3. Compile the application by issuing the command:
+      ```
+      csc Program.cs.
+      ```
+   4. Run the program by issuing the command:
+      ```
+      Program.exe.
+      ```