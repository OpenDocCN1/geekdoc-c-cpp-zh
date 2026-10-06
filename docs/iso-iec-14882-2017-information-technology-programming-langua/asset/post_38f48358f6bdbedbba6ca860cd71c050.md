
# ISO/IEC 14882:2017(E)

provided (including the terminating '\0' in a string literal (5.13.5)) exceeds the number of elements to initialize.

If the expression is erroneous before converting to std::size_t:

-   if the expression is a constant expression, the program is ill-formed;
-   otherwise, an allocation function is not called;
-   if the allocation function that would have been called is a non-throwing exception specification (18.4), the value of the new-expression is the null pointer value of the required result type;
-   otherwise, the new-expression terminates by throwing an exception of a type that would match a handler (18.3) of type std::bad_array_new_length (21.6.3.2).

When the value of the new-expression is zero, the allocation function is called to allocate an array with elements:

- A new-expression may store the object by calling an allocation function (6.7.4.1). If the new-expression terminates by throwing an exception, it may release storage by calling the deallocation function (6.7.4.2). If the allocated type is an array type, the allocation function's operator new and the deallocation function's operator delete[]; Note: An implementation may provide default definitions for the global allocation functions (6.7.4, 21.6.2.1, 21.6.2.2). A C++ program may provide alternative definitions of the allocation functions (20.5.4) and class-specific versions of them. If the set of allocation functions to be called is not only the global ones, the new-expression may include functions that do not perform allocation or deallocation; for example, see 21.6.2.3 —

If the new-expression has a unary : operator, the allocation function's name is looked up in the global scope. If the allocated type is a class T or array type, then the name, or if the allocated type is not a class type, it is looked up in the scope of T. If this lookup fails then the implementation provides, the allocation function's name is looked up in the global scope.

An implementation may omit to call a replaceable function (21.6.2.1, 21.6.2.2). When it does, the storage is provided by the implementation or provided by extending the allocation of another new-expression. The implementation may extend the allocation of a new-expression e1 to provide storage for another new-expression if the following would be true:

-   the evaluation of e1 is sequenced before the evaluation of e2, and
-   e2 is evaluated before it owns storage, and
-   both e1 and e2 invoke the same replaceable allocation function, and
-   if the allocation function called by e1 and e2 is throwing, any exceptions thrown in the evaluation of either e1 or e2 would first be caught in the same handler, and
-   the pointer produced by e1 and e2 are operands to delete-expressions, and
-   the evaluation of e2 is sequenced before the evaluation of delete-expression whose operand is the pointer produced by e1.

Example:
```cpp
void merge_ints(int x) {
  // These allocations are safe for merging:
  std::unique_ptr<char[]> a(new std::nothrow[x]);
  std::unique_ptr<char[]> b(new std::nothrow[x]);
  std::unique_ptr<char[]> c(new std::nothrow[x]);
  a.get(), b.get(), c.get();
}
```

§ 8.3.4 ISO/IEC 2017

# ISO/IEC 14882:2017(E)

```cpp
void mergeable(int x) {
    std::unique_ptr<char> a[8];
    try {
        // Merging this allocation would change its handler.
        std::unique_ptr<char> b(new std::nothrow[x]);
    } catch (const std::bad_alloc& e) {
        std::cerr << "Allocation failed: " << e.what() << std::endl;
        throw;
    }
}
```

11 When a new-expression calls an allocation function and the first argument of new-expression expresses the amount of space requested to the allocation function as type std::size_t. That shall be no less than the size of the object being created; it may be greater than the size of the object created only if the object is an array. For arrays of char, unsigned char, and std::byte, the difference between the result of the new-expression and the address returned by the allocation function is an integral multiple of the size of the array. [Note: because allocation functions are extended to return addresses that are appropriate for any type with fundamental alignment, this idiom of aligning character arrays into other types will be placed.] —

12 When a new-expression calls an allocation function and has been extended, the size argument to the call shall be no greater than the sum of the sizes specified above, plus the size if it has not been extended, plus any padding necessary to align the objects within the allocated memory.

13 The new-placement syntax is used to supply additional arguments to an allocation function; such an expression is called a new-expression.

14 Overload is performed on a function called by an argument list. The first argument is the amount of space requested, and has type std::size_t. If the type of the allocated object has alignment, the next argument is the type's alignment, and has type std::align_val_t. The new-placement syntax is used, the initializer-clauses in its expression-list are the succeeding arguments. If no matching function is found and the allocated object has alignment, the argument is removed from the argument list, and overload resolution is performed again.

15 Example:

-   operator new(size_T)) returns in one of the following:
    operator new(size(T), std::align_val_t(alignof(T)))
-   operator new(f, T) returns in one of the following:
    operator new(size(T), 2, f)
    operator new(size(T), std::align_val_t(alignof(T)), 2, f)
-   new T[5] returns in one of the following:
    operator new[](size(T) * 5 + x)
    operator new[](size(T) * 5 + x, std::align_val_t(alignof(T)))
-   new(2, f) T[5] returns in one of the following:
    operator new[](size(T) * 5 + x, 2, f)
    operator new[](size(T) * 5 + x, std::align_val_t(alignof(T)), 2, f)

Here, instance of x is a non-negative unspecified value representing array overhead; the result of the new-expression will be offset by the value returned by operator new[]. This overhead may be applied in all new-expressions, including the library function operator new(std::size_t, void*) and other placement allocation functions. The amount of overhead may vary from one invocation of new to another.

- Note: Unless an allocation function has a non-throwing exception (18.4), it fails to allocate storage using a std::bad_alloc exception (18.7.4, Clause 18.26.3.1); it returns a non-null pointer otherwise. If the allocation function has a non-throwing exception, it returns null. If the allocation function is a non-allocating function (21.6.2.2) that returns null, the behavior is undefined. Otherwise, if the allocation fails, the deallocation function shall not be called, and the value of the new-expression shall be null.

- Note: When the allocation function returns a value other than null, it must be a pointer to a block of storage for which the object has been reserved. The block of storage is to be appropriately aligned and of the requested size. The address of the created object will not be the same as that of the block if the object is an array.

A new-expression creates an object of type T initializes as follows:

-   If the new-initializer is omitted, the object is de-initialized (11.6). [Note: If no initialization is performed, the object has indeterminate value.]
-   Otherwise, the new-initializer is interpreted according to the initialization rules of 11 for de-initialization.

The invocation of the allocation function is sequenced before the evaluation of expressions in the new-expression. Initialization of the allocated object is sequenced before the value computation of the object's memory to be freed. [Note: This is appropriate when the allocation function does not allocate memory, otherwise]

If any part of the initialization described above terminates by throwing an exception and a deallocation function can be called for what was constructed, after which the exception continues to propagate in the new-expression. If no unambiguous deallocation function is found, propagating the exception does not cause the object's memory to be freed.

If the new-expression creates an object or array of class type, access and access control are done for the deallocation function to free the memory (15.5). If the new-expression creates an array of objects of class type, the destructor is potentially invoked (15.4).

If the new-expression begins with a :: the deallocation function's name is looked up in the global scope. If the allocated type is a class type T or array thereof, the deallocation function's name is looked up in the scope where T was defined, or if the allocated type is not a class type or array thereof, the deallocation function's name is looked up in the global scope.

A declaration of a placement deallocation function with parameters, and the declaration of a placement allocation function if it has the same number of parameters (11.3.5), all parameter types except the first identity. If the lookup finds a matching deallocation function, that function will be called; otherwise, no deallocation function will be called. If the lookup finds a suitable deallocation function with a parameter type std::size_t T (6.7.4.2) and that function, considered as a placement deallocation function, would have been selected as a match for the allocation function, a non-placement allocation function, the program is ill-formed. Use this to find the matching deallocation function (8.3.5) Example:

```cpp
struct S {
```

-   80) This may include evaluating a new-initializer/or a constructor.
