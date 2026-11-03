```
At end, type -999.
80 70 50 40 60 -999

40-->50-->60-->70-->80-->NULL

Input the list of number
At end, type -999
40 70 50 60 80 -999

40-->50-->60-->70-->80-->NULL
```

Fig. 15.32 Creation of sorted list from a given list of numbers

# Review Questions and Exercises

15.1 What is dynamic memory allocation? How does it help in building complex programs?

15.2 What is the principal difference between the functions malloc and calloc.

15.3 Find errors, if any, in the following memory management statements:

+   - (a) *ptr = (int *)malloc(m, sizeof(int));
+   - (b) table = (float *)calloc(100);
+   - (c) node = free(ptr);

15.4 Why is a linked list called a dynamic data structure? What are the advantages of using linked lists over arrays?

15.5 Describe different types of linked lists.

15.6 Identify errors, if any, in the following structure definition statements:

```
struct
{
    char name[30]
    struct *next;
};
typedef struct node;
```

15.7 The following code is defined in a header file list.h

```
typedef struct
{
    char name[15];
    int age;
    float weight;
} DATA;

struct linked_list
{
    DATA person;
    struct linked_list *next;
};

typedef struct_linked_list NODE;
typedef NODE *NDPTR;
```