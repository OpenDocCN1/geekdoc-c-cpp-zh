+   - **inline**, indicating a desire to have function calls implemented by inlining the function body (§12.1.5)
+   - **constexpr**, indicating that it should be possible to evaluate the function at compile time if given constant expressions as arguments (§12.1.6)
+   - **noexcept**, indicating that the function may not throw an exception (§13.5.1.1)
+   - A linkage specification, for example, **static** (§15.2)
+   - **[[noreturn]]**, indicating that the function will not return using the normal call/return mechanism (§12.1.4)

In addition, a member function may be specified as:

+   - **virtual**, indicating that it can be overridden in a derived class (§20.3.2)
+   - **override**, indicating that it must be overriding a virtual function from a base class (§20.3.4.1)
+   - **final**, indicating that it cannot be overridden in a derived class (§20.3.4.2)
+   - **static**, indicating that it is not associated with a particular object (§16.2.12)
+   - **const**, indicating that it may not modify its object (§3.2.1.1, §16.2.9.1)

If you feel inclined to give readers a headache, you may write something like:

```
struct S {
[[noreturn]] virtual inline auto f(const unsigned long int *const) -> void const noexcept;
};
```

# 12.1.3 Function Definitions

Every function that is called must be defined somewhere (once only; §15.2.3). A function definition is a function declaration in which the body of the function is presented. For example:

```
void swap(int*, int*); // adeclaration
```

```
void swap(int * p, int*q) // adefinition {
int t = *p;
*p= *q;
*q=t;
}
```

The definition and all declarations for a function must specify the same type.
Unfortunately, to preserve C compatibility, a **const** is ignored at the highest level of an argument type. For example, this is two declarations of the same function:

```
void f(int); // type is void(int)
void f(const int); // type is void(int)
```

That function, **f()**, could be defined as:

```
void f(int x) { /*wecan modify x here*/ }
```

Alternatively, we could define **f()** as:

```
void f(const int x) { /*wecannot modify x here*/ }
```

In either case, the argument that **f()** can or cannot modify is a copy of what a caller provided, so there is no danger of an obscure modification of the calling context.