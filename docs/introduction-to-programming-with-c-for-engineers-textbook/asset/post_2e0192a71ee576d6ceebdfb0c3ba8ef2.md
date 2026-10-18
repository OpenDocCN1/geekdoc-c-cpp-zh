
## Table A.1 Preprocessor directives.

| Directive | Description | Examples |
|---|---|---|
| `#include < fname >`<br><br>`#include " fname "` | Loads a (header) file name to the translation unit (the same outcome as open-copy-paste).<br><br>The version with `< >` should be used for system headers, since the compiler looks for it in system directories.<br><br>The second version with `" "` searches first in the user’s directory. Hence this version should be used for headers created by a user. | ```cpp
// Common C++ (system) header files
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>
#include <iterator>
#include <array>
#include <random>
#include <fstream>
#include <tuple>
#include <utility>
#include <algorithm>
#include <chrono>

// User’s headers
#include "range.h"
#include "CurrencyCalc.h"
```

To define a special version of code, we can use:

```cpp
#ifndef CODE_VERSION    2

#if CODE_VERSION == 2
        // Code for ver. 2
#endif
``` |

[PAGE 590]

\begin{tabular}{ccc}
\#define name & Used to define a name or a macro. These are then expanded and used by other directives of the preprocessor. & We define a macro MAX with two parameters x and y: \\
\#define name val & A frequently used application is to create an include guard for a header, to define a code version or to define macros that expand before compilation. & #define MAX(x, y) ((x) > (y) ? (x) : (y)) \\
\#define macro(arg) & Although macros look like functions, they are not, and they obscure the code. Therefore they should not be used unless necessary. Instead, in C++, we can use const values or constexpr (Section 3.13.2.2, GROUP 4, Table 3.15). & For example: \\
 &  & cout << MAX("Fox", "Dog") << endl; \\
 &  & is expanded to \\
 &  & cout << ((*Fox") > ("Dog") ? ("Fox") : ("Dog")) << endl; \\
 &  & and then compiled. Do not forget the parentheses in the macro. There can be only one definition of a variable, constant, function, etc. in the program. But header files are included many times, and their inclusions can be chained. Thus, to ensure that a header is included only once, we can use the following preprocessor pattern, called an include guard: \\
 &  & // This is TransDir.h header \\
 &  & #ifndef TransDir_h \\
 &  & #define TransDir_h \\
 &  & // These definitions are included \\
 &  & // only once \\
 &  & #endif // TransDir_h \\
 &  & First it checks if the TransDir.h name has been already defined. If not, it is defined, and the rest of the file is included. Otherwise, nothing between #ifndef and #endif is included. The other option is to use #pragma once. \\
\end{tabular}

[PAGE 591]

## Table A.1 (continued)

| Directive | Description | Examples |
|---|---|---|
| (1) `#ifdef name`<br><br>(2) `#if condition`<br>`#else`<br>`#endif` | Conditional compilation. There are two versions. In (1), the code is compiled if `name` has been defined with the `#define` directive.<br><br>In (2), the code between `#if` and `#else` is compiled if condition is not 0 (`true`). Otherwise, the code between `#else` ... `#endif` is used.<br><br>`#else` is optional. | To compile code only on a selected OS:
```cpp
#if WIN32
#include <urlmon.h>
#pragma comment(lib, "urlmon.lib")
#else
// A version for other OSs
#endif
```

The following trick is used to exclude a fragment of code from the build:
```cpp
#if 0
// Whatever is here will not be compiled
** **
#endif
```
We can restore it quite easily by commenting out the lines containing `#if` and `#endif`. |
| `#pragma` | Compiler-specific option. | ```cpp
// A one-time include guard
#pragma once
// Create a parallel for loop with OpenMP
#pragma omp parallel for
``` |
| `#undef` | Un-defines a macro or name introduced by a previous `#define`. | Let’s change our previous MAX macro and make it “soft.”
```cpp
#undef MAX
#define MAX(x,y) ((x)>(y)?(x):(y))
``` |
| `#error`<br>`#warning` | `#error` stops compilation.<br>`#warning` issues a platform-dependent diagnostic message (sometimes used with `#pragma`). | ```cpp
#if !defined(__cplusplus)
#error This code needs the C++ compiler
#endif
``` |

[PAGE 592]

|  |  | The following fragment defines the REQUIRE macro, which checks whether `expr` is true when executing in the DEBUGGING version of the code. For other versions, it reduces to a semicolon ; denoting an empty expression. |
|---|---|---|
| `#` | Used with the `#define` macro.<br>It makes the first argument after `#` be returned as a string in quotation marks. |  |
| `##` | Concatenates a token before and after the operator `##`. |  |
| `__FILE__`<br>`__LINE__`<br>`__TIME__`<br>`__DATE__`<br>`__cplusplus` | Special predefined preprocessor values (“magic constants”):<br>1. Current file name (string literal)<br>2. Current line (numeric)<br>3. Current time (string)<br>4. Current date (string)<br>5. Defined if a C++ compiler is used |  |

```
```cpp
#if     DEBUGGING

void REQUIRE_Fun( int expr,
                 const char * expr_name,
                 const char * file_name,
                 const int line_num );

#define QUOTE(x) #x
#define QUOTE(x) _QUOTE(x)

// Put REQUIRE to test expressions
#define REQUIRE(expr) \
        REQUIRE_Fun( expr, #expr, \
          __FILE__ , QUOTE(__LINE__) );

#else   // DEBUGGING

#define REQUIRE(expr) ;

#endif // DEBUGGING
```
```

The DEBUGGING version should define the REQUIRE_Fun function elsewhere. Its role is to display a message to the user or to a log file on a given platform. `expr` is an expression provided to REQUIRE, whereas `#expr` is that expression expressed as a string, i.e. within quotation marks " ".

`QUOTE(__LINE__)`—after the first pass of the preprocessor—evolves into `__QUOTE(num)`, which after the second pass is converted into num expressed as a string, i.e. something like "num".

In modern C++, we use `assert` and `cassert` for this diagnostic purpose.
