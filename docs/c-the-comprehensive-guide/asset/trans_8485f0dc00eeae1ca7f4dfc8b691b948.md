
第二个数据竞争检测起来更棘手一些；它发生在 `top()` 和 `pop()` 之间。³ 我将让上一段代码中两个线程的执行过程更清晰一些。时间线自上而下延伸，线程并排显示。

³ 严格来说，这不是一种具有未定义行为的数据竞争，而是一种竞态条件，会导致难以发现的错误行为。

```cpp
/* Thread 1*/                         /* Thread 2*/
if( ! mxs.isEmpty()) {                 if( ! mxs.isEmpty()) {

    const auto value = mxs.top();          const auto value = mxs.top();

    mxs.pop();                              mxs.pop();
    // ... more code ...                    // ... more code ...
}
```

**清单 29.20** 两个线程执行上一段代码的一种可能方式。

假设我们一开始有一个栈 `mxs = {1,2,3}`。那么在前两行中，两个线程都正确地判断出栈非空。然而，二者都使用 `top()` 从栈中取出栈顶元素 3。直到这时，两个栈才执行 `pop()`，不仅移除了 3，还移除了 2。结果就是 3 被处理了两次，而 2 完全没有被考虑。

即使我在内部用互斥量很好地保护了 `MxStack`，防止出现不一致的操作，但整体上 MxStack 接口的使用方式对于并行操作来说仍然不够充分。

解决方案在于修改接口：它必须确保典型操作是一致的。这意味着什么在很大程度上取决于具体应用。如有疑问，应当提供一个精简的接口，不要用不必要的方法使其过载。这样用户更容易从接口规范中识别出正确的操作。

一个能解决我们问题的示例由接口中的以下修改组成：

- `top()` 和 `pop()` 必须合并为一次调用。
- 单独的 `isEmpty()` 是不安全的，必须由 `pop()` 可能抛出的异常来补充。

一个带有实现的简单接口可能如下面的清单所示。

```cpp
// https://godbolt.org/z/vcb9qP8jK
#include <vector>
#include <thread>
#include <mutex>
#include <iostream>
#include <numeric>    // iota
#include <concepts>   // copyable

/* T: noexcept copyable and assignable */
template<std::copyable T>
class MxStack {
    std::vector<T> data_;
    std::mutex mx_;

public:
    MxStack() : data_{} {}

    bool isEmpty() const { return data_.empty(); }

    void push(const T& val) {
        std::lock_guard<std::mutex> g{mx_};
        data_.push_back(val);
    }

    T pop() {
        std::lock_guard g{mx_};
        if(data_.empty())
            throw std::length_error("empty stack");
        T tmp{std::move(data_.back())};
        data_.pop_back();
        return tmp;
    }
};

int main() {
    // Prepare stack
    MxStack<int> mxs{};
    for(int i=1; i<=1'000'000; ++i) mxs.push(i);
    // Define computation
    auto sumIt = [&mxs](long &sum) {
        int val{};
        try {
            while(! mxs.isEmpty()) {
                sum += mxs.pop(); // might still throw
            }
        } catch(std::length_error &ex) {}
    };
    // Compute
    long sum1 = 0;              // for partial result
    std::jthread th1(sumIt, std::ref(sum1));
    long sum2 = 0;                 // for partial result
    std::jthread th2(sumIt, std::ref(sum2));
    th1.join(); th2.join();
    long sum = sum1 + sum2;         // Total result
    // Result
    std::cout << "Expected result: "
              << (1'000'000L*1'000'001)/2 << '\n'; // Output: 500000500000
    std::cout << "Actual: "
              << sum << '\n';                    // Output: 500000500000
}
```

**清单 29.21** 一个非常简单的线程安全栈。

关于并发，可以这样说：

- `push` 和 `pop` 都分别在同一互斥量上由 `lock_guard` 保护，因此它们不会相互干扰。
- `isEmpty` 不需要保护。
- 如果容器为空，`pop` 可以抛出异常。
- `pop` 尝试将元素从内部 vector 中移出。为此，`T` 应当支持移动。如果不支持，则会进行复制。
- 重要的是，复制或移动 `T` 不会抛出异常。如果你在 `pop()` 期间这样做，值尚未成功写入，却已经从栈中移除了。这被称为*非异常安全*。
- 要使 `pop` 方法具备异常安全性，可以采取其他措施，但这超出了本章的范围。

在 MxStack 的影响之外，我还必须为并行性考虑另一件事。我让 `th1` 和 `th2` 分别在单独的变量 `sum1` 和 `sum2` 中累加它们的和。如果我在单个 `sum` 变量中这样做，就必须再次用单独的互斥量保护写访问 `sum += val`。

如你所知，即使 `sumIt` 的参数是引用参数，`sum1` 和 `sum2` 也会被复制到线程中。因此，在将它们传递给线程时，我用 `std::ref` 包装这些变量，以保持引用属性。

> **针对每个互斥量考虑你是否真的需要它**
>
> 互斥量或对其加锁会显著降低计算机的速度。如果你找到一种无需互斥量即可执行操作的方法，那就值得这样做。
>
> 有时，事先将部分输入复制到每个线程中也是有利的——或者——像示例中那样——在最后合并部分结果。

首先，通过避免加锁，你很可能会加快程序速度；其次，你少了一个潜在的错误来源——即共享数据访问。

一般性说明是，`MxStack` 的复制和赋值会被自动禁止，因为数据字段互斥量既不可复制也不可赋值。`MxStack` 的接口可以通过用 `= delete` 再次列出这两个操作来明确这一点。或者，你也可以实现这些操作。不过，我只会在确实必要时才这样做，因为手工实现完美的复制和赋值操作并不容易。如有必要，我更推荐移动操作。一方面，这有助于你可以移动互斥量；另一方面，例如，你可以随后从函数返回 `MxStack`。

## 29.2.6 锁可能导致死锁

对互斥量多次加锁有可能导致死锁。例如，如果 `MxStack` 的一个方法调用另一个方法，而两者都试图锁定该互斥量，那么第二次调用将永远等待。用伪代码表示，大致如下：

```cpp
class MxStack {
    bool isEmpty() const {
        std::lock_guard<std::mutex> g{mx_};
        return data_.empty();
    }
    T pop() {
        std::lock_guard<std::mutex> g{mx_};
        if(data_.isEmpty()) ... // ⚠ lock inside a lock
    }
};
```

当两个不同线程中的两个操作 `a` 和 `b` 需要锁定两个互斥量 `mx` 和 `my` 时，也可能出现类似情况。再次用伪代码表示：

```cpp
Thread 1:                         Thread 2:
operation a():                     operation b():
    mx.lock()                         my.lock()

    my.lock()                         mx.lock()
    /* Work a... */                   /* Work b... */
```

在这里呈现的情形下，线程 1 等待 `my` 被释放，线程 2 等待 `mx` 被释放。但这两件事都永远不会发生，因为每个线程都在等待——这就是死锁。

## 始终按相同顺序锁定多个互斥量

如果多个操作各自需要锁定多个互斥量，就应当始终*按相同的顺序*进行。至少对于简单场景，这样就可以排除死锁。在更复杂的系统中，这种保证在实践中迟早并不总是能够做到。

标准库提供了一种同时锁定多个互斥量的方法，从而消除这些场景中的死锁风险。一个典型例子是大型数据结构的 `swap` 方法，其中每个实例都由自己的互斥量保护，例如来自[清单 29.21]的 `MxStack`。在下一个清单中，你会看到一个 swap 实现的示例定义。

```cpp
// https://godbolt.org/z/9PMcz1qP
friend void swap(MxStack& re, MxStack& li) {
    if(&re==&li) return;  // Same address? Swapping with itself is unnecessary
    std::lock(re.mx_, li.mx_);  // multiple locks simultaneously
    std::lock_guard lkre(re.mx_, std::adopt_lock);  // already locked
    std::lock_guard lkli(li.mx_, std::adopt_lock);  // already locked
    std::swap(li.data_, re.data_);  // perform swap
}
```

**清单 29.22** 用于“MxStack”的“swap”。

在 swap 中，你需要锁定两个参数的互斥量，以确保在交换期间没有其他线程将任一参数改为不一致状态。锁定两个互斥量意味着存在死锁风险。解决方案如下：

- 首先，通过函数调用 `lock(...)` 同时锁定两个互斥量。
- 为确保锁被自动释放，再次使用 `lock_guard`，但必须通过附加参数 `adopt_lock` 指明互斥量已经锁定，不需要在 `lock_guard` 构造函数中再次锁定。

像往常一样，`lkre` 和 `lkli` 在离开临界区时会再次释放它们的锁。

以下是对该清单的一般性说明：我按照常见惯用法实现了 `swap`——即作为友元函数——这样它可以像 `swap(a,b)` 一样作为自由函数使用，而不是像 `a.swap(b)` 那样作为方法使用。这是该函数与标准库最好地协作的方式。在 swap 内部，你应当像赋值操作那样首先检查 `swap(a,a)` 是否被直接或间接调用，从而使交换变得不必要，甚至可能危险。

## 避免死锁的提示

完全避免潜在死锁是很困难的。尽管如此，实现这一点至关重要。因此，仔细的考虑和测试很重要——甚至
