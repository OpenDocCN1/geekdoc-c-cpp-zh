```
is_unsigned<X>
is_constructible<X,args> is_default_constructible<X> is_copy_constructible<X>
is_move_constructible<X> is_assignable<X,Y>
is_copy_assignable<X> is_move_assignable<X> is_destructible<X>
```

For example:

```
template<typename T>
class Cont {
```

Is X a const?
Is X a volatile (§41.4)?
Is X a trivial type (§8.2.6)?
Can X be copied, moved, and destroyed as a simple collection of bits (§8.2.6)?
Is X a standard-layout type (§8.2.6)?
Is X a POD (§8.2.6)?
Does X have a constexpr constructor (§10.4.3)? Does X have a member that requires space in an object? Does X have a virtual function?
Does X have a pure virtual function?
Is X an arithmetic type and signed?
Is X an arithmetic type and unsigned?
Can an X be constructed from args?
Can an X be constructed from {}?
Can an X be constructed from an X&?
Can an X be constructed from an X&&?
Can a Y be assigned to an X?
Can a X& be assigned to an X?
Can a X&& be assigned to an X?
Can an X be destroyed (i.e., ~X() has not been deleted)?

```
T * elem; // store elements in an array pointed to by elem int sz; // sz elements
// ...
Cont(const Cont& a) // copy constructor
  :sz(a.sz), elem(new T[a.elem])
{
  static_assert(Is_copy_constructible<T>(), “Cont::Cont(): no copy”);
  if (Is_trivially_copyable<T>())
    memcpy(elem,a.elem,sz*sizeof(T)); // memcpy optimization
  else
    uninitialized_copy(a.begin(),a.end(),elem); // use copy constructors
  // ...
}
// ...
}
```

This optimization may be unnecessary, though, because uninitialized_copy() is likely to already have been optimized in this way.

For a class to be empty, it can have no virtual functions, no virtual bases, and no base classes for