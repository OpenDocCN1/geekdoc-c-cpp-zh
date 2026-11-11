```
```
promise_type::promise_type
promise_type::get_return_object
promise_type::initial_suspend
createFuture
promise_type::return_value
promise_type::final_suspend
promise_type::~promise_type
MyFuture::MyFuture
MyFuture::get
res: 2021

MyFuture::~MyFuture
```
```

An eager future

The presented coroutine runs immediately and is, therefore, eager. Furthermore, the coroutine runs in the thread of the caller.

Let’s make the coroutine lazy.

# ### 6.6.1 A Lazy Future

A lazy future is a future that runs only if asked for the value. Let's see what I have to change in the eager coroutine, presented in eagerFutureWithComments.cpp, to make it lazy.

Control flow of a lazy future

```
```cpp
// lazyFuture.cpp

#include <coroutine>
#include <iostream>
#include <memory>

template<typename T>
struct MyFuture {
    struct promise_type;
    using handle_type = std::coroutine_handle<promise_type>;

    handle_type coro;

    MyFuture(handle_type h): coro(h) {
        std::cout << "    MyFuture::MyFuture" << '\n';
    }
```
```