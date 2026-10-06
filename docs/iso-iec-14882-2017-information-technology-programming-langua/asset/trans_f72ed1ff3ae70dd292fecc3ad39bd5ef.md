

# ISO/IEC 14882:2017(E)

## 30.10.15.22 是否普通文件

[fs.op.is_regular_file]

```
bool is_regular_file(file_status s) noexcept;
  Returns: s.type() == file_type::regular;
bool is_regular_file(const path& p);
  Returns: is_regular_file(status(p));
Throws: 如果 status(p) 会抛出 filesystem_error 则抛出。
bool is_regular_file(const path& p, error_code& ec) noexcept;
  Effects: 设置 ec 相当于 status(p, ec)。注: file_type::none, file_type::not_found 和 file_type::unknown会将 ec 设置为错误值。要区分这些情况，请调用 status 函数。]
  is_regular_file(status(p, ec)). 如果发生错误则返回 false。
```

# 30.10.15.23 是否套接字

[fs.op.is_socket]

```
bool is_socket(file_status s) noexcept;
  Returns: s.type() == file_type::socket;
bool is_socket(const path& p);
bool is_socket(const path& p, error_code& ec) noexcept;
  Returns: is_socket(status(p)) 或 is_socket(p, ec)，带有
  参数 ec 的签名在发生错误时返回 false。
Throws: 如 30.10.7 所示。
```

# 30.10.15.24 是否为符号链接

[fs.op.is_symlink]

```
bool is_symlink(file_status s) noexcept;
  Returns: s.type() == file_type::symlink.
bool is_symlink(const path& p);
bool is_symlink(const path& p, error_code& ec) noexcept;
  Returns: 分别返回 is_symlink(symlink_status(p)) 或 is_symlink(p, ec)。带有
  参数 ec 的签名在发生错误时返回 false。
Throws: 如 30.10.7 所示。
```

# 30.10.15.25 最后写入时间

[fs.op.last_write_time]

```
file_time last_write_time(const path& p);
file_time last_write_time(const path& p, error_code& ec) noexcept;
  Returns: p 的最后修改时间。其确定方式相当于由 POSIX stat
  结构 st_mtime 按照 POSIX stat(0) 赋值。带有参数 ec 的签名
  在发生错误时返回 file_time::min()。
  Throws: 如 30.10.7 所示。
void last_write_time(const path& p, file_time_type new_time);
void last_write_time(const path& p, error_code& ec) noexcept;
  Effects: 将解析 p 的文件最后修改时间设置为 new_time，相当于通过 POSIX
  futimes() 设置。
```

Throws: 如 30.10.7 所示。

[注：未规定 last_write_time(p) == new_time 的延迟，因为这对于粒度粗糙的文件系统可能不成立。—— 备注结束]

# 30.10.15.26 权限 [fs.op.permissions]

```
void permissions(const path p, perms prms, perm_options opts=perm_options::replace);
void permissions(const path p, perms prms, error_code ec) noexcept;
void permissions(const path p, perms prms, perm_options opts, error_code ec);
```

- 1 要求 opts 中必须存在 replace, add 或 remove perm_options 中的其中之一。
- 2 备注：该签名的行为相当于有一个额外的参数 perm_options opts，其参数为 opts::replace。
- 3 影响：opts 应用于文件 p 的操作解析到 p，或者如果 p 是符号链接且设置了 perm_options::nofollow，则解析到 p 本体，相当于 POSIX fchmod(at)。
- 4 [注：上下文权限被视为位，但实际实现可能使用某些其他机制。—— 备注结束]
- 5 抛出：如 30.10.7 所示。

# 30.10.15.27 接近 [fs.op.proximate]

```
path proximate(const path p, error_code ec);
```

- 1 返回：proximate(p, current_path(), ec)。
- 2 抛出：如 30.10.7 所示。

```
path proximate(const path p, const path base = current_path());
path proximate(const path p, const path base, error_code ec);
```

- 3 返回：对于第一形式：weakly_canonical(p).lexically_proximate(weakly_canonical(base));
  对于第二形式：weakly_canonical(p, ec).lexically_proximate(weakly_canonical(base, ec));
- 4 如果第一次出现时，返回 path()。
- 4 抛出：如 30.10.7 所示。

# 30.10.15.28 读取符号链接 [fs.op.read_symlink]

```
path read_symlink(const path p);
path read_symlink(const path p, error_code ec);
```

- 1 返回：如果 p 解析为符号链接，则返回符号链接内容的路径。带有参数 ec 的签名在发生错误时返回 path()。
- 2 抛出：如 30.10.7 所示。[注：如果 p 解析为符号链接则报错。—— 备注结束]

# 30.10.15.29 相对 [fs.op.relative]

```
path relative(const path p, error_code ec);
```

- 1 返回：relative(p, current_path(), ec)。
- 2 抛出：如 30.10.7 所示。

```
path relative(const path& p, const path base = current_path());
path relative(const path& p, const path base, error_code ec);
```

- 3 返回：对于第一形式：weakly_canonical(p).lexically_proximate(weakly_canonical(base));
  对于第二形式：weakly_canonical(p, ec).lexically_proximate(weakly_canonical(base, ec));
- 4 如果第一次出现时，返回 path()。
- 4 抛出：如 30.10.7 所示。

# 30.10.15.30 删除

```
bool remove(const path& p);
bool remove(const path& p, error_code ec) noexcept;
```

Effects：如果存在(symlink_status(p, ec))，则按照 POSIX remove() 删除 p。[注：删除符号链接本身而非其解析的文件。—— 备注结束]
- 2 后置条件：exists(symlink_status(p)) 为 false。
- 3 返回：如果 p 不存在返回 true。带有参数 ec 的签名在发生错误时返回 false。
- 4 抛出：如 30.10.7 所示。

# 30.10.15.31 全部删除

```
uintmax_t remove_all(const path& p);
uintmax_t remove_all(const path& p, error_code ec) noexcept;
```

Effects：如果 p 存在，则递归删除 p 的内容，删除 p 本体，相当于 POSIX remove()。[注：删除符号链接本身而非其解析的文件。—— 备注结束]
- 2 后置条件：exists(symlink_status(p)) 为 false。
- 3 返回：删除的文件数量。带有参数 ec 的签名在发生错误时返回 static_cast<uintmax_t>(-1)。
- 4 抛出：如 30.10.7 所示。

# 30.10.15.32 重命名

```
void rename(const path& old_p, const path& new_p);
void rename(const path& old_p, const path& new_p, error_code ec) noexcept;
```

- 1 影响：按照 POSIX rename() 将 old_p 移动到 new_p。[注：
(1.1) 如果 old_p 和 new_p 解析为同一个现有文件，则不采取操作。
(1.2) 否则，重命名可能包括以下影响：
(1.2.1) —— 如果 new_p 解析为现有非目录文件，则删除 new_p；否则；
—— 如果 new_p 解析为现有目录，在符合 POSIX 标准的操作系统上如果为空则删除，但在其他操作系统上可能如此。
重命名符号链接本身而非其解析的文件。—— 备注结束]
2 抛出：如 30.10.7 所示。

# 30.10.15.33 调整文件大小

```
resize_file(const path& p, uintmax_t new_size);
resize_file(const path& p, uintmax_t new_size, error_code ec) noexcept;
```

- 后置条件：file_size(p) == new_size。
- 抛出：如 30.10.7 所示。
- 实现：如果通过 POSIX truncate() 实现其后置条件。

# 30.10.15.34 空间

```
space_info(const path& p);
space_info(const path& p, error_code ec) noexcept;
```

返回：一个 space_info 类型的对象。space_info 的值的确定方式相当于使用 POSIX statfs 获取一个 POSIX struct statfs，然后将其 f_blocks、f_bfree 和 f_available 成员分别乘以 f_size，并赋值给 capacity、free 和 available 成员，设置为 static_cast<uintmax_t>(-1)。对于带有参数 ec 的签名，如果发生错误，所有成员都将被设置为 static_cast<uintmax_t>(-1)。

- 抛出：如 30.10.7 所示。
- 实现：space_info::available 的值取决于操作系统。[注：available 可能小于 free。—— 备注结束]

# 30.10.15.35 状态

```
file_status(const path& p);
```

- 影响：如果

error_code ec;
file_status result = status(p, ec);
if (result.type() == file_type::none)
throw filesystem_error(implementation-supplied-message, p, ec);
return result;

- 返回：见下文。
抛出：file_status(file_type::not_found) 和 file_status(file_type::unknown) 的结果值不被视为失败，且不会导致抛出异常。—— 备注结束

```
file_status(const path& p, error_code ec) noexcept;
影响：如果，确定路径 p 解析到的属性，相当于使用 POSIX stat()。如果在确定期间，底层系统 API 报告错误，则 ec 指明指定的错误。否则，ec.clear。[注：这允许用户在 status() 返回的值不是 file_status(file_type::none) 时也能指定 API 错误的细节。—— 备注结束
```

让 perms 为 (m & per::mask) 的结果，其中 m 通过将观测到的 struct stat 的 st_mode 转换为 per 类型确定。

- 返回：
如果 ec != error_code():
如果特定错误指示由于路径中的某些元素不存在导致无法解析，则返回 file_status(file_type::not_found)。

