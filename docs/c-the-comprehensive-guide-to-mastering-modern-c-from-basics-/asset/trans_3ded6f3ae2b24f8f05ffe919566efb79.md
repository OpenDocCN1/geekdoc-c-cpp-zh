

| Sequence | 1st begin() | 2nd begin() | size() | 1st empty() | 2nd empty() |
|---|---|---|---|---|---|---|
| vec | filter | O(n) | O(1) | - | O(n) | O(1) |
| lst | filter | O(n) | O(1) | - | O(n) | O(1) |
| vec | filter drop | O(n) | O(1) | - | O(n) | O(1) |
| lst | filter drop | O(n) | O(1) | - | O(n) | O(1) |

**表 25.2** 各种容器与 C++23 组合带来的性能差异。

这些创新特别有趣。列表 25.6 受 Conor Hoekstra 示例的启发，它展示了视图（views）的功能。[ 67 ]

```cpp
// https://godbolt.org/z/hYTv6f9eo
#include <ranges>
#include <array>
#include <string>
#include <iostream>
#include <string_view>
using namespace std::literals; using namespace std;

// 用于输出各种内容的函数
template <typename OBJ>
void print(OBJ& obj, int level = 0) {
    if consteval(std::ranges::input_range<OBJ>(obj)) { // range
        cout << '[';
        for (const auto& elem : obj) print(elem, level+1);
    } else if consteval(requires { std::get<8>(std::declval<OBJ>>()); }) { // tuple/pair
        cout << "(";
        print(get<0>(obj), level+1); print(get<1>(obj), level+1);
        cout << ")";
    } else 
        cout << obj; // element
    }
    if (level == 0) cout << '\n';
}
```

```cpp
int main() {
    using namespace std; // 为了简洁起见
    auto const nums = array(0, 0, 1, 1, 2);
    auto const animals = array("cat", "dog");
    print(iota(0, 5) | chunk(2)); // 输出: [[01][23] [4]]
    print(nums, chunk_to<{int}>()); // 输出: [[00][11] [22]]
    print(iota(0, 5) | slide(3)); // 输出: [[012] [234]]
    print(iota(0, 10) | stride(3)); // 输出: [[036] [179]]
    print(repeat(8) | take(5)); // 输出: [[08888]]
    print(zip_transform(plus, nums, nums)); // 输出: [[002244]]
    print(zip(iota(0, 3), iota(1, 4))); // 输出: [[01)(12) [23]]
    print(iota(0, 4) | adjacent<2>()); // 输出: [[01)(12) [23]]
    print(iota(0, 4) | pairwise()); // 输出: [[01)(12) [23]]
    print(iota(0, 4) | adjacent_transform<2>(plus)); // 输出: [[135]]
    print(iota(0, 4) | pairwise_transform(plus)); // 输出: [[135]]
    print(animals | join_with('+')); // 输出: [cat+dog]
    print(cartesian_product(iota(0, 2), "AZ")); // 输出: [[0A)(0Z) [1A)(2Z]]
    print(enumerate("APL")); // 输出: [[0A)(1P) [2L]]
}
```

这些创新特别有趣。列表 25.6 受 Conor Hoekstra 示例的启发，它展示了视图（views）的功能。[ 67 ]

（注：由于提供的待翻译文本中存在大量重复和乱码的英文片段，上述译文已根据逻辑要求翻译了核心描述部分，并保持了 Markdown 格式。）

