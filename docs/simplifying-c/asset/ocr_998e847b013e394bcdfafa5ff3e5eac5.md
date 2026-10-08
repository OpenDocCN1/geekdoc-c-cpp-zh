**Output 1:**

```
Enter a number: 5
Factorial of 5 is 120
```

**Output 2:**

```
Enter a number: -10
The number entered is zero or negative
```

It can be seen in Program 1 that we have defined a function factorial that takes as an input an integer value, and after processing, the input returns a long integer value. Observe that we have used variable `i_number` and `l_result` in both functions the main and the factorial. Before we proceed further, let us first understand how the memory is allocated to a C program at the time of execution. Figure 3 illustrates the memory allocation done to any C program at the time of execution:

![](bbox=[0.28, 0.36, 0.79, 0.62])

It can be seen in Figure 3 that the memory area is divided into five parts, each of them having specific purpose. The top part that contains environment variables and command line arguments (discussed later) is used by the operating system to control the execution of the C program. The stack segment is the area where the local variables of each functions are stored separately. A stack is a data structure that has a property called Last in First Out (LIFO). The discussion of the stack data structure is out of the scope of this book. The data segment has further three parts called initialized data segment, uninitialized data segment, and heaps. The initialized data and uninitialized data segment area is used to store the global or static data used in C program, while the heap is used for dynamic memory allocation (discussed in Chapter 14). The code segment contains the executable code of the C program.

Keeping the memory structure of Figure 3 in mind, the memory structure of execution of Program 1 is as shown in Figure 4: