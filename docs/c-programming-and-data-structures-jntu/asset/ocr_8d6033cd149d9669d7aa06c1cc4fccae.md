# Syntax:-

```
Ptr=(cast-type*)malloc(byte size);
```

Ptr- pointer of cast type.

Malloc returns a pointer (of cast type) to an area of memory with the size of given bytes.

Example: - y=(int*)malloc(100*size of(int));

Malloc allocates a block of contiguous bytes. The allocation can fail if the space in the heap is not sufficient. If it fails, it returns null.

Example program that uses a table of integers whose size will be specified interactively at run time.

```
#include<stdio.h>
#define null 0
Main()
{
int *p,*table;
int size;
printf("enter size of table");
scanf("%d", &size);
printf("\n");
if (table=(int*)malloc(size*size of (int))==null)
{
printf("no space available");
exit(1);
}
printf("address of first byte is %u",table);
printf("input table values");
for(p=table;p<table+size;p++)
scanf("%d",&p);
for(p=table+size-1;p>=table;p--)
Printf("%d is stored address %u",*p,p);
}
```

# Memory allocation using calloc() function:-

Calloc() is another memory allocation function that is normally used for requesting memory space at run time for storing derived data types such as arrays and structures. Malloc allocates a single block of storage, each of them, being of the same size, and then sets all bytes to zero.

The general form of calloc() is

```
Ptr=(cast_type*)calloc(n, elem_size);
```

The above statement allocates contiguous space for n blocks, each of size elem_size bytes. All bytes are initialized to zero and a pointer to first byte of the allocated region is returned. If there is not enough space a null pointer is returned. Calloc() allocates blocks of memory.