
```cpp
size_type loc1 = longer.find(shorter);           // sets loc1 to 1
size_type loc2 = longer.find(shorter, loc1 + 1);  // sets loc2 to 16
```

因为第二次搜索从位置 2（That 中的 a）开始，所以它找到的第一次出现的 hat 位于字符串接近末尾处。要测试失败，可使用 string::npos 值：

```cpp
if (loc1 == string::npos)
    cout << "Not found\n";
```

第二种方法与上面相同，只不过它使用字符数组而不是 string 对象作为子字符串：

```cpp
size_type loc3 = longer.find("is");             // sets loc3 to 5
```

第三种方法与第二种相同，只不过它只使用字符串 s 的前 n 个字符。其效果等同于使用 basic_string(const charT* s, size_type n) 构造函数，并将所得对象作为第一种形式的 find() 的 string 参数。例如，下面的代码搜索子字符串 "fun"：

```cpp
size_type loc4 = longer.find("funds", 3);       // sets loc4 to 10
```

第四种方法与第一种相同，只不过它使用单个字符而不是 string 对象作为子字符串：

```cpp
size_type loc5 = longer.find('a');               // sets loc5 to 2
```

### `rfind()` 家族

rfind() 方法具有以下原型：

```cpp
size_type rfind(const basic_string& str,
                size_type pos = npos) const noexcept;
size_type rfind(const charT* s, size_type pos = npos) const;
size_type rfind(const charT* s, size_type pos, size_type n) const;
size_type rfind(charT c, size_type pos = npos) const noexcept;
```

这些方法的工作方式与类似的 find() 方法相同，只不过它们查找的是从位置 pos 处或之前开始的字符串或字符的最后一次出现。如果未找到子字符串，则该方法返回 npos。

下面的代码用于在较长字符串中查找子字符串 "hat" 的位置，从较长字符串的末尾开始：

```cpp
string longer("That is a funny hat.");
string shorter("hat");
size_type loc1 = longer.rfind(shorter);          // sets loc1 to 16
size_type loc2 = longer.rfind(shorter, loc1 - 1); // sets loc2 to 1
```

### find_first_of() 家族

find_first_of() 方法具有以下原型：

```cpp
size_type find_first_of(const basic_string& str,
                        size_type pos = 0) const noexcept;
size_type find_first_of(const charT* s, size_type pos, size_type n) const;
size_type find_first_of(const charT* s, size_type pos = 0) const;
size_type find_first_of(const charT* s, size_type pos = 0) const noexcept;
size_type find_first_of(charT c, size_type pos = 0) const noexcept;
```

这些方法的工作方式与对应的 find() 方法相同，只不过它们不是查找整个子字符串的匹配项，而是查找子字符串中任意单个字符的第一个匹配项：

```cpp
string longer("That is a funny hat.");
string shorter("fluke");
size_type loc1 = longer.find_first_of(shorter);   // sets loc1 to 10
size_type loc2 = longer.find_first_of("fat");     // sets loc2 to 2
```

在 longer 中，fluke 的五个字符中任意一个第一次出现的是 funny 中的 f。在 longer 中，fat 的三个字符中任意一个第一次出现的是 That 中的 a。

### find_last_of() 家族

find_last_of() 方法具有以下原型：

```cpp
size_type find_last_of(const basic_string& str,
                       size_type pos = npos) const noexcept;
size_type find_last_of(const charT* s, size_type pos, size_type n) const;
size_type find_last_of(const charT* s, size_type pos = npos) const;
size_type find_last_of(const charT* s, size_type pos = npos) const noexcept;
size_type find_last_of(charT c, size_type pos = npos) const noexcept;
```

这些方法的工作方式与对应的 rfind() 方法相同，只不过它们不是查找整个子字符串的匹配项，而是查找子字符串中任意单个字符的最后一个匹配项。

下面的代码用于在较长字符串中查找 "fluke" 中任意字母的最后一次和倒数第二次出现的位置：

```cpp
string longer("That is a funny hat.");
string shorter("hat");
size_type loc1 = longer.find_last_of(shorter);   // sets loc1 to 18
size_type loc2 = longer.find_last_of("any");     // sets loc2 to 17
```

在 longer 中，hat 的三个字母中任意一个的最后一次出现是 hat 中的 t。在 longer 中，any 的三个字符中任意一个的最后一次出现是 hat 中的 a。

### find_first_not_of() 家族

find_first_not_of() 方法具有以下原型：

```cpp
size_type find_first_not_of(const basic_string& str,
                            size_type pos = 0) const noexcept;
size_type find_first_not_of(const charT* s, size_type pos,
                            size_type n) const;
size_type find_first_not_of(const charT* s, size_type pos = 0) const;
size_type find_first_not_of(charT c, size_type pos = 0) const noexcept;
```

这些方法的工作方式与对应的 `find_first_of()` 方法相同，只不过它们搜索的是子字符串中不包含的任意字符的第一次出现。

下面的代码用于在较长字符串中查找不在 "This" 中的任意字母的前两次出现的位置：

```cpp
string longer("That is a funny hat.");
string shorter("This");
size_type loc1 = longer.find_first_not_of(shorter);  // sets loc1 to 2
size_type loc2 = longer.find_first_not_of("Thatch"); // sets loc2 to 4
```

That 中的 a 是 longer 中第一个未出现在 This 中的字符。较长字符串中的第一个空格是第一个未出现在 Thatch 中的字符。

### `find_last_not_of()` 家族

`find_last_not_of()` 方法具有以下原型：

```cpp
size_type find_last_not_of(const basic_string& str,
                           size_type pos = npos) const noexcept;
size_type find_last_not_of(const charT* s, size_type pos,
                           size_type n) const;
size_type find_last_not_of(const charT* s,
                           size_type pos = npos) const;
size_type find_last_not_of(charT c, size_type pos = npos) const noexcept;
```

这些方法的工作方式与对应的 `find_last_of()` 方法相同，只不过它们搜索的是子字符串中不包含的任意字符的最后一次出现。

下面的代码用于在较长字符串中查找不在 "This" 中的任意字母的最后两次出现的位置：

```cpp
string longer("That is a funny hat.");
string shorter("That.");
size_type loc1 = longer.find_last_not_of(shorter);       // sets loc1 to 15
size_type loc2 = longer.find_last_not_of(shorter, 10); // sets loc2 to 10
```

longer 中的最后一个空格是 longer 中最后一个未出现在 shorter 中的字符。较长字符串中的 f 是截至位置 10 所找到的、未出现在 shorter 中的最后一个字符。

## 比较方法和函数

string 类提供了用于比较两个字符串的方法和函数。首先，以下是这些方法的原型：

非成员比较函数是重载的关系运算符：

```cpp
operator==()
operator<()
operator<=()
operator>()
operator>=()
operator!=()
```

每个运算符都经过重载，因此可用于比较 string 对象与 string 对象、string 对象与 C 风格字符串，以及 C 风格字符串与 string 对象。这些运算符是依据 compare() 方法定义的，因此它们提供了一种在写法上更方便的比较方式。

## 字符串修饰符

string 类提供了若干用于修改字符串的方法。大多数方法都有大量重载版本，以便可用于 string 对象、字符串数组、单个字符和迭代器范围。

### 追加和添加的方法

可以使用重载的 += 运算符或 append() 方法将一个字符串追加到另一个字符串。如果结果长度超过最大字符串大小，所有这些操作都会抛出 length_error 异常。+= 运算符允许将 string 对象、字符串数组或单个字符追加到另一个字符串：

```cpp
basic_string& operator+=(const basic_string& str);
basic_string& operator+=(const charT* s);
basic_string& operator+=(charT c);
```

append() 方法也允许将 string 对象、字符串数组或单个字符追加到另一个字符串。此外，它们还允许通过指定起始位置和要追加的字符数，或者通过指定范围，来追加 string 对象的一部分。可以通过指定要使用字符串的多少个字符来追加字符串的一部分。用于追加字符的版本允许指定要复制该字符的多少个实例。以下是各种 append() 方法的原型：

```cpp
basic_string& append(const basic_string& str);
basic_string& append(const basic_string& str, size_type pos,
                     size_type n);
template<class InputIterator>
    basic_string& append(InputIterator first, InputIterator last);
basic_string& append(const charT* s);
basic_string& append(const charT* s, size_type n);
basic_string& append(size_type n, charT c);   // append n copies of c
void push_back(charT c);                       // appends 1 copy of c
```
