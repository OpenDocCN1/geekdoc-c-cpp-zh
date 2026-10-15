# 6.6 C++ Standard Library Header Files

The C++ Standard Library is divided into many portions, each with its own header file. The header files contain the function prototypes for the related functions that form each portion of the library. The header files also contain definitions of various class types and functions, as well as constants needed by those functions. A header file “instructs” the compiler on how to interface with library and user-written components.

Figure 6.6 lists some common C++ Standard Library header files, most of which are discussed later in the book. The term “macro” that is used several times in Fig. 6.6 is discussed in detail in Appendix D, Preprocessor. Header file names ending in .h are “old-style” header files that have been superseded by the C++ Standard Library header files. We use only the C++ Standard Library versions of each header file in this book to ensure that our examples will work on most standard C++ compilers.

| C++ Standard Library header file | Explanation |
|---|---|
| <iostream> | Contains function prototypes for the C++ standard input and standard output functions, introduced in Chapter 2, and is covered in more detail in Chapter 15, Stream Input/Output. This header file replaces header file <iostream.h>. |
| <iomanip> | Contains function prototypes for stream manipulators that format streams of data. This header file is first used in Section 4.7 and is discussed in more detail in Chapter 15, Stream Input/Output. This header file replaces header file <iomanip.h>. |
| <cmath> | Contains function prototypes for math library functions (discussed in Section 6.3). This header file replaces header file <math.h>. |
| <cstdlib> | Contains function prototypes for conversions of numbers to text, text to numbers, memory allocation, random numbers and various other utility functions. Portions of the header file are covered in Section 6.7; Chapter 11, Operator Overloading: String and Array Objects; Chapter 16, Exception Handling; and Chapter 19, Bits, Characters, C Strings and structs. This header file replaces header file <stdlib.h>. |
| <ctime> | Contains function prototypes and types for manipulating the time and date. This header file replaces header file <time.h>. This header file is used in Section 6.7. |
| <vector>
<list>
<deque>
<queue>
<stack>
<map>
<set>
<bitset> | These header files contain classes that implement the C++ Standard Library containers. Containers store data during a program’s execution. The <vector> header is first introduced in Chapter 7, Arrays and Vectors. We discuss all these header files in Chapter 20, Standard Template Library (STL). |