

# ISO/IEC 14882:2017(E)

(6.4) 具有特殊含义的文件名。

(6.5) 路径解析中的感知与敏感性。

(6.6) 适用于普通文件之外的文件类型（如目录）的特殊规则。

指向现有文件的硬链接。某些文件系统支持对一个文件的多个硬链接。如果一个文件的最后一个硬链接被删除，该文件本身也会被删除。[注：硬链接可以被视为指向文件的共享所有权指针。] — 附结束

链接是一个与文件关联的实体。多个链接可以关联同一个文件。

字符字符串的原生编码是取决于操作系统的路径名当前编码。宽字符字符串的原生编码是取决于实现的执行期宽字符集编码 (5.3)。

原生格式是取决于操作系统的、被宿主操作系统接受的路径名格式。

通用路径的规范化（Normalization）意味着：

- 1. 如果路径为空，
- 2. 将每个斜杠分隔符替换为首选分隔符。
- 3. 将每个目录分隔符替换为首选分隔符。[注：通用语法 (30.10.8.1) 定义目录分隔符为一个或多个分隔符，首选分隔符亦然。] — 附结束
- 4. 删除每个点目录以及紧随其后的目录分隔符。
- 5. 只要路径存在，就删除紧跟在目录分隔符后的点点，以及任何紧随其后的目录分隔符。
- 6. 如果存在根目录，删除所有点点文件名以及其后的任何目录分隔符。[注：这些点点试图引用不存在的父目录。] — 附结束
- 7. 如果最后一个组件是点点，删除任何末尾的目录分隔符。
- 8. 如果路径为空，

规范化的结果是一个标准形式的路径，被称为已规范化。

取决于操作系统行为和特性的取决于操作系统的行为。30.10.2.2。

目录的父目录是包含该目录条目并在文件中用点点符号表示的目录。其他类型文件的父目录是包含所讨论文件的目录条目的目录。

用于标识文件在文件系统中位置的元素序列。这些元素包括根名称、目录分隔符和可选的文件名序列。序列中元素的最大数量取决于操作系统。

路径名是一个表示路径名称的字符字符串。路径名根据通用路径名语法 (30.10.8.1) 或取决于操作系统的原生路径名格式进行格式化。

路径名解析是将路径名解析为层级结构中文件的取决于操作系统的机制。可能有多个路径指向同一个文件。[示例：POSIX 在第 4.1 节“路径名解析”中规定了该机制。] — 示例结束

相对路径不是绝对路径，因此在相对于隐含起始位置进行解析时，能够唯一地标识文件的位置。决定其是否取决于操作系统的路径元素。[注：路径名 "/" 和 "../" 是相对路径。] — 附结束

符号链接是一种文件类型，其属性为：在路径名解析过程中会遇到该文件，且文件中存储的字符串用于标识路径名解析。[注：符号链接通常称为 symlinks。符号链接可以被视为指向文件的指针。如果文件不存在，则该符号链接被称为“悬空”符号链接。] — 附结束

## 30.10.5 Requirements [fs.req]

- 1. 通过此子类，`char`、`wchar_t`、`char16_t` 和 `char32_t` 共同构成编码字符类型。
- 2. 带有模板参数 `ECharT` 的函数参与重载解析；`ECharT` 是编码字符类型之一。
- 3. 模板参数 `InputIterator` 应满足要求 (27.2.3)，且其值为编码字符类型之一。[注：使用编码字符类型意味着关联字符集和编码。由于 `signed` 和 `unsigned char` 没有字符集和编码，因此它们不是允许的类型。] — 附结束
- 4. 模板参数 `Allocator` 应满足分配器要求 (20.5.3)。

## 30.10.5.1 Namespaces and headers [fs.req.namespace]

- 1. 另有规定，对此子类描述的实体的引用假设通过 `::std::filesystem` 限定

## 30.10.6 Header <filesystem> synopsis [fs.filesystem.syn]

```cpp
namespace filesystem {
// 30.10.8, paths
class path;

// 30.10.8.6, path non-member functions
void swap(path& lhs, path& rhs) noexcept;
size_t hash_value(const path& p) noexcept;

bool operator!==(const path& lhs, const path& rhs) noexcept;
bool operator==(const path lhs, const path& rhs) noexcept;
bool operator<(const path lhs, const path& rhs) noexcept;
bool operator>(const path& lhs, const path& rhs) noexcept;
bool operator<=(const path& lhs, const path& rhs) noexcept;
bool operator>=(const path& lhs, const path& rhs) noexcept;

path operator/(const path& lhs, const path& rhs);

// 30.10.8.1, path inserter and extractor
template<class charT, class traits>
basic_ostream<charT, traits>
operator<<(basic_ostream<charT, traits>& os, const path& p);
template<class charT, class traits>
operator>>(basic_istream<charT, traits>& is, const path& p);

// 30.10.8.6.2, path factory functions
template<class Source>
path u8path(const Source& source);
```

