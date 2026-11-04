
/* Store the string in the allocated memory. */
strcpy(ptr[i], str);
/* We compare the length of each string against max_len and
if a longer string is found, we store its position and length. */
if (len > max_len)
{
    pos = i;
    max_len = len;
}
printf("Longer string: %s\n", ptr[pos]);
for(i = 0; i < SIZE; i++)
    free(ptr[i]);
return 0;
}

**Comments:** This method of handling the strings is more efficient than the one presented in C.10.37. There is no waste of memory.

## C.14.9 Write a program that reads its command line arguments and allocates memory to store their characters in reverse order. For example, if the arguments are next and time, the program should store into the memory txen and emit.

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(int argc, char *argv[])
{
    char *rvs_str;
    int i, j, len;
    if(argc == 1)
    {
        printf("Missing string arguments ...\n");
        exit(EXIT_FAILURE);
    }
    for(i = 1; i < argc; i++)
    {
        len = strlen(argv[i]);
        rvs_str = (char*) malloc(len+1); /* Allocate one extra place for the null character. */
        if(rvs_str == NULL)
        {
            printf("Error: Not available memory\n");
            exit(EXIT_FAILURE);
        }
        for(j = 0; j < len; j++)
            rvs_str[j] = argv[i][len-1-j]; /* The last character is stored in position len-1. */
        rvs_str[j] = '\0'; /* Terminate the string. */
        printf("Reverse of %s is: %s\n", argv[i], rvs_str);
    }
free(rvs_str);
}
return 0;
}
```

## C.14.10

Define the structure type publisher with members: name, address, and phone number. Then, define the structure type book with members: title, author, field, code, price, and a pointer to a structure type publisher. Besides price, all other members must be pointers. Assume that the maximum text length is 100 characters. Write a program that reads the number of books and allocates memory to store their data and the data of the publishers as well. Then, the program should read a book's code and display its title and the name of its publisher, if registered.

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int read_text(char str[], int size, int flag);

typedef struct /* Let's remember typedef. */
{
    char *name;
    char *addr;
    char *phone;
} pub;

typedef struct
{
    char *title;
    char *auth;
    char *code;
    pub  *pub_ptr;
    float prc;
} book;

/* To save space, we assume that all malloc() calls are successful. */
int main(void)
{
    book *books_ptr;
    char str[100];
    int i, num, len;

    printf("Enter number of books: ");
    scanf("%d", &num);
    getchar();

    books_ptr = (book*) malloc(num * sizeof(book));
    for(i = 0; i < num; i++)
    {
        printf("\nTitle: ");
        len = read_text(str, sizeof(str), 1);
        books_ptr[i].title = (char*) malloc(len+1);
        strcpy(books_ptr[i].title, str);
printf("Authors: ");
len = read_text(str, sizeof(str), 1);
books_ptr[i].auth = (char*) malloc(len+1);
strcpy(books_ptr[i].auth, str);

printf("Code: ");
len = read_text(str, sizeof(str), 1);
books_ptr[i].code = (char*) malloc(len+1);
strcpy(books_ptr[i].code, str);

printf("Price: ");
scanf("%f", &books_ptr[i].prc);

getchar();
/* Allocate memory to store the data of the publishing firm. */
books_ptr[i].pub_ptr = (pub*) malloc(sizeof(pub));

printf("Name: ");
len = read_text(str, sizeof(str), 1);
(books_ptr[i].pub_ptr)->name = (char*)malloc(len+1);
strcpy((books_ptr[i].pub_ptr)->name, str);

printf("Address: ");
len = read_text(str, sizeof(str), 1);
(books_ptr[i].pub_ptr)->addr = (char*)malloc(len+1);
strcpy((books_ptr[i].pub_ptr)->addr, str);

printf("Phone: ");
len = read_text(str, sizeof(str), 1);
(books_ptr[i].pub_ptr)->phone = (char*)malloc(len+1);
strcpy((books_ptr[i].pub_ptr)->phone, str);
}
printf("\nEnter code to search: ");
read_text(str, sizeof(str), 1);

for(i = 0; i < num; i++)
{
    if(strcmp(books_ptr[i].code, str) == 0)
    {
        printf("\nTitle: %s\tPublisher: %s\n\n", books_ptr[i].title, (books_ptr[i].pub_ptr)->name);
        break;
    }
}
if(i == num)
    printf("\nCode '%s' isn't registered\n", str);

for(i = 0; i < num; i++)
{
    free((books_ptr[i].pub_ptr)->name);
    free((books_ptr[i].pub_ptr)->addr);
    free((books_ptr[i].pub_ptr)->phone);
free(books_ptr[i].title);
free(books_ptr[i].auth);
free(books_ptr[i].code);
free(books_ptr[i].pub_ptr);
}
free(books_ptr);
return 0;
}
```

## Dynamic Data Structures

The data structures we've met so far are used for data storage and processing in an easy and fast way. For example, arrays are data structures, which are used for the storage of the same type of data. Structures and unions are also data structures, which can be used for the storage of any type of data. These data structures are static, in the sense that the allocated memory is fixed and cannot be modified during program execution. However, in many applications, it'd be more efficient to use a dynamic data structure, a structure whose size may grow or shrink as needed. The next sections introduce you to some simple forms of dynamic data structures and show you implementation examples. For more complex variants of data structures you should read a book focusing on that subject.

## Linked List

A linked list consists of a chain of linked elements, called nodes. Each node is typically represented by a structure, which contains its data and a pointer to the next node in the chain, as depicted in Figure 14.1.

The first node is the head of the list and the last one its tail. The value of the pointer member in the last node must be NULL to indicate the end of the list.

Unlike arrays whose size remains fixed, a linked list is more flexible because its size can be dynamically adjusted to the program's needs. Because we can easily insert and delete nodes at any point of the list, it is much easier to create and maintain a sorted order. On the other hand, to access an array element is very fast; we just use its position as an index. Typically, to access a list node, we should start from the head node (leave out the case of storing the nodes' addresses for direct access) and traverse the list serially, whereas arrays provide random access. Therefore, the time to access a node depends on its position in the list. It is fast if the node is close to the beginning, slow if it is near the end. This can make a huge difference to performance.

![](img/b8da5dcf9ba7f1fad5213c453d095246_491_0.png)

FIGURE 14.1
Linked list.

## Insert a Node

A new node can be inserted at any point in the list. To insert a new node, we check the following cases:

- 1. If the list is empty, the node is inserted at the beginning and becomes the head and the tail of the list. The value of its pointer member is set to NULL since there is no next node in the list.
- 2. If the list is not empty, we check the following subcases:
- a. If the node is inserted at the beginning of the list, it becomes the new head of the list and its pointer member points to the previous head, which now becomes the second node of the list.
- b. If the node is inserted at the end of the list, it becomes the new tail of the list and the value of its pointer member is set to NULL. The old tail becomes the second to last node and the value of its pointer member changes from NULL to point to the new node.
- c. If the node is inserted after an existing node, the pointer member of the new node must point to the node after the current node and the pointer member of the current node must point to the new node. Figure 14.2 depicts how the new node X is inserted between the nodes B and C.

## Delete a Node

To delete a node from the list and release the memory it allocates, we check the following cases:

- 1. If it is the head of the list, we check the following subcases:
- a. If there is a next node, this node becomes the new head of the list.
- b. If there is no next node, the list becomes empty.
- 2. If it is the tail of the list, the previous node becomes the new tail and its pointer member is set to NULL.
- 3. If it is an intermediate node, the pointer member of the previous node must point to the node after the one to be deleted. This operation is shown here with the deletion of node C (Figure 14.3).

![](img/b8da5dcf9ba7f1fad5213c453d095246_492_0.png)

FIGURE 14.2
Node insertion.
