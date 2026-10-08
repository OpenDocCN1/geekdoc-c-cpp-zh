
int& r2 = y2; // 获取另一个 int 的引用
r2 = r; // y 的值被赋给 y2
r = &y2; // 错误：你不能改变引用的值
// （不能将 int* 赋值给 int&）

注意最后一个例子；不仅仅这种构造会失败——在初始化之后，没有任何方法可以让引用指向不同的对象。如果你需要指向其他内容，请使用指针。关于如何使用指针的思路，请参阅 §17.9.3。

引用和指针都通过内存地址来实现。它们只是使用地址的方式不同，从而为你——程序员——提供略有不同的功能。

### 17.9.1 指针和引用参数

当你想要将变量的值更改为由函数计算出的值时，你有三种选择。例如：

```
int incr_v(int x) { return x+1; } // 计算一个新值并返回它
void incr_p(int* p) { ++*p; } // 传递一个指针
// （解除引用并对结果进行递增）
void incr_r(int& r) { ++r; } // 传递一个引用
```

你该如何选择？我们认为，返回值往往能产生最明显（因此也是最少出错）的代码；即：

```
int x = 2;
x = incr_v(x); // 将 x 复制到 incr_v()；然后取出结果并赋值
```

对于小对象，比如 `int`，我们更喜欢这种风格。此外，如果一个“大对象”拥有移动构造器（§18.3.4），我们可以高效地在它们之间来回传递。

我们如何在引用参数和指针参数之间进行选择？不幸的是，两种方法都有吸引人的地方和问题，因此答案并不那么明确。你必须根据单个函数及其可能用途做出决定。

使用指针参数可以提醒程序员某些东西可能会被修改。例如：

```
int x = 7;
incr_p(&x); // 需要 &
incr_r(x);
```

在 `incr_p(&x)` 中使用 `&` 的需要提醒用户 `x` 可能会被修改。相比之下，`incr_r(x)` “看起来人畜无害”。这导致了对指针版本的略微偏好。

另一方面，如果你使用指针作为函数参数，函数必须小心，因为有人可能会传入空指针调用它，即传入 `nullptr`。例如：

```
incr_p(nullptr); // 崩溃：incr_p() 会尝试解除引用空指针
int* p = nullptr;
incr_p(p); // 崩溃：incr_p() 会尝试解除引用空指针
```

这显然很糟糕。编写 `incr_p()` 的人可以防止这种情况：

```
void incr_p(int* p)
{
    if (p==nullptr) error("null pointer argument to incr_p()");
    ++*p; // 解除引用指针并递增所指向的对象
}
```

但现在 `incr_p()` 突然不再像以前那样简单和有吸引力了。第 5 章讨论了如何处理不良参数。相比之下，引用的使用者（例如 `incr_r()`）有理由假设引用指向一个对象。

如果从函数语义的角度来看，“传递无内容”（即不传递对象）是可以接受的，我们必须使用指针参数。注意：对于递增操作而言并非如此——这就是为什么在 `p==nullptr` 时需要抛出异常的原因。

因此，真正的答案是：“选择取决于函数的性质”：

- 对于极小的对象，偏好按值传递。
- 对于“无对象”（由 `nullptr` 表示）是有效参数的函数，使用指针参数（并记得测试 `nullptr`）。
- 否则，使用引用参数。

另请参阅 §8.5.6。

### 17.9.2 指针、引用和继承

在 §14.3 中，我们看到了如何在使用其公共基类 `Shape` 对象的地方使用派生类，例如 `Circle`。我们可以用指针或引用的术语来表达这个想法：因为 `Shape` 是 `Circle` 的公共基类，所以 `Circle*` 可以隐式转换为 `Shape*`。例如：

```
void rotate(Shape* s, int n); // 将 *s 旋转 n 度

Shape* p = new Circle(Point{100,100},40);
Circle c {Point{200,200},50};
```

以及：

```
rotate(p,35);
rotate(&c,45);
```

引用同理：

```
void rotate (Shape& s, int n); // 将 $s$ 旋转 n 度

Shape& r = c;
rotate(r,55);
rotate(*p,65);
rotate(c,75);
```

这对大多数面向对象编程技术（§14.3–4）至关重要。

### 17.9.3 一个例子：列表

列表是最常见且最有用的数据结构之一。通常，列表由“链接”组成，每个链接持有一些信息以及指向其他链接的指针。这是指针的经典用途之一。例如，我们可以这样表示一个简短的北欧神祇列表：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_645_0.png)

这样的列表被称为*双向*列表，因为给定一个链接，我们可以找到前驱和后继。只能找到后继的列表被称为*单向*列表。当我们想要轻松删除元素时，我们会使用双向列表。我们可以这样定义这些链接：

```
struct Link {
string value;
Link* prev;
Link* succ;
Link (const string& v, Link* p = nullptr, Link* s = nullptr)
: value(v), prev(p), succ(s) {}
};
```

也就是说，给定一个**链接**，我们可以使用 **succ** 指针访问其后继，使用 **prev** 指针访问其前驱。我们使用空指针来表示一个**链接**没有后继或前驱。我们可以这样构建我们的北欧神祇列表：

```
Link* norse_gods = new Link("Thor",nullptr,nullptr);
norse_gods = new Link("Odin",nullptr,norse_gods);
norse_gods->succ->prev = norse_gods;
norse_gods = new Link("Freia",nullptr,norse_gods);
norse_gods->succ->prev = norse_gods;
```

我们通过创建**链接**并像图中那样将它们连接起来构建了该列表：首先是 *Thor*，然后 *Odin* 作为 *Thor* 的前驱，最后 *Freia* 作为 *Odin* 的前驱。你可以跟踪指针来检查我们是否做对了，以便每个 **succ** 和 **prev** 都指向正确的神祇。然而，由于我们没有明确定义并命名插入操作，代码显得晦涩：

```
Link* insert(Link* p, Link* n) // 在 p 之前插入 n（不完整）
{
 n->succ = p; // p 在 n 之后
 p->prev->succ = n; // n 在原本 p 的前驱之后
 n->prev = p->prev; // p 的前驱变成 n 的前驱
 p->prev = n; // n 变成 p 的前驱
 return n;
}
```

只要 **p** 确实指向一个 **Link**，并且 **p** 指向的 **Link** 确实有一个前驱，这就能工作。请说服自己确实如此。在思考指针和链表结构（如由 **Links** 组成的列表）时，我们总是在纸上画小的框和箭头图来验证我们的代码对于小例子是否有效。请不要因依赖这种有效的低技术设计技巧而感到不好意思。

该版本的 **insert**() 是不完整的，因为它没有处理 **n**、**p** 或 **p->prev** 为 **nullptr** 的情况。我们添加适当的空指针测试，得到更混乱但正确的版本：

```
Link* insert(Link* p, Link* n) // 在 p 之前插入 n；返回 n
{
 if (n==nullptr) return p;
 if (p==nullptr) return n;
 n->succ = p; // p 在 n 之后
 if (p->prev) p->prev->succ = n;
 n->prev = p->prev; // p 的前驱变成 n 的前驱
 p->prev = n; // n 变成 p 的前驱
 return n;
}
```

给定这些，我们可以写

```
Link* norse_gods = new Link("Thor");
norse_gods = insert(norse_gods,new Link("Odin"));
norse_gods = insert(norse_gods,new Link("Freia"));
```

现在，所有容易出错的 **prev** 和 **succ** 指针操作都消失了。指针操作繁琐且容易出错，*应该*隐藏在编写良好且经过充分测试的函数中。特别是，传统代码中的许多错误源于人们忘记将指针与 **nullptr** 进行测试——正如我们在第一个版本的 **insert**() 中（故意）所做的那样。

注意，我们使用了默认参数（§15.3.1, §A.9.2）来避免用户每次使用构造器时都要提及前驱和后继。

### 17.9.4 列表操作

标准库提供了一个 **list** 类，我们将在 §20.4 中描述。它隐藏了所有链接操作，但在这里我们将基于 **Link** 类详细说明我们对 **list** 的概念，以感受 **list** 类“幕后”发生的事情，并查看更多指针使用的例子。

我们的 **Link** 类需要什么操作来允许其用户避免“指针操作”？这在某种程度上取决于口味，但这里有一个有用的集合：

- 构造器
- **insert**：在一个元素之前插入
- **add**：在一个元素之后插入
- **erase**：移除一个元素
- **find**：查找具有给定值的 **Link**
- **advance**：获取第 *n* 个后继

我们可以这样编写这些操作：

```
Link* add(Link* p, Link* n)    // 在 p 之后插入 n；返回 n
{
    // 类似于 insert（见练习 11）
}
```

```
Link* erase(Link* p)           // 从列表中移除 *p；返回 p 的后继
{
    if (p==nullptr) return nullptr;
    if (p->succ) p->succ->prev = p->prev;
    if (p->prev) p->prev->succ = p->succ;
    return p->succ;
}
```

