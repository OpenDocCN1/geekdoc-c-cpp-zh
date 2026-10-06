# ISO/IEC 14882:2017(E)

interpreted the requested size of an allocation. An allocation function can be a template. Such a template should declare its return type and parameter as specified above (that is, template types should not be used in the return type and first parameter type). Allocation functions shall have two or more parameters.

The allocation function attempts to allocate the requested amount of storage. If it is successful, it returns the address of a block of storage whose length in bytes shall be at least as large as the requested size. There are no constraints on the contents of the allocated storage return from the allocation function. The order, contingency, and initial value of storage allocated by successive calls to allocation functions is unspecified. The pointer returned to the caller can be converted to any suitable object type (21.6.2.1) and then used to access the object or array in the storage. Even if the space is requested, the request is valid until a call to a deallocation function. If the request fails, the returned value shall be a non-null pointer (21.71) or any previously returned value, unless value v was subsequently passed to an operator delete. Furthermore, for the library functions 21.6.2.1 and 21.6.2.2, p shall represent the address of storage from any other object except access by the caller. The effect of indirection through a pointer to such deallocation is undefined.³38

An allocation function that fails to allocate storage may invoke the newly installed new-handler function (21.6.3.3), using the std::get_new_handler function (21.6.3.4) — end note. If an allocation function with a non-throwing exception (8.4) fails to allocate storage, it shall return a null pointer. Other allocation functions that fail to allocate storage shall fail only by throwing an exception (8.1) of a type specified by the caller (18.3), such as std::bad_alloc (21.6.4.1).

A global allocation function is called to report an exception (8.4), or used directly by calling the allocation function in the C++ standard library. [Note: In particular, a global allocation function is not called to allocate storage for objects with storage duration (6.7.1), for references or objects with static storage duration (6.7.2), for objects of type std::type (8.2.8), or for an exception (18.1) — end note][basic.stc.dynamic_deallocation]

# 6.7.4.2 Deallocation functions

Deallocation functions shall be class member functions or global functions; a function is ill-formed if deallocation functions are declared in a namespace other than global scope or declared in global scope.

Each deallocation function shall return void and its first parameter shall be void. A usual deallocation function may have more than one parameter. A usual deallocation function has that:

+   - exactly one parameter;

+   - two parameters, the second of being either std::align_val_t or std::size_t;39); or

+   - three parameters, the second of being std::size_t and the third of being std::align_val_t;

A deallocation function may be an instance of a template. Neither the first nor the return type shall depend on a template parameter. [Note: a deallocation function shall have a first parameter of type void and a return type of void (as specified above). end note] A deallocation template shall have two or more function parameters. A template instance is never a usual deallocation function, regardless of its signature.

> 38 The intent is to have operator delete implement by calling malloc(0) or std::calloc(), so the rules are analytically the same: C++ differs from C in requiring a zero request to return a non-null pointer.

> 39 The global operator delete(void*, std::size_t) precludes an allocation function void operator new(std::size_t, std::size_t) as a placement allocation function (C.3.2).

§ 6.7.4.2 ©/IEC 2017 – All rights reserved 72