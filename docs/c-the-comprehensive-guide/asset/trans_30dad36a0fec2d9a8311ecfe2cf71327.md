
从迭代器和哨兵创建一个视图。一些适配器、工厂和算法也使用此类型。有用之处：当算法返回子范围时，可以用 `auto [beg, end] = ...` 提取该范围的迭代器。

- `views::empty`  
  用法：偶尔；迭代器：–  
  创建一个不含任何元素的空视图。

- `views::single`  
  用法：偶尔；迭代器：–  
  生成一个包含单个元素的视图。

- `views::iota`  
  用法：偶尔；迭代器：–  
  用于生成递增的值序列。对应于 iota 算法。

- `views::istream`  
  用法：很少；迭代器：输入  
  由多个 `operator>>` 创建的视图。

- `views::repeat`  
  用法：偶尔（C++23）；迭代器：输入  
  重复相同的值。

- `views::filter`  
  用法：频繁；迭代器：输入  
  从范围中筛选出满足谓词的元素。注意，只有当修改后的值也满足谓词时，才可以修改结果值！

- `views::transform`  
  用法：频繁；迭代器：输入  
  对每个元素应用一个函数。

- `views::counted`  
  用法：很少；迭代器：输入  
  从迭代器和计数 *n* 创建一个范围。

- `views::take`  
  用法：频繁；迭代器：输入  
  仅传递范围的前 *n* 个元素。

- `views::take_while`  
  用法：频繁；迭代器：输入  
  只要谓词为真就传递元素。

- `views::drop`  
  用法：频繁；迭代器：输入  
  跳过范围的前 *n* 个元素。

- `views::drop_while`  
  用法：频繁；迭代器：输入  
  只要谓词为真就跳过元素。

- **views::join**  
  用法：频繁；迭代器：输入  
  将一个由范围组成的范围转换为扁平化范围。

- **views::join_with**  
  用法：频繁（C++23）；迭代器：输入  
  类似 `ranges::join_view`，但在被连接的范围之间带有分隔元素。

- **views::split**  
  用法：频繁；迭代器：前向  
  在分隔符处将 `forward_range` 拆分为多个范围。

- **views::lazy_split**  
  用法：很少；迭代器：输入  
  也会拆分，但只要求 `input_range`。

- **views::reverse**  
  用法：频繁；迭代器：输入  
  反转范围。

- **views::enumerate**  
  用法：频繁（C++23）；迭代器：输入  
  将元素范围转换为新的元组范围，每个元组包含一个索引和该元素。

- **views::elements**  
  用法：偶尔；迭代器：输入  
  将元组范围转换为第 *n* 个元素的范围。

- **views::keys**  
  用法：偶尔；迭代器：输入  
  类似 elements，用于第一个元组元素。

- **views::values**  
  用法：偶尔；迭代器：输入  
  类似 elements，用于第二个元组元素。

- **views::zip**  
  用法：频繁（C++23）；迭代器：输入  
  接收 *n* 个范围，并创建一个元组范围，每个元组包含 *n* 个元素。

- **views::zip_transform**  
  用法：频繁（C++23）；迭代器：输入  
  类似 zip，但随后用 *n* 个参数调用一个函数。

- **views::chunk**  
  用法：频繁（C++23）；迭代器：输入  
  将范围拆分为多个长度为 *n* 的范围，不重叠。

- **views::chunk_by**  
  用法：频繁（C++23）；迭代器：输入  
  根据某个准则对连续元素进行分组。让人联想到 SQL 的 group by。

- `views::slide`  
  用法：很少（C++23）；迭代器：前向  
  将范围拆分为多个长度为 n 的范围，允许重叠。

- `views::stride`  
  用法：偶尔（C++23）；迭代器：输入  
  取范围中的每第 n 个元素。

- `views::adjacent<N>`  
  用法：很少（C++23）；迭代器：前向  
  创建一个元组范围，每个元组包含输入范围中 N 个相邻元素。  
  与 slide 不同，N 是模板参数。

- `views::pairwise`  
  用法：很少（C++23）；迭代器：前向  
  是 `adjacent<2>` 的特化。

- `views::adjacent_transform<N>`  
  用法：很少（C++23）；迭代器：前向  
  像 `adjacent<N>`（或 slide）那样分组，但随后用 N 个参数调用一个函数。

- `views::pairwise_transform`  
  用法：很少（C++23）；迭代器：前向  
  是 `adjacent_transform<2>` 的特化。

- `views::cartesian_product`  
  用法：偶尔（C++23）；迭代器：输入/前向  
  生成来自多个范围的元素的所有组合。

还有其他几个类，尤其在您设计自己的适配器时会有所帮助：

- `ranges::view_interface`  
  自定义视图的基类。

- `ranges::range_adaptor_closure`（C++23）  
  用于 operator| 的自定义视图适配器的基类。

- `ranges::ref_view`  
  将范围的所有元素作为引用。

- `ranges::owning_view`  
  用于通过移动获取临时值视图的值。可以使用 all 适配器生成它。这是（到目前为止）唯一包含自身的视图。它仍然很划算，因为它只允许可移动的临时值作为参数。

- `views::common`  
  将带哨兵的视图转换为带 end() 迭代器的视图，使其行为更像容器。

- `views::as_const`（C++23）  
  通过将视图转换为 constant_range 来保护视图元素，使元素不可变。这与 `std::as_const` 的工作方式不同，也与在视图变量前加 `const` 对其产生的影响不同；后一种方式遗憾的是会让元素保持可变。

- *views::as_rvalue（C++23）*  
  一个序列视图，将每个元素转换为右值。

您需要了解，视图的性能特征会因使用它们的范围类型（或底层容器）不同而不同。例如，考虑 `drop(10)` 在 vector 上几乎瞬间完成，复杂度为 O(1)，但在 list 上是线性的，复杂度为 O(n)，因此慢得多。前面的视图也会产生影响。标准库会尝试选择性能良好的实现，有时会缓存中间结果。例如，在 `filter` 之后的 `begin()` 总是很慢，因为必须遍历开头要被过滤的元素。然而，对于像 `begin()` 这样重要的操作来说，这会非常不利。因此，`filter` 会缓存 `begin()` 的结果，并在后续每次调用时返回它。

表 25.2 简要概述了一些视图在不同范围上的性能，因此您可以了解需要注意什么。例如，您可以看到在 `filter` 之后不再能使用 `size(...)`。

| 序列 | 第 1 次 begin() | 第 2 次 begin() | size() | 第 1 次 empty() | 第 2 次 empty() |
|---|---|---|---|---|---|
| vector vec | O(1) | O(1) | O(1) | O(1) | O(1) |
| list lst | O(1) | O(1) | O(1) | O(1) | O(1) |
| vec \| drop | O(1) | O(1) | O(1) | O(1) | O(1) |
| lst \| drop | O(n) | O(1) | O(1) | O(1) | O(1) |
| vec \| filter | O(n) | O(1) | – | O(n) | O(1) |
| lst \| filter | O(n) | O(1) | – | O(n) | O(1) |
| vec \| filter \| drop | O(n) | O(1) | – | O(n) | O(1) |
| lst \| filter \| drop | O(n) | O(1) | – | O(n) | O(1) |

**表 25.2** 各种容器和视图组合的性能。

C++23 带来的创新尤其有趣。清单 25.6 受 Conor Hoekstra 的示例启发，展示了这些视图的作用。¹

1  *C++23 中的新算法*，Conor Hoekstra，https://youtu.be/VZPKHqeUQqQ?si=ucMAm2clAl2lAg2UT&ab_channel=ConorHoekstra，2023-10-10，[2023-10-22]

```cpp
// https://godbolt.org/z/hYTv6f9eo
#include <ranges>
#include <array>
#include <string>
#include <iostream>
#include <string_view>
using namespace std::literals; using namespace std;

// Function for outputting all sorts of things
template <typename OBJ>
void print(OBJ&& obj, int level = 0) {
    if constexpr (std::ranges::input_range<OBJ>) {                 // range
        cout << '[';
        for (const auto& elem : obj) print(elem, level+1);
        cout << ']';
    } else if constexpr(requires (OBJ tpl){ std::get<0>(tpl);}) {  // tuple/pair
        cout << '(';
        print(get<0>(obj), level+1); print(get<1>(obj), level+1);
        cout << ')';
    } else cout << obj;                                           // element
    if (level == 0) cout << '\n';
}

int main() {
    using namespace std::views; // exceptionally for brevity
    auto const nums = array{0, 0, 1, 1, 2, 2};
    auto const animals = array{"cat's", "dog's"};
    print(iota(0, 5) | chunk(2));                    // Output: [[0][1][2][3][4]]
    print(nums | chunk_by(equal_to{}));             // Output: [[0][1][2][2]]
    print(iota(0, 5) | slide(3));                    // Output: [[0][12][123][234]]
    print(iota(0, 10) | stride(3));                 // Output: [0369]
    print(repeat(8) | take(5));                     // Output: [88888]
    print(zip_transform(plus{}, nums, nums));       // Output: [002244]
    print(zip(iota(0, 3), nums, 1, 4));             // Output: [(0)(1)(2)(3)]
    print(iota(0, 4) | adjacent<2>);                // Output: [(01)(12)(23)]
    print(iota(0, 4) | adjacent_transform<2>);      // Output: [135]
    print(iota(0, 4) | pairwise_transform(plus{})); // Output: [135]
    print(animals | join_with(" + "));              // Output: [cat+dog]
    print(cartesian_product(iota(0, 2), "AZ"s));  // Output: [(0)(A)(0)(1A)(1Z)]
    print(enumerate("APL"s));                       // Output: [(0)(1P)(2L)]
    return 0;
}
```

清单 25.6 C++23 的视图尤其可以很好地组合。

print 函数既接受单个值，也接受范围和元组。使用 fmt 库会更容易，但我目前还没有它。注意 if 的使用
