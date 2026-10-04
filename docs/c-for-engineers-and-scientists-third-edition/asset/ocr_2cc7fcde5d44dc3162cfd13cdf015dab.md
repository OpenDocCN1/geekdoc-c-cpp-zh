# 668 Pointers

the variable whose address is stored in chrPoint. Figure 12.4 shows the relationship between the address contained in a pointer variable and the variable.

![](bbox=[0.225, 0.168, 0.773, 0.253])

Figure 12.4 Using a pointer variable

Although "d means the variable whose address is stored in d," it is commonly shortened to the statement "the variable pointed to by d." Similarly, referring to Figure 12.4, *y can be read as "the variable pointed to by y." The value's finally obtained, as shown in Figure 12.4, is qqqq.

When using a pointer variable, the value's finally obtained is always found by going to the pointer. The address contained in the pointer is then used to get the variable's contents. Certainly, this is a procedure rather indirect way of getting to the final value, so the indirect addressing is used to describe it.

Because using a pointer requires to a double loop (retrieving the address first, and then using the address to retrieve the actual data), you might wonder why you'd want to store an address in the first place. The answer lies in the intimate relationship between pointers and arrays and the ability of pointers to create and delete storage locations dynamically, as a program is running. Both topics are discussed later in this chapter. For now, however each variable has a memory address associated with it, the idea of storing an address shouldn't seem unusual.

# Declaring Pointers

Like all variables, pointers must be declared before they can be used to store an address. When you declare a pointer, C++ requires also specifying the type of variable that is pointed to. For example, if the address of the pointer numAddr is the address of an integer, this is the correct declaration for the pointer:

```
int *numAddr;
```

This declaration is read as "the variable pointed to by numAddr (from *numAddr in the declaration) is an integer." First, the variable pointed to by numAddr is an integer, and numAddr must be a pointer (because it is used with the indirection operator, *). Similarly, if the pointer tabPoint points to (contains the address of) a double-precision number and chrPoint points to a character variable, the required declarations for these pointers are as follows:

```
double *tabPoint;
char *chrPoint;
```

> *Pointer declarations can be written in the format type*pointerName, with a space between the indirection operator and the pointer name. This form, however, is not common because multiple pointers are declared in the same statement and the compiler might inadvertently decay the first pointer name. For example, the declaration int *num1, num2; declares num1 as a pointer variable and num2 as an integer. To accommodate multiple pointers in the same declaration and clearly mark each as a variable, this book adheres to the convention of placing an asterisk in front of each pointer name. This potential error rarely occurs with reference declarations because references are used almost exclusively as formal parameters, and single declarations are mandatory.