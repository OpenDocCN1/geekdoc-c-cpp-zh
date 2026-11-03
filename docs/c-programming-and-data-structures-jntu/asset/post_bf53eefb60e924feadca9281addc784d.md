
```
product->quantity);
Output
Type filename:INVENTORY
Item name:XXX
Item number:444
Item price:40.50
Quantity:34
Item XXX appended.
Do you want to add another item(1 for YES/0 for NO)?1
Item name:YYY
Item number:555
Item price:50.50
Quantity:45
Item YYY appended.
Do you want to add another item(1 for YES/0 for NO)?0
AAA-1 111 17.50 115
BBB-2 125 36.00 75
C-3 247 31.75 104
XXX 444 40.50 34
YYY 555 50.50 45
```

Fig. 13.7 Adding items to an existing file

## Review Questions and Exercises

- 13.1 Describe the use and limitations of the functions getc and putc.
- 13.2 What is the significance of EOF?
- 13.3 When a program is terminated, all the files used by it are automatically closed. Why is it then necessary to close a file during execution of the program?
- 13.4 Distinguish between the following functions:
  - (a) getc and getchar
  - (b) printf and fprintf.
  - (c) feof and ferror.
- 13.5 How does an append mode differ from a write mode?
- 13.6 What are the common uses of rewind and ftell functions?
- 13.7 Explain the general format of fseek function?
- 13.8 What is the difference between the statements rewind(fp); and fseek(fp, 0L, 0);?
- 13.9 Write a program to copy the contents of one file into another.
- 13.10 Two files DATA1 and DATA2 contain sorted lists of integers. Write a program to produce a third file DATA which holds a single sorted, merged list of these two lists. Use command line arguments to specify the file names.
- 13.11 Write a program that will generate a data file containing the list of customers and their corresponding telephone numbers. Use a structure variable to store the name and telephone of each customer. Create a data file using a sample list.
- 13.12 Write an interactive, menu-driven program that will access the data file created in the above problem and do one of the following tasks:
  - (a) Determine the telephone number of a specified customer.
  - (b) Determine the customer whose telephone number is specified.

## UNIT VI

## Chapter 14

## Data Structures

### 14.1 INTRODUCTION TO DATA STRUCTURES

In the field of computing, we have formulated many ways to handle data efficiently. So far, we have seen how to use variables to store data. However, variables are not feasible when handling a huge amount of data.

Consider a situation when we want to access information, such as student name, roll no, section name, sex, address, subjects, and marks obtained in each subject for students in a specific state of the country. With a single variable, it is an unfeasible task to store such a large amount of related data. Also, we need an organized medium of storage to handle any correlated information. Thus, the concept of data structure is introduced.

Data structure is a collection of organized data that are related to each other. Data structures can be classified into two types:

- Linear data structure
- Non-linear data structure

The linear data structures, such as array and list, and non-linear data structures, such as trees and graphs, are most popularly known data structures.

As we have seen earlier, an array is used to store data in consecutive memory locations. Arrays are considered as a good example for implementing simple data structures. Arrays can be effectively used for random access of fixed amount of data. We can also use arrays to create data structures, such as stack and queue. Stacks and queues are usually known as linear data structures, because data items in stacks and queues are arranged in a linear sequence.

### 14.2 STACKS

A stack is a linear data structure in which a data item is inserted and deleted at one end. A stack is called a Last In First Out (LIFO) structure because the data item that is inserted last into the stack is the first data item to be deleted from the stack. To understand this, imagine a pile of books. Usually, we pick up the topmost book from the pile. Similarly, the topmost item (i.e. the item which made the entry last) is the first one to be picked up/removed from the stack.

Stacks are extensively used in computer applications. Their most notable use is in system software (such as compilers, operating systems, etc.). For example, when one C function calls another function, and passes some parameters, these parameters are passed using the stack. In fact, even many compilers store the local variables inside a function on the stack.

In general, writing a value to the stack is called as a push operation, whereas reading a value from it is called as a pop operation. Like in the case of queues, a pop (i.e. read) operation in the case of a stack is also destructive. That is, once an item is popped from the stack, it is no longer available.

Figure 14.1 specifies what happens when the push and pop operations get executed. Note how the new items get added to the end of the stack, and also how elements get removed from there. We assume that initially the stack is empty.

| Operation | Contents of the stack after the operation |
|---|---|
| Push (A) | A |
| Push (B) | A B |
| Pop | A |
| Push (C) | A C |
| Push (D) | A C D |
| Push (E) | A C D E |
| Pop | A C D |
| Pop | A C |
| Pop | A |
| Pop | Empty |

Fig. 14.1 How a stack works

A typical implementation of the push and pop operations of a stack is shown in Fig. 14.2. As shown, the push operation checks if there is still some room left in the stack, and if there is any, it adds the received item to the top of the stack, and increments the stack counter by one. Similarly, the pop operation decrements the stack counter by one to see if stack is empty. If not, it returns the top of the stack.

Also note that we have implemented the stack as an array. Instead, it can be implemented using the dynamic memory management techniques. The variable top indicates the current top of the stack, and it moves up and down dynamically, depending on whether new items are added to the stack, or existing items are removed.

```c
#define MAX 100
int stack[MAX];

int top = 0;  /* indicates the top of the stack */

/* write an item to the stack */
void push (int t)
{
    if (top >= MAX)
    {
        printf("Stack is already full. Cannot add more items.\n");
        return;
    }

    stack[top] = t;
    top++;
}

/* read the topmost item from the stack */
int pop(void)
{
    top--;
    if (top < 0)
    {
        printf("Stack is already empty. No items to read.\n");
        return;
    }
    return stack[top];
}
```

Fig. 14.2 Push and pop operations of a stack

For a real-life use of stacks, imagine a magazines library. New magazines keep arriving in the library, and keep getting registered. Whenever a member walks in, she asks for the latest magazine that is available. The librarian takes a look at the topmost magazine, and offers it to the member. As and when any magazine is issued to a member, it is removed from the list of the available magazines. Of course, to keep things simple, we shall ignore the cases where the members do not want the latest magazine, but want something else. A stack best implements this arrangement. The program for this is listed in Fig. 14.3.

```c
#include <stdio.h>
#include <string.h>

/* Global variables */
char magazines[1000][1000];    /* library can have 1000 magazines at the most at a time */
int top = 0;                   /* indicates the top of the stack */

/* function declarations */
void push(void);
void pop(void);

void main(void)
{
    int ch = 0;

    while (1)
    {
        printf("\n\n Main Menu \n");
        printf("1. Add new magazine\n");
        printf("2. Issue the latest magazine\n");
        printf("3. Quit\n");
        printf("Your choice: ");
        scanf("%d", &ch);

        switch (ch)
        {
            case 1: push(); break;
            case 2: pop(); break;
            case 3: return;
        }
    }
}
```

Fig. 14.3 Magazines library implemented as a stack—Part I

```c
/* add a new magazine to the top of the stack */
void push (void)
{
    if (top >= 1000)
    {
        printf("Stack is already full. Cannot add more magazines.\n");
        return;
    }

    printf("Magazine details:\n");
    gets(magazines[top]);

    if (!magazines[top])
        return;
    top++;
}

/* issue the topmost magazine from the stack */
void pop (void)
{
    top--;
    if (top < 0)
    {
        printf("Stack is already empty. No magazines to issue.\n");
        return;
    }

    printf("Issuing magazine: %s", magazines[top]);
}
```

Fig. 14.3 Magazines library implemented as a stack—Part II

### 14.3 QUEUES

A queue is very similar to the way we (are supposed to) queue up at train reservation counters or at bank cashiers' desks. A queue is a linear, sequential list of items that are accessed in the order First In First Out (FIFO). That is, the first item inserted in a queue is also the first one to be accessed, the second item inserted in a queue is also the second one to be accessed, and the last one to be inserted is also the last one to be accessed. We cannot store/access the items in a queue arbitrarily or in any random fashion.

Suppose that we are creating a queue of items. For this purpose, let us assume two very simple functions, write and read. The write function adds a new item to the queue, whereas the read function reads one item from the queue. If we go on operating with these two functions with a few insertions and a few retrievals, the resulting values of the queue would look as shown in Fig. 14.4.

| Operation | Contents of the queue |
|---|---|
| write (a) | a |
| write (b) | a b |
| write (c) | a b c |
| read (returns a) | b c |
| write (d) | b c d |
| read (returns b) | c d |
| read (returns c) | d |
| write (e) | d e |

Fig. 14.4 Queue operations
