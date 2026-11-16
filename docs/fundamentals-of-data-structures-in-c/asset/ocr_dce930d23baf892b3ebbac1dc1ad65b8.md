# 3.6.5 Empty Stack

If a stack contains no elements, it is referred to as an **empty stack**. If an element is to be popped from a stack, you have to check whether the stack is empty or not, because elements cannot be popped from an empty stack. In a linked list, if the stack is pointing to NULL the stack is said to be an empty stack. If you want to pop an element, from an empty stack the output, “Stack is underflow” is displayed.

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

# 3.6.6 Fully Occupied Stack

If a stack contains elements equal to its size, we say that the stack is full. If an element is to be pushed into a stack, you have to check whether the stack is full or not, since elements cannot be pushed into a stack when it is fully occupied. In case of stacks, represented using linked lists, there is no limit to store the elements in the stack, since the memory required to store the elements of the stack is allocated dynamically using the malloc() function. However, if the memory required for storing the elements of the stack is not available, we cannot insert elements into a stack. If the malloc() function returns NULL in a linked list it is referred as a **fully occupied stack**. If you want to insert an element, in a fully occupied stack the output “Stack is overflow” is displayed.

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