However, the drawbacks of dynamic memory allocation for the two-dimensional array are to be followed:

+   - Extra memory space is required for storage of pointer array.
+   - Access to the individual array element is obtained only after the first level of indirect addressing.

# Pointers, Arrays and Strings

Sometimes we can use a pointer variable instead of an array. Suppose, a is declared as a one-dimensional array of integer and p is declared as a pointer to an integer.

```
int a[10];
```

we can write instead of the array

```
int *p;
```

Since p is not defined so p may contain a garbage value and p is not automatically allocated a block of a memory. Therefore, before the use of the pointer variable in the place of an array we need to allocate a memory for it.

# Example:

```
p = (int *)malloc(100*sizeof(int));
```

This statement allocates a memory block for 100 integer values.

# Example:

```
char *s;
scanf("%s",s); /* invalid */
or
char *s;
s = "Hello" /* invalid */
```

We should require allocating a block of memory before the use of pointer variable. Otherwise, it may display a runtime error like : -Segmentation fault".

# Example:

```
char *s;
s = (char*)malloc(10);
scanf("%s",s);
```

However in the case of array, memory block is allocated at compile time.

```
char t[10];
scanf("%s", t); /* valid */
```

but we cannot assign a value to a string variable

```
char t[10];
t = "Hello";
```

we should use the library function strcpy() to do this

# Example:

```
char t[10];
strcpy(t, "Hello");
```