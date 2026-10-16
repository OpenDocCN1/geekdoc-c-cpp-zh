

# 39.4.4.2 time_get

基本思想是 get_time 可以读取由 put_time 使用相同 strftime() 格式 (§43.6) 生成的内容：

```
class time_base {
public:
enum dateorder {
no_order, // meaning mdy
dmy, // meaning "%d%m%y"
mdy, // meaning "%m%d%y"
ymd, // meaning "%y%m%d"
ydm // meaning "%y%d%m"
};
};
```

```
template<class C, class In = istreambuf_iterator<C>>
class time_get : public locale::facet, public time_base {
public:
using char_type = C;
using iter_type = In;
// ...
}
```

除了根据格式读取外，还有用于检查 dateorder 以及读取日期和时间表示的特定部分的操作，例如 weekday 和 monthname：

第 39.4.4.2 节 time_get 1141

time_get<C,In> facet (§iso.22.4.5.1) 从 [b:e] 读取到 *pt

```
dateorder do_date_order() const;
In get_time(In b, In e, ios_base& ib, ios_base::iostate& err, tm* pt) const; In
get_date(In b, In e, ios_base& ib, ios_base::iostate& err, tm* pt) const; In
get_weekday(In b, In e, ios_base& ib, ios_base::iostate& err, tm* pt) const; In
get_monthname(In b, In e, ios_base& ib, ios_base::iostate& err, tm* pt) const; In
get_year(In b, In e, ios_base& ib, ios_base::iostate& err, tm* pt) const; In get(In b, In e, ios_base& ib, ios_base::iostate& err, tm* pt, char format, char mod) const; In
get(In b, In e, ios_base& ib, ios_base::iostate& err, tm* pt, char format) const; In
get(In b, In e, ios_base& ib, ios_base::iostate& err, tm* pt, C* fmtb, C* fmte) const;
```

一个 get_*() 函数从 [b:e] 读取到 *pt，从 b 获取其 locale，并在出错时设置 err。它返回指向 [b:e] 中第一个未读字符的迭代器。

调用 p=get(b,e,ib,err,pt,format,mod) 根据 strftime() 指定的格式字符 format 和修饰符字符 mod 进行读取。如果未指定 mod，则使用 mod==0。

调用 **get(b,e,ib,err,pt,fmtb,fmtb)** 使用作为字符串 [**fmtb:fmte**] 提供的 **strftime()** 格式。此重载以及具有默认修饰符的重载没有 **do_get()** 接口。相反，它们通过对第一个 **get()** 的 **do_get()** 调用来实现。

time 和 date **facets** 的明显用途是为 **Date** 类提供 **locale** 敏感的 I/O。考虑 §16.3 中的 **Date** 的一个变体：

```
class Date {
public:
    explicit Date(int d ={}, Month m ={}, int year ={});
    // …
    string to_string(const locale& = locale()) const;
};
```

```
istream& operator>>(istream& is, Date& d);
ostream& operator<<(ostream& os, Date d);
Date::to_string()
```

生成使用 **stringstream** (§38.2.2) 的 **locale()** 特定 **string**：

```
string Date::to_string(const locale& loc) const
{
    ostringstream os;
    os.imbue(loc);
    return os << *this;
}
```

给定 **to_string()**，输出运算符很简单：

```
ostream& operator<<(ostream& os, Date d)
{
    return os<<to_string(d,os.getloc());
}
```

输入运算符需要小心处理状态：

```
istream& operator>>(istream& is, Date& d)
{
    if (istream::sentry guard{is}) {
        ios_base::iostate err = goodbit;
        struct tm t;
        use_facet<time_get<char>>(is.getloc()).get_date(is,0,is,err,&t); // read into t
        if (!err) {
            Month m = static_cast<Month>(t.tm_mon+1);
            d = Date(t.tm_day,m,t.tm_year+1900);
        }
        is.setstate(err);
    }
    return is;
}
```

需要 **+1900**，因为年份 **1900** 是 **tm** 的零年 (§43.6)。提供了一个 **_byname** 版本 (§39.4, §39.4.1) 的 **messages**：

```
template<class C, class In = istreambuf_iterator<C>>
class time_get_byname : public time_get<C, In> {
// …
};
```

## 39.4.5 字符分类

从输入读取字符时，通常需要对其进行分类以理解正在读取的内容。例如，要读取一个数字，输入例程需要知道哪些字母是数字。同样，§10.2.2 显示了标准字符分类函数用于解析输入的用法。

自然地，字符的分类取决于所使用的字母表。因此，提供了一个 facet **ctype** 来表示 **locale** 中的字符分类。字符类由一个名为 **mask** 的枚举描述：

```
class ctype_base {
public:
enum mask {

space = 1, print = 1<<1, cntrl = 1<<2, upper = 1<<3, lower = 1<<4, alpha = 1<<5,
digit = 1<<6, punct = 1<<7, xdigit = 1<<8, blank = 1<<9; alnum=alpha|digit, // alphanumeric characters  graph=alnum|punct

};
};
```

```
// the actual values are implementation-defined // whitespace (in “C” locale: ' ', '\n', '\t', …) // printing characters
// control characters
// uppercase characters
// lowercase characters
// alphabetic characters
// decimal digits
// punctuation characters
// hexadecimal digits
// space and horizontal tab
```

```
template<class C>
class ctype : public locale::facet, public ctype_base {
public:

using char_type = C;
// …
};
```

此 **mask** 不依赖于特定字符类型。因此，此枚举被放置在（非模板）基类中。

显然，mask 反映了传统的 C 和 C++ 分类 (§36.2.1)。然而，对于不同的字符集，不同的字符值会落入不同的类。例如，对于 ASCII 字符集，整数值 125 表示字符 }，它是一个标点字符 (punct)。然而，在丹麦国家字符集中，125 表示元音 å，在丹麦 locale 中必须被分类为 alpha。

分类被称为“mask”，因为对于小型字符集，字符分类的传统高效实现是一个表中，每个条目保存表示分类的位。例如：

```
table['P'] == upper|alpha
table['a'] == lower|alpha|xdigit
table['1'] == digit|xdigit
table[' '] == space|blank
```

给定该实现，table[c]&m 为非零表示字符 c 是 m，否则为 0。ctype facet 定义如下：

```
ctype<C> facet (§iso.22.4.1.1)
```

```
bool is(mask m, C c) const;
const C* is(const C* b, const C* e, mask* v) const;
const C* scan_is(mask m, const C* b, const C* e) const; const C* scan_not(mask m, const C* b, const C* e) const; C toupper(C c) const;
const C* toupper(C* b, const C* e) const;
C tolower(C c) const;
const C* tolower(C* b, const C* e) const;
C widen(C c) const;
const char* widen(const char* b, const char* e, C* b2) const; char narrow(C c, char def) const;
const C* narrow(const C* b, const C* e, char def, char* b2) const;
```

调用 is(m,c) 测试字符 c 是否属于分类 m。例如：

```
int count_spaces(const string& s, const locale& loc)
{
const ctype<char>& ct = use_facet<ctype<char>>(loc); int i = 0;
for(auto p = s.begin(); p!=s.end(); ++p)
if (ct.is(ctype_base::space,*p)) // whitespace as defined by ct
++i;
return i;
}
```

请注意，也可以使用 is() 检查字符是否属于多个分类之一。例如：

```
ct.is(ctype_base::space|ctype_base::punct,c); // is c whitespace or punctuation in ct?
```

调用 is(b,e,v) 确定 [b:e) 中每个字符的分类并将其放在数组 v 的对应位置。

调用 scan_is(m,b,e) 返回 [b:e) 中第一个是 m 的字符的指针。如果没有字符被分类为 m，则返回 e。正如标准 facet 一样，公共

`c == narrow(widen(c),0)` // *not guaranteed*

这在由 `c` 表示的字符在“较小的字符集”中只有一个表示时成立。然而，这并不能保证。如果 `char` 表示的字符不是较大字符集 (`C`) 表示字符的子集，我们应该期望出现异常，并且在以通用方式处理字符的代码中可能出现问题。

同样，对于来自较大字符集的字符 `ch`，我们可能期望：

`widen(narrow(ch,def)) == ch || widen(narrow(ch,def)) == widen(def)` // *not guaranteed*

然而，即使这通常是这种情况，也不能保证字符在较大字符集中有多个值表示而在较小字符集中只有一个值表示的情况。例如，数字，如 `7`，通常在大型字符集中有几个单独的表示。其原因通常是大型字符集有几个常规字符集作为子集，并且来自较小集合的字符被复制以便于转换。

对于基本源字符集 (§6.1.2) 中的每个字符，都保证
`widen(narrow(ch_lit,0)) == ch_lit`

例如：
`widen(narrow('x',0)) == 'x'`

`narrow()` 和 `widen()` 函数在可能的情况下尊重字符分类。例如，如果 `is(alpha,c)`，则 `is(alpha,narrow(c,'a'))` 且 `is(alpha,widen(c))`，只要 `alpha` 是所用 locale 的有效 mask。

使用 `ctype` facet 的主要原因，以及特别使用 `narrow()` 和 `widen()` 函数，是能够编写对任何字符集进行 I/O 和字符串操作的通用代码，即使这种代码相对于字符集也是通用的。这意味着 `iostream` 实现严重依赖这些设施。通过依赖 `<iostream>` 和 `<string>`，用户可以避免对 `ctype` facet 的大多数直接使用。

提供了一个 `_byname` 版本 (§39.4, §39.4.1) 的 `ctype`：

```
template<class C>
class ctype_byname : public ctype<C> {
```

## 39.4.6 字符代码转换

有时，存储在文件中的字符的表示与主内存中这些相同字符的期望表示不同。例如，日文字符通常存储在文件中，其中指示符（“shifts”）指示给定字符序列属于四个常见字符集（汉字、片假名、平假名和罗马字）中的哪一个。这有点笨拙，因为每个字节的含义取决于其“shift 状态”，但它可以节省内存，因为只有汉字需要超过 1 字节的表示。在主内存中，这些字符在每个字符大小相同的多字节字符集中表示时更容易操作，例如 Unicode 字符。这些字符通常放在宽字符 (`wchar_t`; §6.2.3) 中。因此，`codecvt` facet 提供了一种在读取或写入时将字符从一种表示转换为另一种表示的机制。例如：

