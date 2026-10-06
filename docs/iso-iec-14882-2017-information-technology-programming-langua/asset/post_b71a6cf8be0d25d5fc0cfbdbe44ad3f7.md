
# ISO/IEC 14882:2017(E)

sufficient, but not necessary, to satisfy these requirements. These requirements permit thread managers as static-storage-objects. — end note

- Calling the function std::abort() declared in <cstdlib> terminates the program without executing any destructors and without having the functions passed to std::atexit() or std::quick_exit().

## 6.7 Storage duration [basic.c]

- The storage duration is the property of an object that defines the minimum lifetime of the storage containing the object. The storage duration is determined by the construct used to create the object and one of the following:

- (1.1) static storage

- (1.2) thread storage duration

- (1.3) automatic storage duration

- (1.4) dynamic storage duration

- Static, thread, and automatic storage durations are associated with objects introduced by declarations (6.1) and implicitly created by a declaration (15.2). The dynamic storage duration is associated with objects created by a new-expression (8.3.4).

- The storage duration categories apply to references as well.

- When the end of a duration of region storage is reached, the values of all pointers representing the address of any part of that region become invalid pointers (6.9.2). Indirection through an invalid pointer and passing an invalid pointer to a deallocation function has undefined behavior. Any other use of an invalid pointer has implementation-defined behavior.³37

## 6.7.1 Static storage duration [basic.stc.static]

- All variables which have dynamic storage duration, do not have thread storage duration, and are local static storage duration. The entities shall last for the duration of the thread in which they are created (6.6.2, 6.4).

- If a variable with static storage has initialization or a destructor with side effects, it should not be eliminated if it appears to be used, except that a class object or its copy/move may be eliminated in 15.8.

- The keyword static can be used to declare a local variable with static storage duration. [Note: 9.7 describes the initialization of local static variables; 6.6.4 describes the destruction of local static variables. — end note]

- The keyword static used to declare a class member in a class definition has the data member static storage duration.

## 6.7.2 Thread storage duration [basic.stc.thread]

- All variables declared with the thread_local keyword have thread storage duration. The storage for these entities shall last for the duration of the thread in which they are created. There is a distinct object or reference per thread, and of the declared name refers to the entity associated with the current thread.

- A variable with thread storage duration shall be initialized before its first od-use (6.2) and, if constructed, shall be destroyed on thread exit.

> ³7 Some implementations might define copying an invalid pointer value causes a system-generated runtime fault.

## 6.7.3 Automatic storage duration [basic.stc.auto]

1 Block-scope variables not explicitly declared static, thread_local, or extern have automatic storage duration. The storage for these lasts until the block in which they are created. 9.7. — end note

2 [Note: These variables are initialized and destroyed as described in 9.7. — end note]

3 If a variable with automatic storage duration has initialization or a destructor with side effects, an implementation shall not destroy it before the end of the block nor eliminate an allocation, even if it appears to be unused, except a class object or its copy/move may be eliminated in 15.8.

## 6.7.4 Dynamic storage duration [basic.stc.dynamic]

1 Objects can be created dynamically during program execution (4.6), using new-expansions (8.3.4), and destroyed using deleting-expansions (8.3.5). A C++ implementation provides access to, and management of, dynamic storage via the global allocation functions new and operator new and the global deallocation functions operator delete and operator delete [Note: The non-allocating forms declared in 21.6.3 do not perform deallocation and may be eliminated].

2 The library defines default allocation and deallocation functions. Global allocation and deallocation functions are replaceable (21.6.2). A C++ program shall provide at least one definition of a replaceable allocation or deallocation function. Such function defines the default version used by the library (20.5.4.6). The following allocation and deallocation functions (21.6) are implicitly declared in global scope in each translation unit of a program.

```cpp
void operator new(std::size_t);
void operator new(std::size_t, std::align_val_t);

void operator delete(void*) noexcept;
void operator delete(void*, std::size_t) noexcept;
void operator delete(void*, std::size_t, std::align_val_t) noexcept;
```

These implicit declarations only function the names operator new, operator new[], operator delete, and operator delete[] [Note: The implicit declarations do not introduce the names std::size_t, std::align_val_t, or any other name that the library uses to declare these names. A new-expression, deletion-expression or function call to any of these without the header “new” is ill-formed unless the name has been declared including the appropriate header. — end note] Allocation and deallocation functions may also be declared and defined for any class (15.5).

3 Any allocation and/or deallocation functions in a C++ program, using the default versions in the library, shall conform to the semantics specified in 6.7.4.1 and 6.7.4.2.

### 6.7.4.1 Allocation functions [basic.stc.allocation]

1 An allocation function shall be a class member function or a global function; program is ill-formed if an allocation function is declared in a namespace other than global scope or declared static in global scope. The return type shall be void*. The first parameter shall have type std::size_t (21.2). The first parameter shall not have an associated default argument (11.3). The allocation function attempts to allocate the requested size. If it is successful, it returns a pointer to storage whose length is at least large as the requested size. An allocation function may fail by throwing an exception (8.1) of a type specified by the caller, such as std::bad_alloc (21.6.4). Other allocation functions that fail to allocate storage shall return a null pointer.

A global allocation function is called to report an exception, or used directly by the C++ library. [Note: In particular, a global allocation function is not called to allocate storage for storage duration (6.7.1), for objects with static storage duration (6.7.2), for objects of type (8.2), or for an exception (18.1) — end note]

### 6.7.4.2 Deallocation functions [basic.stc.dynamic_deallocation]

Deallocation functions shall be class member functions or global functions; a function is ill-formed if deallocation functions are declared in a namespace other than global scope or declared in global scope.

Each deallocation function shall return void and its first parameter shall be void. A usual deallocation function may have more than one parameter. A usual deallocation function has that:

- exactly one parameter;

- two parameters, the second being either std::align_val_t or std::size_t;39); or

- three parameters, the second being std::size_t and the third being std::align_val_t;

A deallocation function may be an instance of a template. Neither the first nor the return type shall depend on a template parameter. [Note: a deallocation function shall have a first parameter of type void and a return type of void (as specified above). end note] A deallocation template shall have two or more function parameters. A template instance is never a usual deallocation function, regardless of its signature.

> 38 The intent is to have operator delete implement by calling malloc(0) or std::calloc(), so the rules are analytically the same: C++ differs from C in requiring a zero request to return a non-null pointer.

> 39 The global operator delete(void*, std::size_t) precludes an allocation function void new(std::size_t, std::size_t) as a placement allocation function (C.3.2).

§ 6.7.4.2 ©/IEC 2017 – All rights reserved 72
