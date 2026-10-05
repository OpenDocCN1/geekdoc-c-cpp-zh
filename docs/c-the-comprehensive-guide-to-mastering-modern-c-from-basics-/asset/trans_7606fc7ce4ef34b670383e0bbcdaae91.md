
并且对于某些类型。有一些常见的组合，例如 `.2f` 用于表示保留两位小数的浮点数。

各个元素的含义如下：

- * fill:
  指定用于填充的字符。默认是空格格字符。需要配合 `align` 使用。

- * align:
  可以是 `<`（左对齐）、>`（右对齐）或 `^`（居中）。默认是左对齐。

- * sign:
  –仅对负数包含符号（默认值），`+` 始终包含符号，空格则表示负数使用负号，正数使用空格。

- * #:
  启用备用格式，例如整数的前缀或浮点数的计数点。

- * 0:
  用零填充数字。

- * width:
  指定结果应具有的最小宽度。默认值为零。

- * .precision:
  浮点数的小数位数，或者字符串参数中应使用的字符数。

- * 启用数字和布尔值的依赖于区域的格式化。

- * type:
  将输出切换到特定类型：`d` 用于整数，`f` 用于浮点数，依此类推。

要将你自己的类实例作为 `format` 的参数，你需要为你的类特化 `std::formatter<>` 类。该类随后必须提供两个签名正确的方法：

- Parse:
  评估格式属性，并返回指向已解析格式属性之后的第一个字符的迭代器。

- Format:
  将参数的格式化输出写入输出流，并返回指向输出末尾的迭代器。

该类还必须有一个默认构造函数，并且必须可拷贝且可赋值的。

```cpp
// https://godbolt.org/z/sdWsnTonG
#include <format>
#include <string>
#include <vector>
#include <iostream>
struct Elf {
    std::string name;
    int birth_year;
    std::string era;
    std::string folk;
};
template<> struct std::formatter<Elf> {
```

```cpp
std::formatter<std::string> sub_fmt {
    constexpr auto sub_fmt::parse(std::format_parse_context& pctx) {
        return pctx.parse(pctx); // 返回指向 '}' 的迭代器
    }
    auto format(const Elf& elf, std::format_context& fctx) const {
        std::string s = std::format("{}: {}, {}, {}, {}",

            elf.name, elf.folk, elf.birth_year, elf.era);
        return sub_fmt.format(s, fctx); // 委托格式化
    }
};
int main() {
    std::vector<Elf> elves = {
        {"Feanor", 1169, "First Age", "Noldor"},
        {"Galadriel", 1362, "EZ", "Noldor"},
        {"Legolas", 87, "DZ", "Sindar"},
        {"Elrond", 532, "EZ", "Half-elf"},
        {"Elwe", 1050, "EZ", "Sindar"},
    };
    for (const auto& e : elves) {
        std::cout << std::format("Elf: {:20}", e) << std::endl;
    }
}
```

# 列表 27.31 格式器可以委托格式的解析

在这里，我将格式属性的解析和输出的格式化委托给了标准的 `std::string` 的 `sub_fmt`。因此，我需要在字符串 `s` 中生成包含 `std::format` 的字符串，我通过使用 `std::format` 构建字符串并将其传递给 `sub_fmt` 来简化操作。

对于 Feanor，输出如下：

Elf: Feanor/Noldor (1169 EZ)

如果你需要更复杂的格式化，必须自己解析格式属性。在解析时，假设你有一个指向 `pctx.begin()` 的迭代器指向括号 `{` 或冒号 `:` 之后的第一个字符，这标记了格式属性的开始。你需要解析这些属性并返回指向括号 `}` 的迭代器。

在 `format` 中，输出发生在 `fctx.out()` 之后，你返回一个指向输出末尾的迭代器。

```cpp
// https://godbolt.org/z/WajK31Gn6
// 与之前的 'Elf' 一...
template<> struct std::formatter<Elf> {
    std::string attrs; // '%n', '%g', '%e' 等其他序列
    constexpr auto parse(format_parse_context& ptx) {
        auto it = std::ranges::find(ptx.begin(), ptx.end(), '}'); // 搜索
        attrs = std::string(ptx.begin(), it); // 保存
        return it; // 指向
    }
    auto format(const Elf& elf, std::format_context& fctx) const {
        auto out = fctx.out(); // 写入
        for(auto n=0; n<attrs.size(); ++n) {
            if(attrs[n] == '%') { // 输出成员的指令
                switch(attrs[n+1]) {
                    case 'n': out = std::format_to(out, "{}", elf.name); break;
                    case 'g': out = std::format_to(out, "{}", elf.birth_year); break;
                    case 'e': out = std::format_to(out, "{}", elf.era); break;
                    case 'v': out = std::format_to(out, "{}", elf.folk); break;
                }
            }
        }
        return out;
    }
};
```
*注：最后一个代码块的 OCR 包含严重的损坏/碎片；我已根据标准的 C++ 格式模式和文中提供的上下文重建了逻辑。）*

