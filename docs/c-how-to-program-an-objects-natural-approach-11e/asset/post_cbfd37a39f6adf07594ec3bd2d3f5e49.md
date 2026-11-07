
```cpp
// Fig. 16.13: deitel.math-roots.ixx
// Module interface partition unit deitel.math:roots.
export module deitel.math:roots;

import <cmath>;

export namespace deitel::math {
    double squareRoot(double x) { return std::sqrt(x); }
    double cubeRoot(double x) { return std::cbrt(x); }
}
```

**Fig. 16.13** — Module interface partition unit `deitel.math:roots`.

## deitel.math Primary Module Interface Unit

Figure 16.14 defines the `deitel.math.ixx` primary module interface unit. Every module must have one primary module interface unit with an `export module` declaration that does not include a partition name (line 4). Lines 8 and 9 **export import** the module interface partition units:

- First, each **import** imports the module interface partition unit that follows the colon (`:`)—in this case, `powers` or `roots`.
- Next, the **export** keyword before each **import** indicates that the specified module interface partition unit’s exported members should be part of the `deitel.math` module’s primary module interface.

The users of your module cannot see its partitions.[62]

```cpp
// Fig. 16.14: deitel.math.ixx
// Primary module interface unit deitel.math exports declarations from
// the module interface partitions :powers and :roots.
export module deitel.math; // declares the primary module interface unit

// import and re-export the declarations in the module
// interface partitions :powers and :roots
export import :powers;
export import :roots;
```

**Fig. 16.14** — Primary module interface unit that exports declarations from the module interface partitions `:powers` and `:roots`.

You also can **export import** primary module interface units. Let’s assume we have modules named A and B. If module A’s primary module interface unit contains

```cpp
export import B;
```

then a translation unit that imports A also imports B and can use its exported declarations.

If you **export import** a header unit, its preprocessor macros are available for use only in the **importing translation unit**—they are not re-exported. So, to use a macro from a header unit in a specific translation unit, you must explicitly **import** the header.

62. “C++ Standard: 10 Modules—10.1 Module Units and Purviews.” Accessed April 18, 2023. https://timsong-cpp.github.io/cppwp/n4861/module.unit.

## Using the deitel.math Module

Figure 16.15 imports the deitel.math module (line 4) and lines 9–12 use its exported functions to demonstrate that this primary module interface contains all the functions exported by the powers and roots module interface partitions.

```cpp
// fig16_15.cpp
// Using the deitel.math module's functions.
import <iostream>;
import deitel.math; // import the deitel.math module

using namespace deitel::math;

int main() {
    std::cout << "square(6): " << square(6)
        << "\ncube(5): " << cube(5)
        << "\nsquareRoot(9): " << squareRoot(9)
        << "\ncubeRoot(1000): " << cubeRoot(1000) << '\n';
}
```

```text
square(6): 36
cube(5): 125
squareRoot(9): 3
cubeRoot(1000): 10
```

**Fig. 16.15** | Using the deitel.math module's functions.

### Compiling This Example in Visual C++

Add the files deitel.math-powers.ixx deitel.math-roots.ixx and deitel.math.ixx to your Visual C++ project using the steps from Section 16.6.1, then add the file fig16_15.cpp to the project's Source Files folder. Run your project to compile the module and the main application.

### Compiling This Example in g++

When building a module with partitions, you must build the partitions before the primary module interface unit. In g++, use the commands introduced in Section 16.6.6 to compile the standard library header `<cmath>` and `<iostream>` as header units. Next, compile each module interface partition unit:

```bash
g++ -fmodules-ts -c -x c++ deitel.math-powers.ixx
g++ -fmodules-ts -c -x c++ deitel.math-roots.ixx
```

Then, compile the primary module interface unit:

```bash
g++ -fmodules-ts -c -x c++ deitel.math.ixx
```

Finally, compile the main application and link it with deitel.math-powers.o, deitel.math-roots.o and deitel.math.o:

```bash
g++ -fmodules-ts fig16_15.cpp deitel.math-powers.o deitel.math-roots.o deitel.math.o -o fig16_15
```

### Compiling This Example in clang++

When building a module with partitions, you must build the partitions before the primary module interface unit. At the time of this writing, clang++ would not compile the `<cmath>` header into a header unit. So before compiling this example in clang++, change the import statement in line 5 of Fig. 16.13 to

```cpp
#include <cmath>
```

In clang++, use the commands introduced in Section 16.6.6 to compile the standard library header `<iostream>` as a header unit. Next, compile each module interface partition unit into a precompiled module (.pcm) file:

```bash
clang++ -std=c++20 -x c++-module deitel.math-powers.ixx --precompile -o deitel.math-powers.pcm
clang++ -std=c++20 -x c++-module deitel.math-roots.ixx --precompile -o deitel.math-roots.pcm
```

Then, compile the primary module interface unit into a precompiled module (.pcm) file:

```bash
clang++ -std=c++20 -x c++-module deitel.math.ixx -fprebuilt-module-path=. --precompile -o deitel.math.pcm
```

Finally, compile the main application and link it with deitel.math-powers.pcm, deitel.math-roots.pcm and deitel.math.pcm:

```bash
clang++ -std=c++20 -fmodule-file=iostream.pcm fig16_15.cpp -fprebuilt-module-path=. -fmodule-file=deitel.math-powers.pcm deitel.math-roots.pcm -o fig16_15
```

## 16.9.2 Module Implementation Partition Units

You also can divide module implementations into module implementation partition units to define a module’s implementation details across multiple source-code files.[63] Again, this can help you organize a module’s components into smaller, more manageable translation units and possibly reduce compilation times in large systems. In a module implementation partition, the module declaration must not contain the export keyword:

```cpp
module ModuleName:PartitionName;
```

Module implementation partition units do not implicitly import the primary module interface.[64] At the time of this writing, none of our preferred compilers support module implementation partitions, so we do not show them here.

## 16.9.3 Example: “Submodules” vs. Partitions

Some libraries, like the C++ standard library, are quite large. Programmers using such a library might want the flexibility to import only portions of it. A library vendor can divide a library into logical “submodules,” each with its own primary module interface unit. These can be imported independently. In addition, library vendors can provide a primary module interface unit that aggregates the “submodules” by importing and re-exporting

63. Richard Smith, “Merging Modules—Section 2.2 Module Partitions,” February 22, 2019. Accessed April 18, 2023. https://wg21.link/p1103r3.
64. C++ Standard, “10 Modules—10.1 Module Units and Purviews.”

### Compiling This Example in g++

Use the commands introduced in Section 16.6.6 to compile the standard library header `<iostream>` as a header unit. Next, compile the primary module interface unit:

```bash
g++ -fmodules-ts -c -x c++ deitel.math.powers.ixx
```

Then, compile the main application and link it with `deitel.math.powers.o`:

```bash
g++ -fmodules-ts fig16_17.cpp deitel.math.powers.o -o fig16_17
```

### Compiling This Example in clang++

Use the commands introduced in Section 16.6.6 to compile the standard library header `<iostream>` as a header unit. Next, compile the primary module interface unit into a pre-compiled module (`.pcm` file):

```bash
clang++ -std=c++20 -x c++-module deitel.math.powers.ixx --precompile -o deitel.math.powers.pcm
```

Finally, compile the main application and link it with `deitel.math.powers.pcm`:

```bash
clang++ -std=c++20 -fmodule-file=iostream.pcm fig16_17.cpp -fprebuilt-module-path=. deitel.math.powers.pcm -o fig16_17
```

## deitel.math.roots Primary Module Interface Unit

Next, let’s rename the file `deitel.math-roots.ixx` as `deitel.math.roots.ixx` and make `deitel.math.roots` a primary module interface unit (Fig. 16.18). Rather than declaring a module interface partition, as in Fig. 16.13

```cpp
export module deitel.math:roots;
```

line 3 of Fig. 16.18 declares a primary module interface unit with a dot-separated name:

```cpp
export module deitel.math.roots;
```

We can now independently import `deitel.math.roots` and use its functions (Fig. 16.19).

```cpp
// Fig. 16.18: deitel.math.roots.ixx
// Primary module interface unit deitel.math.roots.
export module deitel.math.roots;

import <cmath>;

export namespace deitel::math {
    double squareRoot(double x) { return std::sqrt(x); }
    double cubeRoot(double x) { return std::cbrt(x); }
}
```

**Fig. 16.18**  |  Primary module interface unit `deitel.math.roots`.

```cpp
// fig16_19.cpp
// Using the deitel.math.roots module's functions.
import <iostream>;
import deitel.math.roots; // import the deitel.math.roots module
```

**Fig. 16.19**  |  Using the `deitel.math.roots` module's functions. (Part 1 of 2.)
