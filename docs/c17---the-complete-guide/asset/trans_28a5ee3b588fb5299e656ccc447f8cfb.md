
成员模板 string<>() 可用于转换成特殊的字符串类型，例如不区分大小写的字符串类型：

```
struct ignoreCaseTraits : public std::char_traits<char> {
    // case-insensitively compare two characters:
    static bool eq(const char& c1, const char& c2) {
        return std::toupper(c1) == std::toupper(c2);
    }
    static bool lt(const char& c1, const char& c2) {
        return std::toupper(c1) < std::toupper(c2);
    }
    // compare up to n characters of s1 and s2:
    static int compare(const char* s1, const char* s2, std::size_t n);
    // search character c in s:
    static const char* find(const char* s, std::size_t n, const char& c);
};
```

```
// define a special type for such strings:
using icstring = std::basic_string<char, ignoreCaseTraits>;
```

```
std::filesystem::path p{"/dir\\subdir/subsubdir\\./\\"};
icstring s2 = p.string<char,ignoreCaseTraits>();
```

另请注意，不应该使用同样提供的 c_str() 函数，因为它会转换为原生字符串格式，该格式可能是 wchar_t，因此，例如要将其写入流时，你必须使用 std::wcout 而不是 std::cout。

## 20.3.4 原生格式与通用格式之间的转换

“原生格式与通用格式之间的转换”表列出了可用于在通用路径格式与实际平台的实现特定格式之间进行转换的操作。

在基于 POSIX 的系统上，这些函数应该无效，因为原生路径格式与通用路径格式没有区别。在其他平台上调用这些函数可能会产生影响：

- generic...() 路径函数会按通用格式返回转换为相应字符串格式的路径。
- native() 使用原生字符串编码返回路径，该编码由类型 std::filesystem::path::string_type 定义。在 Windows 下，该类型是 std::wstring，这意味着你必须使用 std::wcout 而不是 std::cout 直接将其写入标准输出流。新的重载允许我们将原生字符串传给文件流的新重载。
- c_str() 做同样的事，但返回以空字符结尾的字符序列。注意，使用此函数也是不可移植的，因为在 Windows 上使用 std::cout 打印该序列不会产生正确输出。你必须使用 std::wcout。
- make_preferred() 用原生目录分隔符替换除根名称以外的任何目录分隔符。注意，这是唯一会修改被调用路径的函数。因此，严格来说，此函数属于下一节“修改路径的函数”，但由于它涉及原生格式的转换，因此也列在这里。

| 调用 | 效果 |
|---|---|
| p.generic_string() | 以通用 std::string 返回路径 |
| p.generic_wstring() | 以通用 std::wstring 返回路径 |
| p.generic_u8string() | 以通用 std::u8string 返回路径 |
| p.generic_u16string() | 以通用 std::u16string 返回路径 |
| p.generic_u32string() | 以通用 std::u32string 返回路径 |
| p.generic_string<...>() | 以通用 std::basic_string<...> 返回路径 |
| p.native() | 以 path::string_type 类型的原生格式返回路径 |
| conversionToNativeString | 隐式转换为原生字符串类型 |
| p.c_str() | 以原生字符串格式返回路径的字符序列 |
| p.make_preferred() | 就地用原生格式替换 p 中的目录分隔符，并返回修改后的 p |

*表20.6 原生格式与通用格式之间的转换*

例如，在 Windows 上，以下代码：

```
std::filesystem::path p{"/dir\\subdir/subsubdir\\./\\"};
std::cout << "p:" << p << '\n';
std::cout << "string():" << p.string() << '\n';
std::wcout << "wstring():" << p.wstring() << '\n';
std::cout << "lexically_normal(): " << p.lexically_normal() << '\n';
std::cout << "generic_string(): " << p.generic_string() << '\n';
std::wcout << "generic_wstring(): " << p.generic_wstring() << '\n';
// because it's Windows and the native string type is wstring:
std::wcout << "native():" << p.native() << '\n'; // Windows!
std::wcout << "c_str():" << p.c_str() << '\n';
std::cout << "make_preferred(): " << p.make_preferred() << '\n';
std::cout << "p:" << p << '\n';
```

输出如下：

```
p:          "/dir\\subdir/subsubdir\\./\\"
string():   /dir\subdir/subsubdir\./\
wstring():  /dir\subdir/subsubdir\./\
lexically_normal(): "\\dir\\subdir\\subsubdir\\"
generic_string():  /dir/subdir/subsubdir//./
generic_wstring(): /dir/subdir/subsubdir//./
native():   /dir\subdir/subsubdir\./\
c_str():    /dir\subdir/subsubdir\./\
make_preferred():  "\\dir\\subdir\\subsubdir\\\...\\"
p:          "\\dir\\subdir\\subsubdir\\\...\\"
```

再次注意：

- 原生字符串类型并不可移植。在 Windows 上它是 `wstring`，在基于 POSIX 的系统上它是 `string`，这意味着你必须使用 `cout` 而不是 `wcout` 打印 `native()` 和 `c_str()` 的结果。只有 `wstring()` 和 `generic_wstring()` 的返回值使用 `wcout` 才是可移植的。
- 只有调用 `make_preferred()` 会修改被调用的路径。所有其他调用都不会影响 p。

## 20.3.5 路径修改

表 *路径修改* 列出了允许我们直接修改路径的操作。

| 调用 | 效果 |
|---|---|
| p = p2 | 赋值一个新路径 |
| p = sv | 将字符串（视图）赋值作为新路径 |
| p.assign(p2) | 赋值一个新路径 |
| p.assign(sv) | 将字符串（视图）赋值作为新路径 |
| p.assign(beg, end) | 将 beg 到 end 范围内的元素赋值给路径 |
| p1 / p2 | 返回将 p2 作为 p1 的子路径追加后得到的路径 |
| p /= sub | 将 sub 作为子路径追加到路径 p |
| p.append(sub) | 将 sub 作为子路径追加到路径 p |
| p.append(beg, end) | 将 beg 到 end 范围内的元素作为子路径追加到路径 p |
| p += str | 将 str 的字符追加到路径 p |
| p.concat(str) | 将 str 的字符追加到路径 p |
| p.concat(beg, end) | 将 beg 到 end 范围内的元素追加到路径 p |
| p.remove_filename() | 从路径中移除尾部的文件名 |
| p.replace_filename(repl) | 替换尾部的文件名（如果有） |
| p.replace_extension() | 移除任何尾部的文件扩展名 |
| p.replace_extension(repl) | 替换尾部的文件扩展名（如果有） |
| p.clear() | 将路径置空 |
| p.swap(p2) | 交换两个路径的值 |
| swap(p1, p2) | 交换两个路径的值 |
| p.make_preferred() | 用原生格式替换 p 中的目录分隔符并返回修改后的 p |

*表20.7 路径修改*

+= 和 concat() 只是向路径追加新字符，而 /、/= 和 append() 则添加一个以当前目录分隔符分隔的子路径：

```
std::filesystem::path p{"myfile"};
p += ".git";              //p:myfile.git
p /= ".git";              //p:myfile.git/.git
p.concat("1");            //p:myfile.git/git1
p.append("1");            //p:myfile.git/git1/1
```

```
std::cout << p << '\n';
std::cout << p / p << '\n';
```

在基于 POSIX 的系统上，输出为：

```
"myfile.git/.git1/1"
"myfile.git/.git1/1/myfile.git/.git1/1"
```

在 Windows 系统上，输出为：

```
"myfile.git\\.git1\\1"
"myfile.git\\.git1\\1\\myfile.git\\.git1\\1"
```

注意，追加绝对子路径意味着替换现有路径。例如，在以下操作之后：

```
namespace fs = std::filesystem;
auto p1 = fs::path("/usr") / "tmp";      // path is /usr/tmp or /usr\tmp
auto p2 = fs::path("/usr/") / "tmp";      // path is /usr/tmp
auto p3 = fs::path("/usr") / "/tmp";      // path is /tmp
auto p4 = fs::path("/usr/") / "/tmp";     // path is /tmp
```

我们有4个路径，分别指向两个不同的文件：

- p1 和 p2 相等，并指向文件 /usr/tmp（注意，在 Windows 上它们也相等，其中 p1 为 /usr\tmp）。
- p3 和 p4 相等，并指向文件 /tmp，因为追加的是绝对路径。

对于根元素，是否分配了新元素也很重要。例如，在 Windows 上，我们有：

```
auto p1 = fs::path("usr") / "C:/tmp";    // path is C:/tmp
auto p2 = fs::path("usr") / "C:";        // path is C:
auto p3 = fs::path("C:") / "";          // path is C:
auto p4 = fs::path("C:usr") / "/tmp";   // path is C:/tmp
auto p5 = fs::path("C:usr") / "C:tmp";  // path is C:usr\tmp
auto p6 = fs::path("C:usr") / "c:tmp";  // path is c:tmp
auto p7 = fs::path("C:usr") / "D:tmp";  // path is D:tmp
```

函数 make_preferred() 将路径内的目录分隔符转换为原生格式。例如：

```
std::filesystem::path p{"//server/dir//subdir///file.txt"};
p.make_preferred();
std::cout << p << '\n';
```

在基于 POSIX 的平台上的输出为：

```
//server/dir/subdir/file.txt
```

在 Windows 上，输出如下：

```
"\\\server\\dir\\\subdir\\\\file.txt"
```

注意，开头的根名称不会被修改，因为它必须由两个斜杠或反斜杠组成。还要注意，此函数无法在基于 POSIX 的系统上将反斜杠转换为斜杠，因为反斜杠不被识别为目录分隔符。

