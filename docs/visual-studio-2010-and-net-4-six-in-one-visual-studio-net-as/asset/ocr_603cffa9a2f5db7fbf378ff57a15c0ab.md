# YOUR FIRST F# PROJECT

Now that you have seen some of F# and a bit of functional programming, it is time you created your first F# project. You can do this pretty much same way you create any project, by going to File > New in Visual Studio. Figure 25-1 shows a typical F# development environment with F# Interactive.

![](bbox=[0.115, 0.246, 0.735, 0.673])

FIGURE 25-1: Developing F# projects

Once Visual Studio has created your project, note that a reference to FSharp.Core.dll has been added. For NET 4.0, this file resides under the following:

```
C:\Program Files\Reference Assemblies\Microsoft\F#1.0\Runtime\v4.0\FSharp.Core.dll
```

FSharp.Core.dll contains all the F# cores, modules, types, and functions. Many of the miscellaneous functionality (including the primitives required to work with the F#-bundled lexer and parser generators) are placed in the F# PowerPack, which, as of this writing, is available as a separate download from MSDN Downloads and Codeplex.