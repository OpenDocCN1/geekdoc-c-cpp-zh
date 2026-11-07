

## 使用 n 个字符副本的构造函数

使用 n 个字符副本的构造函数会创建一个字符串对象，该对象由 n 个连续字符组成，且每个字符的值都为 c：

```cpp
basic_string(size_type n, charT c, const Allocator& a = Allocator());
```

此构造函数要求 n < npos。如果 n 等于 npos，构造函数会抛出 `out_of_range` 异常。否则，在调用构造函数后，以下关系成立：

- `data()` 方法返回一个指针，指向由 n 个元素组成的字符串的第一个元素，且每个元素都被设置为 c。
- `size()` 方法返回 n。
- `capacity()` 方法返回一个至少与 `size()` 一样大的值。

## 使用范围的构造函数

使用范围的构造函数采用 STL 风格的、由迭代器定义的范围：

```cpp
template<class InputIterator>
basic_string(InputIterator begin, InputIterator end,
            const Allocator& a = Allocator());
```

begin 迭代器指向源中开始复制的元素，end 指向要复制范围最后一个位置的下一个位置。

你可以将此形式用于数组、字符串或 STL 容器：

```cpp
char cole[40] = "Old King Cole was a merry old soul.";
string title(cole + 4, cole + 8);
vector<char> input;
char ch;
while (cin.get(ch) && ch != '\n')
    input.push_back(ch);
string str_input(input.begin(), input.end());
```

在第一次使用中，InputIterator 被推导为 `const char *` 类型。在第二次使用中，InputIterator 被推导为 `vector<char>::iterator` 类型。

调用构造函数后，以下关系成立：

- `data()` 方法返回一个指针，指向通过复制 `[begin, end)` 范围内的元素所形成的字符串的第一个元素。
- `size()` 方法返回 begin 与 end 之间的距离。（距离的单位等于对迭代器解引用后所得数据类型的大小。）
- `capacity()` 方法返回一个至少与 `size()` 一样大的值。

## 使用初始化列表的构造函数（C++11）

此构造函数接受一个 `initializer_list<char>` 参数：

```cpp
basic_string(initializer_list<char> il, const Allocator& a = Allocator());
```

你可以将它与字符的花括号列表配合使用：

```cpp
string snail({'s', 'n', 'a', 'i', 'l'});
```

这不是初始化字符串最方便的方式，但它使字符串接口与 STL 容器类的接口保持相似。

`initializer_list` 类具有 `begin()` 和 `end()` 成员，使用此构造函数的效果与使用范围构造函数相同：

```cpp
basic_string(il.begin(), il.end(), a);
```

## 内存杂项

有几个方法用于处理内存，例如清除内存内容、调整字符串大小，或调整字符串容量。表 F.2 列出了一些与内存相关的方法。

表 F.2　一些与内存相关的方法

| 方法 | 作用 |
|---|---|
| `void resize(size_type n)` | 如果 `n > npos`，则抛出 `out_of_range` 异常。否则，将字符串大小更改为 `n`：当 `n < size()` 时截断字符串末尾；当 `n > size()` 时，使用 `charT()` 字符填充字符串。 |
| `void resize(size_type n, charT c)` | 如果 `n > npos`，则抛出 `out_of_range` 异常。否则，将字符串大小更改为 `n`：当 `n < size()` 时截断字符串末尾；当 `n > size()` 时，使用字符 `c` 填充字符串。 |
| `void reserve(size_type res_arg = 0)` | 将 `capacity()` 设置为大于或等于 `res_arg` 的值。由于此操作会重新分配字符串，因此之前指向该字符串的引用、迭代器和指针都会失效。 |
| `void shrink_to_fit()` | 请求将 `capacity()` 减小到 `size()`；此请求不具有强制性（C++11）。 |
| `void clear() noexcept` | 移除字符串中的所有字符。 |
| `bool empty() const noexcept` | 如果 `size() == 0`，则返回 `true`。 |

## 字符串访问

有四种访问单个字符的方法，其中两种使用 `[]` 运算符，另外两种使用 `at()` 方法：

```cpp
reference operator[](size_type pos);
const_reference operator[](size_type pos) const;
reference at(size_type n);
const_reference at(size_type n) const;
```

第一个 `operator[]()` 方法允许你使用数组表示法访问字符串中的单个元素；它既可以用于获取值，也可以用于修改值。第二个 `operator[]()` 方法可用于 const 对象，但只能用于获取值：

```cpp
string word("tack");
cout << word[0];    // 显示 t
word[3] = 't';    // 将 k 覆盖为 t
const string word("garlic");
cout << word[2];   // 显示 r
```

`at()` 方法提供类似的访问功能，不同之处在于索引以函数参数的形式提供：

```cpp
string word("tack");
cout << word.at(0);    // 显示 t
```

区别（语法上的区别）在于，`at()` 方法会进行边界检查，并且当 `pos >= size()` 时抛出 `out_of_range` 异常。注意，`pos` 的类型为 `size_type`，该类型是无符号的；因此，`pos` 不可能为负值。`operator[]()` 方法不进行边界检查，因此当 `pos >= size()` 时，行为是未定义的；但有一个例外：当 `pos == size()` 时，const 版本会返回与空字符等价的值。

因此，你可以在安全性（使用 `at()` 并检测异常）和执行速度（使用数组表示法）之间进行选择。

此外，还有一个函数会返回一个新的字符串，该字符串是原字符串的子字符串：

```cpp
basic_string substr(size_type pos = 0, size_type n = npos) const;
```

它返回一个字符串，该字符串是从位置 pos 开始、包含 n 个字符或一直到字符串末尾（以先到者为准）的原字符串副本。例如，下面的代码将 pet 初始化为 `"donkey"`：

```cpp
string message("Maybe the donkey will learn to sing.");
string pet(message.substr(10, 6));
```

C++11 增加了以下四种访问方法：

```cpp
const char& front() const;
char& front();
const char& back() const;
char& back();
```

`front()` 方法访问字符串的第一个元素，其行为类似于 `operator[]()`。`back()` 方法访问字符串的最后一个元素，其行为类似于 `operator[](size() - 1)`。

### 基本赋值

C++11 有五个重载的赋值方法，比 C++98 多两个：

```cpp
basic_string& operator=(const basic_string& str);
basic_string& operator=(const char* s);
basic_string& operator=(char c);
basic_string& operator=(basic_string&& str) noexcept;   // C++11
basic_string& operator=(initializer_list<char>);        // C++11
```

第一个方法将一个字符串对象赋值给另一个字符串对象；第二个方法将 C 风格字符串赋值给字符串对象；第三个方法将单个字符赋值给字符串对象；第四个方法使用移动语义，将右值字符串对象赋值给字符串对象；第五个方法允许使用初始化列表进行赋值。因此，下面所有操作都是可行的：

```cpp
string name("George Wash");
string pres, veep, source, join, awkward;
pres = name;
veep = "Road Runner";
source = 'X';
join = name + source;   // 现在使用移动语义！
awkward = {'C','l','o','u','d','s','a','u','r'};
```

### 字符串搜索

字符串类提供六个搜索函数，每个函数都有四种原型。下面各节将对它们进行简要介绍。

#### find() 系列

以下是 C++11 提供的 `find()` 原型：

```cpp
size_type find(const basic_string& str, size_type pos = 0) const noexcept;
size_type find(const char* s, size_type pos = 0) const;
size_type find(const char* s, size_type pos, size_type n) const;
size_type find(charT c, size_type pos = 0) const noexcept;
```

第一个成员函数返回 str 子字符串在调用对象中第一次出现的起始位置，搜索从位置 pos 开始。如果找不到该子字符串，此方法返回 npos。

下面的代码用于查找子字符串 `"hat"` 在较长字符串中的位置：

```cpp
string longer("That is a funny hat.");
string shorter("hat");
```

