![](bbox=[0.183, 0.076, 0.909, 0.238])

FIGURE 12-19  Object objectOne

Let us consider the following function prototype:

```
void destroyList(ptrMemberVarType paramObject);
```

The function destroyList has a formal value parameter, paramObject. Now consider the following statement:

```
destroyList(objectOne);
```

In this statement, objectOne is passed as a parameter to the function destroyList. Because objectOne is passed by value to paramObject, the copy constructor copies the member variables of objectOne into the corresponding member variables of paramObject. Just as in the previous case, paramObject.p and objectOne.p would point to the same memory space, as shown in Figure 12-20.

![](bbox=[0.183, 0.576, 0.909, 0.764])

FIGURE 12-20  Pointer member variables of objects objectOne and paramObject pointing to the same array

Because objectOne is passed by value, the member variables of paramObject should have their own copy of the data. In particular, paramObject.p should have its own memory space. How do we ensure that this is, in fact, the case?