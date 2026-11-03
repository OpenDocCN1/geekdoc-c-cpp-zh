The following segment of a program allocates space for a structure variable:

```
```c
....
struct student
{
    char name[25];
    float age;
    long int id_num;
};
typedef struct student record;
record *st_ptr;
int class_size = 30;

st_ptr = (record *)calloc(class_size, sizeof(record));
....
```
```

record is of type struct student having three members: name, age and id_num. The calloc allocates memory to hold data for 30 such records. We must be sure that the requested memory has been allocated successfully before using the st_ptr. This may be done as follows:

```
```c
if(st_ptr == NULL)
{
    printf("Available memory not sufficient");
    exit(1);
}
```
```

# Releasing the Used Space

Compile-time storage of a variable is allocated and released by the system in accordance with its storage class. With the dynamic run-time allocation, it is our responsibility to release the space when it is not required. The release of storage space becomes important when the storage is limited.

When we no longer need the data we stored in a block of memory, and we do not intend to use that block for storing any other information, we may release that block of memory for future use, using the free function:

```
```c
free(ptr);
```
```

ptr is a pointer to a memory block which has already been created by malloc or calloc. Use of an invalid pointer in the call may create problems and cause system crash. The use of free function has been illustrated in Example 15.2.

# Altering the Size of a Block

It is likely that we discover later, the previously allocated memory is not sufficient and we need additional space for more elements. It is also possible that the memory allocated is much larger than necessary and we want to reduce it. In both the cases, we can change the memory size already allocated with