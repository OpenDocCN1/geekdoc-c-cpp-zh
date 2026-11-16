# Chapter 18

# Memory Management

The C++ programming language provides many options to programmers when it comes to managing the memory used by an executing program. This chapter explores some of these frequently used options and introduces modern techniques aimed at reducing the memory management problems that have plagued C++ projects in the past.

# 18.1 Memory Available to C++ Programs

A modern operating system reserves a section of memory for an executing program. This allows the operating system to manage multiple program executions simultaneously. Different operating systems layout the memory of executing programs in different ways, but the layout will include the following four sections:

+   **Code.** The code section of memory holds the program's compiled executable instructions. The contents of the code section should never change while the program executes, and the size of the code segment does not change during the program's execution.

+   **Data.** The data section of memory contains global variables (see Section 10.1) and persistent local variables (`static` locals, see Section 10.2). The variables in the data section exist for the life of the executing program, but unless they are constants (see Section 3.6), the executing program may freely change their values. Even though the values stored in the variables found in the data segment may change during the program's execution, the size of the data segment does not change while the program executes. This is because the program's source code precisely defines the number of global and `static` local variables. The compiler can compute the exact size of the data segment.

+   **Heap.** The heap is where an executing program obtains dynamic memory. The `new` operator gets its memory from the heap, and `delete` returns previously allocated memory back to the heap. The size of the heap grows and shrinks during the program's execution as the program allocates and deallocates dynamic memory using `new` and `delete`.

+   **Stack.** The stack is where local variables and function parameters live. Space for local variables and parameters appears when a function is called and disappears when the function returns. The size of the stack grows and shrinks during the program's execution as various functions execute.

Operating systems generally limit the size of the stack. Deep recursion can consume a considerable amount of stack space. An improperly written recursive function, for example one that omits the base case