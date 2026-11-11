

## atomic_ref 的所有操作

| 成员函数 | 描述 |
|---|---|
| `is_lock_free`<br>`atomic_ref<T>::is_always_lock_free` | 检查 atomic_ref 对象是否为无锁的。<br>在编译时检查原子类型是否始终无锁。 |
| `load`<br>`operator T` | 原子地返回被引用对象的值。<br>原子地返回被引用对象的值。等价于 `atomic::load()`。 |
| `store` | 用一个非原子值原子地替换被引用对象的值。 |
| `exchange` | 用新值原子地替换被引用对象的值。 |
| `compare_exchange_strong`<br>`compare_exchange_weak` | 原子地比较并最终交换被引用对象的值。详情见这里。 |
| `fetch_add`, `+=`<br>`fetch_sub`, `-=` | 原子地对被引用对象进行加（减）值操作。 |
| `fetch_or`, \|=<br>`fetch_and`, `&=`<br>`fetch_xor`, `^=` | 原子地对被引用对象执行按位或、与和异或操作。 |
| `++`, `--` | 递增或递减（前置和后置）被引用对象。 |
| `notify_one`<br>`notify_all` | 通知一个原子等待操作。<br>通知所有原子等待操作。 |
| `wait` | 阻塞直到被通知。<br>将自身与旧值进行比较，以防止虚假唤醒和丢失唤醒。<br>如果旧值比较不相等，则返回。 |

复合赋值运算符返回新值；fetch 变体返回旧值。

每个成员函数都支持一个额外的内存序参数。内存序参数的默认值是 `std::memory_order_seq_cst`，但你也可以使用 `std::memory_order_relaxed`、`std::memory_order_consume`、`std::memory_order_acquire`、`std::memory_order_release` 或 `std::memory_order_acq_rel`。`compare_exchange_strong` 和 `compare_exchange_weak` 成员函数可以用两个内存序参数化：一个用于成功情况，一个用于失败情况。如果你只显式提供一个内存序，它会被同时用于成功和失败情况。以下是内存序的详细说明。

当然，并非所有操作都可用于 `std::atomic_ref` 引用的所有类型。下表列出了取决于 `std::atomic_ref` 引用类型的所有原子操作。

**所有原子操作，取决于 `std::atomic_ref` 引用的类型**

| 函数 | `atomic_ref<T>` | `atomic_ref<floating>` | `atomic_ref<T*>` | `atomic_ref<integral>` |
|---|---|---|---|---|
| is_lock_free | 是 | 是 | 是 | 是 |
| `atomic_ref<T>::is_always_lock_free` | 是 | 是 | 是 | 是 |
| load | 是 | 是 | 是 | 是 |
| `operator T` | 是 | 是 | 是 | 是 |
| store | 是 | 是 | 是 | 是 |
| exchange | 是 | 是 | 是 | 是 |
| compare_exchange_strong | 是 | 是 | 是 | 是 |
| compare_exchange_weak | 是 | 是 | 是 | 是 |
| fetch_add, += |  | 是 | 是 | 是 |
| fetch_sub, -= |  | 是 | 是 | 是 |
| fetch_or, \|= |  |  |  | 是 |
| fetch_and, &= |  |  |  | 是 |
| fetch_xor, ^= |  |  |  | 是 |
| ++, -- |  |  | 是 | 是 |
| notify_one | 是 | 是 | 是 | 是 |
| notify_all | 是 | 是 | 是 | 是 |
| wait | 是 | 是 | 是 | 是 |

原子量及其原子操作是内存模型的基本构建块。它们建立了对原子量和非原子量都成立的同步和排序约束。让我们更深入地研究同步和排序约束。

## 原子操作的特征

| 操作 | 读 | 写 | 读-修改-写 |
|---|---|---|---|
| test_and_set |  |  | 是 |
| clear |  | 是 |  |
| is_lock_free | 是 |  |  |
| load | 是 |  |  |
| operator T | 是 |  |  |
| store |  | 是 |  |
| exchange |  |  | 是 |
| compare_exchange_strong |  |  | 是 |
| compare_exchange_weak |  |  | 是 |
| fetch_add, += |  |  | 是 |
| fetch_sub, -= |  |  | 是 |
| fetch_or, \|= |  |  | 是 |
| fetch_and, &= |  |  | 是 |
| fetch_xor, ^= |  |  | 是 |
| ++, -- |  |  | 是 |
| notify_one | 是 |  |  |
| notify_all | 是 |  |  |
| wait |  | 是 |  |

读-修改-写操作有一个额外保证：它们总是提供最新的值。这意味着在不同线程上的一系列 `atomicVar.fetch_sub(1)` 操作会一个接一个地递减，不会出现间隙或重复。

如果你将原子操作 `atomicVar.load()` 与为写入或读-修改-写操作设计的内存模型一起使用，写入部分没有效果。结果是操作 `atomicVar.load(std::memory_order_acq_rel)` 等价于操作 `atomicVar.load(std::memory_order_acquire)`。相应地，操作 `atomicVar.load(std::memory_order_release)` 等价于 `atomicVar.load(std::memory_order_relaxed)`。

### 2.4.1.2 不同的同步和排序约束

粗略地说，C++ 中有三种不同类型的同步和排序约束：

- 顺序一致性：`memory_order_seq_cst`
- 获取-释放：`memory_order_consume`, `memory_order_acquire`, `memory_order_release` 和 `memory_order_acq_rel`
- 宽松：`memory_order_relaxed`

顺序一致性在线程之间建立全局顺序，而获取-释放语义在同一原子变量的不同线程的读写操作之间建立排序。宽松语义只保证某个原子 `m` 的修改顺序。修改顺序意味着对特定原子 `m` 的所有修改以某个特定的全序发生。因此，一个特定线程对原子对象的读取永远不会看到比该线程已经观察到的“更旧”的值。

不同的内存模型及其对原子和非原子操作的影响使 C++ 内存模型成为一个令人兴奋且具有挑战性的话题。让我们讨论顺序一致性、获取-释放语义和宽松语义的同步和排序约束。

### 2.4.2 顺序一致性

让我们更深入地研究顺序一致性。顺序一致性的关键在于所有线程上的所有操作都遵循一个通用时钟。这个全局时钟使得思考它变得非常直观。

顺序一致性的直观性是有代价的。缺点是该系统必须同步线程。

以下程序借助顺序一致性来同步生产者和消费者线程。

**使用顺序一致性的生产者-消费者同步**

```cpp
// producerConsumer.cpp

#include <atomic>
#include <iostream>
#include <string>
#include <thread>

std::string work;
std::atomic<bool> ready(false);

void consumer() {
  while (!ready.load()) {}
  std::cout << work << '\n';
}

void producer() {
  work = "done";
  ready = true;
}

int main() {
  std::thread prod(producer);
  std::thread con(consumer);
  prod.join();
  con.join();
}
```

程序的输出并不令人兴奋。

![](img/d61a6c83410484053b8892275d2fcc4f_87_0.png)

使用顺序一致性的生产者-消费者同步

由于顺序一致性，程序执行是确定性的。它的输出总是“done”。

该图描绘了操作的顺序。消费者线程在 while 循环中等待，直到原子变量 ready 被设置为 true。当这种情况发生时，消费者线程继续执行它们的工作。

原子操作的获取-释放语义。获取-释放语义是 C# 和 Java 不遵循的领域。这也是我们的直觉开始减弱的领域。

### 2.4.3 获取-释放语义

在获取-释放语义中，线程之间没有全局同步；只有对**同一原子变量**的原子操作之间的同步。一个线程上的写操作与另一个线程上对同一原子变量的读操作同步。

获取-释放语义基于一个基本思想：释放操作与同一原子上的获取操作同步，并建立一个排序约束。该排序约束意味着所有读和写操作都不能被移动到释放操作之后。所有读和写操作都不能被移动到获取操作之前。

什么是获取或释放操作？使用 load 或 test_and_set 读取原子变量是获取操作。还有更多：释放锁或互斥量同步于获取锁或互斥量。线程的构造同步于可调用对象的调用。线程的完成同步于 join 调用。任务的可调用对象的完成同步于 future 中的 wait 或 get 调用。获取和释放操作成对出现。

记住这幅图会很有帮助。

![](img/d61a6c83410484053b8892275d2fcc4f_89_0.png)

### 内存模型：更深入地理解多线程

这是你应该牢记内存模型的主要原因。获取-释放语义帮助你更好地理解高级同步原语，如互斥量。同样的推理也适用于线程的启动和对线程的 join 调用。两者都是获取-释放操作。条件变量上的 wait 和 notify_one 调用也是如此；wait 是获取操作，notify_one 是释放操作。那 notify_all 呢？它也是一个释放操作。

