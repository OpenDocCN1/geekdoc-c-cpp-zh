

## 适当的动机

字符串字面量通常不会太大，因此你可能会想，即使复制它们又有什么关系呢？也许没什么关系。但`std::string_view`可以从任何C风格字符数组创建，而该数组可以任意大。例如，在`Ex9_02`中将分隔符参数改为`string_view`可能并没有带来多大好处。但对于另一个参数`text`，情况确实可能有所不同，如下面的代码片段所示：

```cpp
char* text = ReadHugeTextFromFile();       // last character in text is null ('\0')
find_words(words, text, ",;:!?\"\n");
delete[] text;
```

在这种情况下，假定字符数组以空字符元素结尾，这是C和C++编程中常见的约定。如果不是这种情况，你就需要使用更类似下面这种形式：

```cpp
char* text = ...;                 // again a huge amount of characters...
size_t numCharacters = ...;       // the huge amount
find_words(words, std::string_view(text, numCharacters), ",;:!?\"\n");
delete[] text;
```

无论哪种情况，关键在于：如果使用`std::string_view`，在将其传递给`find_words()`时不会复制巨大的文本数组；而如果使用`const std::string&`，则会被复制。

## Spans：指向vector或array的新型引用

在Ex8_14中，你可能已经注意到前两个`largest()`函数都计算相同数值类型`double`的序列中的最大值。为帮你回顾，这里是它们的函数原型：

```cpp
double largest(const std::vector<double>& data);
double largest(const double data[], size_t count);
```

除了一个操作普通数组而另一个操作vector之外，这两个函数几乎没有区别。

那时我们已经指出，函数模板可以解决重复的函数重载问题。我们将在下一章讨论这一点。但对于这种特殊情况——针对具有相同元素类型的序列的函数重载——C++20提供了一个有趣的替代方案，称为spans。`std::span<T>`类模板允许你引用任何连续的T值序列——无论是`std::vector<T>`、`std::array<T,N>`还是C风格数组——而无需指定具体的数组或容器类型。

让我们用一个例子来更具体地说明。导入`<span>`模块后，你可以将Ex8_14中上述两个`largest()`重载替换为单个重载，如下所示（另请参阅Ex9_03）：

```cpp
// double largest(const std::vector<double>& data);
// double largest(const double data[], size_t count);
double largest(std::span<double> data);
```

除了签名之外，你可以完全按照之前为`std::vector<double>`重载实现此新函数：

```cpp
// Finds the largest of a sequence of double values
double largest(std::span<double> data) /* Note: signature is not ideal yet: see later */
{
    double max {data[0]};
    for (auto value : data)
        if (max < value) max = value;
    return max;
}
```

换句话说，你不仅可以在基于范围的for循环中使用spans，它们还提供了方括号运算符`[]`，允许你按索引访问各个元素。与string_view对象一样，span<>对象可以非常高效地按值传递给函数。

> **注意**  除了范围支持和方括号运算符外，`std::span<>`还提供了你已经从`std::array<>`和`std::vector<>`中了解的各种其他函数：size()、empty()、data()、front()和back()。其他函数，例如用于创建subspan的一些成员，是span<>特有的。你可以查阅标准库参考以获取完整的成员列表。

有了新的largest()重载，你在Ex8_14的main()函数中需要修改的地方很少。只有表达式largest(array, std::size(array))需要修改，因为largest()现在期望输入一个span对象，而不是指针和大小。幸运的是，从指针-大小对创建span非常简单。完整写出来的更新输出语句如下：

```cpp
double array[] {1.5, 44.6, 13.7, 21.2, 6.7};
//
std::cout << "The largest of array is "
          << largest(std::span<double>{ array, std::size(array) }) << std::endl;
```

哎呀！这太冗长了。幸运的是，你可以省略参数类型，仅使用花括号初始化器来调用largest()，如下所示：

```cpp
std::cout << "The largest of array is " << largest({ array, std::size(array) })
          << std::endl;
```

编译器知道它必须在此处创建一个span对象，因为对应的函数重载是唯一接受此花括号初始化器的重载。

但你可以使用更短的表达式。因为编译器知道array的大小——它是类型为double(&)[5]的引用变量——所以大小参数是多余的。

```cpp
std::cout << "The largest of array is " << largest(array) << std::endl;
```

只有当第一个参数是类型为T*或const T*的指针变量，编译器无法从该指针推断出大小时，才需要额外的大小参数来创建span<T>对象。

### Spans与Views对比

在许多方面，`std::span`与`std::string_view`明显相似。两者都允许你检查（查看）未特化的类似数组的元素，无论是普通数组（C风格数组、字符串字面量等）还是属于某个容器对象（如`std::vector<>`、`std::array<>`、`std::string<>`等）的数组。而且，在这样做时，span和string_view都不会复制底层数组的元素。那么，为什么他们将其命名为`std::span<>`，而不是比如`std::array_view<>`呢？

原因是span和view之间有一个重要区别：与string_view不同，span<>允许你重新赋值或更改底层数组的元素。我们可以用下面的代码片段来说明这一点：

```cpp
std::vector<double> my_vector{ 0, 2, 15, 16, 23, 42 };
std::span<double> my_span(my_vector);
my_span.front() = 4;
my_span[1] *= 4;
std::cout << my_vector[0] << ", " << my_vector[1] << std::endl;  // 4, 8
```

std::span<T>的front()、back()和operator[]成员都返回T&引用，引用底层数组的非const元素。这允许你赋值或更改这些元素。回想一下，同样的操作对string_view无效：

```cpp
std::string my_string{
  "Don't accept the limitations of other people who claim things are 'unchangeable'. "
  "If it's written in stone, bring your hammer and chisel."
};
std::string_view my_string_view{ my_string };
// my_string_view[0] = 'W';  // Error: my_string_view[0] returns const char&
```

> **注意**  虽然span<>允许你重新赋值或以其他方式更改元素，但它不允许你添加或删除任何元素。也就是说，span<>不提供push_back()、erase()或clear()等成员。否则，就不可能为C风格数组或std::array<>对象创建span<>了。

### const元素的Spans

你可以修改span<T>所支持的元素这一事实意味着，你不应该能够从const容器等创建span。如果可以，这个span<>将为修改const容器的元素提供后门。你可以尝试编译下面的片段来试试（编译会失败）：

```cpp
const std::vector<double> my_const_vector{ 4, 8, 15, 16, 23, 42 };
std::span<double> my_span(my_const_vector);  // Should not compile!
my_span[3] = 100;                             // Reason: this should not be possible...
```

不幸的是，这给我们之前在`Ex9_03.cpp`中创建的`largest()`函数带来了一个看似严重的问题。为帮你回顾，这里是它的声明：

```cpp
// double largest(const std::vector<double>& data);
// double largest(const double data[], size_t count);
double largest(std::span<double> data);
```

因为无法从const vector创建`span<double>`，所以`Ex9_03`的`largest()`函数实际上根本不是原来两个函数重载的合适替代品。例如，使用本节前面定义的`my_const_vector`，下面的调用将无法工作：

```cpp
auto max = largest(my_const_vector);  // Does not compile!
```

幸运的是，这很容易解决。要替换`const vector<T>&`，你应该使用`span<const T>`而不是`span<T>`。也就是说，你应该使用const元素的span。`span<const T>`的所有元素访问器函数（包括`[]`运算符）都返回const `T&`引用，即使原始数组或容器是非const的。下面的片段说明了这一点。

```cpp
std::vector<double> my_vector{ 4, 8, 15, 16, 23, 42 };
std::span<const double> my_const_span(my_vector);
// my_const_span[3] = 100;          // Does not compile!
```

> **注意**  因此，`std::string_view`最类似于`std::span<const char>`。当然，关键区别在于`std::string_view`提供了专门用于处理字符串的额外成员函数。

因此，`largest()`函数的正确原型如下：

```cpp
double largest(std::span<const double> data);
```

除了签名之外，函数定义不需要其他任何更改。你可以在`Ex9_03A.cpp`中找到最终的程序。

> **提示**  使用`span<const T>`代替`const vector<T>&`。同样，使用`span<T>`代替`vector<T>&`，除非你需要插入或删除元素。

## 固定大小的Spans

你还可以使用`span<>`类模板编写一个能操作固定大小数组的泛型函数。你所需要做的就是将这个固定大小作为模板的第二个参数添加进去。例如，你可以用单个函数替换`Ex8_09A`、`Ex8_09B`和`Ex8_09C`中不同的`average10()`函数，如下所示：

```cpp
// double average10(const double (&values)[10]);
// double average10(const std::array<double, 10>& values);
double average10(std::span<const double, 10> values);
```

