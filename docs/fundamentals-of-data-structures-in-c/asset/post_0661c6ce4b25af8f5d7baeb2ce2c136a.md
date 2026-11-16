
## 3.6.3 PEEK Operation

PEEK operation is used to display the element from the TOP of the stack, pointed by the TOP pointer without actually removing it. PEEK operation of a stack is also implemented using linked lists. When implementing the PEEK operation, underflow condition of a stack is to be checked. The user should not try to PEEK an element from an empty stack. This type of an attempt is illegal and should be avoided.

```
Algorithm to Retrieve the Contents from the Top of the Stack

PEEK(VALUE : INTEGER)
GLOBAL: TOPSTK : STACK
TEMP : STACK
Step 1 : If (IS EMPTY() == 1)
    Return -1
    [End of If Structure]
Step 2 : TEMP = TOPSTK
Step 3 : VALUE = TEMP -> DATA
Step 4 : Return 0
End PEEK()
```

## 3.6.4 Traversing a Stack

To read the information or to display the information in a stack, you have to traverse (move) a linked list, node by node from the first node, until the end of the list is reached. Traversing a list involves the following steps,

- Assign the address of TOP pointer to a variable.
- Display the information in the data field.
- Traverse the list from one node to another by advancing the pointer up to NULL.

```
Algorithm for Displaying the Contents of the Stack

VIEW()
GLOBAL: TOPSTK : STACK
TOP : STACK
Step 1 : If (IS EMPTY() == 1)
    Print "Stack is EMPTY"
    Return
    [End of If Structure]
Step 2 : TOP = TOPSTK
Step 3 : Do While(TOP != NULL)
    Print "Value is", TOP -> DATA
    TOP = TOP -> NEXT
    [End of Step 3 While Structure]
End VIEW()
```

## 3.6.5 Empty Stack

If a stack contains no elements, it is referred to as an **empty stack**. If an element is to be popped from a stack, you have to check whether the stack is empty or not, because elements cannot be popped from an empty stack. In a linked list, if the stack is pointing to NULL the stack is said to be an empty stack. If you want to pop an element, from an empty stack the output, "Stack is underflow" is displayed.

```
Algorithm for IS_EMPTY()
IS_EMPTY(VALUE : INTEGER)
GLOBAL: TOPSTK : STACK
Step 1 : If (TOPSTK == NULL)
            Return 1
        Else
            Return 0
        [End of If Structure]
End IS_EMPTY()
```

## 3.6.6 Fully Occupied Stack

If a stack contains elements equal to its size, we say that the stack is full. If an element is to be pushed into a stack, you have to check whether the stack is full or not, since elements cannot be pushed into a stack when it is fully occupied. In case of stacks, represented using linked lists, there is no limit to store the elements in the stack, since the memory required to store the elements of the stack is allocated dynamically using the malloc() function. However, if the memory required for storing the elements of the stack is not available, we cannot insert elements into a stack. If the malloc() function returns NULL in a linked list it is referred as a **fully occupied stack**. If you want to insert an element, in a fully occupied stack the output "Stack is overflow" is displayed.

```
Algorithm for IS_FULL()
IS_FULL(VALUE : INTEGER)
GLOBAL: TOPSTK : STACK
TEMP: STACK
Step 1 : TEMP = GETNODE()
Step 2 : If (TEMP == NULL)
            Return 1
        Else
            RELEASENODE(TEMP)
            Return 0
        [End of If Structure]
End IS_FULL()
```

## 3.6.7 Stack Size

In case of stacks represented using linked lists, there is no limit to store the elements, since the memory required to store the elements of the stack is allocated dynamically using the malloc() function. To find the size of the stack, (i.e., number of elements that has been stored), to check whether the memory required for storing the elements of the stack is available or not, use the sizeof() function as mentioned in Program 3.2. Note that elements cannot be stored in a stack, when the memory pointed by the linked list points to NULL.

```
Algorithm to Count the Nodes in a Stack
SIZE(VALUE : INTEGER)
GLOBAL: TOPSTK : STACK
TOP : STACK; COUNT : INTEGER
Step 1 : TOP = TOPSTK
Step 2 : COUNT = 0
Step 3 : Do While(TOP != NULL)
    COUNT = COUNT + 1
    TOP = TOP -> NEXT
    [End of Step 3 While Structure]
Step 4 : Return COUNT
End SIZE()
```

## Program 3.3 :

```
/* Program to implement a stack using singly linked list. */
/* linstack.c */
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
typedef struct node
{
    int data;
    struct node *next;
}stack;
int size();
void view();
int isFull();
int isEmpty();
void displayMenu();
int push(int value);
int pop(int *value);
int peek(int *value);
stack *getNode();
void releaseNode(stack *newnode);
stack *topStk = NULL;
void main()
{
    int data, status, choice;
    displayMenu();
    while(1)
    {
        printf("\n\n ? ");
        scanf("%d", &choice);
        switch(choice)
        {
            case 1:
                printf("\n Enter the element : ");
                fflush(stdin);
                scanf("%d", &data);
                status = push(data);
                if(status == -1)
                    printf("\n Memory is not available ...");
                break;
            case 2:
                status = pop(&data);
                if(status == -1)
                    printf("\n Stack underflow on POP");
                else
                    printf("\n The popped value is %d", data);
                break;
            case 3:
                status = peek(&data);
                if(status == -1)
                    printf("\n Stack is Empty !!!");
                else
                    printf("\n The Top most value is %d", data);
                break;
            case 4:
                printf("\n Current Stack Elements = %d", size());
                break;
            case 5 :
                view();
                break;
            default:
                printf("\n End of Run of your Program . . .");
                exit(0);
        }
    }
}

void displayMenu()
{
    printf("\n Representation of stack using single linked lists . . .");
    printf("\n\t 1. Push ");
    printf("\n\t 2. Pop ");
    printf("\n\t 3. Peek ");
    printf("\n\t 4. Size ");
    printf("\n\t 5. View ");
    printf("\n\t 6. Exit ");
}

stack *getNode()
{
    return((stack *)malloc(sizeof(stack)));
}

void releaseNode(stack *newnode)
{
    free(newnode);
}

int push(int value)
{
    extern stack *topStk;
    stack *newptr;
    if(isFull())
    return -1;
    newptr = getNode();
    newptr -> data = value;
    newptr -> next = topStk;
    topStk = newptr;
    return 0;
}

int pop(int *value)
{
    extern stack *topStk;
    stack *temp;
    if(isEmpty())
        return -1;
    temp = topStk;
    topStk = topStk -> next;
    *value = temp -> data;
    releaseNode(temp);
    return 0;
}

int peek(int *value)
{
    extern stack *topStk;
    stack *temp;
    if(isEmpty())
        return -1;
    temp = topStk;
    *value = temp -> data;
    return 0;
}

int isEmpty()
{
    extern stack *topStk;
    if(topStk == NULL)
        return 1;
    else
        return 0;
}

int isFull()
{
    extern stack *topStk;
    stack *temp;
    temp = getNode();
    if(temp == NULL)
        return 1;
    else
    {
        releaseNode(temp);
        return 0;
    }
}

int size()
{
    extern stack *topStk;
    stack *top;
    int count = 0;
    for(top = topStk; top != NULL; top = top -> next)
    count++;
    return count;
}

void view()
{
    extern stack *topStk;
    stack *top;
    if(isEmpty())
    {
    printf("\n The stack is Empty !!! ");
    return;
    }
    printf("\n The content of the stack is... TOP");
    for(top = topStk; top != NULL; top = top -> next)
    printf(" --> %d", top -> data);
}
```

## The program displays the following output

```
Representation of stack using single linked lists ...
1. Push
2. Pop
3. Peek
4. Size
5. View
6. Exit

? 2
Stack underflow on POP

? 3
Stack is Empty
? 4
Current Stack Elements = 0
? 5
The stack is Empty !!!
? 1
Enter the element : 101
? 1
Enter the element : 102
? 1
Enter the element : 103
? 1
Enter the element : 104
? 1
Enter the element : 105
? 5
The content of the stack is... TOP --> 105 --> 104 --> 103 --> 102
--> 101
? 4
Current Stack Elements = 5
? 2
The popped value is 105
? 2
The popped value is 104
? 5
The content of the stack is... TOP --> 103 --> 102 --> 101
? 4
Current Stack Elements = 3
? 2
The popped value is 103
? 2
The popped value is 102
? 5
The content of the stack is... TOP --> 101
? 2
The popped value is 101
? 2
Stack underflow on POP
? 5
The stack is Empty !!!
? 6
End of Run of your Program . . .
```
