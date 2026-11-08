If you're in any doubt about the legitimacy of a static cast, you shouldn't use it. The success of an attempt to cast a pointer down a class hierarchy depends on the pointer containing the address of an object of the destination type. A static cast doesn't check whether this is the case, so if you attempt it in circumstances where you don't know what the pointer points to, you risk an undefined result. Therefore, when you want to cast down a hierarchy, you need to do it differently—in a way in which the cast can be checked at runtime.

# ## Dynamic Casts

A dynamic cast is a conversion that's performed at runtime. The `dynamic_cast<>()` operator performs a dynamic cast. You can only apply this operator to pointers and references to polymorphic class types, which are class types that contain at least one virtual function. The reason is that only pointers to polymorphic class types contain the information that the `dynamic_cast<>()` operator needs to check the validity of the conversion. This operator is specifically for the purpose of converting between pointers or references to class types in a hierarchy. Of course, the types you are casting between must be pointers or references to classes within the same class hierarchy. You can't use `dynamic_cast<>()` for anything else. We'll first discuss casting pointers dynamically.

# ## Casting Pointers Dynamically

There are two kinds of dynamic cast. The first is a “cast down a hierarchy,” from a pointer to a direct or indirect base type to a pointer to a derived type. This is called a downcast. The second possibility is a cast across a hierarchy; this is referred to as a crosscast. Figure 15-6 illustrates these.

![](bbox=[0.155, 0.5, 0.765, 0.7])

*Figure 15-6. Downcasts and crosscasts*

For a pointer, box, of type `Box*` that contains the address of a `CerealPack` object, you could write the downcast shown in Figure 15-6 as follows:

```
```cpp
Carton* carton {dynamic_cast<Carton*>(box)};
```
```