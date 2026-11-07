
- Coroutine `sortCoroutine` (lines 21–78) uses **concurrencpp** to launch two tasks that each sort half the vector.
- Function `main` (lines 80–107) creates the 100-million-element vector and calls `sortCoroutine` to sort the vector.

We’ve split this program into pieces for discussion purposes. After the program, we show a sample output.

## #include Directives and Function `id`

In Fig. 18.3, lines 3–11 include the headers used in this program, and lines 14–18 define function `id`. The **concurrencpp** library (line 3) provides the coroutine support features this program requires.

```cpp
// fig18_03.cpp
// Implementing a coroutine with co_await and co_return.
#include <concurrencpp/concurrencpp.h>
#include <format>
#include <iostream>
#include <memory> // for shared_ptr
#include <random>
#include <sstream>
#include <string>
#include <thread>
#include <vector>

// get current thread's ID as a string
std::string id() {
    std::ostringstream out;
    out << std::this_thread::get_id();
    return out.str();
}
```

**Fig. 18.3** | Implementing a coroutine with `co_await` and `co_return`.

## sortCoroutine That Launches Two Tasks

Lines 21–78 define `sortCoroutine`, which receives as arguments

- a `std::shared_ptr<concurrencpp::thread_pool_executor>` used to schedule tasks and
- a reference to a `vector<int>` to sort.

```cpp
// coroutine that sorts a vector<int> using two tasks
concurrencpp::result<void> sortCoroutine(
    std::shared_ptr<concurrencpp::thread_pool_executor> executor,
    std::vector<int>& values) {

    std::cout << std::format("Thread {}: sortCoroutine started\n\n", id());

    // lambda that sorts a portion of a vector
    auto sortTask{
      [&](auto begin, auto end) {
        std::cout << std::format(
          "Thread {}: Sorting {} elements\n", id(), end - begin);
        std::sort(begin, end);
        std::cout << std::format("Thread {}: Finished sorting\n", id());
      }
    };

    // stores task results
    std::vector<concurrencpp::result<void>> results;

    size_t middle{values.size() / 2}; // middle element index

    std::cout << std::format(
      "Thread {}: sortCoroutine starting first half sortTask\n", id());

    // use a concurrencpp thread_pool_executor to schedule
    // a sortTask call that sorts the first half of values
    results.push_back(
      executor->submit(
        [&]() {sortTask(values.begin(), values.begin() + middle);}
      )
    );

    std::cout << std::format(
      "Thread {}: sortCoroutine starting second half sortTask\n", id());

    // use a concurrencpp thread_pool_executor to schedule
    // a sortTask call that sorts the second half of values
    results.push_back(
      executor->submit(
        [&]() {sortTask(values.begin() + middle, values.end());}
      )
    );

    // suspend coroutine while waiting for all sortTasks to complete
    std::cout << std::format("\nThread {}: {}\n", id(),
      "sortCoroutine co_awaiting sortTask completion");
    co_await concurrencpp::when_all(
      executor, results.begin(), results.end());

    // merge the two sorted sub-vectors
    std::cout << std::format(
      "\nThread {}: sortCoroutine merging results\n", id());
    std::inplace_merge(
      values.begin(), values.begin() + middle, values.end());

    std::cout << std::format("Thread {}: sortCoroutine done\n", id());
    co_return; // terminate coroutine and resume caller
}
```

The **sortCoroutine** operates as follows:

- Line 25 displays a message containing the thread ID in which **sortCoroutine** is running and indicating that **sortCoroutine** started. The thread ID confirms that **sortCoroutine** runs in the same thread as main.
- The **sortCoroutine** will launch two **concurrencpp** tasks that execute the lambda **sortTask** (lines 28–35). The lambda receives random-access iterators representing the beginning and end of a common range to sort. Lines 30–31 display a message containing the thread ID in which a given call to **sortTask** executes and the number of elements it is sorting. Line 32 calls the `std::sort` algorithm to sort the specified portion of the vector. When the sort completes, line 33 displays a message containing the thread ID and indicating that the task’s sort completed.
- The **sortTask** does not return a value, so each **thread_pool_executor**’s **submit** function will return a **concurrencpp::result<void>** for each task. We’ll store these in the vector `results` (defined in line 38).
- Line 40 determines the vector’s middle element, which we’ll use to divide the vector in half.
- Lines 42–43 display a message indicating the executing thread’s ID and that we’re starting the **sortTask** for the first half of the vector. Then lines 47–51 use **thread_pool_executor**’s **submit** function to create a task that calls **sortTask** to sort the elements in the range values.begin() up to, but not including, the middle values element. We store the **result** object returned by **submit** in the `results` vector. Lines 53–62 repeat these steps to launch a second task that sorts the vector elements from the middle element through the end of the vector.
- Lines 65–66 display a message containing the thread ID in which **sortCoroutine** is running and indicate that we are **co_awaiting** the **sortTask** results. Lines 67–68 use **concurrencpp**’s **when_all** function to **co_await** all the sortTasks’ results. We’ll discuss this line in more detail momentarily.
- Lines 71–72 display a message containing the thread ID in which **sortCoroutine** is running and indicate that we are merging the results. Then, lines 73–74 use the standard library algorithm `inplace_merge` to merge the vector’s two sorted halves.
- Finally, line 76 displays the thread ID of the thread in which **sortCoroutine** is currently executing and indicates that **sortCoroutine** is done. Then, line 77 uses the C++20 **co_return** statement to terminate the coroutine and return control to main. Because **sortCoroutine** does not return a value, **concurrencpp** returns a **concurrencpp::result<void>** to the coroutine’s caller. You’ll see that main uses this object’s **get** function to wait for the coroutine to finish executing.

## Using when_all with C++20’s co_await Expression

A coroutine utility function we might see in C++23 or later is **when_all**, which enables a program to wait for a set of tasks to complete. Function **when_all** receives as arguments

- Line 100 calls the `result` object's `get` method to block main from continuing until `sortCoroutine`'s asynchronous tasks finish executing.
- Once that happens, lines 102–103 display a message indicating that main is confirming values is sorted. Then, line 104 calls `std::ranges::is_sorted` with the values as an argument. This algorithm returns `true` if its argument is sorted; otherwise, it returns `false`. Finally, lines 105–106 display a message indicating whether the vector is sorted.

## Sample Output

Let’s discuss the sample output in detail. Below the output, we broke it into pieces for discussion purposes.

```text
Thread 17276: main creating vector of random ints
Thread 17276: main starting sortCoroutine
Thread 17276: sortCoroutine started

Thread 17276: sortCoroutine starting first half sortTask
Thread 17276: sortCoroutine starting second half sortTask

Thread 17276: sortCoroutine co_awaiting sortTask completion

Thread 17276: main resumed. Waiting for sortCoroutine to complete.
Thread 17144: Sorting 50000000 elements
Thread 6252: Sorting 50000000 elements
Thread 6252: Finished sorting
Thread 17144: Finished sorting

Thread 6252: sortCoroutine merging results
Thread 6252: sortCoroutine done

Thread 17276: main confirming that vector is sorted
Thread 17276: values is sorted
```

First, main displays its thread ID and creates the vector of random integers:

```text
Thread 17276: main creating vector of random ints
```

Next, main displays its thread ID and calls sortCoroutine:

```text
Thread 17276: main starting sortCoroutine
```

Then, sortCoroutine displays its thread ID and indicates that it started:

```text
Thread 17276: sortCoroutine started
```

Note that sortCoroutine executes in main’s thread, so it displays the same thread ID.

Next, sortCoroutine launches two tasks to sort the vector:

```text
Thread 17276: sortCoroutine starting first half sortTask
Thread 17276: sortCoroutine starting second half sortTask
```

At this point, sortCoroutine co_awaits completion of the tasks:

```text
Thread 17276: sortCoroutine co_awaiting sortTask completion
```

If the sortTasks have not completed, sortCoroutine suspends execution and returns control to main. We purposely created a large vector so the sorting would not complete immediately. This enables us to show that main continues executing when the coroutine suspends execution:

```text
Thread 17276: main resumed. Waiting for sortCoroutine to complete.
```
