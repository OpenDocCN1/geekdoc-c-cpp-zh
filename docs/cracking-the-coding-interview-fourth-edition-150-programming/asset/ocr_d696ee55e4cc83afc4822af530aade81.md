# Solutions to Chapter 16 | Low Level

16.6 Discuss how you would make sure that a process doesn't access an unauthorized part of the stack.

# SOLUTION

As with any ambiguously worded interview question, it may help to probe the interviewer to understand what specifically you're intended to solve. Are you trying to prevent code that has overflowed a buffer from compromising the execution by overwriting stack values? Are you trying to maintain some form of thread-specific isolation between threads? Is the code of interest native code like C++ or running under a virtual machine like Java?

Remember that, in a multi-threaded environment, there can be multiple stacks in a process.

# NATIVE CODE

One threat to the stack is malicious program input, which can overflow a buffer and overwrite stack pointers, thus circumventing the intended execution of program.

If the interviewer is looking for a simple method to reduce the risk of buffer overflows in native code, modern compilers provide this sort of stack protection through a command line. With Microsoft's CL, you just pass /GS to the compiler. With GCC, you can use -stack-protector-all.

For more complex schemes, you could use individual permissions on the range of memory pages representing the stack section you care about. In the Win32 API, you'd use the VirtualProtect API to mark the page PAGE_READONLY or PAGE_NOACCESS. This will cause the code accessing the region to go through an exception on access to the specific section of the stack.

Alternately, you could use the HW Debug Registers (DRs) to set a read or write breakpoint on the specific memory addresses of interest. A separate process could be used to debug the process of interest, catch the HW exception that would be generated if this section of the stack was accessed.

However, it's very important to note that under normal circumstances, threads and processes are not means of access control. Nothing can prevent native code from writing anywhere within the address space of its process, including to the stack. Specifically, there is nothing to prevent malicious code in the process from calling VirtualProtect and marking the stack sections of interest PAGE_EXECUTE_READWRITE. Equally so, nothing prevents code from zeroing out the HW debug registers, eliminating their breakpoints. In summary, nothing can fully prevent native code from accessing memory addresses, including the stack, within its own process space.

# MANAGED CODE