Click here to view code image

```
D* dbp = dynamic_cast<D*>(bbp); // Error: cannot down-cast to
D
D* ddp = dynamic_cast<D*>(bdp); // Okay: bdp points to a D
object.
```

When the cast cannot be performed, a null pointer is returned so that the programmer can eventually react to the failed down-cast. Incorrect down-casts of references throw exceptions of type std::bad_cast and can be handled in a try-catch-block. These checks are realized with Run-Time Type Information (RTTI) and take a little extra time.

**Advanced background information:** dynamic_cast is implemented under the hood as a virtual function. Therefore, it is only available when the user has made a class polymorphic by defining at least one virtual function. Otherwise, all classes would incur the cost of a vtable. Polymorphic classes have this anyway, so the cost of the dynamic_cast is one extra pointer in the vtable.

# 6.5.1.3 Cross-Casting

An interesting feature of dynamic_cast is casting across from B to C when the referenced object's type is a derived class of both types:

Click here to view code image

```
C* cdp = dynamic_cast<C*>(bdp); // Okay: B -> C with D object
```

Likewise, we could cross-cast from student to mathematician. Static cross-casting from B to C:

Click here to view code image

```
cdp = static_cast<C*>(bdp); // Error: neither sub-nor super-class
```

is not allowed because C is neither a base nor a derived class of B. It can be casted indirectly:

Click here to view code image

```
cdp = static_cast<C*>(static_cast<D*>(bdp)); // B -> D -> C
```

Here again it is the programmer's responsibility to determine whether the addressed object can really be casted this way.