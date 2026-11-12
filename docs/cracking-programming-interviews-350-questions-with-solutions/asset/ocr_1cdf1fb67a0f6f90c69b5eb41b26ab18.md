```
```cpp
void f(D* pd)
{
    pd->v++;
    pd->s++;
    int i = pd->e;
    pd->a++;
}
```
```

# Solution of Question 179

Compiler error is:

```
```text
member_name_lookup1.cpp:22:9:
error: non-static member 'a' found in multiple
    base-class subobjects of type 'A':
        struct D -> struct B -> struct A
        struct D -> struct C -> struct A
        pd->a++;
             ^

member_name_lookup1.cpp:8:9:
note: member lookup found by ambiguous name lookup
        int a;
            ^

1 error generated.
```
```

+   - `pd->v++` is ok : only one `v` (virtual)
+   - `pd->s++` is also ok : only one `s` (static)
+   - `int i = pd->e` is also ok : only one `e` (enumerator)
+   - `pd->a++` is ambiguous because there are two `as` in D

A static member, a nested type or an enumerator defined in a base class T can unambiguously be found even if an object has more than one base class subobject of type T. Two base class subobjects share the non-static member subobjects of their common virtual base classes.

# *** Question 180      member lookup and virtual base

Review the program below.

Program 13.4: member lookup and virtual base

```
```cpp
struct V
{
    int f();
    int x;
};
```
```