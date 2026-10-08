# Stacks

# Stack Operations:

an element to the top of the stack.
and returns the top element of the stack.
the top element of the stack without removing it.
if the stack is empty.

Implementing Stacks using Arrays: Arrays provide a simple way to implement stacks, using an integer to track the top element’s index.

```
#define MAX_SIZE 100 typedef struct { items[MAX_SIZE]; top; }
Stack; void initializeStack(Stack* stack) { = -1; } void push(Stack* stack,
 int item) { (stack->top == MAX_SIZE - 1) { item = }; } int pop(Stack*
stack) { (stack->top == -1) { -1 }; stack->items[stack->top--]; } int
peek(Stack* stack) { (stack->top == -1) { -1 }; stack->items[stack->top]; } int
 isEmpty(Stack* stack) { stack->top == -1; }
```

Implementing Stacks using Linked Lists: For dynamic size requirements, linked lists offer a more flexible implementation of stacks without a fixed size limit.

```
typedef struct Node { data; Node* next; } Node; typedef struct { top; }
StackLinkedList; void initializeStackLinkedList(StackLinkedList* stack)
{ = NULL; } void pushLinkedList(StackLinkedList* stack, int item) {
newNode = (Node*)malloc(sizeof(Node)); item = item; stack->top = =
```