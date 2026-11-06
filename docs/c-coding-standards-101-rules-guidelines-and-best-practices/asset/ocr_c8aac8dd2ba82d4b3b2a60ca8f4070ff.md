# # 62. Don’t allow exceptions to propagate across module boundaries.

# ## Summary

Don’t throw stones into your neighbor’s garden: There is no ubiquitous binary standard for C++ exception handling. Don’t allow exceptions to propagate between two pieces of code unless you control the compiler and compiler options used to build both sides; otherwise, the modules might not support compatible implementations for exception propagation. Typically, this boils down to: Don’t let exceptions propagate across module/subsystem boundaries.

# ## Discussion

The C++ Standard does not specify the way exception propagation has to be implemented, and there isn’t even a *de facto* standard respected by most systems. The mechanics of exception propagation vary not only with the operating system and compiler used, but also with the compiler options used to build each module of your application with a given compiler on a given operating system. Therefore, an application must prevent exception handling incompatibilities by shielding the boundaries of each of its major modules, meaning each unit for which the developer can ensure that the same compiler and options are consistently used.

At a minimum, your application must have *catch-all* `catch(...)` seals in the following places, most of which apply directly to modules:

+   - **Around main:** Catch and log any otherwise uncaught exception that’s about to end your program ignominiously.
+   - **Around callbacks from code you don’t control:** Operating systems and libraries offer frameworks in which you pass a pointer to a function to be invoked later (e.g., when an asynchronous event occurs). Don’t allow exceptions to propagate out of your callback, because it’s very possible that the code invoking your callback does not use the same exception handling mechanism. For that matter, it might not even have been written in C++.
+   - **Around thread boundaries:** Ultimately, a thread is created from within the bowels of the operating system. Make sure your thread mainline function doesn’t surprise the system by passing it an exception.
+   - **Around module interface boundaries:** Your subsystem will expose some public interface for the rest of the world to use. If the subsystem is packaged as a separate library, prefer to confine exceptions inside and use ye olde staid-but-stable error codes for signaling errors to the outer world. (See Item 72.)