
```
}
}
```

**Listing 29.36** Only the "get" needs to be encapsulated in "try".

Even if async starts the calculation immediately and the exception occurs in the thread, it is initially stored. Only get() triggers the stored exception.

## 29.6.4 "promise"

A future can not only be created with async. Looking under the hood, you will find a promise—means to pass the result or the exception from the executing thread to the caller. In this sense, you could see a promise as a kind of channel for communication between threads. This term also can be found in some other APIs.

The typical procedure when working with futures and promises is as follows:

- Create a new promise.
- Request a future associated with the promise.
- Start a new thread and pass it the promise.
- Perform the actual computation in the new thread.
- Assign the result to the promise.
- Wait in the caller until the future can deliver a result.
- Retrieve the result of the future.

Of course, the new thread in which the computation is performed asynchronously must have access to the promise in order to communicate with it. You can pass it to the new thread as an argument, for example. So a future and a promise always belong together.

The future remains with the caller to receive the message with get() (in channels, the roughly corresponds to receive). The called function gets the promise and uses set_value to send a result (which corresponds to send in channels). If an exception occurs, use the set_exception method instead.

Specifically, this means that if you want to have a function asynchronously compute an int, you make a promise that you will compute the int. You create this with the following:

```
promise<int> intPromise;
```

From this promise, you request a future with get_future() to keep in the caller, while you move intPromise itself into the asynchronous function with move()—you cannot copy a promise.

```cpp
// https://godbolt.org/z/7E1E6aezE
#include <future>
#include <thread>
#include <iostream>
#include <exception>
// Ackermann function
void ack(int m, int n, std::promise<int> intPromise) {
try {
    int result = ack(m, n);
    intPromise.set_value(result); // report result
} catch (std::exception& e) {
    intPromise.set_exception(make_exception_ptr(e)); // report
}
} catch (...) {
    intPromise.set_exception(std::current_exception()); // Exc. w/o name
}
int main () {
    std::promise<int> intPromise;                                // Create promise
    std::future<int> intFuture = intPromise.get_future(); // Request future
    std::thread th(longComputation,                     // start
                   std::move(intPromise)); // Pass promise
    th.detach();                               // let it run
    // might throw an exception:
    int result = intFuture.get(); // Request result
    std::cout << result << std::endl;
}
```

# Listing 29.37 A “future” and “promise” working together.

In main(), the process described previously takes place. First, a new promise for an int result is created. Then, you request an associated future from it using get_future, which remains in the main thread.

In this example, I create a thread for the actual execution. But you can also come up with a more elaborate method to distribute the new task, such as an asynchronous queue that processes tasks for as long as there are any. The intPromise is passed as a parameter to the function to be executed in the thread; copying is not possible, so I move intPromise with move().). The subsequent th.detach() detaches the newly started thread from the variable th. I could have also ensured before exiting main() with th.join() that th only becomes invalid when the thread is finished, but that is irrelevant for this example.

The function longComputation started by th received the intPromise as a parameter for communication with the caller. If the calculation leads to a regular result, you communicate this via intPromise.set_value().

Because unhandled exceptions within th lead to terminate() and thus to the end of the program, your own exception handling is important here. If you want to communicate an exception, use intPromise.set_exception(). This is usually done in a catch block. If you hold the exception in the variable e, you can get a reference with make_exception_ptr(e) that the promise can store until it is retrieved with get(). If you do not hold the exception in a variable, you can obtain a reference with current_exception().

In the main thread, the result is requested with get(). This call waits until it is ready. This can be the regular value, which is then assigned to result, or a stored exception, which is thrown here in the main thread.

A combination of threads, promises, and self-created futures, for example, realize asynchronous input and output.

## Bundling Tasks Together

When you use async, the promise part of the communication conveniently does not appear as it would normally always look very similar anyway. However, the execution is either started immediately or at the moment of the get() call.

If you want more control over when the computation is executed, you can use packaged_task. Here too, users deal with the future part of the communication. Preparing the computation function and triggering thencomputation are separated from each other.

```cpp
// https://godbolt.org/z/94r3
#include <future>
#include <thread>
#include <iostream>
int ack(int m, int n); // Ackermann function
int main () {
    std::packaged_task<int(void)> task1 = 
    () { return ack(3,11); }; // Signature of later
    auto f1 = task1.get_future();
    std::thread th1(move(task1)); // In new thread
    std::cout << "ack(3,11):" << f1.get() << '\n'; // Output:
    ack(3,11):16381
}
```

# Listing 29.38 Preparing a packaged task for later.

You are already familiar with get_future and get. What is new is that with task1 you can already prepare the later. The template parameter of packaged_task reflects the signature of the function to be called—here int(void) is a function without parameters that returns an int. Here, it is specifically a lambda that will later perform the time-intensive computation. Now you can trigger the execution of task1 anytime. In the example, however, should happen in a new thread. For this, you create thread object with the task as a parameter. Tasks cannot be copied, only moved, which why move is necessary.

The task ensures that the calculation result is communicated internally via a promise and can be queried via the future. The join() ensures that the thread is cleanly terminated when th1 goes out of scope.

For another scenario where you do not want to set all arguments at the moment of creating the packagedtask but only when starting the thread, there are small differences, as in the next listing.

```cpp
// https://godbolt.org/z/bglhn5r
#include <future>
#include <thread>
#include <iostream>
int ack(int m, int n); // Ackermann function
int main () {
    std::packaged_task<int(int,int)> task2 ( &ack); // different signature
    auto f2 = task2.get_future();
    std::thread th2 (move(task2), 3, 12); // Parameters here
    std::cout << "ack(3,12):" << f2.get() << '\n'; // Output:
    ack(3,12):32765
    th2.join();
}
```

# Listing 29.39 Provide a packaged task with arguments later.

The signature that must be specified when constructing packaged_task is always the one that remains for the actual call—here through jthread. Because I pack ack into task2 without already bound parameters, this is a function that takes two int and returns one—that is, int(int,int). However, as this task is now to be taken over by jthread, these two parameters are now also specified during thread creation.
