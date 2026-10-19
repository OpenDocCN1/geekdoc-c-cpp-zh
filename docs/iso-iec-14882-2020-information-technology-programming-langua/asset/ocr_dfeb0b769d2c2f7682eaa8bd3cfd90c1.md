# 20.14.17.2 Class bad_function_call [func.wrap.badcall]

1 An exception of type bad_function_call is thrown by function::operator() (20.14.17.3.5) when the function wrapper object has no target.

```
namespace std {
  class bad_function_call : public exception {
  public:
    // see 17.9.3 for the specification of the special member functions
    const char* what() const noexcept override;
  };
}
```

```
const char* what() const noexcept override;
```

2 Returns: An implementation-defined NTBS.

# 20.14.17.3 Class template function [func.wrap.func]

# 20.14.17.3.1 General [func.wrap.func.general]

```
namespace std {
  template<class> class function;      // not defined

  template<class R, class... ArgTypes>
  class function<R(ArgTypes...)> {
  public:
    using result_type = R;

    // 20.14.17.3.2, construct/copy/destroy
    function() noexcept;
    function(nullptr_t) noexcept;
    function(const function&);
    function(function&&) noexcept;
    template<class F> function(F);

    function& operator=(const function&);
    function& operator=(function&&);
    function& operator=(nullptr_t) noexcept;
    template<class F> function& operator=(F&&);
    template<class F> function& operator=(reference_wrapper<F>) noexcept;

    ~function();

    // 20.14.17.3.3, function modifiers
    void swap(function&) noexcept;

    // 20.14.17.3.4, function capacity
    explicit operator bool() const noexcept;

    // 20.14.17.3.5, function invocation
    R operator()(ArgTypes...) const;

    // 20.14.17.3.6, function target access
    const type_info& target_type() const noexcept;
    template<class T> T* target() noexcept;
    template<class T> const T* target() const noexcept;
  };

  template<class R, class... ArgTypes>
    function(R(*)(ArgTypes...)) -> function<R(ArgTypes...)>;

  template<class F> function(F) -> function<see below>;

  // 20.14.17.3.7, null pointer comparison operator functions
  template<class R, class... ArgTypes>
    bool operator==(const function<R(ArgTypes...)>&, nullptr_t) noexcept;
```