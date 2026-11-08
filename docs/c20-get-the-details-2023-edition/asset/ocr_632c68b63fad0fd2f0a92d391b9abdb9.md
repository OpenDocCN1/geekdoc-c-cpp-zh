# ### 4.1.7.2.4 Comparison Concepts

+   * `std::equality_comparable`
+   * `std::totally_ordered`

Maybe you know it from your mathematics studies. For values a, b, and c of type T, T models std::totally_ordered if and only if

+   * Exactly one of bool(a < b), bool(a > b), or bool(a == b) is true
+   * If bool(a < b) and bool(b < c), then bool(a < c)
+   * bool(a > b) == bool(b < a)
+   * bool(a <= b) == !bool(b < a)
+   * bool(a >= b) == !bool(b < a)

# ### 4.1.7.2.5 Object Concepts

+   * `std::movable`
+   * `std::copyable`
+   * `std::semiregular`
+   * `std::regular`

Here are the concise definitions of the four concepts:

```
```cpp
template<class T>
concept movable = is_object_v<T> && move_constructible<T> &&
                  assignable_from<T&, T> && swappable<T>;

template<class T>
concept copyable = copy_constructible<T> && movable<T> &&
                   assignable_from<T&, T&> &&
                   assignable_from<T&, const T&> && assignable_from<T&, const T>;

template<class T>
concept semiregular = copyable<T> && default_initializable<T>;

template<class T>
concept regular = semiregular<T> && equality_comparable<T>;
```
```

I have to add a few words. The concept std::movable requires for T that std::is_object_v<T> holds. From the definition of the type-trait std::is_object_v<T>, this means that T is either a scalar, an array, a union, or a class.

I implement the concept semiregular and regular in the section define concepts. Informally, a semiregular type behaves similarly to an int, and a regular type behaves similarly to an int and can be compared using ==.