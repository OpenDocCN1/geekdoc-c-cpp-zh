
实现字符集用于确定排序规则（§32.6、§31.2.2.1）。

## 39.3 facet 类

locale 是 facet 的集合。一个 facet 代表一个特定的文化方面，例如数字在输出时如何表示（num_put）、日期如何从输入中读取（time_get），以及字符如何存储在文件中（codecvt）。标准库中的 facet 列在 §39.4 中。

用户可以定义新的 facet，例如一个决定季节名称如何打印的 facet（§39.3.2）。

在程序中，facet 表示为从 std::locale::facet 派生的类对象。与所有其他 locale 工具一样，facet 定义在 `<locale>` 中：

第 39.3 节 facet 类 1119

```
class locale::facet {
protected:
explicit facet(size_t refs = 0);
virtual ~facet();
facet(const facet&) = delete;
void operator=(const facet&) = delete;
};
```

facet 类被设计为基类，没有公共函数。其构造函数是受保护的，以防止创建“普通 facet”对象；其析构函数是虚函数，以确保派生类对象被正确销毁。

facet 旨在通过存储在 locale 中的指针来管理。facet 构造函数参数为 0 表示当最后一个引用消失时，locale 应删除该 facet。相反，非零构造函数参数确保 locale 永远不会删除该 facet。非零参数用于罕见情况，即 facet 的生命周期由程序员直接控制，而不是通过 locale 间接控制。

每种 facet 接口都必须有一个单独的 id：

```
class locale::id {
public:
id();
void operator=(const id&) = delete;
id(const id&) = delete;
};
```

id 的预期用途是让用户为每个提供新 facet 接口的类定义一个类型为 id 的静态成员（例如，参见 §39.4.1）。locale 机制使用 id 来标识 facet（§39.2、§39.3.1）。在 locale 的一种常见实现中，id 被用作指向 facet 的指针向量的索引，从而实现了高效的 map<id,facet*>。

用于定义（派生）facet 的数据在派生类中定义。这意味着定义 facet 的程序员可以完全控制数据，并且可以使用任意数量的数据来实现 facet 所代表的概念。

facet 旨在不可变，因此用户定义的 facet 的所有成员函数都应定义为 const。

### 39.3.1 访问 locale 中的 facet

locale 的 facet 通过两个模板函数访问：

非成员 locale 函数（[siso.22.3.2](#)）

`f=use_facet<F>(loc)` 是 loc 中 facet F 的引用；如果 loc 没有 F，则抛出 bad_cast。

`has_facet<F>(loc)` loc 是否具有 facet F？noexcept

可以将这些函数视为在其 locale 参数中查找其模板参数 F。或者，可以将 use_facet 视为 locale 到特定 facet 的一种显式类型转换（cast）。这是可行的，因为 locale 只能拥有给定类型的一个 facet。例如：

```
void f(const locale& my_locale) {
  char c = use_facet<numpunct<char>>(my_locale).decimal_point() // use standard facet // …

  if (has_facet<Encrypt>(my_locale)) { // does my_locale contain an Encrypt facet? const Encrypt& f = use_facet<Encrypt>(my_locale); const Crypto c = f.get_crypto();
    // …
  }
  // …
}
// retrieveEncryptfacet // use Encrypt facet
```

标准 facet 保证对所有 locale 都可用（§39.4），因此我们不需要对标准 facet 使用 has_facet。

看待 facet::id 机制的一种方式是将其视为编译时多态的一种优化实现。dynamic_cast 可用于获得与 use_facet 产生的结果非常相似的结果。然而，专门的 use_facet 可以比通用 dynamic_cast 更高效地实现。

id 标识的是接口和行为，而不是类。也就是说，如果两个 facet 类具有完全相同的接口并在 locale 意义上实现相同的语义，那么它们应该由同一个 id 来标识。例如，collate<char> 和 collate_byname<char> 在 locale 中是可互换的，因此两者都由 collate<char>::id（§39.4.1）标识。

如果我们定义具有新接口的 facet——例如 f() 中的 Encrypt——我们必须定义相应的 id 来标识它（参见 §39.3.2 和 §39.4.1）。

### 39.3.2 一个简单的用户自定义 facet

标准库为文化差异最关键的部分提供了标准 facet，如字符集和数字的 I/O。为了将 facet 机制与广泛使用的类型的复杂性及其伴随的效率问题隔离开来，让我先为一个简单的用户自定义类型提供一个 facet：

```
enum Season { spring, summer, fall, winter }; // verysimple user-defined type
```

这里概述的 I/O 风格几乎无需修改即可用于大多数简单的用户自定义类型。

```
class Season_io : public locale::facet {
public:
Season_io(int i = 0) : locale::facet{i} { }
~Season_io() { } // to makeitpossible to destroySeason_io objects (§39.3)
virtual const string& to_str(Season x) const = 0; // stringrepresentation of x
virtual bool from_str(const string& s, Season& x) const = 0; // place Season for s in x
static locale::id id; // facet identifier object (§39.2, §39.3, §39.3.1) };
locale::id Season_io::id; // define the identifier object
```

为简单起见，此 facet 仅限于 char 字符串。

Season_io 类为所有 Season_io facet 提供了通用且抽象的接口。要为特定 locale 定义 Season 的 I/O 表示，我们从 Season_io 派生一个类，并恰当地定义 to_str() 和 from_str()。

Season 的输出很简单。如果流具有 Season_io facet，我们可以使用它将该值转换为字符串。如果没有，我们可以输出 Season 的 int 值：

```
ostream& operator<<(ostream& os, Season x)
{
locale loc {os.getloc()}; // extract the stream’slocale (§38.4.4)
if (has_facet<Season_io>(loc))
return os << use_facet<Season_io>(loc).to_str(x); // stringrepresentation
return os << static_cast<int>(x); // integer representation }
```

为了最大效率和灵活性，标准 facet 倾向于直接操作流缓冲区（§39.4.2.2、§39.4.2.3）。然而，对于像 Season 这样的简单用户自定义类型，无需降低到 streambuf 抽象级别。

与通常情况一样，输入比输出稍微复杂一些：

```
istream& operator>>(istream& is, Season& x)
{
const locale& loc {is.getloc()}; // extract the stream’slocale (§38.4.4)
if (has_facet<Season_io>(loc)) {
const Season_io& f {use_facet<Season_io>(loc)}; // get hold of the locale’sSeason_io facet
string buf;
if (!(is>>buf && f.from_str(buf,x))) is.setstate(ios_base::failbit); return is;
}
// read alphabetic representation
```

```
int i;
is >> i;
x = static_cast<Season>(i); return is;
}
```

```
// read numeric representation
```

错误处理很简单，遵循内置类型的错误处理风格。也就是说，如果输入字符串在所选 locale 中不代表 Season，则流进入失败状态。如果启用了异常，这意味着会抛出 ios_base::failure 异常（§38.3）。

下面是一个简单的测试程序：

```
int main()
// a trivial test
{
Season x;

// use the default locale (no Season_io facet) implies integer I/O: cin >> x;
cout << x << endl;

locale loc(locale(),new US_season_io{});
cout.imbue(loc); // use locale with Season_io facet cin.imbue(loc); // use locale with Season_io facet

cin >> x;
cout << x << endl;
}
```

给定输入

```
2
```

```
summer
```

该程序响应：

```
2
```

```
summer
```

要实现这一点，我们必须从 Season_io 派生一个类 US_season_io，并定义适当的季节字符串表示：

```
class US_season_io : public Season_io {
static const string seasons[];
public:
const string& to_str(Season) const;
bool from_str(const string&, Season&) const;

// note: no US_season_io::id };
```

```
const string US_season_io::seasons[] = {
"spring",
"summer",
"fall",

