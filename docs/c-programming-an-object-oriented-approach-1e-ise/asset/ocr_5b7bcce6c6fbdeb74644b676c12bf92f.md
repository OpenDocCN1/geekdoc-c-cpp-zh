![](bbox=[0.298, 0.088, 0.853, 0.247])

**Figure 9.17** Increment and decrement operators apply to pointers

farther from the beginning of the array; subtraction creates a pointer closer to the beginning of the array. The red arrow shows the original pointer.

**Increment and Decrement** These two operators are designed to be used with variables (*values*). They cannot be used with the name of the array because the name is a constant value. The meaning of ptr++ is the same as ptr = ptr + 1, and the meaning of ptr-- is the same as ptr = ptr - 1. In these cases the original pointer moves as shown in Figure 9.17. After the increment operation, the original pointer is pointing to the arr[3]. After the decrement operation, it is pointing back to arr[2].

**Compound Addition and Subtraction** We can also use compound addition and subtraction operators on pointer variables. If *ptr* is a pointer variable, the expression (ptr += 3) is equivalent to (ptr = ptr + 3) and the expression (ptr -= 3) is equivalent to (ptr = ptr - 3). These operations, like the increment and decrement operators, move the pointer toward the beginning or toward the end, as shown in Figure 9.18.

**Pointer Subtraction** We can subtract one pointer from another. If *ptr1* and *ptr2* are pointers in which *ptr1* points to an element of a lower index and *ptr2* to an element of a higher index, then the expression (ptr2 - ptr1) returns a positive integer and (ptr1 - ptr2) returns a negative integer as shown in Figure 9.19. In other words, the results of these operations are integers, not pointers.

**No Pointer Addition** The addition of pointer values is not allowed in C++ because it does not make sense.

![](bbox=[0.304, 0.714, 0.87, 0.861])

**Figure 9.18** Compound addition and subtraction