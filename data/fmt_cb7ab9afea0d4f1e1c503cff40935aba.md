
文件系统命名空间非常详尽：它包含超过 10 个类和 30 多个函数。可以使用标识符的全限定名（例如 `std::filesystem::path`）。或者，在指定了 `using namespace std::filesystem;` 后，可以在无需进一步限定的情况下使用标识符。还会遇到 `namespace fs = std::filesystem` 的命名空间指定，允许使用 `fs::path` 等指定。文件系统命名空间中的函数可能会失败。当函数无法执行任务时，它们可能会抛出异常（第 10 章），可能会为作为参数传递给函数的 `error_code` 对象赋值（见 4.3.2）。

### 4.3.1 ‘file_clock’ 类型

在 4.2.3 中提到可以使用各种预定义的时钟，其中 `system_clock` 使用不同的时钟：`std::filesystem::file_clock`。使用 `file_clock` 的点与使用系统时钟获取的时间点不同：使用 `file_clock` 的时间点基于一个（目前）纪元远早于 1970 年 1 月 1 日 00:00:00 至 1969 年 12 月 31 日 23:59:59 的纪元。这两个纪元可以在以现在为基准的尺度上定位如下：

| system_clock 的纪元 | file_clock 的纪元 |
| :--- | :--- |
| 现在 |  |

`file_clock` 具有其特殊性：静态成员是可用的，`system_clock` 成员也是可用的。由于 `time_t` 可用，`file_clock` 转换为 `system_clock`。`system_clock` 成员用于 `file_clock`。¹http://www.boost.org/doc/1_6/filesystem/index.html

文件系统命名空间中的函数可能会失败。当函数无法执行其任务时，它们可能会抛出异常（第 10 章），可能会为作为参数传递给函数的 `error_code` 对象赋值（见 4.3.2）。

### 4.3.2 'error_code' 类

`std::error_code` 类（注意：不是 `std::filesystem::error_code`!）封装了错误值以及相关的错误类别（见第 10 章。`error_code` 在包含 `<system_error>` 头文件后可用，但在 `<system_error>` 文件也可用）。传统上，错误值是赋值给全局 `int` 变量的值。转换时，错误值为零表示没有错误。这一约定被 `error_code` 采用。

可以为许多概念不同的情况定义错误代码。情况由它们的错误类别描述。

错误类别用于将 `error_code` 对象与定义的对象关联。默认可用的错误类别可以使用 `EADDRINUSE`（相应的枚举类 `err_address_in_use`），但也可以为其他上下文定义新类型的错误类别。定义错误类别位于 C++ 注释的末尾（第 23.7.1 节）。在此处引入了两个 `error_category` 成员：

```
std::string message(int err) 返回错误 err 的文本描述（当 err 为 address_in_use 时返回 address already use）。
```

- `char const <name>` 返回错误类别的名称（例如通用类别返回 generic）；

错误类别是单例类；每个类别仅存在一个对象。在文件系统命名空间的上下文中使用了标准的 `system_category`，自由函数 `std::system_category` 返回 `system_category` 对象的引用。

## 4.3. std::filesystem 命名空间

不需要参数。`error_code` 类的公共接口声明了这些构造函数和成员：

### 构造函数：

- `error_code() noexcept`:

对象初始化为错误值 0 和 `system_category` 错误类别。值 0 不被视为错误；

- 拷贝-移动构造函数；

- `error_code(int ec, error_category const &ec) noexcept`:

对象从错误值 `ec`（参见 `errno`，由失败的函数设置）和适用 `error_category` 的常量引用初始化（例如由 `std::system_category()` 或 `std::generic_enum` 提供）。以下是一个定义 `error_code` 对象的示例：

```cpp
error_code ec(5, system_category());
```

- `error_code(ErrorCode enum) noexcept`:

这是一个成员（22.1.3），使用模板头模板 `<class ErrorCode>`。使用 `make_error_code(value)` 的返回值初始化对象（见下文）。第 23.7 节涵盖了定义 `ErrorCodeEnum` 的内容。注意：`ErrorCodeEnum` 不存在。它是现有 `ErrorCode` 举型的占位符；

### 成员：

- 可用接受 `ErrorCodeEnum` 的重载运算符和赋值运算符；

- `void assign(int val, error_category const &)` :为对象的错误值和类别分配新值。例如，`ec.assign(0, generic_category());`

- `error_category category() const noexcept`:

返回对象错误类别的引用；

- `void clear() noexcept`:

将 `error_code` 的值设置为 0，将其类别设置为 `system_category`；

- `error_condition default_error_condition() const noexcept`:

返回当前对象的默认错误条件，该条件使用当前对象的错误值和类别初始化（见 10.9.2 关于 `error_condition` 类的详情）；

- `string message() const`:

返回与当前对象错误值关联的消息（等于 `category().ec.value()`）；

- `explicit operator bool() const noexcept`:

如果对象的错误值不等于 0（即它表示一个错误），则返回 true；

- `int value() const noexcept`:

返回对象的错误值。

### 函数：

- `error_code` 对象可以进行（不）相等比较，并可以通过 `operator<` 进行排序。

## 第 4 章 命名空间

与不同错误类别相关的 `error_codes` 排序没有意义。当错误类别相同时，通过它们的错误值进行比较（参见 SG14 讨论总结²）；

- `error_code make_error_code(errc value) noexcept`:返回一个由 `static_cast<int>(value)` 和 `generic_category()` 化的 `error_code`。此函数将枚举 `errc` 值转换为 `error_code`。

也可以定义其他相关的错误，并与定制的 `make_error_code` 函数关联（参见第 23.7 节）；

- `std::ostream &operator<<(std::ostream &os, error_code const &ec)`:执行以下操作：

```cpp
return os << ec.category().name() << ':' << ec.value();
```

引入几个函数定义了一个可选的 `last_error &ec` 参数。如果这些函数没有完成任务，则 `ec` 被设置为相应的错误代码；如果没有遇到错误参数，则调用 `ec.clear()`。如果没有提供 `ec` 参数，则这些函数在无法完成任务时抛出 `filesystem_error` 异常。

### 4.3.3 文件系统条目的名称：path

`filesystem::path` 类的对象持有文件条目的名称。`path` 类是一个值类：提供了默认构造函数（空路径）以及标准的拷贝/移动构造/赋值实用程序。此外，还可以构造以下内容：

- `path(string&);`

- `path(Type const &source)`:

任何提供路径字符的适用类型（例如，`source` 是一个 NTBS）；

- `path(InputIterator begin, InputIterator end)` 定义路径名称。

构造的路径不必引用现有的文件系统。路径构造函数期望字符序列（包括 NTBS），这些序列可能由各种（均为可选）元素组成：

- 根名称（root-name），例如磁盘名称（如 E:）或设备指示器（如 //nfs）；

- 根目录（root-directory），如果它是（可选的）根名称后的第一个字符则存在；

- 文件名（filename）（不包含目录分隔符）。在“单点文件名”中，`..` 表示当前目录；在“双点文件名”中，`..` 表示当前目录的父目录；

- 目录分隔符（默认使用斜杠）。多个连续的分隔符合并为一个分隔符。

² http://www.open-std.org/jstl/sc22/wg21/docs/papers/2018/p0824r1.html

## 4.3. STD::FILESYSTEM 命名空间

构造函数还定义了一个最后的格式 `ftmp = auto_format` 参数，实践中几乎不需要提供该参数（详情见 cppreference.）。

许多函数期望 `path` 参数，这些参数可以通过 NTBS 或 `std::string` 对象创建，`path` 允许提升（参见第 11.5 节）。例如，文件系统函数 `absolute` 需要一个 `const &` 参数。可以这样调用：`absolute("tmp/filename");`

### 4.3.3 访问器和运算符

`path` 类修改以下内容：

运算符：

- `path &=(Type const &);`

## 4.3. STD::FILESYSTEM 命名空间

### 4.3.3.2 自由函数

除了 `path` 成员函数外，还有许多自由函数可用。其中包含拷贝函数。这些函数接受一个可选的 `std::filesystem::copy_options` 参数。枚举类 `copy_options` 定义了可以用于细调这些函数行为的常量。该枚举支持位运算符（“符号”值显示在括号中），并定义了这些符号：

- 当复制文件时：

  - `none (0)`：报告错误（默认行为）；

  - `skip_existing (1)`：保留现有文件，不报告错误；

  - `overwrite_existing (2)`：替换现有文件；

  - `update_existing (4)`：仅当现有文件比要复制的文件旧时，才替换现有文件；

- 当复制子目录时：

  - `none (0)`：跳过子目录（默认行为）；

  - `recursive (8)`：递归地复制子目录及其内容；

- 当复制符号链接时：

  - `none (0)`：跟随符号链接（默认行为）；

  - `copy_symlinks (16)`：将符号链接作为符号链接进行复制

- 控制 `copy` 的行为：

  - `none (0)`：复制文件内容（默认行为）；

  - `directories_only (64)`：复制目录结构，但不复制任何目录文件；

  - `create_symlinks (128)`：不创建副本，而是创建指向原始文件的符号链接（除非目标路径在当前目录，否则源路径必须是绝对路径）；

  - `create_hard_links (256)`：不创建文件的副本，而是创建硬链接指向与原始相同的文件。

以下函数需要 `path` 参数：

- `path absolute(path const &src, [, error_code &ec])`：返回指定为绝对路径的 `src` 副本（即从磁盘根开始）。它可以像 `absolute("/filename")` 这样调用，返回绝对当前工作目录，`absolute` 的参数作为最后一个元素追加其，并用目录分隔符分隔。相对路径指示（`../` 和 `./`）会被保留。返回的仅仅是一个绝对路径。如果应该移除相对路径指示，请使用下一个函数；

- `path canonical(path const &src [, error_code &ec])`：返回指向现有目录的 `src` 的规范路径。示例：

```cpp
int main() {
    path man = "/usr/local/bin/../../share/man";
    cout << canonical(man) << '\n'; // 显示: "/usr/share/man"
}
```

## 第 4 章 命名空间

- `void copy(path const &src, path const &dest [, copy_options opts [, error_code &ec]);`

  - `src` 必须存在。如果 `cp` 程序也能成功，则将 `src` 复制到 `dest`。

  - 如果 `src` 是目录且 `dest` 不存在，则创建 `dest`。如果指定了选项 `recursive` 或 `none`，则递归复制目录；

- `bool copy_file(path const &src, path const &dest [, copy_options opts [, error_code &ec]);`

  - `src` 必须存在。如果 `cp` 程序也能成功，则将 `src` 复制到 `dest`。会跟随符号链接。如果复制成功则返回 true；

- `void copy_symlink(path const &src, path const &dest [, error_code &ec]);`

  - 创建符号链接 `src` 的副本作为符号链接；

- `bool create_directories(path const &dest [, error_code &ec]);`

  - 创建 `dest` 的每个组件，除非已存在。如果 `dest` 确实被创建，则返回 true。如果返回 false，则包含一个错误码，如果已存在则为 0 (`ec.value() == 0`)。另请参见 `create_directory`；

- `bool create_directory(path const &dest [, path const &existing], error_code &ec]);`

  - `dest` 的父目录必须存在。如果目录不存在，此函数将创建它。如果 `dest` 确实被创建，则返回 true。如果返回 false，`ec` 包含错误码，如果已存在则为 0 (`ec.value() == 0`)。

- `void create_directory_symlink(path const &dir, path const &link [, error_code &ec]);`

  - 类似于 `copy_symlink`（见下文），但用于创建指向目录的符号链接；

- `void create_hardlink(path const &dest, path const &link [, error_code &ec]);`

  - 从 `link` 到 `dest` 创建硬链接。`Dest` 必须存在；

- `void create_symlink(path const &dest, path const &link [, error_code &ec]);`

  - 从 `link` 到 `dest` 创建符号（软）链接；`dest` 不一定存在；

- `current_path{error_code &ec}, void current_path(path const &toPath, error_code &ec);`

  - 前者返回当前工作目录 (`cwd`)，后者将 `cwd` 更改为 `toPath`。返回路径的最后一个字符不是斜杠，除非是从根目录调用的；

- `bool equivalent(path const &path1, path const &path2 [, error_code &ec]);`

  - 如果 `path1` 和 `path2` 指向同一个文件或目录且具有相同状态，返回 true。两个路径必须存在；

- `bool exists(path const &dest [, error_code &ec]), exists(file_status status);`

  - 如果 `dest` 存在则返回 true（实际上：如果 `status(dest, ec)` 返回 true）。当遍历目录时，迭代器返回条目的状态。在这种情况下，`exists(iterator->status)` 比调用 `exists(*iterator)` 更高效。如果是符号链接，见第 4.3.4 节。

- `std::uintmax_t file_size(path const &dest [, error_code &ec]);`

  - 返回普通文件（或链接目标）的字节大小；

- `std::uintmax_t hard_link_count(path const &dest [, error_code &ec]);`

  - 返回与 `dest` 关联的硬链接；

- `time_point<__file_clock> last_write_time(path const &dest [, error_code &ec]);`

  - 返回最后修改时间。`void last_write_time(path const &dest, time_point<__file_clock> newTime, error_code = ec);`
