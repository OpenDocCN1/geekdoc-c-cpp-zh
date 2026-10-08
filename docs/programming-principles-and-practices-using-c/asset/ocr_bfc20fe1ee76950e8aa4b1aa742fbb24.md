A **unique_ptr** is very much like an ordinary pointer, but it has one significant restriction: you cannot assign one **unique_ptr** to another to get two **unique_ptr**s to the same object. That has to be so, or confusion could arise about which **unique_ptr** owned the pointed-to object and had to **delete** it. For example:

```
```
void no_good()
{
    unique_ptr<X> p { new X };
    unique_ptr<X> q {p};    // error: fortunately
    // . . .
} // here p and q both delete the X
```
```

If you want to have a “smart” pointer that both guarantees deletion and can be copied, use a **shared_ptr** (§B.6.5). However, that is a more heavyweight solution that involves a use count to ensure that the last copy destroyed destroys the object referred to.

A **unique_ptr** has the interesting property of having no overhead compared to an ordinary pointer.

# ## 19.5.5 Return by moving

The technique of returning a lot of information by placing it on the free store and returning a pointer to it is very common. It is also a source of a lot of complexity and one of the major sources of memory management errors: Who **deletes** a pointer to the free store returned from a function? Are we sure that a pointer to an object on the free store is properly **deleted** in case of an exception? Unless we are systematic about the management of pointers (or use “smart” pointers such as **unique_ptr** and **shared_ptr**), the answer will be something like “Well, we think so,” and that’s not good enough.

Fortunately, when we added move operations to **vector**, we solved that problem for **vectors**: just use a move constructor to get the ownership of the elements out of the function. For example:

```
```
vector<int> make_vec()   // make a filled vector
{
    vector<int> res;
    // . . . fill the vector with data; this may throw an exception . . .
    return res;             // the move constructor efficiently transfers ownership
}
```
```

This (final) version of **make_vec()** is the simplest and the one we recommend. The move solution generalizes to all containers and further still to all resource handles. For example, **fstream** uses this technique to keep track of file handles. The move