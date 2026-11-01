
> 信息隐藏意味着某种封装正在发生，但封装并不意味着信息隐藏正在发生。

C++ 的一些封装机制支持信息隐藏。类为我们提供了访问级别。私有实现中的成员对结构体的客户端是隐藏的。这就是我们减轻客户端强制执行类不变量负担的方式：通过隐藏实现，从而防止客户端破坏它们。枚举不提供信息隐藏：没有办法只暴露枚举的某些成员。函数完美地隐藏信息，仅通过暴露标识符和返回类型，同时隐藏实现。命名空间可以通过分布在多个文件上来暴露声明并隐藏定义。头文件和源文件也做同样的事情，模块也是如此。

考虑手头的问题。封装将如何帮助我们？我们有很多很多选项都在单个函数中处理。也许我们可以为每个选项提供一个不同的函数。然后我们在检查键的 if 语句中调用正确的函数。该函数可以根据参数数据是否有效返回一个 bool。

看起来不错：我们已将所有不同的选项封装在其各自的函数中，并且可以轻松地为新选项添加更多函数；我们只需为每个选项扩展解析函数即可。我们甚至可以捕获返回值来验证选项文件。我们仍然需要创建一个对象来在所有选项都有效时应用它们，因此在添加新选项时需要更新它，但这很容易记录，而且无论如何，其他工程师在查看这些选项函数的其他示例时也会理解这种模式。

嗯...

你的蜘蛛感应应该在这些可能出错的地方启动。你仍然依赖其他工程师在添加新选项时做正确的事情。他们可能会误解验证过程的性质，或忘记在 if 语句中检查函数，或拼错选项文本。你已经大大改善了情况，但有时封装和信息隐藏是不够的。为了解决这些剩余问题，我们不得不祭出大招：抽象。

## 语言的目的与抽象的本质

抽象是一个棘手的词。问题在于抽象的结果是一个抽象，就像封装的结果是封装一样，这并没有帮助。让我们以同样的方式来考虑抽象的过程，就像我们刚才考虑封装和信息隐藏的过程一样。

从字面上讲，抽象意味着抽离。在编程上下文中，它意味着识别并分离问题的关键部分，将其抽离，并丢弃其余部分。我们将它们与实现细节分离。我们用标识符为抽象命名。再次考虑函数的本质：我们将一组指令打包成一个单一实体并为其命名。函数是一个具有对问题域有意义的名称的抽象。类也是如此：类是一个具有对问题域有意义的名称的抽象，包含相关的功能来模拟名称所暗示的行为。

然而，抽象的艺术在于决定什么应该在抽象的范围内，什么应该在范围之外。这就是它与单纯封装不同的地方。另外，我们谨慎地使用“艺术”这个词：没有机械方法来决定抽象的相关内容与不相关内容的界限。这种能力来自实践和经验。

回到我们的问题，我们正试图解析一个键值对文件，并在它们有效时将结果应用到环境中。该函数命名得很好：`parse_options_file`。我们的问题是如何安全地添加任意键值对。完整的键值对集合的身份对 `parse_options_file` 实际上相关吗？它在范围内吗？我们可以将选项与函数分离吗？

目前我们只是从文件中提取键，并在不断增长的 if-else 语句中检查每个键，因为我们无法对字符串进行 switch-case。这听起来像是一个关联容器。事实上，键与函数指针的映射在这里听起来很完美。突然间，我们的函数失去了大量重复，被一次对映射的查询和相应的函数调用所取代。

我们可以添加一个验证函数并执行验证阶段，然后是提交阶段。一切似乎都在逐渐成形。

```cpp
auto options_table = std::map<std::string,
command*> {};

class command {
public:
    command(std::string const& id) {
        options_table.emplace(id, this);}
    virtual bool validate(std::string const&) = 0;
    virtual void commit(std::string const&) = 0;
};

class debug_cmd : public command {
public:
    debug_cmd() : command("debug"s) {}
    bool validate(std::string const& s) override;
    void commit(std::string const& s) override;
};
debug_cmd debug_cmd_instance;

class language_cmd : public command {
public:
    language_cmd() : command("language"s) {}
    bool validate(std::string const& s) override;
    void commit(std::string const& s) override;
};
language_cmd language_cmd_instance;
```

接下来呢？虽然我们正在解析选项文件，但我们只是在读取一系列字符。它们不必来自文件：它们可以来自命令行本身。我们应该重命名函数为 `parse_options` 并将输入参数更改为 `std::istream`。如果找不到键，它可以被视为文件名并尝试打开文件。然后我们可以简单地递归。

```cpp
void parse_options(std::istream& options) {
    while (options.good()) {
        auto key = std::string{};
        auto value = std::string{};
        options >> key >> value;
        auto fn = options_table.find(key);
        if (fn != options_table.end()) {
            if ((*(fn->second)).validate(value)) {
                (*(fn->second)).commit(value);
            }
        } else {
            auto file = std::ifstream(key);
            parse_options(file);
        }
    }
}
```

现在我们为每个键提供了单独的函数对象，我们就不再局限于初始化数据。我们可以将每个键视为一个命令，突然间，我们就拥有了一个基本的脚本功能。而在本章开始时，工程师必须以无界的方式扩展一个函数，现在他们所要做的只是从 `command` 派生一个新类并重写 `validate` 和 `commit`。

我们现在已从单个、可能庞大的解析函数转移到一个小而有界的函数和一个解析对象字典。我们还以极小的成本额外获得了命令行解析。这一切都是通过考虑什么与问题的哪个部分相关而实现的。原本杂乱无章的结构现在变成了一个干净且易于维护的脚本设施，并附带额外功能。每个人都受益。

## 抽象层次

从单个解析函数转向更小的功能集合的另一种方式可能是将相关活动分组到单独的函数中，像这样：

```cpp
void parse_options_file(const char* filename)
{
    auto options = std::ifstream(filename);
    if (!options.good()) return;
    while (!options.eof())
    {
        auto key = std::string{};
        auto value = std::string{};
        options >> key >> value;
        parse_debug_options(key, value);
        parse_UI_options(key, value);
        parse_logging_options(key, value);
        // and so on...
    }
}
```

这确实解决了封装杂乱结构的问题：你现在有几个函数，每个都按类别标记。然而，这只是将问题转移了，而不是改善了情况。未来的维护者必须决定将他们的解析器添加到哪个正确的函数中。当这些函数变得太大时，需要做出决定如何进一步划分它们。这种方法不尊重抽象层次。
