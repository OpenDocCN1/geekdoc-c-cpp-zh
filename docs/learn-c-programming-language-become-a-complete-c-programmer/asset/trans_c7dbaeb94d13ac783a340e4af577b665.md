

奇怪的 **rebind** 模板是一个古老的别名。它本应是这样：

```cpp
template<typename U>
using other = allocator<U>;
```

然而，**allocator** 是在 C++ 支持此类别名之前定义的。提供它是为了让分配器能够分配任意类型的对象。考虑：

```cpp
using Link_alloc = typename A::template rebind<Link>::other;
```

如果 **A** 是一个 **allocator**，那么 **rebind<Link>::other** 就是 **allocator<Link>** 的别名。例如：

```cpp
template<typename T, typename A = allocator<T>>
class list {
private:

class Link { /* ... */ };
using Link_alloc = typename A::template rebind<Link>::other; // allocator<Link>
Link_alloc a; // link allocator
A alloc; // list allocator
// ...
};
```

还提供了一个更受限制的 **allocator<T>** 特化版本：

```cpp
template<>
class allocator<void> {
public:

typedef void * pointer;
typedef const void* const_pointer;
typedef void value_type;
template<typename U> struct rebind { typedef allocator<U> other; };
};
```

这使我们能够避免特殊情况：只要不去解引用它的指针，我们就可以提及 **allocator<void>**。

## 34.4.2 分配器特性

分配器通过 **allocator_traits** “连接在一起”。分配器的某个属性，比如它的 **pointer** 类型，可以在其特性中找到：**allocator_traits<X>::pointer**。和往常一样，使用特性技术是为了让我能够为一个没有符合分配器要求的成员类型的类型（如 **int**）以及一个在设计时完全没有考虑分配器的类型构建分配器。

基本上，**allocator_traits** 为常用的类型别名和分配器函数集合提供了默认实现。与默认的 **allocator**（§34.4.1）相比，**address()** 缺失了，而 **select_on_container_copy_construction()** 被添加进来：

```cpp
template<typename A> // §iso.20.6.8
struct allocator_traits {
using allocator_type = A;
using value_type = A::value_type;
using pointer = value_type; // trick
using const_pointer = Pointer_traits<pointer>::rebind<const value_type>; // trick
using void_pointer = Pointer_traits<pointer>::rebind<void>; // trick
using const_void_pointer = Pointer_traits<pointer>::rebind<const void>; // trick
using difference_type = Pointer_traits<pointer>::difference_type; // trick
using size_type = Make_unsigned<difference_type>; // trick
using propagate_on_container_copy_assignment = false_type; // trick
using propagate_on_container_move_assignment = false_type; // trick
using propagate_on_container_swap = false_type; // trick

template<typename T> using rebind_alloc = A<T,Args>; // trick
template<typename T> using rebind_traits = allocator_traits<rebind_alloc<T>>;
static pointer allocate(A& a, size_type n) { return a.allocate(n); } // trick
static pointer allocate(A& a, size_type n, const_void_pointer hint) // trick
{ return a.allocate(n,hint); }
static void deallocate(A& a, pointer p, size_type n) { a.deallocate(p, n); } // trick

template<typename T, typename ... Args>
static void construct(A& a, T* p, Args&&... args) // trick
{ ::new (static_cast<void*>(p)) T(std::forward<Args>(args)...); }

template<typename T>
static void destroy(A& a, T* p) { p->~T(); } // trick

static size_type max_size(const A& a) // trick
{ return numeric_limits<size_type>::max(); }
static A select_on_container_copy_construction(const A& rhs) { return rhs; } // trick
};
```

“技巧”是指如果分配器 A 中存在对应的成员，则使用它；否则，使用这里指定的默认实现。对于 **allocate(n,hint)**，如果 A 没有接受提示参数的 **allocate()**，则调用 **A::allocate(n)**。**Args** 是 A 所需的任何类型参数。

我并不喜欢在标准库的定义中使用这种技巧，但在 C++ 中，通过自由使用 **enable_if()**（§28.4）可以实现这一点。为了使声明可读，我假设了一些类型别名。

## 34.4.3 指针特性

分配器使用 **pointer_traits** 来确定指针和指针代理类型的属性：

```cpp
template<typename P> // §iso.20.6.3
struct pointer_traits {
    using pointer = P;
    using element_type = T; // trick
    using difference_type = ptrdiff_t; // trick

    using pointer = typename Tr::pointer;
    using const_pointer = typename Tr::const_pointer;
    using void_pointer = typename Tr::void_pointer;
    using const_void_pointer = typename Tr::const_void_pointer;
    using propagate_on_container_copy_assignment = /* 见 §iso.20.12.2*/;
    using propagate_on_container_move_assignment = /* 见 §iso.20.12.2*/;
    using propagate_on_container_swap = /* 见 §iso.20.12.2*/;

    // ...
};
```

对于分配 **vector\<string\>**，我们有四种选择：

```cpp
// vector 和 string 使用各自的（默认）分配器：
using svec0 = vector<string>;
svec0 v0;

// 只有 vector 使用 My_alloc，而 string 使用它自己的分配器（默认分配器）：
using Svec1 = vector<string, My_alloc<string>>;
Svec1 v1 {My_alloc<string>{my_arena1}};

// vector 和 string 都使用 My_alloc（如上）：
using Xstring = basic_string<char, char_traits<char>, My_alloc<char>>;
using Svec2 = vector<Xstring, scoped_allocator_adaptor<My_alloc<Xstring>>>;
Svec2 v2 {scoped_allocator_adaptor<My_alloc<Xstring>>{my_arena1}};

// vector 使用它自己的分配器（默认分配器），而 string 使用 My_alloc：
using Xstring2 = basic_string<char, char_traits<char>, My_alloc<char>>;
using Svec3 = vector<Xstring2, scoped_allocator_adaptor<My_alloc<Xstring2>, My_alloc<char>>>;
Svec3 v3 {scoped_allocator_adaptor<My_alloc<Xstring2>, My_alloc<char>>{my_arena1}};
```

显然，第一种变体 **Svec0** 将是迄今为止最常见的，但对于有严重内存相关性能约束的系统，其他版本（尤其是 **Svec2**）可能很重要。再多几个别名会让这段代码更易读一些，不过好在这不是你每天都要写的代码。

**scoped_allocator_adaptor** 的定义有些复杂，但基本上它是一个与默认 **allocator**（§34.4.1）非常相似的分配器，同时还跟踪其“内部”分配器，以便传递给包含的容器（如 **string**）使用：

**scoped_allocator_adaptor\<OuterA,InnerA\>**（简化版，§iso.20.12.1）

| 表达式 | 描述 |
|---|---|
| `rebind<T>::other` | 一个为此分配器分配 `T` 类型对象的版本的别名 |
| `x=a.inner_allocator()` | `x` 是内部分配器；noexcept |
| `x=a.outer_allocator()` | `x` 是外部分配器；noexcept |
| `p=a.allocate(n)` | 为 **value_type** 的 `n` 个对象获取空间 |
| `p=a.allocate(n,hint)` | 为 **value_type** 的 `n` 个对象获取空间；`hint` 是给分配器的实现相关的帮助；通常，`hint` 是指向某个对象的指针，我们希望 `*p` 靠近该对象 |
| `a.deallocate(p,n)` | 释放 **p** 所指向的 **n** 个 **value_type** 对象的空间 |
| `n=a.max_size()` | n 是可分配元素的最大可能数量 |
| `t=a.construct(args)` | 从 **args** 构造一个 **value_type**：`t=new(p) value_type{args}` |
| `a.destroy(p)` | 销毁 *p：`p->~value_type()` |

## 34.5 垃圾回收接口

垃圾回收（自动回收未被引用的内存区域）有时被描述为万能良药。但它并非如此。特别是，非纯内存的资源可能会被垃圾回收器泄漏，例如文件句柄、线程句柄和锁。在我看来，在用尽常用的防止泄漏的技术之后，垃圾回收是一种方便的最后的补救手段：

- [1] 只要可能，就使用具有适当语义的资源句柄。标准库提供了 **string**、**vector**、**unordered_map**、**thread**、**lock_guard** 等。移动语义使得这类对象能够从函数中高效地返回。
- [2] 使用 **unique_ptr** 来持有那些不隐式管理自身资源的对象（例如指针）、需要防止过早删除的对象（因为它们没有正确的析构函数）、或者需要以需要特别关注的方式（删除器）分配的对象。
- [3] 使用 **shared_ptr** 来持有需要共享所有权的对象。

如果始终如一地使用，这一系列技术可以确保没有泄漏（也就是说，不需要垃圾回收，因为不会产生垃圾）。然而，在大量的现实世界程序中，这些技术（都基于 RAII；§13.3）并没有被始终如一地使用，也难以轻易应用，因为它们涉及大量以不同方式结构化的代码。这些“不同方式”通常涉及复杂的指针使用、裸露的 **new** 和 **delete**、模糊资源所有权的显式类型转换，以及类似的易出错的低级技术。在这种情况下，垃圾回收器是一种合适的最后手段。即使它不能处理非内存资源，它也可以回收/循环利用内存。甚至不要考虑使用在回收时调用的通用“终结器”来处理非内存资源。垃圾回收器有时可以显著延长泄漏系统的运行时间（即使是泄漏非内存资源的系统）。例如，对于一个每天晚上停机维护的系统，垃圾回收器可能将资源耗尽的时间从几小时延长到几天。此外，垃圾回收器还可以被插桩以查找泄漏源。

值得记住的是，垃圾回收系统也可能有自己变体的泄漏。例如，如果我们将一个指向对象的指针放入哈希表却忘记了它的键，那么这个对象实际上已经被泄漏了。类似地，被一个无限线程引用的资源可能永远存活，即使该线程本不应该是无限的（例如，它可能在等待输入）。

