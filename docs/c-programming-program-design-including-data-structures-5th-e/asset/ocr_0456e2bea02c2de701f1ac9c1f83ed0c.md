```
p = head;
while (p != NULL)
{
    cout << p->info << " ";
    p = p->link;
}
cout << endl;
```

The output of this code is: 43 12 72 8

+   17. Item to be deleted is not in the list.
+       18 38 2 15 45 25

+   19. Answer to this question is available at the Web site accompanying this book.

+   21. Answer to this question is available at the Web site accompanying this book.

# Chapter 18

+   1. The two basic operations on a stack are push, to add an element to a stack, and pop, to remove an element from a stack.

+   3.
+      x = 3
+      y = 9
+      7
+      13
+      4
+      7

+   5. a. 26; b. 45; c. 8; d. 29

+   7.
+      a. A * B + C
+      b. (A + B) * (C − D)
+      c. (A − B − C) * D

+   9. 10 20 30 40 50

+   11. If the stack is nonempty, the statement `stack.top();` returns the top element of the stack, and the statement `stack.pop();` removes the top element of the stack.

```
13. template <class elemType>
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
```