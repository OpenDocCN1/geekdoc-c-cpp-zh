

在§21.6.3中，我们将回到道琼斯指数的例子，并将这种广义的**inner_product**()用作更优雅解决方案的一部分。

## 21.6 关联容器

在**vector**之后，标准库中最有用的容器可能是**map**。一个**map**是一个有序的(key,value)对序列，你可以根据键查找值；例如，my_phone_book["Nicholas"]可以是Nicholas的电话号码。在流行度竞争中，**map**唯一的潜在竞争者是**unordered_map**（参见§21.6.4），那是一种针对字符串键进行优化的**map**。与**map**和**unordered_map**类似的数据结构有许多名称，例如*关联数组*、*哈希表*和*红黑树*。流行且有用的概念总是有许多名称。在标准库中，我们将所有这样的数据结构统称为*关联容器*。

标准库提供了八个关联容器：

### 关联容器

| 容器 | 描述 |
| :--- | :--- |
| **map** | 有序的(key,value)对容器 |
| **set** | 有序的键容器 |
| **unordered_map** | 无序的(key,value)对容器 |
| **unordered_set** | 无序的键容器 |
| **multimap** | 键可以出现多次的**map** |
| **multiset** | 键可以出现多次的**set** |
| **unordered_multimap** | 键可以出现多次的**unordered_map** |
| **unordered_multiset** | 键可以出现多次的**unordered_set** |

这些容器在 **<map>**、**<set>**、**<unordered_map>** 和 **<unordered_set>** 中提供。

### 21.6.1 map

考虑一个概念上简单的任务：创建一个文本中单词出现次数的列表。显而易见的做法是维护一个我们见过的单词列表，并记录每个单词出现的次数。当我们读取一个新单词时，查看我们是否已经见过它；如果见过，我们将它的计数加一；如果没有，我们将其插入列表并赋予值1。我们可以使用**list**或**vector**来做这件事，但那样我们就会不得不为读取的每个单词进行搜索。这可能很慢。**map**以使其键易于判断是否存在的方式存储键，从而使任务的搜索部分变得微不足道：

```cpp
int main()
{
    map<string,int> words;      // 存储(单词, 频率)对

    for (string s; cin>>s; )
        ++words[s];            // 注意：words 由字符串下标访问

    for (const auto& p : words)
        cout << p.first << ": " << p.second << "\n";
}
```

程序中最有趣的部分是`++words[s]`。正如我们从main()的第一行看到的，words是一个(string,int)对的map；也就是说，words将字符串映射到整数。换句话说，给定一个字符串，words可以让我们访问其对应的整数。因此，当我们用一个字符串（保存从输入读取的单词）对words取下标时，`words[s]`是对应于s的整数的引用。让我们看一个具体的例子：

```cpp
words["sultan"]
```

如果我们之前没有见过字符串"sultan"，"sultan"将以整数的默认值0进入words。现在，words有一个条目("sultan",0)。因此，如果之前没看到"sultan"，`++words["sultan"]`将把值1与字符串"sultan"关联起来。详细地说：map会发现"sultan"未被找到，插入一个("sultan",0)对，然后`++`将该值递增，得到1。

现在再看一遍程序：`++words[s]`获取我们从输入获得的每个"单词"并将其值增加一。当第一次看到一个新单词时，它获得值1。现在循环的含义就清楚了：

```cpp
for (string s; cin>>s; )
    ++words[s];                // 注意：words 由字符串下标访问
```

这读取输入中的每个（空白分隔的）单词并计算每个单词的出现次数。现在我们要做的只是产生输出。我们可以遍历map，就像遍历其他任何STL容器一样。map<string,int>的元素类型是pair<string,int>。pair的第一个成员称为*first*，第二个成员称为*second*，因此输出循环变为

```cpp
for (const auto& p : words)
    cout << p.first << ": " << p.second << "\n";
```

作为测试，我们可以将*The C++ Programming Language*第一版的开篇语句输入给我们的程序：

> C++ is a general purpose programming language designed to make programming more enjoyable for the serious programmer. Except for minor details, C++ is a superset of the C programming language. In addition to the facilities provided by C, C++ provides flexible and efficient facilities for defining new types.

我们得到输出

```text
C: 1
C++: 3
C_: 1
Except: 1
In: 1
a: 2
addition: 1
and: 1
by: 1
defining: 1
designed: 1
details,,: 1
efficient: 1
enjoyable: 1
facilities: 2
flexible: 1
for: 3
general: 1
is: 2
language: 1
language.: 1
make: 1
minor: 1
more: 1
new: 1
of: 1
programmer: 1
programming: 3
provided: 1
provides: 1
purpose: 1
serious: 1
superset: 1
the: 3
to: 2
types.: 1
```

如果我们不喜欢区分大写字母和小写字母，或者希望消除标点符号，我们可以这样做：见练习13。

### 21.6.2 map 概览

那么什么是map？实现map的方法有很多种，但STL的map实现倾向于使用平衡二叉搜索树；更具体地说，它们是红黑树。我们不会深入细节，但现在你知道了技术术语，因此，如果你想了解更多，可以在文献或网络上查找它们。

一棵树是由节点构成的（类似于列表由链接构成；参见§20.4）。一个Node持有一个键、其对应的值以及指向两个后代Node的指针。

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_811_0.png)

假设我们插入了(Kiwi,100)、(Quince,0)、(Plum,8)、(Apple,7)、(Grape,2345)和(Orange,99)，那么map<Fruit,int>在内存中可能看起来是这样的：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_811_1.png)

给定持有键值的Node成员名称为*first*，二叉搜索树的基本规则是

```cpp
left->first < first && first < right->first
```

也就是说，对于每个节点，

- 它的左子节点的键小于该节点的键，且
- 该节点的键小于其右子节点的键

你可以验证这对树中的每个节点都成立。这允许我们"从树的根向下搜索"。奇怪的是，在计算机科学文献中，树是从根向下生长的。在例子中，根节点是(*Orange*, 99)。我们只需沿着树向下比较，直到找到我们要找的东西或它应该在的位置。当（如上面的例子中）每棵子树拥有的节点数大致与同样距离根的每棵其他子树相同时，树被称为*平衡*的。保持平衡将我们需要访问以到达某个节点的平均节点数降至最低。

一个**Node**也可能持有一些额外的数据，map将使用这些数据来保持其节点树的平衡。当每个节点左侧和右侧的后代数量大致相同时，树是平衡的。如果一棵有N个节点的树是平衡的，我们最多需要查看log₂(N)个节点来找到一个节点。这比我们在列表中包含键并从头搜索时需要检查的平均N/2个节点好得多（这种线性搜索的最坏情况是N）。（另见§21.6.4。）例如，看一棵不平衡的树：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_812_0.png)

这棵树仍然满足每个节点的键大于其左子节点的键且小于其右子节点的键的条件：

```cpp
left->first < first && first < right->first
```

然而，这棵树的版本是不平衡的，因此我们现在需要三次"跳跃"才能到达*Apple*和*Kiwi*，而在平衡树中只需要两次。对于包含许多节点的树，差异可能非常显著，因此用于实现**map**的树是平衡的。

