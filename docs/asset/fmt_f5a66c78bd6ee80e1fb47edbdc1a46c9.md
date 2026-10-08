
```cpp
template<class Y> explicit shared_ptr(const weak_ptr<Y>& r);
```

要求：`Y` 应当转换为 `T*`。

影响：构造一个与 `r` 共享所有权并存储 `r` 中指针的 `shared_ptr` 对象。

后置条件：`use_count() == r.use_count()`。

抛出：如果抛出异常，构造函数没有影响（`bad_weak_ptr`）。

异常安全：如果抛出异常，构造函数没有影响。

```cpp
template<class Y, class D> shared_ptr(unique_ptr<Y, D&&> r);
```

备注：除非 `unique_ptr<Y, D>` 可转换为 `T*`，否则此构造函数不参与重载解析。

影响：当 `D` 不是引用类型时，相当于 `shared_ptr(r.release(), r.get_deleter())`，否则相当于 `shared_ptr(r.release(), ref(r.get_deleter()))`。

异常安全：如果抛出异常，构造函数没有影响。

## 20.8.2.2.2 shared_ptr 析构函数

```cpp
-shared_ptr();
```

影响：

- `*this` 为空或与其他 `shared_ptr` 实例共享所有权（`use_count() > 1`），没有副作用。
- 否则，如果 `*this` 拥有对象和一个删除器，则调用 `d(p)`。
- 否则，`*this` 拥有指针 `p`，并调用 `delete`。

备注：`*this` 的销毁会使与 `*this` 共享所有权的实例减少一个，所有与 `*this` 共享所有权的 `shared_ptr` 实例将报告比之前值少一的 `use_count()`。备注结束

## 20.8.2.2.3 shared_ptr 赋值

```cpp
shared_ptr& operator=(const shared_ptr& r) noexcept;
template<class Y> shared_ptr& operator=(const shared_ptr<Y>& r) noexcept;
```

影响：相当于 `shared_ptr(std::move(r)).swap(*this)`。

返回：

```cpp
shared_ptr<int> p(new int);
shared_ptr<void> q(p);
p = p;
q = p;
```

两次赋值都可能是无操作。—备注结束

```cpp
shared_ptr& operator=(shared_ptr&& r) noexcept;
template<class Y> shared_ptr& operator=(shared_ptr<Y>&& r) noexcept;
```

影响：相当于 `shared_ptr(std::move(r)).swap(*this)`。

返回：`*this`.

```cpp
template <class Y, class D> shared_ptr& operator=(unique_ptr<Y, D&&>& r);
```

影响：等于 `shared_ptr(move(r)).swap(*this)`；

返回：`*this*`

### 20.8.2.2.4 shared_ptr 修饰符

`util.smartptr.shared.modhed`

```cpp
void swap(shared_ptr& r) noexcept;
```

影响：交换 `*this` 和 `r` 的内容。

```cpp
void reset() noexcept;
```

影响：等于 `shared_ptr().swap(*this)`；

```cpp
template<class Y> reset(Y* p);
```

影响：等于 `shared_ptr(p).swap(*this)`；

```cpp
template<class Y, class D> void reset(Y* p, D d);
```

影响：等于 `shared_ptr(p, d).swap(*this)`；

```cpp
template<class Y, class D, class A> void reset(Y* p, D d, A* a);
```

影响：等于 `shared_ptr(p, d, a).swap(*this)`；

### 20.8.2.2.5 shared_ptr 观察者

`util.smartptr.shared.obs`

```cpp
T* get() const noexcept;
```

返回：存储的指针。

```cpp
T& operator() const noexcept;
```

要求：`get() != 0`；

返回：`*get()`；

备注：当 `T` 为 `void` 时，不确定此成员函数是否被声明。如果已声明，则不确定返回类型是什么，但该函数的声明（尽管不一定有定义）应当是良好的。

```cpp
T* operator->() const noexcept;
```

要求：`get() != 0`；

返回：`get()`；

```cpp
long use_count() const noexcept;
```

返回：与 `*this` 共享所有权的（包括 `*this` 在内）的 `shared_ptr` 对象数量，或者当 `*this` 为空时。

> [注：`use_count()` 不一定高效。注结束]

```cpp
bool unique() const noexcept;
```

返回：`use_count() == 1`。

> [注：`unique()` 可能比 `use_count()` 快。要实现写时复制，当 `get() == nullptr` 时，不要依赖特定值。注结束]

```cpp
explicit operator bool() const noexcept;
```

返回：`get() = 0`.

```cpp
template<class U> bool owner_before(shared_ptr<U> const& b) const;
template<class U> bool owner_before(weak_ptr<U> const& b) const;
```

返回：一个未指定的值，使得：

- `x.owner_before(y)` 定义了如 25.4 中定义的 `defined_before` 的严格排序；
- 根据 `owner_before` 定义的等价关系，`!a.owner_before(b) && !b.owner_before(a)`，两个 `shared_ptr` 或 `weak_ptr` 实例仅在它们共享所有权或两者都为空时才等价。

## 20.8.2.6 shared_ptr 创建

`[util.smartptr.shared_create]`

```cpp
template<class T, class Args...> shared_ptr<T> make_shared(Args&&... args);
template<class T, class Args...> class...;
shared_ptr<T> allocate(const T& a, Args&&... args);
```

- 1：表达式 `::(new p) (T(std::forward<Args>(args)...))`，其中 `p` 的类型为 `T*` 并指向用于分配类型为 `T` 的对象的内存，应当良好的。`A` 应该是 `allocator_t(17.8.3.5)`。`A` 的拷贝构造函数和析构函数不应抛出异常。
- 2：为类型为 `T` 的对象分配内存，并通过定位 new 表达式 `::(new p) (T(std::forward<Args>(args)...))` 在内存中构造对象。模板 `allocate` 使用 `a` 的拷贝来分配内存。如果抛出异常，这些函数将没有影响。
- 3：返回一个存储地址并拥有新构造的 `T` 类型对象的 `shared_ptr` 实例。
- 后置条件：`get() != 0 && use_count() == 1`
- 5：来自 `A::allocate` 或 `T` 构造函数的异常
- 6：实现应执行少于一次内存分配。[：这为内联指针提供了效率。注结束]。

> 注：这些函数分配的内存比 `sizeof(T)` 多，用于内部计数结构（如引用计数）。注结束]。

## 20.8.2.7 shared_ptr 比较

`[util.smartptr.shared_cmp]`

```cpp
template<class T> bool operator==(const shared_ptr<T>& a, const shared_ptr<T>& b) noexcept;
```

返回：`a.get() == b.get()`

```cpp
template<class T> bool operator==(const shared_ptr<T>& a, const shared_ptr<T>& b) noexcept;
```

返回：`less<V>(a.get(), b.get())`，其中 `V` 是 `T*` 和 `U` 的复合。[注：定义比较允许 `shared_ptr` 对象在关联容器中作为键。注结束]。

```cpp
template<class T> bool operator==(const shared_ptr<T>& a, nullptr_t) noexcept;
template<class T> bool operator==(nullptr_t, shared_ptr<T>& a) noexcept;
```

返回：`!a`。

## ISO/IEC N26

```cpp
template<class T> bool operator!=(const shared_ptr<T>& a, nullptr_t) noexcept;
template<class T> bool operator!=(nullptr_t, shared_ptr<T>& a) noexcept;
```

5：`(bool)a`。

```cpp
template<class T> bool operator<=(const shared_ptr<T>& a, nullptr_t) noexcept;
template<class T> bool operator<=(nullptr_t, shared_ptr<T>& a) noexcept;
```

6：第一个模板函数返回 `less<T>(a.get())`。第二个模板函数返回 `less<T>(a.get())`。

```cpp
template<class T> bool operator<=(const shared_ptr<T>& a, nullptr_t) noexcept;
template<class T> bool operator<=(nullptr_t, shared_ptr<T>& a) noexcept;
```

7：第一个模板函数返回 `nullptr`。第二个模板函数返回 `a`。

```cpp
template<class T> bool operator>=(const shared_ptr<T>& a, nullptr_t) noexcept;
template<class T> bool operator>=(nullptr_t, shared_ptr<T>& a) noexcept;
```

8：第一个模板函数返回 `!(a < nullptr)`。

```cpp
template<class T> bool operator>=(const shared_ptr<T>& a, nullptr_t) noexcept;
template<class T> bool operator>=(nullptr_t, shared_ptr<T>& a) noexcept;
```

9：第一个模板函数返回 `!(a < nullptr)`。第二个模板函数返回 `!(a < nullptr)`。

## 20.8.2.2 swap 特化算法 [util.smartptr.shared.spec]

```cpp
template<class T> void swap(shared_ptr<T>& a, shared_ptr<T>& b)
```

- 1 影响：等于 `a.swap(b)`。

`[util.smartptr.shared.cast]`

```cpp
template<class T, class U> shared_ptr<T>(const shared_ptr<U>& r) noexcept;
```

- 1 要求：表达式 `static_cast<T>(r.get())` 良好。
- 2 返回：如果 `r` 为空，返回 `empty_ptr<T>`；否则返回一个存储 `static_cast<T>(r.get())` 并与 `r` 共享所有权的 `shared_ptr<T>` 对象。
- 3 后置条件：`w.get() == static_cast<T>(r.get())` 且 `w.use_count() == r.use_count()`，其中 `w` 是返回值。

> 注：看似等等的 `shared_ptr<T>(static_cast<T>(r.get()))` 将不可避免导致未定义行为，尝试删除同一个对象。注结束]

```cpp
template<class T, class U> shared_ptr<T> dynamic_pointer_cast(const shared_ptr<U>& r) noexcept;
```

要求：表达式 `dynamic_cast<T>(r.get())` 良好且具有定义的行为。

返回：

- 当 `dynamic_cast<T>(r.get())` 返回非零值时，返回一个存储其拷贝并与 `r` 共享所有权的 `shared_ptr<T>` 对象：
- 否则，返回一个 `empty_ptr<T>` 对象。

后置条件：`w.get() == dynamic_cast<T>(r.get())`，其中 `w` 是返回值。

> 注：同样等等的 `shared_ptr<T>(dynamic_cast<T>(r.get()))` 将不可避免导致未定义行为，尝试两次删除同一个对象。注结束]

```cpp
template<class T, class U> shared_ptr<T> post_counter(const shared_ptr<U>& r) noexcept;
```

要求：表达式 `const_cast<T>(r.get())` 良好。

返回：如果 `r` 为空，返回 `empty_ptr<T>`；否则返回一个存储 `const_cast<T>(r.get())` 并与 `r` 共享所有权的 `shared_ptr<T>` 对象。

后置条件：`w.get() == const_cast<T>(r.get())` 且 `w.use_count() == r_use_count()`，其中 `w` 是返回值。

> 注：等等的 `shared_ptr<T>(const_cast<T>(r.get()))` 将不可避免导致未定义行为，尝试两次删除同一个对象。注结束]

## 20.8.2.10 get_deleter [util.smartptr.getdeleter]

```cpp
template<class T, class D> get_deleter(const shared_ptr<T>& r) noexcept;
```

返回：如果 `p` 拥有类型为无限定 `D` 的删除器，则返回 `addressof(d)`；否则返回 `nullptr`。只要存在拥有 `d` 的 `shared_ptr` 实例，返回的指针就有效。注：这可能持续直到所有与 `p` 共享所有权的 `weak_ptr` 实例都被销毁。注结束]。

## 20.8.2.11 shared_ptr I/O [util.smartptr.io]

```cpp
template<class E, class T> basic_ostream<E, T& os, shared_ptr<T> const& p;
```

影响：`os << p.get()`；

返回：`os`。

## 20.8.2.13 Class weak_ptr [util.smartptr.weak]

`weak_ptr` 类模板存储对已由 `shared_ptr` 管理的对象的引用。要访问对象，可以将 `weak_ptr` 使用 `lock` 转换为 `shared_ptr`。

```cpp
namespace std {
    template<class T> class weak_ptr {
    public:
        typedef T element_type;
```

```cpp
// 20.8.2.3.1,构造函数
    constexpr weak_ptr() noexcept;
    template<class Y> weak_ptr(shared_ptr<Y> const& r) noexcept;
    weak_ptr(weak_ptr<Y> const& r) noexcept;
    template<class Y> weak_ptr(weak_ptr<Y> const& r) noexcept;
```

# ISO/IEC N4296

```cpp
weak_ptr(weak_ptr&& r) noexcept;
template<class Y> weak_ptr(weak_ptr<Y>&& r) noexcept;
```

```cpp
// 20.8.2.3.2, 析构函数
~weak_ptr();
```

```cpp
// 20.8.2.3.3, 赋值
weak_ptr& operator=(const weak_ptr& r) noexcept;
template<class Y> weak_ptr& operator=(weak_ptr<Y> const& r) noexcept;
template<class Y> weak_ptr& operator=(shared_ptr<U> const& r) noexcept;
weak_ptr& operator=(weak_ptr&& r) noexcept;
template<class Y> weak_ptr& operator=(weak_ptr<Y>&& r) noexcept;
```
