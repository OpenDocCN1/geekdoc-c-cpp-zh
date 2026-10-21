

```
using system_clock = std::chrono::system_clock;
return system_clock::to_time_t(tp + (system_clock::now()
    - decltype(tp)::clock::now()));
}
```

技巧在于将文件系统时间点计算为相对于当前时间的持续时间，然后将该差值加到系统时钟的当前时间上。此函数并不精确，因为两个时钟可能具有不同的分辨率，并且我们在略有不同的时间调用了两次 now()。然而，通常情况下，这种方法效果相当不错。

例如，对于路径 p，我们可以调用：

```
auto ftime = std::filesystem::last_write_time(p);
std::time_t t = toTimeT(ftime);
// 转换为日历时间（包括跳过尾随换行符）：
std::string ts = std::ctime(&t);
ts.resize(ts.size()-1);
std::cout << "last access of " << p << ": " << ts << '\n';
```

可能打印：

```
last access of "fileattr.exe": Sun Jun 24 10:41:12 2018
```

要按我们想要的方式格式化字符串，我们可以调用：

```
std::time_t t = toTimeT(ftime);
char mbstr[100];
if (std::strftime(mbstr, sizeof(mbstr), "last access: %B %d, %Y at %H:%M\n",
    std::localtime(&t))) {
    std::cout << mbstr;
}
```

可能输出：

```
last access: June 24, 2018 at 10:41
```

一个将任意文件系统时间点转换为字符串的有用辅助函数是：

filesystem/ftimeAsString.hpp

```
#include <string>
#include <chrono>
#include <filesystem>

std::string asString(const std::filesystem::file_time_type& tp)
{
    using system_clock = std::chrono::system_clock;
    auto t = system_clock::to_time_t(tp + (system_clock::now()
        - decltype(tp)::clock::now()));

    // 转换为日历时间（包括跳过尾随换行符）：
    std::string ts = std::ctime(&t);
    ts.resize(ts.size()-1);
    
return ts;
}
```

请注意 ctime() 和 strftime() 不是线程安全的，不能并发调用。

参见“修改现有文件”部分，了解修改最后写入访问的相应 API。

## 20.4.2 文件状态

为了避免文件系统访问，有一种特殊类型 file_status 可以用来保存和修改缓存的文件类型和权限。此状态可以设置

- 当按文件状态操作表所列的方式请求特定路径的文件状态时
- 当遍历目录时

| 调用 | 效果 |
|---|---|
| status(p) | 返回文件 p 的 file_status（会跟随符号链接） |
| symlink_status(p) | 返回 p 的 file_status（不会跟随符号链接） |

表 20.12. 文件状态操作

区别在于，如果路径 p 解析为符号链接，status() 会跟随链接并打印该处文件的属性（状态可能为无文件），而 symlink_status(p) 打印符号链接本身的状态。

表 file_status 操作列出了 file_status 对象 fs 的可能调用。

| 调用 | 效果 |
|---|---|
| exists(fs) | 返回文件是否存在 |
| is_regular_file(fs) | 返回文件是否存在且为普通文件 |
| is_directory(fs) | 返回文件是否存在且为目录 |
| is_symlink(fs) | 返回文件是否存在且为符号链接 |
| is_other(fs) | 返回文件是否存在且既不是普通文件也不是目录也不是符号链接 |
| is_block_file(fs) | 返回文件是否存在且为块特殊文件 |
| is_character_file(fs) | 返回文件是否存在且为字符特殊文件 |
| is_fifo(fs) | 返回文件是否存在且为 FIFO 或管道文件 |
| is_socket(fs) | 返回文件是否存在且为套接字 |
| fs.type() | 返回文件的 file_type |
| fs.permissions() | 返回文件的权限 |

表 20.13. file_status 操作

文件状态操作的一个好处是，你可以为同一文件节省多次操作系统调用。

例如，而不是

```
if (!is_directory(path)) {
```

```
if (is_character_file(path) || is_block_file(path)) {
    ...
}
...
}
```

你最好实现以下方式：

```
auto pathStatus{status(path)};
if (!is_directory(pathStatus)) {
    if (is_character_file(pathStatus) || is_block_file(pathStatus)) {
        ...
    }
    ...
}
```

另一个关键好处是，通过使用 symlink_status()，你可以检查路径的状态而不跟随任何符号链接。这有助于例如，如果你想检查特定路径是否存在任何文件。

由于文件状态不使用操作系统，因此不提供返回错误代码的重载。

用于路径参数的 exists() 和 is_...() 函数是调用并检查 file_status 的 type() 的快捷方式。例如，

```
is_regular_file(mypath)
```

是

```
is_regular_file(status(mypath))
```

的快捷方式，

```
status(mypath).type() == file_type::regular
```

的快捷方式。

## 20.4.3 权限

处理文件权限的模型采用自 UNIX/POSIX 世界的方式。有位表示文件所有者、同组成员或所有其他人对文件的读、写和/或执行/搜索访问权限。此外，还有“执行时设置用户 ID”、“执行时设置组 ID”和粘滞位（或另一个系统相关含义）的特殊位。

表 Permission Bits 列出了位掩码作用域枚举类型 perms 的值，定义在命名空间 std::filesystem 中，表示一个或多个权限位。

你可以请求当前权限并作为结果检查返回的 perms 对象的位。要组合标志，你必须使用位运算符。例如：

```
// 如果可写：
if ((fileStatus.permissions()
    & (fs::perms::owner_write | fs::perms::group_write
    | fs::perms::others_write))
    != fs::perms::none) {
```

| 枚举 | 八进制 | POSIX | 含义 |
|---|---|---|---|
| none | 0 |  | 未设置权限 |
| owner_read | 0400 | S_IRUSR | 所有者的读权限 |
| owner_write | 0200 | S_IWUSR | 所有者的写权限 |
| owner_exec | 0100 | S_IXUSR | 所有者的执行/搜索权限 |
| owner_all | 0700 | S_IRWXU | 所有者的所有权限 |
| group_read | 040 | S_IRGRP | 组的读权限 |
| group_write | 020 | S_IWGRP | 组的写权限 |
| group_exec | 010 | S_IXGRP | 组的执行/搜索权限 |
| group_all | 070 | S_IRWXG | 组的所有权限 |
| others_read | 04 | S_IROTH | 所有其他人的读权限 |
| others_write | 02 | S_IWOTH | 所有其他人的写权限 |
| others_exec | 01 | S_IXOTH | 所有其他人的执行/搜索权限 |
| others_all | 07 | S_IRWXO | 所有其他人的所有权限 |
| all | 0777 |  | 所有人的所有权限 |
| set_uid | 04000 | S_ISUID | 执行时设置用户 ID |
| set_gid | 02000 | S_ISGID | 执行时设置组 ID |
| sticky_bit | 01000 | S_ISVTX | 操作系统相关 |
| mask | 07777 |  | 所有可能位的掩码 |
| unknown | 0xFFFF |  | 权限未知 |

表 20.14. 权限位

} ...

一种更简短（但可能可读性较差）的方式来初始化位掩码是使用相应的八进制值并直接使用宽松的枚举初始化：

```
// 如果可写：
if ((fileStatus.permissions() & fs::perms{0222}) != fs::perms::none) {
  ...
}
```

请注意，你必须在将结果与特定值进行比较之前对 & 表达式加上括号。请注意，你也不能跳过比较，因为位掩码作用域枚举类型没有隐式转换为 bool。

作为另一个示例，要将文件的权限转换为与 UNIX 命令 ls -l 相同的表示法的字符串，你可以使用以下辅助函数：

filesystem/permaAsString.hpp

```
#include <string>
#include <chrono>
#include <filesystem>

std::string asString(const std::filesystem::perms& pm)
{
    using perms = std::filesystem::perms;
    std::string s;
    s.resize(9);
    s[0] = (pm & perms::owner_read) != perms::none ? 'r' : '-';
    s[1] = (pm & perms::owner_write) != perms::none ? 'w' : '-';
    s[2] = (pm & perms::owner_exec) != perms::none ? 'x' : '-';
    s[3] = (pm & perms::group_read) != perms::none ? 'r' : '-';
    s[4] = (pm & perms::group_write) != perms::none ? 'w' : '-';
    s[5] = (pm & perms::group_exec) != perms::none ? 'x' : '-';
    s[6] = (pm & perms::others_read) != perms::none ? 'r' : '-';
    s[7] = (pm & perms::others_write) != perms::none ? 'w' : '-';
    s[8] = (pm & perms::others_exec) != perms::none ? 'x' : '-';
    return s;
}
```

这允许你作为标准 ostream 命令的一部分打印文件的权限：

```
std::cout << "permissions: " << asString(status(mypath).permissions())
            << '\n';
```

对于一个对所有者具有所有权限、对所有其他人具有读/执行权限的文件，可能的输出为：

```
permissions: rwxr-xr-x
```

然而，请注意，Windows ACL（访问控制列表）方法并不真正适合这种方案。因此，使用 Visual C++ 时，可写文件始终具有所有读、写和执行位设置（即使它们不是可执行文件），并且具有只读标志的文件始终具有所有读和可执行位设置。这也影响了可移植地修改权限时的 API。

## 20.4.4 文件系统修改

你也可以通过创建和删除文件或修改现有文件来修改文件系统。

### 创建和删除文件

表 Creating and Deleting Files 列出了用于创建和删除文件的路径 p 的操作。

没有用于创建普通文件的函数。这由 I/O 流标准库覆盖。例如，以下语句创建新的空文件（如果尚未存在）：

```
std::ofstream{"log.txt"};
```

