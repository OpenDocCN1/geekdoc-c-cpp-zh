Thus, for example, the code for the telephone table lookup shown in Figure 65 bases all its data accesses on the contents of register 2 which is the base for the DSECT ID. Similarly, if a reentrant program were to make all its data references within a DSECT which itself is based on a user supplied base register, the program would use different data areas for different users. The program itself would have no local data other than constants.

A program which only modifies the contents of its registers and data pointed to by the registers in the user's private data area does not violate reentrancy rules. Each user has their own set of registers and their own private (unshared) data area.

Even if a program is reentrant and each user has their own data area, there is still a problem when a program calls itself (recursive call) if it uses a statically allocated (legacy) save area.

If a program calls itself, the second call will overwrite the statically allocated save area. This is also true if a program indirectly calls itself. Consequently, we need a mechanism to stack multiple save areas for the same function.

One approach is to have the called routine dynamically allocate a new save area each time it is called and free it upon ultimate return. This is usually done with the GETMAIN or STORAGE system macros.

Another approach is to use the system stack. The original IBM 360 architecture did not provide for system supported stacks. It is rumored that the engineers thought this feature was more characteristic of a mini-computer. Nonetheless, the feature was ultimately introduced in 1989 – 25 years later! The system stack and several semi-privileged instructions support recursive calls.

# 19.3.1 Chained Dynamically Allocated Save Areas

As noted, programs that are to be recursively called need to be reentrant so that successive calls do not use or alter previous calls' intermediate results if they are stored in. For example, the calculation of factorials is often done on a series of recursive calls. Each instance waits for the return of one or more deeper invocations. Each invocation stores local values as needed to complete its evaluation level prior to making a return.

An example of factorial in C is given in Figure 67Figure 1 where, on line 12, each invocation waits for lower level invocations to return and, ultimately, their result be multiplied by a current value of i. The variable i must be local to each invocation and not shared.

One way to implement this program is to use a chain of save areas dynamically allocated by the GETMAIN or STORAGE macros.