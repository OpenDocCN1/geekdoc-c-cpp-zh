LOG: Attempting download of new URL
file:///C:/Temp/CalculatorUI/CalculatorUI/bin/Debug/Calculator/Calculator.EXE.
LOG: All probing URLs attempted and failed.

![](bbox=[0.1, 0.25, 0.8, 0.62])

FIGURE 25.29 An assembly load failure log dump.

A few things can be noticed here. First, configuration files can influence the loading process. For more information about this, refer to MSDN documentation (because this is not used that often). Second, notice the search order for “download attempts” to locate assemblies. The CLR can load assemblies using a variety of protocols (including regular file lookup) and does so in a sequence of paths based on the calling assembly’s location and the requested assembly’s name. Also notice how the extension is not part of the assembly name but is appended for searches (where .dll takes precedence over .exe). The whole process of locating an assembly based on a name is called probing.

# DIFFERENCE WITH JAVA

Readers familiar with Java will observe quite a few differences. In .NET, loading of a type is based on finding its containing assembly, not on finding a .class file based on a package name. Hence, there’s no such thing as a CLASSPATH either.

# Native Image Generation (NGEN)

As you know by now, the CLR uses a JIT compilation strategy to turn IL code into instructions executable on the CPU architecture of the machine where the application is running. This has several benefits, including code portability across different architectures. It also simplifies the act of code generation by various front-end language compilers