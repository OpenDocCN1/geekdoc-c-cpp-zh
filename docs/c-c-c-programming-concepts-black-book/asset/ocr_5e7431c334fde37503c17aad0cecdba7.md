is required to allocate. In case, our requirement is clear at compile time, we could have used arrays and strings to handle it. However, even with arrays and strings, that is, with pre-allocated buffers, we overcommit our memory requirement, and most of the allocated buffers remain unused at runtime occupying primary memory storage.

As we know that, when the requirement is unknown till runtime, it is beneficial to use dynamic allocation. Consider an example, where a user inputs the number of questions he/she wants to enter into a system and then starts entering one by one. Now, let’s assume that each question is kept in a buffer during the program, as the user enters it. In this case, one way is to limit the question count to a MAX value, restrict the user from entering anything more than MAX, and declare an array of strings of MAX size to keep the questions. One biggest flaw with this approach is that if the user enters a lower number as question count, then during runtime, most of the program memory is wasted, as MAX number of buffers are pre-allocated but only few of them are used. The most elegant way to handle this situation is to use the dynamic memory management approach. In this approach, we wait till the user enters the number of questions and allocate the space based on the user’s input. Such situations can be handled and managed in C++. Although, both the functions of C, that is, calloc and malloc, are available and legal to use in C++, it also defines two unary operators **new** and **delete** that performs the task of allocating and deallocating the memory in a better and easier way at runtime. Let’s learn about these operators in detail.

The new operator is a unary operator that can be used to create objects of both predefined and custom defined data types. Let’s see how to use the new operator for dynamic memory allocation. Following is the basic syntax of using the new operator in C++:

```
Pointer_variable = new data_type;
```

In the preceding syntax, Pointer_variable is a pointer type variable of data type and a call to new data type returns the address of the newly created object or NULL, if sufficient amount of memory is not available. Consider the following example:

```
int *ptr;
ptr = new int;
```

In the preceding example, we have declared an integer pointer variable ptr and assigned a new memory location dynamically using the new operator. This operator points the pointer to the address of a memory location that can accommodate a member of size data type, which in this case is an integer variable. Alternatively, we can also combine the preceding two lines into a single line as follows:

```
int *ptr = new int;
*ptr = 5;                         //value is assigned to the newly created memory
*option
```

In the first line, we have created a pointer variable and assigned it to the address of a memory location created dynamically with the new operator. In the second line, we have assigned a value to it by accessing the storage cell at the address by indirection operator *ptr. Now, let’s learn about another variant of the new operator, where we can create and assign or rather initialize the new memory location with a value as follows:

```
int *ptr = new int (5); //value is assigned to the newly created memory location
```

The preceding code declares a pointer variable ptr of type integer and allocates a memory location in the main memory of the computer, pointed to by the pointer variable ptr and sets the newly allocated memory location with a value of 5.

Till now, we have learned to create a single memory location dynamically with the new operator and assigned it to a pointer variable of similar data type, where the data type can be either default or basic data types, or custom or user-defined data types. Now, let’s learn how to allocate a set of memory locations at the same time while using the new operator, which is shown as follows:

```
pointer_variable = new data_type [size];
or
int *arr = new int [10];          // creates a dynamic array of size 10 for storing
                                  // integers.
```