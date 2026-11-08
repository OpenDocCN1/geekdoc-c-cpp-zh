```
```cpp
    std::cout << '\n';
}
```
```

Now, the value of counter is as expected:

![](bbox=[0.4, 0.25, 0.61, 0.39])

The expected result with `std::atomic_ref`

In keeping with `std::atomic`<sup>19</sup>, type `std::atomic_ref` can be specialized and supports specializations for the built-in data types.

# ### 6.2.1.2 Specializations of `std::atomic_ref` (C++20)

You can specialize `std::atomic_ref` for user-defined types, use partial specializations for pointer types, or full specializations for arithmetic types such as integral or floating-point types.

# #### 6.2.1.2.1 Primary Template

The primary template `std::atomic_ref` can be instantiated with a `TriviallyCopyable`<sup>20</sup> type T.

```
```cpp
struct Counters {
    int a;
    int b;
};

Counter counter;
std::atomic_ref<Counters> cnt(counter);
```
```

# #### 6.2.1.2.2 Partial Specializations for Pointer Types

The standard provides partial specializations for a pointer type: `std::atomic_ref<T*>`.

+   19. https://en.cppreference.com/w/cpp/atomic/atomic
+   20. https://en.cppreference.com/w/cpp/types/is_trivially_copyable