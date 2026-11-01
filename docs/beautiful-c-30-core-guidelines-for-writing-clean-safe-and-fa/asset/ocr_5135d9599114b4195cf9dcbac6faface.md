cached, but best of all they can be invoked concurrently without synchronization. This is an excellent burden to be relieved of.

This is the point at which we should talk about `constexpr`. First, though, we are going to talk about inline.

# inline

The `inline` keyword is an old, old keyword. It predates C. In C++ the specifier can be applied to a function or an object. It signifies that the definition can be found in the translation unit. It also tells the compiler that the function is a suitable candidate for inline substitution rather than a function call. This makes it a target for optimiza-tion: why pay the price of a function call when you can simply substitute the code instead?

There are in fact several reasons why you might not want to do that.

When a function is called, some CPU context must be preserved so that the call-ing function can continue upon return. Register values are usually put on the stack, and then restored after the function finishes executing. Choices of calling convention dictate whether this is done by the caller or the callee. The execution of these instruc-tions for context preservation incurs a cost in program size and execution speed. Ideally, an inline substitution will be cheaper than all this bookkeeping. However, if the function being substituted is particularly large, it may make the program bigger. Nonetheless, you may want the inline substitution to take place because it will yield faster code: you are exchanging a few bytes of executable size for the performance gain of not preserving registers and jumping somewhere else.

In the last century that was a quite reasonable thing to assess. However, now we have instruction caches. If we make a substitution, we are in danger of filling up the instruction cache and forcing a cache miss. If we are in a loop and the inline func-tion is only called occasionally, it may make more sense to keep it out of the loop. The compiler knows much more about the behavioral characteristics of the proces-sor than you do, so this is a decision best left to the compiler. In addition, the as-if rule allows the compiler to perform an inline substitution on any function that may improve performance. After all, the whole point of functions is that they are