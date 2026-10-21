# 4.5 THE OPERATOR NEW AND DELETE

When we declare variables, arrays, structure (in definition) etc., the memory for them is allocated at compile time. This allocation is static allocation. When you declare the array say int a[5] we give the size of array i.e., number of elements. We just cannot take input for x from user during program execution and declare the array by writing int a[x]. Memory for array in the above declaration is allocated at compile time so compiler requires the size of the array. The size once fixed cannot be changed during the program execution. This may sometimes results in wastage of memory when size specified in the beginning is more than actually used in the program.

When you write your C++ program, the program’s data and code is stored in the RAM. All the local and global variables used in the program are stored in a fixed area of memory allocated to that program. This are allocated is fixed and remain constant during the execution of the program. The local variable are always stored on the stack and are destroyed automatically as soon as control goes out of scope. Global and static variables are known as load time variables they come into existence at the time of loading of the program. Thus, we can say that global and local variables are efficiently handled by C++ compiler. But the programmer must know the amount of space required for every program.

The technique through which a program can obtain space in the RAM during the execution of the program and not during compilation is called dynamic memory allocation. In this method space for the variables (array, strings, structure etc) is allocated from a free memory region which is known as heap. This area is not fixed in nature and keep changing as the memory is allocated and de-allocated from this region. The entire run time view of memory for a program is given below.

Dynamic memory allocation is the allocation of memory at run time i.e., when program executes then required memory is asked from the user and memory is allocated with the help of operator new.

![](bbox=[0.429, 0.606, 0.571, 0.815])

**Figure 4.1.** *Run time memory area of a C++ program*