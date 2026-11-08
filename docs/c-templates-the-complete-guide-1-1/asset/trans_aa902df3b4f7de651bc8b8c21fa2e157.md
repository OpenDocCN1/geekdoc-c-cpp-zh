
```cpp
...
[](std::string const& s) {
    return s == "";
});
```

它包含一个相当小的错误：在用于查找集合中第一个匹配字符串的 lambda 中，我们将它与给定字符串进行比较。然而，map 中的元素是键/值对，因此我们应当期望得到 `std::pair<>`，而不是 `const std::string`。

流行的 GNU C++ 编译器的某个版本报告以下错误：

```text
 1  In file included from /cygdrive/p/gcc/gcc-1/include
 2  from /cygdrive/p/gcc/gcc-1/include/stl_algo.h:...,
 3  from /cygdrive/p/gcc/gcc-1/include/string:40,
 4  /cygdrive/p/gcc/gcc-1/errorcorrel.cpp:1:
 5  /cygdrive/p/gcc/gcc-1/include/bits/predefined_ops.h:
    _Iter_pred<_Predicate>::operator()(_Iterator) const
    [with _Iterator = ...]
 6      ...
 7  /cygdrive/p/gcc/gcc-1/include/bits/stl_algo.h:1044:
    std::_Find_if(...)
 8      with _InputIterator = ...
 9  /cygdrive/p/gcc/gcc-1/include/bits/stl_algo.h:...:
    find_if(_InputIterator, _InputIterator, _Predicate)
 10     ...
 11 /cygdrive/p/gcc/gcc-1/errorcorrel.cpp:13:29:
    required from here
 12     {main()}::{lambda(const string&)>::operator()
 13 /cygdrive/p/gcc/gcc-1/include/bits/predefined_ops.h
 14     const string& () aka bool (const std::string&)
 15 /cygdrive/p/gcc/gcc-1/include/bits/predefined_ops.h:
    arguments, 2 provided
 16 errorcorrel.cpp:13:52: note: candidate: ...
 17  {std::string const& s}
 18 errorcorrel.cpp:13:52: note: no known conversion for argument 1 from
    std::_Rb_tree_const_iterator<std::pair<const std::string, double> >
    to 'std::string const&'
```

像这样的消息开始看起来更像一部小说，而不是一条诊断信息。它也可能让人不知所措，甚至令模板新手用户望而却步。然而，经过一些练习，这类消息会变得可控，错误也开始揭示相对有用的细节。

这条错误消息的第一部分说，在内部 `predefined_ops.h` 头文件深处的一个函数模板实例中发生了错误，该头文件通过其他各种头文件从 `errorcorrel.cpp` 包含进来。此处及后续几行中，编译器报告了以下内容实例化了什么：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_118_0.png)

```cpp
auto p = std::find_if(col.begin(), col.end(),
    [](const int &x) {
        return x % 2 == 0;
    });
```

这导致在 `stl_algo.h` 头文件第 15 行实例化了一个 `find_if` 模板，其中代码

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_118_1.png)

```text
std::find_if(_Iter, _Iter, _Predicate)
```

被实例化为

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_118_2.png)

```text
_Iter = std::_Rb_tree_const_iterator<std::pair<const
std::__cxx11::basic_string<char>,
...>
_Predicate = main::<lambda(const std::string&)>
```

编译器报告所有这些内容，以防我们根本没有预料到所有这些模板会被实例化。它让我们能够确定导致这些实例化的事件链。

然而，在我们的示例中，我们愿意相信各种模板都需要被实例化，我们只是想知道为什么它没有成功。实例化错误位于消息的最后一部分。其中写着“no match for call”（没有匹配的调用）的部分意味着函数调用无法解析，因为实参类型和形参类型不匹配。它说明了被调用的是什么。

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_118_3.png)

```cpp
auto f = [](const std::string& string) {
    std::string::basic_string<char>
};
```

以及导致此调用的代码：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_118_4.png)

```text
{ return bool(_M_pred(*__it)); }
```

此外，就在这一行之后，注记“candidate:”说明只有一个候选者期望一个 `const string&`，并且该候选者定义在我们示例的第 11 行。这个 lambda 是一个可能的候选者，但它不匹配。

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_118_5.png)

```text
no known conversion for argument 1
from 'std::pair<const std::__cxx11::basic_string<char>, ...>'
to 'const string& (aka const std::__cxx11::basic_string<char>&)'
```

这描述了我们遇到的问题。

毫无疑问，这条错误消息本可以更好。实际问题可以在实例化历史之前被精确指出，并且不必使用像 `std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> >` 这样完全展开的实例化名称，使用更短的类型就足够了。但确实，这类错误消息在某些情况下可能有用。因此，其他编译器提供类似信息并不奇怪（尽管有些使用了前面提到的结构化技术）。

例如，Visual C++ 编译器输出类似如下内容：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_118_6.png)

```text
1  c:\tools\root\cl\include\algorithm(166): error C2664:
      '...operator()(const std::string &...'
2      with
3      [
4          _Ty=std::string,
5          _Ty=double
6      ]
7  c:\tools\root\cl\include\algorithm(166): note: Reason:
      _Rx_Ty? to 'const std::string&'
8      with
9      [
10         _Ky=std::string,
11         _Ty=double
12     ]
13 c:\tools\root\cl\include\algorithm(166): note: No user...
14 ... function template specialization ... being compiled
15        with
16        {
17            _Entstd::_Tree_unchecked_iterator<std::_Tree_simple_types<std::pair<const _Ty, double>>>
18            _My..._Tree_simple
              double>>>;
19            _T...=std::lambda_...
20        }
21 main.cpp(13): note: see reference to function template
   <std::_Tree_val<std::_Tree_simple
      ...>
22        with
23        {
24            _Entstd::_Tree_iterator<std::_Tree_val
              const std::pair<const _Ty, double>>
25            _Ty=std::string,
26            _Ty=double,
27            ...
28        }
```

这里同样，我们提供了实例化链，其中的信息告诉我们什么被哪些实参实例化以及在代码中的何处，并且两次看到我们

```text
cannot convert from 'std::pair<const _Ty, _Ty>' to 'const std::string'
with
{
    _Ty=std::string,
    _Ty=double
}
```

## 某些编译器上缺少 const

不幸的是，有时会出现泛型代码只在某些编译器上有问题的情况。考虑以下示例：

basicerrornovo2.cpp

```cpp
#include <string>

#include <unordered_set>


class Customer
{
private:

    std::string name;

public:

    Customer (std::string const& n)
        : name(n) {
        }

        std::string getName() const {

            return name;
        }
};

int main()
{
    struct MyCustomerHash {

        // NOTE: missing const is only an error with g++

        std::size_t operator() (Customer const& c) {

            return std::hash<std::string>()(c.getName());
        }
    };
```

我们将它用于 Customer 的哈希表：

```cpp
std::unordered_set<Customer, MyCustomerHash> coll;
```

在 Visual Studio 中可以看到，这段代码按预期编译。然而，在 g++ 或 clang 下，这段代码会产生大量错误消息。例如，在 g++ 6.1 上，第一条错误消息如下：

```text
 1  In file included from /cygdrive/p/gcc/gcc61-include/...
 2                   from /cygdrive/p/gcc/gcc61-include/bits/...
 3                   from errorno12.cpp:2:
 4  /cygdrive/p/gcc/gcc61-include/bits/hashtable_policy
    _detail.h: is_noexcept_hash<Customer, main()::<>
 5  /cygdrive/p/gcc/gcc61-include/type_traits:143:12:
    std::is_fast_hash<int>::type_traits:143:12: std::...
 6  main(): MyCustomerHash >
 7  /cygdrive/p/gcc/gcc61-include/type_traits:154:38:
    std::__and_<std::is_fast_hash<int>::MyCustomer
    Hash<Customer> main()::<MyCustomerHash> > >
 8  /cygdrive/p/gcc/gcc61-include/bits/unordered_set.h:
    unordered_set<Customer, MyCustomerHash>
 9  errorno12.cpp:28:07: required from here
10  /cygdrive/p/gcc/gcc61-include/bits/hashtable_policy
    'const main()::<MyCustomerHash> (const Customer&)
11  noexcept(std::declval<const Hash&>()(std::declval<const
    ...
12  errorno12.cpp:22:17: note: candidate: std::size_t
    operator() (const Customer& c)
13  std::size_t operator() (const Customer& c) {
14  errorno12.cpp:22:17: note: passing 'const main
    discards qualifiers
```

紧接着还有 20 多条其他错误消息：

```text
16  In file included from /cygdrive/p/gcc/gcc61-include
17                   from /cygdrive/p/gcc/gcc61-include/bits/...
18                   from /cygdrive/p/gcc/gcc61-include/bits/stl_pa
19                   from /cygdrive/p/gcc/gcc61-include/bits/stl_al
20                   from /cygdrive/p/gcc/gcc61-include/bits/char_traits:40,
21                   from errorno12.cpp:1:
22  /cygdrive/p/gcc/gcc61-include/type_traits: In insta
    __and_cat: std::is_fast_hash<int>::MyCustomerHas
    Customer, main()::<MyCustomerHash> >
23  /cygdrive/p/gcc/gcc61-include/bits/hashtable_policy.h:
    unordered_set<Customer, MyCustomerHash>
24  errorno12.cpp:28:47: required from here
25  /cygdrive/p/gcc/gcc61-include/bits/...
```
