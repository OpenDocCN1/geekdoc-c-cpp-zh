

对的元素的修改以及对的交换，如以下示例所示：

```
int n = 1;
std::array<int, 4> arr{ 1,2,3,4 };
std::array<int, 4> arr2{ -1,-2,-3,-4 };
auto p3 = std::make_pair(n, arr);
auto p4 = std::make_pair(-n, arr2);
std::swap(p3, p4);
std::cout << p3.first << "," << p3.second[1] << '\n';

// 4. Modify individual elements of pair
std::get<0>(p3) = 200;
std::get<1>(p3) = std::array<int,4>(arr);
std::cout << p3.first << "," << p3.second[1] << '\n';
```

创建一对后，我们可能希望将它的元素值与另一对的元素值进行比较。为此，通常的二元谓词是适用的。我们以不等式运算符为例：

```
using IntPair = std::pair<int,int>;

// Comparison operators < etc. In general, 1st value
// has higher value
IntPair pi1 = std::make_pair(1, 2);
IntPair pi2 = std::make_pair(1, 1);
IntPair pi3 = std::make_pair(2, 1);
IntPair pi4 = std::make_pair(2, 2);
std::cout << std::boolalpha << (pi1 < pi2) << '\n';    // false
std::cout << std::boolalpha << (pi2 < pi1) << '\n';    // true
std::cout << std::boolalpha << (pi1 < pi3) << '\n';    // true
std::cout << std::boolalpha << (pi3 < pi1) << '\n';    // false
std::cout << std::boolalpha << (pi3 < pi4) << '\n';    // true
std::cout << std::boolalpha << (pi4 < pi3) << '\n';    // false
std::cout << std::boolalpha << (pi4 == pi3) << '\n';   // false
std::cout << std::boolalpha << (pi4 != pi3) << '\n';    // true
```

二元运算符为对定义这一事实意味着它们可以被排序并与 STL 算法一起使用。

我们现在来讨论构造由用户定义类型组成的一对的话题，并将讨论从 std::pair 切换到 std::tuple。我们可以强制调用构造函数而不是将元组作为一个整体使用。我们也可以转发参数来构造元组。为此，让我们首先考虑一个其实例将成为一对元素的类：

```
struct C
{
    C(const std::tuple<int, double>& tup)
    {
        std::cout << "\tConstructed a C from a tuple\n";
    }
}
```

```
C(int, double)
{
    std::cout << "\tConstructed a C from an int and a double\n";
}
;
```

我们首先按如下方式创建元组：

// Create a pair using 'whole' tuples
std::tuple<int, double> t1(1, 3.14), t2(-3.0, 2.71);
std::pair<C, C> p1(t1, t2);
```

这种情况下的输出是：

```
Constructed a C from a tuple
Constructed a C from a tuple
```

我们现在希望绕过元组的显式创建，而是将元组 t1 和 t2 转发给类 C 的元素：

// Now force the ctor to take the elements of the tuple
// rather than the tuple as a whole.
std::pair<C, C> p2(std::piecewise_construct, t1, t2);
```

这种情况下的输出是：

```
Constructed a C from an int and a double
Constructed a C from an int and a double
```

我们可以将参数转发给对的构造函数：

```
std::cout << "\nForward of C: \n";
std::pair<C, C> p2A(std::piecewise_construct,
                    std::forward_as_tuple(1, -1.7),
                    std::forward_as_tuple(2, 110.3));
std::cout << "End, forward of C:\n";
```

```
// Forwarding the arguments
int charCount = 10; char c = 'A';
std::pair<std::complex<value_type>, std::string>
pZ(std::piecewise_construct,
        std::forward_as_tuple(1.0, -1.7),
        std::forward_as_tuple(charCount, c));
std::cout << "\nForward: " << std::get<0>(pZ) << ", " <<
std::get<1>(pZ) << ")\n";
```

这种情况下的输出是：

```
Forward of C:
    Constructed a C from an int and a double
    Constructed a C from an int and a double
End, forward of C:

Forward: (1,-1.7), AAAAAAAAAA
```

通常，转发更高效。

我们在第 6 章讨论类型特征库，我们可以使用该库中的两个相关函数来检查组成元组的元素的类型，例如在由值类型和复数组成的 P1 的情况下：

// 7. Compile-time access to pair's element types.
// Use type traits to check types corresponding to element types
// (chapters 4 and 6)
using TypeFirst = std::tuple_element<0, decltype(p1)>::type;
static_assert(std::is_same<TypeFirst, value_type>::value, "ouch");

using TypeSecond = std::tuple_element<1, decltype(p1)>::type;
static_assert(std::is_same<TypeSecond, std::complex<value_type>>
::value, "ouch");
```

我们现在介绍 std::tie。一般来说，这个函数是一种将变量与一对或元组的<|message|>
