Then, compile the main application and link it with `deitel.math.powers.o`, `deitel.math.roots.o` and `deitel.math.o`:

```
g++ -fmodules-ts fig16_21.cpp deitel.math.powers.o
    deitel.math.roots.o deitel.math.o -o fig16_21
```

# Compiling This Example in C++

For these steps, we assume you’re executing commands in the same folder where you compiled `deitel.math.powers.ixx` and `deitel.math.roots.ixx`. Compile the primary module interface unit into a precompiled module (`.pcm`) file:

```
clang++ -std=c++20 -x c++-module deitel.math.ixx
    -fprebuilt-module-path=. --precompile -o deitel.math.pcm
```

Then, compile the main application and link it with `deitel.math.powers.pcm`, `deitel.math.roots.pcm` and `deitel.math.pcm`:

```
clang++ -std=c++20 -fmodule-file=iostream.pcm fig16_21.cpp
    -fprebuilt-module-path=. deitel.math.pcm deitel.math.powers.pcm
    deitel.math.roots.pcm -o fig16_21
```

# 16.10 Additional Modules Examples

The next several subsections demonstrate additional modules concepts:

+   - importing the modularized Microsoft and Clang++ standard libraries,
+   - some module restrictions and the compilation errors you’ll receive if you violate those restrictions, and
+   - the difference between module members that other translation units can use by name vs. module members that other translation units can use indirectly.

# 16.10.1 Example: Importing the C++ Standard Library as Modules

C++23 requires a modularized standard library containing two modules named `std` and `std.compat`.⁶⁵ Most programs will import the standard library as follows:

```
import std;
```

At the time of this writing, only C++ versions 15 and 16 support this import with their early access modularized C++ standard library.

Microsoft Visual C++ has an experimental modularized C++ standard library containing several modules. You can import the following modules into your Visual C++ projects and “potentially speed up compilation times depending on the size of your project”.⁶⁶

+   - `std.core`—This module contains most of the standard library except for the following items.
+   - `std.filesystem`—Module containing the `<filesystem>` header’s capabilities.
+   - `std.memory`—Module containing the `<memory>` header’s capabilities.

65. Stephan T. Lavavej, Gabriel Dos Reis, Bjarne Stroustrup and Jonathan Wakely, “Standard Library Modules std and std.compat,” October 13, 2021. Accessed April 18, 2023. https://wg21.link/p2465.

66. Colin Robertson and Nick Schonnig, “Overview of Modules in C++,” December 13, 2019. Accessed April 18, 2023. https://docs.microsoft.com/en-us/cpp/cpp/modules-cpp?view=msvc-160.