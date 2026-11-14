+   7.20 How many data variables can be returned through a function's return-type variable?

+   7.21 How can we return multiple variables of the same type from a function?

+   7.22 How can we return multiple variables of different types from a function?

+   7.23 How can we return multiple variables of different types from a function if the return type is void (not void*)?

+   7.24 When a pointer to a local variable that was declared in a called function is returned to the calling function, can that pointer be dereferenced in the calling function? Explain why or why not? If the pointer can be dereferenced, will the result be the value of the local variable.

+   7.25 To what memory address does control flow return to when the function is complete - the address that it was at when the function call occurred, the address following, or the address preceding?

# Pointers to Functions

+   7.26 Are the following declarations equivalent? Why or why not?

```
int (*myFunction)(char val0, int val1);
int *myFunction(char val0, int val1);
```

+   7.27 Can a pointer to a function be passed as an argument into a function?

+   7.28 Should a pointer to a function be initialized? If so, what should value be? If not, why not?

+   7.29 Pointers support several different arithmetic operations such as the addition of a scalar to the pointer. Are these operations supported on a pointer to a function? If so, please explain the results of applying each such operation.

# Structures

+   7.30 How can we include a function in a struct?

+   7.31 Can a struct have more than one function member?

+   7.32 Can we declare an array of structs? Are there any constraints?

+   7.33 Can we compare structs using the == operator? If not, why not?

+   7.34 Can we assign one struct to another using the = operator? If not why not?

# 7.11 PROBLEMS

# Bit Manipulation

Using the bit manipulation operators, develop and test C programs to perform the following.

+   7.35 Why is including arrays in a struct data type ill advised in an embedded C program if an instance of that struct may be passed as an argument to a function?

+   7.36 Can one declare an array of structs in which the data members for each struct are of different types; for example, one struct containing ints, a second floats, and a third chars? If not, why not and if so, how?

+   7.37 Can one declare an array of structs containing both data and function members in which the struct members in each struct are of different types? If not, why not and if so, how?

# Interrupts

+   7.38 If an interrupt service routine is not assigned to a particular interrupt and the interrupt occurs, what will happen?

+   7.39 Identify and describe each of the steps involved in handling an interrupt. Be specific about any registers, data structures, or addresses that may be involved. How can we return several values, of different types, from a function?

+   7.40 Why do interrupt service routines typically accept no arguments and have no return value?

+   7.41 Describe the structure and contents of a typical interrupt vector table.

+   7.42 To what memory address does control flow return to when the interrupt is complete: the address that it was at when the interrupt occurred, the address following, or the address preceding?

+   7.43 An interrupt may be enabled or disabled under program control. Why do we wish to be able to do such a thing?

+   7.44 If interrupts have been disabled, will the interrupts still occur? Please explain your answer.

+   7.45 What are some of the possible side effects of disabling interrupt?

+   7.46 An interrupt may be masked under program control. How is masking different from disabling?

+   7.47 Under what circumstances might we wish to mask versus disable an interrupt? Explain your answer.

+   7.48 If interrupts have been masked, will the interrupts still occur? Explain your answer.

+   7.49 Some interrupts are said to be nonmaskable. What might this mean, and why might we wish to so designate certain interrupts?

+   7.50 Give some examples of situations under which we would want to preclude interrupt masking.

+   7.1 Starting with the word 0xF0A6, reset bit 3, set bit 6, set bit 8, reset bit 13.

+   7.2 Starting with the word 0xCB43, determine if the word contains the pattern 0x43 in the least significant byte.