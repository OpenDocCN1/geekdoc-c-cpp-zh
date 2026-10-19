

## 32.9 Futures [futures]

### 32.9.1 Overview [futures.overview]

32.9 描述了 C++ 程序可用于在一个线程中检索在同一线程或另一个线程中运行的函数的结果（值或异常）的组件。

> [注 1：这些组件并不局限于多线程程序，在单线程程序中也很有用。——注结束]

### 32.9.2 头文件 <future> 概要 [future.syn]

```cpp
namespace std {
    enum class future_errc {
        broken_promise = implementation-defined,
        future_already_retrieved = implementation-defined,
        promise_already_satisfied = implementation-defined,
        no_state = implementation-defined
    };

    enum class launch : unspecified {
        async = unspecified,
        deferred = unspecified,
        implementation-defined
    };

    enum class future_status {
        ready,
        timeout,
        deferred
    };
}
```

```cpp
void wait(arrival_token&& arrival) const;
```

前置条件：arrival 与当前阶段或同一 barrier 对象的紧前阶段的阶段同步点相关联。

效果：阻塞在与 std::move(arrival) 关联的同步点，直到该同步点所在阶段的阶段完成步骤运行。

> [注 3：如果 arrival 与前一阶段的同步点相关联，则调用立即返回。——注结束]

抛出：当需要异常时抛出 system_error（32.2.2）。

错误条件：mutex 类型允许的任何错误条件（32.5.4.2）。

```cpp
void arrive_and_wait();
```

效果：等价于：wait(arrive())。

```cpp
void arrive_and_drop();
```

前置条件：当前 barrier 阶段的预期计数大于零。

效果：将后续所有阶段的初始预期计数递减一。然后将当前阶段的预期计数递减一。

同步：对 arrive_and_drop 的调用强先于当前阶段的阶段完成步骤的开始。

抛出：当需要异常时抛出 system_error（32.2.2）。

错误条件：mutex 类型允许的任何错误条件（32.5.4.2）。

> [注 4：此调用可能导致当前阶段的完成步骤开始。——注结束]

抛出：当需要异常时抛出 system_error（32.2.2）。

错误条件：mutex 类型允许的任何错误条件（32.5.4.2）。

> [注 2：此调用可能导致当前阶段的完成步骤开始。——注结束]

```cpp
template<> struct is_error_code_enum<future_errc> : public true_type { };
error_code make_error_code(future_errc e) noexcept;
error_condition make_error_condition(future_errc e) noexcept;

const error_category& future_category() noexcept;

class future_error;

template<class R> class promise;
template<class R> class promise<R&>;
template<> class promise<void>;

template<class R>
  void swap(promise<R>& x, promise<R>& y) noexcept;

template<class R, class Alloc>
  struct uses_allocator<promise<R>, Alloc>;

template<class R> class future;
template<class R> class future<R&>;
template<> class future<void>;

template<class R> class shared_future;
template<class R> class shared_future<R&>;
template<> class shared_future<void>;

template<class> class packaged_task; // not defined
template<class R, class... ArgTypes>
  class packaged_task<R(ArgTypes...)>;

template<class R, class... ArgTypes>
  void swap(packaged_task<R(ArgTypes...)>&, packaged_task<R(ArgTypes...)>&) noexcept;

template<class F, class... Args>
  [[nodiscard]] future<invoke_result_t<decay_t<F>, decay_t<Args>...>>
    async(F&& f, Args&&... args);
template<class F, class... Args>
  [[nodiscard]] future<invoke_result_t<decay_t<F>, decay_t<Args>...>>
    async(launch policy, F&& f, Args&&... args);
}
```

1 enum 类型 launch 是一个位掩码类型（16.3.3.3.4），其元素为 launch::async 和 launch::deferred。

> [注 1：实现可以提供位掩码以指定由 async() 启动的函数对任务交互的限制，适用于对应于可用启动策略子集的情况。实现可以通过在启动策略下添加其扩展来扩展 async() 的第一个重载的行为，采用“如同”规则。——注结束]

2 future_errc 的枚举值各不相同且不为零。

### 32.9.3 错误处理 [futures.errors]

```cpp
const error_category& future_category() noexcept;
```

1 返回：一个派生自类 error_category 的类型的对象的引用。

2 该对象的 default_error_condition 和等价的虚函数应按类 error_category 指定的方式行为。该对象的 name 虚函数返回指向字符串 "future" 的指针。

```cpp
error_code make_error_code(future_errc e) noexcept;
```

3 返回：error_code(static_cast<int>(e), future_category())。

```cpp
error_condition make_error_condition(future_errc e) noexcept;
```

4 返回：error_condition(static_cast<int>(e), future_category())。

- （7.1.2）——使其共享状态就绪；
- （7.2）——其次，提供者释放其共享状态。

8 共享状态仅在持有可检索的值或异常时才算就绪。等待共享状态就绪可能会在等待线程上调用代码以计算结果，如果创建状态对象的类或函数描述中如此指定。

9 对成功设置共享状态存储结果的函数的调用与（6.9.2）对由此设置导致就绪状态的函数成功检测的调用同步。将结果（正常或异常）存储到共享状态中与对共享状态的等待函数成功返回同步。

10 一些函数（例如，promise::set_value_at_thread_exit）会延迟在调用线程退出前才使共享状态就绪。销毁该线程的每个具有线程存储期（6.7.5.3）的对象的操作在使该共享状态就绪之前排序。

11 对同一共享状态的结果的访问可能冲突（6.9.2）。

> [注 4：这明确规定了共享状态的结果在引用该状态的对象中可见，以数据竞争避免（16.4.6.10）的意义上。例如，通过 shared_future::get()（32.9.8）返回的引用所进行的并发访问必须仅使用只读操作或提供额外同步。——注结束]

### 32.9.6 类模板 promise [futures.promise]

```cpp
namespace std {
  template<class R>
  class promise {
  public:
    promise();
    template<class Allocator>
    promise(allocator_arg_t, const Allocator& a);
    promise(promise&& rhs) noexcept;
    promise(const promise&) = delete;
    ~promise();

    // assignment
    promise& operator=(promise&& rhs) noexcept;
    promise& operator=(const promise&) = delete;
    void swap(promise& other) noexcept;

    // retrieving the result
    future<R> get_future();

    // setting the result
    void set_value(see below);
    void set_exception(exception_ptr p);

    // setting the result with deferred notification
    void set_value_at_thread_exit(see below);
    void set_exception_at_thread_exit(exception_ptr p);
  };

  template<class R>
    void swap(promise<R>& x, promise<R>& y) noexcept;

  template<class R, class Alloc>
    struct uses_allocator<promise<R>, Alloc>;
}
```

1 实现提供了模板 promise 以及两个特化 promise<R&> 和 promise<void>。它们仅在成员函数 set_value 和 set_value_at_thread_exit 的参数类型上有所不同，如下所述。

2 set_value、set_exception、set_value_at_thread_exit 和 set_exception_at_thread_exit 成员函数的行为就好像在更新 promise 对象时获取与 promise 对象关联的单个互斥量。

```cpp
template<class R, class Alloc>
struct uses_allocator<promise<R>, Alloc>
: true_type { };
```

前置条件：Alloc 满足 Cpp17Allocator 要求（表 36）。

```cpp
promise();
template<class Allocator>
promise(allocator_arg_t, const Allocator& a);
```

效果：创建一个共享状态。第二个构造函数使用分配器 a 为共享状态分配内存。

```cpp
promise(promise&& rhs) noexcept;
```

效果：将 rhs 的共享状态（如果有）所有权转移给新构造的对象。

后置条件：rhs 没有共享状态。

```cpp
~promise();
```

效果：放弃任何共享状态（32.9.5）。

```cpp
promise& operator=(promise&& rhs) noexcept;
```

效果：放弃任何共享状态（32.9.5），然后如同 promise(std::move(rhs)).swap(*this)。

返回：*this。

```cpp
void swap(promise& other) noexcept;
```

效果：交换 *this 和 other 的共享状态。

后置条件：*this 具有调用 swap 之前 other 所拥有的共享状态（如果有）。other 具有调用 swap 之前 *this 所拥有的共享状态（如果有）。

```cpp
future<R> get_future();
```

返回：一个与 *this 具有相同共享状态的 future<R> 对象。

同步：对该函数的调用不会与对 set_value、set_exception、set_value_at_thread_exit 或 set_exception_at_thread_exit 的调用引入数据竞争（6.9.2）。

> [注 1：此类调用不必相互同步。——注结束]

抛出：如果 *this 没有共享状态或如果已在与 *this 具有相同共享状态的 promise 上调用过 get_future，则抛出 future_error。

错误条件：
- future_already_retrieved 如果已在与 *this 具有相同共享状态的 promise 上调用过 get_future。
- no_state 如果 *this 没有共享状态。

```cpp
void promise::set_value(const R& r);
void promise::set_value(R&& r);
void promise<R&>::set_value(R& r);
void promise<void>::set_value();
```

效果：原子地将值 r 存储在共享状态中并使该状态就绪（32.9.5）。

抛出：
- 如果其共享状态已存储值或异常，则抛出 future_error，或
- 对于第一个版本，由复制 R 对象所选的构造函数抛出的任何异常，或
- 对于第二个版本，由移动 R 对象所选的构造函数抛出的任何异常。

错误条件：
- promise_already_satisfied 如果其共享状态已存储值或异常。
- no_state 如果 *this 没有共享状态。

