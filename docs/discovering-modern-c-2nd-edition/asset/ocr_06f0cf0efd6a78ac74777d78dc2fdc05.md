One possibility to deal with name conflicts is using different names like abs, my_abs, or library_name_abs. This is in fact what is done in C. Broadly used libraries normally use short function names, user libraries use longer names, and OS-related internals typically start with _. This decreases the probability of conflicts, but not sufficiently. Namespaces are very important when we write our own classes and even more so when they are used in function templates. They allow us to hierarchically structure the names in our software. This avoids name clashes and provides sophisticated access control of function and class names.

Namespaces are similar to scopes regarding the fact that we can see the names in the enclosing namespaces:

```
struct global ();
namespace c1 {
    struct c1c {};
    namespace c2 {
        struct c2c {};
        struct cc {
            global x;
            c1c y;
            c2c z;
        };
    } // namespace c2
} // namespace c1
```

Names that are redefined in an inner namespace hide those of the outer ones. In contrast to blocks, the outer names aren’t lost for us but can still be used by Namespace Qualification:

```
struct same ();
namespace c1 {
    struct same {};
    namespace c2 {
        struct same {};
        struct csame {
            ::same x;
            c1::same y;
            same z;
        };
    }; // namespace c2
} // namespace c1
```