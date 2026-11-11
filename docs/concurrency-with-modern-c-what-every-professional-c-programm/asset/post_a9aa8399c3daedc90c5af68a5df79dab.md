
![](img/d61a6c83410484053b8892275d2fcc4f_475_0.png)

## Data races with references

I made my example `copiedValueDataRace.cpp` an assumption that it is trivial for a boolean but not for a more complex type. Passing the argument by copy is data race free if the argument is a so-called value object.

![](img/d61a6c83410484053b8892275d2fcc4f_475_1.png)

### Value Object

A value object is an object whose equality is not based on identity but based on its state. Value objects should be immutable so that they stay equal for their lifetime if created equal. If you pass a value object by copy to a thread, there is no need to synchronize its access. Due to the article ValueObject<sup>2</sup> from Martin Fowler, you can think of two classes of objects: value objects and reference objects.

### 9.1.1.1.1 When a reference is actually a copy

You may think that the thread `t3` in the previous example `copiedValueDataRace.cpp` can just be replaced with `std::thread t3(byConstReference, shared)`. The program compiles and runs but what seems like a reference is a copy. The reason is that `std::decay` is applied to each argument of the thread.<sup>3</sup> `std::decay` performs lvalue-to-rvalue, array-to-pointer, and function-to-pointer implicit conversions to its type T. In particular, it invokes in this case `std::remove_reference`^1 to the type T. The program `perConstReference.cpp` uses a non-copyable type `NonCopyableClass`.

<sup>2</sup>https://martinfowler.com/bliki/ValueObject.html
<sup>3</sup>https://en.cppreference.com/w/cpp/types/decay

### Implicit copying of a per-reference thread argument

```cpp
// perConstReference.cpp

#include <thread>

class NonCopyableClass{
  public:

    // the compiler generated default constructor
    NonCopyableClass() = default;

    // disallow copying
    NonCopyableClass& operator = (const NonCopyableClass&) = delete;
    NonCopyableClass (const NonCopyableClass&) = delete;
};

void perConstReference(const NonCopyableClass& nonCopy){}

int main(){

    NonCopyableClass nonCopy;

    perConstReference(nonCopy);

    std::thread t(perConstReference, nonCopy);
    t.join();

}
```

The object `nonCopy` (line 21) is not copyable. This is fine if I invoke the function `perConstReference` with the argument `nonCopy` because the function accepts its argument per constant reference. Using the same function in the thread t (line 25) causes GCC 6 to generate a verbose compiler error with more than 300 lines:

^1 https://en.cppreference.com/w/cpp/types/remove_reference

![](img/d61a6c83410484053b8892275d2fcc4f_477_0.png)

The error message’s essential part is in the middle of the screenshot in red rounded rectangle: “error: use of deleted function”. The copy-constructor of the class NonCopyableClass is not available.

![](img/d61a6c83410484053b8892275d2fcc4f_477_1.png)

### 9.1.1.2 Lifetime Issues with References

If your thread uses its argument by reference and you detach the thread, you have to be extremely careful. The small program copiedValueLifetimeIssues.cpp has undefined behavior.

### Lifetime issues with references

```cpp
// copiedValueLifetimeIssues.cpp

#include <iostream>
#include <string>
#include <thread>

void executeTwoThreads(){

    const std::string localString("local string");

    std::thread t1([localString]{
        std::cout << "Per Copy: " << localString << '\n';
    });

    std::thread t2([&localString]{
        std::cout << "Per Reference: " << localString << '\n';
    });

    t1.detach();
    t2.detach();
}

using namespace std::chrono_literals;

int main(){

    std::cout << '\n';

    executeTwoThreads();

    std::this_thread::sleep_for(1s);

    std::cout << '\n';

}
```

executeTwoThreads (lines 7 - 21) starts two threads. Both threads are detached (lines 19 and 20) and print the local variable localString (line 9). The first thread captures the local variable by copy, and the second the local variable by reference. For simplicity reasons, in both cases, I used a lambda expression to bind the arguments.

Because the executeTwoThreads function doesn’t wait until the two threads have finished, the thread t2 refers to the local string, which is bound to the lifetime of the invoking function. This causes

```cpp
// threadLocalSummation.cpp

...

thread_local unsigned long long tmpSum = 0;

void sumUp(std::atomic<unsigned long long>& sum, const std::vector<int>& val,
           unsigned long long beg, unsigned long long end) {
  for (auto i = beg; i < end; ++i) {
    tmpSum += val[i];
  }
  sum.fetch_add(tmpSum, std::memory_order_relaxed);
}

...

std::atomic<unsigned long long> sum{};

std::thread t1(sumUp, std::ref(sum), std::ref(randValues), 0, fir);
std::thread t2(sumUp, std::ref(sum), std::ref(randValues), fir, sec);
std::thread t3(sumUp, std::ref(sum), std::ref(randValues), sec, thi);
std::thread t4(sumUp, std::ref(sum), std::ref(randValues), thi, fou);
```

You put the range-based for-loop into a function, let each thread calculate a fourth of the sum in the thread-local variable tmpSum. The line sum.fetch_add(tmpSum, std::memory_order_relaxed) finally sums up all values in the atomic sum.

I already discussed the various ways to sum up all vector elements in the chapter Calculating the Sum of a Vector. You can study the entire program there.

![](img/d61a6c83410484053b8892275d2fcc4f_480_0.png)

### Use the Algorithms of the Standard Template Library.

You should not write a loop if an algorithm of the standard template library can do the job. In this case, it's the job of std::accumulate to sum up all elements of the vector: sum = std::accumulate(randValues.begin(), randValues.end(), 0). Since C++17, you can use the std::reduce algorithm which is the parallelisable version of std::accumulate: sum = std::reduce(std::execution::par, randValues.begin(), randValues.end(), 0).

### 9.1.2.1 Further Information

- Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects

> ¹https://en.cppreference.com/w/cpp/algorithm/accumulate
> ²https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/

First, protect the critical sections by a lock such as a scoped lock or strategized locking. In object-oriented design, the critical section is typically an object including its interface. The Thread-Safe Interface protects the entire object. If the variable is never modified, synchronization is not needed by using an expensive lock or an atomic. In this case, you only have to ensure that the variable is initialized in a thread-safe way. I already discussed a few possibilities in the previous section thread-safe initialization and the case studies about thread-safe initialization of a singleton, including the infamous double-checked locking pattern.

Second, the modifying thread just signals when it is done with its work. This is the strategy of guarded suspension.

### 9.2.1 Scoped Locking

Scoped locking is the idea of RAII applied to a mutex. Scoped locking is also known as synchronized block and guard. The key idea of this idiom is to bind the resource acquisition and release to an object's lifetime. As the name suggests, the lifetime of the object is scoped. Scoped means that the C++ run time is responsible for object destruction and, therefore, for releasing the resource.

The class `ScopedLock` implements scoped locking.

**Scoped Locking**

```cpp
// scoped_lock.cpp

#include <iostream>
#include <mutex>
#include <new>
#include <string>

class ScopedLock{
private:
    std::mutex& mut;
public:
    explicit ScopedLock(std::mutex& m): mut(m){
        mut.lock();
        std::cout << "Lock the mutex: " << &mut << '\n';
    }
    ~ScopedLock(){
        std::cout << "Release the mutex: " << &mut << '\n';
        mut.unlock();
    }
};

int main(){

    std::cout << '\n';

    std::mutex mutex1;
    ScopedLock scopedLock1{mutex1};

    std::cout << "\nBefore local scope" << '\n';
    {
        std::mutex mutex2;
        ScopedLock scopedLock2{mutex2};
    }
    std::cout << "After local scope" << '\n';

    std::cout << "\nBefore try-catch block" << '\n';
    try{
        std::mutex mutex3;
        ScopedLock scopedLock3{mutex3};
        throw std::bad_alloc();
    }
    catch (std::bad_alloc& e){
        std::cout << e.what();
    }
    std::cout << "\nAfter try-catch block" << '\n';

    std::cout << '\n';
}
```

ScopedLock gets its mutex by reference (line 12). The mutex is locked in the constructor (line 13) and unlocked in the destructor (line 18). Thanks to the RAII idiom, the object's destruction and, therefore, the unlocking of the mutex is done automatically.

Scoped locking has the following advantages and disadvantages.

- Advantage:
  - Robustness, because the locks are automatically acquired and released
- Disadvantages:
  - Recursive locking of a `std::mutex` is undefined behavior and may typically cause a deadlock
  - Locks are not automatically released if the C function `longjmp`^13 is used; `longjmp` does not call C++ destructors of scoped objects

^13https://en.cppreference.com/w/cpp/utility/program/longjmp
