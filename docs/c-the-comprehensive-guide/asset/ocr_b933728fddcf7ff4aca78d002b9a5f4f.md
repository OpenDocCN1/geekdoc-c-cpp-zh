The interface of `promise_type` is intentionally kept general to suit many requirements. This does not make the first steps with coroutines easy, but there will surely soon be libraries built on `promise_type` that can offer you a simple interface for various requirements.

# 29.9  Summary

Here I summarize the elements for multithreading in the standard library in a brief overview:

+   - Avoid having to manage threads yourself wherever possible.
+   - Use `jthread` for threads (from C++20; otherwise `thread`).
+   - Use `stop_token` as a cancellation mechanism (from C++20).
+   - Use `latch` and `barrier` (from C++20) and possibly `future` for synchronization.
+   - For the rest, use mutex.
+   - Use atomic only in the rarest cases.

# 29.9.1  “<thread>” Header

+   - **thread, jthread—join(), detach(), joinable(), get_id(), native_handle()**  
+     Classes for starting threads. `jthread` waits for the thread to finish. `detach()` allows the thread to continue running even if the thread object is destroyed. `get_id()` returns a unique thread identifier. `native_handle()` allows platform-dependent interaction with a thread.
+   - **this_thread::get_id(), yield(), sleep_for, sleep_until**  
+     Namespace with similar helper functions for information and manipulation of the current thread. `get_id` is used to identify the current thread. `yield` lets other threads take their turn. `sleep_for` and `sleep_until` pause the thread for a specified time.
+   - **thread::id—operator<<, operator<, etc., hash<thread::id>**  
+     Type for uniquely identifying a thread. Can be used in associative containers and output to a stream thanks to overloaded operators.

# 29.9.2  “<latch>” and “<barrier>” Headers

+   - **latch—count_down(), wait(), try_wait()**  
+     One-time use latch for threads. `count_down()` decreases the counter. `wait()` blocks until the counter is 0 (since C++20).
+   - **barrier—arrive_and_wait(), arrive_and_drop(), etc.**  
+     Reusable barrier for thread synchronization. `arrive_and_wait()` blocks until all threads have arrived at the barrier (since C++20).