
- `operator delete[]` is used to delete the memory previously allocated by `new[]`. If objects were previously allocated, then the destructor is called for each individual object. Be careful, though, when pointers to objects were allocated. If pointers to objects were allocated, the destructors of the objects to which the allocated pointers point won’t automatically be called. A pointer is a primitive type and so no further action is taken when it is returned to the common pool.

### 11.9.1 Overloading ‘new[]’

To overload `operator new[]` in a class (e.g., in the class String) add the following line to the class’s interface:

```cpp
void *operator new[](size_t size);
```

The member’s size parameter is implicitly provided and is initialized by C++’s run-time system to the amount of memory that must be allocated. Like the simple one-object operator new it should return a void *. The number of objects that must be initialized can easily be computed from size / sizeof(String) (and of course replacing String by the appropriate class name when overloading operator new[] for another class). The overloaded new[] may allocate raw memory using e.g., the default operator new[] or the default operator new:

```cpp
void *operator new[](size_t size)
{
    return ::operator new[](size);
    // alternatively:
    // return ::operator new(size);
}
```

Before returning the allocated memory the overloaded operator new[] has a chance to do something special. It could, e.g., initialize the memory to zero-bytes.

Once the overloaded operator new[] has been defined, it is automatically used in statements like:

```cpp
String *sp = new String[12];
```

Like operator new additional overloads of operator new[] may be defined. One opportunity for an operator new[] overload is overloading placement new specifically for arrays of objects. This operator is available by default but becomes unavailable once at least one overloaded operator new[] is defined. Implementing placement new is not difficult. Here is an example, initializing the available memory to 0-bytes before returning:

```cpp
void *String::operator new[](size_t size, char *memory)
{
    return memset(memory, 0, size);
}
```

To use this overloaded operator, the second parameter must again be provided, as in:

```cpp
char buffer[12 * sizeof(String)];
String *sp = new(buffer) String[12];
```

### 11.9.2 Overloading ‘delete[]’

To overload `operator delete[]` in a class String add the following line to the class’s interface:

```cpp
void operator delete[](void *memory);
```

Its parameter is initialized to the address of a block of memory previously allocated by String::new[].

There are some subtleties to be aware of when implementing operator delete[]. Although the addresses returned by new and new[] point to the allocated object(s), there is an additional size_t value available immediately before the address returned by new and new[]. This size_t value is part of the allocated block and contains the actual size of the block. This of course does not hold true for the placement new operator.

When a class defines a destructor the size_t value preceding the address returned by new[] does not contain the size of the allocated block, but the number of objects specified when calling new[]. Normally that is of no interest, but when overloading operator delete[] it might become a useful piece of information. In those cases operator delete[] does not receive the address returned by new[] but rather the address of the initial size_t value. Whether this is at all useful is not clear. By the time the delete[]'s code is executed all objects have already been destroyed, so operator delete[] is only to determine how many objects were destroyed, but the objects themselves cannot be used anymore.

Here is an example showing this behavior of operator delete[] for a minimal Demo class:

```cpp
struct Demo
{
    size_t idx;
    Demo()
    {
        cout << "default cons\n";
    }
    ~Demo()
    {
        cout << "destructor\n";
    }
    void *operator new[](size_t size)
    {
        return ::operator new(size);
    }
    void operator delete[](void *vp)
    {
        cout << "delete[] for: " << vp << '\n';
        ::operator delete[](vp);
    }
};

int main()
{
    Demo *xp;
    cout << ((int *) (xp = new Demo[3]))[-1] << '\n';
    cout << xp << '\n';
    cout << "====================\n";
    delete[] xp;
}
// This program displays (your 0x?????? addresses might differ, but
// the difference between the two should be sizeof(size_t)):
// default cons
// default cons
// default cons
// 3
// 0x8bdd00c
// ====================
// destructor
// destructor
// destructor
// delete[] for: 0x8bdd008
```

Having overloaded operator `delete[]` for a class String, it will be used automatically in statements like:

```cpp
delete[] new String[5];
```

Operator `delete[]` may also be overloaded using an additional `size_t` parameter:

```cpp
void operator delete[](void *p, size_t size);
```

Here size is automatically initialized to the size (in bytes) of the block of memory to which void *p points. If this form is defined, then void operator delete[](void *) should not be defined, to avoid ambiguities. An example of this latter form of operator delete[] is:

```cpp
void String::operator delete[](void *p, size_t size)
{
    cout << "deleting " << size << " bytes\n";
    ::operator delete[](p);
}
```

Additional overloads of operator `delete[]` may be defined, but to use them they must explicitly be called as static member functions (cf. chapter 8). Example:

```cpp
// declaration:
void operator delete[](void *p, ostream &out);
// usage:
String *xp = new String[3];
String::operator delete[](xp, cout);
```

### 11.9.3 ‘new[]’, ‘delete[]’ and exceptions

When an exception is thrown while executing a `new[]` expression, what will happen? In this section we’ll show that `new[]` is exception safe even when only some of the objects were properly constructed.

To begin, new[] might throw while trying to allocate the required memory. In this case a `bad_alloc` is thrown and we don’t leak as nothing was allocated.

Having allocated the required memory the class’s default constructor is going to be used for each of the objects in turn. At some point a constructor might throw. What happens next is defined by the C++ standard: the destructors of the already constructed objects are called and the memory allocated for the objects themselves is returned to the common pool. Assuming that the failing constructor offers the basic guarantee `new[]` is therefore exception safe even if a constructor may throw.

The following example illustrates this behavior. A request to allocate and initialize five objects is made, but after constructing two objects construction fails by throwing an exception. The output shows that the destructors of properly constructed objects are called and that the allocated *substrate* memory is properly returned:

```cpp
#include <iostream>
using namespace std;

static size_t count = 0;

class X
{
    int x;
public:
    X()
    {
        if (count == 2)
            throw 1;
        cout << "Object " << ++count << '\n';
    }
    ~X()
    {
        cout << "Destroyed " << this << "\n";
    }
    void *operator new[](size_t size)
    {
        cout << "Allocating objects: " << size << " bytes\n";
        return ::operator new(size);
    }
    void operator delete[](void *mem)
    {
        cout << "Deleting memory at " << mem << ", containing: " <<
            *reinterpret_cast<int *>(mem) << "\n";
        ::operator delete(mem);
    }
};

int main()
try
{
    X *xp = new X[5];
    cout << "Memory at " << xp << '\n';
    delete[] xp;
}
catch (...)
{
    cout << "Caught exception.\n";
}
// Output from this program (your 0x??? addresses might differ)
// Allocating objects: 24 bytes
// Object 1
// Object 2
// Destroyed 0x8428010
// Destroyed 0x842800c
// Deleting memory at 0x8428008, containing: 5
// Caught exception.
```

## 11.10 Function Objects

Function Objects are created by overloading the *function call operator* `operator()`. By defining the function call operator an object masquerades as a function, hence the term *function objects*. Function objects are also known as *functors*.

Function objects are important when using *generic algorithms*. The use of function objects is preferred over alternatives like pointers to functions. The fact that they are important in the context of generic algorithms leaves us with a didactic dilemma. At this point in the C++ Annotations it would have been nice if generic algorithms would already have been covered, but for the discussion of the generic algorithms knowledge of function objects is required. This bootstrapping problem is solved in a well known way: by ignoring the dependency for the time being, for now concentrating on the function object concept.
