Finally, we let **elem** point to the new elements:

```
elem = p;                  // now we can reset elem
sz = a.sz;
```

We can represent the result graphically like this:

![](bbox=[0.15, 0.23, 0.75, 0.36])

We now have a **vector** that doesn't leak memory and doesn't free (**delete[]**) any memory twice.

When implementing the assignment, you could consider simplifying the code by freeing the memory for the old elements before creating the copy, but it is usually a very good idea not to throw away information before you know that you can replace it. Also, if you did that, strange things would happen if you assigned a **vector** to itself:

```
vector v(10);
v = v;      // self-assignment
```

Please check that our implementation handles that case correctly (if not with optimal efficiency).

# 18.8.3 Copy terminology

Copying is an issue in most programs and in most programming languages. The basic issue is whether you copy a pointer (or reference) or copy the information pointed to (referred to):

+   *   *Shallow copy* copies only a pointer so that the two pointers now refer to the same object. That's what pointers and references do.
*   *Deep copy* copies what a pointer points to so that the two pointers now refer to distinct objects. That's what **vectors**, **strings**, etc. do. We define copy constructors and copy assignments when we want deep copy for objects of our classes.

Here is an example of shallow copy: