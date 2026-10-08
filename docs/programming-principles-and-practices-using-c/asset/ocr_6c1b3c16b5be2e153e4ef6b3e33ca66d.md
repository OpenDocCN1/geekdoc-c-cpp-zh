In the second example, `const_cast` strips the `const` from the `const Buffer*` called `p`. Presumably, we know what we are doing.

At least `static_cast` can’t mess with the pointer/integer distinction or with “const-ness,” so prefer `static_cast` if you feel the need for a cast. When you think you need a cast, reconsider: Is there a way to write the code without the cast? Is there a way to redesign that part of the program so that the cast is not needed? Unless you are interfacing to other people’s code or to hardware, there usually is a way. If not, expect subtle and nasty bugs. Don’t expect code using `reinterpret_cast` to be portable.

# ## 17.9 Pointers and references

You can think of a reference as an automatically dereferenced immutable pointer or as an alternative name for an object. Pointers and references differ in these ways:

+   - Assignment to a pointer changes the pointer’s value (not the pointed-to value).
- To get a pointer you generally need to use `new` or `&`.
- To access an object pointed to by a pointer you use `*` or `[]`.
- Assignment to a reference changes the value of the object referred to (not the reference itself).
- You cannot make a reference refer to a different object after initialization.
- Assignment of references does deep copy (assigns to the referred-to object); assignment of pointers does not (assigns to the pointer object itself).
- Beware of null pointers.

For example:

```
```cpp
int x = 10;
int* p = &x;    // you need & to get a pointer
*p = 7;         // use * to assign to x through p
int x2 = *p;    // read x through p
int* p2 = &x2;  // get a pointer to another int
p2 = p;         // p2 and p both point to x
p = &x2;        // make p point to another object
```
```

The corresponding example for references is

```
```cpp
int y = 10;
int& r = y;      // the & is in the type, not in the initializer
r = 7;          // assign to y through r (no * needed)
int y2 = r;     // read y through r (no * needed)
```
```