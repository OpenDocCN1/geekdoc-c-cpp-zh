operator). As with the copy constructor, if you don't specify an assignment operator, C++ gives you a default assignment operator that performs a shallow copy. So, you usually only need to overload the assignment operator in the “rule of three” case.

There's one big difference between an assignment operator and a copy constructor. With a copy constructor, you're constructing a new object as a copy of an existing one. With an assignment operator, you're overwriting an already existing instance of an object. For example, the following code invokes the assignment operator for DynamicArray on the third line because the first line previously constructed a1:

Click here to view code image

```
DynamicArray a1(50);
DynamicArray a2(75);
a1 = a2;
```

Because the assignment operator overwrites an already existing instance with new values, it needs to deallocate any previously dynamically allocated data. For example, this is the correct implementation of the assignment operator for DynamicArray:

Click here to view code image

```
DynamicArray& operator=(const DynamicArray& other)
{
```