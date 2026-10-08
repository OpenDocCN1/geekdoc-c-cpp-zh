# Storing Objects in C++ Collections 181

```
template <typename X>
struct object_equal {
    bool operator()(const X s1, const ( s2) const {
        return (s1==s2) || [(id)s1 isEqual:(id)s2];
    }
}
template <typename X>
struct object_hash {
    size_t operator()(const X s1) const {
        return (size_t)[(id)s1 hash];
    }
}
```

From: collection.mm

operation on a C++ collection may assign the pointer several times. This will result in a lot of retain and release operations, which the ARC optimizer will then remove where they are redundant. With a smart pointer class, they will generate a lot of message sends.
In C++ terminology, this means that __unsafe_retained id is a plain old data (POD) type, while __weak id and __strong id implement (implicitly) overloaded assignment operators and nontrivial copy constructors. If you don't understand what that means, then don't worry; just assume that you can use ARC in C++ and everything works