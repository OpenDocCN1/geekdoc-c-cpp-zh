

```
A)dd  L)ook up  Q)uit: a Fred 5550134
A)dd  L)ook up  Q)uit: d
FRED 5550134
A)dd  L)ook up  Q)uit: a Ella 5559921
A)dd  L)ook up  Q)uit: l Ella
ELLA 5559921
A)dd  L)ook up  Q)uit: l Fred
FRED 5550134
A)dd  L)ook up  Q)uit: d
ELLA 5559921
FRED 5550134
A)dd  L)ook up  Q)uit: q
```

清单 21.10 (phone1.cpp) 包含一个名为“dump”的秘密命令，用于打印映射对象的内容。该命令执行以下循环：

```
for (auto& elem : contacts)
    std::cout << elem.first << " " << elem.second << '\n';
```

这段代码揭示了 std::map 对象将其元素存储为 std::pair 对象的事实。

请注意，我们将电话号码存储为整数，但映射对象中的值不仅限于整数。

为了进一步说明映射的用途，请考虑使用条件逻辑将一些西班牙语单词翻译成英语的清单 21.11 (translateif.cpp)。

### 清单 21.11: translateif.cpp

```
#include <iostream>
#include <string>

int main() {
    std::string word = "";        // Initial word to ensure loop entry
    while (word != "quit") {      // Loop until user presses return by itself
        // Obtain word from the user
        std::cout << "Enter Spanish word: ";
        std::cin >> word;
        if (word == "uno")
            std::cout << "one\n";
        else if (word == "dos")
            std::cout << "two\n";
        else if (word == "tres")
            std::cout << "three\n";
        else if (word == "cuatro")
            std::cout << "four\n";
        else if (word == "cinco")
            std::cout << "five\n";
        else if (word == "seis")
            std::cout << "six\n";
        else if (word == "siete")
            std::cout << "seven\n";
        else if (word == "ocho")
            std::cout << "eight\n";
        else // Unknown word
            std::cout << "???\n";
    }
}
```

```
}
}
```

清单 21.11 (translateif.cpp) 可以成功将八个西班牙语单词翻译成英语。如果我们希望增加程序的词汇量，就必须通过为每个新单词添加另一个 else if 块来修改程序的逻辑。清单 21.12 (translatemap.cpp) 提供了一种更好的方法；它使用映射来辅助翻译。

### 清单 21.12: translatemap.cpp

```
#include <iostream>
#include <fstream>
#include <string>
#include <map>
#include <algorithm>

// Convenient type name alias
using Dictionary = std::map<std::string, std::string>;

// English-Spanish word list
Dictionary word_map;

// Load the list of words from a file
void load_words(std::string filename, Dictionary& words) {
    std::ifstream in(filename);
    if (in.good()) { // Make sure the file was opened properly
        std::string english_word, spanish_word;
        while (in >> spanish_word >> english_word) // Read until end of file
            words[spanish_word] = english_word;
    }
    else
        std::cout << "Unable to load in the file\n";
}

int main() {
    // Load words from file
    load_words("engspanwords.txt", word_map);

    std::string word = "";
    while (word != "quit") { // Loop until user presses return by itself
        // Obtain word from the user
        std::cout << "Enter Spanish word: ";
        std::cin >> word;
        std::cout << word << " -> " << word_map[word] << '\n';
    }
}
```

请注意，清单 21.12 (translatemap.cpp) 使用的映射中，键和值都是字符串。清单 21.12 (translatemap.cpp) 配合包含以下数据的文本文件 engspanwords.txt：

| 西班牙语 | 英语 |
|---------|---------|
| uno | one |
| dos | two |
| tres | three |
| cuatro | four |
| cinco | five |
| seis | six |
| siete | seven |
| ocho | eight |

它翻译的单词与清单 21.11 (translateif.cpp) 相同，但我们完全不需要修改程序的逻辑来扩展程序的词汇量；我们只需将适当的单词添加到文本文件中。程序运行时，这些单词将成为我们映射中的键和值项。如果希望包含足够多的单词以使程序实用，这是一个显著的差异。

与 std::set 类似，主要的 C++ 平台使用红黑树（参见 https://en.wikipedia.org/wiki/Red-black_tree）作为 std::map 类的底层数据结构。这种数据结构的特性使得映射对象中的键查找非常快。

## 21.5 std::unordered_map 数据类型

std::unordered_map 类型是 C++ 关联容器的另一个示例。std::unordered_map 对象的工作方式类似于 std::map 对象，但它们各自使用不同的底层数据结构。大多数 std::map 实现使用红黑树（参见 https://en.wikipedia.org/wiki/Red-black_tree）来存储映射的元素，而无序映射使用哈希表（参见 https://en.wikipedia.org/wiki/Hash_table）。这种差异使得无序映射通常比映射通过键访问元素更快。映射对象牺牲原始速度，以便能够根据键高效地按顺序访问元素。无序映射对象确实是无序的；它们不提供客户端按键顺序遍历其键值对的有效方式。

为了在程序中使用 std::unordered_map 对象，我们必须使用适当的 #include 指令：
#include <unordered_map>

与 std::map 类一样，std::unordered_map 类是一个模板类，因此在声明实例时，我们必须在尖括号中提供类型参数，如以下示例所示：
std::unordered_map<std::string, int> my_map;

在此示例中，映射对象中的每个整数都有一个关联的字符串键。

清单 21.13 (ordvsunord.cpp) 以相同的顺序将相同的字符串添加到映射对象和无序映射对象中。然后它遍历每个容器，打印迭代器访问的每个元素。

```
Listing 21.13: ordvsunord.cpp

#include <iostream>
#include <string>
#include <map>
#include <unordered_map>

int main() {
    std::map<std::string, int> m;
    std::unordered_map<std::string, int> um;
```

```
// Add some names in random order
m["fred"] = um["fred"] = 23;
m["adam"] = um["adam"] = 99;
m["cathy"] = um["cathy"] = 2;
m["wilma"] = um["wilma"] = 50;
m["betty"] = um["betty"] = 19;
m["roger"] = um["roger"] = 44;
m["kim"] = um["kim"] = 7;
m["doug"] = um["doug"] = 10;
m["zach"] = um["zach"] = 5;
m["tom"] = um["tom"] = 34;

// Print the names in each container
for (auto& p : m) {
    std::cout << p.first << ": " << p.second << " ";
    std::cout << '\n';
    std::cout << "----------------------------------\n";
}
for (auto& p : um) {
    std::cout << p.first << ": " << p.second << " ";
    std::cout << '\n';
    std::cout << "----------------------------------\n";
}

// Add some more names to each container
m["tammy"] = um["tammy"] = 80;
m["joey"] = um["joey"] = 80;
m["abby"] = um["abby"] = 80;

// Again, print the names in each container
for (auto& p : m) {
    std::cout << p.first << ": " << p.second << " ";
    std::cout << '\n';
    std::cout << "----------------------------------\n";
}
for (auto& p : um) {
    std::cout << p.first << ": " << p.second << " ";
    std::cout << '\n';
    std::cout << "----------------------------------\n";
}
}
```

在一个系统上运行清单 21.13 (ordvsunord.cpp) 会打印

![](img/e84ad11adb18201d71595b31ce6c9eff_732_0.png)

输出表明，我们可以按键的顺序遍历映射对象的元素。字符串键按字典顺序排列。无序映射的顺序看起来是随机的。

清单 21.13 (ordvsunord.cpp) 向两个映射对象中添加了一些额外元素。插入操作不会破坏映射对象的字典键顺序，但请注意，插入操作在无序映射中出现在看似随机的位置。

无序映射中元素的顺序并非真正随机；一种称为哈希函数的特殊函数在插入时决定它们在无序映射中的位置。这种哈希过程使得无序映射比常规映射对象稍快。如果访问速度至关重要且无需按顺序访问元素，那么 C++ std::unordered_map 是更好的选择。

## 21.6 使用关联容器进行计数

关联容器用于计数很有用。我们有使用变量进行计数的经验；请回顾清单 6.3 (countup.cpp) 和清单 6.21 (startree.cpp)。这些程序一次只计算一件事，因此每个程序只使用一个计数器变量。通常，我们需要为每个要管理的计数使用单独的变量。清单 21.14 (countnegnonneg.cpp) 使用一个函数来计算整数向量中负数和非负数的数量，并返回带有结果的 std::pair：

```
Listing 21.14: countnegnonneg.cpp

#include <iostream>
#include <vector>
#include <tuple>

std::pair<int, int> count_neg_nonneg(const std::vector<int>& nums) {
    // Initialize counters
    int neg_count = 0, nonneg_count = 0;
    for (int num : nums)
        if (num < 0)
            neg_count++;
        else
            nonneg_count++;
    return std::make_pair(neg_count, nonneg_count);
}

int main() {
    auto counts = count_neg_nonneg({8, -3, -1, 7, 7, -2, 0, 3});
    std::cout << counts.first << " " << counts.second << '\n';
}
```

由于我们需要计算两种不同的东西，因此必须使用两个单独的计数器。在此示例中，我们使用 neg_count 和 nonneg_count 充当计数器变量。

顺便提一下，请考虑清单 21.14 (countnegnonneg.cpp) 的变体，如清单 21.15 (countnegnonneg2.cpp) 所示。

```
Listing 21.15: countnegnonneg2.cpp

#include <iostream>
#include <vector>
#include <tuple>

// Make an alias for a more complicated type name
using IntPair = std::pair<int, int>;
```

