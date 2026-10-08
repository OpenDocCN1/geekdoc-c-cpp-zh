Long initializer lists for **new** can be impractical, but they can come in very handy when we want just a few elements, and that is typically the most common case.

# **17.4.5 The null pointer**

If you have no other pointer to use for initializing a pointer, use the null pointer, **nullptr**:

```
double* p0 = nullptr; // the null pointer
```

When assigned to a pointer, the value zero is called the *null pointer*, and often we test whether a pointer is valid (i.e., whether it points to something) by checking whether it is **nullptr**. For example:

```
if (p0 != nullptr) // consider p0 valid
```

This is not a perfect test, because **p0** may contain a “random” value that happens to be nonzero (e.g., if we forgot to initialize) or the address of an object that has been **deleted** (see §17.4.6). However, that’s often the best we can do. We don’t actually have to mention **nullptr** explicitly because an *if*-statement really checks whether its condition is **nullptr**:

```
if (p0) // consider p0 valid; equivalent to p0!=nullptr
```

We prefer this shorter form, considering it a more direct expression of the idea “**p0** is valid,” but opinions vary.

We need to use the null pointer when we have a pointer that sometimes points to an object and sometimes not. That’s rarer than many people think; consider: If you don’t have an object for a pointer to point to, why did you define that pointer? Couldn’t you wait until you have an object?

The name **nullptr** for the null pointer is new in C++11, so in older code, people often use **0** (zero) or **NULL** instead of **nullptr**. Both older alternatives can lead to confusion and/or errors, so prefer the more specific **nullptr**.

# **17.4.6 Free-store deallocation**

The **new** operator allocates (“gets”) memory from the free store. Since a computer’s memory is limited, it is usually a good idea to return memory to the free store once we are finished using it. That way, the free store can reuse that memory for a new allocation. For large programs and for long-running programs such freeing of memory for reuse is essential. For example:

```
double* calc(int res_size, int max) // leaks memory
{
```