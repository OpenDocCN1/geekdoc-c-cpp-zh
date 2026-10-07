# 7.5 Atomic Operation and Model CHAPTER 07 PARALLELISM AND CONCURRENCY

```
#include <atomic>
#include <thread>
#include <iostream>
```

```
std::atomic<int> count = {0};
```

```
int main() {
    std::thread t1([](){
        count.fetch_add(1);
    });
    std::thread t2([](){
        count++; // identical to fetch_add
        count += 1; // identical to fetch_add
    });
    t1.join();
    t2.join();
    std::cout << count << std::endl;
    return 0;
}
```

Of course, not all types provide atomic operations because the feasibility of atomic operations depends on the architecture of the CPU and whether the type structure being instantiated satisfies the memory alignment requirements of the architecture, so we can always pass std::atomic<T>::is_lock_free to check if the atom type needs to support atomic operations, for example:

```
#include <atomic>
#include <iostream>
```

```
struct A {
    float x;
    int y;
    long long z;
}
```

```
int main() {
    std::atomic<A> a;
    std::cout << std::boolalpha << a.is_lock_free() << std::endl;
    return 0;
}
```