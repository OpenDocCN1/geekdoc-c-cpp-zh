```
else if (sz===space)
    reserve(2*space);       // get more space
    elem[sz] = d;           // add d at end
    ++sz;                   // increase the size (sz is the number of elements)
}
```

In other words, if we have no spare space, we double the size of the allocation. In practice that turns out to be a very good choice for the vast majority of uses of **vector**, and that's the strategy used by most implementations of the standard library **vector**.

# ### 19.2.5 Assignment

We could have defined vector assignment in several different ways. For example, we could have decided that assignment was legal only if the two vectors involved had the same number of elements. However, in §18.3.2 we decided that vector assignment should have the most general and arguably the most obvious meaning: after assignment **v1=v2**, the vector **v1** is a copy of **v2**. Consider:

![](bbox=[0.3, 0.44, 0.8, 0.6])

Obviously, we need to copy the elements, but what about the spare space? Do we “copy” the “free space” at the end? We don’t: the new **vector** will get a copy of the elements, but since we have no idea how that new **vector** is going to be used, we don’t bother with extra space at the end:

![](bbox=[0.28, 0.71, 0.83, 0.91])