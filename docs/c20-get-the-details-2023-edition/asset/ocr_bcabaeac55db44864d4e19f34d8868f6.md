# Injecting the coroutine handle

```
```cpp
// coroutineTraits.cpp

#include <coroutine>
#include <memory>
#include <iostream>

struct GeneratorVerbose {

    struct promise_type;
    using handle_type = std::coroutine_handle<promise_type>;

    handle_type coro;
    GeneratorVerbose() {
        std::cout << "        GeneratorVerbose::GeneratorVerbose" << '\n';
    }

    ~GeneratorVerbose() {
        std::cout << "        GeneratorVerbose::~GeneratorVerbose" << '\n';
        if ( coro ) coro.destroy();
    }

    int getNextValue() {
        std::cout << "        GeneratorVerbose::getNextValue" << '\n';
        coro.resume();
        return coro.promise().current_value;
    }

    struct promise_type {
        promise_type(int, GeneratorVerbose& genVerbose) {
            std::cout << "        promise_type::promise_type" << '\n';
            genVerbose.coro = handle_type::from_promise(*this);
        }

        ~promise_type() {
            std::cout << "        promise_type::~promise_type" << '\n';
        }

        std::suspend_always initial_suspend() {
            std::cout << "        promise_type::initial_suspend" << '\n';
            return {};
        }
        std::suspend_always final_suspend() noexcept {
            std::cout << "        promise_type::final_suspend" << '\n';
            return {};
        }
    }
};
```
```