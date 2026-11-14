# A.4.3.2 Approach 2: Returning Pointers

We mentioned that we cannot pass two arguments in one bracket, but we could pass them in two brackets, e.g.:

```
A[0][1];
```

This is also how two-dimensional built-in arrays are accessed in C++. For our dense matrix, we can return the pointer to the first entry in row r and when the second bracket with the column argument is applied on this pointer C++ will perform the address calculation:

```
double* operator[](int r) { return data + r*ncols; }
const double* operator[](int r) const { return data + r*ncols; }
```

This method has several disadvantages. First, it only works for dense matrices that are stored row-wise. Second, there is no possibility of verifying the range of the column index.

# A.4.3.3 Approach 3: Returning Proxies

Instead of returning a pointer, we can build a specific type that keeps a reference to the matrix and the row index and that provides an operator[] for accessing matrix entries. Such helpers are called Proxies. A proxy must be therefore a friend of the matrix class to reach its private data. Alternatively, we can keep the operator with the parentheses and call this one from the proxy. In both cases, we encounter cyclic dependencies.

If we have several matrix types, each of them would need its own proxy. We would also need different proxies for constant and mutable access respectively. In Section 6.6, we showed how to write a proxy that works for all matrix types. The same templated proxy will handle constant and mutable access. Eventually, it even solves the problem of mutual dependencies. The only minor flaw is that eventual errors cause lengthy compiler messages.

# A.4.3.4 Comparing the Approaches

The previous implementations show that C++ allows us to provide different notations for user-defined types, and we can implement them in the manner that seems most appropriate to us. The first approach was replacing square brackets with parentheses to enable multiple arguments. This was the simplest solution, and if one is willing to accept this syntax, one can save oneself the effort of coming up with a fancier notation. The technique of returning a pointer is not complicated either, but it relies too strongly on the internal representation. If we use some internal blocking or some other specialized internal storage scheme, we will need an entirely different technique. For that reason, it always helps to encapsulate the technical details and to provide a sufficiently abstract interface for the user. Then our applications do not depend on technical details. Another drawback is that we cannot test the range of the column index.

# A.5 Method Generation

C++ has six methods (four in C++03) with a default behavior:

+   - Default constructor

+   - Copy constructor