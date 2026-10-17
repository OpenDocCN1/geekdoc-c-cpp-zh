
`scoped_allocator_adaptor& operator=(scoped_allocator_adaptor&&) = default;`

- `scoped_allocator_adaptor()`;


```cpp
inner_allocator_type inner_allocator() noexcept;

const inner_allocator_type inner_allocator() const noexcept;

outer_allocator_type outer_allocator() noexcept;

const outer_allocator_type outer_allocator() const noexcept;
```

```cpp
pointer allocate(size_type n, const void_pointer hint);

void deallocate(pointer p, size_type n);

size_type max() const;
```

### 23.13.4 作用域分配器成员 [allocator.adapter.members]

`inner_allocator_type inner_allocator();`
影响：初始化 `scoped_allocator_adaptor` 对象。

```cpp
template <class T, class... Args>
void construct(T* p, Args&&... args);
```

# ISO/IEC 14882:2017(E)

`v<T1, Arg1..., inner_allocator_type&>` 为真，则 `xprime` 为：
`tuple<std::move(x), tuple<inner_allocator_type&>(inner_allocator())>`

否则，程序是非良的。
通过以下规则构造一个元组对象 `y`：

- 如果 `uses_allocator_v<T2>`，`inner_allocator_type&` 为 false 且 `is_constructible<T2, Arg2..>` 为真，则 `yprime` 为 `y`。

- 否则，如果 `uses_allocator_v<T2>`，`inner_allocator_type&` 为 true 且 `is_constructible<T2, allocator_arg_t, inner_allocator_type&, Arg2..>` 为真，则 `yprime` 为：
`tuple<allocator_arg, inner_allocator_type&>(allocator_arg, inner_allocator()), std::move(y)>`

- 否则，如果 `uses_allocator_v<T2>`，`inner_allocator_type&` 为 true 且 `is_constructible<T2, Arg2.., ..., inner_allocator_type&>` 为真，则 `yprime` 为 `ntuple<std::move(y), tuple<inner_allocator_type&>()>()`

否则，程序是非良的。
然后调用：
`OUTERNMOST_TRAITS(*this)::construct(OUTERNMOST*(this), p, piecewise_construct, std::move(xprime), std::move(yprime))`

```cpp
template <class T1, class T2>
void construct(pair<T1, T2*>* p);
```

等价于：
`construct(p, piecewise_construct, tuple<>(), tuple<U>());`

```cpp
template <class T1, class T2, class U, class V>
void construct(pair<T1, T2*>* p, const U& x, V& y);
```

等价于：
`construct(p, piecewise_construct, forward_as_tuple(std::forward<U>(x)), forward_as_tuple(std::forward<V>(y)));`

等价于：
`construct(p, piecewise_construct, forward_as_tuple(x.first), forward_as_tuple(x.second));`

```cpp
template <class T1, class T2, class U, class V>
void construct(pair<T1, T2*>* p, pair<U, V>& x);
```

等价于：
`construct(p, piecewise_construct, forward_as_tuple(std::forward<U>(x.first)), forward_as_tuple(std::forward<V>(x.second)));`

```cpp
template <class T>
void destroy(T* p);
```

# ISO/IEC 14882:2017(E)

16 效果：调用 `OUTERMOST_ALLOC_TRAITS(*this)~:destroy(OUTERNMOST(*this), p)`。

17 `scoped_allocator_adaptor select_on_container_type_construction() const;`
返回：一个新的 `scoped_allocator_adaptor`，其中适配器中的每个分配器 `A` 都通过调用对应于 `*this` 的分配器的 `allocator_traits<A>::select_on_container_type_construction()` 来初始化。

## 23.13.5 作用域分配器运算符 [scoped.adaptor.operators]

```cpp
template <class Outer1, class Outer2, class InnerLocs>
bool operator()=(const scoped_allocator_adaptor<Outer1, InnerLocs..>&& a,
               const scoped_allocator_adaptor<Outer2, InnerLocs..>&& b) noexcept {
// 1 返回：如果 (InnerLocs) 为零，
//    a.allocator() == b.allocator();
//    否则
//    a.allocator() == b.allocator() && a.inner_allocator() == b.inner_allocator()
}
```

```cpp
template <class Outer1, class Outer2, class InnerLocs>
bool operator()=(const scoped_allocator_adaptor<Outer1, InnerLocs..>&& a,
               const scoped_allocator_adaptor<Outer2, InnerLocs..>&& b) noexcept;
```

## 23.14 函数对象 [function.objects]

1 函数对象是一种对象类型（6.9），可以作为函数调用中后缀表达式的类型（8.2.2, 16.3.1）。
2 函数是对象类型对象。在通常期望向算法模板传递函数指针的地方（第 28 节），接口规定为接受函数对象。这不仅使得算法模板能够处理函数指针，还使它们能够处理任意函数对象。

## 23.14.1 头文件 <functional> 概要 [function.syn]

```cpp
namespace {
// 23.14.4. invoke
template <class F, class... Args>
invoke_result<F, Args...> invoke(F&& f, Args&&... args)
  noexcept(is_not_invocable_v<F, Args...>);
// 23.14.5. reference_wrapper
template <class T> reference_wrapper<T>
  reference_wrapper(const T&) noexcept;
template <class T> T& ref(const T&) const noexcept;
template <class T> void ref(const T&&) = delete;
template <class T> T& ref(const reference_wrapper<T>&) const;
template <class T> void ref(const reference_wrapper<T>&) = delete;
// 23.14.6. 算术运算
template <class T = void> struct plus {
// 这种类型是函数指针或具有成员 operator() 的类
template <class T = void> struct minus;
template <class T = void> struct multiplies;
template <class T = void> struct divides;
template <class T = void> struct modulus;
};
// 23.14.7. 比较
template <class T = void> struct equal_to;
template <class T = void> struct not_equal_to;
template <class T = void> struct greater;
template <class T = void> struct less;
template <class T = void> struct greater_equal;
template <class T = void> struct less_equal;
};
// 23.14.8. 逻辑运算
template <class T = void> struct logical_and;
template <class T = void> struct logical_or;
template <class T = void> struct logical_not;
template <class T = void> struct logical_and_not;
template <class T = void> struct logical_or_not;
template <class T = void> struct logical_not_not;
// 23.14.9. 逐位运算
template <class T = void> struct bit_and;
template <class T = void> struct bit_or;
template <class T = void> struct bit_xor;
template <class T = void> struct bit_not;
template <class T = void> struct bit_and_not;
template <class T = void> struct bit_xor_not;
template <class T = void> struct bit_not_not;
// 23.14.10. 函数模板 not_fn
template <class F> auto not_fn(F&);
// 23.14.11. bind
template<class T> struct is_bind_expression;
template<class T> struct is_placeholder;
template<class F, class... BoundArgs>
auto bind(F&, BoundArgs&...);
template<class R, class F, class... BoundArgs>
R bind(F&, BoundArgs&...);
}
```

```cpp
namespace placeholders {
    // M 是实现定义的占位符数量
    // 见下方 _1;
    // 见下方 _2;
    ...
    // 见下方 _M;
}
```

```cpp
// 23.14.12. 成员函数适配器
template<class R, class D> auto mem_fn(R T::*) noexcept;
template<class T> struct bad_function_call;
template<class T> class function; // 未定义
template<class R, class... ArgTypes> class function<R(ArgTypes...)>;
template<class R, class... ArgTypes>
void swap(function<R(ArgTypes...)>&) noexcept;
template<class R, class... ArgTypes>
auto operator*(const function<R(ArgTypes...)>&, void*) noexcept;
template<class R, class... ArgTypes>
auto operator*(void*, const function<R(ArgTypes...)>&) noexcept;
```

```cpp
// 23.14.11. 搜索器
template<class ForwardIterator, class BinaryPredicate = equal_to<>>
class default_searcher;
template<class RandomAccessIterator>
class Hash = hashtype<typename iterator_traits<RandomAccessIterator>::value_type,
             class BinaryPredicate = equal_to<>>
class boyer_more_horspool_searcher;
```

```cpp
// 23.14.10. 哈希函数主模板
template<class T>
struct hash;
```

```cpp
// 23.14.11. 函数对象绑定
template<class T>
inline constexpr bool is_bind_expression_v = is_bind_expression<T>;
template<class T>
inline constexpr bool is_placeholder_v = is_placeholder<T>;
```

# ISO/IEC 14882:2017(E)

1 示例：如果 C++ 程序想要两个包含 double 的 vector a 相加并将结果放入 a，可以这样做：

`transform(a.begin(), a.end(), a.begin(), plus<double>());`

2 示例：对反的每一个元素：

`transform(a.begin(), a.end(), negate<double>());`

# ISO/IEC 14882:2017(E)

## 23.14.2 定义 [func.def]

1 下定义适用于此：

2 调用签名是返回类型的名称，后跟一个圆括的、逗号分隔的参数类型列表。

3 可调用类型是函数对象（23.14）或成员指针。

4 可调用对象是可调用类型的对象。

5 包装类型是持有可调用对象并支持转发到该对象的调用操作的类型。

6 包装对象是包装类型的对象。

## 23.14.3 要求 [func.require]

1 定义 `INVOKEF(f, t1, ..., tN)` 如下：

(1.1) `(t1).*f(t2, ..., tN)` 如果 `f` 是指向类 `T` 成员的指针且 `base_of_v<T, decay_t<type(t1)>>` 为真；

(1.2) `(t1).get(t2, ..., tN)` 如果 `f` 是指向类 `T` 成员的指针且 `decay_t<type(t1)>` 是 `reference_wrapper` 的特化；

(1.3) `(*t1).*f(t2, ..., tN)` 如果 `f` 是指向类 `T` 成员的指针且 `t1` 不满足以下两个：

(1.4) `(*t1).*f` 如果 `N == 1` 且 `f` 是指向类 `T` 数据成员的指针且 `base_of_v<T, decay_t<type(t1)>>` 为真；

(1.5) `(t1).get()` 如果 `N == 1` 且 `f` 是指向类 `T` 数据成员的指针且 `t1` 不满足以下两个：

(1.6) `f(t1, t2, ..., tN)`，所有其他情况下。

2 定义 `INVOKER(f, t1, ..., tN)` 为 `static_cast<void>(INVOKEF(f, t1, ..., tN))` 如果 `R` 为 void；否则 `INVOKEF(f, t1, ..., tN)` 隐式转换为 `R`。

3 每个可调用对象（23.14）必须是可构造的。转发可调用对象是一个可以使用任意参数列表调用并将对象的参数定义为引用的包装类。这种转发调用应确保右值参数被传递为右值引用，左值参数被传递为左值引用。简单包装器是可拷贝且可赋值的转发包装器，且其拷贝构造函数、移动构造函数和赋值运算符不抛出异常。

# ISO/IEC 14882:2017(E)

`template<class... UnboundArgs>`
