# ISO/IEC 14882:2017(E)

2 Placeholders should be defined as:

inline constexpr unspecified _t();
If they are not, they shall be declared as:
extern unspecified _1;

# 23.14.12 Function template mem_fn [func.memfn]

template<class R, class T> unspecified mem_fn(R T::pm) noexcept;
Returns: A simple call (23.14.2) that finds the expression in function(t, a2, ..., a_N) is equivalent to INVOKE(pm, t, a2, ..., a_N) (23.14.3).

# 23.14.13 Polymorphic function wrappers [func.wrap]

+   1 This subclass defines a polymorphic wrapper class that encapsulates arbitrary objects.

# 23.14.13.1 bad_function_call [func.wrap.badcall]

+   1 An exception of type bad_function_call is thrown by function::operator()(23.14.13.2.4) when the function wrapper object has no target.

```
namespace std {
    class bad_function_call : public exception {
    public:
        // 23.14.19.1, constructor
        bad_function_call() noexcept;
    };
}
```

# 23.14.13.1 bad_function_call constructor [func.wrap.badcall.const]

+   bad_function_call() noexcept;
1 Effects: Constructs a bad_function_call object.
2 Postconditions: what() returns an implementation-defined NBS.

# 23.14.13.2 Class template function [func.wrap.func]

```
namespace std {
    template<class> class... // not defined

    template<class B, class... ArgTypes>
    class function<R(ArgTypes...)> {
    public:
        using result_type = R;
        // 23.11.3.2.1, construct/destroy
        function() noexcept;
        function(nullptr_t) noexcept;
        function(const function& function);
        function(function&& function);
        template<class F> function(F);

        function operator=(const function& function);
        function& operator=(function&& function);
        function& operator=(nullptr_t) noexcept;
        template<class F> operator=(F&& function);
        template<class F> operator=(reference_wrapper<F>&) noexcept;
}
```

§ 23.14.13.2

©ISO/IEC 2017 - All rights reserved 667