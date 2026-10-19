optimized to see the kinds of optimizations that are performed. None of these benefits has much to do with the debugger’s intended use—diagnosing errors that have already been detected—but imaginative use of a debugger produces benefits far beyond its initial charter.

# System Perturbers

Another class of test-support tools are designed to perturb a system. Many people have stories of programs that work 99 times out of 100 but fail on the hundredth run-through with the same data. The problem is nearly always a failure to initialize a variable somewhere, and it’s usually hard to reproduce because 99 times out of 100 the uninitialized variable happens to be 0.

Test-support tools in this class have a variety of capabilities:

+   - **Memory filling**  You want to be sure you don’t have any uninitialized variables. Some tools fill memory with arbitrary values before you run your program so that uninitialized variables aren’t set to 0 accidentally. In some cases, the memory might be set to a specific value. For example, on the x86 processor, the value `0xCC` is the machine-language code for a breakpoint interrupt. If you fill memory with `0xCC` and have an error that causes you to execute something you shouldn’t, you’ll hit a breakpoint in the debugger and detect the error.
+   - **Memory shaking**  In multitasking systems, some tools can rearrange memory as your program operates so that you can be sure you haven’t written any code that depends on data being in absolute rather than relative locations.
+   - **Selective memory failing**  A memory driver can simulate low-memory conditions in which a program might be running out of memory, fail on a memory request, grant an arbitrary number of memory requests before failing, or fail on an arbitrary number of requests before granting one. This is especially useful for testing complicated programs that work with dynamically allocated memory.
+   - **Memory-access checking (bounds checking)**  Bounds checkers watch pointer operations to make sure your pointers behave themselves. Such a tool is useful for detecting uninitialized or dangling pointers.

# Error Databases

One powerful test tool is a database of errors that have been reported. Such a database is both a management and a technical tool. It allows you to check for recurring errors, track the rate at which new errors are being detected and corrected, and track the status of open and closed errors and their severity. For details on what information you should keep in an error database, see Section 22.7, “Keeping Test Records.”