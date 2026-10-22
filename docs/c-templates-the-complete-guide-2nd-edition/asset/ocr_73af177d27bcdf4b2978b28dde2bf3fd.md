} the enable_if construct expands to this second argument if the expression yields true. So, if MyType is the concrete type passed or deduced as T, whose size is larger than 4, the effect is MyType foo();

Note that having the enable_if expression in the middle of a declaration is pretty clumsy. For this reason, the common way to use std::enable_if<> is to use an additional function template argument with a default value: Click here to view code image

```
template<typename T,
typename = std::enable_if_t<(sizeof(T) > 4)>>
void foo() {
}
```

which expands to

Click here to view code image

```
template<typename T,
typename = void>
void foo() {
}
```

if sizeof(T) > 4.

If that is still too clumsy, and you want to make the requirement/constraint more explicit, you can define your own name for it using an alias template:⁵

Click here to view code image

```
template<typename T>
using EnableIfSizeGreater4 = std::enable_if_t<(sizeof(T) > 4)>;
```

```
template<typename T,
typename = EnableIfSizeGreater4<T>>
void foo() {
}
```

See Section 20.3 on page 469 for a discussion of how std::enable_if is implemented.

# 6.4 Using enable_if<>

We can use enable_if<> to solve our problem with the constructor template introduced in Section 6.2 on page 95.

The problem we have to solve is to disable the declaration of the template constructor Click here to view code image