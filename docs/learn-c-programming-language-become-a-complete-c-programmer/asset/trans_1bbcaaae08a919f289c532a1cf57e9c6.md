

characters can be written to output using *p++=c:

ostreambuf_iterator<C,Tr> (§iso.24.6.4) (continues) ostreambuf_iterator p {os}; p is an iterator for os.rdbuf(); noexcept ostreambuf_iterator p {psb}; p is an iterator for the istreambuf *psb; noexcept
Section 38.6.3.2 ostreambuf_iterator 1107
ostreambuf_iterator<C,Tr> (continued) (§iso.24.6.4)

p=c If !p.failed() call the streambuf’s sputc(c)
*p Do nothing
++p Do nothing
p++ Do nothing
p.failed() Has a sputc() on p’s streambuf reached eof? noexcept

## 38.7 Advice

- [1] 为具有有意义文本表示的值的用户定义类型定义 << 和 >>；§38.1, §38.4.1, §38.4.2。
- [2] 使用 cout 进行正常输出，使用 cerr 进行错误输出；§38.1。
- [3] 有用于普通字符和宽字符的 iostreams，并且你可以为任何类型的字符定义 iostream；§38.1。
- [4] 有用于标准 I/O 流、文件和字符串的标准 iostreams；§38.2。
- [5] 不要尝试复制文件流；§38.2.1。
- [6] 二进制 I/O 是系统相关的；§38.2.1。
- [7] 在使用文件流之前，记得检查文件流是否已附加到文件；§38.2.1。
- [8] 优先使用 ifstreams 和 ofstreams 而不是通用的 fstream；§38.2.1。
- [9] 使用 stringstreams 进行内存中的格式化；§38.2.2。
- [10] 使用异常来捕获罕见的 bad() I/O 错误；§38.3。
- [11] 使用流状态 fail 来处理可能可恢复的 I/O 错误；§38.3。
- [12] 你不需要修改 istream 或 ostream 来添加新的 << 和 >> 运算符；§38.4.1。
- [13] 在实现 iostream 原始操作时，使用 sentry；§38.4.1。
- [14] 优先使用格式化输入而不是未格式化、低级的输入；§38.4.1。
- [15] 输入到字符串不会溢出；§38.4.1。
- [16] 使用 get()、getline() 和 read() 时要小心终止条件；§38.4.1。
- [17] 默认情况下 >> 会跳过空白字符；§38.4.1。
- [18] 你可以定义一个 <<（或一个 >>），使其基于其第二个操作数表现得像一个虚函数；§38.4.2.1。
- [19] 优先使用操纵符而不是状态标志来控制 I/O；§38.4.3。
- [20] 如果你想混合使用 C 风格和 iostream I/O，请使用 sync_with_stdio(true)；§38.4.4。
- [21] 使用 sync_with_stdio(false) 来优化 iostreams；§38.4.4。
- [22] 对用于交互式 I/O 的流进行绑定；§38.4.4。
- [23] 使用 imbue() 使 iostream 反映 locale 的“文化差异”；§38.4.4。
- [24] width() 规范仅适用于紧随其后的 I/O 操作；§38.4.5.1。
- [25] precision() 规范适用于所有后续的浮点输出操作；
§38.4.5.1。
- [26] 浮点格式规范（例如，科学计数法）适用于所有后续的浮点输出操作；§38.4.5.2。
- [27] 使用带参数的标准操纵符时，#include <iomanip>；§38.4.5.2。
- [28] 你几乎永远不需要 flush()；§38.4.5.2。
- [29] 除非出于美观原因，否则不要使用 endl；§38.4.5.2。
- [30] 如果 iostream 格式化变得过于繁琐，请编写自己的操纵符；§38.4.5.3。
- [31] 你可以通过定义一个简单的函数对象来实现（并提高效率）三元运算符的效果；§38.4.5.3。

## Locales

> *When in Rome, do as the Romans do.*  
> —Proverb

- 处理文化差异
- 类 `locale`
  命名 `locales`；比较 `strings`
- 类 `facet`
  
  在 `locale` 中访问 `facets`；一个简单的用户定义 `facet`；`locales` 和 `facets` 的用途
- 标准 `facets`
  `string` 比较；数字格式化；货币格式化；日期和时间格式化；字符分类；字符代码转换；消息
- 便捷接口
  字符分类；字符转换；字符串转换；缓冲区转换
- 建议

## 39.1 Handling Cultural Differences

A `locale` is an object that represents a set of cultural preferences, such as how strings are compared, the way numbers appear as human-readable output, and the way characters are represented in external storage. The notion of a *locale* is extensible so that a programmer can add new `facets` to a `locale` representing locale-specific entities not directly supported by the standard library, such as postal codes (zip codes) and phone numbers. The primary use of `locales` in the standard library is to control the appearance of information written to an `ostream` and the format of data read by an `istream`.

This chapter describes how to use a `locale`, how a `locale` is constructed out of `facets`, and how a `locale` affects an I/O stream.

The notion of a locale is not primarily a C++ notion. Most operating systems and application environments have a notion of locale. Such a notion is – in principle – shared among all programs on a system, independently of which programming language they are written in. Thus, the C++ standard-library notion of a locale can be seen as a standard and portable way for C++ programs to access information that has very different representations on different systems. Among other things, a C++ `locale` is an interface to system information that is represented in incompatible ways on different systems.

Consider writing a program that needs to be used in several countries. Writing a program in a style that allows that is often called *internationalization* (emphasizing the use of a program in many countries) or *localization* (emphasizing the adaptation of a program to local conditions). Many of the entities that a program manipulates will conventionally be displayed differently in those countries. We can handle this by writing our I/O routines to take this into account. For example:

```
`void print_date(const Date& d) // printing the appropriate format`
```
```
{
switch(where_am_I) { // user-defined style indicator
case DK: // e.g., 7. marts 1999
cout << d.day() << "." << dk_month[d.month()] << " " << d.year();
break;
case ISO: // e.g., 1999-3-7
cout << d.year() << "-" << d.month() << "/" << d.day();
break;
case US: // e.g., 3/7/1999
cout << d.month() << "/" << d.day() << "/" << d.year();
break;
//...
}
}
```

This style of code does the job. However, such code is ugly and hard to maintain. In particular, we have to use this style consistently to ensure that all output is properly adjusted to local conventions. If we want to add a new way of writing a date, we must modify the application code. Worse yet, writing dates is only one of many examples of cultural differences.

Consequently, the standard library provides an extensible way of handling cultural conventions. The iostream library relies on this framework to handle both built-in and user-defined types (§38.1). For example, consider a simple loop copying (Date,double) pairs that might represent a series of measurements or a set of transactions:

```
void cpy(istream& is, ostream& os) // copy(Date,double) stream
{
Date d;
double volume;

while (is >> d >> volume)
os << d << ' ' << volume << '\n';
}
```

Naturally, a real program would do something with the records and ideally also be a bit more careful about error handling.

How would we make this program read a file that conformed to French conventions (where a comma is the character used to represent the decimal point in a floating-point number; for example,

# Section 39.1 Handling Cultural Differences 1111

12,5 means twelve and a half) and write it according to American conventions? We can define locales and I/O operations so that cpy() can be used to convert between conventions:

```
void f(istream& fin, ostream& fout, istream& fin2, ostream& fout2)
{
fin.imbue(locale{"en_US.UTF-8"}); // AmericanEnglish
fout.imbue(locale{"fr_FR.UTF-8"}); // French
```
```
cpy(fin,fout); // read American English, write French // ...
fin2.imbue(locale{"fr_FR.UTF-8"}); // French
fout2.imbue(locale{"en_US.UTF-8"}); // American English
cpy(fin2,fout2); // read French, write American English // ...
}
```

Given these streams:

```
Apr 12, 1999 1000.3
Apr 13, 1999 345.45
Apr 14, 1999 9688.321
...
3 juillet 1950 10,3
3 juillet 1951 134,45
3 juillet 1952 67,9
...
```

this program would produce:

```
12 avril 1999 1000,3
13 avril 1999 345,45
14 avril 1999 9688,321
...
July 3, 1950 10.3
July 3, 1951 134.45
July 3, 1952 67.9
...
```

Much of the rest of this chapter is devoted to describing the mechanisms that make this possible and explaining how to use them. However, most programmers will have little reason to deal with the details of locales and will never explicitly manipulate a locale. At most, they will simply retrieve a standard locale and imbue a stream with it (§38.4.5.1).

- The concept of localization (internationalization) is simple. However, practical constraints make the design and implementation of locale quite intricate:
  
- [1] A locale encapsulates cultural conventions, such as the appearance of a date. Such conventions vary in many subtle and unsystematic ways. These conventions have nothing to do with programming languages, so a programming language cannot standardize them.
  
- [2] The concept of a locale must be extensible, because it is not possible to enumerate every cultural convention that is important to every C++ user.
  
- [3] A locale is used in operations (e.g., I/O and sorting) from which people demand run-time efficiency.
  
- [4] A locale must be invisible to the majority of programmers who want to benefit from facilities “doing the right thing” without having to know exactly what “the right thing” is or how it is achieved.
  
- [5] A locale must be available to designers of facilities that deal with culture-sensitive information beyond the scope of the standard.

The mechanisms provided to compose those locales and to make them trivial to use constitute a little programming language of their own.

