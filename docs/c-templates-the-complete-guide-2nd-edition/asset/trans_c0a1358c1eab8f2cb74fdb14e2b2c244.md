
```cpp
void foo (T&& arg1, T&& arg2)
{
...
}
```

由于这些特殊处理，通常处理数组的最好方法就是简单地使用不同的函数名。更好的是，当然是确保模板的调用者使用 `std::vector` 或 `std::array`。但只要字符串字面量是原始数组，我们就始终必须考虑它们。

## 7.5 处理返回值

对于返回值，你也可以在按值返回或按引用返回之间做出选择。然而，返回引用可能是一个麻烦的来源，因为你引用的是你无法控制的东西。有几种情况下返回引用是常见的编程实践：

- 返回容器或字符串的元素（例如，通过 `operator[]` 或 `front()`）
- 授予对类成员的写访问权限
- 返回用于链式调用的对象（流的 `operator<<` 和 `operator>>` 以及类对象通常的 `operator=`）

此外，返回 const 引用以授予对成员的只读访问权限也很常见。

请注意，如果使用不当，所有这些情况都可能导致麻烦。例如：

[Click here to view code image](#)

```cpp
std::string* s = new std::string("whatever");
auto& c = (*s)[0];
delete s;
std::cout << c; // run-time ERROR
```

这里，我们获得了一个字符串元素的引用，但当我们使用该引用时，底层字符串已不再存在（即我们创建了一个 *悬空引用*），从而导致未定义行为。这个例子有点牵强（经验丰富的程序员很可能会立刻注意到问题），但事情很容易变得不那么明显。例如：[Click here to view code image](#)

```cpp
auto s = std::make_shared<std::string>("whatever");
auto& c = (*s)[0];
s.reset();
std::cout << c; // run-time ERROR
```

因此，我们应该确保函数模板按值返回其结果。

然而，正如本章所讨论的那样，使用模板参数 T 并不能保证它不是引用，因为 T 有时会被隐式推导为引用：Click here to view code image

```cpp
template<typename T>
T retR(T&& p) // p is a forwarding reference
{
return T{}; // OOPS: returns by reference when called for lvalues
}
```

即使 T 是从按值调用推导出的模板参数，当显式指定模板参数为引用时，它也可能变成引用类型：Click here to view code image

```cpp
template<typename T>
T retV(T p) //Note: T might become a reference
{
return T{}; // OOPS: returns a reference if T is a reference
}
```

```cpp
int x;
retV<int&>(x); // retT() instantiated for T as int&
```

为了安全，你有两个选择：
- 使用类型特征 std::remove_reference<>（参见第 D.4 节第 729 页）将类型 T 转换为非引用：Click here to view code image

```cpp
template<typename T>
typename std::remove_reference<T>::type retV(T p)
{
return T{}; // always returns by value
}
```

其他特征，如 std::decay<>（参见第 D.4 节第 731 页），在这里也可能有用，因为它们也会隐式移除引用。

- 让编译器通过将返回类型声明为 auto 来推导返回类型（自 C++14 起；参见第 1.3.2 节第 11 页），因为 auto 总是会衰减：Click here to view code image

```cpp
template<typename T>
auto retV(T p) // by-value return type deduced by compiler
{
return T{}; // always returns by value
}
```

## 7.6 推荐的模板参数声明

正如我们在前几节中所学到的，我们有非常不同的方式来声明依赖于模板参数的参数：
- 声明为按值传递参数：这种方法简单，它会衰减字符串字面量和原始数组，但对于大型对象来说性能并不最佳。尽管如此，调用者仍可使用 std::cref() 和 std::ref() 按引用传递，但调用者必须小心这样做是否有效。
- 声明为按引用传递参数：这种方法对于相对较大的对象通常提供更好的性能，尤其是在传递 – 现有对象（左值）给左值引用， – 临时对象（纯右值）或标记为可移动的对象（xvalue）给右值引用， – 或两者都传递给转发引用时。
因为在所有这些情况下参数都不会衰减，你在传递字符串字面量和其他原始数组时可能需要特别注意。对于转发引用，你还必须注意，使用这种方法时模板参数隐式可以推导为引用类型。

### 一般建议

考虑到这些选项，对于函数模板，我们建议如下：

1. 默认情况下，声明参数为按值传递。这很简单，即使使用字符串字面量也通常有效。对于小型参数以及临时或可移动对象，性能足够好。调用者有时可以使用 std::ref() 和 std::cref() 传递现有的大型对象（左值）以避免昂贵的复制。
2. 如果有充分理由，则另行处理：
   - 如果你需要一个 out 或 inout 参数，该参数返回新对象或允许修改供调用者使用的参数，则将参数作为非常量引用传递（除非你更喜欢通过指针传递）。然而，你可能需要考虑禁用意外接受 const 对象，如第 7.2.2 节第 110 页所讨论的那样。
   - 如果模板是为了转发参数而提供的，请使用完美转发。即，声明参数为转发引用，并在适当的地方使用 std::forward<>()。考虑使用 std::decay<> 或 std::common_type<> 来“协调”不同类型的字符串字面量和原始数组。
   - 如果性能是关键，并且预计复制参数代价高昂，请使用常量引用。当然，如果你无论如何都需要本地副本，则不适用。
3. 如果你知道得更好，就不要遵循这些建议。然而，不要对性能做出直觉上的假设。即使是专家，如果尝试的话也会失败。相反：进行测量！

### 不要过度泛化

请注意，实际上，函数模板通常不是针对参数的任意类型。相反，一些约束适用。例如，你可能知道只会传递某种类型的向量。在这种情况下，最好不要将此类函数声明得过于通用，因为正如所讨论的，可能会出现令人惊讶的副作用。相反，请使用以下声明：Click here to view code image

```cpp
template<typename T>
void printVector (std::vector<T> const& v)
{
...
}
```

使用这种参数 v 的声明，在 printVector() 中，我们可以确定传递的 T 不能成为引用，因为向量不能使用引用作为元素类型。此外，很明显，按值传递向量参数几乎总是会变得昂贵，因为 std::vector<> 的拷贝构造函数会复制元素。因此，出于这个原因，将此类向量参数声明为按值传递几乎永远没有用处。如果我们仅将参数 v 声明为类型 T，则在调用方之间选择按值调用还是按引用调用就不那么明显了。

### std::make_pair() 示例

std::make_pair<>() 是一个很好的例子，展示了决定参数传递机制的陷阱。它是 C++ 标准库中的一个便利函数模板，用于使用类型推导创建 std::pair<> 对象。它的声明在不同版本的 C++ 标准中发生了变化：
- 在第一个 C++ 标准 C++98 中，make_pair<>() 在命名空间 std 内声明，使用按引用调用以避免不必要的复制：Click here to view code image

```cpp
template<typename T1, typename T2>
pair<T1,T2> make_pair (T1 const& a, T2 const& b)
{
return pair<T1,T2>(a,b);
}
```

然而，这几乎立即导致了使用不同大小的字符串字面量或原始数组对时出现重大问题。⁸

- 作为后果，在 C++03 中，函数定义被更改为使用按值调用：Click here to view code image

```cpp
template<typename T1, typename T2>
pair<T1,T2> make_pair (T1 a, T2 b)
{
return pair<T1,T2>(a,b);
}
```

正如你在问题解决的 rationale 中所读到的，“看起来这比其他两个建议对标准来说是一个更小的改动，任何效率问题都比解决方案的优势要小得多。”

- 然而，随着 C++11，make_pair() 必须支持移动语义，因此参数必须变为转发引用。出于这个原因，定义大致再次更改如下：Click here to view code image

```cpp
template<typename T1, typename T2>
constexpr pair<typename decay<T1>::type, typename decay<T2>::type>
make_pair (T1&& a, T2&& b)
{
return pair<typename decay<T1>::type, typename decay<T2>::type>(forward<T1>(a), forward<T2>(b));
}
```

完整的实现甚至更复杂：为了支持 std::ref() 和 std::cref()，函数还将 std::reference_wrapper 的实例解包为真正的引用。

C++ 标准库现在在许多地方以类似的方式完美转发传递的参数，通常结合使用 std::decay<>。

## 7.7 总结

- 测试模板时，使用不同长度的字符串字面量。
- 按值传递的模板参数会衰减，而按引用传递则不会衰减。
- 类型特征 std::decay<> 允许你在模板中衰减按引用传递的参数。
- 在某些情况下，std::cref() 和 std::ref() 允许你按

