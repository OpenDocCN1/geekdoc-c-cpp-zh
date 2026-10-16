

这里有两种可能引发异常的来源：

- [1] **allocate()** 如果没有可用内存可能会抛出异常。
- [2] **T** 的拷贝构造函数如果无法拷贝 **val** 可能会抛出异常。

那分配器的拷贝呢？我们可以设想它会抛出异常，但标准明确要求它不会这样做（§iso.17.6.3.5）。无论如何，我编写的代码即使它真的抛出异常也不会有问题。

在这两种 **throw** 的情况下，都没有创建 **vector** 对象，因此 **vector** 的析构函数不会被调用（§13.3）。当 **allocate()** 失败时，**throw** 会在获取任何资源之前退出，所以一切正常。当 **T** 的拷贝构造函数失败时，我们已经获取了一些必须释放的内存以避免

内存泄漏。更糟的是，**T** 的拷贝构造函数可能在正确构造了几个元素之后，但在构造完所有元素之前抛出异常。这些 **T** 对象可能拥有随后会被泄漏的资源。

## Section 13.6.1 A Simple vector 377

为了解决这个问题，我们可以跟踪哪些元素已被构造，并在出错时销毁这些（且仅这些）元素：

```
template<class T, class A>
vector<T,A>::vector(size_type n, const T& val, const A& a) // elaborate implementation

:alloc{a} // copy the allocator
{
elem = alloc.allocate(n); // get memory for elements

iterator p;

try { iterator end = elem+n;
for (p=elem; p!=end; ++p)

alloc.construct(p,val); // construct element (§34.4)
last = space = p;
}
catch (...) {

for (iterator q = elem; q!=p; ++q)
alloc.destroy(q); // destroy constructed elements
alloc.deallocate(elem,n); // free memory
throw; // rethrow
}
}
```

请注意 **p** 的声明在 **try**-块之外；否则，我们将无法在 **try**-部分和 **catch**-子句中同时访问它。

这里的开销是 **try**-块的开销。在良好的 C++ 实现中，这一开销与分配内存和初始化

元素的成本相比可以忽略不计。对于进入 try-block 会产生成本的实现，在 try 之前添加一个 test if (n) 来显式处理（非常常见）的空 vector 情况可能是值得的。

该构造函数的核心部分是 std::uninitialized_fill() 实现的重复：

```
template<class For, class T>
void uninitialized_fill(For beg, For end, const T& x)
{
For p; try {
for (p=beg; p!=end; ++p)
::new(static_cast<void *>(&*p)) T(x); // construct copy of x in *p (§11.2.4) }
catch (...) {
for (For q = beg; q!=p; ++q)
(&*q)->~T(); // destroy element (§11.2.4)
throw; // rethrow (§13.5.2.1)
}
}
```

有趣的构造 &*p 负责处理不是指针的迭代器。在这种情况下，我们需要取解引用得到的元素地址来获得指针。结合显式的全局 ::new，显式转换为 void* 确保使用标准库的 placement 函数（§17.2.4）来调用构造函数，而不是为 T* 使用某个用户定义的 operator new()。vector 构造函数中的 alloc.construct() 调用只是这种 placement new 的语法糖。同样，alloc.destroy() 调用只是隐藏了显式析构（像 (&*q)->~T()）。这段代码运行在相当低的层次上，编写真正通用的代码可能很困难。

幸运的是，我们不必发明或实现 uninitialized_fill()，因为标准库提供了它（§32.5.6）。通常必须拥有要么成功完成并初始化每个元素，要么失败且不留下任何已构造元素的初始化操作。因此，标准库提供了 uninitialized_fill()、uninitialized_fill_n() 和 uninitialized_copy()（§32.5.6），它们提供强保证（§13.2）。

uninitialized_fill() 算法不保护元素析构函数或迭代器操作抛出的异常（§32.5.6）。这样做代价高昂且可能不可能。

uninitialized_fill() 算法可应用于许多种类的序列。因此，它采用前向迭代器（§33.1.2）并且无法保证按构造的逆序销毁元素。

使用 uninitialized_fill()，我们可以简化我们的构造函数：

```
template<class T, class A>
vector<T,A>::vector(size_type n, const T& val, const A& a) // still a bit messy
```

```
:alloc(a) // copy the allocator
{
 elem = alloc.allocate(n); // get memory for elements
 try {
 uninitialized_fill(elem,elem+n,val); // copy elements
 space = last = elem+n;
 }
 catch (...) {
 alloc.deallocate(elem,n); // free memory
 throw; // rethrow
 }
}
```

这比该构造函数的第一个版本有了显著改进，但下一节将演示如何进一步简化它。

构造函数会重新抛出捕获到的异常。其意图是使 vector 对异常透明，以便用户能够确定问题的确切原因。所有标准库容器都有此特性。异常透明通常是模板和其他“薄”软件层的最佳策略。这与系统的较大部分（“模块”）形成对比，后者通常需要对所有抛出的异常负责。也就是说，此类模块的实现者必须列出模块可能抛出的每个异常。实现这一点可能涉及将异常分组到层次结构中（§13.5.2）并使用 catch(...)（§13.5.2.2）。

## 13.6.2 Representing Memory Explicitly

经验表明，使用显式的 try-block 编写正确的异常安全代码比大多数人预期的要困难。事实上，这是不必要困难的，因为存在另一种选择：“资源获取即初始化”技术（§13.3）可用于减少必须编写的代码量并使代码更规范。在本例中，vector 所需的关键资源是用于保存其元素的内存。通过提供一个辅助类来表示 vector 使用的内存概念，我们可以简化代码并降低意外忘记释放它的可能性：

```
template<class T, class A = allocator<T> >
struct vector_base { // memory structure for vector
 A alloc; // allocator
 T*elem; // start of allocation
 T*space; // end of element sequence, start of space allocated for possible expansion
 T*last; // end of allocated space

 vector_base(const A& a, typename A::size_type n)
 : alloc{a}, elem{alloc.allocate(n)}, space{elem+n}, last{elem+n} { }
 ~vector_base() { alloc.deallocate(elem,last-elem); }

 vector_base(const vector_base&) = delete; // no copy operations vector_base&
 operator=(const vector_base&) = delete;
 vector_base(vector_base&&); // move operations
```

```
vector_base& operator=(vector_base&&);
```

```
};
```

只要 elem 和 last 正确，vector_base 就可以被销毁。类 vector_base 处理类型 T 的内存，而不是类型 T 的对象。因此，vector_base 的使用者必须显式地在分配的空间中构造所有对象，并在销毁 vector_base 本身之前销毁 vector_base 中所有已构造的对象。

vector_base 专为 vector 的实现的一部分而设计。很难预测一个类会被怎样使用以及在何处使用，因此我确保 vector_base 不能被拷贝，并且 vector_base 的移动也能正确转移为元素分配的内存的所有权：

```
template<class T, class A>
vector_base<T,A>::vector_base(vector_base&& a)
: alloc{a.alloc},
elem{a.elem},
space{a.space},
last{a.space}
{
a.elem = a.space = a.last = nullptr; // no longer owns any memory }
```

```
template<class T, class A>
vector_base<T,A>&& vector_base<T,A>::operator=(vector_base&& a) {
swap(*this,a); return *this; }
```

此移动赋值的定义使用 swap() 来转移为元素分配的任何内存的所有权。这里没有类型 T 的对象需要销毁：vector_base 处理内存，而将类型 T 对象的相关问题留给 vector。

有了 vector_base，vector 可以这样定义：

```
template<class T, class A = allocator<T> >
class vector {
vector_base<T,A> vb; // the data is here
void destroy_elements();
public:
using size_type = unsigned int;

explicit vector(size_type n, const T& val = T(), const A& = A());
vector(const vector& a);
vector& operator=(const vector& a);
// copy constructor // copy assignment
vector(vector&& a);
vector& operator=(vector&& a);
// move constructor // move assignment
~vector() { destroy_elements(); }
size_type size() const { return vb.space–vb.elem; } size_type capacity() const { return vb.last–vb.elem; }
void reserve(size_type); // increase capacity
```

