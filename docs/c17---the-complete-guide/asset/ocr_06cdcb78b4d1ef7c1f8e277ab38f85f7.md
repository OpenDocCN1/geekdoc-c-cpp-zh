Note that this problem applies only to the global operator new(). If the type-specific operator new() is defined for S, the operator is still also used as a fallback for over-aligned data, which means that such a program behaves in the same way that it did before C++17.

Note also that printf() is used intentionally here to avoid an output to std::cout allocating memory while we are allocating memory, which might result in nasty errors (core dumps at best).

# 30.4 Tracking All ::new Calls

The following program demonstrates how to use the new operator new() overloads in combination with inline variables and [[nodiscard]] to track all calls of ::new simply by including this header file:

```
lang/tracknew.hpp
#ifndeF TRACKNEW_HPP
#define TRACKNEW_HPP

#include <new>      // for std::align_val_t
#include <cstdio>   // for printf()
#include <cstdlib>  // for malloc() and aligned_alloc()
#ifdef _MSC_VER
#include <malloc.h> // for _aligned_malloc() and _aligned_free()
#endif

class TrackNew {
private:
    static inline int numMalloc = 0;      // num malloc calls
    static inline size_t sumSize = 0;     // bytes allocated so far
    static inline bool doTrace = false;   // tracing enabled
    static inline bool inNew = false;     // don't track output inside new overloads
public:
    static void reset() {                 // reset new/memory counters
        numMalloc = 0;
        sumSize = 0;
    }

    static void trace(bool b) {           // enable/disable tracing
        doTrace = b;
    }

    // implementation of tracked allocation:
    static void* allocate(std::size_t size, std::size_t align,
                          const char* call) {
    // track and trace the allocation:
    ++numMalloc;
    sumSize += size;
```