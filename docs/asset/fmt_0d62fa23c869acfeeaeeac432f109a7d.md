
## 23.11.4 unique_ptr 创建 [unique_ptr.create]

```cpp
template <class T, typename... Args>
unique_ptr<T> make_unique(Args&&... args);
```

- 1 返回 `unique_ptr<T>(std::forward<Args>(args)...)`。

```cpp
template <class T, typename... Args>
unique_ptr<T> make_unique(Args&&... args);
```

- 2 返回 `unique_ptr<T>(new T(std::forward<Args>(args)...))`。

```cpp
template <class T, typename... Args>
unique_ptr<T> make_unique(Args&&... args);
```

- 3 返回 `unique_ptr<T>(new T{std::forward<Args>(args)...})`。

## 23.11.5 unique_ptr 交换 [unique_ptr.swap]

```cpp
void swap(unique_ptr<T>& a, unique_ptr<T>& b) noexcept;
```

- 1 效果：调用 `a.swap(b)`。

```cpp
template <class T>
void swap(unique_ptr<T>& a, unique_ptr<T>& b);
```

- 2 效果：调用 `b.swap(a)`。

## 23.11.2 共享所有权指针 [util.smartptr]

### 23.11.2.1 类 bad_weak_ptr [util.smartptr.weak.bad]

# ISO/IEC 14882:2017(E)

public:

    `bad_weak_ptr()` noexcept;

};

- 1 `shared_ptr` 构造函数在尝试创建 `weak_ptr` 时会抛出 `bad_weak_ptr` 异常。

`bad_weak_ptr()` noexcept;

2 后置条件：`what()` 返回一个实现定义的 NTBS。

### 23.11.2.2 类 shared_ptr [util.smart.shared]

`shared_ptr` 类存储一个指针，该指针通常通过 `new` 获取。`shared_ptr` 实现所有权语义；指针的最后一个剩余所有者负责销毁对象，或者释放与存储的指针相关的资源。如果 `shared_ptr` 不拥有指针，则称其为空指针。

```cpp
namespace std {
template<class T> class shared_ptr {
public:
    using element_type = remove_extent<T>::element_type;
    using weak_type = weak_ptr<T>;

    // 23.11.2.1, 构造函数
    constexpr shared_ptr(nullptr) noexcept;
template<class Y> explicit shared_ptr(Y* p);
template<class Y, class D> shared_ptr(Y* p, D);
template<class Y, class D, class A> shared_ptr(Y* p, D, A);
template<class Y, class D, class A> shared_ptr(nullptr_t p, D, A);
template<class Y> shared_ptr(const shared_ptr<Y&&>& r, element_type* p) noexcept;
shared_ptr(const shared_ptr<Y>& r);
template<class Y> shared_ptr(const shared_ptr<Y&&>& r) noexcept;
template<class Y> shared_ptr(const shared_ptr<Y&&>& r) noexcept;
template<class Y, class D> shared_ptr(unique_ptr<Y, D>&& r);
template<class Y> explicit shared_ptr(const weak_ptr<Y>&& r);
constexpr shared_ptr(nullptr_t) : shared_ptr() {}

    // 23.11.2.2, 析析函数
    ~shared_ptr();

    // 23.11.2.3, 赋值
    shared_ptr& operator=(const shared_ptr<const>& r) noexcept;
template<class Y> shared_ptr& operator=(const shared_ptr<Y>& r) noexcept;
shared_ptr& operator=(shared_ptr<Y>&& r) noexcept;
template<class Y> shared_ptr& operator=(shared_ptr<Y>&& r) noexcept;
template<class Y, class D> shared_ptr& operator=(unique_ptr<Y, D>&& r);

    // 23.11.2.4, 修改器
    void swap(shared_ptr& r) noexcept;
void reset() noexcept;
template<class Y> void reset(Y* p);
template<class Y, class D> void reset(Y* p, D);
template<class Y, class D, class A> void reset(Y* p, D, A);
```

```cpp
// 23.11.2.5, 观察者
element_type* get() const noexcept
T& operator*() const noexcept
T& operator->() const noexcept
element_type* operator[](size_t i) const
long use_count() const noexcept
explicit operator bool() const noexcept
template<class U> bool owner_before(const shared_ptr<U>& b) const noexcept
template<class U> bool owner_after(const weak_ptr<U>& b) const noexcept
};

template<class T> shared_ptr(weak_ptr<T>) -> shared_ptr<T>;
template<class T> shared_ptr(unique_ptr<T>) -> shared_ptr<T>;
// 23.11.2.6, shared_ptr 的创建
template<class T, class... Args>
shared_ptr<T> make_shared(Args&&... args);
template<class T, class A, class... Args>
shared_ptr<T> allocate(A&& a, Args&&... args);

// 23.11.2.7, shared_ptr 比较
template<class T>
bool operator==(const shared_ptr<T>& a, const shared_ptr<T>& b) const
bool operator!=(const shared_ptr<T>& a, const shared_ptr<T>& b) const
template<class T>
bool operator<(const shared_ptr<T>& a, const shared_ptr<T>& b) const
template<class T>
bool operator>(const shared_ptr<T>& a, const shared_ptr<T>& b) const
template<class T>
bool operator==(const shared_ptr<T>& a, nullptr_t) const
template<class T>
bool operator==(nullptr_t, shared_ptr<T>& b) const
template<class T>
bool operator!=(const shared_ptr<T>& a, nullptr_t) const
template<class T>
bool operator!=(nullptr_t, shared_ptr<T>& b) const
template<class T>
bool operator<=(const shared_ptr<T>& a, nullptr_t) const
template<class T>
bool operator<=(nullptr_t, shared_ptr<T>& b) const
template<class T>
bool operator>(const shared_ptr<T>& a, nullptr_t) const
template<class T>
bool operator>(nullptr_t, shared_ptr<T>& b) const;
```

```cpp
// 23.11.2.8, shared_ptr 算法
template<class T>
void swap(shared_ptr<T>& a, shared_ptr<T>& b)

// 23.11.2.9, shared_ptr 类型转换
template<class T>
shared_ptr<T> static_cast(const shared_ptr<U>& r);
template<class T>
shared_ptr<T> dynamic_cast(const shared_ptr<U>& r);
template<class T>
shared_ptr<T> const_cast(const shared_ptr<U>& r);
template<class T>
shared_ptr<T> reinterpret_cast(const shared_ptr<U>& r);

// 23.11.2.10, shared_ptr I/O
template<class E, class T>
basic_ostream& operator<<(basic_ostream& os, const shared_ptr<T>& r);
```

# ISO/IEC 14882:2017(E)

> [注意：此构造函数允许使用一个非空的存储指针创建一个空的 `shared_ptr`。

-- 结束注意]

```
shared_ptr(const shared_ptr& r) noexcept;
template<class Y> shared_ptr(const shared_ptr<Y>& r) noexcept;
```

备注：第二个构造函数不参与重载解析，当 `Y*` 与 `Y*` 兼容时。

影响：如果 `r` 为空，则构造一个空的 `shared_ptr` 对象；否则，构造一个与 `r` 共享所有权的 `shared_ptr`。

后置条件：`get() == r.get() && use_count() == r.use_count()`。

```
shared_ptr(shared_ptr&& r) noexcept;
template<class Y> shared_ptr(shared_ptr<Y>&& r) noexcept;
```

备注：该构造函数不参与重载解析，当 `Y*` 与 `Y*` 兼容时。

影响：从 `r` 移动一个 `shared_ptr` 实例。

后置条件：`*this` 包含了 `r` 的唯一值。`r.get() == nullptr`。

```
template<class Y> explicit shared_ptr(shared_ptr<Y>&& r);
```

影响：构造一个与 `r` 共享所有权并拷贝 `r` 中存储的指针的 `shared_ptr`。如果抛出异常，则构造函数没有影响。

后置条件：`use_count() == r.use_count()`。

抛出：当 `r.expired()` 时抛出 `bad_ptr`。

备注：此构造函数不参与重载解析，当 `Y*` 与 `T*` 兼容时。

```
template<class Y, D> shared_ptr(unique_ptr<Y>, D& d);
```

备注：此构造函数不参与重载解析，当 `Y*` 与 `T*` 和 `unique_ptr<Y>` 兼容时，pointer 可转换为 `element_type`。

影响：如果 `r.get() == nullptr`，则等于 `shared_ptr(r)`。否则，如果 `D` 不是引用类型，则等于 `shared_ptr(r.release(), r.get_delete())`。否则，等于 `shared_ptr(r.release()), ref(r.get_delete()))`。如果抛出异常，则构造函数没有影响。

### 23.11.2.2 shared_ptr 析构函数

```
[util.smartptr.shared_ptr.dest]
```

- `*this` 为空或与另一个 `shared_ptr` 实例共享所有权（`use_count() > 1`），没有侧面影响。

- 否则，`*this` 拥有一个对象 `p` 和一个删除器，并调用了 `d(p)`。

- 否则，`*this` 拥有一个指针，并调用了 `delete p`。

> [注意：由于此处的销毁减少了与 `*this` 共享所有权的实例数量，因此在销毁之后，所有与 `*this` 共享所有权的 `shared_ptr` 实例报告的 `use_count()` 将比之前的值减一。

-- 结束注意]

### 23.11.2.3 shared_ptr 赋值

```
[util.smartptr.shared_ptr.assign]
```

```
shared_ptr& operator=(const shared_ptr& r) noexcept;
template<class Y> shared_ptr& operator=(const shared_ptr<Y>& r) noexcept;
```

影响：等于 `shared_ptr(r).swap(*this)`。

返回：`*this`。

[注意：通过临时对象的构造和销毁引起的引用计数更新不是可观测的影响，因此实现可以通过不同的手段满足这些影响（以及隐含的保证），而无需创建临时对象。特别是，例如所示：

```
shared_ptr<int> p(new int);
shared_ptr<void> q(p);
p = p;
q = q;
```

两次赋值都可能是空操作。 — 结束注意]

```
shared_ptr& operator=(shared_ptr&& r) noexcept;
template<class Y> shared_ptr& operator=(shared_ptr<Y>&& r) noexcept;
```

影响：等于 `shared_ptr(std::move(r)).swap(*this)`。

返回：`*this`。

```
template<class Y, class D> shared_ptr& operator=(unique_ptr<Y, D&&> r);
```

影响：等于 `shared_ptr(std::move(r)).swap(*this)`。

返回：`*this`。

### 23.11.2.4 shared_ptr 修改符

```
void swap(shared_ptr& r) noexcept;
```

影响：交换 `*this` 和 `r` 的内容。

```
void reset() noexcept;
```

影响：等于 `shared_ptr().swap(*this)`。

```
template<class Y> void reset(Y* p);
```

影响：等于 `shared_ptr(p).swap(*this)`。

```
template<class Y, class D> void reset(Y* p, D d);
```

影响：等于 `shared_ptr(p, D).swap(*this)`。

```
template<class Y, class D, class A> void reset(Y* p, D D, A A);
```

影响：等于 `shared_ptr(p, d, a).swap(*this)`。

### 23.11.2.2.5 shared_ptr 观察者

```
element_type* get() const noexcept;
```

返回：存储的指针。

```
T& operator() const noexcept;
```

要求：`get() != 0`。

```
T* get() const noexcept;
```

返回：`*get()`。

备注：当 `T` 是数组类型或 `void` 时，不确定是否声明了此成员函数。如果已声明，不确定其返回类型是什么，但函数的声明（尽管不是定义）应该是良好的。

```
template<class Y>
_ptr_shared_____ r;
```

备注：当 `T` 是数组类型或 `void` 时，不确定是否声明了此成员函数。如果已声明，不确定其返回类型是什么，但函数的声明（尽管不是定义）应该是良好的。

```
template_ptr_shared__() const noexcept;
```

```：shared_()()  
。

```

template<class Y> explicit shared_ptr(shared_ptr<Y>&& r);
