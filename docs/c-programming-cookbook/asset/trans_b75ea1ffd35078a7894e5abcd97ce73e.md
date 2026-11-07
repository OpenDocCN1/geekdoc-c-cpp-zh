
## 第7章：并发与多线程

## 引言

探索 C++ 应用中的并行计算是我们需要掌握的技能，以便提升速度、响应能力和可扩展性。本章将并发编程的复杂细节拆解为易于掌握的部分，并提供有用的提示和解决方案，以充分利用 C++ 的线程特性。从 std::thread 基础开始，我们将深入探讨线程的方方面面，学习如何生成、管理和同步线程来同时执行任务，从而使我们的应用程序执行效率大幅提升。

为了在多个线程访问共享资源时保持数据完整并避免竞态情况，并发之旅将继续深入考察同步方法，包括原子操作、锁和互斥量。在并发程序中，线程安全至关重要。本章提供避免多线程编程中常见错误的解决方案和最佳实践。为了进一步简化针对并发操作优化应用程序的过程，我们还将探讨 C++20 中包含的并行算法。这些算法使并行执行模式的构建变得容易。

我们提供了一个用于开发健壮多线程程序的完整工具箱，涵盖管理线程生命周期和状态、理解并使用 future 和 promise 进行异步任务执行，以及实现基于任务的并发。特别强调避免并发编程中普遍存在的死锁，并提供了实现这一目标的策略示例。本章通过示例和讲解，教你如何充分发挥 C++ 并发与多线程特性的潜力。这将使你能够构建高效、可扩展且高性能的应用程序，以应对当今的软件问题。

## 技巧 1：使用 std::thread 进行基本线程操作

### 场景

当我们的应用程序开始同时处理更多用户请求以及日益复杂的后台操作时，利用宿主系统的众多核心变得至关重要。在这种情况下，C++ 中的 std::thread 模块非常有用。std::thread 是一种简单而强大的线程创建和管理方法，于 C++11 引入，允许任务同时完成。软件工程师可以通过学习如何正确使用 std::thread，使我们的应用程序更快、更高效、更具可扩展性。

### 实用解决方案

### 创建和使用线程

使用 std::thread 实现多线程的第一步是创建新线程并为它们分配要执行的任务。每个 std::thread 实例管理一个独立的执行线程。在给定要运行的函数（或可调用对象）后，线程一经创建便立即开始执行。

以下是基本线程操作的示例：

```cpp
#include <iostream>
#include <thread>
#include <string>

// A simple function that will be executed by a thread
void printMessage(const std::string& message) {
    std::cout << "Thread message: " << message << std::endl;
}

int main() {
    // Creating a thread to execute the printMessage function
    std::thread threadObj(printMessage, "Hello from std::thread!");

    // Ensure the main thread waits for the new thread to finish
    if (threadObj.joinable()) {
        threadObj.join(); // Blocks the current thread until threadObj finishes
    }

    return 0;
}
```

在上述示例程序中，printMessage 在与主程序线程不同的独立线程中执行。创建线程后，主线程使用 join() 等待 threadObj 完成执行。joinable() 检查确保程序不会尝试 join 一个已经 join 过或不可 join 的线程，否则会导致运行时错误。

### 管理线程生命周期

正确管理线程生命周期对于避免未定义行为至关重要。join() 函数用于等待线程完成执行，确保程序不会过早退出。或者，可以使用 detach() 让线程独立于主线程执行，但必须注意确保分离线程不会访问可能被主线程清理或变得不可达的任何资源。正确的线程生命周期管理（包括使用 join() 或 detach()）对于确保应用程序保持稳定以及资源得到正确管理至关重要。

## 技巧 2：实现同步机制：互斥量、锁和原子操作

### 场景

随着更多线程并行运行，检查数据一致性和完整性的重要性日益增加。如果对共享资源的并发修改没有得到正确同步，就可能导致竞态条件、未明确定义的行为或数据损坏。C++ 提供了多种同步方法，例如锁、互斥量和原子操作，用于控制谁可以访问哪些共享资源。为了创建线程安全的可靠程序，理解并有效实施这些原则至关重要。

### 实用解决方案

### 互斥量与锁

互斥量（mutual exclusions）用于保护共享数据，一次只允许一个线程访问数据。std::mutex 类提供了简单的加锁和解锁接口，但 C++ 还提供了 RAII 风格的锁管理类，如 std::lock_guard 和 std::unique_lock，以简化互斥量的使用并避免常见陷阱。

以下是使用 std::lock_guard 配合互斥量的示例：

```cpp
#include <iostream>
#include <mutex>
#include <thread>
#include <vector>

std::mutex mu;
int sharedData = 0;

void incrementSharedData() {
    std::lock_guard<std::mutex> lock(mu); // Locks mu upon construction
                                           // and unlocks on destruction
    ++sharedData;
    std::cout << "Data incremented to " << sharedData << std::endl;
}

int main() {
    std::vector<std::thread> threads;

    for (int i = 0; i < 5; ++i) {
        threads.emplace_back(incrementSharedData);
    }

    for (auto& t : threads) {
        t.join();
    }

    return 0;
}
```

### 原子操作

对于简单数据类型，原子操作提供了一种无锁机制来确保线程安全。C++ 为可以原子地读取、写入或修改的类型提供了 std::atomic 模板类。

以下是使用 std::atomic 的示例：

```cpp
#include <atomic>
#include <iostream>
#include <thread>
#include <vector>

std::atomic<int> atomicData(0);

void atomicIncrement() {
    int oldValue = atomicData.fetch_add(1); // Atomically increments atomicData and returns the old value
    std::cout << "Data incremented from " << oldValue << std::endl;
}

int main() {
    std::vector<std::thread> threads;

    for (int i = 0; i < 5; ++i) {
        threads.emplace_back(atomicIncrement);
    }

    for (auto& t : threads) {
        t.join();
    }

    return 0;
}
```

互斥量结合 RAII 风格的锁，提供了一种稳健的方式来保护需要独占访问的复杂数据结构或代码段。对于简单数据类型上的操作，原子操作提供了一种高性能、无锁的替代方案来确保线程安全。

## 技巧 3：实现线程安全

### 场景

随着我们的应用程序添加需要并发执行的功能，线程安全正变得越来越重要。在开发代码时，牢记线程安全非常重要。在处理共享数据以及大量线程同时执行时尤其如此。使我们的应用程序线程安全，将使其在存在大量并发的各种情况下保持高效和可靠，包括出现竞态条件、死锁或数据损坏时。

### 实用解决方案

### 线程安全策略

在像我们的应用程序这样的多线程应用程序中实现线程安全，需要采用特定的编码实践并有效利用 C++ 并发特性。以下是一些基本策略：

- 最小化共享状态：减少多个线程可访问的共享数据量。这可以包括限制共享变量的作用域，或对不需要跨线程共享的数据使用线程局部存储。
- 不可变数据：尽可能使用创建后无法修改的不可变数据结构。不可变对象本质上线程安全，因为其状态无法改变，从而无需同步。
- 同步机制：对于必须由多个线程共享和修改的数据，使用适当的同步机制来管理访问。互斥量、锁和原子操作是 C++ 提供的用于保护共享资源的关键工具。
- 更高层级的构造：利用线程池、future、promise 和基于任务的并行等更高层级的并发构造，它们抽象掉了许多底层线程细节，包括线程安全的某些方面。

以下是使用互斥量实现线程安全的示例程序：

```cpp
#include <iostream>
#include <mutex>
#include <thread>
```

