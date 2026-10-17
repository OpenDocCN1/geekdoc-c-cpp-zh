
> 在对 `deque`、`string` 或 `vector` 进行插入或删除元素的循环中，不要缓存 `end()` 返回的迭代器。

与其存储 `end()` 迭代器，我们必须在每次插入后重新计算它：

```
// 更安全：当循环添加/删除元素时，每次都重新计算 end
while (begin != v.end()) {
    // 进行一些处理
    ++begin; // 移动 begin，因为我们在这个元素之后插入
    begin = v.insert(begin, 42); // 插入新值
    ++begin; // 移动 begin 跳过我们刚刚添加的元素
}
```

## 9.4. `vector` 如何增长

为了支持快速随机访问，`vector` 的元素是连续存储的——每个元素都与前一个元素相邻。通常情况下，我们不应该关心库类型是如何实现的；我们关心的是如何使用它。然而，在 `vector` 和 `string` 的情况下，部分实现细节泄露到了接口中。

鉴于元素是连续的，且容器的大小是灵活的，请考虑一下当我们向 `vector` 或 `string` 添加元素时会发生什么：如果没有空间存放新元素，容器不能直接在内存的某处添加元素——元素必须是连续的。容器必须分配新内存来存放现有元素加上新元素，将元素从旧位置移动到新空间，添加新元素，并释放旧内存。如果 `vector` 在每次添加元素时都进行这种分配和释放，性能将变得无法接受地缓慢。

## 9.3.6 节练习题

**练习 9.31：** 第 354 页用于删除偶值元素并删除重复奇值元素的程序在 `list` 或 `forward_list` 上无法运行。为什么？修改程序使其也能在这些类型上正常运行。

**练习 9.32：** 在第 354 页的程序中，如下所示的 `insert` 调用是合法的？如果不合法，为什么？

```
iter = vi.insert(iter, *iter++);
```

**练习 9.33：** 在本节最后的示例中，如果我们不将 `insert` 的结果赋值给 `begin`，会发生什么？编写一个省略此赋值的程序，看看你的预期是否正确。

**练习 9.34：** 假设 `vi` 是一个包含偶奇值的 `int` 容器，预测以下循环的行为。在分析完此循环后，编写一个程序测试你的预期是否正确。

```
iter = vi.begin();
while (iter != vi.end())
  if (*iter % 2)
    iter = vi.insert(iter, *iter);
  ++iter;
```

为了避免这些代价，库的实现者使用了分配策略来减少容器重新分配的次数。当它们必须获取新内存时，`vector` 和 `string` 的实现通常会分配超出当前需求所需的容量。容器保留这些存储空间作为备用，并在添加新元素时使用它们来分配内存。因此，不需要为每个新元素都重新分配容器。

这种分配策略比每次添加元素时都重新分配容器要高效得多。事实上，它的性能足够好，使得在实践中，`vector` 的增长通常比 `list` 或 `deque` 更高效，尽管 `vector` 在每次重新分配内存时都必须移动它的所有元素。

### 管理容量的成员

`vector` 和 `string` 类型提供了表 9.10 所示的成员，允许我们与实现的内存分配部分进行交互。`capacity()` 操作告诉我们容器在必须分配更多空间之前可以容纳多少元素。`reserve` 操作允许我们告诉应该准备容纳多少元素。

表 9.10 容器大小管理

| 成员 | 描述 |
| :--- | :--- |
| `size()` | 返回容器中当前的元素数量 |
| `capacity()` | 返回容器在必须分配更多空间之前可以容纳的元素数量 |
| `reserve(n)` | 告诉容器应该准备容纳 `n` 个元素 |
| `shrink_to_fit()` | 请求容器将其容量减小到与其大小相等 |

> `reserve` 不改变容器中的元素数量；它只影响 `vector` 预留的内存。

只有当请求的大小超过当前容量时，`reserve` 改变容量。如果请求的大小大于当前容量，`reserve` 分配至少（也可能更多）请求量。

如果请求的大小小于或等于现有容量，`reserve` 什么都不做。结果是调用 `reserve` 永远不会减少容器使用的内存。因此，调用 `reserve` 后，容量将大于或等于传入的参数。

在新的库中，我们可以调用 `shrink_to_fit()` 请求 `deque`、`vector` 或 `string` 返回多余内存。然而，实现可以忽略这个请求。无法保证调用 `shrink_to_fit()` 会返回内存。

### `capacity` 和 `size`

理解 `capacity` 和 `size` 之间的区别非常重要。容器的大小是已有的元素数量；它的容量是在分配更多空间之前它可以容纳的数量。

以下代码展示了 `size` 和 `capacity` 之间的交互：

```
vector<int> ivec;
// size 应该是 0；容量取决于实现
cout << "ivec: size: " << ivec.size()
  << " capacity: " << ivec.capacity() << endl;
// 给 ivec 添加 24 个元素
for (vector<int>::size_type ix = 0; ix != 24; ++ix)
    ivec.push_back(ix);

// size 应该是 24；容量将 >= 24 且取决于实现
cout << "ivec: size: " << ivec.size()
  << " capacity: " << ivec.capacity() << endl;
```

在我们的系统上运行时，这段代码产生如下输出：

`ivec size: 0 capacity: 0`

`ivec size: 24 capacity: 32`

我们知道空 `vector` 的 `size` 为 0，显然我们的库也将空 `vector` 的容量设为 0。当我们向 `vector` 添加元素时，`size` 和 `capacity` 会随之改变。

# 练习 9.38：编写一个程序来探索你使用的库中向量是如何增长的。

# 练习 9.39：解释以下代码段的作用：

```
vector<string> svec;
svec.reserve(1024);
string word;
while (cin >> word)
    svec.push_back(word);
svec.resize(svec.size() + svec.size()/2);
```

# 练习 9.40：如果上一个练习读取了 256 个单词，在调整大小后可能的容量（capacity）是多少？如果读取了 512 个、1,000 个、1,048 个呢？

## 9.5. 额外的字符串操作

`string` 类型除了常见的顺序容器外还提供了许多额外操作。在大多数情况下，这些额外操作要么支持 `string` 类与 C 风格字符数组之间的紧密交互，要么增加了允许使用索引代替迭代器的版本。

`string` 库定义了大量的函数。幸运的是，这些函数使用了重复的模式。鉴于支持的函数数量，这一节在初读时可能会令人枯燥；因此读者可能想快速浏览一遍。一旦你了解了有哪些可用操作，可以在需要使用特定操作时再回来查看细节。

### 9.5.1. 构建字符串的其他方式

除了我们在 § 3.2.1（第 84 页）中涵盖的构造函数，以及 `string`与其他顺序容器共享的构造函数（表 9.3，第 335 页）之外，`string` 类型还支持表 9.11 中描述的三个构造函数。

# 表 9.11. 构建字符串的其他方式

| n, len2 和 pos2 均为无符号值 | | |
| :--- | :--- |
| `string s(cp, n);` | `s` 是数组中前 `n` 个字符到 `cp` 指向点的拷贝。数组必须要有 `n` 个字符。 |
| `string s(s2, pos2);` | `s` 是字符串 `s2` 中从索引 `pos2` 开始的字符的拷贝。如果 `pos2 > s2.size()` 则行为未定义。 |
| `string s(s2, pos2, len2);` | `s` 是从 `s2` 索引 `pos2` 开始的 `len2` 个字符的拷贝。如果 `pos2 > s2.size()` 则行为未定义。无论 `len2` 的值如何，最多拷贝 `s2.size() - pos` 个字符。 |

接受 `string` 或 `const char*` 的构造函数带有额外的（可选的）参数，用于指定要拷贝多少字符。当我们传递一个字符串时，还可以指定开始拷贝的索引：

```
const char *cp = "Hello World!!!"; // 空字符终止数组
char null1[] = {'H', 'I'}; // 未空字符终止
string s1(cp); // 拷贝 cp 直到空字符处；s1 = "Hello World!!!"
string s2(null1, 2); // 从无空字符处拷贝两个字符；s2 = "Hi"
string s3(null0); // 未定义：未空字符终止
string s4(cp + 6, 5); // 从 cp[6] 开始拷贝 5 个字符；s4 = "World"
string s5(s1, 6, 5); // 从 s1[6] 开始拷贝 5 个字符；s5 = "World"
string s6(s1, 6); // 从 [6] 拷贝到 s1 的末尾；s6 = "World!!!"
string s7(s1, 6, 20); // 可以，只拷贝到 s1 的末尾；s7 = "World"
string s8(s1, 16); // 抛出 out_of_range 异常
```

当我们从 `const char*` 创建字符串时，指针所指向的数组必须是空字符终止的；拷贝 `cp` 直到空字符。如果我们不传递 `count` 且没有空字符，或者给定的 `count` 大于数组的大小，则操作是未定义的。当我们从一个字符串拷贝时，可以提供可选的位置和 `count`。起始位置必须小于或等于给定字符串的大小。如果位置大于字符串的大小，构造函数会抛出 `out_of_range` 异常。无论我们请求多少个字符，库都会拷贝到字符串的大小，而不会更多。

### `substr` 操作

表 9.12 中描述的 `substr` 操作返回原始字符串的一部分或全部。我们可以传递一个可选的位置和 `count`：

```
string s("hello world"); // s
string s2 = s.substr(0, 5);      // s2 = hello
string s3 = s.substr(6);          // s3 = world
string s4 = s.substr(6, 11);     // s3 = world
string s5 = s.substr(12);         // 抛出 out_of_range 异常
```

# 表 9.12. 子string 操作

| `s.substr(pos, n)` | 返回从 `pos` 开始的 `n` 个字符的字符串。`pos` 默认为 0，`n` 默认为拷贝字符串中从 `pos` 开始的所有字符。如果位置超过字符串的大小，`substr` 函数会抛出 `out_of_range` 异常（§ 5.6，第 193 页）。`count` 被调整为拷贝到字符串末尾。 |

### 练习 9.5

- 练习 41：编写一个从 `vector<char>` 初始化字符串的程序。
- 练习 42：假设你想一次读取一个字符到字符串中，并且知道你需要至少读取 100 个字符，你如何改进你程序的性能？

## 9.5.2. 修改字符串的其他方式

`string` 类型支持顺序容器的赋值运算符、`assign`、`insert` 和 `erase`（§ 2.5，第 337 页，§ 9.3.1，第 342 页和 § 9.3.3）。它还定义了 `insert` 和 `erase` 的额外。除了接受迭代器的 `insert` 和 `erase` 版本外，`string` 还提供了接受的版本。索引指示要删除的起始元素或插入的位置：

```
s.insert(s.size(), 5, '!'); // 在 s 的末尾插入5 个感叹号
s.erase(s.size() - 5, 5); // 删除 s 的最后五个字符
```

`string` 库还提供了 C 风格数组的 `insert` 和 `assign` 版本。例如，我们可以使用空字符终止字符数组作为插入或赋值到字符串的值：

```
const char *cp = "Stately, plump";
s.assign(cp, 7);             // s == "Stately"
s.insert(s.size(), cp + 7); // s == "Stately, plump"
```

这里首先通过调用 `assign` 替换字符串的内容。赋值给 `s` 的字符是从 `cp` 指向的字符开始到 `s[size()]`（不存在的）元素。在这种情况下，我们拷贝 `cp` 直到终止空字符。我们还可以指定插入或赋值的字符来自另一个字符串或其子string：

```
string s = "some string", s2 = "other string";
s.insert(0, s2);             // 在 s 的位置 0 之前插入 s2 的拷贝
s.insert(0, s2, s2.size()); // 从 s2[0] 开始从 s2 插入 s2.size() 个字符
```

`string` 类定义了两个额外的成员 `append` 和 `replace`，可以改变字符串的内容。`append` 操作是在末尾插入的快捷方法：表 9.13 总结了这些函数：

```
string s("C++ Primer"), s2 = s; // 初始化 s 和 s2 为 "C++ Primer"
s.insert(s.size(), "4th Ed."); // s == "C++ Primer 4th Ed."
s2.append("4th Ed."); // 等价：将 "4th Ed." 添加到 s2；s == s2
```

# 表 9.13. 修改字符串的操作

| C++ Primer, Fifth Edition | |
| :--- | :--- |
| `s.insert(pos, args)` | 在 `pos` 之前插入由 `args` 指定的字符。`pos` 可以索引或迭代器。接受索引的版本返回 `s` 的引用；接受迭代器的返回表示第一个插入字符的迭代器。 |
| `s.erase(pos, len)` | 从位置开始删除 `len` 个字符。如果省略 `len`，则删除从 `pos` 到 `s` 末尾的字符。返回 `s` 的引用。 |
| `s.assign(args)` | 根据 `args` 替换字符。返回 `s` 的引用。 |
| `s.append(args)` | 将 `args` 添加到 `s`。返回 `s` 的引用。 |
| `s.replace(range, args)` | 从 `s` 中移除范围字符并用 `args` 形成的字符替换它们。`range` 是索引和长度或迭代器对。返回 `s` 的引用。 |

调用 `replace` 时，我们插入的文本恰好与移除的文本相同。我们可以插入更大或更小的字符串：

```cpp
s.replace(11, 3, "Fifth"); // s == "C++ Primer Fifth Ed."
```
