+   e) When a coroutine begins executing, it calls the ________ function on the promise object to determine whether to immediately suspend (for lazy coroutines) or continue executing.
+   f) Generator support libraries use a ________ (from header `<coroutine>`) to refer to and manipulate a running or suspended coroutine. Some capabilities of this class template include: creating a `coroutine_handle` from a promise object, checking whether the referenced coroutine has completed execution, resuming a suspended coroutine, destroying the coroutine state and getting the coroutine's promise object.
+   g) The operand of `co_await` must be a(n) ________ object, such as a `concurrencpp::result`.
+   h) If the result is not ready, the ________ function is called to determine whether to suspend the coroutine's execution and return control to the caller. If this function returns a `coroutine_handle` for another suspended coroutine, that coroutine resumes execution.

**18.2** State whether each of the following is *true* or *false*. If *false*, explain why.

+   a) The mechanisms that suspend a coroutine and return control to its caller and continue a suspended coroutine's execution later are handled entirely by code that's written for you by the compiler.
+   b) A function containing any of the keywords await, yield or return is a coroutine.
+   c) A generator is a coroutine that produces values on demand.
+   d) Memory usage for stackless coroutines is substantial, severely limiting the number of coroutines that can run concurrently.
+   e) Tasks allow developers to be more productive by focusing less on business logic and more on low-level concepts like thread management and inter-thread synchronizations.
+   f) We can use `concurrencpp`'s `thread_pool_executor` to put multiple tasks to work in parallel.
+   g) When a coroutine `co_await`s tasks, it will suspend its execution if their results are not yet available; otherwise, it will simply complete and return.
+   h) According to the C++20 standard, the following kinds of functions cannot be coroutines: `main`, constructors, destructors, `constexpr` and `consteval` functions, functions declared with placeholder types (`auto` or C++20 concepts) and functions with variable numbers of arguments.

# ### Answers to Self-Review Exercises

**18.1** a) callback function. b) coroutine. c) generators. d) promise object. e) `initial_suspend`. f) `coroutine_handle`. g) `awaitable`. h) `await_suspend`.

**18.2** a) True. b) False. Actually, a function containing any of the keywords `co_await`, `co_yield` or `co_return` is a coroutine. c) True. d) False. Actually, Marc Gregoire points out that “memory usage for stackless coroutines is minimal, allowing for millions or even billions of coroutines to be running concurrently.” e) False. Actually, tasks allow developers to be more productive by focusing more on business logic and less on low-level concepts like thread management and inter-thread synchronizations. f) True. g) True. h) True.