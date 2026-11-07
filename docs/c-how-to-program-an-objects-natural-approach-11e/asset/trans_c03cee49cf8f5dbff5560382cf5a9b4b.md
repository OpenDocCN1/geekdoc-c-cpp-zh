
在幸存者中，约三分之二是女性，且头等舱乘客的幸存率高于其他乘客舱位。

```cpp
// percentages who survived by male/female, 1st/2nd/3rd class
std::cout << std::format("Female survivor percentage: {:.2f}%\n",
    100.0 * survivingFemales / survivorCount)
    << std::format("Male survivor percentage: {:.2f}%\n",
        100.0 * survivingMales / survivorCount)
    << std::format("1st class survivor percentage: {:.2f}%\n",
        100.0 * surviving1st / survivorCount)
    << std::format("2nd class survivor percentage: {:.2f}%\n",
        100.0 * surviving2nd / survivorCount)
    << std::format("3rd class survivor percentage: {:.2f}%\n",
        100.0 * surviving3rd / survivorCount);
```

```text
Female survivor percentage: 67.80%
Male survivor percentage: 32.20%

1st class survivor percentage: 40.00%
2nd class survivor percentage: 23.80%
3rd class survivor percentage: 36.20%
```

## 检查点

1. *(填空)* CSV 文件的第一行通常包含________。  
   **答案：** 列名。

2. *(填空)* 在表示数据集的 CSV 文件中，行包含数据，而列通常被称为数据集的________。  
   **答案：** 特征。

3. *(判断正误)* `std::ranges` 算法的一个优点是，你不需要指定容器的开头和结尾——`std::ranges` 算法会为你处理这一点，从而简化代码。  
   **答案：** 正确。

## 8.20 对象——自然数据科学案例研究：正则表达式入门

有时你需要识别文本中的模式，例如电话号码、电子邮件地址、邮政编码、网页地址、社会安全号码等。正则表达式字符串描述了一种搜索模式，用于匹配其他字符串中的字符。正则表达式可以帮助你从非结构化文本（如社交媒体帖子）中提取数据。它们对于在尝试处理数据之前确保数据格式正确也很重要。

### 验证数据

在处理文本数据之前，你通常会使用正则表达式来验证它。例如，你可能会检查：

- 美国邮政编码由五位数字（如 02215）组成，或由五位数字后跟一个连字符和另外四位数字（如 02215-4775）组成。

### 匹配字面字符

`<regex>` 函数 `regex_match` 在其第一个参数中的整个字符串与第二个参数中的模式匹配时返回 true。默认情况下，模式匹配区分大小写。稍后你将看到如何执行不区分大小写的匹配。让我们从匹配字面字符开始——即与自身匹配的字符。第 9 行创建了一个正则表达式对象 `r1`，用于模式 `"02215"`，其中只包含按指定顺序与自身匹配的字面数字。第 12 行对字符串 `"02215"` 和 `"51220"` 调用 `regex_match`。两者具有相同的数字，但只有 `"02215"` 的数字顺序正确，能够匹配。

```cpp
// fig08_16.cpp
// Matching entire strings to regular expressions.
#include <format>
#include <iostream>
#include <regex>

int main() {
    // fully match a pattern of literal characters
    std::regex r1{"02215"};
    std::cout << std::format("Matching against: 02215\n"
        "02215: {}; 51220: {}\n\n",
        std::regex_match("02215", r1), std::regex_match("51220", r1));
}
```

```text
Matching against: 02215
02215: true; 51220: false
```

**图 8.16**  将整个字符串与正则表达式匹配。

### 元字符、字符类和量词

正则表达式通常包含各种称为元字符的特殊符号：

- `[]`  `{}`  `()`  `\`  `*`  `+`  `^`  `$`  `?`  `.`  `|`

`\` 元字符会开始每个预定义字符类，下表列出了其中几个字符类及其匹配的字符组。

| 字符类 | 匹配 |
|---|---|
| `\d` | 任意数字（0–9）。 |
| `\D` | 任意非数字字符。 |
| `\s` | 任意空白字符（如空格、制表符和换行符）。 |
| `\S` | 任意非空白字符。 |
| `\w` | 任意单词字符（也称为字母数字字符）——即任意大写或小写字母、任意数字或下划线。 |
| `\W` | 任意非单词字符。 |

要将任意元字符匹配为其字面值，请在其前面加上反斜杠。例如，`\$` 匹配美元符号（`$`），`\` 匹配反斜杠（`\`）。

### 匹配数字

让我们验证一个五位邮政编码。在正则表达式 `\d{5}`（由第 15 行的原始字符串字面量创建）中，`\d` 是表示数字（0–9）的字符类。字符类是一种匹配单个字符的正则表达式转义序列。要匹配多个字符，请在字符类后跟一个量词。量词 `{5}` 将 `\d` 重复五次，就像我们写了 `\d\d\d\d\d` 来匹配五个连续数字一样。第 18 行第二次调用 `regex_match` 返回 false，因为 `"9876"` 只包含四个连续数字。

```cpp
// fully match five digits
std::regex r2{R"(\d{5})"};
std::cout << R"(Matching against: \d{5})" << "\n"
    << std::format("02215: {}; 9876: {}\n",
        std::regex_match("02215", r2), std::regex_match("9876", r2));
```

```text
Matching against: \d{5}
02215: true; 9876: false
```

### 自定义字符类

方括号 `[]` 中的字符定义了一个自定义字符类，用于匹配单个字符。例如，`[aeiou]` 匹配小写元音字母，`[A-Z]` 匹配大写字母，`[a-z]` 匹配小写字母，`[a-zA-Z]` 匹配任意小写或大写字母。第 21 行定义了一个自定义字符类，用于验证不包含空格或标点符号的简单名字。

```cpp
// match a word that starts with a capital letter
std::regex r3{"[A-Z][a-z]*"};
std::cout << "Matching against: [A-Z][a-z]*\n"
    << std::format("Angel: {}; tina: {}\n",
        std::regex_match("Angel", r3), std::regex_match("tina", r3));
```

```text
Matching against: [A-Z][a-z]*
Angel: true; tina: false
```

名字可能包含许多字母。在正则表达式 `r3`（第 21 行）中，`[A-Z]` 匹配一个大写字母，`[a-z]*` 匹配任意数量的小写字母。`*` 量词匹配其左侧子表达式（此处为 `[a-z]`）的零次或多次出现。因此 `[A-Z][a-z]*` 匹配 `"Vivian"`、`"An"`，甚至 `"A"`。

当自定义字符类以脱字符（`^`）开头时，该类匹配任何未指定的字符。因此 `[^a-z]`（第 27 行）匹配任何不是小写字母的字符。

```cpp
// match any character that's not a lowercase letter
std::regex r4{"[^a-z]"};
std::cout << "Matching against: [^a-z]\n"
    << std::format("A: {}; a: {}\n\n",
        std::regex_match("A", r4), std::regex_match("a", r4));
```

```text
Matching against: [^a-z]
A: true; a: false
```

自定义字符类中的元字符会被视为字符本身。因此 `[*+$]`（第 33 行）匹配单个 `*`、`+` 或 `$` 字符。

```cpp
// match metacharacters as literals in a custom character class
std::regex r5{"[*+$]"};
std::cout << "Matching against: [*+$]\n"
    << std::format("*: {}; !: {}\n\n",
        std::regex_match("*", r5), std::regex_match("!", r5));
```

```text
Matching against: [*+$]
*: true; !: false
```

### * 与 + 量词

要要求名字中至少有一个小写字母，请将第 21 行中的 `*` 量词替换为 `+`（第 39 行）。这会匹配其左侧子表达式的至少一次出现。

```cpp
// matching a capital letter followed by at least one lowercase letter
std::regex r6{"[A-Z][a-z]+"};
std::cout << "Matching against: [A-Z][a-z]+\n"
    << std::format("Angel: {}; T: {}\n\n",
        std::regex_match("Angel", r6), std::regex_match("T", r6));
```

```text
Matching against: [A-Z][a-z]+
Angel: true; T: false
```

`*` 和 `+` 都是贪婪的——它们会尽可能多地匹配字符。因此正则表达式 `[A-Z][a-z]+` 匹配任何以大写字母开头、后跟至少一个小写字母的单词。你可以让 `*` 和 `+` 变为懒惰的，即通过在量词后附加问号（`?`）使它们尽可能少地匹配字符，如 `*?` 或 `+?`。

### 其他量词

`?` 量词本身匹配其左侧子表达式的零次或一次出现。在正则表达式 `labell?ed`（第 45 行）中，子表达式是字面字符 `"l"`。因此，在第 48-49 行的 `regex_match` 调用中，该正则表达式匹配 `labelled`（英式英语拼写）和 `labeled`（美式英语拼写），但在第 50 行的 `regex_match` 调用中，该正则表达式不匹配拼写错误的单词 `label1ed`。

