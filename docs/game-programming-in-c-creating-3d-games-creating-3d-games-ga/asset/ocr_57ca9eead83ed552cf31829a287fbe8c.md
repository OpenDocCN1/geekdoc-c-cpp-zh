```
};
```

With this `DynamicArray` class, you could create a dynamic array with 50 elements by using the following code:

```
DynamicArray scores(50);
```

However, as previously discussed, every call to `new` must have a matching call to `delete`. In this case, `DynamicArray` dynamically allocates an array in its constructor, but there's no matching `delete []` anywhere. This means that when the `scores` object goes out of scope, there is a memory leak.

The solution is to use another special member function called the **destructor**. The destructor is a member function that automatically runs when destroying the object. For objects allocated on the stack, this happens when the object goes out of scope. For dynamically allocated objects, the `delete` call on the object also invokes the destructor.

The destructor always has the same name as the class, except prefaced with a tilde (~). So for `DynamicArray`, this is the destructor:

```
DynamicArray::~DynamicArray()
{
```