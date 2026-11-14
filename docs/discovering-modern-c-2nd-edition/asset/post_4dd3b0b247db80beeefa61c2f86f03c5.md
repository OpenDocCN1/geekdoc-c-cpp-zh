

```
// File: multifile1.cpp
int main (int argc, char* argv[])
{
    fixPi();
    std::cout << "pi = " << pi << std::endl;
}
```

```
// File: multifile1.cpp
void fixPi() { pi = 3.14159265358979323846264338327950288419716939; }
```

It is better to define it once in a source file and declare it in the header using an extern:

![](img/5682e787fc967e93d7e33e8bac5f58a0_639_0.png)

```
// File: herberts/math_functions.hpp
extern double pi;
```

```
// File: herberts/math_functions.cpp
double pi = 3.14159265358979323846264338327950288419716939;
```

Finally, we will do the most reasonable: declaring \(\pi\) as a constant. Constants also have internal linkage^8 (unless previously declared `extern`) and can be safely defined in header files:

- 8. Advanced: They may be stored only once as weak symbols in the executable.

![](img/5682e787fc967e93d7e33e8bac5f58a0_639_1.png)

```
// File: herberts/math_functions.hpp
const double pi = 3.14159265358979323846264338327950288419716939;
```

Headers should not contain ordinary functions and variables.

Some scientific projects are still implemented in C today. If you are involved in a project, you probably miss all the advanced features you learned in this book. In Section A.10 we demonstrate therefore how C++ implementations can be used in C projects.

## 7.3 Modules

C++20. True modularity is possible in C++20 with Modules. In contrast to header files they aren't textually included in other files but remain entirely separate entities. For some C++ experts this is the most drastic change in the history of the language. As Bryce Adelstein pointed out [3], modules change the way:

- We write programs;
- Code is parsed;
- Programs are compiled;
- We organize projects; and
- Our projects are used.

Especially, the development of large projects will change dramatically in the long run. To this end, we will also need a new generation of supporting tools. This is unfortunately not the case yet by the time of writing: g++ doesn't provide support at all and clang++ only partially. Visual Studio supports modules to some extent but module files are treated as ordinary text by the IDE so that the writing process is less convenient than usual. There is also no information available on how to incorporate such files into projects. Likewise, other build tools like CMake will require more information than before to deduce all dependencies. To this end, a new interaction between tools and compilers is most likely required. We hope therefore that the reader will find better tool support when learning modules. All circumstances considered, this section is only a short introduction without discussing all possible subtleties.

```
=> modules/math.cppm
```

Module files for clang++ and Visual Studio have the extension cppm whereas the latter also supports ixx. Let us start with a short example:

Click here to view code image

```
export module math;

namespace math {
    export bool is_prime(long i);
}
```

Here we first declare the new module math whereby export module introduces the module interface. Within this module we have the namespace math. Modules and namespaces are orthogonal; we can declare any other namespace in our module or export everything into the global namespace. However, we are convinced that modules with homonymous namespaces are much easier to use. Finally, we `export` the function `is_prime`. Everything else that we might implement in our module won't be seen outside; only what we `export` can be used. This means that we have the full control of what is seen outside the module, in contrast to header files due to their textual inclusion. Instead a module file is translated by the compiler and the result is accordingly a pre-compiled module file.

=> modules/math.cpp

The implementation of this function resides in a regular source file:

Click here to view code image

```
module math;

#include <cmath>

using namespace std;

namespace math {

long max_check(long i) { return std::sqrt(i) + 1; }

bool is_prime(long i)
{
    if (i == 1)
        return false;
    if (i % 2 == 0)
        return i == 2;
    for (long j = 3; j < max_check(i); j+= 2)
        if (i % j == 0)
            return false;
    return true;
}

} // namespace math
```

The only specialty here is the module declaration at the beginning. When we compile this file, the compiler needs the pre-compiled module file.

=> modules/math_app.cpp

In our application, we import the module:

Click here to view code image

```
#include <iostream>
import math;
int main()
{
    using namespace math;
    cout << "982451653 is " << (is_prime(982451653) ? "" : "not ")
         << "a prime number.\n";
}
```

The example also demonstrates that includes and imports can be mixed. However, you should always prefer a module whenever one is available. Instead of the `<iostream>` header, we could use the module `std.core` here.

=> modules/math.cppm

A disadvantage of templates required to be defined in header files was that all internal template functions and classes were visible everywhere the header was included. This problem is overcome with modules where only the exported modules are visible outside the module:

Click here to view code image

```
export module math;
namespace math {
    auto square(auto x) { return x * x; }
    export auto cubic(auto x) { return square(x) * x; }
} // namespace math
```

The importers of module `math` can only use the template function `cubic` but not `square`.

An even greater relief for the author is that macros defined in modules cannot spoil the programs of importers:

Click here to view code image

```
export module math;
namespace math {
#define MACRO_SQUARE(x) ((x) * (x))
} // namespace math
```

`MACRO_SQUARE` can only be used inside the module. And it goes without saying that macros shouldn't be used in the first place or only as the very last resort.

Large modules can be split into sub-modules which are typically written into separate files:

Click here to view code image

```
export module math.extra;

namespace math {
    export inline double twice(double x) { return 2.0 * x; }
} // namespace math
```

We decided to use the same namespace in the sub-module so that the functions can be equally used as those in the main module. Sub-modules can be imported selectively to maximize the control over the visibility. More conveniently, we can import them into the main module and export them there:

```
// File: modules/math.cppm
export module math;

export import math.extra;

// ...
```

All exported entities of `math.extra` are now exported in the module `math` as well. For proper compilation, the module file `math.cppm` requires the pre-compiled module file `math_extra.pcm`. The complete build process of this example with `clang++` is:

Click here to view code image

```
clang++-10 --precompile -o math_extra.pcm math_extra.cppm
clang++-10 -fmodule-file=math_extra.pcm --precompile -o math.pcm math.cppm
clang++-10 -fmodule-file=math.pcm -c -o math.o math.cpp
clang++-10 -fprebuilt-module-path=. -o math_app math.o math_app.cpp
```

To fit the commands on the page we removed the common flags `-std=c++2a` and `-fmodules-ts`.

The fact that header files are included many times not only slows down the build process dramatically, it also opens the door to a wide spectrum of really nasty bugs. Imagine that our header files contain conditionally compiled code fragments that depend on the existence or value of some macros. When the definition of those macros varies from translation to translation, the generated assembler codes from a certain header can change as well. This danger is particularly high when a project is built by multiple people. For instance, one group might develop and compile a utility library, another a domain-specific library, and yet another the application. In the end, everything is linked together and if the headers were compiled inconsistently, the application might behave strangely and the troubleshooting is then probably quite painful.

Modules are more reliable in this regard. The pre-compiled module keeps information on its compile flags and when it is used in another compilation, those flags must match.

Resuming, modules are still in an early stage at the time of writing. Accordingly, we recommend that before introducing them into larger projects you verify first whether your build environment already provides sufficient support. If it does, modules will improve your project considerably because:

- The separate compilation should lead to noticeably lower compile time since modules are only compiled once and not repeatedly like header files.
- The pre-compiled module has a consistent behavior in all translation units.
- No macros are leaking from the modules.
- No error-prone mechanisms like include guards are needed any longer.
- Templates can be exported selectively.
- Modules can easily be bundled to larger ones.

We are therefore convinced that modules will make a major contribution to better software.

## 7.4 Some Final Words

I hope you have enjoyed reading this book and are eager to apply many of the freshly learned techniques in your own projects. It was not my intention to cover all facets of C++; I tried my best to demonstrate that this powerful language can be used in many different ways and provide both expressiveness and performance. Over time you will find your own personal way of making the best use of C++. “Best use” was a fundamental criterion for me: I did not want to enumerate uncountable features and all subtleties vaguely related to the

