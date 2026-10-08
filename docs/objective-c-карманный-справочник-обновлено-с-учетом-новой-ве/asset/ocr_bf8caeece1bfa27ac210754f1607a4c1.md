68

CHAPTER 3: Memory Management

and calling them for you. The implementation is somewhat more complicated.

**Note:** Most of the examples in this book use manual reference counting. This is intentional. Even though ARC is recommended for new development, there is a lot of legacy code around that does not use it. Even if you are using ARC, you should still understand the retain and release semantics that are implicitly added for you. It's very easy for a programmer who is comfortable with manual reference counting to switch to using ARC, just as it's useful to understand your CPU's instruction set even if you never write any assembly code.

Rather than inserting message sends directly into the code, the compiler front inserts calls to functions like `objc_retain()` and `objc_release()`. The optimizer then tries to combine or eliminate these calls. In the simple case, these functions do the equivalent of a message send. In some common cases, they are significantly more efficient.

In simple use, you can forget about memory management when using ARC. If you are using a recent version of Xcode, then ARC is the default. If you are compiling on the command line or with some other build system, add `-fobjc-arc`. Now just forget about retaining and releasing objects.