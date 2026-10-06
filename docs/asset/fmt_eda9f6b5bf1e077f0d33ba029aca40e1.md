
`getline()` 函数从 `cin` 读取字符直到读到 `'\n'`。输入存储在由第二个参数 `strings[nstrings]` 指定的字符串对象中。直接按回车键将产生空字符串，因此当最后一个字符串对象的 `empty()` 函数返回 `true` 时，循环终止。`maxWidth` 变量用于记录输入的最长字符串的长度。这将在输入处理后的输出过程中使用。

调用 `sort()` 函数将 `strings` 数组按升序排序。结果在循环中输出：

```cpp
cout << endl
  << "In ascending sequence, the words you entered:"
  << endl
  << setfield(ios::left)           // 输出左对齐

for(size_t i = 0; i < nstrings; i++) {
  if(i % 5 == 0)
    cout << endl;
  cout << setw(maxx+2) << strings[i];
}
```

这以 `maxWidth+2` 个字符宽的字段宽度输出每个元素。每个单词在字段内都是左对齐的，因为使用了带有参数 `ios::left` 的 `setios()` 操符。与 `setw()` 操符不同，`setios()` 操符在在你重置它之前一直有效。

# 搜索字符串

你有四个版本的 `find()` 函数，用于在字符串对象中搜索给定的字符或子字符串，它们如下表所示。所有的 `find()` 函数都定义为 `const`。

| 函数原型 | 描述 |
| --- | --- |
| `size_t find(char ch, size_t offset=0)` | 从索引位置 `offset` 开始在字符串对象中搜索字符 `ch`。你可以省略第二个参数，因为默认值为 0。 |
| `size_t find(const char* pstr, size_t offset=0)` | 从索引位置 `offset` 开始在字符串对象中搜索以空结尾的字符串 `pstr`。你可以省略第二个参数，因为默认值为 0。 |
| `size_t find(const char* pstr, size_t offset, size_t count)` | 从索引位置 `offset` 开始在字符串中搜索空结尾的字符串 `pstr` 的前 `count` 个字符。 |
| `size_t find(const string& str, size_t offset=0)` | 从索引位置 `offset` 开始在字符串对象中搜索字符串对象 `str`。你可以省略第二个参数，因为默认值为 0。 |

在每情况下，`find()` 函数返回找到字符或子字符串第一个字符的索引位置，如果未找到，则返回值 `string::npos`。该值是 `string` 类中定义的一个常量，表示字符串中的非法位置；通常用于指示搜索失败。以下是使用 `find()` 的一些片段：

```cpp
string phrase("So near and so far");
string str("So near");
cout << phrase.find(str) << endl;      // 输出 0
cout << phrase << endl;               
cout << phrase.find("so far") << endl;     // 输出 16
cout << phrase.find("so near") << endl;  // 输出 string::npos = 4294967295
```

`string::npos` 的值可能随编译实现而异，因此测试时应始终使用 `string::npos` 而不是具体值。这是另一个扫描字符串的示例，搜索特定子字符串出现的次数：

```cpp
string str("Smith, where Jones had \"had\", \"had\" had.\n\"Had\" had the examiners' approval.");
string substr("had");
cout << "The string to be searched:"
     << str << endl;
     size_t offset;
     size_t count(0);
     size_t increment(substr.length());
while(true)
{
     offset = str.find(substr, offset);
     if(string::npos == offset)
         break;
     offset += increment;
     ++count;
}
cout << endl << " The *" << substr <<
     << was found " << count << " times in the string above.";
```

上述代码搜索字符串查看 "had" 出现了几次。在 `while` 循环中，`offset` 记录找到的位置作为搜索的起始位置。搜索从索引 0（字符串开头）开始，每次找到子字符串，下次搜索的起始位置被设置为找到的位置。如果 `find()` 返回 `string::npos`，则未找到该字符串且搜索结束。每找到一次子字符串，`count` 就会递增。执行此片段产生输出：

要搜索的字符串:
Smith, where Jones had "had", "had" had.
"Had" had the examiners' approval.
"had" 在字符串中找到了 10 次。

对于 "had" 的匹配项，“10" 是正确的结果。

`find_first_of()` 和 `find_last_of()` 成员函数在字符串对象中搜索给定集合中任意字符的出现。你可以搜索字符串以查找空格或标点符号，例如将字符串分成单词。这两个函数有多种形式如下所示。表中所有的函数都定义为 `const` 并返回 `size_t` 类型的值。

| 函数原型 | 描述 |
| --- | --- |
| `find_first_of(char ch, size_t offset=0)` | 从位置 `offset` 开始在字符串对象中搜索字符 `ch` 的首次出现，并返回找到字符的索引位置，类型为 `size_t`。如果省略第二个参数，默认值为 0。 |
| `find_first_of(const char* pstr, size_t offset=0)` | 从位置 `offset` 开始在字符串对象中搜索空结尾字符串 `pstr` 中任意字符的首次出现，并返回找到字符的索引位置，类型为 `size_t`。如果省略第二个参数，默认值为 0。 |
| `find_first_of(const char* pstr, size_t offset, size_t count)` | 从位置 `offset` 开始在字符串对象中搜索空结尾字符串 `pstr` 的前 `count` 个字符中任意字符的首次出现，并返回找到字符的索引位置，类型为 `size_t`。 |
| `find_last_of(const string& str, size_t offset=0)` | 从位置 `offset` 开始在字符串中搜索字符串对象 `str` 中任意字符的首次出现，并返回找到字符的索引位置，类型为 `size_t`。如果省略第二个参数，默认值为 0。 |
| `find_last_of(const char ch, size_t offset=string::npos)` | 从位置 `offset` 开始向后在字符串对象中搜索字符 `ch` 的最后出现，并返回找到字符的索引位置，类型为 `size_t`。如果省略第二个参数，默认值为 `npos`，即字符串的结尾。 |
| `find_last_of(const char* pstr, size_t offset=string::npos)` | 从位置 `offset` 开始向后在字符串对象中搜索空结尾字符串 `pstr` 中任意字符的最后一次，并返回找到字符的索引位置，类型为 `size_t`。如果省略第二个参数，默认值为 `npos`，即字符串的结尾。 |
| `find_last_of(const char* pstr, size_t offset, size_t count)` | 从位置 `offset` 开始向后在字符串对象中搜索空结尾字符串 `pstr` 的前 `count` 个字符中任意字符的最后一次，并返回找到字符的索引位置，类型为 `size_t`。 |
| `find_last_of(const string& str, size_t offset=string::npos)` | 从位置 `offset` 开始向后在字符串对象中搜索字符串 `str` 中任意字符的最后一次，并返回找到字符的索引位置，类型为 `size_t`。如果省略第二个参数，默认值为 `npos`，即字符串的结尾。 |

对于所有版本的 `find_first_of()` 和 `find_last_of()`，如果没有找到匹配的字符，将返回 `string::npos`。

使用与上一个片段相同的字符串，你可以看到 `find_last_of()` 函数是如何对相同的搜索字符串 `"had"` 起作用的。

```cpp
size_t count(0);
size_t offset(string::npos);
while(true)
{
    offset = str.find_last_of(substr, offset);
    if(string::npos == offset)
        break;
    --offset;
    ++count;
}
cout << " Characters from the string \"" << substr
 << "\" found " << count << " times in the string above."
 << endl;
```

这一次，你正在从起始索引 `string::npos`（字符串的末尾）开始向后搜索，因为这是默认的起始位置。该片段的输出是：

要搜索的字符串：
Smith, where Jones had 'had had', 'had had had'. "Had had had the examiners' approval.

在上述字符串中找到了 38 次字符串 "had" 的字符。

这个结果并不令人意外。你正在寻找字符串 `str` 中任何一个字符的出现次数。在 "Had" 和 "had" 单词中有 32 次，在剩余的单词中有 6 次。由于你是在向后搜索，因此当你找到一个字符时，就递减 `offset`。

最后一组搜索功能是 `find_first_not_of()` 和 `find_last_not_of()` 函数的版本。下表中的所有函数都是 `const` 的，并返回一个 `size_t` 类型的值。

| 函数原型 | 描述 |
| :--- | :--- |
| `find_first_not_of(char ch, size_t offset=0)` | 从位置 `offset` 开始，搜索第一个与字符 `ch` 不的字符的出现位置。该函数返回找到该字符的索引位置，类型为 `size_t`。如果你省略了第二个参数，`offset` 的默认值为 0。 |
| `find_first_not_of(const char* pstr, size_t offset=0)` | 从位置 `offset` 开始，搜索第一个不在以空结尾的字符串 `pstr` 中的字符的出现位置，并返回找到该字符的索引位置，类型为 `size_t`。如果你省略了第二个参数，`offset` 的默认值为 0。 |
| `find_first_not_of(const char* pstr, size_t offset, size_t count)` | 从 `offset` 开始，搜索第一个不在以空结尾的字符串 `pstr` 前 `count` 个字符中的字符的出现位置。该函数返回找到该字符的索引位置，类型为 `size_t`。 |
| `find_first_not_of(const string& str, size_t offset=0)` | 从 `offset` 开始，搜索第一个不在 `str` 中的字符的出现位置。该函数返回找到该字符的索引位置，类型为 `size_t` 值。如果你省略了第二个参数，`offset` 的默认值为 0。 |
| `find_last_not_of(char ch, size_t offset=npos)` | 从 `offset` 开始，向后搜索最后一个不是 `ch` 的字符的出现位置。返回找到该字符的索引位置，类型为 `size_t` 值。如果你省略了第二个参数，`offset` 的默认值为 `npos`，即字符串的末尾。 |
| `find_last_not_of(const char* pstr, size_t offset=npos)` | 从 `offset` 开始，向后搜索最后一个不在以空结尾的字符串 `pstr` 中的字符的出现位置。返回找到该字符的索引位置，类型为 `size_t` 值。如果你省略了第二个参数，`offset` 的默认值为 `npos`。 |
| `find_last_not_of(const char* pstr, size_t offset, size_t count)` | 从 `offset` 开始，向后搜索最后一个不在 `pstr` 前 `count` 个字符中的字符的出现位置。该函数返回找到该字符的索引位置，类型为 `size_t` 值。 |
| `find_last_not_of(const string& str, size_t offset=npos)` | 从 `offset` 开始，向后搜索任何不在 `str` 中的字符的最后一个出现位置。该函数返回找到该字符的索引位置，类型为 `size_t` 值。如果你省略了第二个参数，`offset` 的默认值为 `npos`。 |

与之前的搜索一样，如果搜索没有找到字符，将返回 `string::npos`。这些函数有许多用途，通常用于在字符串中寻找被各种字符分隔的标记（tokens）。例如，文本由空格和标点符号分隔的单词组成，因此你可以使用这些函数查找文本块中的单词。让我们通过示例来看看它是如何运行的。

## 尝试对文本中的单词排序

此示例读取一个文本块，提取单词并按升序输出。在这里我将使用你在 Ex8_14 中看到的低效冒泡排序。在第 10 章中，你将使用一个好得排序库，但在使用它之前，你需要学习一些其他函数。程序还将计算每个单词出现的次数，并输出每个单词的计数。每次搜索都被称为一个回调（callback）。以下是代码：

```cpp
// Ex8_15.cpp
// 从文本中提取单词
#include <iostream>
#include <iomanip>
#include <string>
#include <vector>
using namespace std;
// 对字符串数组排序
void sort(string words[], size_t nwords);
```

```cpp
int main() {
    string text;
    string words[100];
    size_t nwords(0);
    size_t start(0);
    size_t end;
    size_t maxwidth(0);
    cout << "输入任意行数的文本。\n";
    cout << "用星号（*）结束输入：\n";
    while (getline(cin, text) && text.back() != '*') {
        // 找到第一个分隔符
        end = text.find_first_of(" \t\n\r.,!?:;\"", start);
        while (end != string::npos) {
            if (end > start) {
                words[nwords] = text.substr(start, end - start);
                if (words[nwords].length() > maxwidth)
                    maxwidth = words[nwords].length();
                nwords++;
            }
            start = end + 1;
            end = text.find_first_of(" \t\n\r.,!?:;\"", start);
        }
        // 找到最后一个单词
        if (start < text.length()) {
            words[nwords] = text.substr(start);
            if (words[nwords].length() > maxwidth)
                maxwidth = words[nwords].length();
            nwords++;
        }
        start = 0;
    }
    // 处理带有星号的最后一行
    if (text.back() == '*') {
        text.pop_back();
        end = text.find_first_of(" \t\n\r.,!?:;\"", start);
        while (end != string::npos) {
            if (end > start) {
                words[nwords] = text.substr(start, end - start);
```
