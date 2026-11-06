
![](img/5e58fb4c840712efd6ed6fa82bb97f57_599_0.png)

如果你想编写一个收集对象（例如左侧的邮票）的程序，你有多种选择。当然，你可以使用数组或链表，但计算机科学家已经发明了其他可能更适合该任务的机制。在本章中，你将学习如何使用 C++ 库提供的集合、映射和优先队列类型。你将看到这些数据结构如何以树状结构实现，以及它们如何用顺序排序换取快速元素查找。

## 14.1 集合

数组、向量和链表有一个共同特征：这些数据结构按照插入元素的相同顺序保存元素。然而，在许多应用中，你并不真正关心集合中元素的顺序。于是你可以做出一个非常有用的权衡：不按顺序保存元素，而是能够快速找到它们。

集合是不同元素的无序集合。

在数学和计算机科学中，不同项的无序集合称为集合。一个典型例子是打印服务器：一台可以访问多台打印机的计算机。服务器可能保存一组表示可用打印机的对象（见图 1）。这些对象的顺序并不真正重要。

集合上的基本操作有

- 添加元素。
- 删除元素。
- 查找元素。
- 遍历所有元素。

集合没有重复项。添加一个已存在元素的重复项会被忽略。

集合拒绝重复项。如果一个对象已经在集合中，再次添加它的尝试会被忽略。这在许多编程情形中很有用。例如，如果我们保存一组可用打印机，每台打印机在集合中最多出现一次。因此，我们将像在数学中那样解释集合的添加和删除操作：添加已经在集合中的元素，以及删除不在集合中的元素，都是有效操作，但它们不会改变集合。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_599_1.png)

图 1   一组打印机

在 C++ 中，你使用 set 类构造集合。与向量和列表一样，set 需要一个类型参数。例如，字符串集合声明如下：

```cpp
set<string> names;
```

你使用 insert 和 erase 成员函数来添加和删除元素：

```cpp
names.insert("Romeo");
names.insert("Juliet");
names.insert("Romeo"); // Has no effect: "Romeo" is already in the set
names.erase("Juliet");
names.erase("Juliet"); // Has no effect: "Juliet" is no longer in the set
```

要确定某个值是否在集合中，使用 count 成员函数。如果该值在集合中，它返回 1，否则返回 0。

```cpp
int c = names.count("Romeo"); // count returns 1
```

最后，你可以使用迭代器访问集合中的元素。迭代器按排序顺序访问元素，而不是按你插入它们的顺序。例如，考虑我们如下继续集合示例时会发生什么：

标准 C++ set 类按排序顺序存储值。

```cpp
names.insert("Tom");
names.insert("Diana");
names.insert("Harry");
set<string>::iterator pos;
for (pos = names.begin(); pos != names.end(); pos++)
{
   cout << *pos << " ";
}
```

这段代码按字典顺序打印集合元素：

```cpp
Diana Harry Romeo Tom
```

集合不能包含重复项。多重集合（也称为袋）是一种无序集合，可以包含一个元素的多个副本。一个例子是装有某些杂货物品不止一次的杂货袋（见图 2）。

在 C++ 库中，multiset 类实现这种数据类型。你使用多重集合的方式与集合相同。当你多次插入一个元素时，元素计数反映插入次数。每次调用 erase 都会递减元素计数，直到它达到 0。

多重集合（或袋）与集合类似，但元素可以出现多次。

```cpp
multiset<string> names;
names.insert("Romeo");
names.insert("Juliet");
names.insert("Romeo"); // Now names.count("Romeo") is 2
names.erase("Juliet"); // Now names.count("Juliet") is 0
names.erase("Juliet"); // Has no effect: "Juliet" is no longer in the bag
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_600_0.png)

集合用法的一个很好示例是检查拼写错误的单词的程序。假设你有一个包含正确拼写单词的文件（即词典），以及一个你想检查的第二个文件。程序将包含正确拼写单词词典的文件读入集合，然后从第二个文件读取单词，并在集合中测试每个单词，如果未找到该单词就打印它。

```cpp
void spell_check(istream& dictionary, istream& text)
{
    set<string> words;
    string word;

    // First put all words from the dictionary into the set
    while (dictionary >> word)
    {
        words.insert(word);
    }

    // Then read words from text
    while (text >> word)
    {
        if (words.count(word) == 0)
        {
            cout << "Misspelled word " << word << endl;
        }
    }
}
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_601_0.png)

# 自测题

- 1. 数组和列表会记住你添加元素的顺序；集合不会。为什么你会想使用集合而不是数组或列表？
- 2. 为什么集合迭代器不同于列表迭代器？
- 3. 以下代码片段的输出是什么？

```cpp
set<int> s;
for (int i = 1; i <= 4; i++)
{
    s.insert(i * i);
    s.insert(-i);
}
for (set<int>::iterator p = s.begin(); p != s.end(); p++) { cout << *p << " "; }
```

- 4. 以下代码片段的输出是什么？

```cpp
set<int> s;
for (int i = 0; i < 20; i = i + 2) { s.insert(i); }
for (int i = 0; i < 20; i = i + 2) { s.erase(i); }
for (set<int>::iterator p = s.begin(); p != s.end(); p++) { cout << *p << " "; }
```

- 5. 给定两个名为 a 和 b 的 sets<string>，以下代码做什么？

```cpp
set<string> c;
for (set<string>::iterator p = a.begin(); p != a.end(); p++) { c.insert(*p); }
for (set<string>::iterator p = b.begin(); p != b.end(); p++)
{
    if (a.count(*p) == 0) { c.erase(*p); }
}
```

**动手实践**  现在你可以尝试本章末尾的这些练习：R14.1、R14.2、P14.3。

## 专题 14.1

![](img/5e58fb4c840712efd6ed6fa82bb97f57_602_0.png)

### 为容器元素定义排序顺序

set 和 multiset 类需要比较元素。默认情况下，这些类使用 < 运算符进行比较。

假设你想构建一个 set<Employee>。编译器会报错，因为它不知道如何比较两个 Employee 对象。

要解决这个问题，你可以为 Employee 对象重载 < 运算符：

```cpp
bool operator<(const Employee& a, const Employee& b)
{
    return a.get_name() < b.get_name();
}
```

这个 < 运算符按姓名比较员工。要了解更多关于运算符重载的内容，请参见 Horstmann 和 Budd，*Big C++，第 2 版*，第 14 章（John Wiley & Sons, Inc.，2009）。

## 14.2 二叉搜索树

集合实现可以按它选择的任何方式重新排列元素，以便快速找到元素。假设某个集合实现对其条目进行*排序*。那么它可以使用*二分查找*在 O(log n) 步内定位元素，其中 n 是集合的大小。这个想法只有一个小问题。我们不能使用数组存储集合的元素，因为在数组中插入和删除很慢；这是一个 O(n) 操作。

在接下来的几节中，我们将介绍计算机科学家为克服这个问题而发明的许多*树*数据结构中最简单的一种。

### 14.2.1 二叉树和二叉搜索树

> 二叉树由节点组成，每个节点最多有两个子节点。

链表是一维数据结构。你可以想象所有节点排成一条线。相比之下，*树*由具有子节点的节点组成，而子节点又可以拥有子节点。你应该把它想象成一棵树，只不过传统上把树倒着画，像家谱或层级图一样（见图 3）。在二叉树中，每个节点最多有两个子节点；因此得名*二叉*。

最后，*二叉搜索树*的构造具有以下重要性质：

- *任何*节点左侧*所有*后代的数据值都小于存储在该节点中的数据值，而右侧的*所有*后代具有更大的数据值。

> 二叉搜索树中的所有节点都满足这一性质：左侧后代的数据值小于该节点的数据值，而右侧后代的数据值更大。

图 3 中的树具有这一性质。要验证二叉搜索树性质，必须检查每个节点。考虑节点“Juliet”。左侧的所有后代的数据都排在“Juliet”之前。右侧的所有后代的数据都排在“Juliet”之后。继续看“Eve”。它有一个左子节点，数据“Adam”排在“Eve”之前，还有一个右子节点，数据“Harry”排在“Eve”之后。用同样的方法检查其余节点。
