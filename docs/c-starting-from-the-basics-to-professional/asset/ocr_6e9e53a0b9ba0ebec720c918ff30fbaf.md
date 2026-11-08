> **Tip**  If needed, you can safely revive a `move()`'d `vector<>` by calling its `clear()` member. After calling `clear()`, the `vector<>` is guaranteed to be equivalent to an empty `vector<>` again and thus safe for further use.

In the rare cases where you do want to reuse moved Standard Library objects, you should always check the specification of their move members. When a `std::optional<T>` object that contains a `T` value is moved, for instance, it will still contain a `T` value—that is now moved (we covered `std::optional<>` in Chapter 9). Similar to a `vector<>`, the `optional<>` can safely be reused after calling its `reset()` member. Smart pointers are a scarce exception:

> **Tip**  The Standard Library specification clearly stipulates that you may continue using smart pointers of type `std::unique_ptr<>` and `std::shared_ptr<>` after moving out the raw pointer, and this without first calling `reset()`. For both types, move operations must always set the encapsulated raw pointer to `nullptr`.

# # A Barrel of Contradictions

Many find move semantics confusing at first, and understandably so. We hope this section can somewhat spare you from this fate, as it aims to alleviate some of the most common sources of confusion.

# ## std::move() Does Not Move

Make no mistake, `std::move()` does not move anything. All this function does is turn a given lvalue into an rvalue reference. `std::move()` is effectively nothing more than a type conversion, not at all unlike built-in cast operators `static_cast<>` and `dynamic_cast<>`. In fact, you could almost implement your own version of the function simply like so (somewhat simplified):

```
```cpp
template <typename T>
T&& move(T&& x) noexcept { return static_cast<T&&>(x); }
```
```

Clearly, this means nothing. What it does, however, is make a persistent lvalue eligible for binding with the rvalue reference parameter of a move constructor or assignment operator. It’s these member functions that are then supposed to move the members of the former lvalue into another object. `std::move()` only performs a type cast to make the compiler pick the right function overload.

If no function or constructor overload exists with an rvalue reference parameter, an rvalue will happily bind with an lvalue reference instead. That is, you can `move()` all you want; but if there’s no function overload standing ready to receive the resulting rvalue, it’s all in vain.

To demonstrate this, we’ll again start from E18_04.cpp. As you may recall, this latest variant of our running example ended with these statements:

```
```cpp
...
Array<std::string> more_strings{ 2'000 };
strings = std::move(more_strings);    // Move more_strings into strings
}
```
```