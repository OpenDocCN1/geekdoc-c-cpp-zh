
应用于字符串。这个对象被泛型算法`sort`作为函数对象调用。该泛型算法调用函数对象的`operator()`成员来比较两个字符串对象。函数对象的`operator()`又会调用字符串数据类型的`operator<`。最终，当`sort`返回时，vector的第一个元素将包含所有字符串中字符串值最大的那个字符串。

函数对象自身的`operator()`此时并不可见。不要将`greater<string>()`实参中的括号与调用`operator()`混淆。当`operator()`在`sort`内部实际使用时，它接收两个实参：两个用于比较“更大性”的字符串。由于`greater<string>::operator()`定义为内联，上述`sort`调用中实际上并不存在该调用本身。相反，`sort`通过`greater<string>::operator()`调用`string::operator>`。

既然我们知道构造函数会作为实参传递给（许多）泛型算法，我们就可以设计自己的函数对象。假设我们想以不区分大小写的方式对我们的 vector 排序。该怎么做？首先要注意，默认的`string::operator<`（用于递增排序）并不合适，因为它执行区分大小写的比较。因此，我们提供自己的`CaseInsensitive`类，它以不区分大小写的方式比较两个字符串。下面的程序使用标准C函数`strcasecmp`实现这一技巧。它按字母升序对其命令行实参进行不区分大小写排序：

```cpp
#include <iostream>
#include <string>
#include <cstring>
#include <algorithm>
using namespace std;

class CaseInsensitive
{
    public:
        bool operator()(string const &left, string const &right) const
        {
            return strcasecmp(left.c_str(), right.c_str()) < 0;
        }
};
int main(int argc, char **argv)
{
    sort(argv, argv + argc, CaseInsensitive());
    for (int idx = 0; idx < argc; ++idx)
        cout << argv[idx] << " ";
    cout << '\n';
}
```

`CaseInsensitive`类的默认构造函数用于向`sort`提供其最后一个实参。因此，必须定义的唯一成员函数是`CaseInsensitive::operator()`。由于我们知道它会以字符串实参调用，我们将其定义为期望两个字符串实参，这两个实参在调用`strcasecmp`时使用。此外，`operator()`函数定义为内联，以便在被`sort`函数调用时不产生开销。`sort`函数会用各种字符串组合调用该函数对象。如果编译器同意我们的内联请求，它实际上会调用`strcasecmp`，跳过两次额外的函数调用。

比较函数对象通常是*预定义函数对象*。预定义函数对象类可用于许多常用操作。以下各节将介绍可用的预定义函数对象，并给出一些展示其用法的示例。在关于函数对象的一节接近末尾处，将介绍*函数适配器*。

预定义函数对象主要与泛型算法一起使用。预定义函数对象可用于算术、关系和逻辑运算。第23.3节将开发执行按位运算的预定义函数对象。

### 18.1.1 算术函数对象

算术函数对象支持标准算术运算：加法、减法、乘法、除法、取模和取负。这些函数对象会调用其被实例化所针对的数据类型的对应运算符。例如，对于加法，可以使用函数对象`plus<Type>`。如果将`Type`替换为`size_t`，则使用针对`size_t`值的加法运算符；如果将`Type`替换为`string`，则使用针对字符串的加法运算符。例如：

```cpp
#include <iostream>
#include <string>
#include <functional>
using namespace std;

int main(int argc, char **argv)
{
    plus<size_t> uAdd;            // function object to add size_ts

    cout << "3 + 5 = " << uAdd(3, 5) << '\n';

    plus<string> sAdd;            // function object to add strings

    cout << "argv[0] + argv[1] = " << sAdd(argv[0], argv[1]) << '\n';
}
/*
    Output when called as: a.out going

    3 + 5 = 8
    argv[0] + argv[1] = a.outgoing
*/
```

为什么这有用？请注意，该函数对象可用于所有支持该函数对象所调用运算符的各种数据类型（不仅是预定义数据类型）。

假设我们想对一个左操作数执行操作，该左操作数始终是同一个变量，而右操作数则依次使用数组中的所有元素。例如，我们想计算数组中所有元素的和；或者我们想拼接文本数组中的所有字符串。在这类情况下，函数对象就派上用场了。

如前所述，函数对象在泛型算法的语境中被大量使用，所以让我们再快速预览另一个算法。

泛型算法`accumulate`会访问由迭代器范围指定的所有元素，并对一个公共元素和该范围内的每个元素执行所请求的二元运算，在访问完迭代器范围指定的所有元素后返回累积结果。这个算法很容易使用。下面的程序累积所有命令行实参并打印最终字符串：

```cpp
#include <iostream>
#include <string>
#include <functional>
#include <numeric>
using namespace std;

int main(int argc, char **argv)
{
    string result =
        accumulate(argv, argv + argc, string(), plus<string>());

    cout << "All concatenated arguments: " << result << '\n';
}
```

前两个实参定义要访问元素的（迭代器）范围，第三个实参是`string`。这个匿名字符串对象提供一个初始值。我们也可以使用

```cpp
string("All concatenated arguments: ")
```

在这种情况下，`cout`语句可以简单地写成`cout << result << '\n'`。这里使用了字符串加法运算，由`plus<string>`调用。最终拼接后的字符串被返回。

现在我们定义一个类`Time`，并重载`operator+`。同样，我们可以应用预定义函数对象`plus`（现在针对我们新定义的数据类型进行定制）来相加时间：

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <functional>
#include <numeric>
using namespace std;

class Time
{
    friend ostream &operator<<(ostream &str, Time const &time);
    size_t d_days;
    size_t d_hours;
    size_t d_minutes;
    size_t d_seconds;
public:
    Time(size_t hours, size_t minutes, size_t seconds);
    Time &operator+=(Time const &rValue);
};
Time operator+(Time const &lValue, Time const &rValue)
{
    Time ret(lValue);
    ret += rValue;
    return ret;
}

Time::Time(size_t hours, size_t minutes, size_t seconds)
:
    d_days(0),
    d_hours(hours),
    d_minutes(minutes),
    d_seconds(seconds)
{}
Time &Time::operator+=(Time const &rValue)
{
    d_seconds   += rValue.d_seconds;
    d_minutes   += rValue.d_minutes   + d_seconds / 60;
    d_hours     += rValue.d_hours     + d_minutes / 60;
    d_days      += rValue.d_days      + d_hours / 24;
    d_seconds   %= 60;
    d_minutes   %= 60;
    d_hours     %= 24;
    return *this;
}
ostream &operator<<(ostream &str, Time const &time)
{
    return str << time.d_days << " days, " << time.d_hours <<
                                 " hours, " <<
                  time.d_minutes << " minutes and " <<
                  time.d_seconds << " seconds.";
}
int main(int argc, char **argv)
{
    vector<Time> tvector;

    tvector.push_back(Time(1, 10, 20));
    tvector.push_back(Time(10, 30, 40));
    tvector.push_back(Time(20, 50, 0));
    tvector.push_back(Time(30, 20, 30));

    cout <<
        accumulate
        (
            tvector.begin(), tvector.end(), Time(0, 0, 0), plus<Time>()
        ) <<
        '\n';
}
// Displays: 2 days, 14 hours, 51 minutes and 30 seconds.
```

上述程序的设计相当直接。`Time`定义了一个构造函数，定义了一个插入运算符，并定义了自己的`operator+`，用于相加两个时间对象。在`main`中，四个`Time`对象存储在一个`vector<Time>`对象中。然后，使用`accumulate`计算累积时间。它返回一个`Time`对象，该对象被插入到`cout`中。

第一个示例展示了*具名*函数对象的用法，而最后两个示例展示了传递给（`accumulate`）函数的*匿名*对象的用法。

STL支持以下算术函数对象集合。这些函数对象的函数调用运算符（`operator()`）会为传递给函数调用运算符的对象调用匹配的算术运算符，并返回该算术运算符的返回值。实际调用的算术运算符如下所示：

- `plus<>`：调用二元`operator+`；
- `minus<>`：调用二元`operator-`；
- `multiplies<>`：调用二元`operator*`；
- `divides<>`：调用`operator/`；
- `modulus<>`：调用`operator%`；
- `negate<>`：调用一元`operator-`。这个算术函数对象是一元函数对象，因为它期望一个实参。

在下一个示例中，使用`transform`泛型算法切换数组中所有元素的符号。`transform`期望两个迭代器，用于定义要转换的对象范围；一个迭代器，用于定义目标范围的起始位置（它可能与第一个实参是同一个迭代器）；以及一个函数对象，用于为所指示的数据类型定义一元运算。

```cpp
#include <iostream>
#include <string>
#include <functional>
#include <algorithm>
using namespace std;

int main(int argc, char **argv)
{
    int iArr[] = { 1, -2, 3, -4, 5, -6 };
```
