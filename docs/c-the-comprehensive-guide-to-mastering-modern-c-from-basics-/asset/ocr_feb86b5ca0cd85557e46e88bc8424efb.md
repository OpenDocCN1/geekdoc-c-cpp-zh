# 2.3 Current Compilers

As already mentioned, the term compiler does not cover a single translation program, but the entire tool chain from the preprocessor to the linker. In addition, the standard library is an integral part of C++. So if you install a compiler on your system, you will always receive a standard library with it.

With well-meaning intentions, this book largely refers to the current standard known as C++23. For C++20, the majority is implemented in the current compilers. I emphasize things that belong to C++23 because the language support is still incomplete, but it is improving. If you use the possibilities that have been added since C++11, you will be able to learn the language faster and use it better than was the case with the previous versions up to C++98, for example.

With a modern compiler, C++ is definitely more enjoyable. Fortunately, most compilers are more or less up to date.

The C++ compiler g++ from the GNU Compiler Collection (GCC) is the compiler available on most platforms. It is also the testing ground for trying out new things, so you will almost always find new features implemented here first. Today, in the middle of 2024, C++20 is very well implemented. Unfortunately, C++23 still lacks some features, especially for ranges. On Linux,