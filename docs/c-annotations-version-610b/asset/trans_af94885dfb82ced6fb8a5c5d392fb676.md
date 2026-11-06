

有些成员函数具有重载版本，期望一个类型为 `char const *` 的初始参数。但即使并非如此，在定义了 `std::string` 形参的地方，第一个实参也*总是*可以是 `char const *` 类型。

若干成员函数接受*迭代器*。第18.2节涵盖*迭代器*的技术细节，但此时可以忽略这些内容而不影响连续性。与 `apos` 和 `opos` 一样，迭代器必须指向字符串对象内容中已存在的位置和/或已存在的字符范围。

最后，所有计算索引的字符串成员函数在失败时返回预定义常量 `string::npos`。

## 5.2.1 初始化器

定义字符串对象后，保证它们处于有效状态。在*定义时*，字符串对象可以通过以下方式之一进行初始化：以下字符串构造函数可用：

- `string object:` 将对象初始化为空字符串。以这种方式定义字符串时，不得指定参数列表；
- `string object(string::size_type count, char ch):` 用 count 个字符 `ch` 初始化对象；
- `string object(string const &argument):` 用 `argument` 初始化对象；
- `string object(std::string const &argument, string::size_type apos, string::size_type an):` 用 `argument` 的内容初始化对象，从索引位置 `apos` 开始，最多使用 `argument` 的 `an` 个字符；
- `string object(InputIterator begin, InputIterator end):` 用两个 InputIterator 定义的字符范围内的字符初始化对象。

## 5.2.2 迭代器

有关*迭代器*的详细信息，请参见第18.2节。作为迭代器的快速介绍：迭代器的作用类似于指针，而在需要迭代器的场合通常可以使用指针。迭代器通常成对出现，定义一个实体范围。begin 迭代器指向第一个实体，end 迭代器指向范围中最后一个实体之后的位置。它们的差等于迭代器范围中的实体数量。

迭代器在*泛型算法*（参见第19章）的语境中起着重要作用。类 `std::string` 定义了以下*迭代器类型*：

- `string::iterator` 和 `string::const_iterator`：这些迭代器是*前向迭代器*。`const_iterator` 由 const 字符串对象返回，普通迭代器由非 const 字符串对象返回。迭代器所引用的字符可以被修改；
- `string::reverse_iterator` 和 `string::const_reverse_iterator`：这些迭代器也是*前向迭代器*，但当*递增*迭代器时，会到达字符串对象中的*前一个*字符。除此之外，它们分别类似于 `string::iterator` 和 `string::const_iterator`。

## 5.2.3 运算符

字符串对象可以通过成员函数操作，也可以通过运算符操作。使用运算符通常会产生看起来更自然的代码。在运算符可用且具有与成员函数等效的功能时，几乎总是优先使用运算符。

以下运算符可用于字符串对象（在示例中，‘object’和‘argument’指现有的 `std::string` 对象）。

- **普通赋值：**

  字符、C 或 C++ 字符串可赋给 `string` 对象。赋值运算符返回其左操作数。示例：

  ```
  object = argument;
  object = "C string";
  object = 'x';
  object = 120;       // same as object = 'x'
  ```

- **加法：**

  算术加法赋值运算符和加法运算符将文本添加到字符串对象。算术赋值运算符返回其左操作数，加法运算符在临时字符串对象中返回其结果。使用加法运算符时，左操作数或右操作数必须是 `std::string` 对象。另一个操作数可以是 char、C 字符串或 C++ 字符串。示例：

  ```
  object += argument;
  object += "hello";
  object += 'x';        // integral expressions are OK

  argument + otherArgument;    // two std::string objects
  argument + "hello";          // using + at least one
  "hello" + argument;          // std::string is required
  argument + 'a'               // integral expressions are OK
  'a' + argument;
  ```

- **下标运算符：**

  下标运算符可用于获取对象的各个字符，或为非 const 字符串对象的各个字符赋予新值。没有范围检查（为此请使用 `at()` 成员函数）。该运算符返回 `char &` 或 `char const &`。示例：

  ```
  object[3] = argument[5];
  ```

- **逻辑运算符：**

  逻辑比较运算符可应用于两个字符串对象，或一个字符串对象和一个 C 字符串，以比较它们的内容。这些运算符返回 bool 值。可用运算符包括 ==、!=、>、>= 和 <=。排序运算符使用 ASCII 字符排序序列对其内容执行字典序比较。示例：

  ```
  object == object;          // true
  object != (object + 'x');  // true
  object <= (object + 'x');  // true
  ```

- **流相关运算符：**

  插入运算符（参见第3.1.4节）可用于将字符串对象插入 ostream，提取运算符可用于从 istream 提取字符串对象。提取运算符默认首先忽略所有空白字符，然后从 istream 中提取所有连续的非空白字符。也可以提取字符数组而不是字符串，但使用字符串对象的优势应该很清楚：目标字符串对象会自动调整为所需字符数。示例：

  ```
  cin >> object;
  cout << object;
  ```

## 5.2.4 成员函数

`std::string` 类提供了许多成员函数以及应视为字符串类一部分的附加非成员函数。所有这些函数按字母顺序列在下面。

符号值 `string::npos` 由字符串类定义。当返回字符串偏移位置的成员函数返回它时，它表示“索引未找到”。示例：对不包含字符 `x` 的字符串对象调用 `find('x')`（见下文）时，返回 npos，因为请求的位置不存在。

在 **C** 字符串中用于指示 ASCII-Z 字符串结束的最终 0 字节并*不*被视为 **C++** 字符串的一部分，因此，在包含 C 字符串字符的字符串对象中查找 0 时，成员函数将返回 npos，而不是 length()。

以下是操作 string 类对象的标准函数。当提到 `size_t` 参数时，它可以被解释为 `string::size_type` 类型的参数，但不定义默认参数值。类型 `size_type` 应读作 `string::size_type`。使用 `size_type` 时，第 **5.2** 节提到的默认参数值适用。所有引用的函数都是 `std::string` 类的成员函数，除非另有说明。

- `char &at(size_t opos);`

  返回对指定位置字符的引用。当对 `string const` 对象调用时，返回 `char const &`。该成员函数执行范围检查；如果传入无效索引，则引发异常（默认情况下会中止程序）。

- `string &append(InputIterator begin, InputIterator end);`

  将由 begin 和 end 定义的范围内的字符追加到当前字符串对象。

- `string &append(string const &argument, size_type apos, size_type an);`

  将 argument（或其子串）追加到当前字符串对象。

- `string &append(char const *argument, size_type an);`

  将 argument 的前 `an` 个字符追加到字符串对象。

- `string &append(size_type n, char ch);`

  将 `n` 个字符 `ch` 追加到当前字符串对象。

- `string &assign(string const &argument, size_type apos, size_type an);`

  将 argument（或其子串）赋给字符串对象。如果 argument 的类型为 `char const *`，并且提供了一个附加参数，则第二个参数被解释为初始化 `an` 的值，并使用 0 初始化 `apos`。

- `string &assign(size_type n, char ch);`

  将 `n` 个字符 `ch` 赋给当前字符串对象。

