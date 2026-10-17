
当然，假设你为 `Fruit` 定义了 `<<`。或者我们可以等价地写为：

```cpp
for (const auto& x : inventory)
    cout << x << '\n';
```

## 21.7 复制（Copying）

在 §21.2 中，我们认为 `find()` 是“最简单有用的算法”。自然，这一点可以争论。许多简单的算法是有用的 – 即使是一些写起来很琐碎的算法。当你可以使用他人编写并调试过的代码时，为什么要费心编写新代码呢，无论它有多简单？谈到简单性和实用性，`copy()` 给 `find()` 带来了强劲的竞争。STL 提供了三种复制版本：

| 复制操作 | 描述 |
| :--- | :--- |
| `copy(b,e,b2)` | 将 `b:e` 复制到 `b2:b2+(e-b)`。 |
| `unique_copy(b,e,b2)` | 将 `b:e` 复制到 `b2:b2+(e-b)`；抑制相邻复制。 |
| `copy_if(b,e,b2,p)` | 将 `b:e` 复制到 `b2:b2+(e-b)`，但仅复制满足谓词 `p` 的元素。 |

### 21.7.1 Copy

基本复制算法定义如下：

```cpp
template<typename In, typename Out>
// requires Input_iterator<In> && Output_iterator<Out>
Out copy(In first, In last, Out res)
{
    while (first!=last) {
        *res = *first;    // 复制元素
        ++res;
        ++first;
    }
    return res;
}
```

给定一对迭代器，`copy()` 将一个序列复制到由指向其第一个元素的迭代器指定的另一个序列中。例如：

```cpp
void f(vector<double>& vd, list<int>& li)
    // 将 int 列表的元素复制到 double 向量中
{
    if (vd.size() < li.size()) error("目标容器太小");
    copy(li.begin(), li.end(), vd.begin());
    // ...
}
```

注意 `copy()` 输入序列的类型可以与输出序列的类型不同。这是 STL 算法的一个有用的通用性：它们适用于所有类型的序列，而不对它们的实现做不必要的假设。我们记得检查输出序列是否有足够的空间来容纳我们放入的元素。检查这样的尺寸是程序员的工作。STL 算法针对最大通用性和最佳性能进行编程；它们（默认情况下）不执行范围检查或其他可能昂贵的测试来保护用户。有时，你会希望它们这样做，但当你需要检查时，可以像上面那样添加它。

### 21.7.2 流迭代器

你听过“复制到输出”和“从输入复制”这样的短语。这是一种漂亮且有用的思考某些形式 I/O 的方式，我们可以实际上使用 `copy()` 来做恰好这件事。

- 有开始和结束
- 我们可以使用 `++` 获取下一个元素
- 我们可以使用 `*` 获取当前元素的值

我们可以轻松地以这种方式表示输入和输出流。例如：

```cpp
ostream_iterator<string> oo{cout}; // 赋值给 *oo 就是写入 cout

*oo = "Hello, "; // 意味着 cout << "Hello, "
++oo; // “为下一个输出操作做准备”
*oo = "World!\n"; // 意味着 cout << "World!\n"
```

你可以想象这是如何实现。标准库提供 `ostream_iterator` 类型，工作方式如此；`ostream_iterator<T>` 是一个迭代器，你可以用它来写入类型 `T` 的值。

类似地，标准库提供类型 `istream_iterator<T>` 用于读取类型 `T` 的值：

```cpp
istream_iterator<string> ii{cin}; // 读取 *ii 就是从 cin 读取一个字符串

string s1 = *ii; // 意味着 cin>>s1
++ii; // “为下一个输入操作做准备”
string s2 = *ii; // 意味着 cin>>s2
```

使用 `ostream_iterator` 和 `istream_iterator`，我们可以将 `copy()` 用于我们的 I/O。例如，我们可以像这样制作一个“快速且粗糙”的词典：

```cpp
int main()
{
    string from, to;
    cin >> from >> to; // 获取源文件和目标文件名
    
    ifstream is {from}; // 打开输入流
    ofstream os {to}; // 打开输出流
    
    istream_iterator<string> ii (is); // 为流创建输入迭代器
    istream_iterator<string> eos; // 输入哨兵
    ostream_iterator<string> oo (os, "\n"); // 为流创建输出迭代器
    
    vector<string> b (ii, eos); // b 是从输入初始化的向量
    sort(b.begin(), b.end()); // 对缓冲区进行排序
    copy(b.begin(), b.end(), oo); // 将缓冲区复制到输出
}
```

迭代器 `eos` 是流迭代器对“输入结束”的表示。当一个 `istream` 达到输入结束（通常称为 `eof`）时，其 `istream_iterator` 将等于默认的 `istream_iterator`（这里称为 `eos`）。

请注意，我们使用一对迭代器初始化了 `vector`。作为容器的初始化器，迭代器对 `(a,b)` 意味着“将序列 `[a:b]` 读入容器”。自然，我们使用的迭代器对是 `(ii,eos)` —— 即输入的起始和结束。这让我们免于显式使用 `>>` 和 `push_back()`。我们强烈建议不要使用替代方案

```cpp
vector<string> b {max_size};     // 不要猜测输入量！
copy(ii,eos,b.begin());
```

那些试图猜测输入最大尺寸的人通常会发现他们低估了，由此产生的缓冲区溢出会给他们或他们的用户带来严重问题。这种溢出也是安全问题的来源。

## 试一试

首先，让按原样编写的程序运行起来，并用一个小文件进行测试，例如包含几百个单词的文件。然后，尝试那个*强烈*不推荐的版本，该版本会猜测输入的大小，并查看当输入缓冲区 `b` 溢出时会发生什么。请注意，最坏的情况是溢出在你的特定示例中并没有导致任何坏事，这会诱惑你把它发布给用户。

在我们的小程序中，我们读取单词，然后对它们进行排序。当时这似乎是一种显而易见的方式，但为什么我们要把单词放在“错误的位置”，以至于后来不得不对它们进行排序？更糟糕的是，我们发现我们存储一个单词并打印它的次数等于它在输入中出现的次数。

我们可以通过使用 `unique_copy()` 而不是 `copy()` 来解决后一个问题。`unique_copy()` 简单地不复制重复的相同值。例如，使用普通的 `copy()`，程序将采用

the man bit the dog

并产生

bit

dog

man

the

the

如果我们使用 `unique_copy()`，程序将写入

bit

dog

man

the

这些换行符是从哪里来的？带有分隔符的输出非常常见，以至于 `ostream_iterator` 的构造函数允许你（可选地）指定在每个值之后打印的字符串：

`ostream_iterator<string> oo(os, "\n");` // 为流创建输出迭代器

显然，换行符是给人阅读的输出的一种流行选择，但也许我们更喜欢空格作为分隔符？我们可以这样写

`ostream_iterator<string> oo(os, " ");` // 为流创建输出迭代器

这将给我们输出

bit dog man the

### 21.7.3 使用集合保持顺序

有一种更简单的方法可以获得该输出；使用集合而不是向量：

```cpp
int main()
{
    string from, to;
    cin >> from >> to; // 获取源文件名和目标文件名

    ifstream is (from); // 创建输入流
    ofstream os {to}; // 创建输出流

    set<string> b (istream_iterator<string>(is), istream_iterator<string>{});
    copy(b.begin() , b.end() , ostream_iterator<string>(os, " "));// 将缓冲区复制到输出
}
```

当我们向集合中插入值时，重复项会被忽略。此外，集合中的元素按顺序保存，因此不需要排序。拥有合适的工具，大多数任务都很简单。

### 21.7.4 copy_if

`copy()` 算法无条件地复制。`unique_copy()` 算法抑制具有相同值的相邻元素。第三个复制算法仅复制谓词为真的元素：

```cpp
template<typename In, typename Out, typename Pred>
// requires Input_iterator<In> && Output_operator<Out>() &&
// Predicate<Pred, Value_type<In>>
Out copy_if(In first, In last, Out res, Pred p)
// 复制满足谓词的元素
{
 while (first!=last) {
 if (p(*first)) *res++ = *first;
 ++first;
 }
 return res;
}
```

使用我们在 §21.4 中的 `Larger_than` 函数对象，我们可以像这样找到序列中所有大于 6 的元素：

```cpp
void f(const vector<int>& v)
// 复制所有值大于 6 的元素
{
 vector<int> v2(v.size());
 copy_if(v.begin(), v.end(), v2.begin(), Larger_than(6));
 // . . .
}
```

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_826_0.png)

由于我犯的一个错误，该算法在 1998 年 ISO 标准中缺失。这个错误现在已经得到补救，但你仍然可能找到没有 `copy_if` 的实现。如果是这样，请仅使用本节的定义。

## 21.8 排序和搜索

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_826_1.png)

通常，我们需要数据有序。我们可以通过使用维护顺序的数据结构（如 `map` 和 `set`）或进行排序来实现。STL 中最常见且最有用的排序操作是我们已经使用过几次的 `sort()`。默认情况下，`sort()` 使用 `<` 作为排序标准，但我们也可以提供自己的标准：

```cpp
template<typename Ran>
// requires Random_access_iterator<Ran>()
void sort(Ran first, Ran last);

template<typename Ran, typename Cmp>
// requires Random_access_iterator<Ran>()
// && Less_than_comparable<Cmp,Value_type<Ran>>()>
void sort(Ran first, Ran last, Cmp cmp);
```

作为一个基于用户指定标准的排序示例，我们将展示如何在不区分大小区分的情况下对字符串进行排序：

```cpp
struct No_case { // lowercase(x)< lowercase(y)?
bool operator()(const string& x, const string& y) const
{
for (int i = 0; i< x.length(); ++i) {
if (i == y.length()) return false; // y<x
char xx = tolower(x[i]);
char yy = tolower(y[i]);
if (xx<yy) return true; // x<y
if (yy<xx) return false; // y<x
}
if (x.length()==y.length()) return false; // x==y
return true; // x<y (x 中的字符较少)
}
};

void sort_and_print(vector<string>& vc)
{
sort(vc.begin(),vc.end(),No_case());
for (const auto& s : vc)
cout<< s << "\n";
}
```

一旦序列被排序，我们就不再需要使用 find() 从头开始搜索；我们可以利用顺序进行二分查找。基本上，二分查找是这样工作的：

假设我们要查找值 *x*；查看中间元素：

- 如果元素的值等于 *x*，我们找到了它！
- 如果元素的值小于 *x*，任何值为 *x* 的元素必须在右侧，因此我们查看右半部分（在该半部分执行二分查找）。
- 如果 $x$ 的值小于元素的值，任何值为 $x$ 的元素必须在左侧，因此我们查看左半部分（在该半部分执行二分查找）。
- 如果我们达到了最后一个元素（向左或向右）而没有找到 $x$，则没有具有该值的元素。

对于更长的序列，二分查找比 find()（线性搜索）快得多。用于二分查找的标准库算法是 binary_search() 和 equal_range()。我们所说的“更长”是什么意思？这取决于情况，但通常十个元素就足以让 binary_search() 在性能上优于 find()。对于一个包含 1000 个元素的序列，binary_search() 的速度将是 find() 的约 200 倍，因为其成本是 $O(log_2(N))$；见 §21.6.4。

binary_search 算法有两种变体：

```cpp
template<typename Ran, typename T>
bool binary_search(Ran first, Ran last, const T& val);

template<typename Ran, typename T, typename Cmp>
bool binary_search(Ran first, Ran last, const T& val, Cmp cmp);
```

这些算法要求并假设其输入序列是排序好的。如果不是，“有趣的事情”，如无限循环，可能会发生。binary_search() 只是告诉我们一个值是否存在：

```cpp
void f(vector<string>& vs)     // vs 已排序
{
    if (binary_search(vs.begin(),vs.end(),"starfruit")) {
        // 我们有一个 starfruit
    }
    // ...
}
```

因此，当我们只关心某个值是否在序列中时，binary_search() 是理想的。如果我们关心找到的元素，我们可以使用 lower_bound()、upper_bound() 或 equal_range()（§B.5.4、§23.4）。在关心找到哪个元素的情况下，原因通常是该对象包含比键更多的信息，可能存在许多具有相同键的元素，或者我们想知道哪个元素满足了搜索标准。

## 21.9 容器算法

因此，我们使用迭代器指定的元素序列来定义标准库算法。输入序列被定义为一对迭代器 `[b:e)`，其中 `b` 指向序列的第一个元素，`e` 指向序列末尾之后的元素（§20.3）。输出序列则简单地指定为其第一个元素的迭代器。例如：

```cpp
void test(vector<int> & v)
{
    sort(v.begin(),v.end());   // 对 v 从 v.begin() 到 v.end() 的元素进行排序
}
```

这样做既简洁又通用。例如，我们可以对一个 `vector` 的一半进行排序：

```cpp
void test(vector<int> & v)
{
    sort(v.begin(),v.begin()+v.size()/2);   // 对 v 的前半部分元素进行排序
    sort(v.begin()+v.size()/2,v.end());      // 对 v 的后半部分元素进行排序
}
```

然而，指定元素范围有点冗长，而且大多数时候，我们是对整个 `vector` 而不是对其一半进行排序。因此，大多数时候，我们想这样写：

```cpp
void test(vector<int> & v)
{
    sort(v);     // 对 v 进行排序
}
```

标准库没有提供 sort() 的这种变体，但我们可以为自己定义它：

```cpp
template<typename C>   // 要求 Container<C>()
void sort(C& c)
{
    std::sort(c.begin(),c.end());
}
```

事实上，我们发现它非常有用，因此将其添加到了 std_lib_facilities.h 中。

像这样处理输入序列很容易，但为了保持简单，我们倾向于将返回类型保留为迭代器。例如：
