```
printf("\n NAME : ");
gets(ptr->name);
printf("\n COURSE : ");
gets(ptr->course);
printf("\n FEES : ");
scanf("%d", &ptr->fees);
display(ptr);
getch();
return 0;
}
void display(struct student *ptr)
{
    printf("\n DETAILS OF STUDENT");
    printf("\n ROLL NO. = %d", ptr->r_no);
    printf("\n NAME = %s", ptr->name);
    printf("\n COURSE = %s", ptr->course);
    printf("\n FEES = %d", ptr->fees);
}
```

Output
Enter the data for the student
ROLL NO. = 01
NAME: Rahul
COURSE = BCA
FEES: 45000
DETAILS OF STUDENT
ROLL NO. = 01
NAME = Rahul
COURSE = BCA
FEES = 45000

# 5.5 SELF-REFERENTIAL STRUCTURES

Self-referential structures are those structures that contain a reference to the data of its same type. That is, a self-referential structure, in addition to other data, contains a pointer to a data that is of the same type as that of the structure. For example, consider the structure node given below.

```
struct node
{
    int val;
    struct node *next;
};
```

Here, the structure node will contain two types of data: an integer val and a pointer next. You must be wondering why we need such a structure. Actually, self-referential structure is the foundation of other data structures. We will be using them throughout this book and their purpose will be clearer to you when we discuss linked lists, trees, and graphs.

# 5.6 UNIONS

Similar to structures, a union is a collection of variables of different data types. The only difference between a structure and a union is that in case of unions, you can only store information in one field at any one time. To better understand a union, think of it as a chunk of memory that is used to store variables of different types. When a new value is assigned to a field, the existing data is replaced with the new data.

Thus, unions are used to save memory. They are useful for applications that involve multiple members, where values need not be assigned to all the members at any one time.