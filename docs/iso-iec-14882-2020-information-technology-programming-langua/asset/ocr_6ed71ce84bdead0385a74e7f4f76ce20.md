# ISO/IEC 14882:2020(E)

```
template<class Clock, class Duration>
    future_status wait_until(const chrono::time_point<Clock, Duration>& abs_time) const;
```

Effects: None if the shared state contains a deferred function (32.9.9), otherwise blocks until the shared state is ready or until the absolute timeout (32.2.4) specified by abs_time has expired.

Returns:

+   - future_status::deferred if the shared state contains a deferred function.
+   - future_status::ready if the shared state is ready.
+   - future_status::timeout if the function is returning because the absolute timeout (32.2.4) specified by abs_time has expired.

Throws: timeout-related exceptions (32.2.4).

# 32.9.9 Function template async [futures.async]

The function template async provides a mechanism to launch a function potentially in a new thread and provides the result of the function in a future object with which it shares a shared state.

```
template<class F, class... Args>
    [[nodiscard]] future<invoke_result_t<decay_t<F>, decay_t<Args>...>>
    async(F&& f, Args&&... args);
template<class F, class... Args>
    [[nodiscard]] future<invoke_result_t<decay_t<F>, decay_t<Args>...>>
    async(launch policy, F&& f, Args&&... args);
```

Mandates: The following are all true:

+   - is_constructible_v<decay_t<F>, F>,
+   - (is_constructible_v<decay_t<Args>, Args> &&...),
+   - is_move_constructible_v<decay_t<F>>,
+   - (is_move_constructible_v<decay_t<Args>> &&...), and
+   - is_invocable_v<decay_t<F>, decay_t<Args>...>.

Preconditions: decay_t<F> and each type in decay_t<Args> meet the Cpp17MoveConstructible requirements.

Effects: The first function behaves the same as a call to the second function with a policy argument of launch::async | launch::deferred and the same arguments for F and Args. The second function creates a shared state that is associated with the returned future object. The further behavior of the second function depends on the policy argument as follows (if more than one of these conditions applies, the implementation may choose any of the corresponding policies):

+   - If launch::async is set in policy, calls invoke(decay-copy(std::forward<F>(f)), decay-copy(std::forward<Args>(args))...) (20.14.4, 32.4.3.3) as if in a new thread of execution represented by a thread object with the calls to decay-copy being evaluated in the thread that called async. Any return value is stored as the result in the shared state. Any exception propagated from the execution of invoke(decay-copy(std::forward<F>(f)), decay-copy(std::forward<Args>(args))...) is stored as the exceptional result in the shared state. The thread object is stored in the shared state and affects the behavior of any asynchronous return objects that reference that state.

+   - If launch::deferred is set in policy, stores decay-copy(std::forward<F>(f)) and decay-copy(std::forward<Args>(args))... in the shared state. These copies of f and args constitute a deferred function. Invocation of the deferred function evaluates invoke(std::move(g), std::move(xyz)) where g is the stored value of decay-copy(std::forward<F>(f)) and xyz is the stored copy of decay-copy(std::forward<Args>(args))... Any return value is stored as the result in the shared state. Any exception propagated from the execution of the deferred function is stored as the exceptional result in the shared state. The shared state is not made ready until the function has completed. The first call to a non-timed waiting function (32.9.5) on an asynchronous return object referring to this shared state invokes the deferred function in the thread that called the waiting function. Once evaluation of invoke(std::move(g), std::move(xyz)) begins, the function is no longer considered deferred.