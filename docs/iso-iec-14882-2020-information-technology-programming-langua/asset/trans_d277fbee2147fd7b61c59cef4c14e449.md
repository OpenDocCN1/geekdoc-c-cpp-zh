

# ISO/IEC 14882:2020(E)

```
template<class T, class A>
    shared_ptr<T> allocate_shared(const A& a, size_t N,
                                    const remove_extent_t<T>& u);    // T is U[]
```

约束：T 的形式为 U[]。

返回：指向类型为 U[N] 的对象的 shared_ptr，其中 U 为 remove_extent_t<T>，并且每个数组元素都具有初始值 u。

```
[Example 4:
    shared_ptr<double[]> p = make_shared<double[]>(1024, 1.0);
    // shared_ptr to a double[1024], where each element is 1.0
    shared_ptr<double[] [2]> q = make_shared<double[] [2]>(6, {1.0, 0.0});
    // shared_ptr to a double[6] [2], where each double[2] element is {1.0, 0.0}
    shared_ptr<vector<int>[]> r = make_shared<vector<int>[]>(4, {1, 2});
    // shared_ptr to a vector<int>[4], where each vector has contents {1, 2}
    — end example]
```

```
template<class T>
    shared_ptr<T> make_shared(const remove_extent_t<T>& u);    // T is U[N]
template<class T, class A>
    shared_ptr<T> allocate_shared(const A& a,
                                  const remove_extent_t<T>& u);    // T is U[N]
```

约束：T 的形式为 U[N]。

返回：指向类型为 T 的对象的 shared_ptr，其中类型为 remove_extent_t<T> 的每个数组元素都具有初始值 u。

```
[Example 5:
    shared_ptr<double[1024]> p = make_shared<double[1024]>(1.0);
    // shared_ptr to a double[1024], where each element is 1.0
    shared_ptr<double[6] [2]> q = make_shared<double[6] [2]>({1.0, 0.0});
    // shared_ptr to a double[6] [2], where each double[2] element is {1.0, 0.0}
    shared_ptr<vector<int>[4]> r = make_shared<vector<int>[4]>({1, 2});
    // shared_ptr to a vector<int>[4], where each vector has contents {1, 2}
    — end example]
```

```
template<class T>
    shared_ptr<T> make_shared_for_overwrite();
template<class T, class A>
    shared_ptr<T> allocate_shared_for_overwrite(const A& a);
```

约束：T 不是未知边界的数组。

返回：指向类型为 T 的对象的 shared_ptr。

```
[Example 6:
    struct X { double data[1024]; };
    shared_ptr<X> p = make_shared_for_overwrite<X>();
    // shared_ptr to a default-initialized X, where each element in X::data has an indeterminate value
    shared_ptr<double[1024]> q = make_shared_for_overwrite<double[1024]>();
    // shared_ptr to a default-initialized double[1024], where each element has an indeterminate value
    — end example]
```

```
template<class T>
    shared_ptr<T> make_shared_for_overwrite(size_t N);
template<class T, class A>
    shared_ptr<T> allocate_shared_for_overwrite(const A& a, size_t N);
```

约束：T 是未知边界的数组。

返回：指向类型为 U[N] 的对象的 shared_ptr，其中 U 为 remove_extent_t<T>。

## 20.11.3.8 比较 [util.smartptr.shared.cmp]

```
template<class T, class U>
    bool operator==(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
```

返回：a.get() == b.get()。

```
template<class T>
    bool operator==(const shared_ptr<T>& a, nullptr_t) noexcept;
```

返回：!a。

```
template<class T, class U>
    strong_ordering operator<=>(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
```

返回：compare_three_way()(a.get(), b.get())。

> [Note 1: 定义比较运算符函数允许 shared_ptr 对象用作关联容器的键。 — end note]

```
template<class T>
    strong_ordering operator<=>(const shared_ptr<T>& a, nullptr_t) noexcept;
```

返回：compare_three_way()(a.get(), nullptr)。

## 20.11.3.9 特化的算法 [util.smartptr.shared.spec]

```
template<class T>
    void swap(shared_ptr<T>& a, shared_ptr<T>& b) noexcept;
```

效果：等价于 a.swap(b)。

## 20.11.3.10 转换 [util.smartptr.shared.cast]

```
template<class T, class U>
    shared_ptr<T> static_pointer_cast(const shared_ptr<U>& r) noexcept;
template<class T, class U>
    shared_ptr<T> static_pointer_cast(shared_ptr<U>&& r) noexcept;
```

强制要求：表达式 static_cast<T*>((U*)nullptr) 是良构的。

返回：
    shared_ptr<T>(R, static_cast<typename shared_ptr<T>::element_type*>(r.get()))
其中 R 为第一个重载的 r，以及第二个重载的 std::move(r)。

> [Note 1: 看似等价的表达式 shared_ptr<T>(static_cast<T*>(r.get())) 最终会导致未定义行为，尝试两次删除同一对象。 — end note]

```
template<class T, class U>
    shared_ptr<T> dynamic_pointer_cast(const shared_ptr<U>& r) noexcept;
template<class T, class U>
    shared_ptr<T> dynamic_pointer_cast(shared_ptr<U>&& r) noexcept;
```

强制要求：表达式 dynamic_cast<T*>((U*)nullptr) 是良构的。表达式 dynamic_cast<typename shared_ptr<T>::element_type*>(r.get()) 是良构的。

前提条件：表达式 dynamic_cast<typename shared_ptr<T>::element_type*>(r.get()) 具有明确定义的行为。

返回：

- 当 dynamic_cast<typename shared_ptr<T>::element_type*>(r.get()) 返回非空值 p 时，shared_ptr<T>(R, p)，其中 R 为第一个重载的 r，以及第二个重载的 std::move(r)。
- 否则，shared_ptr<T>()。

[Example 7:
    shared_ptr<double[]> p = make_shared_for_overwrite<double[]>(1024);
    // shared_ptr to a default-initialized double[1024], where each element has an indeterminate value
— end example]

# ISO/IEC 14882:2020(E)

> [Note 2: 看似等价的表达式 shared_ptr<T>(dynamic_cast<T*>(r.get())) 最终会导致未定义行为，尝试两次删除同一对象。 — end note]

```
template<class T, class U>
  shared_ptr<T> const_pointer_cast(const shared_ptr<U>& r) noexcept;
template<class T, class U>
  shared_ptr<T> const_pointer_cast(shared_ptr<U>&& r) noexcept;
```

强制要求：表达式 const_cast<T*>((U*)nullptr) 是良构的。

返回：

  shared_ptr<T>(R, const_cast<typename shared_ptr<T>::element_type*>(r.get()))

其中 R 为第一个重载的 r，以及第二个重载的 std::move(r)。

> [Note 3: 看似等价的表达式 shared_ptr<T>(const_cast<T*>(r.get())) 最终会导致未定义行为，尝试两次删除同一对象。 — end note]

```
template<class T, class U>
  shared_ptr<T> reinterpret_pointer_cast(const shared_ptr<U>& r) noexcept;
template<class T, class U>
  shared_ptr<T> reinterpret_pointer_cast(shared_ptr<U>&& r) noexcept;
```

强制要求：表达式 reinterpret_cast<T*>((U*)nullptr) 是良构的。

返回：

  shared_ptr<T>(R, reinterpret_cast<typename shared_ptr<T>::element_type*>(r.get()))

其中 R 为第一个重载的 r，以及第二个重载的 std::move(r)。

> [Note 4: 看似等价的表达式 shared_ptr<T>(reinterpret_cast<T*>(r.get())) 最终会导致未定义行为，尝试两次删除同一对象。 — end note]

## 20.11.3.11 get_deleter

[util.smartptr.getdeleter]

```
template<class D, class T>
  D* get_deleter(const shared_ptr<T>& p) noexcept;
```

返回：如果 p 拥有类型为 cv-unqualified D 的删除器 d，则返回 addressof(d)；否则返回 nullptr。返回的指针只要存在拥有 d 的 shared_ptr 实例就保持有效。

> [Note 1: 未指定指针是否在此之外保持有效更长时间。这可能发生在实现不在所有与 p 共享所有权的 weak_ptr 实例都被销毁之前销毁删除器的情况下。 — end note]

## 20.11.3.12 I/O

[util.smartptr.shared.io]

```
template<class E, class T, class Y>
  basic_ostream<E, T>& operator<<(basic_ostream<E, T>& os, const shared_ptr<Y>& p);
```

效果：如同执行：os << p.get()；

返回：os。

## 20.11.4 类模板 weak_ptr

[util.smartptr.weak]

### 20.11.4.1 通用

[util.smartptr.weak.general]

weak_ptr 类模板存储指向已被 shared_ptr 管理的对象的弱引用。要访问该对象，可以使用成员函数 lock 将 weak_ptr 转换为 shared_ptr。

```
namespace std {
  template<class T> class weak_ptr {
  public:
    using element_type = remove_extent_t<T>;

    // 20.11.4.2, 构造函数
    constexpr weak_ptr() noexcept;
    template<class Y>
      weak_ptr(const shared_ptr<Y>& r) noexcept;
    weak_ptr(const weak_ptr& r) noexcept;
```

