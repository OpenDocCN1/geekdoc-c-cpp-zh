

## 第 12 章 类与动态内存分配

两种形式分配的内存量相同。区别在于第一种形式与类的析构函数兼容，而第二种则不兼容。回析构函数包含此代码：

```
delete [] str;
```

使用 `delete []` 与使用 `new []` 初始指针以及空指针兼容。另一种可能性可能是将

```cpp
str = new char[1];
str[0] = '\0'; // 默认字符串
```

替换为：

```
str = 0; // 将 str 设置为空指针
```

对任何通过其他方式初始化的内存使用 `delete []`，其效果是未定义的：

- * words [15] = "坏主意"
- char p1 = words;
- char p2 = new char;
- char p3;
delete [] p1; // 未定义，所以不要这样做
delete [] p2; // 未定义，所以不要这样做
delete [] p3; // 未定义，所以不要这样做

## C++11 空指针

在 C++98 中，字面量 `0` 有两个含义——它可以是数字 `0`，也可以是空指针——这使得读者和编译器难以区分两者。某些程序员使用 `(void *)` 来标识指针版本。（空指针本身可能有一个非零表示）。其他程序员使用 `NULL`（一个 C 宏）来表示空指针。然而，这证明是一个不完整的解决方案。C++11 通过引入新关键字 `nullptr`（空指针）提供了一个更好的解决方案。你仍然像以前一样使用 `0`——否则大量现有代码将失效——但从现在起，建议使用 `nullptr`：

```cpp
str = nullptr; // C++11 空指针表示法
```

## 比较方法

String 类中的三种方法执行比较。`operator<` 函数如果第一个字符串按字母顺序排在第二个之前（或更准确地说，在匹配的排序序列中），则返回 `true`。实现字符串比较函数的简单方法是使用标准的 `strcmp` 函数，如果它的第一个参数在字母顺序上先于第二个，它返回负值；如果字符串相同，返回 0；如果第一个在字母顺序上后第二个，则返回正值。你可以这样使用 `strcmp()`：

```cpp
bool operator<(const String& s1, const String& s2)
{
  if (std::strcmp(str1.str, str2.str) < 0)
```

## 新的改进型 String 类

```cpp
return true;
else
  return false;
}
```

由于内置的 `<` 运算符已经返回 `bool` 类型值，你可以将代码进一步简化为：

```cpp
bool operator<(const String&st1, const String&st2)
{
  return (std::strcmp(st1.str, st2.str) < 0);
}
```

同样，你可以这样编写另外两个比较函数：

```cpp
bool operator>(const String&st1, const String&st2)
{
  return st2 < st1;
}
bool operator=(const String&st1, const String&st2)
{
  return (std::strcmp(st1.str, st2.str) == 0);
}
```

第一版在 `<` 运算符中表达 `>` 运算符，这作为内联函数是一个很好的选择。
将比较函数声明为 `friend`（友元）有助于 String 对象与普通 C 字符串之间的比较。例如，假设 `answer` 是一个 String 对象，并且你有如下代码：

```cpp
if ("love" == answer)
```

这被翻译为如下：
if (operator==("love", answer))
编译器使用其中一个构造函数来转换代码，实际上相当于：
if (operator==(String("love", answer))
这与原型相匹配。

## 使用括号表示法访问字符

对于 C 风格字符串，你可以使用括号访问单个字符：
```cpp
char city[40] = "Amsterdam";
cout << city[0] << endl; // 显示字母 A
```

在 C++ 中，两个括号符号构成单个运算符，即下标运算符，你可以通过名为 `operator[]()` 的方法来重载此运算符。通常，二元 C++ 运算符（具有两个操作数的运算符）将运算符放在两个操作数之间，如 `2 + 5`。但下标运算符将一个操作数放在第一个括号之前，另一个操作数放在两个括号之间。因此，在表达式 `city[0]` 中，`city` 是第一个操作数，`[]` 是运算符，`0` 是第二个操作数。

假设 `opera` 是一个 String 对象：

```cpp
String opera("The Magic Flight");
```

如果你使用表达式 `opera[4]`，C++ 会查找具有此名称和签名名的方法：

```cpp
String::operator[] (int i)
```

如果找到了匹配的原型，编译器会将表达式 `opera[4]` 替换为此函数调用：

```cpp
opera.operator[] (4)
```

`opera` 对象调用该方法，数组下标 4 变成函数参数。

这是一个简单的实现：

```cpp
char & String::operator[] (int i)
{
    return str[i];
}
```

有了此定义，语句 `cout << opera[4];` 变为 `cout << opera.operator[][4];`

返回值是 `opera.str[4]`，即字符 'M'。因此，公共方法提供了访问私有数据的权限。

将返回类型声明为 `char &` 允许你为特定元素赋值。例如，你可以使用：

第二个语句转换为 `means.operator[](0] = 'r';`

返回值是 `opera.str[4]`，即字符 'M'。因此，公共方法提供了访问私有数据的权限。

将返回类型声明为 `char &` 允许你为特定元素赋值。例如，你可以使用：

第二个语句转换为 `means.operator[](0] = 'r';`

返回值是 `opera.str[4]`，即字符 'M'。因此，公共方法提供了访问私有数据的权限。

将返回类型声明为 `char &` 允许你为特定元素赋值。例如，你可以使用：

第二个语句转换为 `means.operator[](0] = 'r';`

返回值是 `opera.str[4]`，即字符 'M'。因此，公共方法提供了访问私有数据的权限。

将返回类型声明为 `char &` 允许你为特定元素赋值。例如，你可以使用：

第二个语句转换为 `means.operator[](0] = 'r';`

返回值是 `opera.str[4]`，即字符 'M'。因此，公共方法提供了访问私有数据的权限。

