
**`tuple_element<N,T>::type`** **`first`** 的类型（如果 `N==0`）或 **`second`** 的类型（如果 `N==1`） **`get<N>(p)`** **`pair`** `p` 的第 `N` 个元素的引用；`N` 必须为 **`0`** 或 **`1`** **`make_pair`** 函数避免了显式提及 **`pair`** 的元素类型。例如：`auto p =`

```
make_pair("Harvard",1736);
```

# 34.2.4.2 tuple

在 `<tuple>` 中，标准库提供了类 **`tuple`** 和各种支持设施。**`tuple`** 是任意类型的 `N` 个元素的序列：

```
template<typename... Types>
class tuple {
public:

// ...
};
```

元素数量为零或正数。

有关 **`tuple`** 设计、实现和使用的详细信息，请参阅 §28.5 和 §28.6.4。

## `tuple<Types...>` Members (§iso.20.4.2) (continues)

- `tuple t {};`

- `tuple t {args};`

- `tuple t {t2};`

- `tuple t {p};`

默认构造函数：空 **`tuple`**；constexpr **`t`** 对 **`args`** 的每个元素有一个元素；显式 从 **`tuple t2`** 构造

从 **`pair p`** 构造

### 第 34.2.4.2 节 **`tuple`** 985

## `tuple<Types...>` Members (continued) (§iso.20.4.2)

```
tuple t {allocator_arg_t,a,args}; tuple t {allocator_arg_t,a,t2}; tuple t {allocator_arg_t,a,p}; t. tuple()
t=t2
t=move(t2)
t=p
t=move(p)
t.swap(t2)
```

使用分配器 **`a`** 从 **`args`** 构造 使用分配器 **`a`** 从 **`tuple t2`** 构造

使用分配器 **`a`** 从 **`pair p`** 构造 析构函数：销毁每个元素

**`tuples`** 的拷贝赋值

**`tuples`** 的移动赋值

**`pair p`** 的拷贝赋值

**`pair p`** 的移动赋值

交换 **`tuples t`** 和 **`t2`** 的值；noexcept

**`tuple`** 的类型和 `=` 的操作数以及 **`swap()`** 等的参数 *不* 需要相同。操作是有效的当且仅当元素上的隐含操作有效。例如，我们可以将一个 **`tuple`** 赋给另一个 **`tuple`**，如果被赋值的 **`tuple`** 的每个元素都可以赋给目标元素。例如：

```
tuple<string,vector<double>,int> t2 = make_tuple("Hello, tuples!",vector<int>{1,2,3},{'x'});
```

操作如果所有元素操作都是 noexcept 则为 noexcept，且操作

仅当成员操作抛出时才抛出。同样，tuple 操作如果元素操作是 constexpr 则为 constexpr。

一对操作数（或参数）中每个 tuple 的元素数量必须相同。请注意，一般 tuple 构造函数是显式的。特别是，这不起作用：

```
tuple<int,int,int> rotate(tuple<int,int,int> t)
{
return {t.get<2>(),t.get<0>(),t.get<1>()}; // error :explicit tuple constructor
}
auto t2 = rotate({3,7,9}); // error :explicit tuple constructor
```

如果您只需要两个元素，可以使用 pair：

```
pair<int,int> rotate(pair<int,int> p)
{
return {p.second,p.first};
}
auto p2 = rotate({3,7});
```

更多示例请参阅 §28.6.4。

## `tuple<Types...>` Helpers (§iso.20.4.2.4, §iso.20.4.2.9) (continues) `t=make_tuple(args)`

从 args 制作 tuple

`t=forward_as_tuple(args)` `t` 是对 `args` 中元素的右值引用的 tuple，因此您可以将 arg 的元素通过 `t` 转发 `t=tie(args)` `t` 是对 `args` 中元素的左值引用的 tuple，因此您可以通过 `t` 将元素赋给 `args` 的元素

## `tuple<Types...>` Helpers (continued) (§iso.20.4.2.4, §iso.20.4.2.9)

`t=tuple_cat(args)` 拼接 tuples：args 是一个或多个 tuples；`t` 具有 args 中 tuples 的成员按顺序

`tuple_size<T>::value` tuple `T` 的元素数量

`tuple_elements<N,T>::type` tuple `T` 的第 `N` 个元素的类型

`get<N>(t)` tuple `t` 的第 `N` 个元素的引用 `t==t2` `t` 和 `t2` 的所有元素是否相等？

`t` 和 `t2` 必须具有相同数量的元素 `t!=t2` `!(t==t2)`

`t<t2` `t` 是否按字典顺序小于 `t2`？

`t>t2` `t2<t`

`t<=t2` `!(t2>t)`

`t>=t2` `!(t2<t)`

`uses_allocator<T,A>::value` 可以用类型为 `A` 的分配器分配 `tuple<T>` 吗？

`swap(t,t2)` `t.swap(t2)`

例如，`tie()` 可用于从 tuple 中提取元素：

```
auto t = make_tuple(2.71828,299792458,"Hannibal");
double c;
string name;
```

```
tie(c,ignore,name) = t; // c=299792458; name="Hannibal"
```

名字 `ignore` 指的是一个类型为“忽略赋值”的对象。因此，在 `tie()` 中使用 `ignore` 意味着对该元组位置的赋值尝试会被忽略。另一种替代方法是：`double c = get<0>(t); // c=299792458`

```
string name = get<2>(t); // name="Hannibal"
```

显然，如果这个元组来自“别处”，使我们无法轻易知道元素值，那么这会更有意义。例如：

```
tuple<int,double,string> compute();
// ...
double c;
string name;
tie(c,ignore,name) = t; // results in c and name
```

# 34.3 资源管理指针

指针指向一个对象（或者不指向）。然而，指针并不表明谁（如果有的话）拥有该对象。也就是说，仅看指针，我们无法知道应该由谁来删除所指向的对象，如何删除，或者是否应该删除。在 `<memory>` 中，我们找到了表达所有权的“智能指针”：

- `unique_ptr`（§34.3.1）表示独占所有权

- `shared_ptr`（§34.3.2）表示共享所有权

- `weak_ptr`（§34.3.3）用于打破循环共享数据结构中的循环

这些资源句柄在 §5.2.1 中介绍。

## 34.3.1 unique_ptr

`unique_ptr`（定义于 `<memory>`）提供了严格所有权的语义：

- `unique_ptr` 拥有其指针所指向的对象。也就是说，`unique_ptr` 有义务销毁其包含的指针所指向的对象（如果有的话）。

- `unique_ptr` 不能被复制（没有复制构造函数或复制赋值）。但它可以被移动。

- `unique_ptr` 存储一个指针，并在自身销毁时（例如当控制线程离开 `unique_ptr` 的作用域时；§17.2.2）使用关联的删除器（如果有的话）删除所指向的对象（如果有的话）。

`unique_ptr` 的用途包括：

- 为动态分配的内存提供异常安全（§5.2.1、§13.3）

- 将动态分配内存的所有权传递给函数

- 从函数返回动态分配的内存

- 在容器中存储指针

可以将 `unique_ptr` 视为由一个简单指针（“包含的指针”）表示，或者（如果它有删除器）由一对指针表示：

```
up1: unique_ptr<T> up2: unique_ptr<T,D>
object object deleter
```

当 `unique_ptr` 被销毁时，会调用其删除器来销毁所拥有的对象。删除器表示销毁对象的意义。例如：

- 对于局部变量的删除器应该什么也不做。

- 对于内存池的删除器应该将对象返回给内存池，并根据该池的定义决定是否销毁它。

- 默认（“无删除器”）版本的 `unique_ptr` 使用 `delete`。它甚至不存储默认删除器。它可以是一个特化版本，或者依赖于空基类优化（§28.5）。这样 `unique_ptr` 就支持通用的资源管理（§5.2）。

```
template<typename T, typename D = default_delete<T>>
class unique_ptr {
public:
using pointer = ptr; // type of the contained pointer;
// ptr is D::pointer if that is defined, otherwise T*
using element_type = T;
using deleter_type = D;
// ...
};
```

包含的指针不能直接被用户访问。

```
unique_ptr up {}
unique_ptr up {p} unique_ptr up {p,del} unique_ptr up {up2} up.~unique_ptr()
up=up2
unique_ptr<T,D> (§iso.20.7.1.2)
```

`cp` 是包含的指针

默认构造函数：`cp=nullptr`; constexpr; noexcept  

`cp=p`; 使用默认删除器；explicit; noexcept  

`cp=p`; `del` 是删除器；noexcept  

移动构造函数：`cp.p=up2.p`; `up2.p=nullptr`; noexcept 析构函数：如果 `cp!=nullptr` 则调用 `cp` 的删除器  

移动赋值：`up.reset(up2.cp)`; `up2.cp=nullptr`;  

`up` 获得 `up2` 的删除器；`up` 的旧对象（如果有）会被删除；noexcept  

`up=nullptr` `up.reset(nullptr)` ; 也就是说，删除 `up` 的旧对象（如果有的话）`bool b {up}`;  

转换为 bool：`up.cp!=nullptr`; explicit  

`x=*up` `x=up.cp`; 仅适用于包含的非数组  

`x=up->m` `x=up.cp->m`; 仅适用于包含的非数组  

`x=up[n]` `x=up.cp[n]`; 仅适用于包含的数组  

`x=up.get()` `x=up.cp`  

`del=up.get_deleter()` `del` 是 `up` 的删除器  

`p=up.release()` `p=up.cp`; `up.cp=nullptr`  

`up.reset(p)` 如果 `up.cp!=nullptr` 则对 `up.cp` 调用删除器；`up.cp=p`  

`up.reset()` `up.cp=pionter{}`（可能是 `nullptr`）；  

对 `up.cp` 的旧值调用删除器  

```cpp
up.swap(up2) Exchange up and up2’s values; noexcept
up=up2 up.cp=up2.cp
up<up2 up.cp<up2.cp
up!=up2 !(up==up2)
up>up2 up2<up
up<=up2 !(up2>up)
up>=up2 !(up2<up)
swap(up,up2) up.swap(up2)
```

注意：**`unique_ptr`** 不提供复制构造函数或复制赋值。如果提供了，“所有权”的含义将很难定义和使用。如果你觉得需要复制，请考虑使用 **`shared_ptr`**（§34.3.3.2）。

可以为一个内置数组使用 **`unique_ptr`**。例如：

```cpp
unique_ptr<int[]> make_sequence(int n)
{
unique_ptr p {new int[n]}; for (int i=0; i<n; ++i)
p[i]=i;
return p;
}
```

这是作为特化版本提供的：

```cpp
template<typename T, typename D>
class unique_ptr<T[],D> { // specialization for arrays (§iso.20.7.1.3)
// the default D=default_delete<T> comes from the general unique_ptr public:
// ... like the unique_ptr for individual objects, but with [] instead of * and -> ...
};
```

为了避免切片（§17.5.1.4），**`Derived[]`** 不能作为 **`unique_ptr<Base[]>`** 的参数，即使 **`Base`** 是 **`Derived`** 的公共基类。例如：

```cpp
class Shape {
// …
};

class Circle : public Base { // …
};

unique_ptr<Shape> ps {new Circle[p,20]}; // OK
unique_ptr<Shape[]> pa {new Circle[] {Circle(p,20), Circle(p,40)}}; // error
```

我们如何最好地理解 **`unique_ptr`**？使用 **`unique_ptr`** 的最佳方式是什么？它被称为指针（**`_ptr`**），我把它读作“unique pointer”，但显然它不仅仅是一个普通指针（否则就没有定义它的必要了）。考虑一个简单的技术示例：

```cpp
unique_ptr<int> f(unique_ptr<int> p)
{
++*p;
return p;
}
```

sp1: sp2:  

使用计数<sub>对象删除器</sub>  

*删除器* 是当引用计数变为零时用来删除共享对象的工具。默认删除器是通常的 **`delete`**（如果有析构函数则调用之，并释放自由存储区）。

例如，考虑一个通用图中的 **`Node`**，该图由一个算法使用，该算法会添加和删除节点以及节点之间的连接（边）。显然，为了避免资源泄漏，**`Node`** 必须且仅在没有其他节点引用它时被删除。我们可以尝试：

```
struct Node {
vector<Node*> edges;
// ...
};
```

鉴于此，回答诸如“有多少个节点指向这个节点？”这类问题非常困难，并且需要大量额外的“维护”代码。我们可以接入一个垃圾收集器（§34.5），但如果图只是大型应用程序数据空间中的一小部分，这可能会带来负面的性能影响。更糟糕的是，如果容器包含非内存资源，如线程句柄、文件句柄、锁等，即使垃圾收集器也会泄漏资源。

相反，我们可以使用 **`shared_ptr`**：

```
struct Node {
vector<shared_ptr<Node>> edges;
thread worker;
// ...
};
```

在这里，**`Node`** 的析构函数（隐式生成的析构函数就可以了）会**删除**它的 **`edges`**。也就是说，每个 **`edges[i]`** 的析构函数会被调用，如果 **`edges[i]`** 是指向它的最后一个指针，那么它所指向的 **`Node`**（如果有）就会被删除。

不要仅仅为了将指针从一个所有者传递给另一个所有者而使用 **`shared_ptr`**；那是 **`unique_ptr`** 的用途，而且 **`unique_ptr`** 做得更好、开销更低。如果你一直使用计数指针作为工厂函数（§21.2.4）等函数的返回值，可以考虑升级到 **`unique_ptr`** 而不是 **`shared_ptr`**。

不要为了阻止内存泄漏而盲目地用 **`shared_ptrs`** 替换指针；**`shared_ptrs`** 不是万灵丹，也不是没有代价的：

- 由 **`shared_ptrs`** 构成的循环链接结构会导致资源泄漏。你需要一些逻辑上的复杂处理来打破循环，例如，使用 **`weak_ptr`**（§34.3.3）。

- 具有共享所有权的对象往往比作用域内的对象“存活”时间更长（因此导致更高的平均资源使用率）。

- 在多线程环境中，共享指针可能代价高昂（因为需要防止对引用计数的数据竞争）。

- 共享对象的析构函数不会在可预测的时间执行，因此更新任何共享对象的算法/逻辑比非共享对象更容易出错。例如，在析构函数的

execution? Which files are open? In general, which objects are "live" and in appropriate states at the (unpredictable) point of execution?

- 如果单个（最后一个）节点保持一个大型数据结构存活，由其删除触发的析构函数调用级联可能会导致显著的“垃圾回收延迟”。这对实时响应是不利的。

**`shared_ptr`** 表示共享所有权，可以非常有用，甚至是必不可少的，但共享所有权并不是我的理想选择，而且它总是有成本的（与你如何表示共享无关）。如果一个对象有一个明确的所有者和一个明确、可预测的生命周期会更好（更简单）。当有选择时：
