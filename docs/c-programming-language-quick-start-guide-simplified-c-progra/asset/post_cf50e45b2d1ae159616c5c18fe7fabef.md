
```c
break;

case 2:
    if (TOP == -1)
        printf("Error: Underflow.\n\n");
    else
    {
        element = pop();
        printf("Element removed from stack is %d.\n", element);
    }
    break;

case 3:
    if (!is_empty())
    {
        element = peek();
        printf("Element at the top of stack is %d\n\n", element);
    }
    else
        printf("Stack is empty.\n\n");
    break;

case 4:
    if (is_empty())
        printf("Stack is empty.\n\n");
    else
        printf("Stack is not empty.\n\n");
    break;

case 5:
    exit(0);
}
}
}

void push(int value)
{
    TOP++;
    stack[TOP] = value;
}

int pop()
{
    int element;
    if (TOP == -1)
        return TOP;
    element = stack[TOP];
    TOP--;
    return element;
}

int is_empty()
{
    if (TOP == -1)
        return 1;
    else
        return 0;
}

int peek()
{
    return stack[TOP];
}
```

### 7.5.2 Queues

A queue is a container of objects (a linear collection) that follows the first-in first-out (FIFO) principle. An example of queues is any real life queue like in a Bank, or ATM or Airport. A new element or object is added to the back of the queue, while removal (or serving) happens from the front. In the queue only two operations are allowed. These are enqueue and dequeue functions. First one means to insert an item into the back of the queue and dequeue refers to removing an item from the front.

The difference between stacks and queues is in removing. In a stack we remove the last item that was added whereas in a queue, we remove the item that has been in the queue more than anyone else.

Here is a complete program illustrating the use of Queues:

```c
#define MAX_SIZE 50

int queue_array[MAX_SIZE];

int rear = -1;

int front = -1;

void main(void)
{
    int choice;

    while (1)
    {
        printf("1.Insert element to queue \n");
        printf("2.Delete element from queue \n");
        printf("3.Display all elements of queue \n");
        printf("4.Quit \n");
        printf("Enter your choice : ");
        scanf("%d", &choice);
        switch (choice)
        {
        case 1:
            insert();
            break;
        case 2:
            delete();
            break;
        case 3:
            display();
            break;
        case 4:
            exit(1);
        default:
            printf("Wrong choice \n");
        }
    }
}

void insert()
{
    int add_item;
    if (rear == MAX_SIZE - 1)
        printf("Queue Overflow \n");
    else
    {
        if (front == -1)
            front = 0;
        printf("Insert the element in queue : ");
        scanf("%d", &add_item);
        rear = rear + 1;
        queue_array[rear] = add_item;
    }
}

void delete()
{
    if (front == -1 || front > rear)
    {
        printf("Queue Underflow \n");
        return;
    }
    else
    {
        printf("Element deleted from queue is : %d\n", queue_array[front]);
        front = front + 1;
    }
}

void display()
{
    int i;
    if (front == -1)
        printf("Queue is empty \n");
    else
    {
        printf("Queue is : \n");
        for (i = front; i <= rear; i++)
            printf("%d ", queue_array[i]);
        printf("\n");
    }
}
```

### 7.5.3 Linked Lists

A linked list is a sequential access data structure, where each element can be accessed only in particular order. A typical illustration of sequential access finding a particular file from an unorganized pile of files. It is like a clothes line on which the data structures hang sequentially. A head pointer addresses the first element of the list, and each element points at a successor element, with the last element having a NULL value.

Here’s a code that implements a linked list. Linked list consists of adjacent nodes with each having the address of next node. Starting from head, we can traverse through the whole list by using the pointer next in each node. We can take another pointer in node which can hold address for previous node as well.

```c
struct Node
{
    int val;
    struct Node *next;
};
typedef struct Node element;

void main()
{
    element *curr, *head;
    int i;
    head = NULL;
    for (i = 1; i <= 10; i++)
    {
        curr = (element *)malloc(sizeof(element));
        curr->val = i;
        curr->next = head;
        head = curr;
    }
    curr = head;
    while (curr)
    {
        printf("%d\n", curr->val);
        curr = curr->next;
    }
}
```

## Chapter 8: Binary Trees

A tree is a finite set of elements, often known as nodes. Every tree has a unique starting node, called the root node, whereas the remaining nodes are a disjoint collection of subtrees of this root node. Each node keeps track of its parents or/and children so that traversal can be made possible. A node with no children is called a leaf node or a terminal node.

A binary tree is a tree whose nodes can have a maximum of two children. A binary tree is a data structure which comprises of two possible sub-elements of every node, called left child and right child. If a node does not have a left or right child, they are assigned NULL values. Each link must point at a new object not pointed at or be NULL.

The general form a node in a binary tree is as follows:

```c
struct node
{
    char value;
    struct node *left, *right;
};
```

The binary tree is a useful data structure for rapidly storing sorted data and rapidly retrieving stored data. This results in an immense increase in efficiency of searching and sorting.

### 8.1 Composition

A binary tree is composed of parent nodes, or leaves, each of which stores data and also links to up to at most two child nodes. It is the relationship between the leaves linked to and the linking leaf, also known as the parent node, which makes the binary tree such an efficient data structure.

Generally, the left node has a lesser value than parent while right child has a greater key value than its parents. Due to these two simple rules, the efficiency of trees is enormous.

As a result, the leaves on the farthest left of the tree have the lowest values and we already know that so if we want to get the lowest value, we only need to traverse to the lowermost leaf node to the left instead of going through every element of the tree.

Similarly, the leaves on the right of the tree have the greatest values and therefore if we need to find the highest number, we just need to traverse to one side of the tree and we can reach the destination much quicker than a program which used sorting and searching algorithms to accomplish this task.

More importantly, as each leaf connects to two other leaves, it is the beginning of a new, smaller, binary tree. Due to this reason, it is possible to easily access and insert any type data in a binary tree at any point of time, using search and insert functions recursively called on successive leaves and maintaining the order of tree as well. The newly inserted node always goes to the right place.

### 8.2 Insert Function

The following insert function inserts elements in a tree. If tree is not created, the element creates it as well. It uses pointers to pointers in order to handle the case of a tree that might not exist. By taking a pointer to a pointer, it is possible to allocate memory if the root pointer is NULL.

```c
void insert(int key, struct node **terminal)
{
    if (*terminal == 0)
    {
        *terminal = (struct node *)malloc(sizeof(struct node));
        (*terminal)->key_value = key;
        (*terminal)->left = 0;
        (*terminal)->right = 0;
    }
    else if (key < (*terminal)->key_value)
    {
        insert(key, &(*terminal)->left);
    }
    else if (key > (*terminal)->key_value)
    {
        insert(key, &(*terminal)->right);
    }
}
```

The insert function follows the two basic rules of a binary tree. For any current node, move left if you have a lower value to enter and move right for a greater value, until it reaches a NULL node, which it allocates memory for and initializes with the new key value. The pointers to the second last node are updated and pointers for newly initialized node are set to NULL. Once, the element has been added, the insert function will stop calling itself and return program control to normal environment for execution.

### 8.3 Search Function

Here is a search function for a binary tree. It takes a key value and a starting node and searches the key value in the tree recursively. If leaf node is found, it is returned elsewise 0 is returned.

```c
struct node *search(int key, struct node *terminal)
{
    if (terminal != 0)
    {
        if (key == terminal->key_value)
        {
            return terminal;
        }
        else if (key < terminal->key_value)
```
