
```cpp
namespace std {
template<class T> class shared_ptr {
public:
    typedef T element_type;

    // 20.7.2.2.1, 构造函数:
    const shared_ptr() noexcept;
    template<class Y> explicit shared_ptr(Y*) noexcept;
    template<class Y, class D> shared_ptr(Y* p, D d);
    template<class Y, class D, class A> shared_ptr(Y* p, D, A);
    template<class D, class A> shared_ptr(nullptr_t, p, D, A);
    template<class Y> shared_ptr(const shared_ptr<Y>& r, T*) noexcept;
    shared_ptr(const shared_ptr<Y>& r);
    template<class Y> shared_ptr(shared_ptr<Y>&& r) noexcept;
    shared_ptr(shared_ptr());
    template<class Y> shared_ptr(shared_ptr<Y>&& r);
    template<class Y> shared_ptr(const weak_ptr<Y>& r);
    template<class Y> shared_ptr(weak_ptr<Y>&& r);
    template<class Y, class D> shared_ptr(const unique_ptr<Y, D>& r);
    template<class Y, class D> shared_ptr(unique_ptr<Y, D>&& r);
    template<class Y, class D> shared_ptr(const unique_ptr<Y, D>& r);
    constexpr shared_ptr(nullptr_t) {}

    // 20.7.2.2.2, 析构函数:
    ~shared_ptr();

    // 20.7.2.2.3, 赋值:
    shared_ptr& operator=(const shared_ptr& r);
    template<class Y> shared_ptr& operator=(const shared_ptr<Y>& r);
    shared_ptr& operator=(shared_ptr&& r);
    template<class Y> shared_ptr& operator=(shared_ptr<Y>&& r);
    template<class Y> shared_ptr& operator=(unique_ptr<Y>&& r);
    template<class Y, class D> shared_ptr& operator=(unique_ptr<Y, D>&& r);

    // 20.7.2.2.4, 修改器:
    void swap(shared_ptr& r) noexcept;
    void reset() noexcept;
    template<class Y> void* reset(Y* p) noexcept;
    template<class Y, class D> void reset(Y* p, D d);
    template<class Y, class D, class A> void reset(Y* p, D d, A a);

    // 20.7.2.2.5, 观察者:
    T* get() const;
    T& operator*() const;
    T* operator->() const;
    long use_count() const;
    bool operator() const;
    explicit bool operator() const;
    template<class U> bool owner_before(const shared_ptr<U>& b) const;
    template<class U> bool owner_before(const weak_ptr<U>& b) const;

    // 20.7.5.2.6, shared_ptr_创建:
    template<class T, class A, class... Args> shared_ptr<T> make_shared(Args&&... args);
    template<class T, class A, class... Args> shared_ptr<T> allocate(const T& a, Args&&... args);

    // 20.7.5.2.7, shared_ptr_比较:
    template<class T, class U> bool operator=(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
    template<class T, class U> bool operator!(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
    template<class T, class U> bool operator<(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
    template<class T, class U> bool operator>(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
    template<class T, class U> bool operator==(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
    template<class T, class U> bool operator>=(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;

    template<class T> bool operator=(const shared_ptr<T>& a, nullptr_t) noexcept;
    template<class T> bool operator=(nullptr_t, const shared_ptr<T>& b) noexcept;
    template<class T> bool operator!(const shared_ptr<T>& a, nullptr_t) noexcept;
    template<class T> bool operator!(nullptr_t, const shared_ptr<T>& b) noexcept;
    template<class T> bool operator!=(const shared_ptr<T>& a, nullptr_t) noexcept;
    template<class T> bool operator!=(nullptr_t, const shared_ptr<T>& b) noexcept;
    template<class T> bool operator<(const shared_ptr<T>& a, nullptr_t) noexcept;
    template<class T> bool operator<(nullptr_t, const shared_ptr<T>& b) noexcept;
    template<class T> bool operator<=(const shared_ptr<T>& a, nullptr_t) noexcept;
    template<class T> bool operator<=(nullptr_t, const shared_ptr<T>& b) noexcept;

    // 20.7.2.2.8, shared_ptr_特化算法:
    template<class T> void swap(shared_ptr<T>& a, shared_ptr<T>& b) noexcept;

    // 20.7.2.2.9, shared_ptr_强制转换:
    template<class T, class U> shared_ptr<T> static_pointer_cast(const shared_ptr<U>& r) noexcept;
    template<class T, class U> shared_ptr<T> dynamic_pointer_cast(const shared_ptr<U>& r) noexcept;
    template<class T, class U> shared_ptr<T> const_pointer_cast(const shared_ptr<U>& r) noexcept;

    // 20.7.5.2.10, shared_ptr_get删除:
    template<class D, class T> get_delete(const shared_ptr<T>& p) noexcept;
    // 20.7.5.2.11, shared_ptr I/O:
    template<class E, class T, class Y> basic_ostream<E, T&> operator<<(basic_ostream<E, T&, const shared_ptr<Y>& p);
} // namespace std
```

- 2 接收 `bad_weak_ptr` 的 `shared_ptr` 构造函数会抛出类型为 `bad_weak_ptr` 的异常。

2 后置条件：`what()` 返回 "`bad_weak_ptr`"。

## 20.7.2.2.1 shared_ptr 构造函数 [util.smartptr.shared]

1 `shared_ptr` 类模板存储一个指针，通常通过 `new` 获取。`shared_ptr` 实现了共享所有语义，指针的最后一个所有者负责销毁对象或者释放与指针相关的资源。如果 `shared_ptr` 对象没有拥有指针，则它为空的。

-1 `constr shared_ptr() noexcept;`

2 影响：构造一个空的 `shared_ptr` 对象。

后置条件：`use_count() == 0 && get() == 0;`

`template<class Y> explicit shared_ptr(Y* p);`

3 要求：`p` 应该可转换为 `T`。`Y` 应该是一个完整类型。表达式 `p` 应该是良好的、有定义行为且不抛出异常。

4 影响：构造一个拥有指针 `p` 的 `shared_ptr` 对象。

5 后置条件：`use_count() == 1 && get() == p;`

6 抛出：`bad_alloc`，或者由于内存以外的原因无法获取时的实现定义的异常。

7 异常安全性：如果抛出异常，将调用 `delete p`。

# ISO/IEC 14882:2011(E)

8 要求：p 应当转换为 `T*`。`D` 应当是可拷贝构造的（CopyConstructible）。`D` 的拷贝构造函数和析构函数不应抛出异常。表达式 `d(p)` 应当是良好的、具有定义的行为，且不应抛出异常。`A` 的分配器（17.6.3.5）拷贝构造函数和析构函数不应抛出异常。

9 效果：构造一个 `shared_ptr` 对象，该对象拥有 `p` 和析构执行器 `d`。第二个和第四个构造函数应使用 `a` 的拷贝来为内部使用分配内存。

10 后置条件：`use_count() == 1 && get() == p`。

11 抛出：`bad_alloc`，或者当无法获取内存以外的资源时抛出实现定义的异常。

12 异常安全性：如果抛出异常，则会调用 `d(p)`。

```cpp
template<class Y> shared_ptr(const shared_ptr<Y>&, T *p) noexcept;
```

13 效果：构造一个 `shared_ptr` 实例，它存储 `p` 并与 `r` 共享所有权。

14 后置条件：`get() == p && r.use_count()`。

15 [注意：由于悬空指针，此构造函数的用户必须确保在 `r` 的所有权销毁之前 `p` 保持有效。—— 注结束]

16 [注意：此构造函数允许使用非空指针创建一个空的 `shared_ptr` 实例。—— 注结束]

```cpp
shared_ptr(const shared_ptr<T>& r) noexcept;
template<class Y> shared_ptr(const shared_ptr<Y>& r) noexcept;
```

17 要求：除非 `Y*` 可以隐式转换为 `T*`，否则第二个构造函数不应参与重载解析。

18 效果：如果 `r` 为空，则构造一个空的 `shared_ptr` 对象；否则构造一个与 `r` 共享所有权的 `shared_ptr` 对象。

19 后置条件：`get() == r.get() && r.use_count()`。

```cpp
shared_ptr(shared_ptr<T>& r) noexcept;
template<class Y> shared_ptr(const shared_ptr<Y>& r) noexcept;
```

20 备注：除非 `Y*` 可以转换为 `T*`，否则第二个构造函数不应参与重载解析。

21 效果：从 `r` 移动构造一个 `shared_ptr` 实例。

22 后置条件：`get()` 应包含 `r` 的值。`r` 应为空。`r.get() == 0`。

```cpp
template<class Y> explicit shared_ptr(const shared_ptr<Y>& r);
```

23 要求：`Y*` 应当转换为 `T*`。

24 效果：构造一个与 `r` 共享所有权的 `shared_ptr` 对象，并存储 `r` 中存储指针的拷贝。

25 后置条件：`use_count() == r.use_count()`。

26 抛出：当 `r.expired()` 时抛出 `bad_weak`。

27 异常安全性：如果抛出异常，则构造函数没有影响。

```cpp
template<class Y> shared_ptr(auto_ptr<Y>&& r);
```

要求：`r.release()` 应当转换为 `T*`。`Y` 应当是一个完整类型。表达式 `delete r.release()` 应当是良好的、具有定义的行为，且不应抛出异常。

效果：构造一个共享并拥有 `r.release()` 的 `shared_ptr` 对象。

后置条件：`use_count() == 1 && r.get() == 0`。

抛出：`bad_alloc`，或者当无法获取内存以外的资源时抛出实现定义的异常。

异常安全性：如果抛出异常，则构造函数没有影响。

```cpp
template <class Y, class D> shared_ptr(unique_ptr<Y, D&&>);
```

效果：等于 `shared_ptr(r.release())` 当 `D` 不是引用类型时，为 `r.get_deleter()`；否则等于 `shared_ptr(r.release()), ref(r.get_deleter())`。

异常安全性：如果抛出异常，则构造函数没有影响。

## 20.7.2.2.2 shared_ptr 析构函数 [util.smart_ptr.dest]

```cpp
~shared_ptr();
```

- 效果：
  - *this为空或与另一个 `shared_ptr` 实例共享所有权（`use_count() > 1`），则没有侧影响。
  - 否则，*this拥有一个对象 `p` 和一个析构执行器 `d`，调用 `d(p)`。
  - 否则，*this拥有一个指针 `p`，并调用 `delete`。

> [注意：*this 的析毁使与 *this 共享所有权的实例数量减少一个，在 *this 被销毁后，所有与 *this 共享所有权的 `shared_ptr` 实例报告的 `use_count()` 将比其之前的值少 1。—— 注结束]

## 20.7.2.2.3 shared_ptr 赋值 [util.smart_ptr.shared.assign]

```cpp
shared_ptr& operator=(const shared_ptr<R>& r) noexcept;
template<class Y> shared_ptr& operator=(const shared_ptr<Y>&& r) noexcept;
template<class Y> shared_ptr& operator=(auto_ptr<Y>&& r);
```

- 效果：等于 `operator=`。
- 返回：*this。

> [注意：通过临时对象构造和析构引起的引用计数更新是不可观测的，因此实现可能会在不创建临时对象的情况下产生影响。特别示例示例：
> ```cpp
> shared_ptr<int> p(new int);
> shared_ptr<int> q(p);
> p = q;
> q = p;
> ```
> 赋值可能是无操作。—— 注结束]

```cpp
shared_ptr& operator=(shared_ptr&& r) noexcept;
template<class Y> shared_ptr& operator=(shared_ptr<Y>&& r) noexcept;
```

### 20.7.2.2.4 shared_ptr 修改器 [util.smart_ptr.shared]
