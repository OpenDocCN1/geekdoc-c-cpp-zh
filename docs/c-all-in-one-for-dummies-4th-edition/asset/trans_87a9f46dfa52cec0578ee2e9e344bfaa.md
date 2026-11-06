
### 本章内容

- 创建和删除目录
- 获取目录内容
- 复制和移动，以及它们为何相关
- 移动和重命名文件，以及它们为何相似

## 第4章：构建目录和内容

C++17 之前的原生 C++ 版本没有提供用于创建目录和获取目录内容的函数。（C++17 及更高版本提供了对 `filesystem` 库的访问，但大多数编译器尚未实现它。）关于这种情况，你需要知道两点：

- 这种缺失确实有充分理由。C++ 是一门通用语言。处理目录的问题因操作系统而异。因此，在 C++ 中包含此类特性没有意义。
- 一些勇敢的“反叛者”添加了一些函数——这些函数存在于大多数 C++ 实现中。这些新增功能很重要；否则，你就得调用操作系统来创建或修改目录。

C++ 从 C 编程语言沿袭了头文件 `stdio.h`，其中包含用于重命名和删除文件及目录的函数。此外，它还支持一个用于创建临时文件的函数。

![](img/128ab511de4e7360e167e3b15cdd5dd0_746_0.png)

本章向你介绍操作目录和文件的方法。（我只在 `Code::Blocks` 产品自带的 GNU GCC 编译器上测试了这些例程，该产品适用于 OS X、Linux 和 Windows。如果你使用其他编译器或操作系统，可以试试这些示例。它们很可能也能正常工作。）

![](img/128ab511de4e7360e167e3b15cdd5dd0_747_0.png)

对于本章的示例，你需要在源代码文件开头同时添加 `#include <stdio.h>` 和 `#include <io.h>`。（请不要把这个文件与 `ios.h` 混淆。现在要用的不是那个文件。）如果你使用的编译器不是 Code::Blocks，不能保证在包含目录中找到 `io.h`，但你应该找一找。

![](img/128ab511de4e7360e167e3b15cdd5dd0_747_1.png)

你不必手动输入本章的源代码。事实上，使用可下载的源代码会容易得多。你可以在可下载源代码的 `\CPP_AIO4\BookVI\Chapter04` 文件夹中找到本章的源代码。有关如何找到这些源文件的详细信息，请参阅引言。

### 操作目录

你可以使用几个函数来创建和删除目录。这些函数位于 `io.h` 头文件中。

#### 创建目录

如果要创建目录，可以调用 `mkdir()` 函数。如果该函数能为你创建目录，则返回 0。否则，返回非零值，例如 1。下面是一些使用该函数的示例代码（见 `MakeDirectory` 示例）：

```cpp
#include <iostream>
#include <stdio.h>
#include <io.h>

using namespace std;

int main() {
  if (mkdir("./abc") != 0)
    cout << "Directory not created." << endl;
  else
    cout << "Directory created." << endl;

  return 0;
}
```

### 使用文件系统库

如今大多数编译器都不支持文件系统库，即使你安装了 C++17 或更高版本。不过，Wandbox（https://wandbox.org/）确实对文件系统库提供了有限支持，因此你可以使用 https://en.cppreference.com/w/cpp/filesystem 上的文档开始试用它。filesystem::path（https://en.cppreference.com/w/cpp/filesystem/path）支持对于让该库正常工作至关重要。在 Wandbox 上操作的问题在于，你无法访问实际的目录。因此，你最终会尝试类似下面这样的代码（见 FileSystem 示例）：

```cpp
#include <iostream>
#include <filesystem>

using namespace std;
namespace fs = std::filesystem;

int main() {
    fs::path APath(".");
    cout << "Exists: " << fs::exists(APath) << endl
         << "Root Name: " << APath.root_name() << endl
         << "Root Path: " << APath.root_path() << endl
         << "Relative Path: " << APath.relative_path() << endl;
    return 0;
}
```

请注意，这段代码通过创建一个命名空间变量 fs 来访问文件系统库，从而简化了信息的输入。代码首先创建一个路径（该示例使用当前路径以避免出现问题）。然后，它开始查询该路径的信息，例如该路径是否存在以及相对路径。遗憾的是，输出有点令人失望（但至少当前路径是存在的）：

```
Exists: 1
Root Name: ""
Root Path: ""
Relative Path: "."
```

为了兼容性，本示例在调用 `mkdir()` 时使用了正斜杠（/）。在 Windows 中，你可以使用正斜杠或反斜杠。第一次运行这个示例后，你应该会看到系统上的 /CPP_AIO4/BookVI/Chapter04 目录中新增了一个名为 abc 的目录。如果第二次运行该示例，你会收到“目录未创建。”消息，因为该目录已经存在。

![](img/128ab511de4e7360e167e3b15cdd5dd0_749_0.png)

如果能够一下子创建整个目录树结构，那会很好——比如调用 `mkdir("/abc/def/ghi/jkl")`，而无需事先存在任何 `abc`、`def` 或 `ghi` 目录——但是，在尝试创建子目录之前，每个父目录都必须存在。除非 `/abc/def/ghi` 目录存在，否则该函数不会创建 `jkl` 目录。这意味着你必须把这个调用拆成多个调用：首先创建 `/abc`。然后创建 `/abc/def`，依此类推。

![](img/128ab511de4e7360e167e3b15cdd5dd0_749_1.png)

如果你确实想同时创建所有目录，可以使用 `system()` 函数，如本章后面“使用快速而粗糙的方法”一节所述。如果执行 `system("mkdir \\abc\\def\\ghi\\jkl")`，就可以一下子创建该目录。

#### 删除目录

要删除目录，可以调用 `rmdir()` 函数，并传入目录名。如果想判断操作是否成功，可以将它的返回值与 0 进行比较。下面是一些示例代码（见 DeleteDirectory 示例）：

```cpp
#include <iostream>
#include <stdio.h>
#include <io.h>

using namespace std;

int main() {
  if (rmdir("./abc") != 0)
    cout << "Directory not deleted." << endl;
  else
    cout << "Directory deleted." << endl;

  return 0;
}
```

运行这个示例后，你在上一节创建的 `/CPP_AIO4/BookVI/Chapter04/abc` 目录就会消失。请务必验证该目录是否按预期添加和删除。如果第二次运行这个示例，你会看到“目录未删除。”消息，因为无法删除不存在的目录。

![](img/128ab511de4e7360e167e3b15cdd5dd0_749_2.png)

这种方法仅在目录为空时有效。如果目录中至少有一个文件或目录，该函数就无法删除该目录——并会返回非零结果。

### 清单 4-1：*（续）*

```cpp
string Chop(string &str) {
    string res = str;

    int len = str.length();
    if (str[len - 1] == '\r')
        res.replace(len - 1, 1, "");

    len = str.length();
    if (str[len - 1] == '\n')
        res.replace(len - 1, 1, "");

    return res;
}

void DumpEntry(_finddata_t &data) {
    string createtime(ctime(&data.time_create));
    cout << Chop(createtime) << "\t";
    cout << data.size << "\t";

    if ((data.attrib & _A_SUBDIR) == _A_SUBDIR)
        cout << "[" << data.name << "]" << endl;
    else
        cout << data.name << endl;
}

int main() {
    _finddata_t data;
    int ff = _findfirst("../*.*", &data);

    if (ff != -1) {
        int res = 0;

        while (res != -1) {
            DumpEntry(data);
            res = _findnext(ff, &data);
        }

        _findclose(ff);
    }
    return 0;
}
```

