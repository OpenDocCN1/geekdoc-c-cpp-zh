```
```cpp
{
    std::cout << "A::f()" << std::endl;
}
};
struct B : virtual A
{
    virtual void f()
    {
        std::cout << "B::f()" << std::endl;
    }
};
struct C : B, virtual A
{
    using A::f;
};
int main()
{
    C c;
    c.f();
    c.C::f();
}
```
```

# Solution of Question 181

It prints

```
```text
B::f()
A::f()
```
```

+   - `c.f()` calls `B::f` because of the final overrider
+   - `c.C::f()` calls `A::f` because of the using declaration

Virtual functions support dynamic binding and object-oriented programming. A class that declares or inherits a virtual function is called a *polymorphic class*.

If a virtual member function `vf` is declared in a class *Base* and in a class *Derived*, derived directly or indirectly from *Base*, a member function `vf` with the same name, parameter-type-list, cv-qualification, and ref-qualifier (or absence of same) as `Base::vf` is declared, then `Derived::vf` is also virtual (whether or not it is so declared) and it overrides `Base::vf`.

For convenience we say that any virtual function overrides itself.

A virtual member function `C::vf` of a class object `S` is a final overrider unless the most derived class of which `S` is a base class subobject (if any) declares or inherits another member function that overrides `vf`.