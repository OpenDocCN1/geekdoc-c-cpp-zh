reading half a million floating-point values into a **vector** using **push_back()** — measurements confirmed that pre-allocation didn’t make a noticeable difference. Always measure before making significant changes in the interest of performance; even for experts, guessing about performance is very hard.

As pointed out in §20.6, moving elements also implies a logical constraint: don’t hold iterators or pointers to elements of a **vector** when you do list operations (such as **insert()**, **erase()**, and **push_back()**); if an element moves, your iterator or pointer will point to the wrong element or to no element at all. This is the principal advantage of **lists** (and **maps**; see §21.6) over **vectors**. If you need a collection of large objects or of objects that you point to from many places in a program, consider using a **list**.

Let’s compare **insert()** and **erase()** for a **vector** and a **list**. First we take an example designed only to illustrate the key points:

```
vector<int>::iterator p = v.begin();     // take a vector
++p; ++p; ++p;                            // point to its 4th element
auto q = p;
++q;                                      // point to its 5th element
```

![](bbox=[0.3, 0.45, 0.8, 0.54])

```
p = v.insert(p,99);                      // p points at the inserted element
```

![](bbox=[0.3, 0.58, 0.8, 0.68])

Note that **q** is now invalid. The elements may have been reallocated as the size of the vector grew. If **v** had spare capacity, so that it grew in place, **q** most likely points to the element with the value **3** rather than the element with the value **4**, but don’t try to take advantage of that.

```
p = v.erase(p);                          // p points at the element after the erased one
```

![](bbox=[0.3, 0.82, 0.8, 0.91])