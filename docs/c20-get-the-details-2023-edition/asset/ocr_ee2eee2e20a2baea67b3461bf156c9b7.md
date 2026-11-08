# 6.1.4.4 Get the Awaitable and the Awaiter

There are essentially two ways to get an Awaiter.

+   - A `co_await` operator is defined.
+   - The Awaitable becomes the Awaiter.

Remember, when `co_await` expression is invoked, the expression is converted to an Awaitable:

+   1. If expression is created by an initial suspension point (`from initial_suspend()`), final suspension point (`from final_suspend()`), or yield expression (`from yield_value(value)`), the Awaitable is the expression.
+   2. If the current coroutine's promise type has a member function `await_transform`, the Awaitable is from `await_transform(expression)`.
+   3. the Awaitable is the expression.

Now, the compiler performs the following lookup rule to get an Awaiter:

+   1. It looks for the `co_await` operator on the promise object and returns an Awaiter:
+   
+       awaiter = awaitable.operator co_await();
+   
+   2. It looks for a freestanding `co_await` operator and returns an Awaiter:
+   
+       awaiter = operator co_await(awaitable);
+   
+   3. If there is no `co_await` operator defined, the Awaitable becomes the Awaiter:
+   
+       awaiter = awaitable;

![](bbox=[0.105, 0.585, 0.175, 0.64])

```
`awaiter = awaitable`
```

> > When you study my coroutine implementations in this chapter, you may notice that I use most of the time that an Awaitable implicitly becomes an Awaiter. Only the example to thread synchronization uses the `co_await` operator to get the Awaiter.

After these static aspects of coroutines, I want to continue with their dynamic aspects.

# 6.1.5 The Workflows

The compiler transforms your coroutine and runs two workflows: the outer promise workflow and the inner Awaiter workflow.

# 6.1.5.1 The Promise Workflow

When you use `co_yield`, `co_await`, or `co_return` in a function, the function becomes a coroutine, and the compiler transforms its body to something equivalent to the following lines.