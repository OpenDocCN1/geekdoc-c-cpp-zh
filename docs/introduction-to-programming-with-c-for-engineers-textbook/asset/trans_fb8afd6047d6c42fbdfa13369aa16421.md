
另一方面，如果 `CreateCurExchanger` 未能创建 `XML_CurrencyExchanger` 对象，则返回空的 `all_my_options`，并在第 [91] 行打印错误消息。

在本节中，我们了解了以下内容：

- 使用文件系统路径对象
- 在另一个命名空间内组合命名空间（嵌套命名空间）
- 使用 `std::transform` 将 `std::map` 的元素复制到文件
- 将派生对象传递给定义为接受基类对象的函数时的多态性

## 6.2.6 构建静态库和终端窗口应用程序

我们可以轻松地将 `main` 函数添加到前面的示例中，来创建我们应用程序的终端窗口版本。但既然我们的项目正在不断发展，并且我们计划在各种项目中利用图 3.29 中的 *CurrencyCalc* 组件，那么最好将其与 `main` 函数分离，放入一个独立的*静态库*中。新的软件组件布局如图 6.8 的 UML 组件图所示。

要从应用程序项目构建静态库，我们需要执行以下操作：

- 1. 移除 `main` 函数（即包含 main 的整个文件）。然后它就可以在其他项目中使用，我们将在后面讨论。
- 2. 更改 *CMakeLists.txt* 文件以生成*静态库项目*，<sup>2</sup> 如附录 A.6.1 所述。
- 3. 运行 *CMake.exe*，构建库项目，然后构建库。

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_420_0.png)

**图 6.8** 基本 *CurrencyExchanger* 的 UML 组件图。

这样，我们就能构建出第一个库，名为 *CurrencyCalc_Lib*。新的 *CurrencyCalc_Terminal* 组件与 *CurrencyCalc_Lib* 链接，如图 6.8 所示。它只包含 `main` 函数，如清单 6.7 所示。

2 也可以在不使用 *CMake* 工具的情况下构建库。也就是说，我们可以在编程环境中创建一个新项目，将项目类型选择为静态库，并手动添加文件。不过，*CMake* 让我们能够在不同平台和编程工具之间灵活切换。

| Member | Description |
| --- | --- |
| /- | 路径连接，根据文件系统适当地插入斜杠或反斜杠符号。多个此类符号会被压缩为一个。 |
| / | 连接路径而不添加分隔符（如 string）。 |
| filename | 返回文件名（File.txt）。 |
| stem | 返回主干名（File）。 |
| extension | 返回扩展名（.txt）。 |
| parent_path | 返回父路径。^ |
| relative_path | 返回相对路径。 |
| root_directory | 返回根目录。 |
| root_name | 返回根名称。 |
| root_path | 返回根路径。 |

| Object | Description | Examples |
| path | path 是一个类，表示各种系统中文件、目录及其链接的路径。它类似于容器，支持许多有用的函数来拆分路径和连接各部分。path 类的一些选定成员： | 要使用 C++ 的新文件系统特性，需要包含 filesystem 头文件。fs 是 std::filesystem 的简称，定义如下： 1 #include <filesystem> 2 3 namespace fs = std::filesystem; 第 [6] 行的以下函数将宽字符串 std::wstring 转换为 fs::path 对象。然后，在第 [9-10] 行，路径的每个部分都会打印到屏幕上。 4 void DisplayPathParts( const wstring & inPath_str ) { 5 6 const fs::path inPath( inPath_str ); 7 8 // We can iterate through different parts of a path 9 for( const auto & p : inPath ) 10 wcout << p << "\n"; 11 } 例如，对于输入路径 D:\\Research\\SC++\\Projects\\CCppBookCode\\ReadMe.txt，得到以下输出： D: Research RC Projects CCppBookCode ReadMe.txt |

| Object | Description | Examples |
| --- | --- | --- |
| file_size | 返回文件大小（以字节为单位）。 | \ |
| is_regular_ file | 如果路径表示常规文件（即不是目录也不是链接），则返回 true。 | \ |
| file_status | 返回一个包含文件信息的对象。 | 以下函数打印所给路径（指向目录或文件）的基本信息： \ |
|  |  | void DisplayDirFileInfo( const wstring & inPath_str ) { \ |
|  |  |  const fs::path inPath( inPath_str ); \ |
|  |  |  \ |
|  |  |  wcout << L"exists - \\t\\t" << fs::exists( inPath ) << endl; \ |
|  |  |  \ |
|  |  |  // Let's call all important members of fs::path \ |
|  |  |  wcout << L"filename - \\t\\t" << inPath.filename() << endl; \ |
|  |  |  wcout << L"stem - \\t\\t" << inPath.stem() << endl; \ |
|  |  |  wcout << L"extension - \\t\\t" << inPath.extension() << endl; \ |
|  |  |  \ |
|  |  |  // If a file, then print its size in bytes \ |
|  |  |  if( fs::is_regular_file( inPath ) ) o << val << mp; \ |
|  |  |  std::cout << L"file size - \\t\\t" << fs::file_size( inPath ) << endl; \ |
|  |  |  \ |
|  |  |  wcout << L"parent_path - \\t\\t" << inPath.parent_path() << endl; \ |
|  |  |  wcout << L"relative_path - \\t\\t" << inPath.relative_path() << endl; \ |
|  |  |  \ |
|  |  | } |
| 19 | wcout << L"root_directory - \\t" << inPath.root_directory() << endl; | |
| 20 | wcout << L"root_name - \\t" << inPath.root_name() << endl; | |
| 21 | wcout << L"root_path - \\t" << inPath.root_path() << endl; | |
|    | 要调用第 [14] 行的 file_size，需要先在第 [13] 行用 is_regular_file 检查对象是否为有效文件。在第 [8-10] 行以及 [16-21] 行，调用了 path 的许多成员来获取路径的各部分。对于测试系统中示例输入文件 C:\\Temp\\Readme.txt，得到以下结果： | |
|    | exists - 1
|    | filename - ReadMe.txt
|    | stem - ReadMe
|    | extension - .txt
|    | file_size - 44
|    | parent_path - C:\\Temp
|    | relative_path - Temp\\ReadMe.txt
|    | root_directory - \\
|    | root_name - C:
|    | root_path - C:\\ |

| Object | Description | Examples |
|---|---|---|
| `copy` | 复制文件和/或目录及其内容。 | 以下函数演示了如何创建两个目录 [13, 16]，然后在其中一个目录中创建文件 [19]，将该文件复制到第二个目录 [22]，再将该文件移回第一个目录 [27]，最后删除所有文件和目录 [31]。应非常谨慎地使用最后一个函数。在第 [9] 行，使用了 path 类的重载 `/` 运算符来连接路径中的各元素。 |
| `remove` | 删除文件或目录及其内容。 |  |
| `remove_all` |  |  |
| `create_directory` | 创建一个目录或多个目录。 |  |
| `create_directories` |  |  |
| `rename` | 重命名或移动文件。 |  |

```cpp
void CreateDirsAndFiles(const wstring& subPath, const wstring& subdir)
{
    try
    {
        // There are conventions stating where to put the path
        filesystem::path subPath;
        // Use overloaded operator / to
        // add path to directory
        indirPath /= subdir; // add subdir
        // Create directory
        fs::path sub_2_path{ indirPath / L"subdir_1" };
        fs::create_directory(sub_2_path); // create subdir_1
        fs::path sub_2_path{ indirPath / L"subdir_2" };
        fs::create_directories(sub_2_path); // create subdir_2
        // Create a new file
    }
}
```

```cpp
void CreateDirsAndFiles(const wstring& subPath, const wstring& subdir)
{
    try
    {
        // There are conventions stating where to put the path
        filesystem::path subPath;
        // Use overloaded operator / to add subdirectory
        indirPath /= subdir;
        // Create directory
        fs::path sub_2_path{ indirPath / L"subdir_1" };
        fs::create_directory(sub_2_path);
        fs::path sub_2_path{ indirPath / L"subdir_2" };
        fs::create_directories(sub_2_path);
        // Create a new file
    }
}
```

