a problem, regardless of whether the language uses implicit or explicit deallocation. In the following sections, we investigate how language designers have dealt with the problems of dangling pointers and lost heap-dynamic variables.

# ### 6.11.4 Pointers in C and C++

In C and C++, pointers can be used in the same ways as addresses are used in assembly languages. This means they are extremely flexible but must be used with great care. This design offers no solutions to the dangling pointer or lost heap-dynamic variable problems. However, the fact that pointer arithmetic is possible in C and C++ makes their pointers more interesting than those of the other programming languages.

C and C++ pointers can point at any variable, regardless of where it is allocated. In fact, they can point anywhere in memory, whether there is a variable there or not, which is one of the dangers of such pointers.

In C and C++, the asterisk (*) denotes the dereferencing operation and the ampersand (&) denotes the operator for producing the address of a variable. For example, consider the following code:

```
~~~c
int *ptr;
int count, init;
. . .
ptr = &init;
count = *ptr;
~~~
```

The assignment to the variable ptr sets it to the address of init. The assignment to count dereferences ptr to produce the value at init, which is then assigned to count. So, the effect of the two assignment statements is to assign the value of init to count. Notice that the declaration of a pointer specifies its domain type.

Pointers can be assigned the address value of any variable of the correct domain type, or they can be assigned the constant zero, which is used for nil.

Pointer arithmetic is also possible in some restricted forms. For example, if ptr is a pointer variable that is declared to point at some variable of some data type, then

```
~~~
ptr + index
~~~
```

is a legal expression. The semantics of such an expression is as follows. Instead of simply adding the value of index to ptr, the value of index is first scaled by the size of the memory cell (in memory units) to which ptr is pointing (its base type). For example, if ptr points to a memory cell for a type that is four memory units in size, then index is multiplied by 4, and the result is added to ptr. The primary purpose of this sort of address arithmetic is array manipulation. The following discussion is related to single-dimensioned arrays only.