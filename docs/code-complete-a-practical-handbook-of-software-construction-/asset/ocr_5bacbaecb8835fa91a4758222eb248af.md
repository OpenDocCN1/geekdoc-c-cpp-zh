Cross-Reference For more on checking input parameters, see Section 8.1, "Protecting Your Program from Invalid Inputs," and the rest of Chapter 8, "Defensive Programming."

# Check input parameters for validity

Another valuable form of initialization is checking input parameters for validity. Before you assign input values to anything, make sure the values are reasonable.

# Use a memory-access checker to check for bad pointers

In some operating systems, the operating-system code checks for invalid pointer references. In others, you're on your own. You don't have to stay on your own, however, because you can buy memory-access checkers that check your program's pointer operations.

# Initialize working memory at the beginning of your program

Initializing working memory to a known value helps to expose initialization problems. You can take any of several approaches:

+   - You can use a preprogram memory filler to fill the memory with a predictable value. The value 0 is good for some purposes because it ensures that uninitialized pointers point to low memory, making it relatively easy to detect them when they're used. On the Intel processors, 0xCC is a good value to use because it's the machine code for a breakpoint interrupt; if you are running code in a debugger and try to execute your data rather than your code, you'll be awash in breakpoints. Another virtue of the value 0xCC is that it's easy to recognize in memory dumps—and it's rarely used for legitimate reasons. Alternatively, Brian Kernighan and Rob Pike suggest using the constant 0xDEADBEEF as memory filler that's easy to recognize in a debugger (1999).
+   - If you're using a memory filler, you can change the value you use to fill the memory once in awhile. Shaking up the program sometimes uncovers problems that stay hidden if the environmental background never changes.
+   - You can have your program initialize its working memory at startup time. Whereas the purpose of using a preprogram memory filler is to expose defects, the purpose of this technique is to hide them. By filling working memory with the same value every time, you guarantee that your program won't be affected by random variations in the startup memory.

# 10.4 Scope

“Scope” is a way of thinking about a variable’s celebrity status: how famous is it? Scope, or visibility, refers to the extent to which your variables are known and can be referenced throughout a program. A variable with limited or small scope is known in only a small area of a program—a loop index used in only one small loop, for instance. A variable with large scope is known in many places in a program—a table of employee information that’s used throughout a program, for instance.

Different languages handle scope in different ways. In some primitive languages, all variables are global. You therefore don’t have any control over the scope of a variable,