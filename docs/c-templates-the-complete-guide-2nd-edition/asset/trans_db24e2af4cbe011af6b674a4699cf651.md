

```
_Predicate = main()::<lambda(const string&)>
```

编译器报告所有这些信息，只是因为我们原本没有预料到所有这些模板都会被实例化。它让我们能够确定导致实例化的事件链。

然而，在我们的示例中，我们愿意相信各种模板都需要被实例化，只是想知道为什么它不起作用。这些信息出现在消息的最后部分：“no match for call”表示函数调用无法解析，因为参数类型和参数类型不匹配。它列出了所谓的

```
(main()::<lambda(const string&)>) (std::pair<const std::__cxx11::basic_string<char>, double>&)
```

以及导致此调用的代码：

```
{ return bool(_M_pred(*__it)); }
```

此外，紧随其后，含有“note: candidate:”的行说明了有一个候选类型期望 `const string&`，并且该候选定义在 errornovel1.cpp 的第11行，即 `lambda [] (std::string const& s)`，同时还有一个可能候选不适合的原因：

```
no known conversion for argument 1
from 'std::pair<const std::__cxx11::basic_string<char>, double>'
to 'const string& {aka const std::__cxx11::basic_string<char>&}'
```

这描述了我们遇到的问题。

毫无疑问，错误消息可以写得更好。实际问题可以在实例化历史之前输出，而且不要使用完全展开的模板实例化名称，比如 `std::__cxx11::basic_string<char>`，只用 `std::string` 也许就够了。然而，同样正确的是，这个诊断中的所有信息在某些情况下都可能有用。因此，其他编译器提供类似信息也就不足为奇了（尽管有些编译器使用了前面提到的结构化技术）。

例如，Visual C++ 编译器输出类似如下内容：

```
1 c:\tools_root\cl\inc\algorithm(166): error C2664: 'bool main::<lambda_b863c1c7cd07048816f454330789acb4>::operator ()(const std::string &) const': cannot convert argument 1 from
'std::pair<const _Kty,_Ty>' to 'const std::string &'
2 with
3 [
4 _Kty=std::string,
5 _Ty=double
6 ]
7 c:\tools_root\cl\inc\algorithm(166): note: Reason: cannot
convert from 'std::pair<const _Kty,_Ty>' to 'const std::string'
8 with
9 [
10 _Kty=std::string,
11 _Ty=double
12 ]
13 c:\tools_root\cl\inc\algorithm(166): note: No user-defined-conversion operator available
that can perform this conversion, or the operator cannot be called
14 c:\tools_root\cl\inc\algorithm(177): note: see reference to
function template instantiation '_InIt
std::_Find_if_unchecked<std::_Tree_unchecked_iterator<_Mytree>,_Pr>(_InIt,_InIt,_Pr &)' being compiled
15 with
16 [
17 _InIt=std::_Tree_unchecked_iterator<std::_Tree_val<std::_Tree_simple_types<std::pair<const std::string,double>>>>,
18 _Mytree=std::_Tree_val<std::_Tree_simple_types<std::pair<const std::string,double>>>
19 _Pr=main::<lambda_b863c1c7cd07048816f454330789acb4>
20 ]
21 main.cpp(13): note: see reference to function template
instantiation '_InIt std::find_if<std::_Tree_iterator<std::_Tree_val<std::_Tree_simple_types<std::pair<_Kty,_Ty>>>>,main::<lambda_b863c1c7cd07048816f454330789acb4>>(_InIt,_InIt,_Pr)' being compiled
22 with
23 [
24 _InIt=std::_Tree_iterator<std::_Tree_val<std::_Tree_simple_types<std::pair<const std::string,double>>>>,
25 _Kty=std::string,
26 _Ty=double,
27 _Pr=main::<lambda_b863c1c7cd07048816f454330789acb4>
28 ]
```

这里，我们再次看到实例化链，其中包含信息告诉我们哪个参数实例化了什么、在代码中的位置，并且我们两次看到

```
cannot convert from 'std::pair<const _Kty,_Ty>' to 'const std::string'
with
[
_Kty=std::string,
_Ty=double
]
```

## 某些编译器上缺少 const

不幸的是，有时泛型代码只在某些编译器上出问题。考虑以下示例：

*basics/errornovel2.cpp*

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
    // provide our own hash function:
    struct MyCustomerHash {
        // NOTE: missing const is only an error with g++ and clang:
        std::size_t operator() (Customer const& c) {
            return std::hash<std::string>()(c.getName());
        }
    };

    // and use it for a hash table of Customers:
    std::unordered_set<Customer,MyCustomerHash> coll; ...
}
```

使用 Visual Studio 2013 或 2015 时，这段代码按预期编译。然而，使用 g++ 或 clang 时，代码会产生大量错误消息。例如，在 g++ 6.1 上，第一条错误消息如下：

```
1 In file included from /cygdrive/p/gcc/gcc61-include/bits/hashtable.h:35:0,
2 from /cygdrive/p/gcc/gcc61-include/unordered_set:47,
3 from errornovel2.cpp:2:
4 /cygdrive/p/gcc/gcc61-include/bits/hashtable_policy.h: In instantiation of 'struct std::__is_noexcept_hash<Customer, main()::MyCustomerHash>':
  __detail::__is_noexcept_hash<Customer, main()::MyCustomerHash>'
5 /cygdrive/p/gcc/gcc61-include/type_traits:143:12: required from 'struct std::__and_<
  std::__is_fast_hash<main()::MyCustomerHash>,
  std::__detail::__is_noexcept_hash<Customer,
  main()::MyCustomerHash> >'
6 /cygdrive/p/gcc/gcc61-include/type_traits:154:38: required from
  'struct std::__not_<
  std::__and_<std::__is_fast_hash<main()::MyCustomerHash>,
  std::__detail::__is_noexcept_hash<Customer,
  main()::MyCustomerHash> > >'
7 /cygdrive/p/gcc/gcc61-include/bits/unordered_set.h:95:63:
  required from 'class std::unordered_set<Customer, main()::MyCustomerHash>'
8 errornovel2.cpp:28:47: required from here
9 /cygdrive/p/gcc/gcc61-include/bits/hashtable_policy.h:85:34:
  error: no match for call to
  '(const main()::MyCustomerHash) (const Customer&)'
10 noexcept(declval<const _Hash&>()(declval<const _Key&>()))
11 ~~~~~~~
12 errornovel2.cpp:22:17: note: candidate: std::size_t
  main()::MyCustomerHash::operator()(
  const Customer&) <near match>
13 std::size_t operator() (const Customer& c) {
14 ^~~~~~~~
15 errornovel2.cpp:22:17: note: passing 'const
  main()::MyCustomerHash*' as 'this' argument
  discards qualifiers
```

紧接着是超过20条其他错误消息：

```
16 In file included
from /cygdrive/p/gcc/gcc61-include/bits/move.h:57:0,
18 from /cygdrive/p/gcc/gcc61-include/bits/stl_pair.h:59,
19 from /cygdrive/p/gcc/gcc61-include/bits/stl_algobase.h:64,
20 from /cygdrive/p/gcc/gcc61-include/bits/char_traits.h:39,
21 from /cygdrive/p/gcc/gcc61-include/string:40,
22 from errornovel2.cpp:1:
23 /cygdrive/p/gcc/gcc61-include/type_traits: In instantiation of 'struct std::__not_<std::__and_<std::__is_fast_hash<main()::MyCustomerHash>,
```

对于 `std::unordered_set<Customer,MyCustomerHash> coll;`，在实例化 `noexcept(declval<const _Hash&>()(declval<const _Key&>()))` 时，`const main()::MyCustomerHash (const Customer&)` 的调用没有匹配项。

（`declval<const _Hash&>()` 是一个类型为 `main()::MyCustomerHash` 的表达式）。一个可能的“近似匹配”候选是

```
std::size_t main()::MyCustomerHash::operator()(const Customer&)
```

其声明为

```
std::size_t operator() (const Customer& c) {
^~~~~~~
```

最后一条说明提到了问题所在：

```
passing ‘const main()::MyCustomerHash*’ as ‘this’ argument discards qualifiers
```

你能看出问题是什么吗？这个 `std::unordered_set` 类模板的实现要求哈希对象的函数调用运算符是一个 const 成员函数（另请参见第159页的11.1.1节）。如果不是这样，就会在算法深处引发错误。

所有其他错误消息都源自第一条，只要在哈希函数运算符上简单地添加 const 限定符，它们就都会消失：

```
std::size_t operator() (const Customer& c) const {
...
}
```

Clang 3.9 在第一条错误消息的末尾给出了稍微好一点的提示，指出哈希仿函数的 `operator()` 没有标记为 const：

```
...
errornovel2.cpp:28:47: note: in instantiation of template class
’std::unordered_set<Customer
```

