
```cpp
// show that task woke up and arrived at continuationBarrier
std::cout << std::format(
    "{} done painting. Waiting for next car.\n", name);

// decrement paintingDone barrier's counter and
// wait for other painting robots to arrive here
paintingDone.arrive_and_wait();
}

std::cout << std::format("{} shut down.\n", name);
}
};

moveCarIntoPosition(); // move the first car into position

// start up two painting robots
std::cout << "Starting robots.\n";
std::jthread leftSideRobot{paintingRobotTask, "Left side robot"};
std::jthread rightSideRobot{paintingRobotTask, "Right side robot"};
}
```

```text
Moving next car into painting position.
Car ready for painting.

Starting robots.

Left side robot painting for 4564 ms
Right side robot painting for 2758 ms
Right side robot done painting. Waiting for next car.
Left side robot done painting. Waiting for next car.
Painting robots completed tasks

Moving next car into painting position.
Car ready for painting.

Left side robot painting for 4114 ms
Right side robot painting for 2860 ms
Right side robot done painting. Waiting for next car.
Left side robot done painting. Waiting for next car.
Painting robots completed tasks

Moving next car into painting position.
Car ready for painting.

Right side robot painting for 4730 ms
Left side robot painting for 3794 ms
Left side robot done painting. Waiting for next car.
Right side robot done painting. Waiting for next car.
Painting robots completed tasks

Shutting down assembly line

Right side robot shut down.
Left side robot shut down.
```

**图 17.15** | 使用 `std::barrier` 对象协调线程。（第 3 部分，共 3 部分。）

主线程代表装配线。程序运行如下：

- 第 13–19 行定义了一个 lambda，用于模拟将下一辆汽车移入装配线的喷漆工位。
- 第 21 行定义了 `carsToPaint`——模拟中要处理的汽车数量。
- 我们使用协作式取消（第 17.9 节）在装配线关闭时终止机器人线程。`jthread` 的析构函数会在加入线程之前调用其 `stop_source` 的 `request_stop` 成员函数。随后，`jthread` 的任务可以检查其 `stop_token` 参数，以确定是否终止。然而，在此模拟中，我们不希望在 `main` 结束时 `jthreads` 离开作用域时机器人线程终止，因此我们手动处理取消。`stop_source`（第 24 行）与机器人线程协调取消。处理完三辆汽车后，我们将对此 `stop_source` 调用 `request_stop`，以通知机器人线程装配线正在关闭。
- 第 27 行获取 `stop_source` 的 `stop_token`。在喷漆之前，每个机器人线程将调用其 `stop_token` 的 `stop_requested` 函数，以检查装配线是否正在关闭。
- 第 30–44 行定义了 `paintingDone` 屏障，将其初始化为计数 2（用于两个喷漆机器人），并设置一个完成函数（第 31–43 行），当 `barrier` 的内部计数达到 0 时调用该函数。静态局部变量 count 跟踪目前已经处理的汽车数量。当 count 等于 `carsToPaint` 时，第 38 行对 `stop_source` 调用 `request_stop`，以表明装配线正在关闭。否则，第 41 行模拟将下一辆汽车移动到工位。
- 第 47–74 行定义了 `paintingRobotTask` lambda。第 56–70 行会一直执行，直到第 56 行判定由于装配线正在关闭而应停止任务。第 57–65 行模拟喷漆工作。喷漆完成后，调用方 `jthread` 到达 `paintingDone` 屏障并调用其 `arrive_and_wait` 函数（第 69 行）。这会递减 `barrier` 的内部计数。如果计数不为 0，调用方 `jthread` 会在此阻塞。如果计数为 0，则执行 `barrier` 的完成函数，将下一辆汽车移动到工位，或关闭装配线。完成函数执行完毕后，`barrier` 重置其内部计数，并解除等待中的 `jthreads` 的阻塞，使它们可以继续执行。
- 为开始模拟，第 76 行将第一辆汽车移动到工位，第 80–81 行启动两个 `jthreads`，分别代表左侧和右侧喷漆机器人。

## 17.14 C++20 信号量

另一种互斥机制是信号量，正如 Dijkstra 在其关于协作顺序进程的开创性论文中所描述的那样。¹⁰⁵,¹⁰⁶,¹⁰⁷ 信号量包含一个整数值，表示可以访问共享资源（例如**共享可变数据**）的最大并发线程数。初始化后，该整数只能通过两个操作 $P$ 和 $V$ 访问和修改。它们分别是荷兰语单词 *proberen*（意为“测试”）和 *verhogen*（意为“增加”）的缩写。¹⁰⁸ 线程想要进入**临界区**时调用 $P$ 操作（也称为**等待操作**），想要退出临界区时调用 $V$ 操作（也称为**信号操作**）。一旦临界区中运行的线程数达到最大值，其他试图进入的线程就必须等待。$P$ 和 $V$ 是封装互斥实现细节的抽象。它们可以支持任意数量的协作线程。C++ 的信号量类将这两个操作称为 **acquire** 和 **release**。关于信号量基础的精彩讨论，请查看 Allen B. Downey 的 *信号量小书*。¹⁰⁹

C++20 的 `<semaphore>` 头文件包含用于实现**计数信号量**和**二元信号量**的特性：

- `std::counting_semaphore` 实现了信号量概念，它比 `std::latch` 和 `std::barrier` 层次更低，但仍比互斥量、锁、条件变量和原子操作层次更高。¹¹⁰,¹¹¹ **counting_semaphore** 可以允许多个线程访问共享资源。其构造函数初始化内部整数计数器。当线程**获取信号量**时，内部计数器减一。如果计数器达到零，试图**获取信号量**的线程将阻塞，直到计数增加以表明共享资源可用。当线程释放信号量时，内部计数器加一（默认情况下），等待**获取信号量**的线程解除阻塞。
- `std::binary_semaphore` 只是一个计数为 1 的 **counting_semaphore**，可以像 `std::mutex` 一样使用。¹¹²

### 使用 C++20 `std::binary_semaphore` 的生产者–消费者

C++ 标准指出，信号量“被广泛用于实现其他同步原语，并且在两者都适用时，可以比条件变量更高效。”¹¹³ 图 17.16 使用 `binary_semaphores` 进行互斥，重新实现了第 17.6 节中 `zeidbuf` 里的 Synchron 类。这为你提供了一种简洁、简单且更高层次的方式来替代较低层次的互斥量代码。我们复用了图 17.8 的 main 函数，因此这里不再重复。

108. “信号量（编程）——操作名称。”访问于 2023 年 4 月 18 日。https://en.wikipedia.org/wiki/Semaphore_(programming)#Operation_names

109. Allen B. Downey，*信号量小书*（版本 2.2.1），第“3.6.4 屏障解决方案”节，2016 年。Green Tea Press。https://greenteapress.com/semaphores/littlebookofsemaphores.pdf。许可证：http://creativecommons.org/licenses/by-nc-sa/4.0。感谢我们的审阅者之一 Anthony Williams 向我们指出 Downey 的工作。

110. C++ 标准，“线程支持库——信号量。”访问于 2023 年 4 月 18 日。https://tim-song-cpp.github.io/cppwp/n4861/thread.sema。

111. `std::counting_semaphore`、`std::binary_semaphore.` 访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/thread/counting_semaphore。

112. `std::counting_semaphore`、`std::binary_semaphore.` 访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/thread/counting_semaphore。

113. C++ 标准，“32.7 信号量。”访问于 2023 年 4 月 18 日。https://timsong-cpp.github.io/cppwp/n4861/thread.sema。

