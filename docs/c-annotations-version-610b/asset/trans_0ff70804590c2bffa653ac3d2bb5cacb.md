
## 12.1 本章使用的记号

在本章关于容器的内容中，使用以下记号约定：

- 容器位于标准命名空间中。在代码示例中这会清晰可见，但在正文中通常省略 `std::`。
- 不带尖括号的容器表示该类型的任意容器。在脑中用尖括号记法补上所需类型。例如，`pair` 可以表示 `pair<string, int>`。
- 记号 `Type` 表示泛型类型。`Type` 可以是 `int`、`string` 等。
- 标识符 `object` 和 `container` 表示所讨论的容器类型的对象。
- 标识符 `value` 表示存储在容器中的该类型的一个值。
- 简单的单字母标识符（如 `n`）表示无符号值。
- 较长的标识符表示迭代器。例如 `pos`、`from`、`beyond`。

有些容器（例如 map 容器）包含成对的值，通常称为“键”和“值”。对于这类容器，还额外使用以下记号约定：

- 标识符 `key` 表示所用键类型的一个值。
- 标识符 `keyvalue` 表示特定容器所用的‘value_type’的一个值。

## 12.2 ‘pair’ 容器

`pair` 容器是一个相当基础的容器。它用于存储两个元素，称为 `first` 和 `second`，差不多就是这样。在使用 `pair` 容器之前，必须已经包含头文件 `<utility>`。

pair 的数据类型在定义（或声明）pair 对象时使用模板的尖括号记法指定（参见第 20 章）。示例：

```cpp
pair<string, string> piper("PA28", "PH-ANI");
pair<string, string> cessna("C152", "PH-ANG");
```

这里，变量 `piper` 和 `cessna` 被定义为包含两个 string 的 pair 变量。两个 string 都可以使用 pair 类型的 first 和 second 字段获取：

```cpp
cout << piper.first << '\n' <<    // shows 'PA28'
     cessna.second << '\n';       // shows 'PH-ANG'
```

first 和 second 成员也可以用来重新赋值：

```cpp
cessna.first = "C152";
cessna.second = "PH-ANW";
```

如果必须完全重新赋值一个 pair 对象，可以使用匿名 pair 对象作为赋值运算符的右操作数。匿名变量定义一个临时变量（不接收名称），其唯一目的是（重新）赋值给另一个同类型变量。其一般形式为

```cpp
type(initializer list)
```

注意，使用 pair 对象时，仅提及容器名 `pair` 并不能完成类型指定。它还需要指定存储在 pair 中的数据类型。为此，再次使用（模板）尖括号记法。例如，cessna pair 变量的重新赋值可以按如下方式完成：

```cpp
cessna = pair<string, string>("C152", "PH-ANW");
```

在这种情况下，类型指定可能变得相当繁琐，这重新引起了人们对 typedef 关键字所提供可能性的兴趣。如果源文件中使用了许多 `pair<type1, type2>` 子句，那么先为该子句定义一个名称，然后再使用所定义的名称，可以减少键入工作量并提高可读性。例如，

```cpp
typedef pair<string, string> pairStrStr;
```

```cpp
cessna = pairStrStr("C152", "PH-ANW");
```

除此之外（以及基本的操作集（赋值和比较）），pair 不提供进一步的功能。然而，它是后续抽象容器 map、multimap 和 hash_map 的基本组成部分。

C++11 标准提供了一个*泛化*的 pair 容器：*元组*，将在 21.6 节中介绍。

## 12.3 顺序容器

### 12.3.1 'vector' 容器

`vector` 类实现一个可扩展数组。在使用 `vector` 容器之前，必须已经包含 `<vector>` 头文件。

以下构造函数、运算符和成员函数可用：

- **构造函数：**
  - 可以构造一个空 vector：

    ```cpp
    vector<string> object;
    ```

    注意 `vector` 中要存储的数据类型的指定方式：数据类型写在尖括号内，紧跟在 'vector' 容器名之后。这是容器的常见做法。

  - 可以将 vector 初始化为一定数量的元素。vector（以及其他容器）的一个较好特性是，它将其数据元素初始化为数据类型的默认值。此初始化使用数据类型的*默认构造函数*。对于非类数据类型，使用值 0。因此，对于 `int` vector，我们知道其初始值为零。随着 C++11 标准的出现（从 g++ 4.4 版本开始），也可以使用初始化列表。一些示例：

    ```cpp
    vector<string> object(5, string("Hello")); // initialize to 5 Hello's,
    vector<string> container(10);              // and to 10 empty strings
    vector<string> names = {"george", "frank", "tony", "karel"}; // g++ 4.4
    ```

  - 可以使用迭代器初始化 vector。要用现有 `vector<string>` 的第 5 到第 10 个元素（包括最后一个）初始化 vector，可以使用以下构造：

    ```cpp
    extern vector<string> container;
    vector<string> object(&container[5], &container[11]);
    ```

    注意，这里第二个迭代器（`&container[11]`）所指向的最后一个元素*不*存储在 `object` 中。这是一个使用*迭代器*的简单示例，其中使用的值范围从第一个值开始，包含所有元素，直到但不包括第二个迭代器所指的元素。其标准记法是 `[begin, end)`。

  - 可以使用拷贝构造函数初始化 vector：

    ```cpp
    extern vector<string> container;
    vector<string> object (container);
    ```

- 除了容器的标准运算符之外，`vector` 还支持下表运算符，可用于获取或重新赋值 vector 的单个元素。注意，被索引的元素必须存在。例如，在定义了一个空 vector 之后，像 `ivec[0] = 18` 这样的语句会产生错误，因为 vector 为空。因此，vector *不*会自动扩展，并且它*确实*遵守其数组边界。在这种情况下，应首先调整 vector 的大小，或者应使用 `ivec.push_back(18)`（见下文）。

- `vector` 类提供以下成员函数：

  - `Type &back():`
    该成员返回 vector 中最后一个元素的引用。程序员有责任仅在 vector 非空时使用该成员。
  - `vector::iterator begin():`
    该成员返回指向 vector 中第一个元素的迭代器；如果 vector 为空，则返回 `end`。
  - `size_t capacity():`
    已为其分配内存的元素数量。它至少返回 `size` 所返回的值。
  - `void clear():`
    该成员删除 vector 的所有元素。
  - `bool empty():`
    如果 vector 不包含元素，该成员返回 `true`。
  - `vector::iterator end():`
    该成员返回指向 vector 中最后一个元素之后的迭代器。
  - `vector::iterator erase():`
    该成员可用于删除 vector 中特定范围的元素：
    - `erase(pos)` 删除迭代器 `pos` 所指向的元素。返回迭代器 `++pos`。
    - `erase(first, beyond)` 删除迭代器范围 `[first, beyond)` 所指示的元素，返回 `beyond`。
  - `Type &front():`
    该成员返回 vector 中第一个元素的引用。程序员有责任仅在 vector 非空时使用该成员。
  - `... insert():`
    可以从某个位置开始插入元素。返回值取决于所调用的 `insert()` 版本：
    - `vector::iterator insert(pos)` 在 `pos` 处插入类型 `Type` 的默认值，返回 `pos`。
    - `vector::iterator insert(pos, value)` 在 `pos` 处插入 `value`，返回 `pos`。
    - `void insert(pos, first, beyond)` 插入迭代器范围 `[first, beyond)` 中的元素。
    - `void insert(pos, n, value)` 在位置 `pos` 处插入 `n` 个值为 `value` 的元素。

