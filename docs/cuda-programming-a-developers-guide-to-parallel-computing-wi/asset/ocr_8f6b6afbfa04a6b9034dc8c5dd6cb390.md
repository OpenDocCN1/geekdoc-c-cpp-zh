| Name | Description | Speed | Kernel Access | Host Access | Visibility |
| :--- | :--- | :--- | :--- | :--- | :--- |
| .reg | Registers (fastest) | Fastest | Read/write | None | Per thread |
| .const | Constant memory | Fast for uniform access | Read only | Read/write | Per context |
| .global | Global memory | Slow (coalesced) to very slow (noncoalesced) | Read/write | Read/write | Per context |
| .local | Private memory | Slow on compute 1.x devices; much faster on compute 2.x devices | Read/write | None | Per thread |
| .param (kernel call) | Formal parameters used in kernel call from host | As per constant memory | Read only | Read/write | Per grid |
| .param (device call) | Formal parameters used in calls from global to device functions | As per registers; generally device functions are in-lined | Read/write | None | Per thread |
| .shared | Shared memory | Fast for bank conflict-free access | Read/write | None | Per block |

not always the case. More blocks can mean more contention for shared resources (shared memory, L1/L2 caches).

Register usage can often be reduced simply by rearranging the C source code. By bringing the assignment and usage of a variable closer together you enable the compiler to reuse registers. Thus, at the start of the kernel you might assign a, b, and c. If in fact they are used only later in the kernel, you'll often find reduced register usage by moving the creation and assignment close to the usage. The compiler may then be able to use a single register for all three variables, as they exist in distinct and disjoint phases of the kernel.

# Section summary

+   - Understand how thread layout impacts memory and cache access patterns.
+   - Use only multiples of 32 when specifying the thread count for kernel launch.
+   - Think about how to increase the amount of work performed per kernel fetch.
+   - Understand at least a little of how compilers work when optimizing code and adapt your source code to aid the compiler.
+   - Consider how branching within a warp can be avoided.
+   - Look at the PTX and final target code to ensure the compiler is not generating inefficient code. If it is, understand why and make changes at the source level to address it.
+   - Be aware and understand where data is being placed and what the compiler is telling you.