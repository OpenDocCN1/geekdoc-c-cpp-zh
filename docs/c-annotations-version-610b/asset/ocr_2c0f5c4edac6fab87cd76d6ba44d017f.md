in Vehicle. The specific characteristics of virtual member functions would then only be available for Auto objects and for objects of classes derived from Auto. For a Vehicle pointer static binding would remain to be used. The effect of late binding is illustrated below:

```
Vehicle v(1200);                 // vehicle with mass 1200
Truck t(6000, 115,               // truck with cabin mass 6000, speed 115,
        "Scania", 15000);        // make Scania, trailer mass 15000
Vehicle *vp;                      // generic vehicle pointer

int main()
{
    vp = &v;                      // see (1) below
    cout << vp->mass() << '\n';

    vp = &t;                      // see (2) below
    cout << vp->mass() << '\n';

    cout << vp->speed() << '\n'; // see (3) below
}
```

Now that mass is defined virtual, late binding is used:

+   - at (1), `Vehicle::mass` is called.
+   - at (2) `Truck::mass` is called.
+   - at (3) a syntax error is generated. The member `speed` is no member of `Vehicle`, and hence not callable via a `Vehicle*`.

The example illustrates that when a pointer to a class is used *only the members of that class can be called.* These functions may or may not be virtual. A member’s virtual characteristic only influences the type of binding (early vs. late), not the set of member functions that is visible to the pointer.

Through virtual members derived classes can redefine the behavior performed by functions called from base class members or from pointers or references to base class objects. This redefinition of base class members by derived classes is called *overriding members.*

# 14.2  Virtual destructors

When an object ceases to exist the object’s destructor is called. Now consider the following code fragment (cf. section 13.1):

```
Vehicle *vp = new Land(1000, 120);

delete vp;            // object destroyed
```

Here `delete` is applied to a base class pointer. As the base class defines the available interface `delete vp` calls `~Vehicle` and `~Land` remains out of sight. Assuming that Land allocates memory a memory leak results. Freeing memory is not the only action destructors can perform. In general they may perform any action that’s necessary when an object ceases to exist. But here none of the actions defined by `~Land` are performed. Bad news....

In C++ this problem is solved by *virtual destructors.* A destructor can be declared virtual. When a base class destructor is declared virtual then the destructor of the actual class pointed to by a base