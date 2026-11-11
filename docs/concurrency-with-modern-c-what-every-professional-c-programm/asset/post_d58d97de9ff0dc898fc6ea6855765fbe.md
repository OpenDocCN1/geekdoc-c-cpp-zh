
|  |  |
|---|---|
| `std::osyncstream` | `std::basic_osyncstream<char>` |
| `std::wosyncstream` | `std::basic_osyncstream<wchar_t>` |

You can create a named-synchronized output stream. Here is how the previous program coutUnsynchronized.cpp is refactored to write synchronized to std::cout.

## Synchronized access of std::cout with std::basic_osyncstream

```cpp
// synchronizedOutput.cpp

#include <chrono>
#include <iostream>
#include <syncstream>
#include <thread>

class Worker{
public:
    Worker(std::string n):name(n) {};
    void operator() (){
        for (int i = 1; i <= 3; ++i) {
            // begin work
            std::this_thread::sleep_for(std::chrono::milliseconds(200));
            // end work
            std::osyncstream syncStream(std::cout);
            syncStream << name << ": " << "Work " << i << " done !!!" << '\n';
        }
    }
private:
    std::string name;
};


int main() {

    std::cout << '\n';

    std::cout << "Boss: Let's start working.\n\n";

    std::thread herb= std::thread(Worker("Herb"));
    std::thread andrei= std::thread(Worker("  Andrei"));
    std::thread scott= std::thread(Worker("    Scott"));
    std::thread bjarne= std::thread(Worker("      Bjarne"));
    std::thread bart= std::thread(Worker("        Bart"));
    std::thread jenne= std::thread(Worker("          Jenne"));

    herb.join();
    andrei.join();
    scott.join();
    bjarne.join();
    bart.join();
    jenne.join();

    std::cout << "\n" << "Boss: Let's go home." << '\n';

    std::cout << '\n';

}
```

The only change to the previous program coutUnsynchronized.cpp is that std::cout is wrapped in a std::osyncstream (line 16). To use the std::osyncstream, I add the header `<syncstream>`. When the std::osyncstream goes out of scope in line 17, the characters are transferred, and std::cout is flushed. It is worth mentioning that the std::cout calls in the main program do not introduce a data race and have, therefore, not be synchronized.

Because I use the syncStream declared on line 17 only once, a temporary object may be more appropriate. The following code snippet presents the modified call operator.

```cpp
void operator()() {
    for (int i= 1; i <= 3; ++i) {
        // begin work
        std::this_thread::sleep_for(std::chrono::milliseconds(200));
        // end work
        std::osyncstream(std::cout) << name << ": " << "Work " << i << " done !!!" 
                                    << '\n';
    }
}
```

std::basic_osyncstream syncStream offers two interesting member functions.

- `syncStream.emit()` emits all buffered output and executes all pending flushes.
- `syncStream.get_wrapped()` returns a pointer to the wrapped buffer.

cppreference.com²⁰ shows how you can sequence the output of different output streams with the get_wrapped member function.

²⁰https://en.cppreference.com/w/cpp/io/basic_osyncstream/get_wrapped

## Sequence output

```cpp
// sequenceOutput.cpp

#include <syncstream>
#include <iostream>

int main() {

    std::osyncstream bout1(std::cout);
    bout1 << "Hello, ";
    {
        std::osyncstream(bout1.get_wrapped()) << "Goodbye, " << "Planet!" << '\n';
    } // emits the contents of the temporary buffer

    bout1 << "World!" << '\n';

} // emits the contents of bout1
```

![](img/d61a6c83410484053b8892275d2fcc4f_242_0.png)

Synchronized access to `std::cout`

## Distilled Information

- C++ supports two kinds of threads: the basic thread std::thread (C++11) and the improved thread std::jthread (C++20).
  - A std::thread gets a callable as work package and starts immediately. The creator of a thread is responsible for the created thread. Either the creator waits until the created thread is done (t.join()) or the creator detaches (t.detach()) itself from the created thread. A thread is joinable if no operation t.join() or t.detach() was performed on it. A joinable thread calls std::terminate in its destructor, and the program terminates.
  - A std::jthread extends the interface of a std::thread. It automatically joins in its destructor and supports cooperative interruption.
- You have to coordinate access to a shared variable if more than one thread uses it simultaneously and the variable is mutable. A mutex guarantees that only one thread can access a shared variable at any given time. You should encapsulate a mutex in a lock to release the mutex automatically and, therefore, overcome the many issues of mutexes. C++ offers mutex and locks in many variations.
- If shared data is read-only, it's sufficient to initialize it in a thread-safe way. C++ offers various ways to achieve this, including using a constant expression, a static variable with block scope, or the function std::call_once combined with the flag std::once_flag.
- Declaring a variable as thread-local ensures that each thread gets its copy. The lifetime of thread-local data is bound to the lifetime of its thread.
- Condition variables enable threads to be synchronized via messages. One thread acts as the sender while the other acts as the receiver of the message. The receiver blocks waiting for the message from the sender.
- std::jthread and std::condition_variable_any support cooperative interruption by design. Cooperative interruption is based on the std::stop_source, std::stop_token, and the std::stop_callback.
- Semaphores are a synchronization mechanism used to control concurrent access to a shared resource. The counter of a semaphore is initialized in the constructor. Acquiring the semaphore decreases the counter, and releasing the semaphore increases the counter. If a thread tries to acquire the semaphore when the counter is zero, the thread will block until another thread increments the counter by releasing the semaphore.
- Latches and barriers are coordination types that enable some threads to block until a counter becomes zero. The counter is initialized in the constructor.
- Tasks have a lot in common with threads. While you explicitly create a thread, a task is just a job you start. The C++ runtime automatically handles the task's lifetime, such as in the simple case of std::async. Tasks are like data channels between two communication endpoints. They enable thread-safe communication between threads. The promise as one endpoint puts data into the data channel, the future at the other endpoint picks the value up. The data can be a value, an exception, or simply a notification. In addition to std::async, C++ has the class templates std::promise and std::future that give you more control over the task.
- C++ enables synchronized output streams. A synchronized output stream accumulates output in its buffer and flushes it when it is destructed. Consequently, the content appears as a contiguous sequence of characters, and no interleaving of characters can happen

## 4. Parallel Algorithms of the Standard Template Library

![](img/d61a6c83410484053b8892275d2fcc4f_244_0.png)

Cippi clones herself

The Standard Template Library has more than 100 algorithms for searching, counting, and manipulating ranges and their elements. With C++17, 69 of them get new overloads, and eight new ones are added. The overloaded, and new algorithms can be invoked with a so-called execution policy.

![](img/d61a6c83410484053b8892275d2fcc4f_245_0.png)

Parallel algorithms of C++17

Using an execution policy, you can specify whether the algorithm should run sequentially, in parallel, or parallel with vectorization. For using the execution policy, you have to include the header `<execution>`.

```cpp
14
15 // permitting parallel and vectorized execution, but no interleaving of individual threads
16 std::sort(std::execution::unseq, v.begin(), v.end());
```

The example shows that you can still use the classic variant of std::sort (line 4). Besides, in C++17, you can specify explicitly whether the sequential (line 7), parallel (line 10), or the parallel and vectorized (line 13) version should be used.

Thanks to std::is_execution_policy you can check, whether T is a standard or implementation-defined execution policy type: std::is_execution_policy<T>::value. The function checks whether T is a standard or implementation-defined execution policy type. The expression evaluates to true, if T is std::execution::sequenced_policy, std::execution::parallel_policy, std::execution::unsequenced_policy, std::execution::parallel_unsequenced_policy, or an implementation-defined execution policy type. Otherwise, value is equal to false.

### 4.1.1 Parallel and Vectorized Execution

Whether an algorithm runs in a parallel and vectorized way depends on many factors. For example, it depends on whether the CPU and the operating system support SIMD instructions. Additionally, it also depends on the compiler and the optimization level you used to translate your code.

The following example shows a simple loop for filling a vector.

**Filling a vector**

```cpp
1  const int SIZE= 8;
2
3  int vec[] = {1, 2, 3, 4, 5, 6, 7, 8};
4  int res[] = {0, 0, 0, 0, 0, 0, 0, 0};
5
6  int main(){
7      for (int i = 0; i < SIZE; ++i) {
8          res[i] = vec[i]+5;
9      }
10 }
```

Line 8 is the crucial line in this small example. Thanks to Compiler Explorer⁴, we can have a closer look at the assembler instructions generated by clang 3.6.

#### 4.1.1.1 Without Optimization

Here are the assembler instructions. Each addition is done sequentially.

⁴https://godbolt.org/
