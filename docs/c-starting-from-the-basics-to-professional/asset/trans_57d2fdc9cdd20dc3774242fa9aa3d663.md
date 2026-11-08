
在每个输出语句中，都会通过调用 `sentence` 的 `find()` 函数从头开始搜索 `sentence`。该函数返回被搜索内容第一次出现时首字符的索引。在最后一条语句中，字符串中找不到 `'x'`，因此返回 `std::string::npos`。这是一个在 `<string>` 模块中定义的常量。它表示字符串中的非法字符位置，用于表示搜索失败。

在我们的计算机上，Ex7_04 因此产生这四个数字：

- 15
- 0
- 10
- 18446744073709551615

从该输出可以看出，`std::string::npos` 被定义为一个非常大的数。更具体地说，它是类型 `size_t` 所能表示的最大值。对于 64 位平台，该值等于 2<sup>64</sup>−1，数量级为 10<sup>19</sup>——即 1 后面跟 19 个零。因此，你不太可能处理长到足以让 npos 表示有效索引的字符串。给你一个直观印象：我们上次统计时，英文版维基百科的所有字符可以放进一个仅有 210 亿个字符的字符串中——仍比 npos 小约 8.78 亿倍。

当然，对于搜索失败，你应当用类似下面的语句来处理：

```cpp
if (sentence.find('x') == std::string::npos)
    std::cout << "Character not found" << std::endl;
```

**注意** 当作为布尔值使用时，`std::string::npos` 常量求值为 true，而不是 false。

唯一求值为 false 的数值是零，而零作为索引是完全有效的值。因此，你应注意不要写出这样的代码：

```cpp
if (!sentence.find('x'))    // Oops...
    std::cout << "Character not found" << std::endl;
```

虽然这个 if 语句读起来似乎合理，但它实际做的事情却相当不合理。当字符 'x' 在索引 0 处被找到时，也就是对于所有以 'x' 开头的句子，它会打印 "Character not found"。

## 在子字符串中搜索

`find()` 函数的另一种变体允许你从指定位置开始搜索字符串的一部分。例如，在 `sentence` 像之前那样定义的情况下，你可以这样写：

```cpp
std::cout << sentence.find("an", 1) << std::endl;    // Outputs 1
std::cout << sentence.find("an", 3) << std::endl;    // Outputs 16
```

每条语句都从第二个参数指定的索引开始搜索 `sentence`，直到字符串末尾。第一条语句找到字符串中第一次出现的 "an"。第二条语句找到第二次出现，因为搜索从索引位置 3 开始。

你可以将字符串对象作为 `find()` 的第一个参数传入，从而搜索该字符串对象。下面是一个例子：

```cpp
std::string sentence {"Manners maketh man"};
std::string word {"an"};
int count {};                                      // Count of occurrences
for (size_t i {}; i <= sentence.length() - word.length(); )
{
    size_t position = sentence.find(word, i);
    if (position == std::string::npos)
        break;
    count++;
    i = position + 1;
}
std::cout << "\"" << word << "\" occurs in \"" << sentence
          << "\" " << count << " times." << std::endl;  // 2 times...
```

字符串索引的类型是 `size_t`，因此存储 `find()` 返回值的 `position` 也是该类型。循环索引 `i` 定义了 `find()` 操作的起始位置，所以它也是无符号类型。`word` 在 `sentence` 中最后一次出现的位置，至少要从 `sentence` 末尾往前 `word.length()` 个位置开始，因此循环中 `i` 的最大值是 `sentence.length() - word.length()`。递增 `i` 的循环表达式被省略了，因为这一步在循环体中完成。

如果 `find()` 返回 npos，说明没有找到 `word`，因此循环通过执行 break 语句结束。否则，`count` 递增，并且 `i` 被设置为找到 `word` 的位置之后的一个位置，为下一次迭代做准备。你可能认为应该把 `i` 设置为 `i + word.length()`，但这样无法找到重叠的出现，例如在字符串 "banana" 中搜索 "an" 时。

你还可以在字符串对象中搜索 C 风格字符串或字符串字面量的子串。在这种情况下，`find()` 的第一个参数是以空字符结尾的字符串，第二个参数是你想要开始搜索的索引位置，第三个参数是你想从该以空字符结尾的字符串中取多少个字符作为要查找的字符串。下面是一个例子：

```cpp
std::cout << sentence.find("ananas", 8, 2) << std::endl; // Outputs 16
```

这会从 `sentence` 中的位置 8（也就是在 Manners 之后）开始，在 `sentence` 中搜索 "ananas" 的前两个字符（即 "an"）。下面的变体展示了更改参数的效果：

```cpp
std::cout << sentence.find("ananas", 0, 2) << std::endl; // Outputs 1
std::cout << sentence.find("ananas", 8, 3) << std::endl; // Outputs std::string::npos
```

第一次搜索现在从 `sentence` 的开头查找 "an"，并在索引 1 处找到它。第二次搜索查找 "ana"，但失败了，因为该子串不在 `sentence` 中。

下面是一个程序，它在字符串对象中搜索给定的子串，并确定该子串出现了多少次：

```cpp
// Ex7_05.cpp
// Searching within substrings
import <iostream>;
import <string>;

int main()
{
    std::string text;             // The string to be searched
    std::string word;             // Substring to be found
    std::cout << "Enter the string to be searched and press Enter:\n";
    std::getline(std::cin, text);

    std::cout << "Enter the string to be found and press Enter:\n";
    std::getline(std::cin, word);

    size_t count{};               // Count of substring occurrences
    size_t index{};               // String index
    while ((index = text.find(word, index)) != std::string::npos)
    {
        ++count;
        index += word.length();   // Advance by full word (discards overlapping occurrences)
    }

    std::cout << "Your text contained " << count << " occurrences of \""
              << word << "\"." << std::endl;
}
```

下面是一些示例输出：

```text
Enter the string to be searched and press Enter:
Smith, where Jones had had "had had", had had "had". "Had had" had had the examiners' approval.
Enter the string to be found and press Enter:
had
Your text contained 10 occurrences of "had".
```

这里只有十处 "had" 出现。"Had" 不算，因为它以大写字母开头。程序在 `text` 中搜索 `word` 里的字符串，这两个字符串都是使用 `getline()` 从标准输入流读取的。输入以换行符终止，按下 Enter 时就会产生换行符。搜索在 while 循环中进行，只要 `text` 的 `find()` 函数不返回 npos，循环就会继续。返回值为 npos 表示从指定索引到字符串末尾，在 `text` 中未找到搜索目标，因此搜索结束。每次迭代返回非 npos 的值时，说明在 `text` 中找到了 `word` 中的字符串，因此 `count` 递增，`index` 增加该字符串的长度；这里假设我们不是在搜索重叠出现。这个循环中发生了很多事情，为了帮助你理解操作过程，图 7-3 展示了该过程。

另一个选项是查找*不在*给定集合中的字符。`find_first_not_of()` 和 `find_last_not_of()` 函数可以做到这一点。要找到 `text` 中第一个不是元音的字符的位置，你可以这样写：

```cpp
std::cout << text.find_first_not_of("AaEeIiOoUu") << std::endl; // Outputs 0
```

第一个不是元音的字符显然就是第一个字符，位于索引 0。

让我们在一个可运行的示例中尝试其中一些函数。这个程序从字符串中提取单词。它结合使用了 `find_first_of()` 和 `find_first_not_of()`。代码如下：

```cpp
// Ex7_06.cpp
// Searching a string for characters from a set
import <iostream>;
import <format>;
import <string>;
import <vector>;

int main()
{
    std::string text;
    std::cout << "Enter some text terminated by *:\n";
    std::getline(std::cin, text, '*');

    const std::string separators{ " ,;:.\"!?'\n" };   // Word delimiters
    std::vector<std::string> words;                   // Words found
    size_t start { text.find_first_not_of(separators) }; // First word start index

    while (start != std::string::npos)                // Find the words
    {
        size_t end = text.find_first_of(separators, start + 1); // Find end of word
        if (end == std::string::npos)                  // Found a separator?
            end = text.length();                       // No, so set to end of text
        words.push_back(text.substr(start, end - start)); // Store the word
        start = text.find_first_not_of(separators, end + 1); // Find first character of next word
    }

    std::cout << "Your string contains the following " << words.size() << " words:\n";
    size_t count{};                                    // Number output
    for (const auto& word : words)
    {
        std::cout << std::format("{:15}", word);
        if (!(++count % 5))
            std::cout << std::endl;
    }
    std::cout << std::endl;
}
```
