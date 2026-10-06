

# ISO/IEC 14882:2017(E)

public:
    bad_weak_ptr() noexcept;
};

- 1 `shared_ptr` 构造函数在尝试创建 `weak_ptr` 时会抛出 `bad_weak_ptr` 异常。
bad_weak_ptr() noexcept;
2 后置条件：`what()` 返回一个实现定义的 NTBS。

## 23.11.2.2 类 shared_ptr [util.smart.shared]

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
