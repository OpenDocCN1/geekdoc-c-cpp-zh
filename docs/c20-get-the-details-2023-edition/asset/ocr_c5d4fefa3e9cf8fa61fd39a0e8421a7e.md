![](bbox=[0.3, 0.08, 0.7, 0.28])

Use a std::stop_token more times on various threads

# ### 6.5.4 A General Mechanism to Send Signals

The pair `std::stop_source` and `std::stop_token` can be considered as a general mechanism to send a signal. By copying the `std::stop_token`, you can send the signal to any entity executing something. In the following example, I use `std::async`, `std::promise`, `std::thread`, and `std::jthread` in various combinations.

Sending a signal to various executing entities

```
```cpp
// signalStopRequests.cpp

#include <iostream>
#include <thread>
#include <future>

using namespace std::literals;

void function1(std::stop_token stopToken, const std::string& str){
    std::this_thread::sleep_for(1s);
    if (stopToken.stop_requested()) std::cout << str << ": Stop requested\n";
}

void function2(std::promise<void> prom,
               std::stop_token stopToken, const std::string& str) {
    std::this_thread::sleep_for(1s);
    std::stop_callback callBack(stopToken, [&str] {
        std::cout << str << ": Stop requested\n";
    });
    prom.set_value();
}
```
```