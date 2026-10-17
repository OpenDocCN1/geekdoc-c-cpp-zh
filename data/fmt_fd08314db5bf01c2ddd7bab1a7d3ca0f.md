
```cpp
// 使用延迟通知设置结果
void set_value_at_thread(const R& r);
void set_value_at_thread_exit(见下文);
void set_exception_at_thread_exit(exception_ptr p);
template <class R>
void swap(promise<R>& x, promise<R>& y) noexcept;
template <class R>
class Alloc {
struct uses_allocator<promise<R>, Alloc>;
```
+ 1 实现应提供 `promise` 以及两个特殊特化版本 `promise&&` 和 `promise<void>`。它们仅在成员函数 `set_value` 的参数类型上不同，正如其描述所示。
+ 2 `set_value`、`set_exception`、`set_value_at_thread_exit` 和 `set_exception_at_thread_exit` 成员函数的行为就像在更新 promise 对象时获取了与该 promise 对象相关的互斥锁。

```cpp
template <class R, class Alloc>
struct uses_allocator<promise<R>, Alloc>
: true_type { };
```
+ 3 要求：`Alloc` 为一个分配器 (17.6.3.5)。

```cpp
promise();
template <class Alloc>
promise(allocator_arg_t, const Alloc& a);
```
+ 4 效果：构造一个 promise 对象和一个共享状态。第二个构造函数使用分配器为共享状态分配内存。

```cpp
promise(promise&& rhs) noexcept;
```
+ 5 效果：构造一个新的 promise 对象，并将 `rhs` 的共享状态的所有权（如果有）转移给新构造的对象。
+ 6 后置条件：`rhs` 不再拥有状态。

```cpp
promise();
```
+ 7 效果：放弃任何共享状态 (30.6.4)。

§ 30.6.5

```cpp
promise& operator=(promise&& rhs) noexcept;
效果：放弃任何共享状态 (30.6.4)，然后执行 promise(std::move(rhs)).swap(*this);
返回：*this;
```

```cpp
void swap(promise& other) noexcept;
```
效果：交换 `*this` 和 `other` 之间的共享状态。
后置条件：`*this` 拥有在调用 `swap` 之前 `other` 所拥有的共享状态（如果有），`other` 拥有在调用 `swap` 之前 `*this` 所拥有的共享状态（如果有）。

```cpp
future<R> get_future();
```
返回：一个共享状态为 `*this` 的 `future<R>` 对象。
抛出异常：如果 `*this` 没有共享状态，或者如果已经在共享状态为 `*this` 的 promise 上已经调用过 `get_future`，则抛出错误。
错误条件：
+ - `future_already_retrieved`：如果已经在共享状态为 `*this` 的 promise 上已经调用过 `get_future`。
+ - `no_state`：如果 `*this` 没有共享状态。

```cpp
void promise::set_value(const R& r);
void promise::set_value(R&& r);
void promise<R&>::set_value(R&& r);
void promise<void>::set_value();
```
效果：原子性地在共享状态中设置值 `r` 并使该状态就绪 (30.6.4)。
抛出异常：
+ - 如果 `*this` 共享状态已经存储了值或异常，则抛出错误，或
+ - 对于第一个版本，`R` 的拷贝构造函数抛出的任何异常，或
+ - 对于第二个版本，`R` 的构造函数抛出的任何异常。
错误条件：
+ - `promise_already_satisfied`：如果 `*this` 共享状态已经存储了值或异常。
+ - `no_state`：如果 `*this` 没有共享状态。

```cpp
void set_exception(exception_ptr p);
```
效果：原子性地在共享状态中设置异常 `p` 并使该状态就绪 (30.6.4)。
抛出异常：如果 `*this` 共享状态已经存储了值或异常。
错误条件：
+ - `promise_already_satisfied`：如果 `*this` 共享状态已经存储了值或异常。
+ - `no_state`：如果 `*this` 没有共享状态。

```cpp
void promise::set_value_at_thread(const R& r);
void promise::set_value_thread_exit(R&& r);
void promise<R&>::set_value_thread_exit(R&& r);
void promise<void>::set_value_thread_exit();
```
§ 30.6.5
效果：在共享状态中存储值 `r` 而不使该状态就绪。调度在当前线程退出时（在与该线程相关的线程存储对象都销毁后）状态就绪。
抛出：如果发生错误则抛出 `future_error`。
错误：
+ - `promise_already_satisfied`：如果其共享状态已经存储了值或异常。
+ - `no_state`：如果 `*this` 没有共享状态。

```cpp
void promise::set_exception_at_thread_exit(exception_ptr p);
```
效果：在共享状态中存储异常 `p` 而不使该状态就绪。调度在当前线程退出时（在与该线程相关的线程存储对象都销毁后）状态就绪。
抛出：如果发生错误则抛出 `future_error`。
效果：如果 `*this` 共享状态已经已经存储了值或异常。
错误：
+ - `promise_already_satisfied`：如果其共享状态已经存储了值或异常。
+ - `no_state`：如果 `*this` 没有共享状态。

```cpp
template <class R>
void swap(promise<R>& x, promise<R>& y) noexcept;
template <class R>
class Alloc {
struct uses_allocator<promise<R>, Alloc>;
```

# ISO/IEC 14882:2011(E)

## 30.6.7 类模板 shared_future [futures.shared_future]

类模板 `shared_future` 定义了一种异步返回对象的类型，该对象可能与其他异步返回对象共享其共享状态。默认构造的 `shared_future` 对象不包含共享状态。可以通过从 `future` 对象转换创建一个具有共享状态的 `shared_future` 对象，并将其状态与原始提供者 (30.6.4) 共享作为共享状态。`shared_future` 对象的的结果（值或异常）可以通过在共享相同状态的对象上调用相应的函数来设置。

[注：`shared_future` 的成员不与自身同步，但它们与共享状态同步。—— 注结束]

对于 `valid() == false` 的 `shared_future` 对象，调用析构函数、移动赋值运算符或 `valid()` 以外的任何成员函数，其行为是未定义的。[注：鼓励实现检测此情况并抛出错误码为 `future_errc::no_state` 的 `future_error`—— 注结束]

```cpp
namespace std {
 template <class R>
 class shared_future {
 public:
 shared_future() noexcept;
 shared_future(const shared_future<R>& rhs) noexcept;
 shared_future(shared_future<R>&& rhs) noexcept;
 shared_future(shared_future&&) noexcept;
 const R& get() const;
 shared_future& operator=(const shared_future<R>& rhs);
 shared_future& operator=(shared_future&& rhs) noexcept;
 // 获取值
 查看下文 get(const) const;
 // 检查状态的函数
 bool valid() const noexcept;
 void wait() const;
 template <class Rep, class Period>
 future_status wait_for(chrono::duration<Rep, Period>& rel_time) const;
 template <class Clock, class Duration>
 future_status wait_until(chrono::time_point<Clock, Duration>& abs_time) const;
 };
}
```

实现应当提供模板 `shared_future` 以及两个特化版本：`shared_future<R>` 和 `shared_future<void>`。它们仅在成员函数 `get` 的返回类型和返回值上有所不同，下文描述如下。

```cpp
shared_future<void>() noexcept;
```
影响：构造一个空的 `shared_future` 对象，其不引用共享状态。
后置条件：`valid() == false`。

```cpp
shared_future(const shared_future<R>& rhs);
```
影响：构造一个 `shared_future` 对象，其引用与 `rhs` 相同的共享状态（如果有）。
后置条件：`valid()` 返回的值与 `rhs.valid()` 相同。

```cpp
shared_future(future<R&&> rhs) noexcept;
shared_future(shared_future&& rhs) noexcept;
```
影响：构造一个 `shared_future` 对象，其引用 `rhs` 原引用的共享状态（如果有）。
后置条件：
- `valid()` 返回的值与调用构造函数之前 `rhs.valid()` 返回的值相同。
- `rhs.valid() == false`。

```cpp
~shared_future();
```
影响：
- 释放任何共享状态 (30.6.4)；
- 销毁 *this*。

```cpp
shared_future& operator=(shared_future&& rhs) noexcept;
```
影响：
- 释放任何共享状态 (30.6.4)；
- 将 `rhs` 的内容移动赋值给 *this*。
后置条件：
- `valid()` 返回的值与赋值之前 `rhs.valid()` 返回的值相同。
- `rhs.valid() == false`。

```cpp
shared_future& operator=(const shared_future&& rhs);
```
影响：
- 释放任何共享状态 (30.6.4)；
- 将 `rhs` 的内容赋值给 *this*。[注：结果是，*this 指向了共享状态（如果有）。]
后置条件：`valid() == rhs.valid()`。

```cpp
const R shared_future::get() const;
R shared_future<R>::get() const;
void shared_future::get() const;
```
如上所述，模板及其两个特化版本仅在成员函数 `get` 的返回类型和返回值上不同。对存储在共享状态值的访问是非同步的，因此程序员应只对 `R` 执行那些不会引入数据竞争的操作 (1.10)。
影响：`wait()` 直到共享状态就绪，然后获取存储在共享状态的值。
返回：
- `shared_future::get()` 返回存储在对象中的值的 `const` 引用。[注：在共享状态被销毁后通过该引用进行访问是未定义的；可以通过返回引用的 `shared_future` 对象来避免。]

```cpp
shared_future<R&>::get() 返回存储在共享状态中的值。
shared_future<void>::get() 返回空。
```
抛出：如果共享状态中存储了任何异常。

```cpp
bool valid() const noexcept;
```
返回：如果 *this 指向共享状态，则返回 `true`。

```cpp
void wait() const;
```
影响：直到共享状态就绪。

```cpp
template <class Rep, class Period>
future_status wait_for(chrono::duration<Rep, Period>& rel_time) const;
```
影响：如果共享状态包含延迟函数 (30.6.8)，否则直到共享状态就绪或 `rel_time` 相对超时 (3.2)。
返回：
- 如果共享状态包含延迟函数，返回 `future_status::deferred`。
- 如果共享状态就绪，返回 `future_status::ready`。
- 如果通过 `rel_time` 相对超时 (3.2)，返回 `future_status::timeout`。

```cpp
template <class Clock, class Duration>
future_status wait_until(chrono::time_point<Clock, Duration>& abs_time) const;
```
影响：如果共享状态包含延迟函数 (30.6.8)，否则直到共享状态就绪或 `abs_time` 绝对超时 (3.2)。
返回：
- 如果共享状态包含延迟函数，返回 `future_status::deferred`。
- 如果共享状态就绪，返回 `future_status::ready`。
- 如果通过 `abs_time` 绝对超时 (3.2)，返回 `future_status::timeout`。

## 30.6.8 函数模板 async

模板 `async` 提供了一种可能在新线程中启动函数的机制，并提供与其共享共享状态的 `future` 对象的结果。

```cpp
template <class F, class... Args>
typename result_of<F(Args...)>::type async(F&& f, Args&&...);
template <class F, class... Args>
future<typename result_of<F(Args...)>::type> async(launch:: policy, F&& f, Args&&...);
```
