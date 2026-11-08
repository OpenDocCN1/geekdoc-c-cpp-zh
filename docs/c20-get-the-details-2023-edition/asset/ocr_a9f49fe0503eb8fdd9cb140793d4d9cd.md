# **Functions of a std::thread t**

| Method | Description |
| --- | --- |
| t.~jthread() | If joinable(), calls request_stop() and then join(). |
| t.join() | Waits until thread t has finished its execution. |
| t.detach() | Executes the created thread t independently of the creator. |
| t.joinable() | Returns true if thread t is still joinable. |
| t.get_id() and std::this_thread::get_id() | Returns the id of the thread. |
| std::jthread::hardware_concurrency() | Indicates the number of threads that can run concurrently. |
| std::this_thread::sleep_until(absTime) | Puts thread t to sleep until time point absTime. |
| std::this_thread::sleep_for(relTime) | Puts thread t to sleep for time duration relTime. |
| std::this_thread::yield() | Enables the system to run another thread. |
| t.swap(t2) | Swaps the threads. Same as std::swap(t, t2). |
| t.get_stop_source() | Returns a std::stop_source object associated with the shared stop state. |
| t.get_stop_token() | Returns a std::stop_token object associated with the shared stop state. |
| t.request_stop() | Requests execution stop via the shared stop state. Returns true if the stop request was successful. |

Detaching a std::jthread t with t.detach() still allows it to call the functions t.get_stop_source() and t.get_stop_token().

# ### 6.6.1 Automatically Joining

This is the *non-intuitive* behavior of std::thread. If a std::thread is still joinable, std::terminate^39 is called in its destructor, which calls std::abort^40. A thread thr is joinable if neither thr.join() nor thr.detach() has been called.