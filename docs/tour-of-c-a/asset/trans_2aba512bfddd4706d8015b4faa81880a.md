

路径在被使用之前不会对其有效性进行检查。即便是如此，其有效性也取决于运行该程序的系统约定。

自然地，可以使用路径来打开文件。

[点击此处查看代码图片]

```cpp
void use(path p)
{
    ofstream f(p);
    if (!f) error("bad file name: ", p);
    f << "Hello, file";
}
```

除了 `path` 之外，`<filesystem>` 还提供了用于遍历目录和查询所用文件属性的类型：

## 文件系统类型（部分）

| path | 目录路径 |
|---|---|
| filesystem_error | 文件系统异常 |
| directory_entry | 目录条目 |
| directory_iterator | 用于遍历目录 |
| recursive_directory_iterator | 用于遍历目录及其子目录 |

考虑一个简单但并非不实际的示例：

[点击此处查看代码图片]

```cpp
void print_directory(path p) // 打印 p 中所有文件的名称
{
    if (is_directory(p)) {
        cout << p << "\n";
        for (const directory_entry& x : directory_entry(p)) {
            cout << " " << x << "\n";
        }
    }
}
catch (const filesystem_error& ex) {
    cerr << ex.what() << "\n";
}
```

字符串可以隐式转换为 `path`，因此我们可以这样练练 `print_directory`：

[点击此处查看代码图片]

```cpp
void use()
{
    print_directory(""); // 当前目录
    print_directory("..."); // 父目录
    print_directory("/"); // Unix 根目录
    print_directory("c:"); // Windows C 卷
    for (string s; cin>>s);
    print_directory(s);
}
```

如果我想列出子目录，我会使用 `recursive_directory_iterator(p)`。如果我想按字典顺序打印条目，我将把路径复制到 `vector` 中并在打印之前进行排序。`path` 类提供了许多常用且实用的操作：

| 路径操作（部分） | p 和 p2 |
|---|---|
| value_type | 用于文件系统的原生编码：POSIX 上为 `char`，Windows 上为 `wchar_t` |
| string_type | `basic_string<value_type>` |
| const_iterator | `const_iterator` 的别名 |
| iterator | p=p2 : 将 p2 赋值给 p |
| /=p2 | p 和 p2 使用文件名分隔符（默认认为 `/`）拼接 |
| p+=p2 | p 和 p2 拼接（无分隔符） |
| s=p.native() | p 的原生格式的引用 |
| s=p.string() | 原生格式的字符串 |
| s=p.generic_string(p) | 通用格式的字符串 |
| p2=filename() | p 的文件名 |
| p2=extension() | p 的扩展名部分 |
| i=begin() | p 元素序列的起始迭代器 |
| i=end() | p 元素序列的结束迭代器 |
| p2=p1, p1=p2 | p 和 p2 的相等与不相等判断 |
| p2<p1, p1<p2>p1 | 字典序比较
| p2=p2 | 到/从 p 的流 I/O |
| iss>>p, os<<p | |
| upath(s) | 来自 UTF-8 源 s 的路径 |

```cpp
if (is_directory(p)) {
    cout << f.stem() << " 是一个 Windows 可执行文件\n";
} else {
    string n = f.extension().string();
    if (n == ".cpp" || n == ".cc") {
        cout << f.stem() << " 是一个 C++ 文件\n";
    }
}
```

