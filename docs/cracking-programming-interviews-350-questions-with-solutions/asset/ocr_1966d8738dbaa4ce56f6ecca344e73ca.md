```
```text
using3.cpp:10:14:
error: using declaration cannot refer
to a template
      specialization
      using A::func<double>;
      -------
using3.cpp:12:14:
error: using declaration cannot refer
to a template
      specialization
      using A::B<int>;
      -----
2 errors generated.
```
```

The reason is simple : a using-declaration cannot be used to name a template-id.

# *** Question 130    using declaration and member decl

What is problem with this code ?

Program 11.11: using declaration and member declaration

```
```cpp
1 struct A
2 {
3     int i;
4     static int si;
5 };
6
7 void f()
8 {
9     using A::i;
10    using A::si;
11 }
```
```

# Solution of Question 130

This program results into a compiler error :

```
```text
using4.cpp:9:14:
error: using declaration cannot refer to
class member
      using A::i;
      ---
using4.cpp:10:14:
error: using declaration cannot refer to
```
```