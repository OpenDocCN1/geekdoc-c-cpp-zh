subset of the main functionality, including many container data types like priority queues or trees.

Although many libraries are available, sometimes it is inevitable to implement some specialized but basic functions by yourself. In this case, after the code has been proven to be reliable and useful for some time, you can put it in a self-created library. How to create libraries is explained in the last part of this chapter.

Many libraries are dynamically linked. This means, when the linker assembles the executable, no code will be included from the libraries. Only when the program is executed, the executable functions from the corresponding library will be loaded to the memory. This helps to keep the sizes of the executables of your simulation programs small. Nevertheless, sometimes you have to force the linker to include the library functions in the executable already when the program is linked. This is called static linking. This may happen when you want to run your simulations on another machine where the library is not installed. You can tell the linker to link the executable code for the library function by using the linker/compiler option -static.

# 7.1 Standard C library

You have already encountered many standard C library functions in Chap. 1, for example for allocating memory via malloc(), for calling shell functions via system(), or converting strings to integers via atoi(). To use functions from this library properly, you have to use the directive

```
#include <stdlib.h>
```

Note that you do not have to use a -l option for linking executables of functions for the standard C library, because they are linked always.

Here, we are discussing only one more function, which is used quite frequently in the context of simulations. It is qsort(), which allows to sort in ascending order arrays of arbitrary data types. The function implements the efficient quicksort algorithm [Sedgwick (1990); Cormen et al. (2001)], which sorts n elements in typically O(n log n) comparison steps. The order is determined by some sorting criterion, which has to be provided by the program which calls qsort().

The function prototype of qsort() looks as follows: