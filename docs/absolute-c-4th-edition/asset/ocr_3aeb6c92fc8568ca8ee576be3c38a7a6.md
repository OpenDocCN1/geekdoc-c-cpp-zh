# ## 10.2 Dynamic Arrays

In this section you will see that array variables are actually pointer variables. You will also find out how to write programs with dynamically allocated arrays. A **dynamically allocated array** (also called simply a **dynamic array**) is an array whose size is not specified when you write the program, but is determined while the program is running.

# ### ARRAY VARIABLES AND POINTER VARIABLES

Chapter 5 described how arrays are kept in memory. At that point we discussed arrays in terms of memory addresses. But a memory address is a pointer. So, in C++ an array variable is actually a kind of pointer variable that points to the first indexed variable of the array. Given the following two variable declarations, p and a are both pointer variables.

```
int a[10];
typedef int* IntPtr;
IntPtr p;
```

The fact that a and p are both pointer variables is illustrated in Display 10.6. Since a is a pointer that points to a variable of type int (namely, the variable a[0]), the value of a can be assigned to the pointer variable p as follows:

```
p = a;
```

After this assignment, p points to the same memory location that a points to. Thus, p[0], p[1], . . . p[9] refer to the indexed variables a[0], a[1], . . . a[9]. The square bracket notation you have been using for array variables to point to pointer variables as long as the pointer variable points to an array in memory. After the above assignment, you can treat the identifier p as if it were an array identifier. You can also treat the identifier a as if it were a pointer variable, but there is one important reservation: *You cannot change the pointer value in an array variable.* If the pointer variable p2 has a value, you might be tempted to think the following is legal, but it is not:

```
a = p2; //ILLEGAL. You cannot assign a different address to a.
```

The underlying reason why this assignment does not work is that an array variable is not of type int*, but its type is a constant version of int*. An array variable, like a, is a pointer variable with the modifier const, which means that its value cannot be changed.

(An array variable is actually more than an ordinary pointer variable since it carries some additional size information about the array, but an array variable does include a pointer to the array and the array variable can be assigned to a pointer variable. So, an array variable is a kind of pointer variable and can be treated like a pointer variable whose value cannot be changed.)