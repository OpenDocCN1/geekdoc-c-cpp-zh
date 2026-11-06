the function declares. Non-`static` local variables need to exist while a function is executing. They need to remain active if the function makes calls to other functions. But when a called function returns to its caller, the called function’s non-`static` local variables need to “go away.” The called function’s stack frame is a perfect place to reserve the memory for the called function’s non-`static` local variables. That stack frame exists as long as the called function is active. When that function returns—and no longer needs its non-`static` local variables—its stack frame is *popped* from the stack, and those non-`static` local variables no longer exist.

# *Stack Overflow*

Of course, the amount of memory in a computer is finite, so only a certain amount of memory can be used to store activation records on the function-call stack. If more function calls occur than can have their activation records stored on the function-call stack, a fatal error known as **stack overflow** occurs.[^3]

+   3. This is how the website [**stackoverflow.com**](https://stackoverflow.com) got its name. This is a great website for getting answers to your programming questions.

# *Function-Call Stack in Action*

Now let’s consider how the call stack supports the operation of a `square` function called by `main` (lines 9–13 of [Fig. 6.12](#)).