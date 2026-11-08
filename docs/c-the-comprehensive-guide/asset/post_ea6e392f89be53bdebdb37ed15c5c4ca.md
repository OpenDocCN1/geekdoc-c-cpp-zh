
By the way, you can save yourself the conversion of the `const char []` literal because the compiler automatically interprets string literals with the `""s` suffix as `std::string`. So you can write the following:

```cpp
std::string s = max2("Ernie", "Bert");
```

However, you must have included `operator""s` beforehand—for example, with `using namespace std::literals`.

## 21.7 Summary

For clarity, Table 21.1 lists the most important preprocessor directives once again. I have added a few more with a brief explanation.

| Directive | Explanation |
|---|---|
| `#include` | Include another file |
| `#define` | Define identifier or macro |
| `#undef` | Remove identifier definition |
| `#ifdef` | Check if a preprocessor identifier is defined |
| `#ifndef` | Check if a preprocessor identifier is not defined |
| `#elifdef` | Alternative check if an identifier is defined (C++23) |
| `#elifndef` | Alternative check if an identifier is not defined (C++23) |
| `#if` | Check preprocessor expression |
| `#else` | Alternative source code to one of the preprocessor ifs |
| `#elif` | Alternative source code and another check |
| `#endif` | End of the alternative source code |
| `#line` | Set current line number and filename for compiler error messages |
| `#error` | Abort with an error message |
| `#pragma` | Special instruction to the compiler; very compiler-dependent |

**Table 21.1** Overview of possible preprocessor directives.

# Chapter 22

## Interface to C

### Chapter Takeaways

- **C library with C interface**
  Extension often provided by third parties.
- **extern "C"**
  Mark a function so that it can be used by C++ programs.
- **void\* or void pointer**
  Non-type-safe raw pointer type, to and from which all raw pointer types can be converted; often part of C interfaces.
- **Custom delete function or custom deleter**
  Feature of `shared_ptr`, which can be useful for releasing C resources.

If you are writing a program that uses third-party libraries, then there is a good chance that these libraries come with a C interface. Fortunately, C++ is written in such a way that you can definitely include libraries for C as well. So your choice is not limited.

What is limited is your choice of language features. If you want to use a C library, you can only use C language elements. Here is a by no means exhaustive list of restrictions that you have to accept:

- You have no classes. Structures can only have certain elements; for example, constructors are omitted, and everything must be public. For simplicity, you should only have data elements.
- There are no references. You pass a value or raw pointer.
- Many things from the C++ standard library are taboo. You cannot use standard containers, strings, or streams, but the C++ language designers have thought about interaction possibilities.
- C functions do not throw exceptions. You usually deal with error codes as return values or parameters.
- There are no overloaded functions in C; each name has a fixed set of parameter types (this has partially changed with C11). operator functions do not exist either.
- You will rarely encounter `const` with parameters. When `const` is present, it is more for documentation purposes. You cannot be sure that the C function does not modify your parameter passed by pointer.

After this theoretical list, we dive into practice. As an example, I have chosen the *zlib*¹ C library, which I want to integrate.

The zlib library contains functions for *compressing* data. This means that redundant information is removed, leaving a smaller package of data that you can, for example, transfer over the internet or store on a hard drive. A group of functions in the library is used for reading and writing `*.gz` files—a widely used data format. If you have a program on your computer for packing or unpacking files (e.g., 7zip or WinZip), you can most likely also unpack `*.gz` files. One difference of `*.gz` compared to other packing formats is that each packed file may contain only exactly one original file. It is common to simply append `.gz` to the original file name when the file has been compressed.

## 22.1 Working with Libraries

A C library that you include consists of the following components:

- **Library file**
  You link your program with the library file to use the third-party functions. These are one or more `*.a`, `*.dll` (Windows), or `*.so` files (Linux). In rare cases, you also receive the source code and link the `*.o`/`*.obj` object files to your program.
- **Header files**
  You are usually provided with several `*.h` files. You need to include these in your source code with `#include`.
- **Documentation**
  Sometimes you get a separate document; sometimes you only have the header.

How you make the library and header known during translation is very compiler-dependent. Refer to the documentation on how to adjust the *library* and *include path* and how to link a specific library.

With g++, this example is translated as follows:

```cpp
g++ gzpack.cpp -o gzpack.x -lz -Lzlib -Izlib/include
```

You should already be familiar with the g++ `gzpack.cpp -o gzpack.x` part. The remaining parameters are as follows:

- `-lz`
  `-l` means that a library should be linked. Here it is z for libz.
- `-Lzlib`
  `-L` specifies search paths for libraries; here libz.a is located in the zlib directory.
- `-I zlib/include`
  `-I` specifies search paths for header files; here `zlib.h` is located in the `zlib/include` directory.

¹ “A Massively Spiffy Yet Delicately Unobtrusive Compression Library,” *http://zlib.net*, [2014-05-21]

## 22.2 C Header

The demonstration program creates a compressed output file from any input file. Only three functions from zlib are needed for this. The documentation contains a lot of information about those functions, which I recommend you read. I focus here on the information in the header file or the function signatures from the documentation (some things are simplified). For your own experiments and to replicate the examples, you should of course use the original library:

```cpp
typedef struct gzFile_s *gzFile;
extern "C" gzFile gzopen (const char *path, const char *mode);
extern "C" int gzwrite (gzFile file, voidpc buf, unsigned len);
extern "C" int gzclose (gzFile file);
```

These and many other types and functions are available to you when you include the following in your source code:

```cpp
#include <zlib.h>
```

First, the typedef introduces the new `gzFile` type. This is a pointer to `struct gzFile_s`. Its internal details are intentionally not mentioned because they are irrelevant. Consider `gzFile` simply as a handle that allows you to access the `*.gz` file.

The three functions are free functions, and all parameters and returns are either built-in types or raw pointers—very common in C.

Each function is introduced with `extern "C"` so that as a C++ author, when you include that header, you can distinguish C++ functions from C functions. This is necessary because C++ uses different mechanisms when searching for the appropriate function; this is important for overloading and the like. So, coming from C++, every function signature you want to use must be marked with `extern "C"`. If this is missing in a header, you can alternatively include it in your source code in a slightly more cumbersome way:

```cpp
extern "C" {
    #include <zlib.h>
}
```

So you wrap the entire `#include` in a large `extern "C"`.

After you have the header, you continue with the rest of the program. In addition to `<zlib.h>`, you also need some of the usual C++ headers from the standard library. For error handling with zlib, the `<cerrno>` and `<cstring>` C headers are necessary. The former allows querying the global error code variable, `errno`, which zlib uses; this is stated in the documentation. The latter provides `strerror` to convert an error code into a readable text message. Both headers are part of the C standard library. Therefore, each header exists in two variants: In C++, you use `<cerrno>` when `<errno.h>` is specified in the C documentation. Similarly, the C include `<string.h>` becomes `<cstring>` for C++ programs. The “prefix with c, remove the .h” rule applies to most headers of the C standard library—but only to those, not to third-party libraries. The C++ variants are part of the C++ standard library and guarantee, for example, that each function also gets its `extern "C"`. In addition, all C functions imported this way are provided in the `std::` namespace. Therefore, you can also call the function via `std::strerror()`.

```cpp
// https://godbolt.org/z/9Trh8h8Mb
#include <string>
#include <vector>
#include <span>       // C++20
#include <fstream>    // ifstream
#include <stdexcept>  // runtime_error
#include <iostream>   // cerr
// C-Header:
#include <zlib.h>     // gzXyz; sudo aptitude install libz-dev
#include <cerrno>     // errno
#include <cstring>    // strerror
namespace {
using std::string; using std::span; using std::byte;
```

**Listing 22.1** The “gzpack.cpp” program uses a C library. Here you see the section with the includes.

In the second-to-last line, I start with `namespace {`—an anonymous namespace. This hides all variables, types, and functions in this `*.cpp` file from potential conflicts with others. Instead of free functions, you could also write `static`, but for data types, this is only possible through an anonymous namespace, which is often a good idea.

With the two using declarations, I save typing effort for the rest of the source code. Another advantage of the anonymous namespace is that the two using declarations also apply only within the namespace and do not affect the outside.

Next, I define the class that bundles the main functionality of the C library. In this example, all three relevant C functions are already included. Based on the names, you can probably already guess the meanings and some of the operating rules:
