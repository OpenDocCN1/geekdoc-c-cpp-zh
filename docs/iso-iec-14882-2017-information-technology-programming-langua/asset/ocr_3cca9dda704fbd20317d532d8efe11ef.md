# ISO/IEC 14882:2017(E)

template<class... UnboundArgs>
 R operator()(UnboundArgs&&... unbound_args) cu-qual;
-- end note

# 23.14.4 Function template invoke [func.invoke]

```
template <class F, class... Args>
invoke_result_t<F, Args...> invoke(F&& f, Args&&... args)
noexcept(is_nothrow_invocable_v<F, Args...>)
Returns: INVOKE(std::forward<F>(f), std::forward<Args>(args)...)) (23.14.3).
```

# 23.14.5 Class template reference_wrapper [refwrap]

```
namespace std {
  template <class T> class reference_wrapper {
  public:
    // types
    using type = T;

    // construct/copy/destroy
    reference_wrapper(T&&) noexcept;
    reference_wrapper(T&&) = delete; // do not bind to temporary objects
    reference_wrapper(const reference_wrapper& x) noexcept;

    // assignment
    reference_wrapper& operator=(const reference_wrapper& x) noexcept;

    // access
    operator T() const noexcept;
    T& get() const noexcept;

    // invocation
    template<class... ArgTypes>
    invoke_result_t<class..., ArgTypes...> operator()(reference_wrapper<T>&&, ArgTypes...) const;
  }
```

reference_wrapper<T> is a CopyConstructible and CopyAssignable wrapper around a reference to an object or function of type T.

reference_wrapper<T> should be a trivially copyable type (6.9).

# 23.14.5.1 reference_wrapper construct/copy/destroy [refwrap.const]

reference_wrapper(T&&) noexcept;

> Effects: Constructs a reference_wrapper object that stores a reference to t.

reference_wrapper(const reference_wrapper& x) noexcept;

> Effects: Constructs a reference_wrapper object that stores a reference to x.get().

# 23.14.5.2 reference_wrapper assignment [refwrap.assign]

reference_wrapper& operator=(const reference_wrapper& x) noexcept;