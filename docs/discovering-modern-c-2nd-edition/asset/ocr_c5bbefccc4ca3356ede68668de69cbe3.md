+   1. What is the static type of `pr` or `pp`? That is, how is `pr` or `pp` declared?
+   2. Is there a function named `all_info` in that class?
+   3. Can it be accessed? Or is it `private`?
+   4. Is it a `virtual` function? Otherwise just call it.
+   5. What is the dynamic type of `pr` or `pp`? That is, what is the type of the object referred to by `pr` or `pp`?
+   6. Call `all_info` from that dynamic type.

To realize these dynamic function calls, the compiler maintains _Virtual Function Tables_ (a.k.a. _Virtual Method Tables_) or short _Vtables_. They contain function pointers through which each virtual method of the actual object is called. The reference `pr` has the type `person&` and refers to an object of type `student`. In this case, the `all_info` entry in the vtable contains a function pointer to `student::all_info`, which is executed when `pr.all_info()` is called. This indirection over function pointers adds some extra cost to `virtual` functions which is significant for tiny functions and negligible for sufficiently large functions.

# Definition 6-2. (Late Binding and Dynamic Polymorphism).

Selecting the executed method during run time is called _Late Binding_ or _Dynamic Binding_. It also represents _Dynamic Polymorphism_—as opposed to static polymorphism with templates.

Analogously to the reference `pr`, the pointer `pp` points to a `student` object, and `student::all_info` is called by late binding for `pp->all_info()`. We can also introduce a free function `spy_on()` that provides Tom’s complete information thanks to late binding even when we pass a reference to the base class:

```
void spy_on(const person & p)
{
    p.all_info();
}
```

The benefit of dynamic selection is that the code exists only once in the executable no matter for how many sub-classes of `person` it is called. Another advantage over function templates is that only the declaration (i.e.,