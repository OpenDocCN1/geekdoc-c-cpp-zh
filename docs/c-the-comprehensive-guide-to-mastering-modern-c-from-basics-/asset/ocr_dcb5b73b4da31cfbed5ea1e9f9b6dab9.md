next co_yield until—in this case—10 values have been delivered. The coroutine terminates and is cleaned up (because promise_type dictates so).

# 29.8.3 Coroutines with "promise_type"

return types with promise_type are somewhat complicated. You need to write the class yourself and implement the properties you need.

Your return type must be a class that contains or names promise_type. This promise_type must have the following methods:

+   - get_return_object()
This method is called when the coroutine is started. It returns an appropriate std::coroutine_handle. With this, the caller communicates with the coroutine.

+   - initial_suspend()
Returns either suspend_always if the coroutine should not start immediately or suspend_never.

+   - final_suspend()
Contains final cleanup operations of the coroutine. Returns either suspend_always OR suspend_never.

+   - unhandled_exception()
Called when an exception occurs in the coroutine. It can handle this exception or rethrow it.

One of the simplest possible implementations looks like the following listing: