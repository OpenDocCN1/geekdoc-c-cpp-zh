Program
Before exchange: x = 100 y = 200
After exchange: x = 200 y = 100

# Fig. 11.11 Passing pointers as function parameters

+   1. The function parameters are declared as pointers.
+   2. The dereferenced pointers are used in the function body.
+   3. When the function is called, the addresses are passed as actual arguments.

```
copy(s1, s2)
{
char *s1, *s2;
while((*s1++ = *s2++) != '\0')
}
```

This copies the contents of s2 into the string s1. Parameters s1 and s2 are the pointers to character strings, whose initial values are passed from the calling function. For example, the calling statement copy(name1, name2); will assign the address of the first element of name1 to s1 and the address of the first element of name2 to s2.

Note that the value of *s2++ is the character that s2 pointed to before s2 was incremented. Due to the postfix ++, s2 is incremented only after the current value has been fetched. Similarly, s1 is incremented only after the assignment has been completed. Each assignment, after it has been copied, is compared with '0' and therefore copying is terminated as soon as the '0' is copied.

# Pointers to Pointers

A pointer to a pointer in C can be used to indirectly point to the memory address of a variable. A pointer to a variable is a pointer that contains the memory address of a variable. As a result, a pointer to a pointer contains the memory address of a pointer. In C, a pointer is a data type that points to the address where the value of a variable is stored in memory. Therefore, you can have a pointer to a pointer that points to the memory address of a pointer. In C, a pointer to a pointer can point to any type of pointer irrespective of the fact that the pointer is referencing an integer or character value. For example, you can create a pointer ptr2 pointing to a pointer, ptr1, which points to the memory address in which the value of 'Name' variable is stored as shown under:

```
ptr2
|
|
vptr1
|
|
vName variable

Address 7645 -> Address 7676 -> Address 8687 storing the value of Name variable
```

![](bbox=[0.05, 0.93, 0.95, 0.98])

# Fig. 11.12