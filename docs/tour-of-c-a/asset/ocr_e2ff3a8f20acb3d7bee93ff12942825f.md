}

The implementation of views and pipelines involves some quite hair-raising template metaprogramming, if you are concerned about performance make make sure to measure whether your implementation delivers what you need. If not, there is always a conventional workaround around

Click here to view code image

```
void user(forward_range auto& r)
{
  int count = 0;
  for (int x : r) {
    cout << x << ' '';
    if (++count == 3) return;
  }
}
```

However, the logic of what's going on is obscured.

# 14.5 Concepts Overview

The standard library offers many useful concepts:

+   - Concepts defining properties of types (§14.5.1)
- Concepts defining iterators (§14.5.2)
- Concepts defining ranges (§14.5.3)

# 14.5.1 Type Concepts

The concepts relate to properties of types and the relations among them reflect the variety of types. These concepts help simplify templates.

| Core language concepts <concepts> T and U are types |
| same_as<T,U> | T is the same as U |
| derived_from<T,U> | T is derived from U |
| convertible_to<T,U> | A T can be converted to a U |
| common_reference_with<T,U> | T and U share a common reference type |
| common_with<T,U> | T and U share a common type |
| integral<T> | T is an integral type |
| signed_integral<T> | T is a signed integral type |
| unsigned_integral<T> | T is an unsigned integral type |
| floating_point<T> | T is a floating point type |
| assignable_from<T,U> | A U can be assigned to a T |