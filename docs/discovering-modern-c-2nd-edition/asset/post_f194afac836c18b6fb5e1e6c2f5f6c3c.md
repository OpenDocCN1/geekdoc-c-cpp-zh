
```cpp
#include <iostream>
#include <cmath>
int main (int argc, char* argv[])
{
    std::cout << "sqrt(17) is " << sqrt(17) << '\n';
}
```

=> c++03/build_example.ii.cpp

```cpp
# 1 "build_example.cpp"
# 1 "<command-line>"
// ... skipped some lines here
# 1 "/usr/include/c++/4.8/iostream" 1 3
# 36 "/usr/include/c++/4.8/iostream" 3
// ... skipped some lines here
# 184 "/usr/include/x86_64-linux-gnu/c++/4.8/bits/c++config.h" 3
namespace std
{
typedef long unsigned int size_t;
// ... skipped many, many lines here
# 3 "build_example.cpp" 2

int main (int argc, char* argv[])
{
    std::cout << "sqrt(17) is " << sqrt(17) << '\n';
}
```

```cpp
int main ()
{
# if __has_include(<any>)
    std::cout << "any found, we do something useful.\n";
# else
    std::cerr << "any not found, we have to skip this example.\n";
# endif
}
```

```asm
.file   "build_example.cpp"
.local  _ZStl8__ioinit
.comm   _ZStl8__ioinit,1,1
.section        .rodata
.LC0:
.string "sqrt(17) is "
.text
.globl  main
.type   main, @function
main:
.LFB1055:
.cfi_startproc
pushq   %rbp
.cfi_def_cfa_offset 16
.cfi_offset 6, -16
movq    %rsp, %rbp
.cfi_def_cfa_register 6
subq    $32, %rsp
movl    %edi, -4(%rbp)
movq    %rsi, -16(%rbp)
movl    $.LC0, %esi
movl    $_ZSt4cout, %edi
call    _ZStlsISt11char_traitsIcEERSt13basic_ostream
movq    %rax, %rdx
; just a bit more code
```

fluxer.o: fluxer.cpp mesher.hpp solver.hpp
g++ fluxer.cpp -c -o fluxer.o

```makefile
.cpp.o:
	${CXX} ${CXXFLAGS} $^ -c -o $@
```

```makefile
CXX=      g++-10
CXXFLAGS= -O3 -DNDEBUG   # Release
# CXXFLAGS= -O0 -g       # Debug
```

libmesher.a: mesher.o # more mesher sources
ar cr $@ $^

libsolver.a: solver.o # more solver sources
ar cr $@ $^

fluxer: fluxer.o libmesher.a libsolver.a
${CXX} ${CXXFLAGS} $^ -o $@

g++ fluxer.cpp -c -o fluxer.o
g++ mesher.cpp -c -o mesher.o
ar cr libmesher.a mesher.o
g++ solver.cpp -c -o solver.o
ar cr libsolver.a solver.o
g++ fluxer.o libmesher.a libsolver.a -o fluxer

g++ mesher.cpp -c -o mesher.o
ar cr libmesher.a mesher.o
g++ fluxer.o libmesher.a libsolver.a -o fluxer

```cmake
cmake_minimum_required (VERSION 2.6)
project (Fluxer)
```

```cmake
add_library(solver solver.cpp)
```

```cmake
add_library(mesher SHARED mesher.cpp)
```

```cmake
add_executable(fluxer fluxer.cpp)
target_link_libraries(fluxer solver mesher)
```

```text
-- The C compiler identification is GNU 4.9.2
-- The CXX compiler identification is GNU 4.9.2
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Configuring done
-- Generating done
-- Build files have been written to: ... /CMake_example/build
```

```text
Scanning dependencies of target solver
[ 33%] Building CXX object CMakeFiles/solver.dir/solver.cpp.o
Linking CXX static library libsolver.a
[ 33%] Built target solver
Scanning dependencies of target mesher
[ 66%] Building CXX object CMakeFiles/mesher.dir/mesher.cpp.o
Linking CXX shared library libmesher.so
[ 66%] Built target mesher
Scanning dependencies of target fluxer
[100%] Building CXX object CMakeFiles/fluxer.dir/fluxer.cpp.o
Linking CXX executable fluxer
[100%] Built executable fluxer
[100%] Built target fluxer
```

```cpp
// File: herberts/math_functions.hpp
#ifndef HERBERTS_MATH_FUNCTIONS_INCLUDE
#define HERBERTS_MATH_FUNCTIONS_INCLUDE

typedef double hreal; // Herbert's real numbers

hreal sine(hreal);
hreal cosine(hreal);
...
#endif

// File: herberts/math_functions.cpp
#include <herberts/math_functions.hpp>

hreal divide_by_square(hreal x, hreal y) { ... }

hreal sine(hreal) { ... }
hreal cosine(hreal) { ... }
...
```

```cpp
// File: herberts/math_functions.hpp
..
double square(double x) { return x*x; }
double pi= 3.14159265358979323846264338327950288419716939;
```

```text
g++-4.8 -o multiref_example multiref1.cpp multiref2.cpp
/tmp/cc65d1qC.o:(.data+0x0): multiple definition of 'pi'
/tmp/cc1slHBY.o:(.data+0x0): first defined here
/tmp/cc65d1qC.o: In function 'square(double)':
multiref2.cpp:(.text+0x0): multiple definition of 'square(double)'
/tmp/cc1slHBY.o:multiref1.cpp:(.text+0x63): first defined here
collect2: error: ld returned 1 exit status
```

```cpp
static double square(double x) { return x*x; }
```

```cpp
inline double square(double x) { return x*x; }
```

```cpp
// File: herberts/math_functions.hpp
double square(double x);
```

```cpp
// File: herberts/math_functions.cpp
double square(double x) { return x*x; }
```

```cpp
static double pi= 3.14159265358979323846264338327950288419716939;
```

```cpp
// File: multiref.hpp
static double pi = 17.4;
```

```cpp
// File: multiref1.cpp
int main (int argc, char* argv[])
{
    fix_pi();
    std::cout << "pi = " << pi << std::endl;
}
```

```cpp
// File: multiref2.cpp
void fix_pi() { pi= 3.14159265358979323846264338327950288419716939; }
```

```cpp
// File: herberts/math_functions.hpp
extern double pi;
```

```cpp
// File: herberts/math_functions.cpp
double pi= 3.14159265358979323846264338327950288419716939;
```

```cpp
// File: herberts/math_functions.hpp
const double pi = 3.14159265358979323846264338327950288419716939;
```

```cpp
export module math;
namespace math {
    export bool is_prime(long i);
}
```

```cpp
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

```cpp
#include <iostream>

import math;

int main()
{
    using namespace math;
    cout << "982451653 is " << (is_prime(982451653) ? "" : "not ")
         << "a prime number.\n";
}
```

```cpp
export module math;

namespace math {
    auto square(auto x) { return x * x; }
    export auto cubic(auto x) { return square(x) * x; }
} // namespace math
```

```cpp
export module math;
namespace math {
#define MACRO_SQUARE(x) ((x) * (x))
} // namespace math
```

```cpp
export module math.extra;

namespace math {
    export inline double twice(double x) { return 2.0 * x; }
} // namespace math
```

```text
clang++-10 --precompile -o math_extra.pcm math_extra.cppm
clang++-10 -fmodule-file=math_extra.pcm --precompile -o math.pcm math.cppm
clang++-10 -fmodule-file=math.pcm -c -o math.o math.cpp
clang++-10 -fprebuilt-module-path=. -o math_app math.o math_app.cpp
```

```cpp
#include <iostream>
#include <cmath>

void diag_prec(int size, double *x, double* y)
{
    y[0] = x[0];

    for (int i = 1; i < size; i++)
        y[i] = 0.5 * x[i];

}
```

```cpp
double one_norm(int size, double *vp)
{
    double sum= 0;
    for (int i = 0; i < size; i++)
        sum+= fabs(vp[i]);

    return sum;
}
```

```cpp
double dot(int size, double *vp, double *wp)
{
    double sum= 0;
    for (int i = 0; i < size; i++)
        sum+= vp[i] * wp[i];

    return sum;
}
```

```cpp
int cg(int size, double *x, double *b,
       void (*prec)(int, double*, double*), double eps)
{
    int i, j, iter= 0;
    double rho, rho_1, alpha;
    double *p= new double[size];
    double *q= new double[size];
    double *r= new double[size];
    double *z= new double[size];

    // r = A*x;
    r[0] = 2.0 * x[0] - x[1];
    for (int i= 1; i < size-1; i++)
        r[i] = 2.0 * x[i] - x[i-1] - x[i+1];
```
