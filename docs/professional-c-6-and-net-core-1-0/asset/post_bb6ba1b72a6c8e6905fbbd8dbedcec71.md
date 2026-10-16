
advanced XML variant. With MSBuild projects, you can use the MSBuild command with the project file as input, and all the sources will be compiled. Using build files is very helpful on a separate build server on which all developers check their code in, and overnight the build process is done. Chapter 1 mentions the .NET Core command line (CLI) tools, the command line to build with the .NET Core environment.

## Debugging and Release Builds

The idea of having separate builds is very familiar to C++ developers, and to a lesser degree to those with a Visual Basic background. The point here is that when you are debugging, you typically want your executable to behave differently from when you are ready to ship the software. When you are ready to ship your software, you want the executable to be as small and fast as possible. Unfortunately, these two requirements are not compatible with your needs when you are debugging code, as explained in the following sections.

### Optimization

High performance is achieved partly by the compiler’s many optimizations of the code. This means that the compiler actively looks at your source code as it is compiling to identify places where it can modify the precise details of what you are doing in a way that does not change the overall effect but makes things more efficient. For example, suppose the compiler encountered the following source code:

```
double InchesToCm(double ins) => ins * 2.54;

// later on in the code
Y = InchesToCm(X);
```

It might replace it with this:

```
Y = X * 2.54;
```

Similarly, it might replace

```
{
    string message ="Hi";
    Console.WriteLine(message);
}
```

with this:

```
Console.WriteLine("Hi");
```

By doing so, the compiler bypasses having to declare any unnecessary object reference in the process.

It is not possible to exactly pin down what optimizations the C# compiler does—nor whether the two previous examples would actually occur in any particular situation—because those kinds of details are not documented. (Chances are good that for managed languages such as C#, the previous optimizations would occur at JIT compilation time, not when the C# compiler compiles source code to assembly.) Obviously, for proprietary reasons, companies that write compilers are usually quite reluctant to provide many details about the tricks that their compilers use. Note that optimizations do not affect your source code—they affect only the contents of the executable code. However, the previous examples should give you a good idea of what to expect from optimizations.

The problem is that although optimizations like the examples just shown help a great deal in making your code run faster, they are detrimental for debugging. In the first example, suppose that you want to set a breakpoint inside the InchesToCm method to see what is going on in there. How can you possibly do that if the executable code does not actually have an InchesToCm method because the compiler has removed it? Moreover, how can you set a watch on the Message variable when that does not exist in the compiled code either?

### Debugger Symbols

During debugging, you often have to look at the values of variables, and you specify them by their source code names. The trouble is that executable code generally does not contain those names—the compiler replaces the names with memory addresses. .NET has modified this situation somewhat to the extent that certain items in assemblies are stored with their names, but this is true of only a small minority of items—such as public classes and methods—and those names will still be removed when the assembly is JIT-compiled. Asking the debugger to tell you the value in the variable called HeightInInches is not going to get you very far if, when the debugger examines the executable code, it sees only addresses and no reference to the name HeightInInches anywhere.

Therefore, to debug properly, you need to make extra debugging information available in the executable. This information includes, among other things, names of variables and line information that enables the debugger to match up which executable machine assembly language instructions correspond to your original source code instructions. You will not, however, want that information in a release build, both for proprietary reasons (debugging information makes it a lot easier for other people to disassemble your code) and because it increases the size of the executable.

### Extra Source Code Debugging Commands

A related issue is that quite often while you are debugging there will be extra lines in your code to display crucial debugging-related information. Obviously, you want the relevant commands removed entirely from the executable before you ship the software. You could do this manually, but wouldn’t it be so much easier if you could simply mark those statements in some way so that the compiler ignores them when it is compiling your code to be shipped? You’ve already seen in the first part of the book how this can be done in C# by defining a suitable processor symbol, and possibly using this in conjunction with the Conditional attribute, giving you what is known as conditional compilation.

What all these factors add up to is that you need to compile almost all commercial software in a slightly different way when debugging than in the final product that is shipped. Visual Studio can handle this because, as you have already seen, it stores details about all the options it is supposed to pass to the compiler when it has your code compiled. All that Visual Studio has to do to support different types of builds is store more than one set of such details. These different sets of build information are referred to as configurations. When you create a project, Visual Studio automatically gives you two configurations—Debug and Release:

- **Debug**—This configuration commonly specifies that no optimizations are to take place, extra debugging information is to be present in the executable, and the compiler is to assume that the debug preprocessor symbol `DEBUG` is present unless it is explicitly `#undef`'ed in the source code.
- **Release**—This configuration specifies that the compiler should optimize the compilation, that there should be no extra debugging information in the executable, and that the compiler should not assume that any particular preprocessor symbol is present.

You can define your own configurations as well. You might want to do this, for example, to set up professional-level builds and enterprise-level builds so that you can ship two versions of the software. In the past, because of issues related to Unicode character encodings being supported on Windows NT but not on Windows 95, it was common for C++ projects to feature a Unicode configuration and an MBCS (multi-byte character set) configuration.

### Selecting a Configuration

At this point you might be wondering how Visual Studio, given that it stores details about more than one configuration, determines which one to use when arranging for a project to be built. The answer is that there is always an active configuration, which is the configuration that is used when you ask Visual Studio to build a project. (Note that configurations are set for each project, rather than each solution.)

By default, when you create a project, the Debug configuration is the active configuration. You can change which configuration is the active one by clicking the Build menu option and selecting the Configuration Manager item. It is also available through a drop-down menu in the main Visual Studio toolbar.

### Editing Configurations

In addition to choosing the active configuration, you can also examine and edit the configurations. To do this, select the relevant project in Solution Explorer and then select Properties from the Project menu. This brings up a sophisticated dialog. (Alternatively, you can access the same dialog by right-clicking the name of the project in Solution Explorer and then selecting Properties from the context menu.)

This dialog contains a tabbed view that enables you to select many different general areas to examine or edit. Space does not permit showing all of these areas, but this section outlines a couple of the most important ones.

Depending on whether the application is MSBuild or CLI, the options available are very different. First, look at the properties of the WPF application in Figure 17.34, which shows a tabbed view of the available properties. This screenshot shows the general Application settings.

![](img/3d365b72b289213a91ade7eb366b8f35_639_0.png)

**Figure 17.34**

Among the points to note are that you can select the name of the assembly as well as the type of assembly to be generated. The options here are Console Application, Windows Application, and Class Library. Of course, you can change the assembly type if you want. (Though arguably, you might wonder why you did not pick the correct project type when you asked Visual Studio to generate the project for you in the first place!)

Figure 17.35 shows the same configuration for a CLI-based application. You also can see Application settings, but the options are limited to the default namespace name and the selection of the runtime. With this screenshot, a specific version of RC 2 is selected.
