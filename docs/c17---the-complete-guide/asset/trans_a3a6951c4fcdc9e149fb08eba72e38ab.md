

那么下面的代码将导致未定义行为：

```
optional<X> optStr{42};
optStr.emplace(77);
std::cout << *optStr;    // undefined behavior (probably outputs 42 or 77)
```

这是因为输出操作调用了operator*，它返回payload；而emplace()中调用的placement new仅仅在payload内存中放置了一个新值，却没有使用其返回值。

对于这样的类，你必须添加一个额外的指针成员，用来保存placement new的返回值，并在需要该值时使用它：

```
template<typename T>
class optional
{
private:
    T payload;
    T* p;           // to be able to use the return value of placement new
public:
    optional(const T& t)
    : payload(t) {
        p = &payload;
    }

    template<typename... Args>
    void emplace(Args&&... args) {
        payload.~T();
        p = ::new (&payload) T(std::forward<Args>(args)...);
    }

    const T& operator*() const {
        return *p;  // don't use payload here!
    }
};
```

基于分配器的容器（如std::vector）也存在类似的问题，因为它们在内部通过分配器使用placement new。例如，像vector这样的类大致实现如下：

```
template<typename T, typename A = std::allocator<T>>
class vector
{
public:
    typedef typename std::allocator_traits<A> ATR;
    typedef typename ATR::pointer pointer;
private:
    A _alloc;        // current allocator
```

```
pointer _elems;  // array of elements
size_t _size;    // number of elements
size_t _capa;    // capacity
public:
    void push_back(const T& t) {
        if (_capa == _size) {
            reserve((_capa+1)*2);
        }
        ATR::construct(_alloc, _elems+_size, t);  // calls placement new
        ++_size;
    }

    T& operator[] (size_t i){
        return _elems[i];  // UB for replaced elements with constant members
    }
    ...
};
```

再次注意，ATR::construct()不会返回所调用的placement new的返回值。因此，我们不能用这个返回值来代替_elems。

请注意，这仅仅是从C++11开始才成为问题。在C++11之前，使用带有常量成员的元素要么不可能（std::vector），要么不被正式支持，因为元素必须是可复制构造（CopyConstructible）和可赋值（Assignable）的（尽管像list这样基于节点的容器对于具有const成员的元素完全正常工作）。然而，随着C++11引入移动语义，带有常量成员的元素（如上文的类X）得到了支持，并导致了这种未定义行为。

引入std::launder()的目的是解决这些问题。然而，正如我将在下面描述的，事实证明我们根本无法用std::launder()解决vector的问题。

## 32.2 launder()如何解决问题

C++标准委员会的核心工作组决定通过引入std::launder()来解决这个问题，如下所示（参见 http://wg21.link/cwg1776）：如果你有一个指针，由于底层内存已被替换，对其访问属于未定义行为：

```
struct X {
    const int n;
    double d;
};
X* p = new X{7, 8.8};
new (p) X{42, 9.9};    // request to place a new value into p
int i = p->n;          // undefined behavior (i is probably 7 or 42)
auto d = p->d;         // also undefined behavior (d is probably 8.8 or 9.9)
```

你可以在使用指针时调用std::launder()，以确保对底层内存进行重新求值：

```
int i = std::launder(p)->n;  // OK, i is 42
```

```
auto d = std::launder(p)->d;  // OK, d is 9.9
```

请注意，launder()并不能修复之后使用p时的问题，它只解决它所使用的特定表达式中的问题：

```
int i2 = p->n;                 // still undefined behavior
```

任何时候访问调用了placement new的数据，都必须使用std::launder()。

对于前面引入的optional之类的类，可以这样实现：

```
template<typename T>
class optional
{
    private:
        T payload;
    public:
        optional(const T& t)
            : payload(t) {
        }

        template<typename... Args>
        void emplace(Args&&... args) {
            payload.~T();
            ::new (&payload) T(std::forward<Args>(args)...); // *
        }

        const T& operator*() const {
            return *(std::launder(&payload));  // OK
        }
};
```

请注意，我们必须确保对原始payload的每次访问都要经过std::launder()的“洗白”处理，就像这里operator*所做的那样。

## 32.3 为什么/何时launder()不起作用

然而，对于像vector这样基于分配器的容器，该解决方案并不奏效。这是因为如果我们尝试这样做：

```
template<typename T, typename A = std::allocator<T>>
class vector
{
    public:
        typedef typename std::allocator_traits<A> ATR;
        typedef typename ATR::pointer pointer;
    private:
        A _alloc;        // current allocator
        pointer _elems;  // array of elements
```

```
size_t _size;    // number of elements
size_t _capa;    // capacity
public:
    void push_back(const T& t) {
        if (_capa == _size) {
            reserve((_capa+1)*2);
        }
        ATR::construct(_alloc, _elems+_size, t);  // calls placement new
        ++_size;
    }

    T& operator[] (size_t i){
        return std::launder(_elems)[i];  // OOPS, still UB
    }
    ...
};
```

在operator[]中调用launder()并没有帮助，因为指针可能是一个智能指针（即类类型），而对于智能指针，launder()没有效果。¹

尝试 std::launder(this)->_elems[i]; 也不起作用，因为launder()只适用于指向生命周期已结束对象的指针。²

因此，如果你拥有带常量/引用成员的元素，std::launder()并不能解决基于分配器的容器中避免未定义行为的问题。看来需要一个通用的核心修复方案（参见我的论文 http://wg21.link/p0532）。

## 32.4 后续说明

std::launder()是作为C++14的国家机构评论的结果而引入的（参见 http://wg21.link/n3903），并首次作为核心工作组问题1776进行讨论（参见 http://wg21.link/cwg1776）。作为解决方案，它最早由Richard Smith和Hubert Tong在 http://wg21.link/n4303 中提出。最终被接受的措辞由Richard Smith在 http://wg21.link/p0137r1 中拟定。

# 33.2 std::bool_constant<>

还要注意，调用函数模板需要显式实例化。如果print()是一个模板：

```
```cpp
template<typename T>
void print(const T &coll)
{
    std::cout << "elems: ";
    for (const auto& elem : coll) {
        std::cout << elem << ' ';
    }
    std::cout << '\n';
}
```
```

那么你必须以显式指定的模板参数来传递对它的调用：

> // ERROR: can't deduce template parameter T
> call(print, vals);

```
call(print<std::vector<int>>, vals); // OK
```

最后，请注意，根据移动语义的规则，返回调用结果需要decltype(auto)来完美地将返回值返回给调用者：

```
```cpp
template<typename Callable, typename... Args>
decttype(auto) call(Callable&& op, Args&&... args)
{
    return std::invoke(std::forward<Callable>(op),   // call passed callable with
        std::forward<Args>(args)...); // all additional passed args
}
```
```

## 33.2 std::bool_constant<>

如果trait产生布尔值，它们现在使用别名模板bool_constant<>：

```
```cpp
namespace std {
    template<bool B>
    using bool_constant = integral_constant<bool, B>; // since C++17
    using true_type = bool_constant<true>;
    using false_type = bool_constant<false>;
}
```
```

在C++17之前，你必须直接使用integral_constant<>，这意味着true_type和false_type定义如下：

```
```cpp
namespace std {
    using true_type = integral_constant<bool, true>;
    using false_type = integral_constant<bool, false>;
}
```
```

尽管如此，布尔trait通常应该在特定属性适用时继承std::true_type，在不适用时继承std::false_type。例如：

