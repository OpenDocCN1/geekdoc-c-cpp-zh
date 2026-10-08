```
{
    printf("%.3f\n", p[r][cols-1]);
} else {
    printf("%.3f\n", p[r][cols-1]);
}
}
} else {
    // Matrix is empty
    printf("*\n");
}
}
```

We have made use of pointers in the Matrix class and we briefly discuss their implementation here but please note that a full explanation of pointers is beyond the scope of this book.

A pointer is an object; whose value refers to ('points to') another value stored elsewhere in memory using its address. A pointer references a location in memory, and obtaining the value stored at that location is known as dereferencing the pointer. Pointers to data significantly improve performance for repetitive operations such as traversing matrices. It is often much cheaper in time to copy and dereference pointers than it is to copy and access the data to the pointers point. Whenever a program needs to dynamically allocate memory, C++ provides the operators new and delete. Dynamic memory is allocated using the new operator and returns a pointer to the beginning of the new block of memory allocated, for example:

```
double *ptr; or
ptr = new double[5];
```

In the second case, the system dynamically allocates space for five elements of type double and returns a pointer to the first element of the sequence, which is assigned to ptr (a pointer). Therefore, ptr now points to a valid block of memory with space for five elements of type double. In Source 6.3, we have declared a pointer ptr as follows:

```
DBL** p;
```

This is in fact a double pointer. We have used a double pointer since we are dealing with dynamic 2D arrays. In essence we are saying; DBL** is a pointer to DBL* and