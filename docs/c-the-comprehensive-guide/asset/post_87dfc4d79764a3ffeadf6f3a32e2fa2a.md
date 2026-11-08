
## Parameter by Move

Instead of a copy or reference, assume you have a resource that you cannot or do not want to copy, but you can move—for example, a unique_ptr (copying forbidden) or an Image you painted (copying expensive). In that case, you use std::move, and the source object is empty after starting the thread.

```cpp
// https://godbolt.org/z/Pjzqsv9nz
// ... includes ...
#include <thread>
using namespace std::chrono; // seconds, suffix s
struct Image {
    std::vector<char> data_; // Copying expensive
    explicit Image() : data_(1'000'000) {}
};
void showImage(Image img) {
    std::cout << img.data_.size() << '\n';
}
void showPtr(std::unique_ptr<int> iptr) {
    std::cout << *iptr << '\n';
}
int main() {
    // expensive to copy, but good to move:
    Image image{};
    std::cout << image.data_.size() << std::endl;     // Output: 1000000
    std::jthread th1{ showImage, std::move(image) };  // Output: 1000000
    std::this_thread::sleep_for(1s);
    std::cout << image.data_.size() << std::endl;     // Output: 0
    th1.join(); // explicitly wait until the thread is done
    // impossible to copy, but good to move:
    auto iptr = std::make_unique<int>( 657 );
    std::cout << (bool)iptr << std::endl;             // Output: 1 for true
    std::jthread th2{ showPtr, std::move(iptr) };     // Output: 657
    std::this_thread::sleep_for(1s);
    std::cout << (bool)iptr.get() << std::endl;       // Output: 0 for false
}
```

**Listing 29.7** Using “move” to transfer inputs to the thread.

The Image class contains data representing a large actual image. I choose vector as the container for the data because it can be moved. And because I adhere to the rule of zero, the Image class is also movable.

Before I start th1, image.data_ contains a lot of data. Due to std::move in the constructor of th1, the image or its content is moved into the thread. The local variable image in main is empty afterward, as indicated by the size 0.

It is similar with *iptr*, except that you cannot even copy a *unique_ptr*, even if you wanted to. Before creating th2, the pointer held by *iptr* is valid: `(bool)iptr` outputs 1, which stands for *true*. After moving at the start of th2, the same expression outputs 0 for *false*, which means that *iptr* no longer contains an int. It was moved into the thread function `showPtr`.

### 29.1.6 Moving a Thread

You do not need to keep `jthread` as a local variable. You can have a function or method create `jthread` instances—that is, return them as values.

```cpp
// https://godbolt.org/z/Kv84eb96E
#include <iostream>
#include <thread>
#include <chrono>
using namespace std::chrono; // seconds, suffix s
auto makeThread(std::string who) {
    return std::jthread([who] {
        std::this_thread::sleep_for(1s);
        std::cout << "Good luck, " << who << std::endl;
    });
}
int main() {
    auto th = makeThread("Jim"); // Output: Good luck, Jim
    th.join();
}
```

**Listing 29.8** Returning a thread.

You cannot copy `jthread`. If you want to pass a thread as a parameter, you have to move it.

```cpp
// https://godbolt.org/z/8cMTrEWz6
#include <thread>
#include <chrono>
using namespace std::chrono; // seconds, suffix s
void yourMission(std::jthread job) {
    job.join();
}
int main() {
    std::jthread th( [] {
        std::this_thread::sleep_for(1s);
        std::cout << "should you choose to accept it" << std::endl;
    });
    yourMission( std::move(th) ); // Transfer responsibility
}
```

**Listing 29.9** Moving a thread.

The th instance in main is moved to the thread function. It would be fine to exit main and let th be removed. The responsibility has been transferred to the thread function. In this specific example, it is just waiting for the thread to finish anyway, but as far as the lifetime of th in main is concerned, detach would also be okay.

The most practical aspect of jthread is that containers can hold them. This way, you can manage a completely dynamic number of threads with little effort.

```cpp
// https://godbolt.org/z/YrEPnYMaP
#include <iostream>
#include <thread>
#include <vector>
using std::cout; using std::endl;
long fib(long n) { return n<=1 ? n : fib(n-1)+fib(n-2); }
void runFib(long n) { auto r = fib(n); cout << "fib("<<n<<")=" << r << endl; }
int main() {
    std::vector<std::jthread> threads;
    // starten
    for( auto n : { 38, 39, 40, 41, 42, 43, }) {
        threads.emplace_back(runFib, n );
    }
}
```

**Listing 29.10** Threads in containers.

Not even waiting with join() on the elements of the container is necessary because the destructor of jthread takes care of that.

As you know, emplace_back creates the threads directly in place in the vector, but you can also use one of these two variants:

```cpp
std::jthread th1(runFib, n);
threads.push_back( std::move(th1) );             // Moving a thread variable
threads.push_back( std::jthread(runFib, n) );    // temp-value automatically moved
```

With thread instead of jthread, don't forget to join all threads in the container at the end using join().

The hardware level: the more expensive Intel CPUs support *hyperthreading*. That means, for example, they have four **cores** (quasi-CPUs), each of which can run two hyperthreads. Hyperthreading means that one thread can theoretically utilize a core at 100%, two threads as well, but from three onward the CPU has to switch between the threads. Consequently, for a four-core CPU with dual hyperthreading, the optimal number of threads would be between four and eight. Whether `hardware_concurrency()` returns 0, 4, 8, or something entirely different is not specified.

```cpp
// https://godbolt.org/z/zojG68dWq
#include <thread>
#include <iostream>
#include <vector>
#include <chrono> //steady_clock
using std::cout; using std::endl; using namespace std::chrono;
long fib(long n) { return n<=1 ? n : fib(n-1)+fib(n-2); }

int main() {
    cout << std::thread::hardware_concurrency() << '\n';
    for(int nthreads : { 1,2,3,4,5,6 }) {
        cout << "Threads: ";
        const auto start = steady_clock::now();

        std::vector<std::thread> threads;
        for(int ti = 1; ti <= nthreads; ++ti) {
            threads.emplace_back(std::thread(fib, 40));
            cout << ti << " ... "; cout.flush();
        }

        for(auto &th : threads) th.join(); // explicitly join before timing

        const auto now = steady_clock::now();
        cout << " Time: " << duration_cast<milliseconds>(
            now-start).count()<<"ms\n";
    }
}
```

**Listing 29.11** Finding out the hardware concurrency.

Here, I sequentially calculate `fib(40)` one to six times in parallel and measure how long the calculations take. With `steady_clock::now()`, I get the current time before and after each series of calculations. The difference is the time taken. The `duration_cast` ensures that I get the output in a known time unit.

In the vector `threads`, I collect the thread instances. After starting the threads, I need to call `join()` on all elements of the container to wait until all are finished to measure the time.

For example, I have an Intel CPU i7-3520M with two cores, each with two hyperthreads.

The previous program outputs 4 for me.

And the required times for parallel computation of `fib(40)` are as follows:

```text
Threads: 1...    Time: 727ms
Threads: 1... 2...    Time: 758ms
Threads: 1... 2... 3...    Time: 1113ms
Threads: 1... 2... 3... 4...    Time: 1274ms
Threads: 1... 2... 3... 4... 5...    Time: 1703ms
Threads: 1... 2... 3... 4... 5... 6...    Time: 1955ms
```

Although 4 is returned for hardware parallelism, only two computations are actually fully parallelized. While the hardware may be able to execute up to four threads without significant context-switching overhead, they still steal computation time from each other. Note, however, that it was still faster to execute four `fib(40)` in parallel with `1274ms` than to compute two `fib(40)` in parallel twice in a row, which takes 2 × 758ms = 1516ms.

### 29.1.8 Which Thread Am I?

The `std::this_thread` variable always represents the current thread. Its `get_id()` method returns a variable of type `std::thread::id`. You can compare this variable using `==`, and you can also apply a hash to it. This means you can put it in associative containers like `map` and `unordered_set`. A thread can then identify itself and, for example, retrieve data associated with it from a container.

You can also output an `id`, but how the output looks is implementation-dependent.

```cpp
// https://godbolt.org/z/TM6c7cdss
#include <thread>
#include <iostream>

int main() {
    std::cout << "Main: " << std::this_thread::get_id() << '\n';
    std::jthread th { [] {
        std::cout << "Thread: " << std::this_thread::get_id() << '\n';
    }};
}
```

**Listing 29.12** Each thread has an identifier.

The output can be different with each program run, but it doesn't have to be:

```text
Main: 139822070269824
Thread: 139822053463808
```
