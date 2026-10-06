# ISO/IEC 14882:2017(E)

pointer.
Remarks: Default function called when any part of the initialization in a placement new-expression invokes the library's non-array placement operator new terminates by throwing an exception (8.3.4).

```
void operator delete[](void* ptr, void*) noexcept;
```

Effects: Intentionally performs no action.

Requires: If an initialization has strict pointer safety (6.7.4.3) then ptr shall be a safely-derived pointer.

Default function called when any part of the initialization in a placement new-expression invokes the library's array placement operator new terminates by throwing an exception (8.3.4).

# 21.6.2.4 Data races

+   For purposes of determining the existence of data races, the library versions of operator new, replacement versions of global operator new, the C standard library functions aligned_alloc, calloc, and malloc; the library versions of operator delete, replacement versions of operator delete, the C standard library free and the C standard libraryalloc shall not introduce a data race (20.5.9). All calls to allocate and deallocate particular of storage occur in a single total order, and each deallocation shall happen before (4.7) the next allocation (if any) in this order.

# 21.6.3 Storage allocation errors

# 21.6.3.1 Class bad_alloc

```
namespace std {
    class bad_alloc : public exception {
    public:
        bad_alloc() noexcept;
        bad_alloc(const bad_alloc&) noexcept;
        bad_alloc operator=(const bad_alloc&) noexcept;
        char* what() const noexcept override;
    };
};
```

+   The class bad_alloc defines the types of objects thrown as exceptions by the implementation to report a failure to allocate storage.

```
bad_alloc() noexcept;
```

Effects: Constructs an object of class bad_alloc.

```
bad_alloc(const bad_alloc&) noexcept;
bad_alloc operator=(const bad_alloc&) noexcept;
```

Effects: Copies an object of class bad_alloc.

```
char* what() const noexcept override;
```

Returns: An implementation-defined NTBS.

Remarks: The message may be a multibyte string (20.4.2.15.2), suitable for conversion and display as a wstring (24.3, 25.4.1.4).

# 21.6.3.2 Class bad_array_new_length

```
namespace std {
    class bad_array_new_length : public bad_alloc {
    public:
        bad_array_new_length() noexcept;
    };
```