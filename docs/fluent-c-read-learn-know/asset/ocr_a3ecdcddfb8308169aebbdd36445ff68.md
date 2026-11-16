When you create an instance of a value type, the actual value is stored on the stack.

```
Int32 x = 5;
```

x = 5

But when you create an instance of a reference type, the actual data is stored in the heap, and a reference to it is stored on the stack.

```
Elephant e = new Elephant();
```

e =

> It's easy to remember the difference: the stack stores a reference to a reference type and the value of a value type.

![](bbox=[0.52, 0.68, 0.78, 0.83])