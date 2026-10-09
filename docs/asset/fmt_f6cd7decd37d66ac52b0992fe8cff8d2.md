
`promise_already_satisfied` 如果其共享状态已存储值或异常。

`no_state` 如果 `*this` 无状态。

```cpp
void set_exception(exception_ptr p);
```

前置条件：`p` 不空。

影响：原子地将异常指针存储在共享状态中，并使状态准备就绪 (`32.9.5`)。

抛出：如果其共享状态已经有一个已存储的值或异常，则抛出 `future_error`。

错误条件：

- `promise_already_satisfied`：如果其共享状态已经有一个存储的值或异常。
- `no_state`：如果该对象没有共享状态。

```cpp
void promise::set_value_at_exit(const R& r);
void promise::set_value_at_thread_exit(R& r);
void promise<R>::set_value_at_thread_exit(R& r);
void promise<void>::set_value_at_thread_exit();
```

影响：将值存储在共享状态中，但不会立即让状态就绪。调度该状态在当前线程退出时准备就绪，在所有与当前线程相关的线程存储对象被销毁后执行。

抛出：

- `promise_already_satisfied`：如果其共享状态已经有一个存储的值或异常；
- 第一次：任何用于选择 `R` 实例对象的构造函数中抛出的任何异常；
- 第二次：任何用于移动 `R` 实例对象的构造函数中抛出的任何异常。

错误条件：

- `promise_already_satisfied`：如果其共享状态已经有一个存储的值或异常。
- `no_state`：如果该对象没有共享状态。

```cpp
void set_exception_at_exit(exception_ptr p);
```

前置条件：`p` 不空。

影响：将异常指针存储在共享状态中，但不会立即让状态就绪。调度该状态在当前线程退出时准备就绪，在所有与当前线程相关的线程存储对象被销毁后执行。

抛出：如果发生错误条件，则抛出 `future_error`。

错误条件：

- `promise_already_satisfied`：如果其共享状态已经有一个存储的值或异常。
- `no_state`：如果该对象没有共享状态。

```cpp
template<class R>
void swap(promise<R>& x, promise<R>& y) noexcept;
```

影响：如果 `x.swap(y)`。

## 32.97 类模板 future

该类模板为异步返回对象定义了一种类型，这些对象不与其他异步对象共享其共享状态。一个默认构造的 `future` 对象没有共享状态。带有共享状态的 `future` 可以通过异步提供者 (`32.9.5`) 或通过移动构造函数创建，并与原始异步提供者共享其共享状态。`future` 对象的结果（值或异常）可以通过在共享该状态的对象上调用相应函数来设置。

> [注 1] `future` 的成员不会与其自身或与 `shared_future` 的成员同步——结束注。

如果 `valid() == false`，则在 `future` 对象上调用除析构函数、移动赋值运算符、`share` 或 `value` 之外的任何成员函数时，其行为是未定义的。

> [注 2] 如果 `valid() == false`，从 `future` 移动对象是合法的——结束注。

推荐做法：实现应当检测到此情况，并抛出一个类型为 `future_error` 的对象，其错误条件为 `future_err::no_state`。

```cpp
namespace std {
template<class R>
class future {
public:
    future() noexcept;
    future(future&& rhs) noexcept;
    future(const future&) = delete;
    ~future();
    future& operator=(const future&) = delete;
    future& operator=(future&& rhs) noexcept;
    shared_ptr<R> share() const noexcept;
```

```cpp
// 获取值
见下文 get();
```

```cpp
// 检查状态的
bool valid() const noexcept;
```

```cpp
void wait() const {
template<class Rep, class Period>
future_status wait_for(chrono::duration<Rep, Period>& rel_time) const;
template<class Clock, class Duration>
future_status wait_until(chrono::time_point<Clock, Duration>& abs_time) const;
};
```

4 实现提供了模板 `future` 和两个特化版本，`future<R&>` 和 `future<void>`。它们仅在成员函数 `get` 的返回类型和返回值有所不同，正如其描述所示：

`future() noexcept;`

影响：该对象不引用任何共享状态。

- 5 后置条件：`valid() == false`。

`future(future&& rhs) noexcept;`

影响：移动构造一个 `future` 对象，该对象引用 `rhs` 原引用的共享状态（如果有）。

后置条件：

- `valid()` 返回的值与构造函数调用前 `rhs.valid()` 的值相同。
- `rhs.valid() == false`。

`~future();`

影响：

- 释放任何共享状态 (`32.9.5`)。
- 销毁 `*this*`。

`future& operator=(future&& rhs) noexcept;`

影响：

- 释放任何共享状态 (`32.9.5`)。
- 将 `rhs` 的内容移动赋值给 `*this`。

后置条件：

- `valid()` 返回的值与 `rhs.valid()` 的值相同。
- `rhs.valid() == false`。

`shared_ptr<R> share() const noexcept;`

返回：`shared_ptr<R>`。

后置条件：`valid() == false`。

## 32.98 类模板 shared_future

该类模板定义了一种用于异步返回对象的类型，这些对象与其他异步对象共享其共享状态。一个默认构造的 `shared_future` 对象没有共享状态。带有共享状态的 `shared_future` 可以通过异步提供者 (`32.9.5`) 或通过移动构造函数创建，并与原始异步提供者共享其共享状态。`shared_future` 对象的结果（值或异常）可以通过在共享该状态的对象上调用相应函数来设置。

> [注 1] `shared_future` 的成员会与其自身或与 `future` 的成员同步——结束注。

如果 `valid() == false`，则在 `shared_future` 对象上调用除析构函数、移动赋值运算符、`share` 或 `value` 之外的任何成员函数时，行为是未定义的。

> [注 2] 如果 `valid() == false`，从 `shared_future` 移动对象是合法的——结束注。

推荐做法：实现应当检测到此情况，并抛出一个类型为 `future_error` 的对象，其错误条件为 `future_err::no_state`。

```cpp
namespace std {
template<class R>
class shared_future {
public:
    shared_future() noexcept;
    shared_future(future&& rhs) noexcept;
    shared_future(const shared_future&) = delete;
    ~shared_future();
    shared_future& operator=(const shared_future&) = delete;
    shared_future& operator=(shared_future&& rhs) noexcept;
    shared_ptr<R> get() const noexcept;
```

```cpp
// 获取值
见下文 get();
```

```cpp
// 检查状态的
bool valid() const noexcept;
```

```cpp
void wait() const {
template<class Rep, class Period>
future_status wait_for(chrono::duration<Rep, Period>& rel_time) const;
template<class Clock, class Duration>
future_status wait_until(chrono::time_point<Clock, Duration>& abs_time) const;
};
```

4 实现提供了模板 `shared_future` 和两个特化版本，`shared_future<R&>` 和 `shared_future<void>`。它们仅在成员函数 `get` 的返回类型和返回值有所不同，正如其描述所示：

`shared_future() noexcept;`

影响：该对象不引用任何共享状态。

- 5 后置条件：`valid() == false`。

`shared_future(future&& rhs) noexcept;`

影响：移动构造一个 `shared_future` 对象，该对象引用 `rhs` 原引用的共享状态（如果有）。

后置条件：

- `valid()` 返回的值与构造函数调用前 `rhs.valid()` 的值相同。
- `rhs.valid() == false`。

`~shared_future();`

影响：

- 释放任何共享状态 (`32.9.5`)。
- 销毁 `*this*`。

`shared_future& operator=(shared_future&& rhs) noexcept;`

影响：

- 释放任何共享状态 (`32.9.5`)。
- 将 `rhs` 的内容移动赋值给 `*this`。

后置条件：

- `valid()` 返回的值与 `rhs.valid()` 的值相同。
- `rhs.valid() == false`。

`shared_ptr<R> get() const noexcept;`

返回：`shared_ptr<R>`。

后置条件：`valid() == false`。

## 32.99 类模板 shared_future

该类模板定义了一种用于异步返回对象的类型，这些对象与其他异步对象共享其共享状态。一个默认构造的 `shared_future` 对象没有共享状态。带有共享状态的 `shared_future` 可以通过异步提供者 (`32.9.5`) 或通过移动构造函数创建，并与原始异步提供者共享其共享状态。`shared_future` 对象的结果（值或异常）可以通过在共享该状态的对象上调用相应函数来设置。

> [注 1] `shared_future` 的成员会与其自身或与 `future` 的成员同步——结束注。

如果 `valid() == false`，则在 `shared_future` 对象上调用除析构函数、移动赋值运算符、`share` 或 `value` 之外的任何成员函数时，其行为是未定义的。

> [注 2] 如果 `valid() == false`，从 `shared_future` 移动对象是合法的——结束注。

推荐做法：实现应当检测到此情况，并抛出一个类型为 `future_error` 的对象，其错误条件为 `future_err::no_state`。

```cpp
namespace std {
template<class R>
class shared_future {
public:
    shared_future() noexcept;
    shared_future(future&& rhs) noexcept;
    shared_future(const shared_future&) = delete;
    ~shared_future();
    shared_future& operator=(const shared_future&) = delete;
    shared_future& operator=(shared_future&& rhs) noexcept;
    shared_ptr<R> get() const noexcept;
```

`shared_future& operator=(shared_future&& rhs) noexcept;`

# 影响：

- 释放任何共享状态 (`32.9.5`)；
- 移动赋值将 `rhs` 的内容赋值给 `*this*`。

# 后置条件：

- `valid()` 返回的值与赋值前 `rhs.valid()` 返回的值相同。
- `rhs.valid() == false`。

```cpp
shared_future& operator=(const shared_future& rhs) noexcept;
```

# 影响：

- 释放任何共享状态 (`32.9.5`)；
- 将 `*this*` 的内容赋值给与 `rhs` 相同的共享状态（如果有的话）。

> [注意 3: 结果，*this 指向*]

# 后置条件：

- `rhs.valid()`。

```cpp
const R& shared_future::get() const;
R& shared_future<R>::get() const;
void shared_future::get() const;
```

> [注意 4: 如上所述，该模板及其两个特化版本之间的区别在于成员函数的返回类型和返回值。]

> [注意 5: 访问共享状态中存储的值是不同步的，可能会执行某些操作以引入竞态条件 (`32.9.2`)。]

> [注意 6: 在共享状态销毁后通过引用访问会产生未定义行为：可以通过不将引用存储在任何生命周期比 `get()` 返回的 `shared_future` 更长的存储器中来避免。]

```cpp
shared_future<R>::get() const 返回对象共享状态中存储的值。
shared_future<void>::get() const 不返回任何内容。
```

抛出：如果在处理共享状态时抛出了异常，则抛出该异常。

```cpp
bool valid() const noexcept;
```

# 返回：

如果 `*this` 共享状态就绪，则返回 true。

# 影响：

阻塞直到状态就绪。

```cpp
template<class Rep, class Period>
future_status wait_for(chrono::duration<Rep, Period>& rel_time) const;
```

抛出：如果共享状态包含一个延迟执行的函数 (`32.9.4`)，否则阻塞直到状态就绪或相对超时 (`rel_time`) 到期。

# 返回：

- 如果共享状态包含一个延迟执行的函数，返回 `future_status::deferred`。
- 如果共享状态就绪，返回 `future_status::ready`。
- 如果函数因为相对超时 (`rel_time`) 到期而返回，返回 `future_status::timeout`。

抛出：超时相关的异常 (`32.2.4`)。

```cpp
template<class Clock, Duration>
future_status wait_until(const chrono::time_point<Clock, Duration>& abs_time) const;
```

# 影响：

如果共享状态包含一个延迟执行的函数 (`32.9.9`)，否则阻塞直到状态就绪或由 `abs_time` 决定的绝对超时 (`32.2.4`) 到期。

# 返回：

- 如果共享状态包含一个延迟执行的函数，返回 `future_status::deferred`。
- 如果共享状态就绪，返回 `future_status::ready`。
- 如果函数因为由 `abs_time` 决定的绝对超时 (`32.2.4`) 到期而返回，返回 `future_status::timeout`。

# 抛出：超时相关的异常 (`32.2.4`)。

## 32.9.9 函数模板 async [futures.async]

函数模板 `async` 提供了一种在线程线程中启动函数的机制，并在其共享的共享状态的 `future` 对象中提供函数的结果。

```cpp
template<class F, class Args...>
[[nodiscard]] future<invoke_result_t<decay_t<F>, decay_t<Args>...>>
async(F&& f, Args&&...);
template<class F, class Args...>
[[nodiscard]] future<invoke_result_t<decay_t<F>, decay_t<Args>...>>
async(launch::policy policy, F&& f, Args&&...);
```

2 强制要求：

以下条件均成立：

- (2.1) `is_constructible<decay_t<F>, F>`。
- (2.2) `is_constructible<decay_t<Args>, Args> && ...`
- (2.3) `is_move_constructible<decay_t<F>>`。
- (2.4) `is_move_constructible<decay_t<Args>>...> && ...`
- (2.5) `is_invocable<decay_t<F>>` 且 `decay_t<Args>...` 中的每个类型都符合 C++17 MoveConstructible 要求。
