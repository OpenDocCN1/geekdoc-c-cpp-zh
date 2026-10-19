

```cpp
bool exists(error_code& ec) const noexcept;
bool is_block_file() const;
bool is_block_file(error_code& ec) const noexcept;
bool is_character_file() const;
bool is_character_file(error_code& ec) const noexcept;
bool is_directory() const;
bool is_directory(error_code& ec) const noexcept;
bool is_fifo() const;
bool is_fifo(error_code& ec) const noexcept;
bool is_other() const;
bool is_other(error_code& ec) const noexcept;
bool is_regular_file() const;
bool is_regular_file(error_code& ec) const noexcept;
bool is_socket() const;
bool is_socket(error_code& ec) const noexcept;
bool is_symlink() const;
bool is_symlink(error_code& ec) const noexcept;
uintmax_t file_size() const;
uintmax_t file_size(error_code& ec) const noexcept;
uintmax_t hard_link_count() const;
uintmax_t hard_link_count(error_code& ec) const noexcept;
file_time_type last_write_time() const;
file_time_type last_write_time(error_code& ec) const noexcept;
file_status status() const;
file_status status(error_code& ec) const noexcept;
file_status symlink_status() const;
file_status symlink_status(error_code& ec) const noexcept;

bool operator==(const directory_entry& rhs) const noexcept;
strong_ordering operator<=>(const directory_entry& rhs) const noexcept;

private:
  filesystem::path pathobject;          // exposition only
  friend class directory_iterator;      // exposition only
};
}
```

> ¹  `directory_entry` 对象存储一个路径对象，并且可能存储文件属性的额外对象，例如硬链接计数、状态、符号链接状态、文件大小和最后写入时间。

> ²  实现应在目录迭代期间存储此类额外文件属性，如果其值可用并且存储这些值可以使实现消除 `directory_entry` 观察者函数 ([29.11.13]) 的文件系统访问。 这种存储的文件属性值被称为 *缓存*。

> ³  [*注 1:* 为便于说明，类 `directory_iterator` ([29.11.11]) 在此显示为类 `directory_entry` 的友元。 友元关系允许 `directory_iterator` 实现直接将已可用的属性值缓存到 `directory_entry` 对象中，而无需不必要的对 `refresh()` 的调用。 — *注结束*]

```
⁴  [*示例 1:*

```cpp
using namespace std::filesystem;

// use possibly cached last write time to minimize disk accesses
for (auto&& x : directory_iterator("."))
{
  std::cout << x.path() << " " << x.last_write_time() << std::endl;
}

// call refresh() to refresh a stale cache
for (auto&& x : directory_iterator("."))
{
  lengthy_function(x.path());   // cache becomes stale
  x.refresh();
  std::cout << x.path() << " " << x.last_write_time() << std::endl;
}
```]
```

在未缓存最后写入时间的实现上，两个循环都将导致对 `std::filesystem::last_write_time` 函数的潜在昂贵调用。 在缓存最后写入时间的实现上，第一个循环将使用缓存的值，因此不会导致对 `std::filesystem::last_write_time` 函数的潜在昂贵调用。 代码可移植到任何实现，无论是否采用缓存。 — *示例结束*

## 29.11.10.2 构造函数

```cpp
explicit directory_entry(const filesystem::path& p);
directory_entry(const filesystem::path& p, error_code& ec);
```

1  *效果：* 分别调用 `refresh()` 或 `refresh(ec)`。

2  *后置条件：* 如果未发生错误，则 `path() == p`，否则 `path() == filesystem::path()`。

3  *抛出：* 如 [29.11.5] 所述。

## 29.11.10.3 修改器

```cpp
void assign(const filesystem::path& p);
void assign(const filesystem::path& p, error_code& ec);
```

1  *效果：* 等价于 `pathobject = p`，然后分别调用 `refresh()` 或 `refresh(ec)`。 如果发生错误，则任何缓存属性的值为未指定。

2  *抛出：* 如 [29.11.5] 所述。

```cpp
void replace_filename(const filesystem::path& p);
void replace_filename(const filesystem::path& p, error_code& ec);
```

3  *效果：* 等价于 `pathobject.replace_filename(p)`，然后分别调用 `refresh()` 或 `refresh(ec)`。 如果发生错误，则任何缓存属性的值为未指定。

*抛出：* 如 [29.11.5] 所述。

```cpp
void refresh();
void refresh(error_code& ec) noexcept;
```

4  *效果：* 存储文件 `p` 解析到的任何缓存属性的当前值。 如果发生错误，则报告错误 ([29.11.5])，并且任何缓存属性的值为未指定。

5  *抛出：* 如 [29.11.5] 所述。

6  [*注 1:* `directory_iterator` ([29.11.11]) 的实现禁止直接或间接调用 `refresh` 函数，如 [29.11.11.1] 所述。 — *注结束*]

## 29.11.10.4 观察者

1  `directory_entry` 观察者下方 *返回：* 元素中的不合格函数名指的是 `std::filesystem` 命名空间的成员。

```cpp
const filesystem::path& path() const noexcept;
operator const filesystem::path&() const noexcept;
```

2  *返回：* `pathobject`。

```cpp
bool exists() const;
bool exists(error_code& ec) const noexcept;
```

3  *返回：* 分别为 `exists(this->status())` 或 `exists(this->status(ec))`。

4  *抛出：* 如 [29.11.5] 所述。

```cpp
bool is_block_file() const;
bool is_block_file(error_code& ec) const noexcept;
```

5  *返回：* 分别为 `is_block_file(this->status())` 或 `is_block_file(this->status(ec))`。

6  *抛出：* 如 [29.11.5] 所述。

```cpp
bool is_character_file() const;
bool is_character_file(error_code& ec) const noexcept;
```

7  *返回：* 分别为 `is_character_file(this->status())` 或 `is_character_file(this->status(ec))`。

# ISO/IEC 14882:2020(E)

抛出：如 29.11.5 所述。

```
bool is_directory() const;
bool is_directory(error_code& ec) const noexcept;
```

返回：is_directory(this->status()) 或 is_directory(this->status(ec))，分别。

抛出：如 29.11.5 所述。

```
bool is_fifo() const;
bool is_fifo(error_code& ec) const noexcept;
```

返回：is_fifo(this->status()) 或 is_fifo(this->status(ec))，分别。

抛出：如 29.11.5 所述。

```
bool is_other() const;
bool is_other(error_code& ec) const noexcept;
```

返回：is_other(this->status()) 或 is_other(this->status(ec))，分别。

抛出：如 29.11.5 所述。

```
bool is_regular_file() const;
bool is_regular_file(error_code& ec) const noexcept;
```

返回：is_regular_file(this->status()) 或 is_regular_file(this->status(ec))，分别。

抛出：如 29.11.5 所述。

```
bool is_socket() const;
bool is_socket(error_code& ec) const noexcept;
```

返回：is_socket(this->status()) 或 is_socket(this->status(ec))，分别。

抛出：如 29.11.5 所述。

```
bool is_symlink() const;
bool is_symlink(error_code& ec) const noexcept;
```

返回：is_symlink(this->symlink_status()) 或 is_symlink(this->symlink_status(ec))，分别。

抛出：如 29.11.5 所述。

```
uintmax_t file_size() const;
uintmax_t file_size(error_code& ec) const noexcept;
```

返回：如果已缓存，则为文件大小属性值。 否则，分别为 file_size(path()) 或 file_size(path(), ec)。

抛出：如 29.11.5 所述。

## 29.11.11.2 成员 [fs.dir.itr.members]

6 通过解引用 directory_iterator 获得的 directory_entry 对象的 path() 成员调用的结果是引用到由迭代器构造时使用的目录参数组成的路径对象，并附加目录条目的文件名，方式如同 operator/=

7 目录迭代不得为当前目录（点）和父目录（点点）产生目录条目。

8 通过对 directory_iterator 进行连续递增解引用获得的目录条目的顺序是不指定的。

9 构造函数和非 const directory_iterator 成员函数在 operator*() 返回的 directory_entry 元素中存储任何缓存属性（29.11.10）的值。 directory_iterator 成员函数不得直接或间接调用任何 directory_entry refresh 函数。

> [注 2: 存储缓存属性值的确切机制未向用户公开。 为便于说明，类 directory_iterator 在 29.11.10 中显示为类 directory_entry 的友元。 — 注结束]

> [注 3: 通过解引用目录迭代器获得的路径可能实际上并不存在；例如如果它是链接到不存在文件的符号链接。 为删除和重命名条目目的递归遍历目录树可能会使正在被跟随的符号链接失效。 — 注结束]

> [注 4: 如果在为目录构造 directory_iterator 之后从目录中删除或添加文件，则是否随后递增迭代器会产生引用已删除或已添加目录条目的迭代器是不指定的。 请参阅 POSIX readdir_r。 — 注结束]

```
directory_iterator() noexcept;
```

1 效果：构造结束迭代器。

```
explicit directory_iterator(const path& p);
directory_iterator(const path& p, directory_options options);
directory_iterator(const path& p, error_code& ec);
directory_iterator(const path& p, directory_options options, error_code& ec);
```

2 效果：对于 p 解析到的目录，构造一个表示目录中文件的 directory_entry 元素序列中第一个元素的迭代器，如果有的话；否则为结束迭代器。 然而，如果 (options & directory_options::skip_permission_denied) != directory_options::none 并且构造遇到指示无法访问 p 的权限被拒绝的错误，则构造结束迭代器并且不报告错误。

3 抛出：如 29.11.5 所述。

> [注 1: 要迭代当前目录，请使用 directory_iterator(".") 而不是 directory_iterator("")。 — 注结束]

```
directory_iterator(const directory_iterator& rhs);
directory_iterator(directory_iterator&& rhs) noexcept;
```

5 后置条件：*this 具有 rhs 的原始值。

```
directory_iterator& operator=(const directory_iterator& rhs);
directory_iterator& operator=(directory_iterator&& rhs) noexcept;
```

6 效果：如果 *this 和 rhs 是同一对象，则该成员无效果。

7 后置条件：*this 具有 rhs 的原始值。

8 返回：*this。

```
directory_iterator& operator++();
directory_iterator& increment(error_code& ec);
```

9 效果：如输入迭代器（23.3.5.3）的前缀递增操作所述。

10 返回：*this。

11 抛出：如 29.11.5 所述。

## 29.11.11.3 非成员函数 [fs.dir.itr.nonmembers]

1 这些函数为 directory_iterator 启用范围访问。

