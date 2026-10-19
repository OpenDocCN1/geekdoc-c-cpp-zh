
```
}
    cout << "World!" << '\n';
}
```

产生*非交错*输出

```
Goodbye, Planet!
Hello, World!
```

— *示例结束*]

## 29.11 文件系统 [filesystems]

### 29.11.1 概述 [fs.general]

1 第 29.11 条描述了文件系统及其组件的操作，例如路径、常规文件和目录。

2 *文件系统*是文件及其属性的集合。

3 *文件*是文件系统内保存用户或系统数据的对象。文件可以写入、读取，或者两者兼可。文件具有某些属性，包括类型。文件类型包括常规文件和目录。实现还可以支持其他类型的文件，如符号链接。

4 *目录*是文件系统内充当目录项容器的文件，这些目录项包含关于其他文件的信息，可能包括其他目录文件。目录的*父目录*是这样一个目录：它既包含给定目录的目录项，又在该目录中以双点文件名（29.11.6.2）表示。其他类型文件的*父目录*是包含所讨论文件的目录项的目录。

5 *链接*是将文件名与文件关联的对象。多个链接可以将名称与同一文件关联。*硬链接*是指向现有文件的链接。某些文件系统支持一个文件有多个硬链接。如果指向某文件的最后一个硬链接被移除，该文件本身也会被移除。

[注 1：硬链接可以视为对文件的共享所有权智能指针。——*注终*]

*符号链接*是一种文件类型，当在路径名解析（29.11.6）期间遇到该文件时，该文件存储的字符串用于修改路径名解析。

[注 2：符号链接通常称为 symlink。符号链接可以视为指向文件的原始指针。如果所指向的文件不存在，则称该符号链接为“悬空”符号链接。——*注终*]

### 29.11.2 符合性 [fs.conformance]

#### 29.11.2.1 概述 [fs.conformance.general]

1 符合性以行为来规定。理想行为并不总是可实现，因此符合性子条款考虑到了这一点。

#### 29.11.2.2 POSIX 符合性 [fs.conform.9945]

#### 29.11.2.3 依赖于操作系统行为的符合性 [fs.conform.os]

1 被指定为依赖于操作系统的行为依赖于操作系统的行为和特性。实现所依赖的操作系统由实现定义。

2 实现可以依赖于操作系统模拟器，而不是实际底层操作系统。

#### 29.11.2.4 文件系统竞争行为 [fs.race.behavior]

1 文件系统竞争是指多个线程、进程或计算机对同一文件系统内的对象交错访问和修改时出现的状况。如果调用第 29.11 条提供的函数引发文件系统竞争，则行为未定义。

2 如果文件系统竞争的可能性使得程序在调用此处所描述的函数之前测试前置条件变得不可靠，则该函数的前置条件（Preconditions:）不予以指定。

[注 1：作为设计实践，当程序在调用函数之前无法合理地检测到前置条件时，不指定前置条件。—— 注终]

### 29.11.3 要求 [fs.req]

#### 29.11.3.1 概述 [fs.req.general]

1 在整个第 29.11 条中，char、wchar_t、char8_t、char16_t 和 char32_t 统称为编码字符类型。

2 具有名为 EcharT 的模板参数的函数不得参与重载决议，除非 EcharT 是编码字符类型之一。

3 名为 InputIterator 的模板参数应满足 Cpp17InputIterator 要求（23.3.5.3），并且其值类型应为编码字符类型之一。

4 [注 1：使用编码字符类型意味着关联的字符集和编码。由于 signed char 和 unsigned char 没有隐含的字符集和编码，因此它们不包括在允许的类型中。—— 注终]

5 名为 Allocator 的模板参数应满足 Cpp17Allocator 要求（表 36）。

#### 29.11.3.2 命名空间和头文件 [fs.req.namespace]

1 除非另有规定，对第 29.11 条所描述实体的引用应视为使用 ::std::filesystem:: 限定。

### 29.11.4 `<filesystem>` 头文件概要 [fs.filesystem.syn]

```
#include <compare>    // see 17.11.1

namespace std::filesystem {
  // 29.11.6, paths
  class path;

  // 29.11.6.8, path non-member functions
  void swap(path& lhs, path& rhs) noexcept;
  size_t hash_value(const path& p) noexcept;

  // 29.11.7, filesystem errors
  class filesystem_error;

  // 29.11.10, directory entries
  class directory_entry;

  // 29.11.11, directory iterators
  class directory_iterator;

  // 29.11.11.3, range access for directory iterators
  directory_iterator begin(directory_iterator iter) noexcept;
  directory_iterator end(const directory_iterator&) noexcept;

  // 29.11.12, recursive directory iterators
  class recursive_directory_iterator;

  // 29.11.12.3, range access for recursive directory iterators
  recursive_directory_iterator begin(recursive_directory_iterator iter) noexcept;
  recursive_directory_iterator end(const recursive_directory_iterator&) noexcept;

  // 29.11.9, file status
  class file_status;

  struct space_info {
    uintmax_t capacity;
    uintmax_t free;
    uintmax_t available;

    friend bool operator==(const space_info&, const space_info&) = default;
  };

  // 29.11.8, enumerations
  enum class file_type;
  enum class perms;
  enum class perm_options;
  enum class copy_options;
  enum class directory_options;

  using file_time_type = chrono::time_point<chrono::file_clock>;

  // 29.11.13, filesystem operations
  path absolute(const path& p);
  path absolute(const path& p, error_code& ec);

  path canonical(const path& p);
  path canonical(const path& p, error_code& ec);

  void copy(const path& from, const path& to);
  void copy(const path& from, const path& to, error_code& ec);
  void copy(const path& from, const path& to, copy_options options);
  void copy(const path& from, const path& to, copy_options options, error_code& ec);

  bool copy_file(const path& from, const path& to);
  bool copy_file(const path& from, const path& to, error_code& ec);
  bool copy_file(const path& from, const path& to, copy_options option);
  bool copy_file(const path& from, const path& to, copy_options option, error_code& ec);

  void copy_symlink(const path& existing_symlink, const path& new_symlink);
  void copy_symlink(const path& existing_symlink, const path& new_symlink, error_code& ec) noexcept;

  bool create_directories(const path& p);
  bool create_directories(const path& p, error_code& ec);

  bool create_directory(const path& p);
  bool create_directory(const path& p, error_code& ec) noexcept;

  bool create_directory(const path& p, const path& attributes);
  bool create_directory(const path& p, const path& attributes, error_code& ec) noexcept;

  void create_directory_symlink(const path& to, const path& new_symlink);
  void create_directory_symlink(const path& to, const path& new_symlink, error_code& ec) noexcept;

  void create_hard_link(const path& to, const path& new_hard_link);
  void create_hard_link(const path& to, const path& new_hard_link, error_code& ec) noexcept;

  void permissions(const path& p, perms prms, perm_options opts=perm_options::replace);
  void permissions(const path& p, perms prms, error_code& ec) noexcept;
  void permissions(const path& p, perms prms, perm_options opts, error_code& ec);

  path proximate(const path& p, error_code& ec);
  path proximate(const path& p, const path& base = current_path());
  path proximate(const path& p, const path& base, error_code& ec);

  path read_symlink(const path& p);
  path read_symlink(const path& p, error_code& ec);

  path relative(const path& p, error_code& ec);
  path relative(const path& p, const path& base = current_path());
  path relative(const path& p, const path& base, error_code& ec);

  bool remove(const path& p);
  bool remove(const path& p, error_code& ec) noexcept;

  uintmax_t remove_all(const path& p);
  uintmax_t remove_all(const path& p, error_code& ec);

  void rename(const path& from, const path& to);
  void rename(const path& from, const path& to, error_code& ec) noexcept;

  void resize_file(const path& p, uintmax_t size);
  void resize_file(const path& p, uintmax_t size, error_code& ec) noexcept;

  space_info space(const path& p);
  space_info space(const path& p, error_code& ec) noexcept;

  file_status status(const path& p);
  file_status status(const path& p, error_code& ec) noexcept;

  bool status_known(file_status s) noexcept;

  file_status symlink_status(const path& p);
  file_status symlink_status(const path& p, error_code& ec) noexcept;

  path temp_directory_path();
  path temp_directory_path(error_code& ec);

  path weakly_canonical(const path& p);
  path weakly_canonical(const path& p, error_code& ec);
}
```

1 实现应确保 file_time_type 的分辨率和范围反映操作系统相关文件时间值的分辨率和范围。

### 29.11.5 错误报告 [fs.err.report]

1 文件系统库函数通常提供两个重载：一个抛出异常来报告文件系统错误，另一个设置 error_code。

[注 1：这支持两种常见使用场景：

- (1.1) —— 文件系统错误确实属于异常情况并表明严重失败的场景。抛出异常是适当的响应。
- (1.2) —— 文件系统错误属于常规情况且不一定代表失败的场景。返回错误码是最适当的响应。这允许特定于应用程序的错误处理，包括简单地忽略错误。

—— 注终]

2 除非另有规定，没有 error_code& 类型参数的函数按以下方式处理错误：

- (2.1) —— 当实现调用操作系统或其他底层 API 导致错误，使函数无法满足其规范时，应抛出 filesystem_error 类型的异常。对于具有单个路径参数的函数，该参数应被传递

