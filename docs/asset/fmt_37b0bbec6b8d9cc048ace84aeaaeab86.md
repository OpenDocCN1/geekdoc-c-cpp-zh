
在这里我们使用 `getline` 从标准输入读取整条记录。如果 `getline` 调用成功，`line` 就会包含来自输入文件的一条记录。在 `while` 循环内部，我们定义了一个局部的 `PersonInfo` 对象来存储当前记录的数据。

接下来，我们将一个 `istream` 绑定到我们刚刚读取的行上。现在我们就可以对 `istream` 使用输入运算符来读取当前记录中的每个元素。我们首先读取名称，然后通过一个 `while` 循环读取该人的电话号码。

当读完 `line` 中的所有数据时，内部的 `while` 循环结束。这个循环的工作原理与我们为 `cin` 编写的其他类似。区别在于这个循环是从字符串而不是标准输入读取数据的。当字符串被完全读取后，会发出“文件结束”信号，对 `record` 的下一次输入操作将失败。

我们通过将刚刚处理的 `PersonInfo` 添加到 `vector` 中来结束 `while` 循环。外层循环持续运行，直到在 `cin` 上遇到文件结束。

### 练习题 8.3.1 节
- **练习 8.9:** 使用你在 § 8.12 (第 314 页) 的第一个练习中编写的函数来打印 `istream` 对象的的内容。
- **练习 8.10:** 编写一个程序，将文件的每一行存储在 `vector<string>` 中。现在使用 `istream` 每次一个单词地从 `vector` 中读取每个元素。
- **练习 8.11:** 本节中的程序在外层 `while` 循环内部定义了它的 `istream` 对象。如果 `record` 定义在那个循环之外，你需要做哪些更改？重写程序，将 `record` 的定义移动 `while` 之外，并看看你是否想所有所有的更改。
- **练习 8.12:** 为什么我们没有在 `PersonInfo` 中使用类内初始化？

### 8.3.2. 使用 ostreams

当我们我们需要构建输出但不想稍后才打印输出时，`ostringstream` 非常有用。例如，我们可能想对上一个示例中读取的数字进行验证和重新格式化。如果所有数字都是有效的，我们就打印一个包含重新格式化数字的新文件。如果某人有任何无效数字，我们不会将他们放入新文件中。相反，我们将写入包含该人姓名及其无效数字列表的错误信息。

由于我们不想包含任何无效数字的人的数据，因此在看到并验证他们所有的数字之前，我们无法输出。然而，我们可以将输出“写入”到内存中的 `ostringstream`：

点击此处查看代码图片

```cpp
for (const auto &entry : people) { // for each entry in people

    ostringstream formatted, badNums; // 每次循环都创建的对象

    for (const auto &nums : entry.phones) { // for each number

        if (!valid(nums))

            badNums << " " << nums; // badNums 中的字符串

        } else // "写入"到 formatted 的字符串中

            formatted << " " << format(nums);

        }

    }

    if (badNums.empty()) { // 没有坏数字

        os << entry.name << " " << // 打印姓名

            << formatted.str() << endl; // 和重新格式化的数字

    } else

        cerr << "input error: " << entry.name << // 否则打印姓名和坏数字

            << " invalid number(s) " << badNums.str() <<

            endl;

}
```
