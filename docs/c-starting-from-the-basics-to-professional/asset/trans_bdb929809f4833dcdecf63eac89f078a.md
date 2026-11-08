
compare() 的第一个参数是 word 的子字符串中第一个字符的索引位置，该子字符串要与 word2 进行比较。第二个参数是子字符串中的字符数，合理地将其指定为第三个参数 word2 的长度。显然，如果你指定的子字符串长度与第三个参数的长度不同，那么按定义该子字符串和第三个参数就不相等。

你可以使用 compare 函数来搜索子字符串。下面是一个示例：

```cpp
std::string text {"Peter Piper picked a peck of pickled peppers."};
std::string word {"pick"};
for (size_t i{}; i < text.length() - word.length() + 1; ++i)
    if (text.compare(i, word.length(), word) == 0)
        std::cout << "text contains " << word << " starting at index " << i << std::endl;
```

这个循环会在 text 中索引位置 12 和 29 找到 word。循环变量的上限允许将 text 中最后的 word.length() 个字符与 word 进行比较。这并不是搜索的最高效实现。当找到 word 时，更高效的做法是安排下一次检查的 text 子字符串向后移动 word.length() 个字符，但前提是 text 末尾之前仍有 word.length() 个字符。不过，搜索字符串对象还有更简单的方法，你很快就会看到。

你可以使用 compare() 函数将一个字符串的子字符串与另一个字符串的子字符串进行比较。这需要向 compare() 传递五个参数。下面是一个示例：

```cpp
std::string text {"Peter Piper picked a peck of pickled peppers."};
std::string phrase {"Got to pick a pocket or two."};
for (size_t i{}; i < text.length() - 3; ++i)
    if (text.compare(i, 4, phrase, 7, 4) == 0)
        std::cout << "text contains " << phrase.substr(7, 4)
                  << " starting at index " << i << std::endl;
```

这两个额外参数分别是 phrase 中子字符串的索引位置及其长度。phrase 的子字符串会与 text 的子字符串进行比较。

还没完！compare() 函数还可以将字符串对象的子字符串与以空字符结尾的字符串进行比较。

```cpp
std::string text {"Peter Piper picked a peck of pickled peppers."};
for (size_t i{}; i < text.length() - 3; ++i)
    if (text.compare(i, 4, "pick") == 0)
        std::cout << "text contains \"pick\" starting at index " << i << std::endl;
```

这段代码的输出将与前面的代码相同；"pick" 会在索引位置 12 和 29 被找到。还有一种选择是通过指定字符数，从以空字符结尾的字符串中选择前 n 个字符。循环中的语句可以写成如下形式：

```cpp
if (text.compare(i, 4, "picket", 4) == 0)
    std::cout << "text contains \"pick\" starting at index " << i << std::endl;
```

compare() 的第四个参数指定从 "picket" 中使用多少个字符参与比较。

**注意** 你已经看到，`compare()` 函数可以相当自然地处理不同类型、不同数量的参数。我们之前简要提到的 `append()` 函数也是如此。这里看到的是几个同名但不同的函数。它们被称为*重载函数*，你将在下一章学习如何以及为什么创建它们。

### 使用 substr() 比较子字符串

当然，如果你记不住 `compare()` 函数较复杂版本中的参数顺序，可以使用 `substr()` 函数来提取 `string` 对象的子字符串。然后在许多情况下，你可以将结果与比较运算符一起使用。例如，要检查两个子字符串是否相等，你可以编写如下测试：

```cpp
std::string text {"Peter Piper picked a peck of pickled peppers."};
std::string phrase {"Got to pick a pocket or two."};
for (size_t i{}; i < text.length() - 3; ++i)
  if (text.substr(i, 4) == phrase.substr(7, 4))
    std::cout << "text contains " << phrase.substr(7, 4)
              << " starting at index " << i << std::endl;
```

与前面使用 `compare()` 函数的等效操作不同，这段新代码很容易理解。当然，它会稍微低效一些（因为创建了临时子字符串对象），但在这里，代码的清晰度和可读性远比边际性能提升重要。事实上，这是一条应当遵循的重要准则。你应该始终选择正确且可维护的代码，而不是容易出错、晦涩难懂的代码，即使后者可能快几个百分点。只有当基准测试表明性能有可能显著提升时，你才应该把事情复杂化。

**提示** 假设创建临时子字符串对象真的让你困扰（它不应该困扰你，但假设你是一位死硬的 C++ 开发者，每一个字节和时钟周期都很重要）。那么你可以将前一个示例中的前两行替换为：

```cpp
std::string_view text {"Peter Piper picked a peck of pickled peppers."};
std::string_view phrase {"Got to pick a pocket or two."};
```

你将在第 9 章学习所有关于 `string_views` 的内容，但简而言之，`string_view` 允许你使用与 `std::string` 相同的高层函数来检查任何类型的字符序列（在我们的例子中是字符串字面量），但额外保证它绝不会复制任何（子）字符串。`string_view` 对象只允许你查看字符串的字符（因此得名），而不能修改、添加或删除它们。

### 检查字符串的开头或结尾

有时需要检查一个字符串是否以给定的子字符串开头或结尾。当然，你仍然可以使用 `compare()` 或 `substr()` 来做到这一点。例如，像这样：

```cpp
std::string text {"Start with the end in mind."};
if (text.compare(0, 5, "Start") == 0)
    std::cout << "The text starts with 'Start'." << std::endl;
if (text.substr(text.length() - 3, 3) != "end")
    std::cout << "The text does not end with 'end'." << std::endl;
```

但这段代码的可读性并不出色，而且也很容易把那些恼人的子字符串索引弄错。幸运的是，C++20 引入了两个有用的成员函数来解决这个问题：starts_with() 和 ends_with()。

```cpp
std::string text {"Start with the end in mind."};
if (text.starts_with("Start"))
    std::cout << "The text starts with 'Start'." << std::endl;
if (!text.ends_with("end"))
    std::cout << "The text does not end with 'end'." << std::endl;
```

这段代码可读性极佳，而且完全不容易出错。除了 C 风格字符串或字符串对象之外，这两个函数也适用于单个字符：

```cpp
if (text.ends_with('.'))
    std::cout << "The text ends with a period.";
```

此外，starts_with() 和 ends_with() 在空字符串上使用总是完全安全的（自然，对于空字符串它们都总是返回 false）。而 []、front()、back() 或 substr() 则不是这样。

## 搜索字符串

除了 compare() 之外，你还有许多其他在字符串对象内搜索的替代方法。它们都涉及返回索引的函数。我们将从最简单的一类搜索开始。字符串对象有一个 find() 函数，用于查找子字符串在其中的索引。你也可以用它来查找给定字符的索引。你要搜索的子字符串可以是另一个字符串对象，也可以是字符串字面量。下面是一个小示例，展示了这些选项：

```cpp
// Ex7_04.cpp
// Searching within strings
import <iostream>;
import <string>;

int main()
{
    std::string sentence {"Manners maketh man"};
    std::string word {"man"};
    std::cout << sentence.find(word) << std::endl;  // Outputs 15
    std::cout << sentence.find("M") << std::endl;  // Outputs 0
    std::cout << sentence.find('k') << std::endl;  // Outputs 10
    std::cout << sentence.find('x') << std::endl;  // Outputs std::string::npos
}
```

¹ 嗯，实际上，如果吹毛求疵的话，几乎总是如此。每个字符串都以空字符串开头和结尾，甚至空字符串也是如此。
