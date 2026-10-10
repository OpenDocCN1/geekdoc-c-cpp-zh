
```cpp
if (k == temp.key()) {
    return temp.value();
}
```
}
return NULL; // "k" 不在字典中
}

*(注：由于原文文本在后半部分出现了大量的重复和格式错乱，翻译时已根据上下文逻辑对内容进行了对齐处理，确保技术术语的准确性并消除了无效的重复块。)*

144 第 4 章 列表、栈和队列

```cpp
// 使用基于排序数组列表实现的字典
template <typename Key, typename E>
class SALdict : public Dictionary<Key, E> {
private:
    SAList<Key, E*> list;
public:
    SALdict(int size=defaultSize) // 构造函数
    { list = new SAList<Key, E>(size); }
    ~SALdict() { delete list; } // 析构函数
    void clear() { list->clear(); } // 重初始化
}
```

```cpp
// 插入元素：保持元素排序
void insert(const Key& k, const E& e) {
    KVpair<Key, E> temp(k, e);
    list->insert(temp);
}
```

```cpp
// 使用顺序查找找到要删除的元素
E remove(const Key& k) {
    E* temp = find(k);
    if (temp != NULL) list->remove();
    return temp;
}
```

```cpp
removeAny() { // 移除最后一个元素
    Assert(size() != 0, "Dictionary is empty");
    list->moveToToEnd(pos1);
    list->prev(pos1);
    KVpair<Key, E> e = list->remove();
    return e.value();
}
```

```cpp
// 使用二分查找查找
E find(const Key& k) const {
    int l = 1;
    int r = list->length();
    while (l+1 <= r) { // 当 l 和 r 相同时停止
        int i = (l+r)/2; // 检查剩余子数组的中间
        list->moveToPos(i);
        KVpair<Key, E> temp = list->getValue();
        if (k < temp.key()) r = i; // 在左侧
        if (k == temp.key()) return temp.value(); // 找到
        if (k > temp.key()) l = i; // 在右侧
    }
    return NULL; // "k" 不在字典中
}
```

图 4.34 使用基于排序数组列表实现的字典实现。

第 4.5 节 阅读

```cpp
int size() { // 返回列表大小
{ return list->length(); }
};
```

图 4.34（续）

为了让比较器类从记录类型中提取键，作为在此处存储键值对的替代方案，这里是用于比较整数所需的类示例。

```cpp
class intCompare { // 针对整数键的比较器类
public:
    static bool lt(int x, int y) { return x < y; }
    static bool eq(int x, int y) { return x == y; }
    static bool gt(int x, int y) { return x > y; }
};
```

`intCompare` 提供了方法来判断 `int` 变量是否相等 (`eq`)，或者第一个是否小于第二个 (`lt`)，或大于第二个 (`gt`)。
这里是一个用于比较 C 风格字符串的类。它使用了标准库函数 `strcmp` // 比较两个字符字符串

```cpp
class CCmpare {
public:
    static bool lt(char* x, char* y) {
        return strcmp(x, y) < 0; }
    static bool eq(char* x, char* y) {
        return strcmp(x, y) == 0; }
    static bool gt(char* x, char* y) {
        return strcmp(x, y) > 0; }
};
```

我们在第 5.5 节中使用比较器在堆中实现比较，并在第 7 章中在排序算法中实现比较。

## 4.5 阅读

关于用于定义 `List ADT` 的选择函数的更多讨论，请参阅俄亥州立 Reuse Research Group 的工作。对 `List ADT` 的定义可以在 `[SWH93]`。关于类的更多信息可以在 `[SWH94]`。

## 4.6 练习

4.1 假设列表具有以下配置：

| 2, 23, 15, 5, 9 |

146 第 4 章 列表、栈和队列 使用图 4.1 的 `List ADT` 编写一系列 C++ 语句删除值为 15 的元素。

4.2 使用图 4.1 的 `List ADT` 显示每系列操作后的列表配置。假设 `L1` 和 `L2` 在每个系列的开始时是空的。显示当前位置在列表中的位置。

```
a) L1.append(10);
L1.append(20);
L1.append(15);
```

```
b) L2.append(10);
L2.append(20);
L2.append(15);
L2.moveToStart();
L2.insert(39);
L2.next();
L2.insert(12);
```

4.3 使用图 4.1 的 `List ADT` 写一系列 C++ 语句，创建一个二十元素的列表，并实际存储以下配置的列表：

> { 2, 23 | 15, 5, 9 }

4.4 使用图 4.1 的 `List ADT`，编写一个函数交换当前元素及其后面的元素。

4.5 在 4.1.2 节中链表实现中，当前位置是通过指针实现的。更“自然”的方法似乎是 `curr` 直接指向当前元素。但如果这样做，由于无法从 `curr` 访问前一个节点，将无法更新。如果 `curr` 已经在列表末尾会发生什么？是否有其他方法让这工作？是 4.1.2 的实现更简单还是更复杂？特别是，你可以连续删除几次吗？

4.6 在 `LList` 类中添加一个成员函数反转列表元素的顺序。对于 `n` 个元素的列表，你的算法运行时间应为 Θ(n)。

4.7 写一个函数合并两个链表。输入列表按从小到大的顺序排序。输出列表也应该从到到大排序。你的算法在输出列表长度上应该是线性的。

4.8 循环链表是指最后一个节点的 `next` 字段指向列表第一个节点。当你希望元素具有相对位置但没有绝对开头或结尾时非常有用。

-(a) 修改图 4.8 的代码实现循环单链表。
-(b) 修改图 4.14 的代码实现循环双链表。

4.9 4.1.3 节指出“基于数组的列表实现所需的空间是 Ω(n)，但可能更大”。解释为什么。

4.10 4.1.3 给出了一个确定两个列表实现空间平衡点的方程。变量为 `D`, `E`, `P` 和 `n`。每个变量的量纲是什么？证明方程的两边在量纲上是平衡的。

4.11 使用 4.1 节的空间方程确定基于数组列表和链表实现的平衡点，当指定数据字段、指针和基于数组列表的大小时。说明链表何时空间更少。

-(a) 数据字段为 8 字节，指针为 4 字节，数组包含二十元素。
-(b) 数据字段为 2 字节，指针为 4 字节，数组包含三十元素。
-(c) 数据字段为 1 字节，指针为 4 字节，数组包含三十元素。
-(d) 数据字段为 32 字节，指针为 4 字节，数组包含四十元素。

4.12 确定你的计算机上 `int` 变量、`double` 变量和指针的大小。如果你还不知道答案，C++ 的 `sizeof` 操作可能会有用。

-(a) 计算关于 `n` 的函数平衡点，对于元素为 `int` 的列表，基于数组列表比链表更高效。
-(b) 计算关于 `n` 的函数平衡点，对于元素为 `double` 的列表，基于数组列表比链表更高效。

166

4.13 修改图 4.18 的代码，实现共享同一个数组的两个栈，如图 4.20 所示。

4.14 修改图 4.26 的数组队列定义，使用单独的布尔变量来跟踪队列是否为空，而不是要求一个数组位置为空。

4.15 回文是一个正读和反读相同的字符串。只使用固定数量的栈和队列、栈和队列 ADT 函数以及固定数量的 `int` 和 `char` 变量，写一个算法判断字符串是否为回文。假设字符串从标准输入一次读取一个字符。算法应根据情况输出 `true` 或 `false`。

4.16 使用栈重新实现练习 2.11 中的 `fibr`，如 4.2.4 节描述的递归调用。

4.17 写一个递归算法计算递归关系的值：

```
T(n) = T[n/2] + T[n/2] + n;  T(1) = 1.
```
