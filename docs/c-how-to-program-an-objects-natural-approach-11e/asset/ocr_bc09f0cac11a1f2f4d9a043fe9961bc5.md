# Coroutine Restrictions

According to the C++20 standard, the following kinds of functions cannot be coroutines:39

+   - `main`,
+   - constructors,
+   - destructors,
+   - `constexpr` and `consteval` functions,
+   - functions declared with **placeholder types** (`auto` or concepts) and
+   - functions with variable numbers of arguments.

# Promise Object

Every coroutine has a **promise object**40 that’s created when the coroutine is first called. It’s used by the coroutine to

+   - return a result to its caller or
+   - return an exception to its caller.

The **promise object** is part of the coroutine state. It provides several member functions:

+   - `get_return_object`—When the coroutine begins executing, it calls this function on the **promise object** to get the coroutine's **result object**, which will be returned to the coroutine's caller when the coroutine first suspends. The caller uses the **result object** to access the coroutine's result when it becomes available.
+   - `initial_suspend`—When the coroutine begins executing, it calls this function on the **promise object** to determine whether to immediately suspend (for **lazy coroutines**, like our `fibonacciGenerator` in Fig. 18.1) or continue executing (like our `sortCoroutine` coroutine in Fig. 18.3). The `<coroutine>` header provides types `suspend_always` and `suspend_never` to support these two possibilities.
+   - `unhandled_exception`—The coroutine calls this function on the **promise object** if an **unhandled exception** causes the coroutine to terminate.
+   - `return_void`—The coroutine calls this function on the **promise object** when execution reaches the coroutine's closing brace, a `co_return` statement with no expression or a `co_return` statement with an expression that evaluates to `void`. The **promise object** may define only `return_void` or `return_value`, but not both.
+   - `return_value`—The coroutine calls this function when a `co_return` statement contains a **non-void** expression. The **promise object** may define either `return_value` or `return_void`, but not both.

39. C++ Standard, Sections 6.9.3.1, 9.2.5, 9.2.8.5, 11.4.4, 11.4.6. Accessed April 18, 2023. https://timsong-cpp.github.io/cppwp/n4861/.

40. Lewis Baker, “C++ Coroutines: Understanding the Promise Type,” September 5, 2018. Accessed April 18, 2023. https://lewissbaker.github.io/2018/09/05/understanding-the-promise-type.