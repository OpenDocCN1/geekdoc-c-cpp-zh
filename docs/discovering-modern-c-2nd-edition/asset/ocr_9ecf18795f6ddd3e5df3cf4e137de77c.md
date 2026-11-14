Now we can entertain ourselves with subsets of the five overloads. First, we could omit drop c1::f; it did not matter anyway. What would happen if we also omitted c1:c2::f? Then the situation would be clear: f1::f2::f would be called. What if we kept c1::c2::f and removed f1::f2::f? The situation would be ambiguous: between c1::c2::f and f1::f, which would be visible now?

So far, all overloads have the same argument type. Let us consider the scenario where the global f takes a non-const reference:

Click here to view code image

```
void f(cl::c2::cc& o) {}
```

```
namespace f1 {
 void f(const cl::c2::cc& o) {}
 namespace f2 {
  void f(const cl::c2::cc& o) {}
  void g() {
   cl::c2::cc o;
   f(o);
  }
 } // namespace f2
} // namespace f1
```

Regarding overload resolution, the global f is the best match. However, it is still hidden by f1::f2::f despite the different signatures. In fact, everything (class, namespace) named f would hide the function f.

# Name Hiding

Any item (function, class, type definition) from an outer namespace is invisible whenever the same name is used in an inner namespace— even if the name is used for something entirely different.

To make the global f visible for g, we can apply a using declaration:

Click here to view code image

```
void f(cl::c2::cc& o) ()

namespace f1 {
 void f(const cl::c2::cc& o) {}
 namespace f2 {
```