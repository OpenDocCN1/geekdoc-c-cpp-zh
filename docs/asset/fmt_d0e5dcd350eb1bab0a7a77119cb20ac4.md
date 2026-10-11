
要求：`options` 在每个组（30.10.10.3）中至少设置了一个元素。

影响：

- 如果 `f.type()` 或 `t.type()` 是实现类型（30.10.10.2），则影响由实现定义。
- 否则，如果满足以下条件将按 30.10.7 报告错误：
    - `exists(f)` 为 false，或
    - `equivalent(from, to)` 为 true，或
    - (4.5.3) — `is_other(f)` || `is_other(t)` 为 true，或
    - (4.5.4) — `is_directory(f)` && `is_regular_file(t)` 为 true。
    - (4.6) — 否则，如果 `is_symlink(t)`，则：
        - (4.6.1) — 如果 (`options` & `copy_options::skip_symlinks`) != `copy_options::none` 则
        - (4.6.2) — 否则如果 `exists(t)` && (`options` & `copy_options::copy_symlinks`) != `copy_options::none`，则 `copy_symlink(from,to)`。
        - (4.6.3) — 否则按 30.10.7 报告错误。
    - (4.7) — 否则，如果 `is_regular(f)`，则：
        - (4.7.1) — 如果 (`options` & `copy_options::directories_only`) != `copy_options::none`，则
        - (4.7.2) — 否则，如果 (`options` & `copy_options::create_symlinks`) != `copy_options::none`，则创建源文件创建符号硬链接。
        - (4.7.3) — 否则，如果 (`options` & `copy_options::create_hard_links`) != `copy_options::none`，则向源文件创建硬链接。
        - (4.7.4) — 否则，如果 `is_directory(t)`，则 `copy_file(from,to.filename(), options)`。
        - (4.7.5) — 否则，`copy_file(from, to, options)`。
    - (4.8) — 否则，如果 `is_directory(f)` && ((`options` & `copy_options::recursive`) != `copy_options::none` || `options` = `copy_options::none`) 则
        - (4.8.1) — 如果 `exists(t)` 为 false，则 `create_directory(to, from)`。
        - (4.8.2) — 然后，遍历 `from` 中的文件，仿佛 `for (const directory_entry& x : directory_iterator(from)) copy(x.path(), to/x.path().filename(), options | copy_options::unspecified)`
        - 否则，对于带有 `ec` 的签名，`ec.clear()`。
        - 否则，无影响。

5 抛出：如 30.10.7 规定。

6 备注：对于带有 `ec` 的签名，实现调用的任何库函数都应具有适用的 `error_code` 参数。

## 30.10.15.5 拷贝符号链接 (Copy_symlink)

```cpp
void copy_symlink(const path& from, const path& to, const copy_options& = none);
void copy_symlink(const path& from, const path& to, error_code& ec) noexcept;
void copy_symlink(const path& from, const path& to, const copy_options& options);
void copy_symlink(const path& from, const path& to, const copy_options& options, error_code& ec) noexcept;
```

## 30.10.15.6 创建目录 (Create_directories)

```cpp
bool create_directories(const path& p);
bool create_directories(const path& p, error_code& ec) noexcept;
```

## 30.10.15.7 创建目录 (Create_directory)

```cpp
bool create_directory(const path& p);
bool create_directory(const path& p, error_code& ec) noexcept;
bool create_directory(const path& p, const path& existing_p);
bool create_directory(const path& p, const path& existing_p, error_code& ec) noexcept;
```

# ISO/IEC 14882:2017(E)

7 返回：如果创建了新目录则返回 true，否则返回 false。带有参数 `ec` 的签名在发生错误时返回 false。

8 抛出：如 30.10.7 所示。

# 30.10.15 创建目录符号链接

```cpp
void create_directory_symlink(const path& to, const path& new_symlink);
void create_directory_symlink(const path& to, const path& new_symlink, error_code& ec) noexcept;
```

- 1 效果：建立了后置条件，如 POSIX `symlink()`。
- 2 后置条件：`new_symlink` 解析为一个包含一个未指定 respect 的符号链接文件。
- 3 抛出：如 30.10.7 所示。
- 4 [注意：某些操作系统要求在创建符号链接时识别该链接为目录。可移植代码应使用 `create_directory_symlink()` 来创建目录符号链接，而不是 `create_symlink()` -- 注释]
- 5 [注意：某些操作系统完全不支持符号链接，或者仅支持普通文件。某些文件系统（如 FAT 文件系统）无论操作系统如何都不支持符号链接 -- 注释]

# 30.10.15.9 创建硬链接

```cpp
void create_hard_link(const path& to, const path& new_hard_link);
void create_hard_link(const path& to, const path& new_hard_link, error_code& ec) noexcept;
```

- 1 效果：建立了后置条件，如 POSIX `symlink()`。
- 2 后置条件：
  - `exists(to)` && `exists(new_hard_link)` && `equivalent(to, new_hard_link)`
  - 文件或目录的内容不会改变。
- 3 抛出：如 30.10.7 所示。
- 4 [注意：某些操作系统完全不支持硬链接，或者仅支持普通文件。某些文件系统（如 FAT 文件系统）无论操作系统如何都不支持硬链接。某些文件系统限制了每个文件的链接数 -- 注释]

# 30.10.15.10 创建符号链接

```cpp
void create_symlink(const path& to, const path& new_symlink);
void create_symlink(const path& to, const path& new_symlink, error_code& ec) noexcept;
```

- 1 效果：建立了后置条件，如 POSIX `symlink()`。
- 2 后置条件：`new_symlink` 解析为一个包含一个未指定 respect 的符号链接文件。
- 3 抛出：如 30.10.7 所示。
- 4 [注意：某些操作系统完全不支持符号链接，或者仅支持普通文件。某些文件系统（如 FAT 文件系统）无论操作系统如何都不支持符号链接 -- 注释]

# 30.10.15.11 当前路径 [fs.op.current_path]

```cpp
path current_path();
path current_path(error_code ec);
```

- 1 返回：当前工作目录的绝对路径，其在原生格式下的路径名通过 POSIX `getcwd()` 获取。带有参数 `ec` 的签名在发生错误时返回 `path()`。
- 2 抛出：如 30.10.7 所示。
- 3 备注：当前工作目录是与进程关联的目录，在相对路径的位置解析中作为起始位置。
- 4 [注意：选择 `current_path()` 作为名称是为了强调返回的是路径，而不仅仅是单个目录 -- 注释]
- 5 [注意：许多操作系统返回的路径是一个全局变量。它可能会被第三方库或线程意外地改变 -- 注释]

```cpp
void current_path(const path& p);
void current_path(const path& p, error_code ec) noexcept;
```

- 6 效果：建立了后置条件，如 POSIX `chdir()`。
- 7 后置条件：`equivalent(p, current_path())`。
- 8 抛出：如 30.10.7。
> 注意：许多操作系统返回的路径是一个全局变量。它可能会被第三方库或线程意外地改变 -- 注释]

# 30.10.15.12 等价 [fs.op.equivalent]

```cpp
bool equivalent(const path& p1, const path& p2);
bool equivalent(const path& p1, const path& p2, error_code ec) noexcept;
```

- 1 让 `s1` 和 `s2` 为 `file_status`，分别通过 `status(p1)` 和 `status(p2)` 确定。
- 2 效果：确定 `s1 == s2` 且 `p1` 和 `p2` 解析为同一个文件实体，否则返回 false。如果 `(!exists(s1) && !exists(s2)) || (is_other(s1) && is_other(s2)))` 则在 30.10.7 中报告错误。
- 3 返回：如果 `s1 == s2` 且 `p1` 和 `p2` 解析为同一个文件实体则返回 true，否则返回 false。带有参数 `ec` 的签名在发生错误时返回 `path()`。
- 4 如果两个路径位于同一设备的相同位置，则认为解析为同一个文件实体。这是通过 POSIX `st_dev` 和等于 `st_ino` 定的。
- 5 抛出：如 30.10.7。

# 30.10.15.13 存在 [fs.op.exists]

```cpp
bool exists(const path& p) noexcept;
bool exists(status_known s && s.type() != file_type::not_found);
bool exists(const path& p, error_code ec) noexcept;
```

- 1 返回：如果 `s` 是 `file_status`，分别通过 `status(p)` 和 `status(p, ec)` 确定。
- 2 效果：如果 `status_known(s)`，带有参数 `ec` 的签名清空 `ec`。
- 3 返回：`exists(s)`。
- 5 抛出：如 30.10.7。

# 30.10.15.14 文件大小

```cpp
uintmax_t file_size(const path& p);
uintmax_t file_size(const path& p, error_code ec) noexcept;
```

- 1 返回：
  - 如果 `(p)` 为 false，则在 30.10.7 中报告错误。
  - 否则，如果 `is_file(p)`，文件 `p` 的字节大小由 POSIX `stat()` 获取的 `st_size` 确定。
  -- 否则，结果由实现定义的。带有参数 `ec` 的签名在发生错误时返回 `static_cast<uintmax_t>()`。
- 2 抛出：如 30.10.7。

# 30.10.15.15 硬链接数

```cpp
uintmax_t hard_link_count(const path& p);
uintmax_t hard_link_count(const path& p, error_code ec) noexcept;
```

- 1 返回：`p` 的硬链接数。带有参数 `ec` 的签名在发生错误时返回 `static_cast<uintmax_t>()`。
- 2 抛出：如 30.10.7。

# 30.10.15.16 块

```cpp
bool is_block(const file_status s) noexcept;
bool s.type() == file_type::block;
bool is_block(const path& p, error_code ec) noexcept;
```

- 1 返回：分别通过 `is_block(status(p))` 或 `is_block(status(p, ec))`。带有参数 `ec` 的签名在发生错误时返回 false。
- 3 抛出：如 30.10.7。

# 30.10.15.17 字符文件

```cpp
bool is_character_file(file_status s) noexcept;
bool s.type() == file_type::character;
bool is_character_file(const path& p, error_code ec) noexcept;
```

- 1 返回：分别通过 `is_character_file(status(p))` 或 `is_character_file(status(p, ec))`。带有参数 `ec` 的签名在发生错误时返回 false。
- 3 抛出：如 30.10.7。

# 30.10.15.18 目录

```cpp
bool is_directory(file_status s) noexcept;
Returns: s.type() == file_type::directory.
- 1
```
```cpp
bool is_directory(const path& p);
bool is_directory(const path& p, error_code ec) noexcept;
```

- 2 返回：分别通过 `is_directory(status(p))` 或 `is_directory(status(ec))`。带有参数 `ec` 的签名在发生错误时返回 false
- 3 抛出：如 30.10.7。

# 30.10.15.19 是否空

```cpp
bool is_empty(const path& p);
bool is_empty(const path& p, error_code ec) noexcept;
```

- 1 效果：
  - (1.1) - 确定 `file_type s`，分别通过 `status(p)` 或 `status(ec)` 确定。
  - (1.2) - 带有参数 `ec` 的签名在发生错误时返回 false
  - (1.3) - 否则，如果 `is_directory(s)`:
    - (1.3.1) - 创建一个变量 `itr`，分别通过 `directory_iterator itr(p)` 或 `directory_iterator itr(p)` 创建。
    - (1.3.2) - 带有参数 `ec` 的签名在发生错误时返回 false
    - (1.3.3) - 否则，返回 `itr = directory_iterator()`。
  - (1.4) - 否则：
    - (1.4.1) - 确定 `uintmax_t sz`，分别通过 `file_size(p)` 或 `file_size(ec)` 确定。
    - (1.4.2) - 带有参数 `ec` 的签名在发生错误时返回 false
    - (1.4.3) - 否则，返回 `sz = 0`。
- 2 抛出：如 30.10.7。

# 30.10.15.20 文件

```cpp
bool is_file(file_status s) noexcept;
bool is_file(const path& p, error_code ec) noexcept;
```

- 1 返回：`s.type() == file_type::file.`

```cpp
bool is_file(const path& p);
bool is_file(const path& p, error_code ec) noexcept;
```

- 2 返回：分别通过 `is_file(status(p))` 或 `is_file(status(ec))`。带有参数 `ec` 的签名在发生错误时返回 false。
- 3 抛出：如 30.10.7。

# 30.10.15.21 其他

```cpp
bool is_other(file_status s) noexcept;
```

- 1 返回：`exists(s) && !is_regular(s) && !is_directory(s) && !is_symlink(s).`
