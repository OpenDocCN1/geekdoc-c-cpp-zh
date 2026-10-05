

258

然而在实践中，处理 `std::string` 以外的类型往往并不易事。在处理外部接口时，你总是需要确保应用了正确的解释：输出是否期望特定的编码？期望什么种类型的字符串？这是一个非常广泛的领域。请阅读相关系统文档或请同事为你解释你需要的内容。

## 6.1.4 只读：“string_view”

C++17 中新的 `string_view` 是解决方案。`string_view`（以及相应的类似类型）是一个只读对象。只要是只读的，该类就提供了与相同的函数和方法。因此，你可以使用 `begin()`、`end()`、`find()`、`compare()` 或 `==`，检查 `starts_with()` 等更多操作进行迭代——并在算法中使用它们。然而，你可以进行某些修改。例如，你可以从开头和结尾剪掉某些内容。通过 `remove_prefix()` 和 `remove_suffix()`，你可以缩短 `string_view` 前部或部的字符数。`string_view` 需要资源极少——即恰好一个指向现有字符串的指针和它的长度。最重要的是，绝对不需要堆内存。因此，`string_view` 特别适用于函数参数。`string_view` 可以通过自动转换从字符串中轻松生成，这非常有用。

```cpp
// https://godbolt.org/z/7fP
#include <iostream>
#include <string>
#include <string_view>

void middle(std::string_view msg) { // string_view is a good parameter
    auto middle = msg.substr(2, 4); // substr returns
    std::cout << middle << "\n";
}

int main() {
    using namespace std::literals;
    const std::string aaa = "Some text";
    middle(aaa); // conversion to string_view
    auto bbb = "More text"sv; // string_view as literal
    middle(bbb);
}
```

**列表 6.2** 可以从字符串字符串轻松地创建 `string_view`。编译器会自动将名为 `aaa` 的字符串转换为 `string_view`。几乎不可能传递一个资源更少的字符串了。正如你从 `msg` 中看到的，`string_view` 也拥有从 `string` 中已知的方法。返回值是一个新的 `string_view`。

值得注意的是，你可以使用后缀 "sv" 直接作为字面量生成 `string_view`。这指向源代码（或编译后程序的静态部分），并且几乎不占用它自己的内存。你有时也可以将 `string_view` 作为返回值。然而，就像指针和引用一样，你必须确保 `string_view` 所基于的原始字符串仍然存在。

## 6.2 流 (Streams)

你已经在示例中多次看到流，但它们的类型很少出现，因为我们使用了标准库中预定义的流：

- 类型为 `std::ostream` 的 `std::cout` 用于标准输出，通常到控制台——即屏幕。你可以将输出重定向到文件。
- 类型为 `std::istream` 的 `std::cin` 用于标准输入，通常来自键盘或重定向的文件。
- `std::cerr` 和 `std::clog` 也是 `std::ostream` own输出流，通常显示在屏幕上，但你可以将它们重定向到与 `std::cout` 分的文件。

对于普通程序流的输入输出，我们通常使用 `std::cin` 和 `std::cout`。每次输出都需要时间，且调用会有开销，因此 `std::cout` 是缓冲的：输出有时不会立即出现，而是先被收集。

`std::cerr` 则不同，它的输出应该立即出现。使用此流进行错误输出。如果 `std::cout` 已被重定向到文件，此输出仍将显示在控制台上，如代码列表 6.3 所示。

```cpp
// https://godbolt.org/z/Pfn5g8z8
// Call this program with 'prog.exe file.txt', for example.
#include <iostream> // cout, cerr
int main() {
    std::cout << "Output to cout\n"; // is output after 'file.txt'
    std::cerr << "Error message!\n"; // still appears on the console
    std::cout << "Normal output\n"; // back into the file

**列表 6.3** 错误流与标准输出分离。

### 6.2.1 输入和输出运算符

正如你经常看到的，你可以使用 `<<` 运算符将数据输出到 `cout`。所有内置类型都可以以这种方式输出。你不需要担心格式——但你可以这样做，正如你稍后通过操纵符看到的。这值得提到，与 C 语言函数 `printf()` 不同，编译器为你选择了正确的格式——即全局运算符 `<<` 的正确重载。你也可以为自己的数据添加重载。

（注：由于原文中存在大量重复段落，此处已根据要求翻译核心内容并保持格式）

