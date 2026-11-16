# Introduction to Pointers

A simple variable in a program is stored in a certain number of bytes at a particular memory location or address in the machine. For example, if `v` is a variable, then `v` is the address in memory of its stored value. In this context, the `&` is referred to as the *address-of* operator. When placed in front of any variable, it represents the address in memory of that variable. `&v` is therefore considered a constant.

A pointer variable is a variable holds the address of another variable. All pointer variables are typically the same size on any machine. Pointer variables can be declared in programs and then used to take addresses as values. For example:

```
int num;
int *ptr;
ptr = &num;

num is an integer variable
ptr is a pointer to integer variable
address of integer variable num is assigned to pointer variable ptr
```

The type specification identifies the type of the variable pointed to and the asterisk (*) identifies the variable itself as a pointer. Thus, the declaration:

```
int *ptr;
or
int* ptr;
```

says that `ptr` is a pointer variable and that the thing it points to, `*ptr`, is of type `int`.

As previously mentioned, the *address of operator*, `&`, when followed by a variable name, gives the address of that variable. `&num` is therefore the address in memory of the variable `num`.

The *indirection operator* (sometimes called the *dereference operator*), `*`, when followed by a pointer variable, gives the value stored at the pointed to address. It represents the thing being pointed to.