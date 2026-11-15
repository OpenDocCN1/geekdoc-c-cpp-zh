
![](img/02c4582f051c5b51776411c92b079035_386_0.png)

### Figure 7.12 Push and pop operations.

![](img/02c4582f051c5b51776411c92b079035_386_1.png)

### Figure 7.13 Implementation of a stack using a linked list.

## Binary tree.

The final dynamic data structure that we present is a binary tree. A binary tree is a data structure that begins with a single node, often called the root of the tree. This node has a left branch and a right branch. The node at each branch also has a left branch and a right branch. The overall structure of a binary tree is shown in Figure 7.16.

Binary trees are especially useful in certain types of searches. For example, assume that the data stored in a tree are ordered, and the smaller values are always on the left, with the
![](img/02c4582f051c5b51776411c92b079035_387_0.png)
![](img/02c4582f051c5b51776411c92b079035_387_1.png)
![](img/02c4582f051c5b51776411c92b079035_387_2.png)
![](img/02c4582f051c5b51776411c92b079035_387_3.png)
larger values always on the right. Thus, the algorithm to determine whether a particular value is in the list is very efficient. We first compare the root to the value for which we are searching. The results of the comparison immediately determine which half of the tree must be searched. The comparison in the first branch of the correct half of the tree reduces the search to one-fourth of the tree and so on. This process can be illustrated using Figure 7.17. Suppose we wish to determine if the number 189 is contained in the tree. We begin with the root node. Since 189 is greater than 157, we know we must search the right branch. The first right
![](img/02c4582f051c5b51776411c92b079035_388_0.png)
branch contains the value 208, which is greater than the number 189. We thus take the left branch at the value 208. The branch value 179 represents the end of the branch, and we now know that the value 189 is not in the tree. If we wanted to insert it in the tree, we are now at the correct position to perform the insertion.

The routines to search a tree and to add and delete nodes in the tree require the use of the root position and the left and right links. The implementation of the tree using a linked data structure can be performed as shown in Figure 7.18.

## SUMMARY

Structures provide a convenient way to define a collection of data values that may or may not be of the same data type. Several examples illustrated how structures are used in C programs. Dynamic data structures were introduced and an algorithm for implementing a linked list was presented. Other dynamic structures were discussed, including circularly linked lists, doubly linked lists, queues, stacks, and trees.

## KEY TERMS

- binary tree
- circularly linked list
- data member
- doubly linked list
- dynamic data structures
- empty list
- FIFO structure
- head
- LIFO structure
- linked list
- node
- pointer operator
- queue
- stack
- structure
- structure member operator
- tag

## C STATEMENT SUMMARY

Structure definition:

```c
struct tsunami
{
    int mo, da, yr, fatalities;
    double max_height;
    char location[20];
};
```

```c
struct node
{
 int data;
 struct node *link;
};
```

Structure declaration:

```c
struct tsunami t1;
struct node n1, n2={2,NULL};
```

Accessing members:

```c
t1.mo = 10;
n1.link = &n2;
```

Arrays of structures:

```c
struct tsunami t2[100];
```

![](img/02c4582f051c5b51776411c92b079035_389_0.png)

## NOTES

- 1. Structure definitions are often included in .h files outside of main.

![](img/02c4582f051c5b51776411c92b079035_389_1.png)

## DEBUGGING NOTES

- 1. A structure definition does not allocate memory. To allocate memory, a variable must be declared after the structure has been defined.
- 2. The structure member operator must be used with the name of the structure variable to reference individual data members.
- 3. The name of the structure variable without the structure member operator refers to the entire structure.
- 4. The relational operators cannot be used on an entire structure.

## PROBLEMS

### SHORT-ANSWER PROBLEMS

### True-False Problems

Indicate if the following statements are true (T) or false (F).

- 1. It is possible for a structure to have data members of different data types. T F
- 2. To reference a data member of a structure, use the name of the structure followed by parentheses and an offset. T F
- 3. To print the values of all four data members of the structure r1, use the following statement: T F

```c
printf("The values of r1 are: %f %f %f %f \n",r1);
```

- 4. The structure member operator is used with the name of a structure to reference a data member of a structure. T F

- 5. The pointer operator is used with a pointer to a structure to access the data members of a structure. T F

### Multiple Choice Problems

Use the following structure definition to answer Problems 6 through 10:

```c
struct computer
{
    char manufacturer[10];
    double price;
    int speed;
};
struct computer pc1, pc2;
```

- 6. The correct function header to input values for the structure pc1 is
  (a) void get_pc(computer pc1);
  (b) void get_pc(struct computer pc1);
  (c) void get_pc(struct computer *pc1);
  (d) void get_pc(struct *pc1);
  (e) void get_pc(computer *pc1);

- 7. The correct function header to print the value of the structure pc1 is
  (a) void print_pc(computer pc1);
  (b) void print_pc(struct computer pc1);
  (c) void print_pc(struct computer.pc1);
  (d) void print_pc(struct *pc1);

- 8. The correct statement to assign a value of $800 to the data member price in the structure pc1 is
  (a) struct price = 800;
  (b) struct computer.price = 800;
  (c) struct pc1->price = 800;
  (d) pc1.price = 800;
  (e) pc1->price = 800;

- 9. The correct set of statements to define a pointer to the structure pc1 is
  (a) struct computer pc1, *ptr_pc1;
     ...
     pc1 = ptr_pc1;
  (b) struct computer pc1, *ptr_pc1;
     ...
     ptr_pc1 = pc1;
  (c) struct computer pc1, *ptr_pc1;
     ...
     ptr_pc1 = &pc1;
  (d) struct computer pc1, *ptr_pc1;
     ...
     ptr_pc1 = *pc1;

### Memory Snapshot Problem

Use the following structure definition to answer Problems 10 through 13:

```c
struct date
{
int month, day, year;
};
```

Give the corresponding snapshot of memory for the structures start_date and end_date; assume that each statement builds on the previous statements.

```c
struct date start_date, end_date;
```

- 10. struct date start_date, end_date;
- 11. start_date.month = 9;
- 12. start_date.year = 2005;
    end_date.year = start_date.year + 3;
- 13. if (end_date.month < 7)
    end_date.day = 1;
    else
    end_date.day = 30;

### PROGRAMMING PROBLEMS

### Hurricanes.

In this chapter, we defined a structure that can be used to represent information for hurricanes.

```c
struct hurricane
{
char name[20];
int year, category;
};
```

These problems refer to the file storms2.txt, which contains information for the strongest hurricanes in the United States during 1950 to 2002. Note that the information in the file is ordered by year:

- 14. Write a program to read the information in storms2.txt. Use the preceding structure and print a report with the average category of these hurricanes. Use an output format similar to the following:

```
Hurricane Summary for Strongest Hurricanes in 1950–2002
Average Category: xx.x
```

Note: You do not need an array to solve this problem.

- 15. Write a program to read the information in storms2.txt. Use the preceding structure and print the number of hurricanes in each category. Use an output format similar to the following:

```
Hurricane Summary for Strongest Hurricanes in 1950–2002
Category Hurricanes
1 x
2 x
3 x
```

Note: You do not need an array to solve this problem.

- 16. Write a program to read the information in storms2.txt. Use the preceding structure and print the information for the hurricanes that occurred between 1960 and 1969. Use an output format similar to the following:
Strongest Hurricanes between 1960 and 1969
Name Year Category
Note: You do not need an array to solve this problem.

- 17. Write a program to read the information in storms2.txt. Use the preceding structure and print the information for the hurricanes that occurred between two years entered by the user. Use an output format similar to the following:
Hurricane Summary for Strongest Hurricanes between x and x
Name Year Category
Note: You do not need an array to solve this problem.

- 18. Write a program to read the information in storms2.txt. Use the preceding structure and print the information for the hurricanes such that you first print the information for category 5 hurricanes, then the information for category 4 hurricanes, and so on.
Strongest Hurricanes between 1950 and 2002
Category Number of Hurricanes
Instead of sorting the information in the file, read it into an array and then make multiple passes through the array.

- 19. Write a program to read the information in storms2.txt. Use the preceding structure and print the hurricane names in alphabetical order:
Strongest Hurricanes between 1950 and 2002
Hurricane Name
You may want to review the sections on sorting data in arrays (Chapter 5).

- 20. Write a program to read the information in storms2.txt. Use the preceding structure and print the hurricane names in alphabetical order, along with the other information:
Strongest Hurricanes between 1950 and 2002
Hurricane Year Category
Hint: First solve the problem presented in Problem 19. Then modify the program so that each time you switch values in the hurricane name array, you do the same switches in the year array and the category array.

**Tsunamis.** In this chapter, we defined a structure that can be used to represent information for tsunamis:

```c
struct tsunami
{
    int mo, da, yr, fatalities;
    double max_height;
    char location[20];
};
```
