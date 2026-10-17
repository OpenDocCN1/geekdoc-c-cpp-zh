
```cpp
std::lock_guard<std::mutex> lk(pm);

// 在共享数据上执行操作。
}
```

# 11.2.4 风险评估

如果在锁定互斥锁状态下发生异常，可能会发生死锁。

| 规则 | 严重性 | 概率 | 修复成本 | 优先级 | 等级 |
| --- | --- | --- | --- | --- | --- |
| CON51-CPP | 低 | 可能 | 低 | P6 | L2 |

并发 (CON) - CON51-CPP. 确保在异常情况下释放活动持有的锁

# 11.2.5 相关准则

此规则是 ERR56-CPP 的子集。保证异常安全。

| MITRE CWE | CWE-667, 不恰的锁定 |
| --- | --- |
| SEI CERT Java 语言编码标准 | LCK08-J. 确保在异常情况下释放活动持有的锁 |

# 11.2.6 参考文献

| [ISO/IEC 14882-2014] | 子章节 30.4.2, “锁” |
| SEI CERT C++ 编码标准 (2016 年版) | V01 |
| 软件工程研究所 | 卡内基梅梅隆大学 |

[分发声明 A] 批准公开发布和不受限制的分发。

# 11.3 CON52-CPP. 防止从多个线程访问位域时发生数据竞态

在访问位域（bit-field）时，线程可能会无意中访问相邻内存中的另一个位域。由于编译器要求在存在多个相邻位域时将它们存储在一个存储单元中，因此数据竞态不仅可能发生在多个线程访问的位域上，也可能发生在共享相同字节或字的其它位域上。这个问题很难诊断，因为并不容易看出同一个内存位置正在被多个线程修改。

在并发编程中，防止数据竞态的一种方法是使用互斥锁。当所有线程正确遵守时，互斥锁可以为共享对象提供安全的访问。然而，对于在互斥锁未被线程控制时可能被访问的对象，互斥锁不提供任何保证。遗憾的是，没有通用方法可以确定哪些相邻位域与目标位域存储在一起。

另一种方法是在任意两个位域之间插入非位域字段，以确保每个位域都是其存储单元内唯一被访问的字段。这种技术有效地保证了不会有两个位域同时被访问。

## 11.3.1 不合规代码示例（位域）

相邻的位域可能存储在同一个内存位置。因此，在不同的线程中修改相邻位域是未定义行为，如此不合规代码所示。

```cpp
struct MultiThreadedFlags {
  unsigned int flag1 : 2;
  unsigned int flag2 : 2;
};
MultiThreadedFlags flags;
void thread1() {
  flags.flag1 = 1;
}
void thread2() {
  flags.flag2 = 2;
}
```

并发 (CON) - CONS52-CPP. 防止从多个线程访问位域时发生数据竞态

例如，可能会出现指令序列：

```
线程 1: 寄存器 0 = flags
线程 1: 寄存器 0 &= -mask(flag1)
线程 2: 寄存器 0 = flags
线程 2: 寄存器 0 &= -mask(flag2)
线程 1: 寄存器 0 |= 1 << shift(flag1)
线程 1: flags = 寄存器 0
线程 2: 寄存器 0 |= 2 << shift(flag2)
线程 2: flags = 寄存器 0
```

## 11.3.2 合规解决方案（位域，C++11 及后续版本，互斥锁）

此简单解决方案使用互斥锁保护对 `flags` 的访问，防止任何数据竞态。

```cpp
#include <mutex>
struct MultiThreadedFlags {
    unsigned int flag1 : 2;
    unsigned int flag2 : 2;
};
struct MtfMutex {
    MultiThreadedFlags s;
    std::mutex mutex;
};
MtfMutex flags;
void thread1() {
    std::lock_guard<std::mutex> lk(flags.mutex);
    flags.s.flag1 = 1;
}
void thread2() {
    std::lock_guard<std::mutex> lk(flags.mutex);
    flags.s.flag2 = 2;
}
```

## 11.3.3 合规解决方案（C++11）

在此合规解决方案中，两个线程同时访问 `flags`。

```cpp
struct ThreadedFlags {
    unsigned char flag1;
    unsigned char flag2;
};
ThreadedFlags flags;
std::mutex mtx;
void thread1() {
    std::lock_guard<std::mutex> lk(mtx);
    flags.flag1 = 1;
}
void thread2() {
    std::lock_guard<std::mutex> lk(mtx);
    flags.flag2 = 2;
}
```

并发 (CON) - CON53-CPP. 通过预定义的顺序加锁避免死锁

```cpp
balance(initialAmount) {
    int get_balance() const { return balance; }
    void set_balance(int amount) { balance = amount; }
}
int deposit(BankAccount *from, BankAccount *to, int amount) {
    std::lock_guard<std::mutex> from_lock(from->balanceMutex);
    // 余额不足，无法转账。
    if (from->get_balance() < amount) {
        return -1; // 表示错误
    }
    std::lock_guard<std::mutex> to_lock(to->balanceMutex);
    from->set_balance(from->get_balance() - amount);
    to->set_balance(to->get_balance() + amount);
    return 0;
}
void f(BankAccount *ba1, BankAccount *ba2) {
    // 执行存款。
    std::thread thr1(deposit, ba1, ba2, 100);
    std::thread thr2(deposit, ba2, ba1, 100);
    thr1.join();
    thr2.join();
}
```

## 11.4.2 合规解决方案（手动排序）

该合规解决方案通过在 `deposit (int)` 函数中建立预定义的加锁顺序，消除了循环等待条件。每个线程将根据 `BankAccount` 的 ID 进行加锁，该 ID 在 `BankAccount` 对象初始化时设置。

```cpp
#include <atomic>
#include <mutex>
#include <thread>
class BankAccount {
    static std::atomic<unsigned int> globalId;
    const unsigned int id;
    int balance;
public:
    std::mutex balanceMutex;
    BankAccount() = delete;
    explicit BankAccount(int initialAmount) :
    id(globalId++), balance(initialAmount) {
    unsigned int get_id() const { return id; }
    int get_balance() const { return balance; }
    void set_balance(int amount) { balance = amount; }
}
std::atomic<unsigned int> BankAccount::globalId(1);
int deposit(BankAccount *from, BankAccount *to, int amount) {
    std::mutex *first;
    std::mutex *second;
    if (from->get_id() == to->get_id()) {
        return -1; // 表示错误
    }
    // 确保加锁顺序正确。
    if (from->get_id() < to->get_id()) {
        first = &from->balanceMutex;
        second = &to->balanceMutex;
    } else {
        first = &to->balanceMutex;
        second = &from->balanceMutex;
    }
    std::lock_guard<std::mutex> firstLock(*first);
    std::lock_guard<std::mutex> secondLock(*second);
    // 检查余额是否足够转账。
    if (from->get_balance() >= amount) {
        from->set_balance(from->get_balance() - amount);
        to->set_balance(to->get_balance() + amount);
        return 0;
    }
    return -1;
}
void f(BankAccount *ba1, BankAccount *ba2) {
    // 执行存款。
    std::thread thread1(deposit, ba1, ba2, 100);
    std::thread thread2(deposit, ba2, ba1, 100);
    thread1.join();
    thread2.join();
}
```

## 11.4.3 合规解决方案 (std::lock())

该合规解决方案使用标准模板库的设施来确保不会因循环等待条件导致死锁。`std::lock()` 函数接受可数量的可锁对象，并尝试锁定它们 [ISO/IEC 14882-2014]，以防止死锁发生。在实际实现中，通过 `lock()`、`try_lock()` 和 `unlock()` 的组合来尝试锁定，如果未获取锁则回退，其性能可能比预定义顺序的解决方案差。

```cpp
#include <mutex>
#include <thread>
class BankAccount {
    int balance;
public:
    std::mutex balanceMutex;
    BankAccount() = delete;
    explicit BankAccount(int initialAmount) :
        balance(initialAmount) {}
    int get_balance() const { return balance; }
    void set_balance(int amount) { balance = amount; }
};
void deposit(BankAccount *from, BankAccount *to, int amount) {
    // 锁定对象但推后执行。
    std::unique_lock<std::mutex> l1(from->balanceMutex, std::defer_lock);
    std::unique_lock<std::mutex> l2(to->balanceMutex, std::defer_lock);
    // 同时锁定两个对象。
    std::lock(l1, l2);
    if (from->get_balance() >= amount) {
        from->set_balance(from->get_balance() - amount);
        return 0;
    }
    return -1;
}
void f(BankAccount *ba1, BankAccount *ba2) {
    // 执行存款。
    std::thread thr1(deposit, ba1, ba2, 100);
    std::thread thr2(deposit, ba2, ba1, 100);
    thr1.join();
    thr2.join();
}
```

并发 (CON) - CON53-CPP. 通过预定义的顺序加锁避免死锁

## 11.4.4 风险评估

死锁会导致多线程无法进展停止执行。如果攻击者可以创建死锁条件，则可能拒绝服务攻击。

| 规则 | 严重性 | 可能性 | 修复成本 | 优先级 | 级别 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| CON53-CPP | 低 | 可能 | 中 | P4 | L3 |

## 11.4.5 相关指南

- Java 安全编码标准: LCK07-J. 以相同的顺序请求和释放锁避免死锁
- SEI CERT 编码标准: CON35-C. 通过预定义的顺序加锁避免死锁
- MITRE CWE: CWE-764，关键资源的多次锁定

## 11.4.6 参考文献

- [ISO/IEC 14882-2014]: 节 30.4，“互斥”，节 30.4.3，“通用锁定”

# 11.5 CON54-CPP. 封装可以在循环中虚假唤醒的函数

`std::condition_variable` 类的 `wait()`、`wait_for()` 和 `wait_until()` 成员函数临时放弃互斥锁的所有权，以便其他线程通过加锁被唤醒。这些函数必须从暂停执行的代码中调用。只有在另一个线程调用 `notify_one()` 或 `notify_all()` 成员函数后，等待线程才会恢复执行。

`wait()` 函数必须从检查条件谓词的循环中调用。条件谓词是一个由变量组成的表达式，该表达式必须线程执行必须为真。线程通过 `wait()`、`wait_for()`、`wait_until()` 或其他机制暂停执行，并在条件谓词为真且收到通知时恢复。

```cpp
#include <condition_variable>
#include <mutex>
extern bool until_finish(void);
extern std::mutex m;
extern std::condition_variable condition;
void func(void) {
    std::unique_lock<std::mutex> lk(m);
    while (until_finish()) { // 谓词不成立。
        condition.wait(lk);
    }
    // 条件成立时恢复。
}
```

通知机制会通知等待线程并允许其检查条件谓词。在另一个线程中调用 `notify_all()` 无法精确确定哪个等待线程将恢复。条件谓词语句允许被通知线程在收到通知后判断是否应该恢复。

## 11.5.1 不合规代码示例

此不合规代码示例监控链表并在为空时未能消费列表元素。

该线程使用 `wait()` 暂停执行并在收到通知时恢复，假设有元素可以消费。即使列表为空，线程也可能被通知，可能是因为通知线程使用了 `notify_all()`，它会通知所有线程。通常认为使用 `notify_all()` 通知优于使用 `notify_one()`。（更多信息请参见 CON55-CPP. 使用条件变量时保持线程安全和活跃。）

条件谓词通常是循环中条件表达式的否定。在此不合规代码示例中，从链表中移除元素的条件谓词是 `(list->next != nullptr)`，而 `while` 循环的条件表达式是 `(list->next == nullptr)`。

此不合规代码在 `if` 块内部调用 `wait()`，导致在收到通知后未能检查条件谓词。如果通知是虚假的或恶意的，线程将提前唤醒。

```cpp
#include <condition_variable>
#include <mutex>
struct Node {
    void *node;
    struct Node *next;
};
static Node list;
static std::mutex m;
static std::condition_variable condition;
void consume_list_element(std::condition_variable &condition) {
    std::unique_lock<std::mutex> lk(m);
    if (list.next == nullptr) {
        condition.wait(lk);
    }
    // 条件成立时继续。
}
```
