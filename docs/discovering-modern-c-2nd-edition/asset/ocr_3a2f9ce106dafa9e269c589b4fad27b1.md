Let us jump into it and start with a challenging example. For conciseness, we choose short names: c1 and c2 for the namespaces containing a class and f1 and f2 containing the calling function:

Click here to view code image

```
```cpp
namespace c1 {
namespace c2 {
struct cc {};
void f(const cc& o) {}
} // namespace c2
void f(const c2::cc& o) {}
} // namespace c1

void f(const c1::c2::cc& o) {}

namespace f1 {
void f(const c1::c2::cc& o) {}
namespace f2 {
void f(const c1::c2::cc& o) {
{
c1::c2::cc o;
f(o);
}
} // namespace f2
} // namespace f1
```
```

Now the evil question: Which f is called in f1::f2::g? Let us look at each overload first:

+   - c1::c2::f: is a candidate by ADL;
+   - c1::f: is no candidate as ADL does not consider outer namespaces;
+   - f: lies in the outer namespace of g but is hidden by f1::f2::f;
+   - f1::f: same as f; and
+   - f1::f2::f: is a candidate because it is in the same namespace as f1::f2::g.

At least, we could rule out three of five overloads and have only c1::c2::f and f1::f2::f left. There remains the question of which overload is prioritized. The answer is none; the program is ambiguous.