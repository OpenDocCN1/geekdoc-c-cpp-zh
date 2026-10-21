```
if constexpr (T::i == 42) {
    ...
}
}
instead of just:
    if constexpr (std::is_same_v<MyType, T> && T::i == 42) {
    ...
}
```

# 10.2.2 Other Compile-Time if Examples

# Perfect Return of a Generic Value

One application of compile-time if is the perfect forwarding of return values, where they have to be processed before they can be returned. Because decltype(auto) cannot be deduced for void when declaring a variable (as void is an incomplete type), you have to write something like the following:

tmpl/perfectreturn.hpp

```
#include <functional>  // for std::forward()
#include <type_traits>  // for std::is_same<> and std::invoke_result<>

template<typename Callable, typename... Args>
decltype(auto) call(Callable op, Args&&... args)
{
    if constexpr(std::is_void_v<std::invoke_result_t<Callable, Args...>>) {
        // return type is void:
        op(std::forward<Args>(args)...);
        ... // do something before we return
        return;
    }
    else {
        // return type is not void:
        decltype(auto) ret{op(std::forward<Args>(args)...)};
        ... // do something (with ret) before we return
        return ret;
    }
}
```

The return type declaration works for void but the declaration of ret does not, so we have to skip the use of ret in that case.