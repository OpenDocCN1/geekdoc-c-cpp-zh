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
math.cppm
clang++-10 -fmodule-file=math.pcm -c -o math.o math.cpp
clang++-10 -fprebuilt-module-path=. -o math_app math.o math_app.cpp
math_app.cpp
```

To fit the commands on the page we removed the common flags `-std=c++2a` and `-fmodules-ts`.

The fact that header files are included many times not only slows down the build process dramatically, it also opens the door to a wide spectrum of really nasty bugs. Imagine that our header files contain conditionally compiled code fragments that depend on the existence or value of some macros. When the definition of those macros varies from translation to translation, the generated