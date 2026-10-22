# 12.4.6 Fold Expressions

A recurring pattern in programming is the *fold* of an operation on a sequence of values. For example, a *right fold* of a function fn over a sequence x[1], x[2], ..., x[n-1], x[n] is given by `fn(x[1], fn(x[2], fn(..., fn(x[n-1], x[n])...)))` While exploring a new language feature, the C++ committee ran into the need to deal with such constructs for the special case of a logical binary operator (i.e., `&&` or `||`) applied to a pack expansion. Without an extra feature, we might write the following code to achieve that for the `&&` operator: [Click here to view code image](#)

```
```cpp
bool and_all() { return true; }
template<typename T>
bool and_all(T cond) { return cond; }
template<typename T, typename... Ts>
bool and_all(T cond, Ts... conds) {
  return cond && and_all(conds...);
}
```
```

With C++17, a new feature called *fold expressions* was added (see Section 4.2 on page 58 for an introduction). It applies to all binary operators except `,`, `->*`, and `[]`.

Given an unexpanded expression pattern *pack* and a nonpattern expression *value*, C++17 allows us to write for any such operator *op*, either `(pack op ... op value)` for a right fold of the operator (called a *binary right fold*), or `(value op ... op pack)` for a left fold (called a *binary left fold*). Note that the parentheses are required here. See Section 4.2 on page 58 for some basic examples.

The fold operation applies to the sequence that results from expanding the pack and adding `value` as either the last element of the sequence (for a right fold) or the first element of the sequence (for a left fold).

With this feature available, code like

[Click here to view code image](#)

```
```cpp
template<typename... T> bool g() {
  return and_all(trait<T>()...);
}
```
```

(where `and_all` is as defined above), can instead be written as [Click here to view code image](#)

```
```cpp
template<typename... T> bool g() {
  return (trait<T>() && ... && true);
}
```
```