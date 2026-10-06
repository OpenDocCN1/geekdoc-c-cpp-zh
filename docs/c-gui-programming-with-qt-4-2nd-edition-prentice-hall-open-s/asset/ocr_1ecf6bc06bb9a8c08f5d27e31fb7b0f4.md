qDeleteAll() algorithm calls delete on every pointer a pointer type. In a container, the call, makes sense only on containers whose value type is a pointer type. After the call, the items are still present in the container as dangling pointers, so normally we would also call clear() on the container. For example:

```
qDeleteAll(list);
list.clear();
```

The qSwap() algorithm exchanges the value of two variables. For example:

```
int x1 = line.x1();
int x2 = line.x2();
if (x1 > x2)
    qSwap(x1, x2);
```

Finally, the <QtGlobal> header, which is included by every other Qt header, provides several useful definitions, including the qAbs() function, that returns the absolute value of its argument, and the qMin() and qMax() functions, that return the minimum or maximum of two values.