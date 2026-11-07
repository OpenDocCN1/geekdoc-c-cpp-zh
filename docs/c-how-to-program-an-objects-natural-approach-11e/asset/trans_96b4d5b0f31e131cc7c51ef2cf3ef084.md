
非 range 的 `std::remove` 和 `std::remove_if` 算法各自返回一个单独的迭代器，指向向量中第一个无效元素。使用这些非 range 算法时，你可以在一条语句中执行 erase-remove 惯用法，如下所示：

```cpp
v1.erase(std::remove(v1.begin(), v1.end(), 10), v1.end());
```

像 `erase` 这样的容器成员函数尚不支持 C++20 的 Ranges。

## C++20 的 std::erase 和 std::erase_if

为了简化 erase-remove 惯用法，C++20 新增了 `std::erase` 和 `std::erase_if` 函数。这两个函数都在头文件 `<string>`、`<vector>`、`<deque>`、`<list>` 和 `<forward_list>` 中提供了重载，而 `std::erase_if` 还在 `<map>`、`<set>`、`<unordered_map>` 和 `<unordered_set>` 中提供了重载。每个函数都通过一次函数调用完成 erase-remove 惯用法，并将给定容器作为第一个参数。例如，第 17–18 行可以替换为：

```cpp
std::erase(v1, 10);
```

## remove_copy 算法

第 28 行使用 `std::ranges::remove_copy` 算法，将 v2 中所有值不等于 10 的元素复制到向量 c1 中。第一个参数必须是 input_range，它支持 input_iterator 来读取范围。同样，向量支持更强大的 random_access_iterator，因此满足 `remove_copy` 的最低要求。我们稍后会讨论第二个参数。第 30 行输出 c1 的所有元素。

```cpp
std::vector v2{init}; // initialize with copy of init
std::cout << "\n\nv2: ";
std::ranges::copy(v2, output);

// copy from v2 to c1, removing 10s in the process
std::vector<int> c1{};
std::ranges::remove_copy(v2, back_inserter(c1), 10);
std::cout << "\n\nc1 after copying v2 without 10s: ";
std::ranges::copy(c1, output);
```

```text
v2: 10 2 15 4 10 6
c1 after copying v2 without 10s: 2 15 4 6
```

## 迭代器适配器：back_inserter、front_inserter 和 inserter

第二个参数指定了一个输出迭代器，指示复制的元素将被写入的位置——通常是另一个容器。`remove_copy` 算法不会检查目标容器是否有足够空间来存储所有复制的元素。因此，第二个参数中的迭代器必须引用一个具有足够空间容纳所有元素的容器。与其预先分配内存，不如使用迭代器适配器来增长容器，使其在插入新元素时能够分配更多元素。在第 28 行，表达式 `std::back_inserter(c1)` 使用 `back_inserter` 迭代器适配器（头文件 `<iterator>`）创建一个 `back_insert_iterator`。当算法使用此迭代器向 c1 中插入元素时，该迭代器会调用容器的 **push_back** 函数将元素放在 c1 的末尾。如果容器需要更多空间，它会增长以容纳新元素。**back_insert_iterator** 不能用于数组，因为数组是固定大小的容器，没有 **push_back** 函数。

17. “Erase–remove idiom（擦除-移除惯用法）。”维基百科. 维基媒体基金会. 访问于2023年4月18日. https://en.wikipedia.org/wiki/Erase-remove_idiom.

还有另外两种 inserter：

- **front_inserter** 创建一个 **front_insert_iterator**，它使用容器的 **push_front** 成员函数将元素插入容器的开头。
- inserter 创建一个 **insert_iterator**，它使用容器的 **insert** 成员函数，在适配器第一个参数指定的容器中、适配器第二个参数中的 **迭代器** 所指定的位置插入元素。

## remove_if 算法

第 38 行调用 C++20 的 **std::ranges::remove_if** 算法，从 v3 中删除所有使一元谓词函数 **greaterThan9** 返回 true 的元素。第一个参数必须是 **forward_range**，它使 **remove_if** 能够读取范围内的元素。一元谓词函数必须接收一个参数并返回 bool 值。

```cpp
32    std::vector v3{init};  // initialize with copy of init
33    std::cout << "\nv3: ";
34    std::ranges::copy(v3, output);
35
36    // remove elements greater than 9 from v3
37    auto greaterThan9{[](auto x){ return x > 9; }};
38    auto removed2{std::ranges::remove_if(v3, greaterThan9)};
39    v3.erase(removed2.begin(), removed2.end());
40    std::cout << "\nv3 after removing elements greater than 9: ";
41    std::ranges::copy(v3, output);
```

```text
v3: 10 2 15 4 10 6
v3 after removing elements greater than 9: 2 4 6
```

第 37 行将一元谓词函数定义为泛型 lambda：

```cpp
[](auto x){return x > 9;}
```

如果其参数大于 9，则返回 true；否则返回 false。编译器会推断 lambda 的参数类型和返回类型：

- 向量包含 int，因此编译器将参数类型推断为 int。
- lambda 返回条件求值的结果，因此编译器将返回类型推断为 bool。

与 **remove** 一样，**remove_if** 不会修改容器中元素的数量。相反，它会将所有未删除的元素放到容器的开头。它返回一个由不再有效的元素组成的子范围。在第 39 行，我们使用该子范围来擦除 v3 中的这些元素。第 41 行输出 v3 更新后的内容。第 38–39 行可以用 C++20 的 **std::erase_if** 替换：

```cpp
std::erase_if(v3, greaterThan9);
```

## remove_copy_if 算法

第 49 行调用 C++20 的 `std::ranges::remove_copy_if` 算法，从它的 `input_range` 参数 v4 中复制所有使一元谓词函数（第 37 行的 lambda）返回 true 的元素。第二个参数必须是 `output_iterator`，以便正在复制的元素可以被写入目标范围。我们使用 `back_inserter` 将复制的元素插入向量 c2。第 51 行输出 c2 的内容。

```cpp
43    std::vector v4{init}; // initialize with copy of init
44    std::cout << "\nv4: ";
45    std::ranges::copy(v4, output);
46
47    // copy elements from v4 to c2, removing elements greater than 9
48    std::vector<int> c2{};
49    std::ranges::remove_copy_if(v4, std::back_inserter(c2), greaterThan9);
50    std::cout << "\nc2 after copying v4 without elements greater than 9: ";
51    std::ranges::copy(c2, output);
52    std::cout << '\n';
53 }
```

```text
v4: 10 2 15 4 10 6
c2 after copying v4 without elements greater than 9: 2 4 6
```

## 14.4.4 replace、replace_if、replace_copy 和 replace_copy_if

图 14.5 演示了使用 C++20 的 `std::ranges` 算法 `replace`、`replace_if`、`replace_copy` 和 `replace_copy_if` 替换序列中的值。

```cpp
1  // fig14_05.cpp
2  // Algorithms replace, replace_if, replace_copy and replace_copy_if.
3  #include <algorithm>
4  #include <array>
5  #include <iostream>
6  #include <iterator> // ostream_iterator
7
8  int main() {
9     std::ostream_iterator<int> output{std::cout, " "};
10
```

**图 14.5**  |  算法 replace、replace_if、replace_copy 和 replace_copy_if。

### replace 算法

第 16 行调用 C++20 的 `std::ranges::replace` 算法，将 `input_range` a1 中所有 10 替换为 100。第一个参数必须支持 `indirectly_writable` 迭代器，这样 `replace` 才能解引用迭代器以替换范围内的值。数组 a1 是非 const 的，因此它的迭代器可以用于写入数组。

```cpp
11    std::array a1{10, 2, 15, 4, 10, 6};
12    std::cout << "a1: ";
13    std::ranges::copy(a1, output);
14
15    // replace all 10s in a1 with 100
16    std::ranges::replace(a1, 10, 100);
17    std::cout << "\na1 after replacing 10s with 100s: ";
18    std::ranges::copy(a1, output);
```

```text
a1: 10 2 15 4 10 6
a1 after replacing 10s with 100s: 100 2 15 4 100 6
```

### replace_copy 算法

第 26 行调用 C++20 的 `std::ranges::replace_copy` 算法，复制 `input_range` a2 中的所有元素，并将每个 10 替换为 100。第二个参数必须是输出迭代器，表示将复制的元素写入到哪里。该算法会复制或替换 `input_range` 的每个元素，因此我们为 c1 分配了与 a2 相同数量的元素，但我们本可以使用一个空向量和 back_inserter。

```cpp
20    std::array a2{10, 2, 15, 4, 10, 6};
21    std::array<int, a2.size()> c1{};
22    std::cout << "\na2: ";
23    std::ranges::copy(a2, output);
24
25    // copy from a2 to c1, replacing 10s with 100s
26    std::ranges::replace_copy(a2, c1.begin(), 10, 100);
27    std::cout << "\nc1 after replacing a2's 10s with 100s: ";
28    std::ranges::copy(c1, output);
```

```text
a2: 10 2 15 4 10 6
c1 after replacing a2's 10s with 100s: 100 2 15 4 100 6
```

### replace_if 算法

第 36 行调用 C++20 的 `std::ranges::replace_if` 算法，将 `input_range` a3 中使**一元谓词函数**（第 35 行的 `greaterThan9`）返回 true 的每个元素进行替换。第一个参数必须支持输出迭代器，这样 `replace_if` 才能替换范围内的值。这里，我们将每个大于 9 的值替换为 100。

```cpp
30    std::array a3{10, 2, 15, 4, 10, 6};
31    std::cout << "\na3: ";
32    std::ranges::copy(a3, output);
33
34    // replace values greater than 9 in a3 with 100
35    auto greaterThan9{[](auto x) { return x > 9; }};
36    std::ranges::replace_if(a3, greaterThan9, 100);
37    std::cout << "\na3 after replacing values greater than 9 with 100s: ";
38    std::ranges::copy(a3, output);
39 }
```

