

## ISO/IEC 14882:2020(E)

当 T 不是数组类型时，使用 p 启用 shared_from_this。如果抛出异常，当 T 不是数组类型时调用 delete p，否则调用 delete[] p。

后置条件：use_count() == 1 && get() == p。

抛出：bad_alloc，或当无法获取内存以外的资源时抛出实现定义的异常。

```
template<class Y, class D> shared_ptr(Y* p, D d);
template<class Y, class D, class A> shared_ptr(Y* p, D d, A a);
template<class D> shared_ptr(nullptr_t p, D d);
template<class D, class A> shared_ptr(nullptr_t p, D d, A a);
```

约束：is_move_constructible_v<D> 为 true，且 d(p) 是良构表达式。对于前两个重载：

- 如果 T 是数组类型，则要么 T 是 U[N] 且 Y(*)[N] 可转换为 T*，要么 T 是 U[] 且 Y(*)[] 可转换为 T*。
- 如果 T 不是数组类型，则 Y* 可转换为 T*。

前置条件：构造 d 以及使用 std::move(d) 初始化的 D 类型删除器的构造不会抛出异常。表达式 d(p) 具有良好定义的行为且不会抛出异常。A 满足 Cpp17Allocator 要求（表 36）。

效果：构造一个 shared_ptr 对象，该对象拥有对象 p 和删除器 d。当 T 不是数组类型时，第一个和第二个构造函数使用 p 启用 shared_from_this。第二个和第四个构造函数应使用 a 的副本来分配内部使用的内存。如果抛出异常，则调用 d(p)。

后置条件：use_count() == 1 && get() == p。

抛出：bad_alloc，或当无法获取内存以外的资源时抛出实现定义的异常。

```
template<class Y> shared_ptr(const shared_ptr<Y>& r, element_type* p) noexcept;
template<class Y> shared_ptr(shared_ptr<Y>&& r, element_type* p) noexcept;
```

效果：构造一个 shared_ptr 实例，该实例存储 p 并与 r 的初始值共享所有权。

后置条件：get() == p。对于第二个重载，r 为空且 r.get() == nullptr。

> [注 1：除非 p 在 r 的所有权组被销毁之前保持有效，否则使用此构造函数会导致悬空指针。——尾注]

> [注 2：此构造函数允许创建一个存储非空指针的空 shared_ptr 实例。——尾注]

```
shared_ptr(const shared_ptr& r) noexcept;
template<class Y> shared_ptr(const shared_ptr<Y>& r) noexcept;
```

约束：对于第二个构造函数，Y* 与 T* 兼容。

效果：如果 r 为空，则构造一个空的 shared_ptr 对象；否则，构造一个与 r 共享所有权的 shared_ptr 对象。

后置条件：use_count() == r.use_count()。

抛出：当 r.expired() 时抛出 bad_weak_ptr。

```
template<class Y, class D> shared_ptr(unique_ptr<Y, D>&& r);
```

约束：Y* 与 T* 兼容，且 unique_ptr<Y, D>::pointer 可转换为 element_type*。

效果：如果 r.get() == nullptr，则等同于 shared_ptr()。否则，如果 D 不是引用类型，则等同于 shared_ptr(r.release(), r.get_deleter())。否则，等同于 shared_ptr(r.release(), ref(r.get_deleter()))。如果抛出异常，则构造函数无效果。

### 20.11.3.3 析构函数 [util.smartptr.shared.dest]

```
~shared_ptr();
```

效果：

- 如果 `*this` 为空或与另一个 shared_ptr 实例共享所有权（use_count() > 1），则没有副作用。
- 否则，如果 `*this` 拥有对象 p 和删除器 d，则调用 d(p)。
- 否则，`*this` 拥有指针 p，并调用 delete p。

> [注 1：由于 `*this` 的销毁会使与 `*this` 共享所有权的实例数量减少一，因此在 `*this` 被销毁后，所有与 `*this` 共享所有权的 shared_ptr 实例将报告的 use_count() 比其先前值少一。——尾注]

### 20.11.3.4 赋值 [util.smartptr.shared.assign]

```
shared_ptr& operator=(const shared_ptr& r) noexcept;
template<class Y> shared_ptr& operator=(const shared_ptr<Y>& r) noexcept;
```

效果：等同于 `shared_ptr(r).swap(*this)`。

返回：`*this`。

> [注 1：由临时对象的构造和销毁引起的使用计数更新不是可观察的副作用，因此实现可以通过不同方式满足效果（以及隐含的保证），而无需创建临时对象。特别是，在示例中：
> shared_ptr<int> p(new int);
> shared_ptr<void> q(p);
> p = p;
> q = p;
> 两个赋值都可以是无操作。——尾注]

```
shared_ptr& operator=(shared_ptr&& r) noexcept;
template<class Y> shared_ptr& operator=(shared_ptr<Y>&& r) noexcept;
```

效果：等同于 `shared_ptr(std::move(r)).swap(*this)`。

返回：`*this`。

```
template<class Y, class D> shared_ptr& operator=(unique_ptr<Y, D>&& r);
```

效果：等同于 `shared_ptr(std::move(r)).swap(*this)`。

返回：`*this`。

### 20.11.3.5 修改器 [util.smartptr.shared.mod]

```
void swap(shared_ptr& r) noexcept;
```

效果：交换 `*this` 与 r 的内容。

```
void reset() noexcept;
```

效果：等同于 `shared_ptr().swap(*this)`。

```
template<class Y> void reset(Y* p);
```

效果：等同于 `shared_ptr(p).swap(*this)`。

- (7.10) 当返回值所管理对象的生命周期结束时，或当数组元素的初始化抛出异常时，已初始化的元素将按照其原始构造的相反顺序销毁。
- (7.11) 当由 make_shared 初始化的非数组类型 U 的（子）对象即将被销毁时，通过表达式 pv->~U() 销毁它，其中 pv 指向该类型为 U 的对象。
- (7.12) 当由 allocate_shared 初始化的非数组类型 U 的（子）对象即将被销毁时，通过表达式 allocator_traits<A2>::destroy(a2, pv) 销毁它，其中 pv 指向该类型为 remove_cv_t<U> 的对象，类型为 A2 的 a2 是传递给 allocate_shared 的分配器 a 的重绑定副本，其 value_type 为 remove_cv_t<U>。

> [注 2：这些函数通常会分配比 sizeof(T) 更多的内存，以容纳诸如引用计数之类的内部簿记结构。——尾注]

```
template<class T, class... Args>
  shared_ptr<T> make_shared(Args&&... args);        // T 不是数组
template<class T, class A, class... Args>
  shared_ptr<T> allocate_shared(const A& a, Args&&... args);  // T 不是数组
```

约束：T 不是数组类型。

返回：一个指向类型 T 对象的 shared_ptr，其初始值为 T(forward<Args>(args)...)。

备注：这些函数调用的 shared_ptr 构造函数使用新构造的 T 类型对象的地址启用 shared_from_this。

> [示例 1：
>   shared_ptr<int> p = make_shared<int>(); // shared_ptr to int()
>   shared_ptr<vector<int>> q = make_shared<vector<int>>(16, 1);
>   // shared_ptr to vector of 16 elements with value 1
>   ——尾注]

```
template<class T> shared_ptr<T>
  make_shared(size_t N);                         // T 是 U[]
template<class T, class A>
  shared_ptr<T> allocate_shared(const A& a, size_t N);  // T 是 U[]
```

约束：T 的形式为 U[]。

返回：一个指向类型 U[N] 对象的 shared_ptr，该对象具有默认初始值，其中 U 是 remove_extent_t<T>。

> [示例 2：
>   shared_ptr<double[]> p = make_shared<double[]>(1024);
>   // shared_ptr to a value-initialized double[1024]
>   shared_ptr<double[][2][2]> q = make_shared<double[][2][2]>(6);
>   // shared_ptr to a value-initialized double[6][2][2]
>   ——尾注]

```
template<class T>
  shared_ptr<T> make_shared();                  // T 是 U[N]
template<class T, class A>
  shared_ptr<T> allocate_shared(const A& a);    // T 是 U[N]
```

约束：T 的形式为 U[N]。

返回：一个指向类型 T 对象的 shared_ptr，该对象具有默认初始值。

> [示例 3：
>   shared_ptr<double[1024]> p = make_shared<double[1024]>();
>   // shared_ptr to a value-initialized double[1024]
>   shared_ptr<double[6][2][2]> q = make_shared<double[6][2][2]>();
>   // shared_ptr to a value-initialized double[6][2][2]
>   ——尾注]

```
template<class T>
  shared_ptr<T> make_shared(size_t N,
                            const remove_extent_t<T>& u);   // T 是 U[]
```

