

## 常量成员函数：

- s.capacity()       // 返回可以放入 s 中而无需添加更多内存的字符最大数量。
                     //
- s.c_str()          // 返回一个 const 字符数组，其中包含以 null 结尾的字符串，
                     // 该字符串与 s 具有相同的字符。
- s.data()           // 与 s.c_str() 相同，但没有空终止符。
- s.empty()          // 如果 s 没有字符，则返回 true。
- s.length()         // 返回 s 中当前的字符数量。
- s.max_size()       // 返回 s 可能拥有的最大字符数量。
                     //
- s.size()           // 与 s.length() 相同。
- s1 == s2 和 s1 != s2   // 布尔测试，用于判断两个字符串是否相等或不相等。
- s1 < s2 和 s1 > s2     // 测试字符串的字典序排列。
- s1 <= s2 和 s1 >= s2

## 提供对字符串字符访问的函数：

对于 0 到 s.length() - 1 范围内的索引，表示法 s[index] 或 s.at(index) 返回指定索引处的字符。这两个函数都返回对字符的引用。当字符串不是 const 时，此引用可用于更改字符，例如 s[2] = 'x'。当索引超出范围时，at 版本会引发异常，但在这种情况下，s[index] 的行为是未定义的。

## 连接：

表达式 s1 + s2 是一个新字符串，包含 s1 的字符，后跟 s2 的字符。

## 追加函数：

这些函数将指定字符添加到字符串现有内容的末尾，使用前面所示的一种参数形式。

- s.append(str) 或 s += str
- s.append(str, index, n)
- s.append(c) 或 s += c
- s.append(n, c)
- s.append(carry) 或 s += carry
- s.append(carry, n)
- s.append(begin, end)

## 插入函数：

这些函数插入新字符，使用前面所示的一种参数形式指定。这些字符从 s[i] 开始插入。i 的值必须小于或等于 s.size()。s[i] 或之后的任何现有字符都将向右移动，为新字符腾出空间。

- s.insert(i, str)
- s.insert(i, str, index, n)
- s.insert(i, n, c)
- s.insert(i, carry)
- s.insert(i, carry, n)

## 替换函数：

这些函数替换从 s[i] 开始的 s 中的 len 个字符。i 的值必须小于或等于 s.size()，并且如果从该位置开始的字符少于 len 个，则替换字符串末尾的所有字符。新字符使用前面所示的一种参数形式指定。

- s.replace(i, len, str)
- s.replace(i, len, str, index, n)
- s.replace(i, len, n, c)
- s.replace(i, len, carry)
- s.replace(i, len, carry, n)

## 查找字符串中位置的函数：

这些函数返回 string::size_type 类型的值。如果未找到字符，则返回值为常量 string::npos。

- s.find(c) // 返回字符 c 在 s 中首次出现的索引
- s.find(c, i) // 返回 c 在 s[i] 或之后首次出现的索引
- s.rfind(c) // 返回字符 c 在 s 中最后一次出现的索引
- s.rfind(c, i) // 返回 c 在 s[i] 或之前最后一次出现的索引
- s.find(str) // 返回子串 str 在 s 中首次出现的索引
- s.find(str, i) // 返回 str 在 s[i] 或之后首次出现的索引
- s.rfind(str) // 返回子串 str 在 s 中最后一次出现的索引
- s.rfind(str, i) // 返回 str 在 s[i] 或之前最后一次出现的索引

## 返回子串的函数：

- s.substr(i) // 返回包含从 s[i] 到 s 末尾的字符的字符串
- s.substr(i, n) // 返回包含从 s[i] 开始最多 n 个字符的字符串

## 其他修改成员函数：

- s.clear() // 从 s 中删除所有字符。
- s.erase() // 从 s 中删除所有字符。
- s.erase(i) // 从 s[i] 到 s 末尾删除所有字符。
- s.erase(i, len) // 从 s[i] 开始删除最多 len 个字符。
- s.reserve(amount) // 请求将 s 的容量更改为指定的数量（可能小于当前容量）。但是，更改后的容量永远不会小于当前字符串大小。
- s.resize(n, c) // 将 s 的长度更改为 n（如果这增加了长度，则新字符为字符 c）。
- s.resize(n) // 与 s.resize(n, '\0') 相同。

## 输入和输出：

- cout << s // 将 s 的全部内容打印到 cout。
- cin >> s // 跳过空白字符，然后将字符读入 s，直到遇到空白字符。终止空白字符不被读取。
- getline(cin, s, c) // 从 cin 将字符读入 s，直到遇到 c。终止 c 被读取但不添加到 s 的末尾。
- getline(cin, s) // 与 getline(cin, s, '\n') 相同。

## 来自 <vector> 的向量、来自 <list> 的列表和来自 <deque> 的双端队列

vector<Item> 模板类提供一系列项目，类似于字符串提供一系列字符的方式。虽然 C++ 标准不要求，但典型的 vector 实现将项目存储在动态数组中。

list<Item> 模板类也提供一系列项目，类似于第 3 到第 5 章中的序列类。在由迭代器标记的任何点进行插入和删除，列表更高效，因为它们通常使用链表实现。

deque<Item> 模板类是一个双端队列，即一种可以快速访问两端元素的序列（如第 8.4 节所述）。

## 构造函数和赋值：

所有三个类都有一个默认构造函数（创建一个空序列）、一个拷贝构造函数和一个赋值运算符。函数 w.assign(n, element) 将 w 更改为包含指定元素 n 个副本的序列。

## 常量成员函数：

```
w.capacity() // (Vector only) Returns the maximum number of items
that could be put in w without adding more memory.
w.empty() // Returns true if w has no items.
w.size() // Returns the current number of items in w.
w.max_size() // Returns the maximum number of elements that w could
ever have.
w1 == w2 and w1 != w2 // Boolean tests of whether two sequences are equal or unequal.
w1 < w2 and w1 > w2 // Tests for lexicographical ordering of sequences.
w1 <= w2 and w1 >= w2
```

## 提供对向量项目随机访问的函数（但不适用于列表或双端队列）：

对于 0 到 v.size() - 1 范围内的索引，表示法 v[index] 或 v.at(index) 返回指定索引处的项目。这两个函数都返回对项目的引用。当向量不是 const 时，此引用可用于更改项目，例如 v[2] = 'x';。当索引超出范围时，at 版本会引发异常，但在这种情况下，v[index] 的行为是未定义的。

## 插入函数：

每个插入函数都有一个参数 pos，它是序列的迭代器。新元素插入到此位置。此位置或之后的任何现有项目都将向右移动，为新项目腾出空间。

```
w.insert(pos, element) // Inserts new element at specified position.
w.insert(pos, n, element) // Inserts n copies of new element at specified position.
w.insert(pos, begin, end) // Inserts elements [begin..end) into the sequence at the
specified position.
```

## 其他修改成员函数：

```
w.clear() // Removes all elements from w.
w.erase(pos) // Pos is an iterator for the sequence; this function removes the item
// at this position.
w.erase(begin, end) // Removes all elements from begin up to (but not including) *end,
// i.e., the left-inclusive interval [begin...end).
w.erase(i, len) // (Vector only) Removes up to len elements starting at w[i].
w.front() // Returns a reference to the first element of the sequence.
w.back() // Returns a reference to the last element of the sequence.
w.pop_back() // Removes the final element of w.
w.push_back(element) // Appends the specified element to the end of w.
w.pop_front() // Removes the first element of w.
w.push_front(element) // Inserts the specified element to the front of w.
w.reserve(amount) // (Vector only) Requests that the capacity of w be increased to the
// amount. (Unlike the string, this will never reduce the capacity.)
w.resize(n, element) // Changes the length of w to n (if this increases the
// length, new items are the specified element).
w.resize(n) // Changes the length of w to n (if this increases the length, new
// items are the default value of the Item type).
```

## 返回迭代器的函数：

```
w.begin() // Returns an iterator that is positioned at the start of w.
w.end() // Returns an end iterator (just beyond the last item of w).
w.rbegin() // Returns a reverse iterator that is positioned at the last item of w.
w.rend() // Returns a reverse end iterator (just before the first item of w).
```

## 来自 <map> 的映射和多重映射

来自 <map> 的 map<Key, Item> 和 multimap<Key, Item> 模板类允许程序员存储一组项目，其中每个项目都有一个关联的键，类似于第 12 章中的哈希表（但存储方式不同，取决于键由小于运算符排序）。map 最多只能为任何给定键包含一个不同的项目，而 multimap 允许具有相同键的许多不同项目。map 和 multimap 具有类似于 set 的各种成员函数，但它们还允许独特的映射操作，如下所述：

## 插入带有特定键的项目

要将带有键的项目 e 插入到映射 m 中，请写入 m[k] = e;。对于 multimap，语法更复杂：m.insert(multimap<xxx,yyy>::value_type(k,e));，其中 xxx 是键的类型，yyy 是项目的类型。

## 检索带有特定键的项目：

与键 k 关联的项目可以使用 m[k] 表示法从映射中检索，例如：cout << m[k];。对于 multimap，可以通过多种方式获取所有具有指定键 k 的项目序列。Lippmann 和 Lajoie 采用的一种方法是使用 count 和 find 函数，如下所示（其中 it 是 multimap m 的迭代器）：

```
int i = m.count(k);
it = m.find(k);
for (i = 0; i < many; ++i, ++it)
// Do something with *it
```

