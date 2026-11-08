# 7.12.2  Inline Functions

At runtime, for a function call, a stack area is created where the function stores its data. You will also find the return address stored there so that the function knows where it was called from and can return there. In addition, the stack area is used to store local data, local parameters, and the return type. Modern CPUs can handle all of this easily. What hurts, however, is that caches and pipelines need to be cleared for a function call—things that make modern CPUs really fast. This is a considerable effort for a simple function call. If speed is crucial and such a function is called frequently in a loop, then unnecessary computation time is wasted.

For such purposes, you can mark a function with the keyword inline:

```
inline int simple_func(double a, double b, double c);
```

With the keyword inline before the function, you suggest to the compiler that it should not integrate the function code as a callable function but should insert it in place of the function call.

> **Suggestion for the Compiler**
> 
> The term should is used here because it is merely a suggestion for the compiler. Whether the compiler integrates the function in place or not is ultimately decided by the compiler itself.

There are other scenarios where the compiler can inline:

+   - The compiler can decide to inline a function definition from the same source file, even without the inline keyword, especially if the function is used frequently.
+   - If this function definition is also a function template, compilers are even more eager to inline it.
+   - And at the maximum optimization level, newer compilers even inline arbitrary functions across source file boundaries.

What the compiler actually inlines depends on many factors and is hard to predict.

# 7.12.3  “constexpr”

A function whose return is not only marked with const but also with constexpr must have a quite simple function body that the compiler can compute during translation to insert the result. As a rule of thumb, if you only write a return statement in the function body, then the chances are good that the use of constexpr is allowed:

```
constexpr int doubledUntil100(int value) {
    return value<=50 ? value*2 : 100;
}
```