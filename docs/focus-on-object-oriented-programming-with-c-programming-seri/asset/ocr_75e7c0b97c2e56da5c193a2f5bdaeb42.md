is determined at execution time. The return type is identical to a single instance, and the actual value returned is a pointer to the first element of the array.

For example:

```
int max 5;
char *p = new char[1]; // an array of one character
float* p = new float[max]; // an array of 5 floats
char** p = new char*[max]; // an array of 5 pointers to char
```

# The delete Keyword

The delete keyword in C++ is used to release the space that was reserved by new. It is analogous to the function free() in C, which takes as its one argument a pointer to the memory to be released. The content of the pointer itself is not modified by delete.

Note: You should not commingle C and C++ styles of dynamic memory allocation. That is, if you malloc() some storage, then you should free() it. Similarly, if you new some storage, then you should delete it. Do not use delete with malloc(), nor free() with new.

To delete a single instance from the heap (including a pointer), we use the keyword delete followed by the name of the pointer that points to the heap space.

For example:

```
int* ptr1 = new int;
int** ptr2 = new int*;
...
delete ptr1;
delete ptr2;
```

To delete an array of instances from the heap (including an array of pointers), we use the keyword delete followed by a pair of empty brackets and the name of the pointer variable.