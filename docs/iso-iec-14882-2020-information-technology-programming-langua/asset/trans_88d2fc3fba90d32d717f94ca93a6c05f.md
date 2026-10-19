

## 29.11.13.37 状态已知 [fs.op.status.known]

```
bool status_known(file_status s) noexcept;
```

返回：s.type() != file_type::none。

## 29.11.13.38 符号链接状态 [fs.op.symlink.status]

```
file_status symlink_status(const path& p);
file_status symlink_status(const path& p, error_code& ec) noexcept;
```

效果：与上面的 status() 相同，只是 p 的属性是使用 POSIX lstat() 获取 POSIX struct stat 的方式确定的。

令 prms 表示 (m & perms::mask) 的结果，其中 m 是将获得的 struct stat 的 st_mode 成员转换为类型 perms 时确定的。

返回：与上面的 status() 相同，只是如果属性指示符号链接，如同 POSIX S_ISLNK，则返回 file_status(file_type::symlink, prms)。带 ec 参数的签名如果发生错误则返回 file_status(file_type::none)。

否则，如果属性指示套接字，如同 POSIX S_ISSOCK，则返回 file_status(file_type::socket, prms)。

否则，如果属性指示实现定义的文​​件类型 (29.11.8.2)，则返回 file_status(file_type::A, prms)，其中 A 是实现定义文件类型的常量。

否则，返回 file_status(file_type::unknown, prms)。

说明：路径名解析在 p 命名符号链接时终止。

抛出：如 29.11.5 所述。

## 29.11.13.39 临时目录路径 [fs.op.temp.dir.path]

```
path temp_directory_path();
path temp_directory_path(error_code& ec);
```

令 p 为适合临时文件的未指定目录路径。

效果：如果 exists(p) 为 false 或 is_directory(p) 为 false，则报告错误 (29.11.5)。

返回：路径 p。带 ec 参数的签名如果发生错误则返回 path()。

抛出：如 29.11.5 所述。

[示例 1：对于基于 POSIX 的操作系统，实现可以返回在列表 TMPDIR、TMP、TEMP、TEMPDIR 中找到的第一个环境变量提供的路径，或如果均未找到，则返回 "/tmp"。
对于基于 Windows 的操作系统，实现可以返回 Windows GetTempPath API 函数报告的路径。——示例结束]

## 29.11.13.40 弱规范化 [fs.op.weakly.canonical]

```
path weakly_canonical(const path& p);
path weakly_canonical(const path& p, error_code& ec);
```

返回：p 在解析符号链接并结果规范化后 (29.11.6.2)。

效果：使用 status(p) 或 status(p, ec) 分别确定存在性，返回由 operator/= 组成的路径，该路径由调用 canonical() 时使用 p 的已存在的前导元素（如果有）组成的路径参数的结果，后跟 p 的不存在的元素（如果有）。对于第一种形式，canonical() 在不带 error_code 参数的情况下调用。对于第二种形式，canonical() 使用 ec 作为 error_code 参数调用，并在首次出现错误时返回 path()。

后置条件：返回的路径处于规范形式 (29.11.6.2)。

说明：如果在路径名解析过程中遇到符号链接，则路径名解析会继续使用符号链接的内容。

*说明：* 实现应避免不必要的规范化，例如当 *canonical* 已对 p 的全部内容调用时。

*抛出：* 如 [29.11.5](#) 所述。

## 29.12 C 库文件

### 29.12.1 头文件 `<cstdio>` 概要

```
namespace std {
    using size_t = see 17.2.4;
    using FILE = see below;
    using fpos_t = see below;
}

#define NULL see 17.2.3
#define _IOFBF see below
#define _IOLBF see below
#define _IONBF see below
#define BUFSIZ see below
#define EOF see below
#define FOPEN_MAX see below
#define FILENAME_MAX see below
#define L_tmpnam see below
#define SEEK_CUR see below
#define SEEK_END see below
#define SEEK_SET see below
#define TMP_MAX see below
#define stderr see below
#define stdin see below
#define stdout see below

namespace std {
    int remove(const char* filename);
    int rename(const char* old_p, const char* new_p);
    FILE* tmpfile();
    char* tmpnam(char* s);
    int fclose(FILE* stream);
    int fflush(FILE* stream);
    FILE* fopen(const char* filename, const char* mode);
    FILE* freopen(const char* filename, const char* mode, FILE* stream);
    void setbuf(FILE* stream, char* buf);
    int setvbuf(FILE* stream, char* buf, int mode, size_t size);
    int fprintf(FILE* stream, const char* format, ...);
    int fscanf(FILE* stream, const char* format, ...);
    int printf(const char* format, ...);
    int scanf(const char* format, ...);
    int snprintf(char* s, size_t n, const char* format, ...);
    int sprintf(char* s, const char* format, ...);
    int sscanf(const char* s, const char* format, ...);
    int vfprintf(FILE* stream, const char* format, va_list arg);
    int vfscanf(FILE* stream, const char* format, va_list arg);
    int vprintf(const char* format, va_list arg);
    int vscanf(const char* format, va_list arg);
    int vsnprintf(char* s, size_t n, const char* format, va_list arg);
    int vsprintf(char* s, const char* format, va_list arg);
    int vsscanf(const char* s, const char* format, va_list arg);
    int fgetc(FILE* stream);
    char* fgets(char* s, int n, FILE* stream);
    int fputc(int c, FILE* stream);
    int fputs(const char* s, FILE* stream);
    int getc(FILE* stream);
    int getchar();
    int putc(int c, FILE* stream);
    int putchar(int c);
```

```
#define PRIxFASTN see below
#define PRIXFASTN see below
#define SCNdFASTN see below
#define SCNiFASTN see below
#define SCNoFASTN see below
#define SCNuFASTN see below
#define SCNxFASTN see below
#define PRIdMAX see below
#define PRIiMAX see below
#define PRIoMAX see below
#define PRIuMAX see below
#define PRIxMAX see below
#define PRIXMAX see below
#define SCNdMAX see below
#define SCNiMAX see below
#define SCNoMAX see below
#define SCNuMAX see below
#define SCNxMAX see below
#define PRIdPTR see below
#define PRIiPTR see below
#define PRIoPTR see below
#define PRIuPTR see below
#define PRIxPTR see below
#define PRIXPTR see below
#define SCNdPTR see below
#define SCNiPTR see below
#define SCNoPTR see below
#define SCNuPTR see below
#define SCNxPTR see below
```

1 头文件 <cinttypes> 的内容和含义与 C 标准库头文件 <inttypes.h> 相同，但有以下更改：

- (1.1) — 头文件 <cinttypes> 包含头文件 <cstdint> (17.4.2) 而不是 <stdint.h>，并且

- (1.2) — 如果且仅如果类型 intmax_t 指定了扩展整数类型 (6.8.2)，则添加以下函数签名：
  - intmax_t abs(intmax_t);
  - imaxdiv_t div(intmax_t, intmax_t);
  其语义应与函数签名 intmax_t imaxabs(intmax_t) 和 imaxdiv_t imaxdiv(intmax_t, intmax_t) 相同。

另请参阅：ISO C 7.8

```
// 30.7, class template regex_traits
template<class charT> struct regex_traits;

// 30.8, class template basic_regex
template<class charT, class traits = regex_traits<charT>> class basic_regex;

using regex = basic_regex<char>;
using wregex = basic_regex<wchar_t>;

// 30.8.6, basic_regex swap
template<class charT, class traits>
  void swap(basic_regex<charT, traits>& e1, basic_regex<charT, traits>& e2);

// 30.9, class template sub_match
template<class BidirectionalIterator>
  class sub_match;

using csub_match = sub_match<const char*>;
using wcsub_match = sub_match<const wchar_t*>;
using ssub_match = sub_match<string::const_iterator>;
using wssub_match = sub_match<wstring::const_iterator>;

// 30.9.3, sub_match non-member operators
template<class BiIter>
  bool operator==(const sub_match<BiIter>& lhs, const sub_match<BiIter>& rhs);
template<class BiIter>
  auto operator<=>(const sub_match<BiIter>& lhs, const sub_match<BiIter>& rhs);

template<class BiIter, class ST, class SA>
  bool operator==(
    const sub_match<BiIter>& lhs,
    const basic_string<typename iterator_traits<BiIter>::value_type, ST, SA>& rhs);
template<class BiIter, class ST, class SA>
  auto operator<=>( 
    const sub_match<BiIter>& lhs,
    const basic_string<typename iterator_traits<BiIter>::value_type, ST, SA>& rhs);

template<class BiIter>
  bool operator==(const sub_match<BiIter>& lhs,
    const typename iterator_traits<BiIter>::value_type* rhs);
template<class BiIter>
  auto operator<=>(const sub_match<BiIter>& lhs,
    const typename iterator_traits<BiIter>::value_type* rhs);

template<class BiIter>
  bool operator==(const sub_match<BiIter>& lhs,
    const typename iterator_traits<BiIter>::value_type& rhs);
template<class BiIter>
  auto operator<=>(const sub_match<BiIter>& lhs,
    const typename iterator_traits<BiIter>::value_type& rhs);

template<class charT, class ST, class BiIter>
  basic_ostream<charT, ST>&
    operator<<(basic_ostream<charT, ST>& os, const sub_match<BiIter>& m);

// 30.10, class template match_results
template<class BidirectionalIterator,
    class Allocator = allocator<sub_match<BidirectionalIterator>>>
  class match_results;

using cmatch = match_results<const char*>;
using wcmatch = match_results<const wchar_t*>;
using smatch = match_results<string::const_iterator>;
using wsmatch = match_results<wstring::const_iterator>;
```

