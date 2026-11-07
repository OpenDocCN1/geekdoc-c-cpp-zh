
指定迭代器对也可与 std 命名空间中的常见 ranges 版本配合使用。在此示例中，两个范围位于不同容器中，但范围也可以位于同一容器中，此时这些范围不得重叠。

```cpp
37    // swap first five elements of values and values2
38    std::ranges::swap_ranges(values.begin(), values.begin() + 5,
39                            values2.begin(), values2.begin() + 5);
40
41    std::cout << "\nAfter swap_ranges for 5 elements"
42              << "\nvalues contains: ";
43    std::ranges::copy(values, output);
44    std::cout << "\nvalues2 contains: ";
45    std::ranges::copy(values2, output);
46    std::cout << "\n";
47 }
```

```
After swap_ranges for 5 elements
values contains: 1 2 3 4 5 5 4 3 2 1
values2 contains: 10 9 8 7 6 6 7 8 9 10
```

## 14.4.8 copy_backward、merge、unique、reverse、copy_if 和 copy_n

图 14.9 演示了来自 C++20 的 std::ranges 命名空间的算法 copy_backward、merge、unique、reverse、copy_if 和 copy_n。

```cpp
1    // fig14_09.cpp
2    // Algorithms copy_backward, merge, unique, reverse, copy_if and copy_n.
3    #include <algorithm>
4    #include <array>
5    #include <iostream>
6    #include <iterator>
7    #include <vector>
8
9    int main() {
10      std::array a1{1, 3, 5, 7, 9};
11      std::array a2{2, 4, 5, 7, 9};
12      std::ostream_iterator<int> output{std::cout, " "};
13
14      std::cout << "array a1 contains: ";
15      std::ranges::copy(a1, output); // display a1
16      std::cout << "\narray a2 contains: ";
17      std::ranges::copy(a2, output); // display a2
18
```

图 14.9 | 算法 copy_backward、merge、unique、reverse、copy_if 和 copy_n。（第 1 部分，共 2 部分。）

```
array a1 contains: 1 3 5 7 9
array a2 contains: 2 4 5 7 9
```

**图 14.9** | 算法 copy_backward、merge、unique、reverse、copy_if 和 copy_n。（第 2 部分，共 2 部分。）

### copy_backward 算法

C++20 的 `std::ranges::copy_backward` 算法（第 21 行）将其第一个参数的 *双向范围*（`a1`）复制到其第二个参数中 *输出迭代器* 指定的范围——在此例中，即目标容器的末尾（`results.end()`）。该算法按相反顺序复制元素，将每个元素放入目标容器时从 `results.end()` 之前的元素开始，并向容器开头推进。该算法返回一个 `std::ranges::copy_backward_result`，其中包含两个迭代器：

- 第一个位于 `a1.end()`。
- 第二个位于复制到目标范围中的最后一个元素——即 `results` 的开头，因为复制是向后执行的。

尽管元素按相反顺序复制，但它们在 `results` 中的放置顺序与 `a1` 相同。`copy` 与 `copy_backward` 的一个区别是

- `copy` 返回的迭代器位于所复制的最后一个元素之后，而
- `copy_backward` 返回的迭代器位于所复制的最后一个元素处，也就是该范围中的第一个元素。

```cpp
19 // place elements of a1 into results in reverse order
20 std::array<int, a1.size()> results{};
21 std::ranges::copy_backward(a1, results.end());
22 std::cout << "\nAfter copy_backward, results contains: ";
23 std::ranges::copy(results, output);
24
```

```
After copy_backward, results contains: 1 3 5 7 9
```

### move 和 move_backward 算法

可以将移动语义与 ranges 一起使用。C++20 的 `std::ranges` 算法 `move` 和 `move_backward`（来自头文件 `<algorithm>`）的工作方式与 `copy` 和 `copy_backward` 算法类似，但会移动指定范围中的元素，而不是复制它们。

### merge 算法

C++20 的 `std::ranges::merge` 算法（第 27 行）合并两个均按升序排序的 *输入范围*，并将结果写入第三个参数的 *输出迭代器* 所指定的目标容器。此操作后，`results2` 按排序顺序包含两个范围的值。`merge` 的第二个版本接受表示这两个范围的迭代器/哨兵对。两个版本都允许你提供一个 *二元谓词函数*，它通过比较两个参数来指定排序顺序，并在排序时第一个参数应被视为小于第二个参数时返回 `true`。

```cpp
25        // merge elements of a1 and a2 into results2 in sorted order
26        std::array<int, a1.size() + a2.size()> results2;
27        std::ranges::merge(a1, a2, results2.begin());
28
29        std::cout << "\n\nAfter merge of a1 and a2, results2 contains: ";
30        std::ranges::copy(results2, output);
31
```

合并 a1 和 a2 后，results2 包含：1 2 3 4 5 5 7 7 9 9

### unique 算法

概念 C

C++20 的 `std::ranges::unique` 算法（第 34 行）确定由其 *前向范围* 参数指定的已排序值范围中的唯一值。将 *unique* 应用于包含重复值的已排序范围后，每个值在范围中仅保留一份副本。该算法返回一个子范围，从最后一个唯一值之后的元素直到原始范围的末尾。容器中最后一个唯一值之后的所有元素的值都是未定义的。不应使用它们，因此这是另一种可以擦除未使用元素的情况（第 35 行）。你还可以提供一个 *二元谓词函数*，指定如何比较两个元素是否相等。

```cpp
32        // eliminate duplicate values from v
33        std::vector<int> v(results2.begin(), results2.end());
34        auto [first, last]{std::ranges::unique(v)};
35        v.erase(first, last); // remove elements that no longer contain values
36
37        std::cout << "\n\nAfter unique, v contains: ";
38        std::ranges::copy(v, output);
39
```

执行 unique 后，v 包含：1 2 3 4 5 7 9

### reverse 算法

概念 C

C++20 的 `std::ranges::reverse` 算法（第 41 行）反转其参数中的元素——一个支持 *双向迭代器* 的 *双向范围*。

```cpp
40        std::cout << "\n\nAfter reverse, a1 contains: ";
41        std::ranges::reverse(a1); // reverse elements of a1
42        std::ranges::copy(a1, output);
43
```

反转后，a1 包含：9 7 5 3 1

### copy_if 算法

概念 C

C++20 的 `std::ranges::copy_if` 算法（第 47–48 行）接收一个 *输入范围*、一个输出迭代器和一个 *一元谓词函数* 作为参数。该算法对 *输入范围* 中的每个元素调用 *一元谓词函数*，并且仅复制该函数返回 true 的元素。输出迭代器指定将元素输出到何处——在此例中，我们使用 **back_inserter** 将元素添加到 vector。该算法返回一个 **std::ranges::in_out_result**，其中包含两个迭代器：

- 第一个是 **输入迭代器**，位于 **input_range** 的末尾，而
- 第二个是 **输出迭代器**，位于复制到输出容器中的最后一个元素之后。

```cpp
44 // copy odd elements of a2 into v2
45 std::vector<int> v2{};
46 std::cout << "\nAfter copy_if, v2 contains: ";
47 std::ranges::copy_if(a2, std::back_inserter(v2),
48     [](auto x){return x % 2 == 0;});
49 std::ranges::copy(v2, output);
50
```

执行 copy_if 后，v2 包含：2 4

### copy_n 算法

C++20 的 **std::ranges::copy_n** 算法（第 54 行）从其第一个参数（a2.begin()）中 **input_iterator** 指定的位置开始，复制其第二个参数（3）指定的元素数量。这些元素输出到第三个参数中 **output_iterator** 指定的位置——在此例中，我们使用 **back_inserter** 将元素添加到 vector。

概念

```cpp
51 // copy three elements of a2 into v3
52 std::vector<int> v3{};
53 std::cout << "\nAfter copy_n, v3 contains: ";
54 std::ranges::copy_n(a2.begin(), 3, std::back_inserter(v3));
55 std::ranges::copy(v3, output);
56 std::cout << "\n";
57 }
```

执行 copy_n 后，v3 包含：2 4 5

## 14.4.9 inplace_merge、unique_copy 和 reverse_copy

图 14.10 演示了来自 C++20 的 **std::ranges** 命名空间的算法 **inplace_merge**、**unique_copy** 和 **reverse_copy**。

```cpp
1 // fig14_10.cpp
2 // Algorithms inplace_merge, unique_copy and reverse_copy.
3 #include <algorithm>
4 #include <array>
5 #include <iostream>
6 #include <iterator>
7 #include <vector>
8
```

**图 14.10** | 算法 inplace_merge、unique_copy 和 reverse_copy。（第 1 部分，共 2 部分。）

