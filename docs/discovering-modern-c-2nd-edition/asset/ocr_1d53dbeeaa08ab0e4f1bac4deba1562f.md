As you certainly have guessed, ::same refers to the type from the global namespace and c1::same to the name in c1. The member variable z has type c1::c2::same since the inner name hides the outer ones. Namespaces are brought out from inside out. If we add a namespace c1 in c2, this will hide the outer one with the same name and the type of y becomes incorrect:

Click here to view code image

```
struct same {};
namespace c1 {
    struct same {};
    namespace c2 {
        struct same {};
        namespace c1 {} // hides ::c1
        struct csame {
            ::same x;
            c1::same y; // Error: c1::c2::c1::same not
        };
        same z;
    } // namespace c2
} // namespace c1
```

Here, c1::same exists in the global namespace, but since c1 is hidden by c1::c2::c1, we cannot access it. We would observe similar hiding if we defined a class named c1 in namespace c2. We can avoid the hiding and be more explicit about the type of y by placing double colons in front of the namespace:

Click here to view code image

```
struct csame {
    ::c1::same y; // this is unique
};
```

This makes clear that we mean the name c1 in the global namespace and not any other name c1. Names of functions or classes that are often needed can be imported with a using declaration:

```
void fun( ... )
{
    using c1::c2::cc;
    cc x;
    ...
    cc y;
}
```