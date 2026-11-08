# The transformed coroutine

```
```c
{
    Promise prom;
    co_await prom.initial_suspend();
    try {
        <function body having co_return, co_yield, or co_await>
    }
    catch (...) {
        prom.unhandled_exception();
    }
FinalSuspend:
    co_await prom.final_suspend();
}
```
```

The compiler automatically runs the transformed code using the functions of the promise object. In short, I call this workflow the promise workflow. Here are the main steps of this workflow.

+   - Coroutine begins execution
+     - allocates the coroutine frame if necessary
+     - copies all function parameters to the coroutine frame
+     - creates the prom object prom (line 2)
+     - calls prom.get_return_object() to create the coroutine handle and keeps it in a local variable. The result of the call will be returned to the caller when the coroutine first suspends.
+     - calls prom.initial_suspend() and co_awaits its result. The promise type typically returns suspend_never for eagerly-started coroutines or suspend_always for lazily-started coroutines. (line 3)
+     - the body of the coroutine is executed when co_await prom.initial_suspend() resumes
+   - Coroutine reaches a suspension point
+     - the return object (prom.get_return_object()) is returned to the caller which resumed the coroutine
+   - Coroutine reaches co_return
+     - calls prom.return_void() for co_return or co_return expression, where expression has type void
+     - calls prom.return_value(expression) for co_return expression, where expression has non-void type.
+     - destroys all stack-created variables
+     - calls prom.final_suspend() and co_awaits its result
+   - Coroutine is destroyed (by terminating via co_return or via uncaught exception, or via the coroutine handle)