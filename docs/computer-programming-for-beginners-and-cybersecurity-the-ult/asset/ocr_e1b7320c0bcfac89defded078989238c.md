To create a pointer, we use the dereferencing operator (*), this will create a pointer variable that is designed to hold a memory locations address. Below is a program that creates a pointer and uses reference operator (&) to store another regular variable's address in the newly created pointer. The dereferencing operator (*) is also used to access or change the actual data in that memory location.

+   - Dereferencing operator (*) is used to create a pointer, it is also used when changing the actual value
+   - Referencing operator (&) is used when obtaining the memory location of a pointer

Must be in increase indent.

```
```c
//Regular variable

int var = 10;

//Pointer
int* pointer;

//Storing of var memory location
pointer = &var;

//Pointer is now effecivly 'var' so
//things like this can happen
*pointer = 20;

printf("Var's value is now: %d", var);
```
```

Output:

> >Var's value is now: 20

# ## NULL pointers

When you create a pointer, is it initially not given anything to point at, this is dangerous because the pointer when created it references random memory, and changing this data in the memory location can