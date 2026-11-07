
might then run out of memory spaces for data manipulation, which would result in an abnormal termination of the program.

The question at hand is how to *avoid* memory leak. When a dynamic variable is no longer needed, it can be destroyed; that is, its memory can be deallocated. The C++ operator `delete` is used to destroy dynamic variables. The syntax to use the operator `delete` has two forms:

```cpp
delete pointerVariable;    //to deallocate a single
                           //dynamic variable
delete [] pointerVariable; //to deallocate a dynamically
                           //created array
```

Thus, given the declarations of the previous section, the statements

```cpp
delete p;
delete [] name;
delete str;
```

deallocate the memory spaces that the pointers p, name, and str point to.

Suppose p and name are pointer variables, as declared previously. Notice that an expression such as

```cpp
delete p;
```

or

```cpp
delete [] name;
```

only marks the memory spaces that these pointer variables point to as deallocated. Depending on the particular operating system, after these statements execute, these pointer variables may still contain the addresses of the deallocated memory spaces. In this case, we say that these pointers are **dangling**. Therefore, if later you access the memory spaces via these pointers without properly initializing them, depending on the particular system, either the program will access a wrong memory space, which may result in corrupting data now stored in those spaces, or the program may terminate with an error message. One way to avoid this pitfall is to set these pointers to `nullptr` after the `delete` operation. Also note that for the operator `delete` to work properly, the pointer must point to a valid memory space.

In Example 12-3, we used the pointer variable `radiusPtr` to access the memory location of the variable *radius*. However, in that example, the `radiusPtr` pointed to an existing memory, which was not created during program execution. In the following example, we illustrate how to use the `new` and `delete` operators to allocate and deallocate dynamic memory.

```cpp
cout << "Line 23: Value stored in radiusPtr: "
     << radiusPtr << endl;                         //Line 23
cout << "Line 24: Value stored in the memory "
     << "location to which radiusPtr is pointing: "
     << *radiusPtr << endl;                        //Line 24
cout << "Line 25: Value stored in lengthPtr: "
     << lengthPtr << endl;                         //Line 25

return 0;                                          //Line 26
}                                                  //Line 27
```

**Sample Run:** In this sample run, the user input is shaded.

```
Line 10: Enter the radius: 4.50

Line 13: Radius = 4.50, area = 63.62

Line 14: Address of radiusPtr: 0093F9A0
Line 15: Value stored in radiusPtr: 00DE0230
Line 16: Value stored in the memory location to which
         radiusPtr is pointing: 4.50
Line 20: Address of radiusPtr: 0093F9A0
Line 21: Value stored in radiusPtr: 00DE00A8
Line 22: Value stored in the memory location to which
         radiusPtr is pointing: 5.38
```

For the most part, the preceding program is the same as the program in Example 12-3. However, let us note the following: the statement in Line 9 allocates memory of type double and stores the address of the allocated memory in radiusPtr. The output of the statement in Line 15 shows that the address of the allocated memory is 00DE0230. The next statement in Line 17 deallocates the memory space to which radiusPtr is pointing. The statement in Line 20 allocates (another) memory space of type double and stores the address of the allocated memory space in radiusPtr, and the statement in Line 21 stores 5.38 in the allocated memory space. The statements in Lines 23 to 25 output the addresses as shown by the output. (Note that the addresses printed by this program are machine dependent. When you run this program on your machine, you are likely to get different values.)

## Operations on Pointer Variables

The operations that are allowed on pointer variables are the assignment and relational operations and some limited arithmetic operations. The value of one pointer variable can be assigned to another pointer variable of the same type.

For example, suppose that we have the following statements:

```cpp
int *p, *q;
```

The statement

```cpp
p = q;
```

copies the value of q into p. After this statement executes, both p and q point to the same memory location. Any changes made to *p automatically change the value of *q, and vice versa.

Two pointer variables of the same type can be compared for equality, and so on. The expression

```cpp
p == q
```

evaluates to true if p and q have the same value—that is, if they point to the same memory location. Similarly, the expression

```cpp
p != q
```

evaluates to true if p and q point to different memory locations.

Integer values can be added and subtracted from a pointer variable. The value of one pointer variable can be subtracted from another pointer variable. The arithmetic operations that are allowed differ from the arithmetic operations on numbers. First, let us use the following statements to explain the increment and decrement operations on pointer variables:

```cpp
int *p;
double *q;
char *chPtr;
studentType *stdPtr;    //studentType is as defined before
```

Recall that the size of the memory allocated for an int variable is 4 bytes, a double variable is 8 bytes, and a char variable is 1 byte. The memory allocated for a variable of type studentType is then 40 bytes.

The statement

```cpp
p++ or p = p + 1;
```

increments the value of p by 4 bytes because p is a pointer of type int. Similarly, the statements

```cpp
q++;
chPtr++;
```

increment the value of q by 8 bytes and the value of chPtr by 1 byte, respectively. The statement

```cpp
stdPtr++;
```

increments the value of stdPtr by 40 bytes.

The increment operator increments the value of a pointer variable by the size of the data type or structure to which it is pointing. Similarly, the decrement operator decrements the value of a pointer variable by the size of the data type or structure to which it is pointing.

Moreover, the statement

```cpp
p = p + 2;
```

increments the value of p (an `int` pointer) by 8 bytes.

Thus, when an integer is added to a pointer variable, the value of the pointer variable is incremented by the integer times the size of the data type or structure to which the pointer is pointing. Similarly, when an integer is subtracted from a pointer variable, the value of the pointer variable is decremented by the integer times the size of the data type or structure to which the pointer is pointing.

> **NOTE**
> 
> Pointer arithmetic can be very dangerous. Using pointer arithmetic, the program can accidentally access the memory locations of other variables and change their content without warning, leaving the programmer trying to find out what went wrong. If a pointer variable tries to access either the memory spaces of other variables or an illegal memory space, some systems might terminate the program with an appropriate error message. Always exercise extra care when doing pointer arithmetic.

## Dynamic Arrays

In Chapter 8, you learned how to declare and process arrays. The arrays discussed in Chapter 8 are called static arrays because their size was fixed at compile time. One of the limitations of a static array is that every time you execute the program, the size of the array is fixed, so it might not be possible to use the same array to process different data sets of the same type. One way to handle this limitation is to declare an array that is large enough to process a variety of data sets. However, if the array is very big and the data set is small, such a declaration would result in memory waste. On the other hand, it would be helpful if, during program execution, you could prompt the user to enter the size of the array and then create an array of the appropriate size. This approach is especially helpful if you cannot even guess the array size. In this section, you will learn how to create arrays during program execution and process such arrays.

An array created during the execution of a program is called a **dynamic array**. To create a dynamic array, we use the second form of the `new` operator.

The statement

```cpp
int *p;
```

declares p to be a pointer variable of type `int`. The statement

```cpp
p = new int[10];
```

allocates 10 contiguous memory locations, each of type `int`, and stores the address of the first memory location into p. In other words, the operator `new` creates an array of 10 components of type `int`, it returns the base address of the array, and the assignment operator stores the base address of the array into p. Thus, the statement
