
typedef `basic_string<char>` `string`;

定义。无符号整数类型 `size_type` 在此类中定义，同时还定义了一个整数常量 `npos`，它是某个整数，该整数为负数或大于字符串中的字符数。以下是对字符串对象 `s` 的主要操作的列表；`pos`、`pos1`、`pos2`、`n`、`n1` 和 `n2` 为 `size_type` 类型；`str`、`str1` 和 `str2` 为 `string` 类型；`charArray` 为字符数组；`ch` 和 `delim` 为 `char` 类型；`istr` 为 `istream`；`ostr` 为 `ostream`；`it1` 和 `it2` 为迭代器；`inpIt1` 和 `inpIt2` 为输入迭代器。除 `>>`、`<<`、`+`、关系运算符、`getline()` 和第二版本的 `swap()` 之外的所有这些操作都是函数成员。

### 构造器：

`string s;`
此声明调用默认构造器将 `s` 构造为空字符串

`string s(charArray);`
此声明将 `s` 初始化为包含 `charArray` 的副本

`string s(charArray, n);`
此声明将 `s` 初始化为包含 `charArray` 中前 `n` 个字符的副本

`string s(str);`
此声明将 `s` 初始化为包含字符串 `str` 的副本

`string s(str, pos, n);`
此声明将 `s` 初始化为包含字符串 `str` 从位置 `pos` 开始的 `n` 个字符的副本；如果 `n` 太大，则仅复制到 `str` 的末尾

`string s(n, ch);`
此声明将 `s` 初始化为包含 `n` 个字符 `ch` 的副本

`string s(inpIt1, inpIt2)`
此声明将 `s` 初始化为包含范围 [`inpIt1`, `inpIt2`) 中的字符

```
istr >> s
```

从 `istr` 中提取字符并存储到 `s` 中，直到提取 `s.max_size()` 个字符、遇到文件结束或遇到空白字符为止，此时空白字符不会从 `istr` 中移除；返回 `istr`

```
ostr << s
```

将 `s` 的字符插入到 `ostr` 中；返回 `ostr`

```
s = val
```

将 `val` 的副本赋给 `s`；`val` 可以是字符串、字符数组或字符

```
s += val
```

将 `val` 的副本追加到 `s` 后；`val` 可以是字符串、字符数组或字符

```
s[pos]
```

返回 `s` 中位置 `pos` 存储的字符的引用，前提是 `pos < s.length()`

```
s + t

t + s
```

返回 `s` 和 `t` 拼接的结果；`t` 可以是字符串、字符数组或字符

```
s < t, t < s

s > t, t > s

s <= t, t <= s

s >= t, t >= s

s == t, t == s

s != t, t != s
```

根据关系运算符返回 `true` 或 `false`；`t` 可以是字符串或字符数组

```
s.append(str)
```

在 `s` 末尾追加字符串 `str`；返回 `s`

| 成员函数 | 描述 |
|---|---|
| `s.assign(str, pos, n)` | 将 `str` 从位置 `pos` 开始的 `n` 个字符的副本赋给 `s`；如果 `n` 过大，则只复制到 `str` 末尾；返回 `s` |
| `s.assign(charArray)` | 将 `charArray` 的副本赋给 `s`；返回 `s` |
| `s.assign(charArray, n)` | 将 `charArray` 中前 `n` 个字符组成的字符串赋给 `s`；返回 `s` |
| `s.assign(n, ch)` | 将由 `n` 个 `ch` 副本组成字符串赋给 `s`；返回 `s` |
| `s.assign(impT1, impT2)` | 将范围 [`impT1`, `impT2`) 中的字符组成的字符串赋给 `s`；返回 `s` |
| `s.at(pos)` | 返回 `s[pos]` |
| `s.begin()` | 返回指向 `s` 中第一个字符的迭代器 |
| `s.c_str()` | 返回包含 `s` 中存储字符、以空字符结尾的 `char` 数组的基地址 |
| `s.capacity()` | 返回 `s` 中分配存储的大小，类型为 `size_type` |
| `s.clear()` | 删除 `s` 中的所有字符；返回类型为 `void` |
| `s.compare(str)` | 根据 `s` 小于、等于或大于 `str` 返回负值、0 或正值 |
| `s.compare(charArray)` | 按前述方法比较 `s` 和 `charArray` |
| `s.compare(pos, n, str)` | 按前述方式比较字符串 `s` 和 `str`，但从 `s` 的位置 `pos` 开始，只比较接下来的 `n` 个字符 |
| `s.compare(pos, n, charArray)` | 按前述方法比较字符串 `s` 和 `charArray` |
| `s.compare(pos1, n1, str, pos2, n2)` | 按前述方式比较 `s` 和 `str`，但从 `s` 的位置 `pos1`、`str` 的位置 `pos2` 开始，只比较 `s` 中接下来的 `n1` 个字符和 `str` 中接下来的 `n2` 个字符 |

```
s.compare(pos1, n1, charArray, n2)
```

按前述方式比较字符串 `s` 和 `charArray`，但仅使用 `charArray` 中的前 `n2` 个字符

```
s.copy(charArray, pos, n)
```

用从位置 `pos` 开始的 `charArray` 中的 `n` 个字符，或若省略 `pos` 则从位置 `0` 开始，替换 `s` 中的字符串；如果 `n` 过大，则只复制到 `charArray` 末尾；返回已复制的字符数，类型为 `size_type`

```
s.data()
```

返回包含 `s` 中存储字符的 `char` 数组。

```
s.empty()
```

如果 `s` 不包含字符则返回 `true`，否则返回 `false`

```
s.end()
```

返回指向 `s` 中最后一个字符之后位置的迭代器

```
s.erase(pos, n)
```

从位置 `pos` 开始删除 `s` 中的 `n` 个字符，默认值 `0`；如果 `n` 过大或被省略，则只删除到 `s` 末尾；返回 `s`

```
s.erase(it)
```

删除 `it` 指定的位置的字符；返回指向被删除字符之后位置的迭代器

```
s.find(str, pos)
```

返回第一个 `≥ pos` 的位置，使得 `s` 的下一个 `str.size()` 个字符与 `str` 中的字符匹配；如果不存在此类位置则返回 `npos`；`pos` 的默认值为 `0`

```
s.find(ch, pos)
```

按前述方法搜索 `s`，但搜索 `ch`

```
s.find(charArray, pos)
```

按前述方法搜索 `s`，但搜索 `charArray` 中的字符

```
s.find_first_not_of(ch, pos)
```

按前述方法搜索 `s`，但搜索 `ch`

```
s.find_first_not_of(charArray, pos)
```

按前述方法搜索 `s`，但搜索 `charArray` 中的字符

```
s.find_first_not_of(charArray, pos, n)
```

按前述方法搜索 `s`，但仅使用 `charArray` 中的前 `n` 个字符；`pos` 值必须给出

```
s.find_first_of(str, pos)
```

返回第一个 `≥ pos` 的 `s` 中与 `str` 中任意字符匹配的字符的位置；如果不存在此类位置则返回 `npos`；`pos` 的默认值为 `0`

```
s.find_first_of(ch, pos)
```

按前述方法搜索 `s`，但搜索 `ch`

```
s.find_first_of(charArray, pos)
```

按前述方法搜索 `s`，但搜索 `charArray` 中的字符

```
s.find_first_of(charArray, pos, n)
```

按前述方法搜索 `s`，但仅使用 `charArray` 中的前 `n` 个字符；`pos` 值必须给出

```
s.find_last_not_of(str, pos)
```

返回最高位置 `≤ pos` 的 `s` 中与 `str` 中任意字符都不匹配的字符；如果不存在此类位置则返回 `npos`；`pos` 的默认值为 `npos`

```
s.find_last_not_of(ch, pos)
```

按前述方法搜索 `s`，但搜索 `ch`

```
s.find_last_not_of(charArray, pos)
```

按前述方法搜索 `s`，但使用 `charArray` 中的字符

```
s.find_last_not_of(charArray, pos, n)
```

按前述方法搜索 `s`，但仅使用 `charArray` 中的前 `n` 个字符；`pos` 值必须给出

```
s.find_last_of(str, pos)
```

返回最高位置 `≤ pos` 的 `s` 中与 `str` 中任意字符匹配的字符；如果不存在此类位置则返回 `npos`；`pos` 的默认值为 `npos`

```
s.find_last_of(ch, pos)
```

按前述方法搜索 `s`，但搜索 `ch`

```
s.find_last_of(charArray, pos)
```

按前述方法搜索 `s`，但使用 `charArray` 中的字符

```
s.find_last_of(charArray, pos, n)
```

按前述方法搜索 `s`，但仅使用 `charArray` 中的前 `n` 个字符；`pos` 值必须给出

```
s.insert(pos, str)
```

在 `s` 的位置 `pos` 插入 `str` 的副本；返回 `s`

```
s.insert(pos1, str, pos2, n)
```

在 `s` 的位置 `pos` 插入从位置 `pos2` 开始的 `str` 的 `n` 个字符的副本；如果 `n` 过大，则只复制到 `str` 末尾；返回 `s`

```
s.insert(pos, charArray, n)
```

在 `s` 的位置 `pos` 插入 `charArray` 的前 `n` 个字符的副本；如果省略 `n` 则插入全部字符；返回 `s`

```
s.insert(pos, n, ch)
```

在 `s` 的位置 `pos` 插入 `n` 个字符 `ch` 的副本；返回 `s`

```
s.insert(it, ch)
```

在 `it` 指定的位置插入字符 `ch` 的副本，并返回指向该副本的迭代器

```
s.insert(it, n, ch)
```

在 `it` 指定的位置插入 `n` 个字符 `ch` 的副本到 `s` 中；返回类型为 `void`

```
s.insert(it, inpIt1, inpIt2)
```

在 `it` 指定的位置插入范围 [`inpIt1`, `inpIt2`) 中的字符的副本到 `s` 中；返回类型为 `void`

```
s.length()
```

返回 `s` 的长度，类型为 `size_type`

```
s.max_size()
```

返回 `s` 的最大长度，类型为 `size_type`

```
s.rbegin()
```

返回指向 `s` 中最后一个字符的反向迭代器

```
s.rend()
```

返回指向 `s` 中第一个字符之前的反向迭代器

```
s.replace(pos1, n1, str)
```

用 `str` 替换 `s` 中从位置 `pos1` 开始长度为 `n1` 的子串；如果 `n1` 过大，则替换到 `s` 末尾的所有字符；返回 `s`

```
s.replace(it1, it2, str)
