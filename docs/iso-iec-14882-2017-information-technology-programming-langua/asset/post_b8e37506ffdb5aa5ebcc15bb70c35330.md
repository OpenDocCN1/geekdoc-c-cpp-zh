
# ISO/IEC 14882:2017(E)

without the size parameter. [Note: The behavior below may change in the future, which will require both deallocation functions when replacing the allocation function. -- end note --]

Requires: ptr shall be a null pointer or its value shall represent the address of a block of memory allocated by a caller to (possibly replaced) operator new(std::size_t t, or operator new(std::size_t t, std::align_val t) which has not been invalidated by an intervening call to operator delete.

Requires: If an implementation has stricter pointer alignment (6.7.4.3) then ptr shall be a safety-derived pointer.

Requires: If the alignment argument is not present, ptr shall have been returned by an allocation function without an alignment parameter. If present, the alignment argument should equal the alignment argument passed to the allocation function that returned ptr. If present, the size argument shall equal the size argument passed to the allocation function that returned ptr.

Required: A call to an operator delete with a size parameter may be changed to the corresponding operator delete without a size parameter, without affecting memory. [Note: A conforming implementation for operator delete(void* ptr, std::size_t size) to supply operator delete(ptr). -- end note --]

Default: The functions that have a size parameter forward their other parameters to the corresponding function without a size parameter. [Note: See in the above Replaceable: paragraph. --]

Default: If ptr is null, nothing happens. Otherwise, reclaims the storage allocated by the caller to operator delete.

Remarks: It is uncertain whether what part of or if all of reclaimed storage shall be returned by subsequent calls to operator new or any of alloc, malloc, calloc, or realloc, from <cstdlib>

```
void delete(void* ptr, const std::size_t) noexcept;
void delete(void* ptr, const std::size_t, const std::align_val alignment) noexcept;
```

Effects: The deletion (6.7.4.2) called by the implementation may return the value of ptr invalid when the constructor invoked from a new placement of the new-expression throws an exception.

Replaceable: A C++ program may define functions with either of these function signatures, and they displace the default versions defined by the C++ standard library.

Requires: ptr shall be a null pointer or its value shall represent the address of a block of memory allocated by a caller to (possibly replaced) operator new(std::size_t t, or operator new(std::size_t t, std::align_val t) which has not been invalidated by an intervening call to operator delete.

Requires: If an implementation has stricter pointer alignment (6.7.4.3) then ptr shall be a safety-derived pointer.

Requires: If the alignment argument is not present, ptr shall have been returned by an allocation function without an alignment parameter. If present, the alignment argument should equal the alignment argument passed to the allocation function that returned ptr.

Default: Calls operator delete(ptr), or operator delete(ptr, alignment), respectively.

## 21.6.2.2 Array forms

```
void* operator new[](std::size_t size);
void* operator new[](std::size_t size, std::align_val alignment);
```

Effects: The allocation functions (6.7.4.1) called by a new-expression (8.3.4) to allocate bytes of storage. The second form is called for a type with extended-alignment, and allocates storage with the specified alignment. The first form is called otherwise, and allocates storage suitably aligned to represent any object of size or smaller, provided the object's type does not have extended-alignment.²¹⁸

2 Replaceable: A C++ program may define functions with either of these functions, and thereby displace the versions defined by the C++ standard library.

3 Required: Behavior as defined for the single-object forms. This requirement is binding on order any replacement versions of these functions.

4 Default: Behavior Returns operator new(size), or operator new(size, alignment), respectively.

```
void operator new[](std::size_t size, const std::nothrow& noexcept);
void operator new[](std::size_t size, std::align_val alignment, const std::nothrow& noexcept);
```

5 Effects: As above, except that are caused by a placement version of a new-expression when a C++ program may return a null pointer as an error indication, of a bad_alloc exception.

6 Required: A C++ program may define functions with either of these functions, and thereby displace the versions defined by the C++ standard library.

7 Required: Return a null-pointer to suitably aligned storage (6.7.4), or return a null pinter. Each of these another versions of operator new[] returns a pointer as acquired if from the (possibly) replacing non-placement function. This requirement is binding on any replacement versions of these functions.

8 Default: Behavior Calls operator new[](size), or operator new[](size, alignment), respectively. If the call returns null, the result of that call is. Otherwise, returns a null pointer.

```
void operator delete(void* ptr);
void operator delete(std::size_t size) noexcept;
void operator delete(std::size_t size, std::align_val alignment) noexcept;
void operator delete(std::size_t size, std::align_val alignment) noexcept;
```

9 Effects: The deallocations (6.7.4.2) called by the implementation of the new-expression returns the value of ptr.

10 Required: A C++ program may define functions with either of these functions, and thereby displace the versions defined by the C++ standard library. The provisions of 6.7.4 do not apply to these placement forms of the operator new and delete.

11 Required: ptr shall be a null pointer or its value shall represent the address of a block of memory allocated by a caller to (possibly replaced) operator new(std::size_t t, or operator new(std::size_t t, std::align_val t) which has not been invalidated by an intervening call to operator delete.

12 Required: If an implementation has stricter pointer alignment (6.7.4.3) then ptr shall be a safety-derived pointer.

13 Required: If the alignment argument is not present, ptr shall have been returned by an allocation function without an alignment parameter. If present, the alignment argument should equal the alignment argument passed to the allocation function that returned ptr. If present, the size argument shall equal the size argument passed to the allocation function that returned ptr.

14 Required: A call to an operator delete with a size parameter may be changed to the corresponding operator delete without a size parameter, without affecting memory. [Note: A conforming implementation for operator delete(void* ptr, std::size_t size) to supply operator delete(ptr). -- end note --]

15 Default: The functions that have a size parameter forward their other parameters to the corresponding function without a size parameter. [Note: See in the above Replaceable: paragraph. --]

16 Default: If ptr is null, nothing happens. Otherwise, reclaims the storage allocated by the caller to operator delete.

17 Remarks: It is uncertain whether what part of or if all of reclaimed storage shall be returned by subsequent calls to operator new or any of alloc, malloc, calloc, or realloc, from <cstdlib>

18 Effects: The deletion (6.7.4.2) called by the implementation may return the value of ptr invalid when the constructor invoked from a new placement of the new-expression throws an exception.

19 Replaceable: A C++ program may define functions with either of these function signatures, and they displace the default versions defined by the C++ standard library.

20 Required: ptr shall be a null pointer or its value shall represent the address of a block of memory allocated by a caller to (possibly replaced) operator new(std::size_t t, or operator new(std::size_t t, std::align_val t) which has not been invalidated by an intervening call to operator delete.

21 Required: If an implementation has stricter pointer alignment (6.7.4.3) then ptr shall be a safety-derived pointer.

22 Required: If the alignment argument is not present, ptr shall have been returned by an allocation function without an alignment parameter. If present, the alignment argument should equal the alignment argument passed to the allocation function that returned ptr.

23 Default: Calls operator delete(ptr), or operator delete(ptr, alignment), respectively.

## 21.6.2.3 Non-allocating functions

These functions are reserved; a C++ program may not define functions that displace the versions in the C++ standard library (20.5.4). The provisions of 6.7.4 do not apply to these reserved placement forms of the operator new and operator delete.
