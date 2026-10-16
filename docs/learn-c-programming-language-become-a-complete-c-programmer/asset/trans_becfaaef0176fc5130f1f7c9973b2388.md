
原始字符串字面量使用 `R"(ccc)"` 表示法来表示字符序列 ccc。开头的 R 用于区分原始字符串字面量与普通字符串字面量。圆括号的存在是为了允许（“无需转义的”）双引号。例如：

```
R"("quoted string")" // the string is "quoted string"
```

那么，我们如何把字符序列 `)"` 放进原始字符串字面量中呢？幸运的是，这是一个很少见的问题；`"(` 和 `)"` 只是默认的分隔符对。我们可以在 `"(...)"` 的 `(` 之前和 `)` 之后添加分隔符。例如：

```
R"***("quoted string containing the usual terminator (")")***"
// "quoted string containing the usual terminator (")"
```

`)` 之后的字符序列必须与 `(` 之前的字符序列完全相同。这样我们就能处理（几乎）任意复杂的模式。

除非你使用正则表达式，否则原始字符串字面量可能只是一种新奇特性（而且还要多学一样东西）。但正则表达式非常有用且应用广泛。来看一个现实世界中的例子：

```
"('(?:[^\\]|\.)*|' (?:[^\\]|\.)*')" // Are the five backslashes correct or not?
```

面对这样的例子，即使是专家也容易感到困惑，而原始字符串字面量正好能帮上大忙。

与非原始字符串字面量不同，原始字符串字面量可以包含换行符。例如：

```
string counts {R"(1
22
333)"};
```

等价于

```
string x {"1\n22\n333"};
```

## 7.3.2.2 更大的字符集

带有前缀 L 的字符串（如 `L"angst"`）是宽字符字符串（§6.2.3），其类型为 `const wchar_t[]`。类似地，带有前缀 `LR` 的字符串（如 `LR"(angst)"`）是类型为 `const wchar_t[]` 的宽字符原始字符串（§7.3.2.1）。这种字符串以 `L'\0'` 字符结尾。

## 第 7.3.2.2 节 更大的字符集（第 179 页）

有六种支持 Unicode 的字符字面量（Unicode 字面量）。这听起来有点过多，但 Unicode 有三种主要编码：UTF-8、UTF-16 和 UTF-32。对于这三种编码中的每一种，都同时支持原始字符串和“普通”字符串。所有三种 UTF 编码都支持全部 Unicode 字符，因此使用哪一种取决于你需要适配的系统。基本上，所有互联网应用（例如浏览器和电子邮件）都依赖其中一种或多种编码。

UTF-8 是一种可变宽度编码：常见字符占 1 字节，较少使用的字符（按某种使用频率估计）占 2 字节，更罕见的字符占 3 或 4 字节。特别是，ASCII 字符在 UTF-8 中占 1 字节，其编码（整数值）与 ASCII 相同。各种拉丁字母、希腊字母、西里尔字母、希伯来字母、阿拉伯字母等等都占 2 字节。

UTF-8 字符串以 `'\0'` 结尾，UTF-16 字符串以 `u'\0'` 结尾，UTF-32 字符串以 `U'\0'` 结尾。我们可以用多种方式表示一个普通的英文字符串。考虑一个使用反斜杠作为分隔符的文件名：

```
“folder\ file” // implementation character set string
R”(folder\file)” // implementation character rawset string
u8”folder\file” // UTF-8 string
u8R”(folder\file)” // UTF-8 rawstring
u”folder\file” // UTF-16 string
uR”(folder\file)” // UTF-16 rawstring
U”folder\file” // UTF-32 string
UR”(folder\file)” // UTF-32 rawstring
```

如果打印出来，这些字符串看起来都一样；但除了“普通”字符串和 UTF-8 字符串之外，它们的内部表示很可能不同。

显然，Unicode 字符串的真正用途是能够把 Unicode 字符放入其中。例如：

```
u8”The official vowels in Danish are: a, e, i, o, u, \u00E6, \u00F8, \u00E5 and y.”
```

适当地打印该字符串，你会得到：

```
The official vowels in Danish are: a, e, i, o, u, æ, ø, å and y.
```

`\u` 后面的十六进制数是一个 Unicode 码点（§iso.2.14.3）[Unicode,1996]。这样的码点与所使用的编码无关；实际上，它在不同编码中会有不同的表示（字节中的位模式）。例如，`u'\u0430'`（西里尔小写字母“а”）在 UTF-8 中是 2 字节十六进制值 D0B0，在 UTF-16 中是 2 字节十六进制值 0430，在 UTF-32 中是 4 字节十六进制值 00000430。这些十六进制值被称为通用字符名称。

u 和 R 的顺序以及它们的大小写是有讲究的：`RU` 和 `Ur` 不是有效的字符串前缀。

## 7.4 指向数组的指针

在 C++ 中，指针和数组关系密切。数组名可以用作指向其首元素的指针。例如：

```
int v[] = { 1, 2, 3, 4 };
int* p1 = v; // pointer to initial element (implicit conversion) int* p2 = &v[0]; // pointer to initial element
int* p3 = v+4; // pointer to one-beyond-last element
```

或图示如下：

```
p1 p2 p3
v: 1 2 3 4
```

取数组末尾之后一个元素的指针是保证可行的。这对许多算法（§4.5、§33.1）很重要。然而，由于这样的指针实际上并不指向数组中的元素，因此不能用于读取或写入。取首元素之前的元素地址，或取最后一个元素之后（one-past-the-last）的地址，结果是未定义的，应当避免。例如：

```
int* p4 = v-1; // before the beginning, undefined: don’t do it
int* p5 = v+7; // beyond the end, undefined: don’t do it
```

在 C 风格的代码中，数组名到指向其首元素的指针的隐式转换被广泛用于函数调用。例如：

```
extern "C" int strlen(const char*); // from <string.h>
void f() {
char v[] = "Annemarie";
char*p=v; // implicit conversion of char[] to char*
strlen(p);
strlen(v); // implicit conversion of char[] to char*
v = p; // error :cannot assign to array
}
```

两次调用传递给标准库函数 `strlen()` 的值是相同的。问题在于无法避免这种隐式转换。换句话说，无法声明一个函数，使函数调用时数组 v 被复制。幸运的是，不存在从指针到数组的隐式或显式转换。

数组参数到指针的隐式转换意味着被调函数无法得知数组的大小。然而，被调函数必须以某种方式确定大小，才能执行有意义的操作。与其它接受字符指针的 C 标准库函数一样，`strlen()` 依靠零表示字符串结束；`strlen(p)` 返回直到终止符 0（不含终止符）为止的字符数。这些都是相当底层的操作。标准库中的 `vector`（§4.4.1、§13.6、§31.4）、`array`（§8.2.4、§34.2.1）和 `string`（§4.2）没有这个问题。这些库类型通过 `size()` 给出元素个数，而不必每次都去数元素。

### 7.4.1 遍历数组

高效而优雅地访问数组（以及类似的数据结构）是许多算法的关键（见 §4.5、第 32 章）。访问可以通过指向数组的指针加下标实现，也可以通过指向元素的指针实现。例如：

```
void fi(char v[])
{
for (int i = 0; v[i]!=0; ++i) use(v[i]);
}
void fp(char v[]) {
for (char*p=v; *p!=0; ++p)
use(*p);
}
```

前缀 `*` 运算符对指针进行解引用，因此 `*p` 是 `p` 指向的字符；`++` 使指针递增，使其指向数组的下一个元素。

没有内在的理由认为某个版本会比另一个版本更快。使用现代编译器，两个示例应该（而且通常确实）生成相同的代码。程序员可以根据逻辑和审美上的理由在这两个版本之间进行选择。

对内置数组进行下标操作是根据指针运算 `+` 和 `*` 定义的。对于每个内置数组 `a` 以及 `a` 范围内的整数 `j`，都有：

```
a[j] == *(&a[0]+j) == *(a+j) == *(j+a) == j[a]
```

人们通常会很惊讶地发现 `a[j]==j[a]`。例如，`3["Texas"]=="Texas"[3]=='a'`。这种小聪明在生产代码中没有立足之地。这些等价关系非常底层，不适用于标准库容器（如 `array` 和 `vector`）。

对指针应用算术运算符 `+`、`-`、`++` 或 `--` 的结果取决于所指向对象的类型。当对类型 `T*` 的指针 `p` 应用算术运算符时，`p` 被假定指向 `T` 类型对象数组中的某个元素；`p+1` 指向该数组的下一个元素，`p-1` 指向前一个元素。这意味着 `p+1` 的整数值比 `p` 的整数值大 `sizeof(T)`。例如：

```
template<typename T>
int byte_diff(T* p, T* q)
{
return reinterpret_cast<char*>(q)-reinterpret_cast<char*>(p); }
```

```
void diff_test() {
int vi[10];
short vs[10]; cout << vi << ' ' << &vi[1] << ' ' << &vi[1]-&vi[0] << ' ' <<
byte_diff(&vi[0],&vi[1]) << '\n'; cout << vs << ' ' << &vs[1] << ' ' << &vs[1]-&vs[0]
<< ' ' << byte_diff(&vs[0],&vs[1]) << '\n';
}
```

输出为：

```
0x7fffaef0 0x7fffaef4 1 4
0x7fffaedc 0x7fffaede 1 2
```

指针值是以默认的十六进制表示法打印的。这表明在我的实现中，`sizeof(short)` 为 2，`sizeof(int)` 为 4。

指针相减只有在两个指针都指向同一数组的元素时才有定义（尽管语言没有快速的方法来确保这一点）。当从另一个指针 `q` 中减去指针 `p` 得到 `q-p` 时，结果是序列 `[p:q)` 中数组元素的个数（一个整数）。可以将整数加到指针上，也可以从指针中减去整数；两种情况下结果都是一个指针值。如果该值不指向与原指针同一个数组中的某个元素，也不是该数组的尾后位置，那么使用该值的结果是未定义的。例如：

```
void f()
{
int v1[10]; int v2[10];
int i1 = &v1[5]-&v1[3]; // i1 = 2
int i2 = &v1[5]-&v2[3]; // result undefined
```
