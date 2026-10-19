# 20.14.12 Class identity [func.identity]

```
struct identity {
    template<class T>
    constexpr T&& operator()(T&& t) const noexcept;

    using is_transparent = unspecified;
};
```

```
template<class T>
    constexpr T&& operator()(T&& t) const noexcept;
```

Effects: Equivalent to: return std::forward<T>(t);

# 20.14.13 Function template not_fn [func.not.fn]

```
template<class F> constexpr unspecified not_fn(F&& f);
```

In the text that follows:

+   - g is a value of the result of a not_fn invocation,
+   - FD is the type decay_t<F>,
+   - fd is the target object of g (20.14.3) of type FD, direct-non-list-initialized with std::forward<F>(f),
+   - call_args is an argument pack used in a function call expression (7.6.1.3) of g.

Mandates: is_constructible_v<FD, F> && is_move_constructible_v<FD> is true.

Preconditions: FD meets the Cpp17MoveConstructible requirements.

Returns: A perfect forwarding call wrapper g with call pattern !invoke(fd, call_args...).

Throws: Any exception thrown by the initialization of fd.

# 20.14.14 Function template bind_front [func.bind.front]

```
template<class F, class... Args>
    constexpr unspecified bind_front(F&& f, Args&&... args);
```

In the text that follows:

+   - g is a value of the result of a bind_front invocation,
+   - FD is the type decay_t<F>,
+   - fd is the target object of g (20.14.3) of type FD, direct-non-list-initialized with std::forward<F>(f),
+   - BoundArgs is a pack that denotes decay_t<Args>...,
+   - bound_args is a pack of bound argument entities of g (20.14.3) of types BoundArgs..., direct-non-list-initialized with std::forward<Args>(args)..., respectively, and
+   - call_args is an argument pack used in a function call expression (7.6.1.3) of g.

Mandates:
    is_constructible_v<FD, F> &&
    is_move_constructible_v<FD> &&
    (is_constructible_v<BoundArgs, Args> && ...) &&
    (is_move_constructible_v<BoundArgs> && ...)
    is true.

Preconditions: FD meets the Cpp17MoveConstructible requirements. For each T_i in BoundArgs, if T_i is an object type, T_i meets the Cpp17MoveConstructible requirements.

Returns: A perfect forwarding call wrapper g with call pattern invoke(fd, bound_args..., call_args...).

Throws: Any exception thrown by the initialization of the state entities of g (20.14.3).