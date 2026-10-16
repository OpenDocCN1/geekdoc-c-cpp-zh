
```
protected:
~collate(); // note: protected destructor
virtual int do_compare(const C * b, const C* e, const C* b2, const C* e2) const;
virtual string_type do_transform(const C* b, const C* e) const; virtual long do_hash(const C* b, const C* e) const;
};
```

这定义了两个接口：

+   - 面向 facet 使用者的公共接口。
+   - 面向派生 facet 实现者的受保护接口。

构造函数参数指定是由 locale 还是由用户负责删除 facet。默认值 (0) 表示“由 locale 管理”（§39.3）。

所有标准库 facet 都有共同的结构，因此关于某个 facet 的要点可由以下关键函数概括：

```
collate<C> facet (§iso.22.4.4.1)
int compare(const C * b, const C* e, const C* b2, const C* e2) const; long hash(const C* b, const C* e) const;
string_type transform(const C* b, const C* e) const;
```

要定义 facet，可以以 collate 为模式。要从标准模式派生，只需定义关键函数的 do_* 版本即可提供 facet 的功能。这里列出函数的完整声明（而不是使用模式），以便为编写覆盖的 do_* 函数提供足够的信息。示例见 §39.4.1.1。

hash() 函数为其输入字符串计算一个哈希值。显然，这对于构建哈希表很有用。

## 39.4.1 节 字符串比较 1127

transform() 函数生成一个字符串，当它与另一个经 transform() 处理过的字符串比较时，会得到与直接比较这两个字符串相同的结果。即：

```
cf.compare(cf.transform(s),cf.transform(s2)) == cf.compare(s,s2)
```

transform() 的目的是允许对将一个字符串与许多其他字符串进行比较的代码进行优化。这在实现一组字符串中的搜索时很有用。

compare() 函数根据为特定 collate 所定义的规则执行基本字符串比较。它返回：

+   1 如果第一个字符串按字典序大于第二个字符串
+   0 如果两个字符串相同
+   −1 如果第二个字符串大于第一个字符串

例如：

```
void f(const string& s1, const string& s2, const collate<char>& cmp)
{
const char* cs1 {s1.data()}; // because compare() operates on char[]s const char* cs2 {s2.data()};

switch (cmp.compare(cs1,cs1+s1.size(),cs2,cs2+s2.size()) {
case 0: // identical strings according to cmp
// ...
break;
case -1: // s1 < s2
// ...
break;
case 1: // s1 > s2
// ...
break;
}
}
```

**collate** 的成员函数比较的是 **C** 的 [b:e) 范围，而不是 **basic_string** 或零结尾的 C 风格字符串。特别是，数值为 **0** 的 **C** 被当作普通字符而不是终止符。

标准库的 **string** 对 **locale** 不敏感。也就是说，它按照实现字符集的规则比较字符串（§6.2.3）。此外，标准 **string** 没有提供直接指定比较准则的方式（第 36 章）。要进行 **locale** 敏感的比较，可以使用 **collate** 的 **compare()**。例如：

```
void f(const string& s1, const string& s2, const string& name)
{
bool b {s1==s2}; // compare using implementation’s character set values

const char * s1b {s1.data()};
const char* s1e {s1.data()+s1.size()} const char* s2b {s2.data()};
const char* s2e {s2.data()+s2.size()}

// get startofdata // get end of data
using Col = collate<char>;
const Col& global {use_facet<Col>(locale{})}; int i0
{global.compare(s1b,s1e,s2b,s2e)};
// from the current global locale
const Col& my_coll {use_facet<Col>(locale{""})}; int i1 {my_coll.compare(s1b,s1e,s2b,s2e)};
// from mypreferred locale
const Col& n_coll {use_facet<Col>(locale{name})}; int i2
{n_coll.compare(s1b,s1e,s2b,s2e)}; }
// from a named locale
```

在符号形式上，通过 **locale** 的 **operator()**（§39.2.2）间接使用 **collate** 的 **compare()** 可能更方便。例如：

```
void f(const string& s1, const string& s2, const string& name)
{ int i0 = locale{}(s1,s2); int i1 = locale{""}(s1,s2); int i2 = locale{name}(s1,s2); // ...
}
```

// 使用当前全局 locale 进行比较 // 使用我偏好的 locale 进行比较 // 使用命名 locale 进行比较

不难想象 **i0**、**i1** 和 **i2** 不同的情况。考虑一下来自德语词典的这一串单词：

**Dialekt, Di¨at, dich, dichten, Dichtung**

按照惯例，只有名词大写，但排序不区分大小写。

区分大小写的德语排序会将所有以 **D** 开头的单词排在以 **d** 开头的单词之前：

**Dialekt, Di¨at, Dichtung, dich, dichten**

变音符号 ¨（即 **a** 上的变音）被视为“一种 **a**”，所以它排在 **c** 之前。然而，在大多数常见字符集中，**¨a** 的数值大于 **c** 的数值。因此，**int(’c’) < int(’¨a’)**，而基于数值的简单默认排序会得到：

**Dialekt, Dichtung, Di¨at, dich, dichten**

编写一个能按照字典顺序正确排列这个序列的比较函数，是一项有趣的练习。

### 39.4.1.1 命名 collate

**collate_byname** 是 **collate** 的一个版本，适用于由构造函数字符串参数指定的 **locale**：

```
template<class C>
class collate_byname : public collate<C> { // note: no id and no newfunctions
public:

typedef basic_string<C> string_type;
explicit collate_byname(const char*,size_t r = 0); // constructfrom named locale

explicit collate_byname(const string&, size_t r = 0);

protected:
~collate_byname(); // note: protected destructor

int do_compare(const C * b, const C* e, const C* b2, const C * e2) const override;
string_type do_transform(const C * b, const C * e) const override;
long do_hash(const C * b, const C * e) const override;
};
```

因此，**collate_byname** 可用于从程序执行环境中所命名的 **locale** 中取出一个 **collate**（§39.4）。在执行环境中存储 **facet** 的一种明显方式是将其作为文件中的数据。一个不太灵活的替代方案是将 **facet** 表示为程序文本，并将数据放在 **_byname** facet 中。

## 39.4.2 数值格式化

数值输出由 **num_put** facet 写入流缓冲区来完成（§38.6）。相反，数值输入由 **num_get** facet 从流缓冲区读取来完成。**num_put** 和 **num_get** 所使用的格式由称为 **numpunct** 的“数值标点” **facet** 定义。

### 39.4.2.1 数值标点

**numpunct** facet 定义了内建类型（如 **bool**、**int** 和 **double**）的 I/O 格式：

**numpunct<C> facet** (siso.22.4.6.3.1)

**C decimal_point() const**; 例如，`,`

**C thousands_sep() const**; 例如，`,`

**string grouping() const**; 例如，`""` 表示“无分组” **string_type truename() const**; 例如，**“true”**

**string_type falsename() const**; 例如，**“false”**

**grouping()** 返回的字符串中的字符被读取为一串小整数值。每个数字指定一组中的位数。字符 **0** 指定最右边的组（最低有效位），字符 **1** 指定其左侧的组，依此类推。因此，**“004\002\003”** 描述了一个像 **123–45–6789** 这样的数字（假设您使用 **‘_’** 作为分隔字符）。如有必要，分组模式中的最后一个数字会重复使用，因此 **“\003”** 等同于 **“\003\003\003”**。分组最常见的用途是让大数字更易读。**grouping()** 和 **thousands_sep()** 函数定义了整数以及浮点值整数部分的输入和输出格式。

我们可以通过从 **numpunct** 派生来定义新的标点风格。例如，我可以定义 facet **My_punct**，用空格将整数数字按三位分组，并用欧式逗号作为浮点值的“小数点”：

```
class My_punct : public numpunct<char> {
public:
  explicit My_punct(size_t r = 0) : numpunct<char>(r) { }

protected:
  char do_decimal_point() const override { return ','; } // comma
  char do_thousands_sep() const override { return '_'; } // underscore string
  do_grouping() const override { return "\003"; } // 3-digit groups
};

void f()
{
  cout << "style A: " << 12345678
       << " *** " << 1234567.8
       << " ***" << fixed << 1234567.8 << '\n';

  cout << defaultfloat; // reset floating for mat
  locale loc(locale(), new My_punct);
  cout.imbue(loc);
  cout << "style B: " << 12345678
       << " *** " << 1234567.8
       << " ***" << fixed << 1234567.8 << '\n';
}
```

这将产生：

**style A:** 12345678 *** 1.23457e+06 *** 1234567.800000

