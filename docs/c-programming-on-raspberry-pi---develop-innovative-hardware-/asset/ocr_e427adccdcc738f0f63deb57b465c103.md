```
~~~
b = *p;            // b = a
*p = *p + 2;       // a = a + 2
*p = *p * *p       // a = a * a
(*p)++;            // a++
~~~
```

# **Pointer arithmetic**

Pointers can be incremented, decremented, added, subtracted, or compared as shown in the following examples:

+   - `p++` — increment a pointer
+   - `p--;` — decrement a pointer
+   - `p = p + 10` — add value to a pointer
+   - `p1 = p1 + p2` — add two pointers
+   - `p = p - 5` — subtract value from a pointer
+   - `p1 = p1 - p2` — subtract two pointers

Strings can be created using character pointers as shown below. Here, pointer p has the address of the first character (R) of the string. Notice the string is automatically terminated with a NULL character:

```
~~~
char *p = "Raspberry Pi"
~~~
```

Examples of using pointers in C programs are given below.

# **Example 3.31**

Write a function to calculate the length of a string from the first principles using pointers.

# **Solution 3.31**

The required program listing is shown in Figure 3.59 (Program: **mystrlen.c**). Function **mystrlen** has one argument as a character pointer which points to the string of which the length is required. The contents of the string are compared to the string terminator (NULL character) and a count is incremented until the string terminator is found. The count is then returned to the calling program. The main program calls the function as shown in the figure

```
~~~
/*----------------------------------------
        STRING LENGTH
        =============

This program shows how a string length function can be
written using pointers and how this function can be used

Author: Dogan Ibrahim
File  : mystrlen.c
~~~
```