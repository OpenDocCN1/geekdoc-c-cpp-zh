Line 2 terminates. From Figure 19–22, it follows that a pointer to each node in the linked list is saved in the stack. The top element of the stack contains a pointer to the last node in the list, and so on. Let us now execute the following statements:

```
```cpp
while (!stack.isEmptyStack())        //Line 5
{
    current = stack.top();            //Line 6
    stack.pop();                      //Line 7
    cout << current->info << " ";     //Line 8
}
```
```

The loop condition in Line 5 evaluates to true because the stack is nonempty. Therefore, the statements in Lines 6, 7, and 8 execute. After the statement in Line 6 executes, current points to the last node. The statement in Line 7 removes the top element of the stack. (See Figure 19-23.)

![](bbox=[0.182, 0.384, 0.912, 0.601])

The statement in Line 8 outputs `current->info`, which is 15. Next, the loop condition in Line 5 is evaluated. Because the loop condition evaluates to true, the statements in Lines 6, 7, and 8 execute. After the statements in Lines 6 and 7 execute, Figure 19-24 results.

![](bbox=[0.182, 0.751, 0.912, 0.909])