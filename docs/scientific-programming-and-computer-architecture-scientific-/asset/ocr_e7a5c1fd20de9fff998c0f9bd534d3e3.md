# 1.3. C++ review

present the contents of the header file in stages, gradually unveiling features of C++.
nThe skeleton of the header file is listed below.

```
1 #ifndef MYVECTOR
2 #define MYVECTOR
3 #include <cassert>
4 #include <cmath>
5 #include <cstdlib>
6 #include <string>
7 #include <iostream>
8 #include <fstream>
9
10 using namespace std;
11
12 class Vector{
13 private:
14 ..
15 public:
16 ...
17 };
18
19 #endif
```

Lines 1, 2, and 19 ensure that the header file expands to the source code in between
if only if the variable MYVECTOR is defined. Here MYVECTOR is not good
nomenclature, as it may be inadvertently used by some other header, subverting
our attempt to ensure conditional inclusion of header files.

It is typical for C/C++ sources to begin by including a number of header files to
interface to other source files or libraries. C programs include the header assert.h
to use the assert() macro (see section 1.2.3). C++ programs may include either
assert.h or cassert, as on line 3, to emphasize that a C facility is being employed.

The Vector class uses other C facilities as well. It uses the fabs() function fromncmath (line 4) in one of its member functions to compute the norm of the vector. C
facilities to allocate and release memory are defined in stdlib (line 5).

C++ facilities for input/output from terminals and files are in iostream (line
7) and fstream (line 8), respectively. Member functions that input/output vectors