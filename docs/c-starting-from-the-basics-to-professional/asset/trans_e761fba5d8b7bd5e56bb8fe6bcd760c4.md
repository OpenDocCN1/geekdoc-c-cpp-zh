

如果 `optional<>` 的 `start_index` 包含一个值，则该函数将返回与 `value()` 相同的结果；如果它不包含值，`value_or()` 会直接计算为你作为参数传入的值。因此，`value_or()` 函数是等效的 if-else 语句或条件运算符表达式的理想替代方案，后者需要先调用 `has_value()` 再调用 `value()`。

> **注意**  Ex9_01 涵盖了关于 `std::optional<>` 的大部分知识。一如既往，如果你需要了解更多，请查阅你最喜欢的标准库参考。不过有一点现在就要指出：除了 `*` 运算符之外，`std::optional<>` 还支持 `->` 运算符。也就是说，在下面的示例中，最后两条语句是等价的：

```
std::optional<string> os{ "Failing in life is inevitable--staying down is optional." };
if (os) std::cout << (*os).size() << std::endl;
if (os) std::cout << os->size() << std::endl;
```

请注意，虽然这种语法让 `optional<>` 对象看起来和用起来都像指针，但它们绝对不是指针。每个 `optional<>` 对象都包含一个分配给它的值的副本，并且这个副本不保存在自由存储区中。也就是说，复制指针不会复制它指向的值，而复制 `optional<>` 总是涉及复制存储在其中的整个值。

## 字符串视图：新的 const 字符串引用

从上一章中，你知道将输入参数按引用传递给 const 而不是按值传递的主要动机是避免不必要的复制。例如，过于频繁地复制较大的字符串，在时间和内存方面都可能会变得相当昂贵。假设你有一个函数不会修改它作为输入接收的字符串。那么此时你的自然本能应该是将相应的参数声明为 `const string&`。例如，我们在 Ex8_08 中的 `find_words()` 就这样做了。

```
void find_words(vector<string>& words, const string& text, const string& separators);
```

然而不幸的是，`const string&` 参数并不完美。虽然它们确实避免了 `std::string` 对象的复制，但它们仍然有缺点。为了说明原因，假设我们稍微修改一下 Ex8_08 的 `main()` 函数，如下所示：

```
int main()
{
    std::string text;        // 要搜索的字符串
    std::cout << "Enter some text terminated by *:\n";
    std::getline(std::cin, text, '*');

    // const std::string separators{ " ,;:.!?\"\n" };
    std::vector<std::string> words;  // 找到的单词

    find_words(words, text, " ,;:.!?\"\n"); /* 不再使用 'separators' 常量！ */
    list_words(words);
}
```

唯一的区别是我们不再将分隔符存储在一个单独的 `separators` 常量中。相反，我们直接将它们作为第三个参数传递给 `find_words()`。你可以很容易地验证这仍然可以编译并正确工作。

那么第一个问题是，为什么这能编译并工作？毕竟，`find_words()` 的第三个参数期望的是一个 `std::string` 对象的引用，而我们现在传递的参数是一个 `const char[]` 类型的字符串字面量——一个字符数组——因此它肯定不是 `std::string` 对象。自然，你会回想起上一章的内容：编译器一定是在应用某种形式的隐式转换。也就是说，函数的引用实际上不会指向字面量，而是指向编译器在内存中某个位置静默创建的临时 `std::string` 对象。（我们将在后面的章节中解释这些转换是如何对非基本类型起作用的。）在这种情况下，临时字符串对象将用字符串字面量中所有字符的副本来初始化。

作为细心的读者，你现在会意识到为什么按引用传递字符串给 const 在某种程度上是有缺陷的。我们使用引用的动机是为了避免复制。但是，由于字符串字面量在传递给 `const std::string&` 参数时仍然会被复制，它们会被复制到由隐式转换产生的临时 `std::string` 对象中。

这就引出了本节第二个也是真正的问题：我们如何创建从不复制输入字符串参数的函数，即使是字符串字面量或其他字符数组也不复制？我们不想为此重新使用 `const char*`。那样的话，我们不仅必须同时传递字符串的长度，以避免总是扫描终止空字符，而且还会错过 `std::string` 提供的所有好用且安全的函数。

答案在于 `std::string_view`，这是 `<string_view>` 模块中定义的一种类型。这种类型的值在行为上类似于 `const std::string` 类型的值——注意是 const！——只有一个区别：创建 `string_view` 永远不会涉及复制任何字符。即使是从字符串字面量创建也是如此。它内部使用的只是字符串长度的副本和一个指向某个外部字符序列的指针。`string_view` 不关心字符本身存储在哪里：在 `std::string` 对象内部、作为字符串字面量、还是作为普通的 C 风格字符串。对于 `string_view` 和使用它的代码来说，这完全没有区别。在某种程度上，`string_view` 抽象掉了你所操作的文本数据的具体类型，使你能够轻松编写一个单一的函数，可以高效且有效地处理此类输入。

因此：

> **提示**  对于输入字符串参数，始终使用类型 `std::string_view` 而不是 `const std::string&`。（虽然使用 `const std::string_view&` 也没有错，但你也可以按值传递 `std::string_view`。因为这不涉及复制整个字符数组，初始化或复制一个 `string_view` 非常廉价。）

由于 string_view 是为字符串字面量而设计的，它们确实有一个重要的限制：底层字符串的字符永远不能通过 string_view 的接口进行修改。`string_views` 天生就是 const 的。即使是非 const 的 string_view 也不允许你更改底层字符串的字符。套用“老板”的话说，你可以看，但不能摸。但这通常已经足够了，如下一节的示例所证明的那样。

> **注意**  除了用于 `char` 元素字符串的 `std::string_view` 之外，当然还存在 `std::wstring_view`、`std::u8string_view`、`std::u16string_view` 和 `std::u32string_view`，用于宽字符或 Unicode 字符字符串的视图。由于它们都是同一个类模板（`std::basic_string_view<CharType>`）的实例化，它们的行为完全类似。

## 使用字符串视图函数参数

为了避免字符串字面量和其他字符序列的不经意复制，Ex8_08 中的 `find_words()` 函数最好声明如下：

```
void find_words(vector<string>& words, string_view text, string_view separators);
```

`std::string_view` 类型在大多数情况下可以替代 `const std::string&` 和 `const std::string` 直接使用。但在我们的示例中并非完全如此。巧合吗？当然不是！我们选择这个示例正是为了解释将 `const std::string&` 替换为 `string_view` 可能会如何出错。为了使 `find_words()` 函数定义使用新的改进签名进行编译，你必须稍微修改它，如下所示（完整程序见 Ex9_02.cpp）：

```
void find_words(vector<string>& words, string_view text, string_view separators)
{
    size_t start{ text.find_first_not_of(separators) };    // 第一个单词的起始索引
    size_t end{};                                          // 单词结束索引

    while (start != string_view::npos)                     // 查找单词
    {
        end = text.find_first_of(separators, start + 1);   // 查找单词结尾
        if (end == string_view::npos)                      // 找到了分隔符吗？
            end = text.length();                           // 没有，则设置为文本末尾

        words.push_back(std::string(text.substr(start, end - start)));  // 存储单词
        start = text.find_first_not_of(separators, end + 1); // 查找下一个单词的首字母
    }
}
```

我们必须修改的是倒数第二条语句，最初它没有包含显式的 `std::string{ ... }` 初始化：

```
words.push_back(text.substr(start, end - start));
```

然而，编译器会拒绝任何将 `std::string_view` 对象隐式转换为 `std::string` 类型的行为（你可以试试！）。这种刻意限制背后的理由是，你通常使用 `string_view` 是为了避免字符串复制操作，而将 `string_view` 转换回 `std::string` 总是涉及复制底层字符数组。为了保护你避免意外这样做，编译器不允许隐式进行这种转换。你总是必须自己显式地添加这种方向的转换。

> **注意**  还有另外两种情况，`string_view` 并不完全等同于 `const string`。首先，`string_view` 不提供 `c_str()` 函数将其转换为 `const char*` 数组。幸运的是，它确实与 `std::string` 共用 `data()` 函数，而在大多数情况下该函数是等效的。其次，`string_views` 不能使用加法运算符（`+`）进行连接。要在连接表达式中使用 `string_view` 值 `my_view`，你必须先将其转换为 `std::string`，例如使用 `std::string{my_view}`。

