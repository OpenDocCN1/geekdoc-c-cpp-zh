```
;
void return_void() {std::cout << "good-bye, coroutine has exited\n";}
void unhandled_exception() { };
```

```
std::coroutine_handle<promise_type> handle;

ReturnObject(std::coroutine_handle<promise_type> _handle) :
    handle{handle} {
```

Here get_return_object creates a coroutine handle from the promise_type object and the constructor for ReturnObject uses this handle to instantiate a ReturnObject.

The coroutine_handle provides the resume() method to resume a coroutine. The done() method is a predicate function that checks whether a coroutine is finished. done() returns true if the coroutine is suspended at it's final suspend point and false otherwise.

In the following example, the coroutine suspends itself twice and the calling function resumes the coroutine twice:

```
#include <coroutine>
#include <iostream>

using namespace std;

struct ReturnObject {
    struct promise_type {
        promise_type() = default;

        ReturnObject get_return_object() {
            return ReturnObject{std::coroutine_handle<promise_type>::from_promise(*this)};
        }
    }

    suspend_never initial_suspend() {
        cout << "ready to execute coroutine" << endl;
        return {};
    };
```