is passed into the function and can, therefore, be used by the function to check if a stop request has been requested.

The following table gives you a concise overview of the additional `std::thread t` functionality.

Additional member functions of a std::thread t

| Member functions | Description |
|---|---|
| `t.get_stop_source()` | Returns a `std::stop_source` object associated with the shared stop state. |
| `t.get_stop_token()` | Returns a `std::stop_token` object associated with the shared stop state. |
| `t.request_stop()` | Requests execution stop via the shared stop state. Returns `true` if the stop request was successful. |

# ### 3.2.1 Automatically Joining

This is the *non-intuitive* behavior of `std::thread`. If a `std::thread` is still joinable, `std::terminate` is called in its destructor. A thread `thr` is joinable if either `thr.join()` nor `thr.detach()` was called.

**Terminating a still joinable `std::thread`**

```
    // threadJoinable.cpp
    #include <iostream>
    #include <thread>

    int main() {

        std::cout << '\n';
        std::cout << std::boolalpha;

        std::thread thr([] { std::cout << "Joinable std::thread" << '\n'; });

        std::cout << "thr.joinable(): " << thr.joinable() << '\n';

        std::cout << '\n';

    }
```

When executed, the program terminates.