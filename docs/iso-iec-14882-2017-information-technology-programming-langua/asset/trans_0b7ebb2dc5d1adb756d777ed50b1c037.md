

# ISO/IEC 14882:2017(E)

表 31 — 分配器 realloc (续)

| 表达式 | 返回类型 | 断言/注 前/后条件 | 默认值 |
|---|---|---|--|
| *q | const T& | *q 指向与 *p 相同的对象 | |
| p->m | T::m 的类型 | *p 需要: (*p).m 是定义良好的，等同于 (*p).m。 | |
| q->m | T::m 的类型 | *q 需要: (*q).m 是定义良好的，等同于 (*q).m。 | |
| static_cast<X::pointer>(w) | | static_cast<X::pointer>(w) == p | |
| static_cast<I::const_pointer<>()>> | X::const_pointer | static_cast<X::const_pointer>(x) == q | |
| pointer_traits<X::pointer<r>>::a.allocate(n) | X::pointer | 为类型为 T 的对象分配了内存但未进行构造。allocate可能会抛出适当异常。175 [注：如果 n == 0，则返回值未定义——注] | |
| a.allocate(n, y) | X::pointer | 与 a.allocate(n) 相同。y 的使用未定义，但其目的是辅助局部性。 | |
| a.deallocate(p,n) | (未使用) | 需要: p 应当由早先调用 allocate 返回的值，且未被中间的 deallocate 调用失效。a 应与传递给 allocate 以获取此内存的值匹配。抛出：可以有意义地传递给 X::allocate() 的最大值 | |
| a.max_size() | X::size_type | numeric_limits<size>::max() / sizeof(value_type) | |
| a1 == a2 | bool | 仅当从每个分配器分配的内存可以通过另一个释放时，返回 true。operator== 应当具有自反、对称性，且不应通过异常退出。175 设计意图是 a.allocate 是分配单个类型为 T 的对象的手段，即使 sizeof(T) 很小。也就是说，容器不需要维护其空闲列表 § 20.5.3.5 |

# ISO/IEC 14882:2017(E)

表 31 — 分配器 requires (续)

| 表达式 | 返回类型 | 断言/注 前/后条件 | 默认值 |
|---|---|---|---|
| a1 != a2 | bool | 等于 !(a1 == a2) | |
| a == b | bool | 等于 a == b Y::rebind<DP>::other(b) | |
| a != b | bool | 等于 (a == b) 不应通过异常退出。后条件：u == a | |
| X(u); | | 不应通过异常退出。后条件：Y(u) = b, u == X(b) | |
| u = a; | | 不应通过异常退出。后条件：u 等于 a 的先决值。 | |
| U(b); | | 不应通过异常退出。后条件：u 等于 X(b) 的先决值。 | |
| X(std::move(a)); | | 不应通过异常退出。后条件：u 等于 a 的先决值。 | |
| X(std::move(b)); | | 不应通过异常退出。后条件：u 等于 X(b) 的先决值。 | |
| a.construct(c, args) | (未使用) | 影响：在 ::new(void*) 构造对象 c C(forward<Args>(args)) | |
| a.destroy(c) | (未使用) | 影响：销毁 c 处的对象。通常返回错误或 X() | |
| X::propagate_on_copy_assignment | 等于或派生自 type_type 或 false_type | 如果客户端容器执行拷贝赋值时，应拷贝类型为 X 的分配器，则为 true_type。参见见下文注。 | false_type |
| X::propagate_on_move_assignment | 等于或派生自 type_type 或 false_type | 如果客户端容器执行移动赋值时，应移动类型为 X 的分配器，则为 true_type。参见见下文注。 | false_type |
| X::propagate_on_container_swap | 等于或派生自 type_type 或 false_type | 当客户端容器交换时，应交换类型为 X 的分配器，则为 true_type。参见见下文注。 | false_type |
| X::is_always_equal | 等于或派生自 type_type 或 false_type | 如果该表达式对于类型为 X 的两个（可能的）值 a1, a2 保证为真。 | is_same<X>::type |

注：上表中的成员类模板 rebind 实际上是一个类型定义模板。[注：一般情况下，如果名称 Allocator 是 SomeAllocator<T>，那么 Allocator::rebind<U>::other 与 SomeAllocator<T>::value_type 是相同类型，后者是 T 而 SomeAllocator<U>:: § 20.5.3.5 |

# ISO/IEC 14882:2017(E)

value_type 是 U. ... 注结束；如果 Allocator 是某些 SomeAllocator<T, Args> 的类实例化，其中 Args 是零个或多个类型参数，且 Allocator 未提供重绑定成员模板，则对于不是上述模板实例化的分配器，使用 allocator_traits 模板 SomeAllocator<U, Args> 代替 Allocator::rebind<U>，无默认值。

注 B：如果 X::`propagate_on_copy` 为真，则拷贝操作不应抛出异常。如果 X::`propagate_on_move` 为真，则移动操作满足 Moveable 要求（表 25）。如果 X::`propagate_on_swap` 为真，则交换操作不应抛出异常并满足 (20.5.3.2)。

分配器类型 X 满足 Constructible (20.5.3.1) 要求。X::pointer、X::const_pointer 和 X::const 类型满足 NullPointer (20.5.3.3) 要求。对这些类型的构造函数、函数、拷贝操作、移动操作或操作均可能通过异常退出。X::pointer 和 X::const_pointer 应当满足随机访问迭代器 (27.2.7) 和连续迭代器 (27.2.1) 的要求。

6 如果（可能不同的）类型 X::pointer、X::const_pointer 或 X::const_pointer 的对象 x1 和 x2 是等值的值，当且仅当 x1 和 x2 都能显式转换为类型为 X::const_ 的版本 pr1 和 pr2（且仅使用这四种类型），且表达式 pr1 == pr2

7 如果类型为 X::pointer 的对象 x1 和 x2。那么对于以下表达式

a1 == a2
a1 != a2
a == b
a != b
X(u);
u = a;
U(b);
X(std::move(a));
X(std::move(b));
a.construct(c, args)
a.destroy(c)
X::propagate_on_copy_assignment
X::propagate_on_move_assignment
X::propagate_on_container_swap
X::is_always_equal

9 如果关联类型的分配器未被分配器支持，分配器的实例化可能会失败。示例：以下支持最小接口的分配器：

```:
template <class T>
struct SimpleAllocator {
  typedef T value_type;
  SimpleAllocator(const T&);
  SimpleAllocator(const SimpleAllocator&);
  T* allocate(size_type n);
  void deallocate(T* p, size_type n);
  void construct(T* c, const Args&... args);
  void destroy(T* c);
};
```

10 如果关联类型的分配器未被分配器支持，分配器的实例化可能会失败。[注：分配器可能会静忽略忽略请求的对齐。]

