`src.stop_requested()` returns true when `src` has an associated stop state and was not asked to stop earlier.

`src.stop_possible()` return false if there is no associated stop state or no stop source anymore and stop has never been requested before.

The calls `src.stop_possible()`, `src.stop_requested()`, and `src.request_stop()` are thread-safe.

`src.request_stop()` of a stop source `src` is visible to all `std::stop_token` and is guaranteed callback of the same associated stop state. Also, any `std::condition_variable_any` waiting on the associated `std::stop_token()` will be awoken. Once a stop is requested, it cannot be withdrawn. `src.request_stop()` is successful and returns true if `src` has an associated stop state and was not requested to stop before.

# 6.5.2 `std::stop_token`

`std::stop_token` is essentially a thread-safe “view” of the associated stop state. It is typically retrieved from a `std::jthread` or a `std::stop_source` via `src.get_token()`. This causes them to share the same associated stop state as the `std::jthread` or `std::stop_source`.

Thanks to the `std::stop_token`, you can check for the associated `std::stop_source` if a stop request has been made.

The `std::stop_token` can also be passed to the constructor of `std::stop_callback` or the interruptible waiting functions of `std::condition_variable_any`.

**Member functions of `std::stop_token`**

| Member function | Description |
|---|---|
| `std::stop_token stoken` | Creates a stop token with no associated stop state. |
| `stoken.stop_possible()` | Returns true if `stoken` has an associated stop state or a stop request has already been made, otherwise false. |
| `stoken.stop_requested()` | true if `request_stop()` was called on the associated `std::stop_source src`, otherwise false. |

`stoken.stop_possible()` also returns false if there is no longer a stop source.

If the `std::stop_token` should be temporarily disabled, you can replace it with a default-constructed token. A default-constructed token has no associated stop state. The following code snippet shows how to disable and enable a thread’s capability to accept stop requests.