

下面有几个示例：

```cpp
string test("The");
test.append("ory");  // test is "Theory"
test.append(3, '!'); // test is "Theory!!!"
```

`operator+()` 函数被重载以支持字符串拼接。这些重载函数不会修改某个字符串；相反，它们会创建一个新字符串，该字符串由一个字符串追加到另一个字符串后构成。这些加法函数不是成员函数，它们允许你将一个 string 对象加到另一个 string 对象上、将一个字符串数组加到一个 string 对象上、将一个 string 对象加到一个字符串数组上、将一个字符加到一个 string 对象上，以及将一个 string 对象加到一个字符上。下面是一些示例：

```cpp
string s1("red");
string s2("rain");
string s3 = s1 + "uce";  // s3 is "reduce"
string s4 = 't' + s2;    // s4 is "train"
string s5 = s1 + s2;     // s5 is "redrain"
```

## 更多赋值方法

除了基本的赋值运算符之外，string 类还提供 `assign()` 方法，这些方法允许你将一个完整字符串、字符串的一部分或一串相同字符赋给一个 string 对象。下面是各种 `assign()` 方法的原型：

```cpp
basic_string& assign(const basic_string& str);
basic_string& assign(basic_string& str) noexcept;  // C++11
basic_string& assign(const basic_string& str, size_type pos,
                     size_type n);
basic_string& assign(const charT* s, size_type n);
basic_string& assign(const charT* s);
basic_string& assign(size_type n, charT c); // assign n copies of c
template<class InputIterator>
    basic_string& assign(InputIterator first, InputIterator last);
basic_string& assign(initializer_list<charT>);  // C++11
```

下面有几个示例：

```cpp
string test;
string stuff("set tubs clones ducks");
test.assign(stuff, 1, 5);   // test is "et tu"
test.assign(6, '#');        // test is "######"
```

带右值引用的 `assign()` 方法（由 C++11 添加）支持移动语义，而第二个新增的 `assign()` 方法允许将一个 `initializer_list` 赋给一个 string 对象。

## 插入方法

`insert()` 方法允许你将一个 string 对象、一个字符串数组、一个字符或若干字符插入到一个 string 对象中。这些方法类似于 `append()` 方法，不同之处在于它们多接受一个参数，用于指明在何处插入新内容。该参数可以是一个位置或一个迭代器。内容会插入到插入点之前。其中几个方法返回对结果字符串的引用。如果 `pos1` 超出目标字符串末尾，或者 `pos2` 超出要插入的字符串末尾，则该方法抛出 `out_of_range` 异常。如果结果字符串将大于最大大小，则该方法抛出 `length_error` 异常。下面是各种 `insert()` 方法的原型：

```cpp
basic_string& insert(size_type pos1, const basic_string& str);  
basic_string& insert(size_type pos1, const basic_string& str,  
                     size_type pos2, size_type n);  
basic_string& insert(size_type pos, const char* s, size_type n);  
basic_string& insert(size_type pos, const char* s);  
basic_string& insert(size_type pos, size_type n, char c);  
iterator insert(const_iterator p, charT c);  
iterator insert(const_iterator p, size_type n, charT c);  
template<class InputIterator>  
  void insert(iterator p, InputIterator first, InputIterator last);  
iterator insert(const_iterator p, initializer_list<charT> il); // C++11
```

例如，下面的代码将字符串 `"former "` 插入到 `"The banker."` 中的 `b` 之前：

```cpp
string st3("The banker.");  
st3.insert(4, "former ");
```

然后，下面的代码将字符串 `" waltzed"`（不包括 `\0`，它将是第九个字符）插入到 `"The former banker."` 末尾的句点之前：

```cpp
st3.insert(st3.size() - 1, " waltzed!", 8);
```

## 删除方法

`erase()` 方法从字符串中删除字符。下面是它们的原型：

```cpp
basic_string& erase(size_type pos = 0, size_type n = npos);  
iterator erase(const_iterator position);  
iterator erase(const_iterator first, iterator last);  
void pop_back();
```

第一种形式从位置 `pos` 开始删除字符，直到其后 `n` 个字符处或字符串末尾（以先到者为准）。第二种形式删除迭代器 `position` 所引用的单个字符，并返回指向下一个元素的迭代器；如果没有更多元素，则返回 `end()`。第三种形式删除范围 `[first, last)` 中的字符；也就是说，包括 `first`，直到但不包括 `last`。该方法返回指向最后一个被删除元素之后的元素的迭代器。最后，`pop_back()` 方法删除字符串中的最后一个字符。

### 替换方法

各种 `replace()` 方法会确定要替换的字符串部分，并确定替换内容。要替换的部分可以通过起始位置和字符数来确定，也可以通过迭代器范围来确定。替换内容可以是一个 string 对象、一个字符串数组，或重复若干次的特定字符。替换用的 string 对象和数组还可以进一步限定，具体做法是指明一个特定部分：使用位置和计数、仅使用计数，或使用迭代器范围。下面是各种 `replace()` 方法的原型：

```cpp
basic_string& replace(size_type pos1, size_type n1, const basic_string& str);
basic_string& replace(size_type pos1, size_type n1, const basic_string& str,
                      size_type pos2, size_type n2);
basic_string& replace(size_type pos, size_type n1, const charT* s,
                      size_type n2);
basic_string& replace(size_type pos, size_type n1, const charT* s);
basic_string& replace(size_type pos, size_type n1, size_type n2, charT c);
basic_string& replace(const_iterator i1, const_iterator i2,
                      const basic_string& str);
basic_string& replace(const_iterator i1, const_iterator i2,
                      const charT* s, size_type n);
basic_string& replace(const_iterator i1, const_iterator i2,
                      const charT* s);
basic_string& replace(const_iterator i1, const_iterator i2,
                      size_type n, charT c);
template<class InputIterator>
  basic_string& replace(const_iterator i1, const_iterator i2,
                        InputIterator j1, InputIterator j2);
basic_string& replace(const_iterator i1, const_iterator i2,
                      initializer_list<charT> il);
```

下面是一个示例：

```cpp
string test("Take a right turn at Main Street.");
test.replace(7, 5, "left"); // replace right with left
```

注意，你可以使用 `find()` 来查找 `replace` 中使用的位置：

```cpp
string s1 = "old";
string s2 = "mature";
string s3 = "The old man and the sea";
string::size_type pos = s3.find(s1);
if (pos != string::npos)
    s3.replace(pos, s1.size(), s2);
```

这个示例会将 `old` 替换为 `mature`。

## 其他修改方法：`copy()` 和 `swap()`

`copy()` 方法将一个 string 对象或其一部分复制到指定的字符数组中：

```cpp
size_type copy(char* s, size_type n, size_type pos = 0) const;
```

在这种情况下，`s` 指向目标数组，`n` 表示要复制的字符数，`pos` 表示从 string 对象中开始复制的位置。复制会进行 `n` 个字符，或直到 string 对象中的最后一个字符（以先到者为准）。该函数返回已复制的字符数。该方法不会追加空字符，并且需要程序员确保数组足够大以容纳副本。

> **注意**
>
> `copy()` 方法不会追加空字符，也不会检查目标数组是否足够大。

`swap()` 方法使用常数时间算法交换两个 string 对象的内容：

```cpp
void swap(basic_string& str);
```

## 输出与输入

string 类重载了 `<<` 运算符以显示 string 对象。它返回对 `iostream` 对象的引用，以便输出可以串联：

```cpp
string claim("The string class has many features.");
cout << claim << endl;
```

string 类重载了 `>>` 运算符，以便你可以将输入读入 string：

```cpp
string who;
cin >> who;
```

输入会在以下情况下终止：到达文件尾、读取到字符串中允许的最大字符数，或遇到空白字符。（空白字符的定义取决于字符集以及 `char` 所表示的类型。）

