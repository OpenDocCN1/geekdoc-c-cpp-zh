+   5. 13
+      32 32 13 16 28
+      `temp = 16`

+   7. `secretNum = 226`

+   9.
+      a. 16
+      b. -4
+      c. 39
+      d. 12
+      e. 15

+   11.
+      a. `x * y + z - t`
+      b. `x * (y + z) - w / u`
+      c. `(x - y) * (z / u) - (t + s)`
+      d. `x * (y - (z + w))`

+   13. 1 16 27 16 5

15. If the stack is nonempty, the statement `stack.top();` returns the top element of the stack and the statement `stack.pop();` removes the top element of the stack.

```
template <class elemType>
elemType second(stackType<elemType> stack)
{
    elemType temp1, temp2;

    if (stack.isEmptyStack())
    {
        cout << "Stack is empty." << endl;
        exit(0); //terminate the program
    }

    temp1 = stack.top();
    stack.pop();

    if (stack.isEmptyStack())
    {
        cout << "Stack has only one element." << endl;
        exit(0); //terminate the program
    }

    temp2 = stack.top();
    stack.push(temp1);

    return temp2;
}
```