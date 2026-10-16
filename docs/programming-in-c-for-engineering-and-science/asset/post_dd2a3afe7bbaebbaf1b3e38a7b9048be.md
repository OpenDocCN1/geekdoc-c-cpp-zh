
```cpp
int main()
{
    int i = 11,
        j = 22,
        k = 33;

    int * iPtr = &i;
    int * jPtr = &j;
    int * kPtr = &k;

    cout << "\nAt address " << iPtr
         << ", the value " << *iPtr << " is stored.\n"
         << "\nAt address " << jPtr
         << ", the value " << *jPtr << " is stored.\n"
         << "\nAt address " << kPtr
         << ", the value " << *kPtr << " is stored.\n";
}
```

# SAMPLE RUN:

At address 0xbffff970, the value 11 is stored.

At address 0xbffff96c, the value 22 is stored.

At address 0xbffff968, the value 33 is stored.

## 15.1.1 Declaring and Initializing Pointers

We begin with the second set of declarations in the program in Example 15.1:

```cpp
int * iPtr = &i;
int * jPtr = &j;
int * kPtr = &k;
```

There are two new items in these statements:

- 1. *An asterisk (*) following the type name in a declaration of the form*
  
      ```cpp
      type * variableName;
      ```
  
      declares that `variableName` can store the address of a memory location where a value of the specified `Type` is stored. Such variables are often called **pointer variables**, or simply pointers. Thus, the declarations
  
      ```cpp
      int * iPtr;
      int * jPtr;
      int * kPtr;
      ```

declare that iPtr, jPtr, and kPtr are pointer variables, each of which can store the address of a memory location where an int is stored. The type of each of these variables is int *.

2. The ampersand operator (&) can be used as a unary prefix operator on a variable name,

```
&variableName
```

that returns the address with which variableName is associated, so & is called the address-of operator. Thus, the expressions &i, &j, and &k return the addresses (or references³) associated with variables i, j, and k, respectively.

Combining these two pieces of information, we see that the declarations

```
int * iPtr = &i;
int * jPtr = &j;
int * kPtr = &k;
```

declare iPtr, jPtr, and kPtr as pointer variables, each of which can store the address of a memory location containing an int, and they initialize iPtr to the address of variable i, jPtr to the address of variable j, and kPtr to the address of variable k. In the sample run in Example 15.1, the address associated with variable i is the hexadecimal value 0xbffff970, the address of j is 0xbffff96c, and the address of k is 0xbffff968. We can visualize the layout of the program’s data in memory as follows:⁴

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_611_0.png)

It is important to remember that in a declaration, an asterisk operator * must precede each identifier that is to serve as a pointer. Thus,

```
double * ptr1,
    * ptr2;
```

is a correct declaration of ptr1 and ptr2 as pointers to doubles. Had we written

```
double * ptr1,
    ptr2;
```

> ¹ The word reference is used as a synonym for address. In fact, this is the origin of the phrase reference parameter—the value of a reference parameter is actually the address of its argument, rather than a copy of the argument.

> ¹ Note that (using hexadecimal arithmetic)
> 0xbffff970 - 0xbffff96c = 4
> and
> 0xbffff96c - 0xbffff968 = 4
> which indicates that the size of an int on this particular machine is 4 bytes (32 bits).

however, only ptr1 would be a pointer variable; ptr2 would be an ordinary double variable. To avoid making this mistake, we will normally use a separate declaration for each pointer variable:

```
double * ptr1;
double * ptr2;
```

### 15.1.1.1 Using typedef for Readability

An alternative notation that does not require the repeated use of the asterisk in pointer declarations is to use typedef to rename a type. For example, we could first declare

```
typedef int * IntPointer;
```

in Example 15.1 and then use IntPointer to declare the pointers:

```
IntPointer iPtr = &i,
    jPtr = &j,
    kPtr = &k;
```

Such declarations improve the readability of pointer declarations, especially when pointer parameters are being declared.

## 15.1.2 Basic Pointer Operations

C++ supports a variety of operations on pointers, including initialization, dereferencing, I/O, assignments, comparisons, and arithmetic. We examine each of these in turn.

### 15.1.2.1 Initialization

When a pointer variable is initialized to an address, as in

```
int * iPtr = &i;
```

that address must be the address of an object whose type is the same as the type to which the pointer points. The pointer is said to be bound to that type. For example, the declarations

```
double doubleVar;
int * iPtr = &doubleVar; // ERROR
```

will cause a compiler error, because an integer pointer can only store addresses of integer objects.

One important exception is that 0 can be assigned to any pointer variable. The value that results is called the null pointer value for that type and 0 is often called the null address. Thus, the declarations

```
char * cPtr = 0;
int * iPtr = 0;
double * dPtr = 0;
```

are all valid initializations using the null address.
The null address can also be used in a boolean expression to indicate whether or not a pointer is pointing to anything:

```
if (dPtr == 0)
    // dPtr is not currently pointing to anything
else
    // dPtr is pointing to a memory location
```

As we will see, such comparisons are especially important when pointers are used to store the addresses of blocks of memory allocated during execution.

### 15.1.2.2 Indirection and Dereferencing

Pointer variables not only store addresses but also provide access to the values stored at those addresses. An expression of the form

```
*pointerVariable
```

can be used to access the value at the address stored in pointerVariable. It can be thought of as going to the reference (address) stored in pointerVariable and accessing the value stored at that address. To illustrate, in the sample run of Example 15.1, the value of the expression

```
iPtr
```

is 0xbffff970, and the value of the expression

```
*iPtr
```

is 11, because 11 is the value stored at address 0xbffff970:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_613_0.png)

For the same reason, the values of the expressions *jPtr and *kPtr are 22 and 33, respectively. Thus, the value of variable i can be accessed via the expression *iPtr, the value of j via *jPtr, and the value of k via *kPtr. In general, the value of a variable v can be accessed indirectly by applying the * operator to a pointer variable vPtr whose value is the address of v. For this reason, the * operator is called the indirection operator. Because reference is another term for address and applying the indirection operator to a pointer variable accesses the value at the address stored in that pointer variable, applying the indirection operator to a pointer variable is called dereferencing that pointer variable.

We have already used this indirect access technique in earlier chapters. For example, in our study of vector<T> objects in Section 12.6, we saw that dereferencing an iterator

provides access to the value stored at the position in a vector<T> object to which the iterator points. Also, although we didn’t discuss it in our study of classes in the preceding chapter, each class object contains a pointer variable this whose value is the address of the object that contains it, and dereferencing this provides a way to (indirectly) access that object. We might picture this as follows:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_614_0.png)

The indirection operator can be applied more than once to produce additional levels of indirection. For example, the declarations

```
typedef int * IntPointer;    // or without using typedef:
IntPointer * ptr;            //     int ** ptr;
```

declare ptr to be a pointer to a memory location that contains a pointer to another memory location where an int can be stored.

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_614_1.png)

The indirection operator can be used on either side of an assignment statement. If the statement

```
i = *jPtr;
```

were added to the program in Example 15.1, the value of i would be changed from 11 to 22, because dereferencing jPtr produces the value 22 stored at address 0xbffff96c and this value would be assigned to i. The statement

```
*iPtr = j;
```

would produce the same result. *iPtr refers to the memory location with address 0xbffff970 and the assignment operator copies the value of j (22) into this memory location. Because this address is associated with the variable i, the effect is to change the value of i.

As noted earlier, the purpose of the program in Example 15.1 was to introduce the basics of pointers and indirection. Pointers are not often used to store addresses that are
