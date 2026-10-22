```
image
template<typename Rep>
double foo(Array<double, Rep> const&); and no conversion happens unless one is actually needed.
```

The valarray proposal came late in the C++ standardization process and practically rewrote all the text regarding valarray in the standard. It was rejected as a result, and instead, a few tweaks were added to the existing text to allow implementations based on expression templates. However, the exploitation of this allowance remains much more cumbersome than what was discussed here. At the time of this writing, no such implementation is known, and standard valarrays are, generally speaking, quite inefficient at performing the operations for which they were designed.

Finally, it is worth observing here that many of the pioneering techniques presented in this chapter, as well as what later became known as the STL,² were all originally implemented on the same compiler: version 4 of the Borland C++ compiler. This was perhaps the first compiler that made template programming broadly popular in the C++ programming community.

Expression templates were first applied primarily for operations on array-like types. However, after a few years, new applications were found. Among the most ground-breaking were Jaakko Järvi’s and Gary Powell’s Boost.Lambda library(see [LambdaLib]), which provided a usable lambda expression facility years before lambda expressions became a core language feature³, and Eric Niebler’s Boost.Proto library, which is a library to meta-program expression templates, with the goal of creating embedded domain-specific languages in C++. Other Boost libraries, like Boost.Fusion and Boost.Hana, also make advanced use of expression templates.

1 It is convenient to reuse the previously developed SArray here, but in an industrial-strength library, a special-purpose implementation may be preferable because we won’t use all the features of SArray.

2 The Standard Template Library (STL) revolutionized the world of C++ libraries and was later made part of the C++ standard library (see [JosuttisStdLib]).

3 Jaakko was also instrumental in developing the core language feature.