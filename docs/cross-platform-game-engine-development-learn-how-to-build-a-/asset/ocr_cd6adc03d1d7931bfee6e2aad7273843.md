```
// . . .

// function inlining
#if defined(__clang__) || defined(__gcc__)
    #define FUSE_INLINE __attribute__((always_inline)) inline
    #define FUSE_NO_INLINE __attribute__((noinline))
#elif defined(_MSC_VER)
    #define FUSE_INLINE __forceinline
    #define FUSE_NO_INLINE __declspec(noinline)
#else
    #define FUSE_INLINE inline
    #define FUSE_NO_INLINE
#endif
```

You will also notice that the inline keyword is different across different compilers, so we also need to make sure the correct version is used when compiling our project on different platforms.

# Constants and Macros

Below are some macros that are going to be essential for us as we move forward with the development of our engine. Make sure to update your pch.h and pch.cpp files accordingly.

FUSE_DELETE will be used to free allocated memory and set it to a null pointer. FUSE_BIND is going to be necessary as we create our own event system to handle events. It will be used to bind a class's method to the event dispatcher as a callback function.

+   engine/src/pch.h