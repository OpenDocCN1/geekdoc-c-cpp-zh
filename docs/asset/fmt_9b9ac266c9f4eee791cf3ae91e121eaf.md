
```cpp
1: int value;
2: mutex valueMutex;
3: mutex coutMutex;
4:
5: void fun1()
6: {
7:   scoped_lock sl1(coutMutex, valueMutex);
8:   cout << "fun 1 locks cout\n";
9:   sleep(1);
10:  cout << "fun 1 locks value\n";
11: }
12:
13: void fun2()
14: {
15:   scoped_lock sl1(valueMutex, coutMutex);
16:   cout << "fun 2 locks value\n";
17:   sleep(1);
18:  cout << "fun 2 locks cout\n";
19: }
20:
21: int main()
22: {
23:   thread t1(fun1);
24:   fun2();
25:   t1.join();
26: }
27: // Displays:
28: // fun 2 locks value
29: // fun 2 locks cout
30: // fun 1 locks cout
31: // fun 1 locks value
```

### 20.3.3 共享锁

共享锁通过 `std::shared_lock` 类型可用，包括 `<shared_mutex>` 头文件。

`std::shared_lock` 类型的对象在作用域内控制对可锁对象的共享所有权。可锁对象的共享所有权可以在构造时或之后获取，一旦获取，它就可以转移给另一个 `shared_lock`。`shared_lock` 类型的对象不能拷贝，但支持移动构造和赋值。

如果指向互斥量的指针 `pm` 有非零值，且 `pm` 指向的可锁对象在 `shared_lock` 的剩余生命周期内不存在，则程序的行为是未定义的。提供的互斥量必须是 `shared_mutex` 或具有相同特征的类型。`shared_lock` 类型提供了以下构造函数、析构函数和运算符：

- `shared_lock()`: 默认构造函数，创建一个不拥有锁的对象。
- `shared_lock(mutex_type& m)`: 构造函数，获取 `m` 的共享锁。
- `shared_lock(mutex_type& m, std::defer_lock dl)`: 构造函数，延迟获取对 `m` 的所有权。
- `shared_lock(mutex_type& m, std::try_lock tl)`: 构造函数，尝试获取 `m` 的共享锁。
- `shared_lock(mutex_type& m, std::adopt_lock al)`: 构造函数，如果当前线程已经锁定了 `m`，则接管该锁的所有权。
- `shared_lock(mutex_type& m, std::try_to_lock tl)`: 构造函数，如果 `m` 尚未被锁定，则尝试接管该锁的所有权。
- `shared_lock(mutex_type& m, std::shared_lock sl)`: 构造函数，如果当前线程已经锁定了 `m`，则接管该锁的所有权。
- `shared_lock(const shared_lock& other)`: 拷贝构造函数，从 `other` 拷贝锁所有权。
- `shared_lock(shared_lock&& other)`: 移动构造函数，从 `other` 移动锁所有权。
- `shared_lock& operator=(const shared_lock& other)`: 拷贝赋值运算符。
- `shared_lock& operator=(shared_lock&& other)`: 移动赋值运算符。
- `~shared_lock()`: 析构函数，如果拥有锁，则释放锁。
- `explicit operator bool() const`: 返回 `shared_lock` 对象是否拥有锁。
- `void lock()`: 获取共享锁。
- `mutex_type* mutex() const`: 返回指向互斥量的指针。
- `mutex_type* release()`: 释放所有权并返回互斥量指针，当前对象不再拥有锁。
- `void swap(shared_lock& other) noexcept`: 交换当前对象和 `other` 的锁所有权。
- `void swap(shared_lock& first, shared_lock& second) noexcept`: 自由函数，交换两个 `shared_lock` 对象的锁权。
- `bool try_lock()`: 尝试获取共享锁。
- `bool try_lock_for(const chrono::durationRep& rel_time)`: 在指定的时间范围内尝试获取共享锁。
- `bool try_lock_until(const chrono::time_point<Clock, Duration>)`: 在指定的时间点尝试获取共享锁。
- `void unlock()`: 释放共享锁。

### 20.3.4 作用域锁

可以使用上一节中描述的原则来避免死锁。然而，与其将避免死锁的责任放在软件工程师的肩上，一个

## 20.3. 锁与锁的处理

还有另一种替代方法：可以使用 `scoped_lock` 同时锁定多个信号量，其中 `scoped_lock` 确保避免了死锁。

`scoped_lock` 还有一个默认构造函数，它不执行任何操作，因此需要工程师来定义至少包含一个互斥锁的 `scoped_lock` 对象。在使用用 `scoped_lock` 对象之前，必须包含 `<mutex>` 头文件。改编第 20.3.2 节的示例：两个函数都定义了一个 `scoped_lock`（注意互斥锁指定的顺序并不重要），并且没有发生死锁。

```cpp
1:
2: int value;
3: mutex valueMutex;
4: mutex countMutex;
5:
6: void fun1()
7: {
8:   unique_lock<mutex> lg1(countMutex, defer_lock);
9:   unique_lock<mutex> lg2(valueMutex, defer_lock);
10:
11:   lock(lg2, lg1);
12:
13:   cout << "fun 1 locks\n";
14:   cout << "fun 1 locks value\n";
15: }
16:
17: void fun2()
18: {
19:   unique_lock<mutex> lg1(countMutex, defer_lock);
20:   unique_lock<mutex> lg2(valueMutex, defer_lock);
21:
22:   lock(lg2, lg1);
23:
24:   cout << "fun 2 locks\n";
25:   cout << "fun 2 locks value\n";
26: }
27:
28: int main()
29: {
30:   thread t1(fun1);
31:   thread t2(fun2);
32:
33:   t1.join();
34:   t2.join();
35: }
```

因此，与其使用 `lock_guard` 对象，不如使用 `scoped_lock` 对象。在只使用一个互斥锁时，偏好使用 `lock_guard` 还是 `scoped_lock` 取决于个人喜好。也许应该偏好 `scoped_lock`，因为它始终有效……

## 20.4 事件处理（条件变量）

本节介绍了条件变量。条件变量允许程序使用数据状态来同步线程，而不是简单地对数据访问进行锁定（后者是通过使用互斥锁实现的）。

在使用条件变量之前，必须包含 `<condition_variable>` 头文件。

为了开始讨论，考虑一个经典的生产者-消费者场景：生产者产生项目，消费者消耗这些项目。生产者在存储容量被填满之前只能产生一定数量的项目，而客户端消耗的项目数量不能超过生产者产生的项目数量。

在某个时刻，生产者的存储容量已完全充满，生产者必须等待客户端消耗某些项目，以便在生产者的存储器中腾出空间。同样，在生产者产生某些项目之前，消费者无法开始消费。

不使用互斥锁（数据锁定）来实现这种场景 并不是一个理想的选项，或者使用互斥锁通过轮询来实现该场景：进程必须不断地释放互斥锁锁，或者判断它们是否可以执行某些操作，然后释放锁。通常没有操作需要执行，进程正忙于获取和释放互斥锁。轮询强制线程等待直到它们可以锁定互斥锁，尽管可能已经可以继续。可以缩短轮询间隔，但这不是一个理想的选项，因为这增加了处理互斥锁相关的开销（也称为“忙等”）。

可以使用条件变量来防止轮询。线程可以使用条件变量通知等待的线程有它们有事情要做。这样一来，线程就可以在数据上进行同步。

数据可能被多个线程修改，线程仍然需要使用互斥锁，但仅用于控制对数据的访问。此外，条件变量允许线程在获取某个特定值、通过预设时间后、或者到达预设时间点之前释放互斥锁的所有权。

使用条件变量的线程的典型设置如下：

- 消费者线程（线程）的行为类似：

```
锁定互斥锁
当所需条件未满足（即为假）时：
    等待直到被通知
    （这会自动释放互斥锁锁）。
  一旦重新获得互斥锁且满足了所需条件：
    处理数据
释放互斥锁锁。
```

- 生产者线程（线程）的行为类似：

```
锁定互斥锁
当所需条件未满足时：
    执行某些操作以满足所需条件
通知等待的线程（所需条件已满足）
释放互斥锁锁。
```

无论哪个线程启动，持有互斥锁锁的线程在某个时刻都会释放锁，允许另一个进程（重新）获取它。如果由消费者启动，它在进入等待状态后立即释放锁；如果由生产者启动，它会在条件为真时释放锁。

这种协议隐藏了一个微妙的初始同步需求。如果消费者（即消费者）尚未进入其等待状态，它将错过生产者的通知。因此，需要 `在通知（生产者）线程之前开始等待`。由于线程已经启动，无法对任何条件变量成员的顺序做出任何假设。

线程已经启动，无法对任何条件变量成员的顺序做出任何假设。

函数参数的类型不需要显式指定。例如，为了等待 5 秒，可以这样调用 `wait_for`：

```
cond::wait_for(&unique_lock, std::chrono::seconds(5));
```

该成员函数在被通知或指定的 `relTime` 指定的时间间隔通过后时返回。

如果是由于超时而返回，则返回 `std::cv_status::timeout`，否则返回 `std::cv_status::no_timeout`。

线程在 `wait_for` 返回后会验证所需的条件是否已经满足。

- `bool wait_for(unique_lock<mutex>& unique_lock, chrono::duration<Rep, Predicate> const &relTime, Predicate pred);`

这被定义为成员模板，使用了头部模板 `<typename Rep, typename Pred, typename Predicate>`。模板的类型根据函数参数的类型自动推导，不需要显式指定。

只要 `pred` 返回 `false`，就会调用 `wait_for` 成员函数。如果上一个成员函数返回 `cv_status::timeout`，则返回 `pred`，否则返回 `true`。

- `cv_status wait_until(unique_lock<mutex>& unique_lock, chrono::time_point<Clock, Duration> const &absTime);`

这被定义为成员模板，使用了头部模板 `<typename Clock, typename Duration>`。模板的类型根据函数参数的类型自动推导，不需要显式指定。例如，为了等待到当前时间 5 分钟后，可以这样调用 `wait_until`：

```
cond::wait_until(&unique_lock, chrono::system_clock::now() + std::chrono::minutes(5));
```

该函数的作用与之前描述的 `wait_for(unique_lock<mutex>&unique_lock, chrono::duration<Rep, Predicate> const &relTime)` 相同，后者使用的是绝对时间点，而不是指定的相对时间。

该成员函数在被通知或指定的 `relTime` 指定的时间间隔通过后返回。

如果是由于超时而返回，则返回 `std::cv_status::timeout`，否则返回 `std::cv_status::no_timeout`。

- `wait_until(unique_lock<mutex>& &unique_lock, chrono::time_point<Clock, Duration> const &absTime, Predicate pred);`

这被定义为成员模板，使用了头部模板 `<typename Clock, typename Duration, typename Predicate>`。模板的类型根据函数参数的类型自动推导，不需要显式指定。

只要 `pred` 返回 `false`，就会调用上一个 `wait_until` 成员函数。如果上一个成员函数返回 `cv_status::timeout`，则返回 `pred`，否则返回 `true`。

当条件变量的等待成员返回时，线程会验证所需的条件是否为真。

### 20.4.2 std::condition_variable_any 类

与 `condition_variable` 类不同，`std::condition_variable_any` 类可以与任何（例如用户提供的）锁类型配合使用，而不仅仅是 STL 提供的 `unique_lock<mutex>`。

在使用 `condition_variable_any` 类之前，可以包含 `<condition_variable>` 头文件。

`condition_variable_any` 提供的功能与 `condition_variable` 类提供的功能相同，尽管 `condition_variable_any` 使用的锁类型不是预定义的。因此，`condition_variable_any` 要求指定其对象必须使用的锁类型。

在所示所示接口中，该锁类型被称为 `Lock`。大多数 `condition_variable_any` 成员被定义为成员模板，将 `Lock` 类型定义为其参数之一。这些锁类型的要求与 STL 提供的 `unique_lock` 相同，用户定义的锁类型实现至少应提供 `unique_lock` 提供的接口和语义。

本节介绍了 `condition_variable_any` 类的接口。由于其接口提供了与 `condition_variable` 相同的成员函数（允许向相应成员传递任何锁类型而非 `unique_lock`），读者请参阅上一节以获取关于类成员语义的描述。

像 `condition_variable` 一样，`condition_variable_any` 类只提供默认构造函数。不允许拷贝构造函数或重载赋值运算符。

同样，像 `condition_variable` 一样，该类的析构函数要求当前线程没有阻塞线程。这意味着所有（等待中的）线程都已收到通知；然而这些线程随后可能会阻塞在它们等待调用中指定的锁上。

注意，除了 `Lock` 之外，类型 `Lock`、`Duration`、`Period`、`Predicate` 和 `Rep` 都是模板类型，定义方式类似于上一节中的同名类型。

假设 `MyMutex` 是用户定义的互斥量，`MyLock` 是用户定义的锁类型（详见 20.3 关于锁类型的说明），则可以这样定义 `condition_variable_any` 对象：

```
MyMutex mut;
MyLock<MyMutex> ul(mut);
condition_variable_any cva;

cva.wait(ul);
```

这些是 `condition_variable_any` 类的成员：

- `notify_one() noexcept;`
- `notify_all() noexcept;`
- `wait(Lock& lock);`
- `wait(Lock& lock, Predicate pred);`
- `cv_status waituntil(Lock& lock, const chrono::time_point<Clock, Duration>& absTime);`
- `bool wait_until(Lock& lock, const chrono::time_point<Clock, Duration>& absTime, Predicate pred);`
- `cv_status wait_until(unique_lock<mutex>& unique_lock, chrono::duration<Rep, Predicate> const &relTime);`
- `bool wait_for(unique_lock<mutex>& unique_lock, chrono::duration<Rep, Predicate> const &relTime);`

### 20.4.1 使用 wait_until

为了等待到当前时间 5 分钟后，可以这样调用 `wait_until`：
