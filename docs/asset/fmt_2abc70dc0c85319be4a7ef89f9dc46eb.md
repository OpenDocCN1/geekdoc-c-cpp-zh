
## C 字符串的问题

尽管 C++ 字符串提供了一种使用字符串的方法，但它们比 C++ 字符数组更容易出错，且不够健壮。我们建议尽可能使用 C++ 字符串。我们将在下一节中讨论 C++ 字符串。

## 10.2 C++ string 类

C++ 库提供了一个名为 *string* 的类，与 C++ 字符数组相比，它的对象通常被称为 C++ 字符串。要使用该类的对象和成员函数，你必须在程序中包含头文件 `<string>`。

C++ 字符串库定义了一个类，而 C 字符串库定义了字符数组。当在处理 C 字符串时，我们必须创建一个数组并应用在`<string>` 库中定义的函数。当使用 C++ 字符串时，我们可以构造一个字符串对象，并使用`<string>` 库中预定义的成员函数对它进行操作。我们强烈建议尽可能使用 C++ 字符串。

| 要使用 C++ 字符串，我们需要 <string> 头文件。 |

### 10.2.1 通用设计思想

为了理解字符串类是如何运作的，我们必须考虑用户在设计字符串时喜好的通用概念。字符串类具有私有数据成员和公共成员函数来操作字符串对象。通常情况下，数据包含一个指向字符数组的指针。其他数据成员通常在栈上创建，但字符数组本身分配在堆上，因为它的大小直到运行时才被定义。虽然 C++ 字符串可以被视作字符数组，但它并不像我们在 C 字符串中看到的那样有终止。图 10.7 显示了 C++ 字符串的概览。

> C++ 字符串是一个字符数组，但它不是空字符终止的。

![](img/ce9c99d45f71111839bc062830bd19fd_478_0.png)

- 注意：
1. C++ 字符串不是终止的。
2. 大小（size）必须小于或等于容量（capacity）。
3. 头部位于索引 0。
4. 尾部位于索引 (size – 1)。

图 10.7 C++ 字符串对象的通用设计

## 10.2 C++ 字符串类

在讨论每个成员函数之前，我们先讨论库中使用的元数据类型和常量：`size_type` 和 `npos`。我们用不同的颜色显示它们，以强调它们不是基本类型；它们是在库中使用基本类型创建的定义。`size_type` 是一个无符号整数。它的定义是为了防止出现负数整数大小，因为它有两个用途：它是字符数组的索引，并且它包含一组字符的计数；在两种情况下，该值都不能为负数。`npos` 是一个 `size_type`，其值被设置为 -1。`npos` 用于表示我们在正向移动时越过了最后一个元素，或者在反向移动时越过了第一个元素。换句话说，它是一个不存在的索引。这两个标识符定义在 `std::string` 命名空间中。我们在程序中使用它们时，必须像下面所示使用它们的名称进行限定：

```cpp
string::size_type length;
string::npos;
```

### 10.2.2 C++ 字符串库

在讨论库中的成员函数之前，我们先给出它们的原型（表 10.2）：

| 表 10.2 C++ 库的选成员 |
| :--- |
| // 构造函数 |
| string::() |
| string(size_type count, char c) |
| string(const char* cstr) |
| string(const char* cstr, size_type count) |
| // 析构函数 |
| string::~string() |
| // 拷贝构造函数 |
| string(const string& strg) |
| string(const string& strg, size_type index, size_type length = npos) |
| // 与大小和容量相关的操作 |
| size_type::size() const |
| size_type::max_size() const |
| void::resize(size_type n, char c) |
| size_type::capacity() const |
| void::reserve(size_type n = 0) |
| bool::empty() const |
| // 输入和输出 |
| istream& operator>(ostream& in, const string& strg) |
| ostream& operator<<(ostream& out, const string& strg) |
| (续) |

| 表 10.2 C++ 库的选成员（续） |
| :--- |
| istream& getline(istream& in, string& strg) |
| istream& getline(istream& in, string& strg, char delim) |

```cpp
// 根据给定位置访问字符
const char& string::operator[](size_type pos) const
char& string::operator[](size_type pos) const
const char& string::at(size_type pos) const
char& string::at(size_type pos) const
```

```cpp
// 根据第一个字符的位置和长度访问子字符串
string string::substr(size_type pos, size_type length = npos) const
```

```cpp
// 查找给定字符的位置（正向或反向搜索）
size_type string::find(char c, size_type index = 0) const
size_type string::rfind(char c, size_type index = npos) const
```

```cpp
// 查找不在集合中的字符的位置（正向或反向搜索）
size_type string::find_not_of(const char* s, size_type index = 0) const
size_type string::rfind_not_of(const char* s, size_type index = npos) const
// 查找集合中第一个出现的字符的位置
size_type string::find_first_of(const char* s, size_type index = 0) const
size_type string::find_last_of(const char* s, size_type index = npos) const
```

```cpp
// 比较字符串
int string::compare(const string& str) const
int string::compare(const char* cstr) const
int string::compare(const char* cstr, size_type count) const
// 逻辑比较
bool operator==(const string& str) const
bool operator!=(const string& str) const
bool operator<(const string& str) const
bool operator<=(const string& str) const
bool operator>(const string& str) const
bool operator>=(const string& str) const
// 赋值相关的赋值运算符
string& operator+=(const string& str)
string& operator+=(const char* cstr)
string& operator+=(const char* cstr, size_type count)
string
// 拼接运算符
string operator+(const string& str1, const string& str2)
string operator+(const string& str1, const char* cstr)
string operator+(const char* cstr, const string& str2)
string operator+(const char* cstr1, const char* cstr2)
// 复合赋值
string& operator-=(const string& str)
string& operator-=(const char* cstr)
// 拼接运算符
string operator+=(const char* cstr, const char* cstr, size_type count)
// 复合赋值
string operator*=(const string& str1, const string& str2)
string operator*=(const string& str1, const char* cstr)
string operator*=(const char* cstr, const string& str2)
string operator*=(const char* cstr1, const char* cstr2)
// 赋值运算符
string& operator=(const string& str)
string& operator=(const char* cstr)
string& operator=(const char* cstr, size_type count)
// 交换
void swap(string& str1, string& str2)
// 改变字符串
void string::clear()
void string::erase(size_type pos)
void string::erase(size_type pos, size_type len)
void string::erase(const_iterator pos)
void string::erase(const_iterator first, const_iterator last)
bool string::empty() const
size_type string::size() const
size_type string::capacity() const
size_type string::max_size() const
const char* string::c_str() const
void string::resize(size_type n, char c = ' ')
void string::reserve(size_type n = 0)
void string::replace(size_type pos, size_type len, const string& str)
void string::replace(size_type pos, size_type len, const char* cstr)
void string::replace(size_type pos, size_type len, char c)
void string::insert(size_type pos, const string& str)
void string::insert(size_type pos, const char* cstr)
void string::insert(size_type pos, char c, size_type count)
// 查找
size_type string::find(char c, size_type index = 0) const
size_type string::rfind(char c, size_type index = npos) const
size_type string::find_first_of(const char* s, size_type index = 0) const
size_type string::find_last_of(const char* s, size_type index = npos) const
size_type string::find_first_not_of(const char* s, size_type index = 0) const
size_type string::find_last_not_of(const char* s, size_type index = npos) const
// 子字符串
string string::substr(size_type pos, size_type len = npos) const
// 迭代器
iterator begin()
iterator end()
const_iterator begin() const
const_iterator end() const
```

*(注：由于原文文本中部分函数原型存在截断或格式错误，如 `string; ::operator[]` 应为 `string::operator[]`，翻译时已根据标准逻辑进行了修正补全以确保文档可读性)*

### 10.2.3 用于 C++ 字符串的操作

我们简要描述在 10.2 中定义的操作。

#### 构造

C++ 字符串定义了一个默认构造函数和三个构造函数。

默认构造函数如 10.2 所示，它创建一个空字符串。

```cpp
string str; // 创建空字符串
```

构造函数除了默认构造函数外，字符串类允许我们通过三种方式创建字符串，如 10.2 所示。我们可以使用相同的值、字符串面量或字符串面量的一部分。

```cpp
string str1(5, 'a'); // 创建5个 'a'
string str2("hello"); // 创建 "hello"
string str3("hello", 2); // 创建 "he"
```

#### 析构

字符串类的析构函数简单的删除在堆上创建的数组并弹出栈成员。

```cpp
{
    string str("hello");
} // str 被析构，内存释放
```

## 容量与预留

`capacity` 函数返回字符数组的当前容量。如果我们没有进行过预留，容量与大小相同。我们可以调用 `reserve` 函数使容量大于大小。

```
size_type n = str.capacity(); // 获取容量
str.reserve(n); // 预留更大的数组
```

然而，这里存在一些限制。如果函数的参数小于大小，则不会发生任何操作（容量不能小于大小）。如果参数定义了较小的增加，系统可能会对其进行扩展。

空检查：`empty` 函数在大小为 0 时返回 `true`；否则，

```cpp
bool fact = str.empty(); // 检查是否为空
```
