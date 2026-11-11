# ### Member functions of std::stop_source

| Member function | Description |
| --- | --- |
| std::stop_source src | The default constructor creates a stop source with an associated stop state. |
| std::stop_source src(nostopstate) | Creates a stop_source without associated stop state. |
| src.get_token() | If src.stop_possible(), returns a stop_token for the associated stop state. Otherwise, returns a default-constructed (empty) stop_token. |
| src.stop_possible() | true if src can be requested to stop. |
| src.stop_requested() | true if stop_possible() and request_stop() was called by one of the owners. |
| src.request_stop() | Calls a stop request if src.stop_possible() and !src.stop_requested(). Otherwise, the call has no effect. |

The call src.get_token() returns the stop token token. Thanks to token you can check if a stop request has been made or can be made by its associated stop source src. The stop token observes the stop source src.

src.stop_requested() returns true when src has an associated stop state and was asked to stop earlier.

src.stop_possible() return false if there is no associated stop state or no stop source anymore and stop was never requested before.

The calls src.stop_possible(), src.stop_requested(), and src.request_stop() are thread-safe.

src.request_stop() of a stop source src is visible to all std::stop_token and registered callback of the same associated stop state. Also, any std::condition_variable_any waiting on the associated std::stop_token() will be awaken. When a stop is requested, it cannot be withdrawn. src.request_stop() is successful and returns true if src' has an associated stop state and it was not requested to stop before.

# ### 3.6.2 std::stop_token

std::stop_token is essentially a thread-safe "view" of the associated stop state. It is typically retrieved from a std::jthread or a std::stop_source src via src.get_token(). This causes them share the same associated stop state as the std::jthread or std::stop_source.

Thanks to the std::stop_token, you can check for the associated std::stop_source if a stop request has been made.

The std::stop_token can also be passed to the constructor of std::stop_callback, or to the interruptible waiting functions of std::condition_variable_any.