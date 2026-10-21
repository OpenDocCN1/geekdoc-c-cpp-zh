

考虑以下示例：

pmr/pmrnul.l.cpp

```
#include <iostream>
#include <string>
#include <unordered_map>
#include <array>
#include <cstddef>  // for std::byte
#include <memory_resource>

int main()
{
    // use memory on the stack without fallback on the heap:
    std::array<std::byte, 200000> buf;
    std::pmr::monotonic_buffer_resource pool{buf.data(), buf.size(),
                                            std::pmr::null_memory_resource()};

    // and allocate too much memory:
    std::pmr::unordered_map<long, std::pmr::string> coll {&pool};
    try {
        for (int i=0; i<buf.size(); ++i) {
            std::string s{"Customer" + std::to_string(i)};
            coll.emplace(i, s);
        }
    }
    catch (const std::bad_alloc& e) {
        std::cerr << "BAD ALLOC EXCEPTION: " << e.what() << '\n';
    }
    std::cout << "size: " << coll.size() << '\n';
}
```

我们在栈上分配内存并将其传递给单调缓冲区作为内存资源：

```
std::array<std::byte, 200000> buf;
std::pmr::monotonic_buffer_resource pool{buf.data(), buf.size(),
                                        std::pmr::null_memory_resource()};
```

通过同时将 null_memory_resource() 作为后备内存资源传递，我们确保任何尝试分配更多内存都会抛出异常，而不是在堆上分配内存。

其效果是 sooner or later 程序会结束，例如，以下输出：

```
BAD ALLOC EXCEPTION: bad allocation
size: 2048
```

当堆内存分配不是一个选项时，这有助于获得合理的反馈，而不是陷入需要避免的行为。

## 29.2 定义自定义内存资源

你可以提供自定义内存资源。为此，你需要：

- 派生自 std::pmr::memory_resource
- 实现私有成员
  - do_allocate() 用于分配内存
  - do_deallocate() 用于释放内存
  - do_is_equal() 用于定义你的类型何时可以与其他内存资源对象互换分配的内存

下面是一个完整的示例，它只是允许我们跟踪任何其他内存资源的分配和释放：

```
pmr/tracker.hpp
#include <iostream>
#include <string>
#include <memory_resource>

class Tracker : public std::pmr::memory_resource
{
private:
    std::pmr::memory_resource* upstream; // wrapped memory resource
    std::string prefix{};
public:
    // we wrap the passed or default resource:
    explicit Tracker(std::pmr::memory_resource* us)
        : upstream{us} {
    }
    explicit Tracker(std::string p, std::pmr::memory_resource* us)
        : prefix{std::move(p)}, upstream{us} {
    }
private:
    void* do_allocate(size_t bytes, size_t alignment) override {
        std::cout << prefix << "allocate " << bytes << " Bytes\n";
        void* ret = upstream->allocate(bytes, alignment);
        return ret;
    }
    void do_deallocate(void* ptr, size_t bytes, size_t alignment) override {
        std::cout << prefix << "deallocate " << bytes << " Bytes\n";
        upstream->deallocate(ptr, bytes, alignment);
    }
    bool do_is_equal(const std::pmr::memory_resource& other) const noexcept
    {
        return upstream->is_equal(other);
    }
};
```

```
// track allocating chunks of memory (starting with 10k) without deallocating:
Tracker track1{"keeppool:"};
std::pmr::monotonic_buffer_resource keeppool{10000, &track1};
{
    Tracker track2{"  syncpool:", &keeppool};
    std::pmr::synchronized_pool_resource pool{&track2};

    for (int j=0; j < 100; ++j) {
        std::pmr::vector<std::pmr::string> coll{&pool};
        coll.reserve(100);
        for (int i=0; i < 100; ++i) {
            coll.emplace_back("just a non-SSO string");
        }
        if (j==2) std::cout << "--- third iteration done\n";
    } // deallocations are given back to pool, but not deallocated
    // so far nothing was allocated
    std::cout << "--- leave scope of pool\n";
}
std::cout << "--- leave scope of keeppool\n";
} // deallocates all allocated memory
}
```

输出可能看起来像这样：

```
syncpool:allocate 48 Bytes
keeppool:allocate 10000 Bytes
syncpool:allocate 16440 Bytes
keeppool:allocate 16464 Bytes
syncpool:allocate 96 Bytes
keeppool:allocate 24696 Bytes
syncpool:deallocate 48 Bytes
syncpool:allocate 312 Bytes
syncpool:allocate 568 Bytes
syncpool:allocate 1080 Bytes
syncpool:allocate 2104 Bytes
syncpool:allocate 4152 Bytes
syncpool:deallocate 312 Bytes
syncpool:deallocate 568 Bytes
syncpool:deallocate 1080 Bytes
syncpool:deallocate 2104 Bytes
syncpool:allocate 8248 Bytes
syncpool:deallocate 4152 Bytes
--- third iteration done
--- leave scope of pool
syncpool:deallocate 8248 Bytes
syncpool:deallocate 16440 Bytes
syncpool:deallocate 96 Bytes
--- leave scope of keeppool
keeppool:deallocate 24696 Bytes
keeppool:deallocate 16464 Bytes
keeppool:deallocate 10000 Bytes
```

输出演示了以下内容：

- 通过对象的第一次分配，syncpool 分配 48 字节，这导致 keeppool 分配其初始的 10,000 字节。这 10,000 字节在堆上分配，使用 keeppool 初始化时来自 get_default_resource() 的资源。
- 后续对象分配和释放内存，这导致 syncpool 不时从中分配更多内存块，但也释放内存块。如果 syncpool 有效分配的内存多于 keeppool 已分配的内存，keeppool 再次从堆分配更多内存。也就是说，只有 keeppool 分配才会成为（相当昂贵的）系统调用。
- 通过额外跟踪第三次迭代结束，你可以看到所有这些分配都在外部循环的前三次迭代期间发生。然后（重新）使用的内存量保持稳定。因此，后续的 97 次迭代根本不会从操作系统分配内存。
- 即使 syncpool 已释放其所有内存，keeppool 也不会释放任何内存。
- 只有在 keeppool 被销毁时，已分配的六个内存块才会被真正释放，调用 ::delete（或使用 set_default_resource() 在 keeppool 初始化时定义的内容）。

如果我们在此程序中引入第三个跟踪器，我们也可以跟踪对象何时从 syncpool 分配和释放内存：

```
// track each call, the effect in the sync pool, and the effect in the mono pool:
Tracker track1{"keeppool:"};
std::pmr::monotonic_buffer_resource keepAllocatedPool{10000, &track1};
Tracker track2{"  syncpool:", &keepAllocatedPool};
std::pmr::synchronized_pool_resource syncPool{&track2};
Tracker track3{"     objects:", &syncPool};
...
std::pmr::vector<std::pmr::string> coll{&track3};
```

### 29.2.1 内存资源的相等性

让我们简要讨论 do_is_equal()，该函数定义了两个内存资源何时可以互换。此函数需要比最初预期的更多思考。

在我们的跟踪器中，我们定义了如果它们都是 Tracker 类型并且使用相同的 prefix，则分配器是可互换的：

```
bool do_is_equal(const std::pmr::memory_resource& other) const noexcept override {
    // same object?:
    if (this == &other) return true;
    // same type and prefix and equal upstream?:
    auto op = dynamic_cast<const Tracker*>(&other);
    return op != nullptr && op->prefix == prefix
        && upstream->is_equal(other);
}
```

这具有以下效果：

```
Tracker track1{"track1:"};
Tracker track2{"track2:"};

std::pmr::string s1{"more than 15 chars", &track1};    // allocates with track1
std::pmr::string s2{std::move(s1), &track1};            // moves (same tracker)
std::pmr::string s3{std::move(s2), &track2};            // copies (different prefix)
std::pmr::string s4{std::move(s3)};                     // moves (allocator copied)
std::string s5{std::move(s4)};                          // copies (other allocator)
```

也就是说，只有当源和目标具有可互换的分配器时，移动才作为移动执行。这是使用多态分配类型时移动构造函数的情況（新对象复制了分配器）。然而，如果需要不可互换的分配器（如这里前缀不同的跟踪器）或如果使用不同分配器类型（如移动到使用默认分配器的 std::string），内存将被复制。因此，可互换性会影响移动的性能。

如果我们只通过检查类型使所有 Tracker 类型的内存资源可互换：

```
bool do_is_equal(const std::pmr::memory_resource& other) const noexcept override {
    // all Tracker's are interchangeable if they have the same type:
    return this == &other || dynamic_cast<const Tracker*>(&other) != nullptr;
}
```

我们将得到以下行为：

```
Tracker track1{"track1:"};
Tracker track2{"track2:"};

std::pmr::string s1{"more than 15 chars", &track1};    // allocates with track1
std::pmr::string s2{std::move(s1), &track1};            // moves (same tracker type)
std::pmr::string s3{std::move(s2), &track2};            // moves (same tracker type)
std::pmr::string s4{std::move(s3)};                     // moves (allocator copied)
std::string s5{std::move(s4)};                          // copies (other allocator)
```

正如你所见，其效果将是使用 track1 分配的内存通过 s3 传递给 s4，两者都使用 track2，从而得到：

```
track1:allocate 32 Bytes
track2:deallocate 32 Bytes
```

如果我们的内存资源没有不同的状态（即没有前缀），这将是一个良好的实现，因为它提高了移动的性能。

因此，使内存资源可互换是值得的，因为较少的移动会转换为复制。然而，你不应该使其比其用途需要的更可互换。

