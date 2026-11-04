```
{
    printf("Code seg: %p\n", test);
    printf("Data seg: %p %p\n", &global, &st);
    printf("Stack seg: %p\n", &i);
    printf("Heap: %p\n", ptr);
}
    return 0;
}
void test(void)
{
}
```

Notice that this distribution model is a typical choice; each system may define its own. Moreover, each compiler may apply its own optimization policy. For example, the parameters of a function might be stored in system registers for faster access, not in the stack.

# Static Memory Allocation

In static allocation, the memory is allocated from the stack. The size of the allocated memory is fixed; we must specify its size when writing the program and it cannot change during program execution. For example, with the statement:

```
float grades[1000];
```

the compiler allocates 1000×4 = 4000 bytes to store the grades of 1000 students. The length of the array remains fixed; if we need to store grades for more students, we cannot change it during program execution. If the students proved to be less than 1000, memory is wasted. The only way to change the length of the array is to modify the program and compile it again.

Let’s discuss briefly what happens when a function is called. A detailed discussion is beyond the scope of this book. The compiler allocates memory in the stack to store the function’s data. As said, system registers might be used; for simplicity, we assume that the allocation occurs in the stack. For example, if the function returns a value, accepts parameters, and uses local variables, the compiler allocates memory to store:

+   a. The values of the parameters.
+   b. The local variables.
+   c. The return value.
+   d. The address of the next statement to be executed, when the function terminates.

When the function terminates, the following actions take place:

+   a. If the return value is assigned into a variable, it is extracted from the stack and stored into that variable.