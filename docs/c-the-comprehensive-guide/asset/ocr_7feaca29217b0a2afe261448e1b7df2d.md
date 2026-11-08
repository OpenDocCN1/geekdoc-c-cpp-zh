# 29.3  Other Synchronization Options

There are special tasks for which a mutex with a lock is unsuitable. In this section, I will show you a few cases that you can solve using the tools of the standard library.

# 29.3.1  Call Only Once with “once_flag” and “call_once”

It often happens that you do not want to create a large object in advance just because it might be used later. You want to create the object only on first use—the so-called *lazy initialization*, or sometimes called *late initialization*. With only one thread, you could hold a global unique_ptr to the object and initialize it only on first use.

```
```cpp
// https://godbolt.org/z/T7vehq58b
std::shared_ptr<BigData> bigData{};
BigData& getBigData() {
    if(!bigData) bigData.reset(new BigData{});
    return *bigData;
}

int useBigData() {
    auto bigData = getBigData();
    // bigData->...
}
```
```

**Listing 29.24** Late initialization with a single thread.

This is problematic with multiple threads. If two threads call getBigData() simultaneously, BigData will be initialized twice. You could protect the entire function with a mutex, but there's a more effective way, as in the following listing.

```
```cpp
// https://godbolt.org/z/3vcnzfqfM
#include <mutex> // once_flag, call_once
std::shared_ptr<BigData> bigData{};
std::once_flag bigDataInitFlag;
void initBigData() {
    bigData = std::make_shared<BigData>();
}
int useBigData() {
    std::call_once(bigDataInitFlag, initBigData);
    // bigData->...
}
```
```

**Listing 29.25** Late initialization with multiple threads.

This way, useBigData can be called within threads, and the standard library guarantees that initBigData is called exactly once. You see that the function is passed here as a