

传递给带单个路径实参的`filesystem_error`构造函数。对于具有两个路径实参的函数，这些实参中的第一个应作为`path1`实参传递给`filesystem_error`构造函数，第二个应作为`path2`实参传递。`filesystem_error`构造函数的`error_code`实参按特定操作系统相关错误的适当方式进行设置。

-   (2.2) — 分配存储失败通过抛出异常来报告，如16.4.6.13所述。
-   (2.3) — 析构函数不抛出任何异常。

3 除非另有规定，否则具有`error_code&`类型实参的函数按如下方式处理错误：

-   (3.1) — 如果实现调用操作系统或其他底层API时产生的错误导致函数无法满足其规范，则按特定操作系统相关错误的适当方式设置`error_code&`实参。否则，对`error_code&`实参调用`clear()`。

## 29.11.6 类 path [fs.class.path]

### 29.11.6.1 概述 [fs.class.path.general]

1 类`path`的对象表示一个路径并包含一个路径名。此类对象仅涉及路径的词法和语法方面。该路径不一定存在于外部存储中，路径名也不一定对当前操作系统或特定文件系统有效。

> [注1：类`path`用于支持不同操作系统表示路径名所用的字符串类型之间的差异，并在必要时执行编码之间的转换。—— 注结束]

3 *路径*是标识文件在文件系统内位置的一系列元素。元素包括*根名称*opt、*根目录*opt，以及可选的*文件名*序列（29.11.6.2）。序列中元素的最大数量取决于操作系统（29.11.2.3）。

4 *绝对路径*是一种无需参考额外起始位置即可明确标识文件位置的路径。决定路径是否为绝对路径的元素取决于操作系统。*相对路径*是非绝对路径，因此只有在相对于隐含的起始位置进行解析时，才能明确标识文件的位置。决定路径是否为相对路径的元素取决于操作系统。

> [注2：路径名“.”和“..”是相对路径。—— 注结束]

5 *路径名*是表示路径名称的字符串。路径名的格式遵循通用路径名格式文法（29.11.6.2），或遵循宿主操作系统所接受的与操作系统相关的*本机路径名格式*。

6 *路径名解析*是一种依赖于操作系统的机制，用于将路径名解析为文件层次结构中的特定文件。可能存在多个路径名解析到同一文件。

> [示例1：POSIX在4.11节“路径名解析”中规定了该机制。—— 示例结束]

```
namespace std::filesystem {
  class path {
  public:
    using value_type  = see below;
    using string_type = basic_string<value_type>;
    static constexpr value_type preferred_separator = see below;

    // 29.11.8.1, enumeration format
    enum format;

    // 29.11.6.5.1, constructors and destructor
    path() noexcept;
    path(const path& p);
    path(path&& p) noexcept;
    path(string_type&& source, format fmt = auto_format);
    template<class Source>
      path(const Source& source, format fmt = auto_format);
    template<class InputIterator>
      path(InputIterator first, InputIterator last, format fmt = auto_format);
    template<class Source>
      path(const Source& source, const locale& loc, format fmt = auto_format);
    template<class InputIterator>
      path(InputIterator first, InputIterator last, const locale& loc, format fmt = auto_format);
    ~path();

    // 29.11.6.5.2, assignments
    path& operator=(const path& p);
    path& operator=(path&& p) noexcept;
    path& operator=(string_type&& source);
    path& assign(string_type&& source);
    template<class Source>
      path& operator=(const Source& source);
    template<class Source>
      path& assign(const Source& source);
    template<class InputIterator>
      path& assign(InputIterator first, InputIterator last);

    // 29.11.6.5.3, appends
    path& operator/=(const path& p);
    template<class Source>
      path& operator/=(const Source& source);
    template<class Source>
      path& append(const Source& source);
    template<class InputIterator>
      path& append(InputIterator first, InputIterator last);

    // 29.11.6.5.4, concatenation
    path& operator+=(const path& x);
    path& operator+=(const string_type& x);
    path& operator+=(basic_string_view<value_type> x);
    path& operator+=(const value_type* x);
    path& operator+=(value_type x);
    template<class Source>
      path& operator+=(const Source& x);
    template<class EcharT>
      path& operator+=(EcharT x);
    template<class Source>
      path& concat(const Source& x);
    template<class InputIterator>
      path& concat(InputIterator first, InputIterator last);

    // 29.11.6.5.5, modifiers
    void clear() noexcept;
    path& make_preferred();
    path& remove_filename();
    path& replace_filename(const path& replacement);
    path& replace_extension(const path& replacement = path());
    void swap(path& rhs) noexcept;

    // 29.11.6.8, non-member operators
    friend bool operator==(const path& lhs, const path& rhs) noexcept;
    friend strong_ordering operator<=>(const path& lhs, const path& rhs) noexcept;

    friend path operator/(const path& lhs, const path& rhs);

    // 29.11.6.5.6, native format observers
    const string_type& native() const noexcept;
    const value_type* c_str() const noexcept;
    operator string_type() const;

    template<class EcharT, class traits = char_traits<EcharT>,
             class Allocator = allocator<EcharT>>
    basic_string<EcharT, traits, Allocator>
    string(const Allocator& a = Allocator()) const;
    std::string string() const;
```

3 点（.）文件名被视作对当前目录的引用。双点（..）文件名被视作对父目录的引用。双点（..）文件名相对于*根目录*所指的是由实现定义的。特定文件名对于特定操作系统可能具有特殊含义。

4 *根名称*标识路径名解析的起始位置（29.11.6）。如果没有依赖于操作系统的*根名称*，则至少需要一个由实现定义的*根名称*。

> [*注2：*许多操作系统将两个*目录分隔符*字符开头的名称定义为*根名称*，用于标识网络或其他资源位置。某些操作系统将单个字母后跟冒号定义为驱动器说明符——即标识特定设备（如磁盘驱动器）的*根名称*。—— *注结束*]

5 如果*根名称*在其他方面存在歧义，则选择字符序列最长的可能项。

> [*注3：*在类POSIX操作系统上，不可能在没有*根目录*元素介入的情况下同时存在*根名称*和*相对路径*。—— *注结束*]

6 通用格式路径名的*规范化*意味着：

-   1. 如果路径为空，则停止。
-   2. 将*根名称*中的每个斜杠字符替换为*首选分隔符*。
-   3. 将每个*目录分隔符*替换为*首选分隔符*。

> [*注4：*通用路径名文法将*目录分隔符*定义为一个或多个斜杠以及*首选分隔符*。—— *注结束*]

-   4. 删除每个点（.）文件名以及紧随其后的任何*目录分隔符*。
-   5. 只要出现任何非双点（..）文件名后紧跟*目录分隔符*和双点（..）文件名的情况，就删除该非双点文件名、*目录分隔符*和双点文件名，以及紧随其后的任何*目录分隔符*。
-   6. 如果存在*根目录*，则删除所有双点（..）文件名及紧随其后的任何*目录分隔符*。

> [*注5：*这些双点（..）文件名试图引用不存在的父目录。—— *注结束*]

-   7. 如果最后一个文件名是双点（..），则删除末尾的任何*目录分隔符*。
-   8. 如果路径为空，则添加一个点（.）。

规范化的结果是*规范形式*的路径，该路径被称为*规范化*。

### 29.11.6.3 转换

#### 29.11.6.3.1 参数格式转换

> 1 [*注1：*本子条款描述的格式转换不应用于基于POSIX的操作系统，因为在这些系统上：
>
> -   (1.1) — 通用格式可作为本机路径被接受。
> -   (1.2) — 函数参数中无需区分本机格式和通用格式。
> -   (1.3) — 常规文件的路径与目录的路径共享相同的语法。
>
> —— *注结束*]

2 有些函数被定义为接受*检测格式*实参，这些实参是字符序列。检测格式实参使用通用格式（29.11.6.2）的路径名或本机格式（29.11.6）的路径名来表示路径。此类实参当且仅当与通用格式匹配且不被操作系统接受为本机路径时，才被视为采用通用格式。

> 3 [*注2：*某些操作系统没有一种明确的方法来区分本机格式实参和通用格式实参。这是有意为之，因为它简化了不需要消歧的操作系统的使用。对于需要消歧的操作系统，其实现被允许区分这两种格式。—— *注结束*]

4 路径名按需以依赖于操作系统的方式在通用格式与本机格式之间转换。从数学意义上，设G(n)和N(g)分别为实现中用于将本机格式转换为通用格式以及将通用格式转换为本机格式的函数。如果对于某个n有g=G(n)，则G(N(g))=g；如果对于某个g有n=N(g)，则N(G(n))=n。

> [*注3：*G和N都不必是可逆的。—— *注结束*]

5 如果本机格式要求常规文件的路径与目录的路径格式不同，则当路径的最后一个元素是*目录分隔符*时，该路径应被视为目录路径；否则，应被视为常规文件路径。

