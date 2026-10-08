than array elements (as in the definitions of ai2 and ad), the remaining elements are initialized by the element type's default value.

# ## 18.6.4 Pointer problems

Like arrays, pointers are often overused and misused. Often, the problems people get themselves into involve both pointers and arrays, so we'll summarize the problems here. In particular, all serious problems with pointers involve trying to access something that isn't an object of the expected type, and many of those problems involve access outside the bounds of an array. Here we will consider

+   - Access through the null pointer
- Access through an uninitialized pointer
- Access off the end of an array
- Access to a deallocated object
- Access to an object that has gone out of scope

In all cases, the practical problem for the programmer is that the actual access looks perfectly innocent; it is "just" that the pointer hasn't been given a value that makes the use valid. Worse (in the case of a write through the pointer), the problem may manifest itself only a long time later when some apparently unrelated object has been corrupted. Let's consider examples:

> > *Don't access through the null pointer:*

```
```
int* p = nullptr;
*p = 7;         // ouch!
```
```

Obviously, in real-world programs, this typically occurs when there is some code in between the initialization and the use. In particular, passing p to a function and receiving it as the result from a function are common examples. We prefer not to pass null pointers around, but if you have to, test for the null pointer before use:

```
```
int* p = fct_that_can_return_a_nullptr();

if (p == nullptr) {
    // do something
}
else {
    // use p
    *p = 7;
}
```
```