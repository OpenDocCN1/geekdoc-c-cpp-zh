Using the #define directive, a symbol can be defined for further use in conditional preprocessing directives like #if. Blocks of code surrounded by #if and #endif are conditionally included in the source code analyzed by the compiler, based on whether the conditioning symbol is defined:

```
using System;

class Program
{
    static void Main(string[] args)
    {
#if DEBUG
        Console.WriteLine("Some diagnostic output:");
        Console.WriteLine(DateTime.Now);
#endif

        foreach (string arg in args)
        {
            Console.WriteLine(arg);
        }
    }
}
```

The DEBUG symbol I'm using in the preceding fragment is automatically set when using the Debug mode in Visual Studio. In Release mode, it isn't. You can define your own symbols using #define in the source text or by specifying the symbols to be set to a compiler flag. The Project Properties dialog's Build tab provides easy access to this setting, illustrated in Figure 4.25.

![](bbox=[0.1, 0.83, 0.7, 0.9])

FIGURE 4.25 Defining symbols for conditional compilation.

# TIP

Conditional compilation is a very powerful beast to maintain different build flavors of the same source code. For example, large portions of the BCL are compiled for the “desktop CLR” as well as for Silverlight. To accommodate for the slight differences required here and there, conditional compilation is used.