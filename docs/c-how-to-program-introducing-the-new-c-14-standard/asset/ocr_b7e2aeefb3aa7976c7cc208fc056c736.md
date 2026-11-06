```
```cpp
// pop floating-point values from doubleStack
while (!doubleStack.isStackEmpty()) {
    doubleStack.pop(popDouble);
    cout << popDouble << "popped from stack" << endl;
    doubleStack.printStack();
}
}
```
```

```
```
processing an integer Stack
The list is: 0

The list is: 1 0

The list is: 2 1 0

2 popped from stack
The list is: 1 0

1 popped from stack
The list is: 0

0 popped from stack
The list is empty

processing a double Stack
The list is: 1.1

The list is: 2.2 1.1

The list is: 3.3 2.2 1.1

3.3 popped from stack
The list is: 2.2 1.1

2.2 popped from stack
The list is: 1.1

1.1 popped from stack
The list is empty

All nodes destroyed

All nodes destroyed
```
```

Fig. 19.14 A simple stack program.