```
```cpp
{
    stack [++top] =element;
}
return 1;
}
```
```

To pop the element from the stack, first we would check for the empty condition. If the stack is empty then underflow message will be flashed to the user. To check the empty condition, we check the value associated to the top variable.

if (top== -1)

Value of -1 represents the empty condition. If there are more than zero elements in the stack, in that case pop operation can be performed. Before pop operation, the top element of the stack is stored in the temp variable. Afterwards, the top moves one pointer down and finally the value of the top stored in the temp variable is returned to the caller function, for the later usage, if any.

```
```cpp
//function to pop the element from the stack
int stacks::pop ()
{
    int temp=0;
    // Examine whether stack is empty or not.
    if (top==-1)  // top=-1 indicates the empty state of stack
    {
        cout<<"underflow: \n";
    }
    else
    {
        temp=stack [top--];
    }
    return temp;
}
```
```

We have also designed the function isEmpty () to determine whether the stack is empty or not. isEmpty() function can be used in several places, for instance, to determine the number of elements in a stack, at any point in time. This function can be utilized before the pop operation is performed. If the stack is empty then pop should not be permitted, instead suitable message need to be flashed to the user. It returns 1 that represents true, if the stack is empty otherwise returns 0 that represents false. Same has been illustrated in following program.