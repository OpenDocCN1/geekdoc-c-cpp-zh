
## 7.3 Modification and Generalization of a Generator

![](img/c60a87adb7f61e2e82071d081bbb389a_566_0.png)

Cippi handles a data stream

Before I modify and generalize the generator for an infinite data stream, I want to present it as a starting point of our journey. I intentionally put many output operations in the source code and only ask for three values. This simplification and visualization should help to understand the control flow.

**Generator generating an infinite data stream**

```cpp
// infiniteDataStreamComments.cpp

#include <coroutine>
#include <memory>
#include <iostream>

template <typename T>
struct Generator {

    struct promise_type;
    using handle_type = std::coroutine_handle<promise_type>;

    Generator(handle_type h): coro(h) {
        std::cout << "        Generator::Generator" << '\n';
    }
    handle_type coro;
}
void return_void() {}
void unhandled_exception() {
    std::exit(1);
}

T current_value;
};

};

Generator<int> getNext(int start = 10, int step = 10) {
    std::cout << " getNext: start " << '\n';
    auto value = start;
    while (true) {
        std::cout << " getNext: before co_yield " << '\n';
        co_yield value;
        std::cout << " getNext: after co_yield " << '\n';
        value += step;
    }
}

int main() {

    auto gen = getNext();
    for (int i = 0; i < 2; ++i) {
        auto val = gen.getNextValue();
        std::cout << " main: " << val << '\n';
    }
}
```

Executing the program on the Compiler Explorer⁵ makes the control flow transparent.

⁵https://godbolt.org/z/cTW9Gq

```text
        promise_type::promise_type
        promise_type::get_return_object
    Generator::Generator
        promise_type::initial_suspend
        Generator::getNextValue
getNext: start
getNext: before co_yield
            promise_type::yield_value
main: 10
            Generator::getNextValue
getNext: after co_yield
getNext: before co_yield
            promise_type::yield_value
main: 20
            Generator::getNextValue
getNext: after co_yield
getNext: before co_yield
            promise_type::yield_value
main: 30
            Generator::~Generator
            promise_type::~promise_type
```

**Generator generating an infinite data stream**

Let's analyze the control flow.

The call getNext() (line 87) triggers the creation of the Generator<int>. First, the promise_type (line 38) is created, and the following get_return_object call (line 54) creates the generator (line 56) and stores it in a local variable. The result of this call is returned to the caller when the coroutine is suspended the first time. The initial suspension happens immediately (line 48). Because the member function initial_suspend returns an awaitable std::suspend_always (line 48), the control flow continues with the coroutine getNext until the instruction co_yield value (line 79). This call is mapped to the call yield_value(int value) (line 59), and the current value is prepared current_value = value (line 61). The member function yield_value(int value) returns the awaitable std::suspend_always (line 59). Consequently, the execution of the coroutine pauses and the control flow goes back to the main function, and the for loop starts (line 89). The call gen.getNextValue() (line 89) starts the execution of the coroutine by resuming the coroutine, using coro.resume() (line 34). Further, the function getNextValue() returns the current value that was prepared using the previously invoked member function yield_value(int value) (line 59). Finally, the generated number is displayed in line 90, and the for loop continues. In the end, the generator and the promise are destructed.

After this detailed analysis, I would like to make a first modification of the control flow.

### 7.3.1 Modifications

The snippets and line numbers are based on the previous program `infiniteDataStreamComments.cpp`. I only show the modifications.

#### 7.3.1.1 The Coroutine Is Not Resumed

When I disable the resumption of the coroutine (`gen.getNextValue()` in line 89) and the display of its value (line 90), the coroutine pauses immediately.

**Not resuming the coroutine**

```cpp
int main() {

    auto gen = getNext();
    for (int i = 0; i <= 2; ++i) {
        // auto val = gen.getNextValue();
        // std::cout << "main: " << val << '\n';
    }

}
```

The coroutine never runs. Consequently, the generator and its promise are created and destroyed.

![](img/c60a87adb7f61e2e82071d081bbb389a_570_0.png)

#### 7.3.1.2 `initial_suspend` Never Suspends

In the program, the member function `initial_suspend` returns the awaitable `std::suspend_always` (line 46). As its name suggests, the awaitable `std::suspend_always` causes the coroutine to pause immediately. Let me return `std::suspend_never` instead of `std::suspend_always`.

**initial_suspend suspends never**

```cpp
std::suspend_never initial_suspend() {
    std::cout << " promise_type::initial_suspend" << '\n';
    return {};
}
```

In this case, the coroutine runs immediately and pauses when the function `yield_value` (line 59) is invoked. A subsequent call `gen.getNextValue()` (line 89), resumes the coroutine and triggers the execution of the member function `yield_value` once more. The result is that the starting value 10 is ignored, and the coroutine returns the values 20, 30, and 40.

```text
promise_type::promise_type
promise_type::get_return_object
Generator::Generator
promise_type::initial_suspend
getNext: start
getNext: before co_yield
    promise_type::yield_value
Generator::getNextValue
getNext: after co_yield
getNext: before co_yield
    promise_type::yield_value
main: 20
    Generator::getNextValue
getNext: after co_yield
getNext: before co_yield
    promise_type::yield_value
main: 30
    Generator::getNextValue
getNext: after co_yield
getNext: before co_yield
    promise_type::yield_value
main: 40
    Generator::~Generator
    promise_type::~promise_type
```

**Not Resuming the Coroutine**

#### 7.3.1.3 `yield_value` Never Suspends

The member function `yield_value` (line 59) is triggered by the call `co_yield value` and prepares the `current_value` (line 61). The function returns the awaitable `std::suspend_always` (line 62) and, therefore, pauses the coroutine. Consequently, a subsequent call gen.getNextValue() (line 89) has to resume the coroutine. When I change the return value of the member function yield_value to std::suspend_never, let me see what happens.

**yield_value never suspends**

```cpp
std::suspend_never yield_value(int value) {
    std::cout << "        promise_type::yield_value" << '\n';
    current_value = value;
    return {};
}
```

As you may guess, the while loop (lines 77 - 82) runs forever, and the coroutine does not return anything.

```text
promise_type::promise_type
promise_type::get_return_object
Generator::Generator
promise_type::initial_suspend
Generator::getNextValue
getNext: start
getNext: before co_yield
        promise_type::yield_value
getNext: after co_yield
getNext: before co_yield
        promise_type::yield_value
getNext: after co_yield
getNext: before co_yield
        promise_type::yield_value
getNext: after co_yield
getNext: before co_yield
        promise_type::yield_value
getNext: after co_yield
getNext: before co_yield
        promise_type::yield_value
getNext: after co_yield
getNext: before co_yield
        promise_type::yield_value
getNext: after co_yield
```

**yield_value Never Suspends**

It is straightforward to restructure the generator infiniteDataStreamComments.cpp so that it produces a finite number of values.

### 7.3.2 Generalization

You may wonder why I never used the full generic potential of Generator. Let me adjust its implementation to produce the successive elements of an arbitrary container of the Standard Template Library.

**Generator successively returning each element**

```cpp
// coroutineGetElements.cpp

#include <coroutine>
#include <memory>
#include <iostream>
#include <string>
#include <vector>

template<typename T>
struct Generator {

    struct promise_type;
    using handle_type = std::coroutine_handle<promise_type>;

    Generator(handle_type h) : coro(h) {}

    handle_type coro;

    ~Generator() {
        if (coro) coro.destroy();
    }
    Generator(const Generator&) = delete;
    Generator& operator = (const Generator&) = delete;
    Generator(Generator&& oth) : coro(oth.coro) {
        oth.coro = nullptr;
    }
    Generator& operator = (Generator&& oth) {
        coro = oth.coro;
        oth.coro = nullptr;
        return *this;
    }
    T getNextValue() {
        coro.resume();
        return coro.promise().current_value;
    }
    struct promise_type {
        promise_type() {}

```
