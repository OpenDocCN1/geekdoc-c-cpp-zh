
如你所见，在这里你可以使用已经熟悉的关于 `unique_ptr` 的所有知识。你可以将其作为返回值，而无需担心释放问题。通过 `data.get()`，你可以访问指向 C 数组的底层指针，通过 `data[n]`，你甚至可以直接通过 `unique_ptr` 访问单个元素。

一种特定的 C 数组形式是字符串字面量，这特别重要，因为它非常常见：`const char[]` C 数组。

如果你直接将文本作为字面量写入源码中，编译器会将其解释为类型为 `char` 的 C 数组，其大小与文本长度对应。然而，末尾有一个字符是不可见的：每个字符串字面量都以 `'\0`（值为零的字符）结尾，用标记其结束。

所以你这样写是完全正确的：

```
const char hello[3] = "hi";
```

`hi` C 数组的长度为三个字符。它包含元素 `{'h', 'i', '\0'}`。因此，你也可以用一种更麻烦的方式写它：

```
const char hello[3] = { 'h', 'i', '\0' };
```

这是完全等价的，但出于显而易见的原因很少这样做。

你还可以简化其他内容。当你在定义变量以这种方式指定字面量时，编译器可以确定 C 数组的大小。你不需要自己数。只需写下：

```
const char hello[] = "hi";
```

这也将变量 `hello` 定义为 `const char[3]`。

在实践中，使用数组括号 `[]` 还是指针星号 `*` 来声明类型通常并不重要。选择更适合你的方式即可。有一点可能寻的是，数组括号放在变量之后（尽管它们实际上属于变量的类型），而指针星号被放在类型之后——为了符合更直观的表示法：

```cpp
// https://godbolt.org/z/S6sss481E
const char vimes[13] = "Samuel Vimes"; // const char[13]
const char colon[] = "Fred Colon"; // const char[11]
const char* nobby = "Nobby Nobbs"; // const char[12]
```

当你将此类文本字面量与字符串配合时，你甚至不会注意到它是一个 `const char[]`。有一个构造函数可以将 `const char*` 转换为 `string`：

```cpp
// https://godbolt.org/z/oKsz7d55T
#include <string>
#include <iostream>
using std::cout; using std::cout;
```

```cpp
string greet(string name) {
    return name + "!";
} // string operator+(string, const char*)
```

```cpp
int main() {
    string name = "Havalock Vetinari"; // 式: string(const char*)
    cout << "Angua"; // ostream& operator<<(ostream,
    const char*);
    cout << // ostream& operator<<(ostream,
    string);
    greet("Carrot Ironfoundersson"); // 隐式: string(const char*)
}
```

**列表 20.13** 使用 "string" 时，你往往甚至注意到文本字面量是 "const char[]"。

虽然 `cout << "Angua"` 直接输出 C 数组，但通过 `cout << greet(...)` 输出的是返回的字符串。`greet` 的参数从 C 数组隐式转换为 `string`。对于 `greet()` 的返回值，现有的字符串使用 `operator+-` 与 `const char[]` 拼接，从而产生一个新的新字符串。

## 20.8 迭代器

容器
指针可以被视为迭代器的一种特例，而迭代器又是容器的一部分。迭代器在第 24 章第 24.2 节详细解释。尽管如此，我想向你展示指针如何与 `vector`、`array` 和 `string` 等容器相互作用（这一点已经提到过）。

如果你已经了解关于原始指针和 C 数组的所有知识，那么也是时候考虑迭代器的原理了。归根结底，这很简单：原始指针之于 C 数组，迭代器之于标准容器区别在于你可以用迭代器和标准容器做的事情比指针和 C 数组多得多。这是因为迭代器被实现为类，你可以使用常用的 C++ 手段为它们配备额外的智能。原始指针与迭代器也是兼容的，意义在于你可以在需要迭代器的地方使用原始指针。也可以说原始指针只是迭代器的一种特定形式。因此，迭代器是一个原始指针可以融入的概念。

如果你想将原始指针与迭代器比较，你首先需要知道 `int carr[10]` C 数组起始部分的对应物。对于原始指针，这很简单：

`carr` 被隐式转换为 `int*` 并作为起始。对于标准容器，你通过 `begin()` 方法或 `begin(container)` 自由函数获取起始。既然有起始，在这种情况下也有一个结尾：你通过 `end()` 方法或 `end(container)` 获取它。这适用于所有标准容器，从 `list` 到 `vector` 再到 `unordered_map` 等。

```cpp
// https://godbolt.org/z/4ngz4ed4W
#include <vector>
#include <iostream> // cut

std::vector;
int main() {
    vector<int> data={5,4,3,2,1};
    vector<int>::const_iterator end = data.end();
    for(vector<int>::const_iterator it = data.begin(); it!=end; ++it) {
        std::cout << *it << " ";
    }
}
```

（注：原文文本中存在大量重复和 OCR 错误，此处翻译已根据逻辑进行了清理和整合。）
