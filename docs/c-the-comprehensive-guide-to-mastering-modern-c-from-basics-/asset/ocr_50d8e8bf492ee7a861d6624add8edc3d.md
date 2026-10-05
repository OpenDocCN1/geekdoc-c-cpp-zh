# 20.3 Dangers of Aliasing

Did you notice that I secretly inserted the following into
Listing 20.1?

```
values.reserve(50); // Ensure space for 50 values
```

The reason for this is that I need to avoid a danger that
arises from being able to access the same value—its
memory range—in different ways. That is known as
aliasing.

The vector also manages its data somewhere in memory.
One of its properties is that it promises to store
them consecutively. However, this means that there
might be no space left at the “back” of the vector when
you add an element with push_back(). But vector handles
this: it requests a new memory range twice as large and
copies (or moves) all existing values to the new area.
Finally, vector removes the old area.

![](bbox=[0.254, 0.676, 0.742, 0.813])

Figure 20.2 A pointer points into the data of a vector.