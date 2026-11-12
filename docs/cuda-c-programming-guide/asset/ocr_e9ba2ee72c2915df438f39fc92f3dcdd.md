# Example:

```
void foo(void) {
  // Error: __host____device__ extended lambdas cannot be
  // generic lambdas.
  auto lam1 = []__host____device__ (auto i) { return i; };
  // Error: __host____device__ extended lambdas cannot be
  // generic lambdas.
  auto lam2 = []__host____device__ (auto ...i) {
    return sizeof...(i);
  };
}
```

8. If the enclosing function is an instantiation of a function template or a member function template, and/or the function is a member of a class template, the template(s) must satisfy the following constraints:

+   - The template must have at most one variadic parameter, and it must be listed last in the template parameter list.
+   - The template parameters must be named.
+   - The template instantiation argument types cannot involve types that are either local to a function (except for closure types for extended lambdas), or are private or protected class members.