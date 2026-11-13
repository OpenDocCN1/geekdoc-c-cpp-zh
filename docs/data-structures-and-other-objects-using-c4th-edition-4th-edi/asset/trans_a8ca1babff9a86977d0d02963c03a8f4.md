

这一点，不需要高效的实现。例如，仅仅向集合中添加一个新项将需要线性时间，因为你需要检查新项是否已存在。稍后我们将探讨更高效的实现（包括 C++ 标准库中 set 的实现）。

你可能还希望为你的 set 类添加额外的操作，例如减法运算符。

假设你实现了一个序列，其中 value_type 具有比较运算符 <，用于确定一个项何时“小于”另一个项。例如，整数、双精度数和字符都有这样的比较运算符（你自己实现的类也可以赋予这样的比较）。使用新类名 sorted_sequence 重写序列类。在有序序列中，insert 函数始终会插入新项，使得所有项都保持从小到大的顺序。没有 attach 函数。所有其他函数都与原始序列类相同。

在这个项目中，你将实现一个名为 带收据的包（bag with receipts）的新类。这个新类类似于普通的包，但添加和移除项的方式不同。每次向带收据的包中添加一项时，insert 函数会返回一个名为 收据（receipt）的唯一整数。稍后，当你想要移除一项时，必须将收据的副本作为参数提供给 remove 函数。remove 函数会移除出示了收据的那一项，并通过引用参数返回该项的副本。这里有一个实现思路：带收据的包可以有两个私有数组，如下所示：

```cpp
class bag_with_receipts
{
   ...
   private:
      value_type data[CAPACITY];
      bool in_use[CAPACITY];
};
```

这样的数组（大小相同）称为并行数组。其思路是通过在第二个数组中放置布尔值来跟踪 data 数组的哪些部分正在被使用。当 in_use[i] 为 true 时，data[i] 当前正在被使用；当 in_use[i] 为 false 时，data[i] 当前未被使用。当添加新项时，我们会找到第一个当前未使用的位置并将新项存储在那里。该项的收据是存储新项的位置的索引。

存储项集合的另一种方式是使用键控包（keyed bag）。这种包在每次添加项时，使用包的程序员还需要提供一个名为 键（key）的整数。添加到键控包中的每一项都必须具有唯一的键；两项不能具有相同的键。因此，插入函数的规格如下所示：

```cpp
void keyed_bag::insert
(const value_type& entry, int key);
// Precondition: size() < CAPACITY, and the
// bag does not yet contain any item with
// the given key.
// Postcondition: A new copy of entry has
// been added to the bag, with the given key.
```

当程序员想要从键控包中移除一项时，必须指定该项的键，而不是项本身。键控包还应有一个布尔成员函数，可用于确定包中是否具有指定键的项。

（键控包与带收据的包在两个重要方面有所不同。）在键控包中，使用该类的程序员在插入项时指定一个特定的键。相比之下，对于带收据的包，insert 函数返回一个收据，使用该类的程序员无法控制该收据可能是什么。

在这个项目中，对键控包进行完整的规格说明、设计和实现。

这是一个将在第 4 章中开发的更长项目的简单版本。该项目从一元多项式的定义开始，一元多项式是形式如下的算术表达式：

$a_0 + a_1x + a_2x^2 + ... + a_kx^k$

最高指数 k 称为多项式的 **次数**，常数 $a_0, a_1, \dots$ 是 **系数**。例如，这里有三个次数为 3 的多项式：

2.1 + 4.8x + 0.1x^2 + (-7.1)x^3
2.9 + 0.8x + 10.1x^2 + 1.7x^3

为多项式指定、设计并实现一个类。该类可以包含一个静态成员常量 MAXDEGREE，用于指示任何多项式的最大次数。（这样可以让你在固定大小的数组中存储系数。）花些时间思考对多项式有意义的操作。例如，你可以编写一个添加两个多项式的操作。另一个操作应该对给定的 x 值求解多项式。

- 10 指定、设计并实现一个类，该类可以作为井字棋游戏中的一名玩家。构造函数应指定该对象是第一个玩家（X）还是第二个玩家（O）。应有一个成员函数来请求对象进行下一步移动，以及一个成员函数来告知对象对手的下一步移动。还应包含其他有用的成员函数，例如一个函数来询问井字棋板上的给定位置是否被占用，如果是，是被 X 还是 O 占用。此外，还应包含一个成员函数来确定游戏何时结束，以及是平局、X 获胜还是 O 获胜。在两个程序中使用该类：一个是与程序用户对弈的井字棋程序，另一个是两个井字棋对象相互对弈的程序。

- 11 指定、设计并实现一个容器类，最多可容纳五张扑克牌。将该类命名为 pokerhand，并重载布尔比较运算符，以便比较两手扑克牌。对于两手牌 x 和 y，关系 x > y 表示 x 是比 y 更好的牌。如果你自己不参加每周的扑克游戏，那么可能需要查阅纸牌规则书来了解扑克牌排名的规则。

- 12 指定、设计并实现一个类，用于跟踪堆叠在桩上的环，有点像叠在主轴上的留声机唱片。这里展示了一个五个环的示例：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_178_0.png)

桩最多可容纳 64 个环，每个环都有自己的直径。此外，还有一条规则要求每个环必须比其下方的任何环都小，如我们的示例所示。该类的成员函数应包括：(a) 一个构造函数，不在桩上放置任何环（n 可以大到 64），使用默认参数（这些是直径从 1 英寸到 n 英寸的环）来初始化桩。(b) 一个返回桩上环的数量的成员函数。(c) 一个常量成员函数，返回最顶部环的直径。(d) 一个向顶部添加新环的成员函数（环的直径作为函数参数）。(e) 一个移除最顶部环的成员函数。(f) 一个重载的输出函数，用于打印桩及其环的某种巧妙表示。确保所有函数都有适当的前置条件，以保证强制执行关于环大小的规则。同时花些时间设计适当的私有数据字段。

- 13 在这个项目中，你将设计并实现一个名为 towers 的类，它是一个让孩子玩汉诺塔游戏的程序的一部分。该游戏由三个桩和一堆堆叠在桩上的环组成。环的大小各不相同。五个环游戏的初始配置如下所示，第一个塔上的环大小从一英寸（顶部）到五英寸（底部）。

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_178_1.png)

一次将一个环从一个桩的顶部移到另一个桩的顶部。游戏的目标是将所有环从第一个桩移到第二个桩。困难在于，孩子不能将一个环放在直径较小的环上方。还有一个额外的桩用于暂时存放环，但禁令也适用于该桩以及另外两个桩。三个环游戏的解决方案如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_179_0.png)

towers 类必须跟踪所有三个桩的状态。你可以使用三个桩的数组，其中每个桩都是上一个项目中的对象。towers 函数的规格如下所示：

```cpp
towers::towers(size_t n = 64);
// Precondition: 1 <= n <= 64.
// Postcondition: The towers have been initialized
// with n rings on the first peg and no rings on
// the other two pegs. The diameters of the first
// peg's rings are from one inch (on the top) to n
// inches (on the bottom).
```

```cpp
size_t towers::many_rings
(int peg_number) const;
// Precondition: peg_number is 1, 2, or 3.
// Postcondition: The return value is the number
// of rings on the specified peg.
```

```cpp
size_t towers::top_diameter
(int peg_number) const;
// Precondition: peg_number is 1, 2, or 3.
// Postcondition: If many_rings(peg_number) > 0,
// then the return value is the diameter of the top
// ring on the specified peg; otherwise the return
// value is zero.
```

```cpp
void towers::move
(int start_peg, int end_peg);
// Precondition: start_peg is a peg number
// (1, 2, or 3), and many_rings(start_peg) > 0;
// end_peg is a different peg number (not equal
// to start_peg, and top_diameter(end_peg) is
// either 0 or more than top_diameter(start_peg)).
// Postcondition: The top ring has been moved
// from start_peg to end_peg.
```

此外，重载输出运算符，以便可以轻松显示 towers 对象。在允许孩子玩汉诺塔的程序中使用 towers。确保不允许孩子做出任何非法移动。

- 14 指定、设计并实现一个名为 integer 的类，每个对象跟踪一个最多 100 位的十进制大整数。数字可以存储在 100 个元素的数组中，数字的符号可以存储在单独的成员变量中，正数为 +1，负数为 -1。该类应包含几个方便的构造函数，例如从普通 int 初始化对象的构造函数。还应重载常用的算术和比较运算符（用于对这些大数进行算术运算和比较），并重载输入和输出运算符。

- 15 使用第 2 章（编程项目 4）中开发的 card 类来创建一个新的牌组类。deck 类具有一个容量为 52 的序列来存放卡片。构造函数按花色和点数顺序将 52 张卡片分配给序列。一个友元函数应使用单词显示整个牌组（即，“黑桃 A”）。第 5 章（项目 16）将向此类添加更多函数。

