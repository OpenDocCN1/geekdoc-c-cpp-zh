

# ISO/IEC 14882:2020(E)

6 [注 4：一个 path 存储原生格式路径名（29.11.6.5.6）并如同也存储一个通用格式路径名，其关系如下给出。实现可以在需要时基于原生格式路径名（以及可能的其他信息）生成通用格式路径名。——注结束]

7 当一个 path 从或被赋值为与任何 path 分离的单个表示时，另一个表示由适当的转换函数（G 或 N）选择。

8 当一个 path 的一个表示的（新）值 p 由该 path 或另一个 path 的表示派生时，为另一个表示选择一个值 q。q 转换为 p（按 G 或 N 视情况而定）如果有任何这样的值可以做到；否则 q 未指定。
[注 5：如果 q 是转换任何 path 的结果，则它是转换 p 的结果。——注结束]

# 29.11.6.3.2 类型和编码转换 [fs.path.type.cvt]

1 普通字符字符串的原生编码是路径名（29.11.6）的操作系统相关当前编码。宽字符字符串的原生编码是实现定义的执行宽字符集编码（5.3）。

2 对于接受表示路径的字符序列的成员函数参数以及返回字符串的成员函数，如果参数或返回值的值类型与 path::value_type 不同，则执行值类型和编码转换。对于参数或返回值，转换方法和要转换到的编码由其值类型决定：

+   (2.1) — char：编码为原生普通编码。转换方法，如有，取决于操作系统。
+   [注 1：对于基于 POSIX 的操作系统 path::value_type 为 char，因此不执行来自 char 值类型参数或到 char 值类型返回值的转换。对于基于 Windows 的操作系统，原生普通编码由调用 Windows API 函数确定。——注结束]
+   [注 2：这导致的行为与使用普通字符字符串标识路径执行文件操作的其他 C 和 C++ 标准库函数相同。改变此行为会令人惊讶且容易出错。——注结束]

+   (2.2) — wchar_t：编码为原生宽编码。转换方法未指定。
+   [注 3：对于基于 Windows 的操作系统 path::value_type 为 wchar_t，因此不执行来自 wchar_t 值类型参数或到 wchar_t 值类型返回值的转换。——注结束]

+   (2.3) — char8_t：编码为 UTF-8。转换方法未指定。

+   (2.4) — char16_t：编码为 UTF-16。转换方法未指定。

+   (2.5) — char32_t：编码为 UTF-32。转换方法未指定。

3 如果目标编码对源字符没有表示，则转换后的字符，如有，未指定。实现不应修改已为 path::value_type 类型的成员函数参数。

# 29.11.6.4 要求 [fs.path.req]

1 除要求（29.11.3）外，名为 Source 的函数模板参数应为以下之一：

+   (1.1) — basic_string<EcharT, traits, Allocator>。函数参数 const Source& source 应具有有效范围 [source.begin(), source.end())。

+   (1.2) — basic_string_view<EcharT, traits>。函数参数 const Source& source 应具有有效范围 [source.begin(), source.end())。

+   (1.3) — 满足 Cpp17InputIterator 要求的迭代 NTCTS 的类型。值类型应为编码字符类型。函数参数 const Source& source 应具有有效范围 [source, end)，其中 end 是元素值等于 iterator_traits<Source>::value_type() 的第一个迭代器值。

+   (1.4) — 在数组到指针衰变后得到指向 NTCTS 起始的指针的字符数组。值类型应为编码字符类型。函数参数 const Source& source 应具有有效范围 [source, end)，其中 end 是元素值等于 iterator_traits<decay_t<Source>>::value_type() 的第一个迭代器值。

2 接受名为 Source 的模板参数的函数除非 Source 表示的类型不同于 path，且满足以下条件之一，否则不应参与重载决议

+   (2.1) — Source 是 basic_string 或 basic_string_view 的特化，或

# ISO/IEC 14882:2020(E)

(2.2) — 限定符 id iterator_traits<decay_t<Source>>::value_type 有效且表示可能是 const 的编码字符类型（13.10.3）。

> 3 [注 1：参见路径转换（29.11.6.3）了解上述值类型及其编码如何转换为 path::value_type 及其编码。——注结束]

4 类型为 Source 的参数不应为 null 指针。

# 29.11.6.5 成员 [fs.path.member]

# 29.11.6.5.1 构造函数 [fs.path.construct]

```
path() noexcept;
```

1 后置条件：empty() == true。

```
path(const path& p);
path(path&& p) noexcept;
```

2 效果：构造一个 path 类对象，其原生和通用格式中的路径名分别与 p 的原始值相同。在第二种形式中，p 被置于有效但未指定的状态。

```
path(string_type&& source, format fmt = auto_format);
```

3 效果：构造一个 path 类对象，其源的检测格式中的路径名具有源的原始值（29.11.6.3.1），在需要时转换格式（29.11.6.3.1）。source 被置于有效但未指定的状态。

```
template<class Source>
  path(const Source& source, format fmt = auto_format);
template<class InputIterator>
  path(InputIterator first, InputIterator last, format fmt = auto_format);
```

4 效果：令 s 为 source 的有效范围（29.11.6.4）或范围 [first, last)，在需要时转换编码（29.11.6.3）。找到 s 的检测格式（29.11.6.3.1）并构造一个 path 类对象，其该格式中的路径名为 s。

```
template<class Source>
  path(const Source& source, const locale& loc, format fmt = auto_format);
template<class InputIterator>
  path(InputIterator first, InputIterator last, const locale& loc, format fmt = auto_format);
```

5 强制要求：Source 和 InputIterator 的值类型为 char。

6 效果：令 s 为 source 的有效范围或范围 [first, last)，在执行以下编码转换后：

+   (6.1) — 如果 value_type 为 wchar_t，则使用 loc 的 codecvt<wchar_t, char, mbstate_t> 方面转换为原生宽编码（29.11.6.3.2）。
+   (6.2) — 否则使用 loc 的 codecvt<wchar_t, char, mbstate_t> 方面执行一次转换，然后执行第二次转换到当前普通编码。

7 找到 s 的检测格式（29.11.6.3.1）并构造一个 path 类对象，其该格式中的路径名为 s。

> [示例 1：要从数据库读取一个编码为 ISO/IEC 8859-1 的字符串，并用于创建目录：

```
namespace fs = std::filesystem;
std::string latin1_string = read_latin1_data();
codecvt_8859_1<wchar_t> latin1_facet;
std::locale latin1_locale(std::locale(), latin1_facet);
fs::create_directory(fs::path(latin1_string, latin1_locale));
```

对于基于 POSIX 的操作系统，path 是首先使用 latin1_facet 将 ISO/IEC 8859-1 编码的 latin1_string 转换为原生宽编码（29.11.6.3.2）中的宽字符字符串构建的。然后将得到的宽字符串转换为当前原生普通编码中的普通字符路径名字符串。如果原生宽编码为 UTF-16 或 UTF-32，且当前原生普通编码为 UTF-8，则 ISO/IEC 8859-1 字符集中的所有字符都将被转换为其 Unicode 表示，但对于其他原生普通编码，一些字符可能没有表示。

