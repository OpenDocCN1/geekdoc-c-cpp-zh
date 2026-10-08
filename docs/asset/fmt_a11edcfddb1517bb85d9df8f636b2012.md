
这使用 `istream_iterator<int>` 创建了一个名为 `numbersInput` 的迭代器，它可以指向流中类型为 `int` 的对象。构造函数的参数指定了迭代器关联的流，因此这是一个可以从 `cin`（标准输入流）读取整数的迭代器。

默认的 `istream_iterator<T>` 构造函数会创建一个流结束迭代器（end-of-stream iterator），它等同于通过调用 `end()` 函数获取的容器的结束迭代器。以下是创建流结束迭代器的方法，用于配合 `numbersInput` 迭代器：

```cpp
istream_iterator<int> numbersEnd;
```

现在你有一对定义了来自 `cin` 的 `int` 类型值序列的迭代器。你可以使用它们将值从 `cin` 加载到 `vector<int>` 容器中：

```cpp
vector<int> numbers;

cout << "Enter integers separated by spaces then a letter to end:" << endl;

istream_iterator<int> numbersInput(cin, numbersEnd);

while(numbersInput != numbersEnd)
    numbers.push_back(*numbersInput++);
```

## 第 10 章 标准模板库

在定义了存储 `int` 类型值的 `vector` 后，你创建了两个输入流迭代器：`numbersInput` 是一个从 `cin` 读取 `int` 类型值的输入迭代器，而 `numbersEnd` 是流结束迭代器。只要 `numbersInput` 不等于流结束迭代器 `numbersEnd`，`while` 循环就会继续。当你执行该片段时，输入将一直持续，直到识别出 `cin` 的流结束。但那是什么？当你输入 Ctrl+Z 关闭流，或者输入无效字符时，就会出现流结束条件。

### 关于迭代器的更多 | 579

- `back_insert_iterator<T>` 在类型为 `T` 的容器末尾插入元素。该容器必须提供 `push_back()` 函数来完成此工作。
- `front_insert_iterator<T>` 在类型为 `T` 的容器头部插入元素。这取决于容器是否支持 `push_front()`。
- `insert_iterator<T>` 从类型为 `T` 的容器内的指定位置开始插入元素。该容器必须有一个 `insert()` 函数，该函数接受一个迭代器作为第一个参数，并将一个要插入的项作为第二个参数。

你可以使用前两种迭代器类型，除了一个指定容器的参数外。例如：

```
list<int> numbers;
front_insert_iterator<list<int>> iter(numbers);
```

在这里，你可以创建一个可以在 `list<int> numbers` 头部插入元素的迭代器。

向容器中插入值非常简单：

```
*iter = 99; // 在 numbers 容器的头部插入 99
```

你也可以像下面这样配合 `numbers` 容器使用 `front_inserter()`：

```
front_inserter(numbers) = 99;
```

这为该 `list` 创建了一个迭代器，并使用它将 99 插入到列表头部。`front_inserter()` 函数的参数是迭代器应用的容器。

`insert_iterator<T>` 的构造函数需要两个参数：

```
vector<int> values;
insert_iterator<vector<int>> iter_anywhere(values, begin(values));
```

第二个参数是指定数据插入位置的迭代器——在本例中是容器的。你可以像之前完全相同的方式使用该迭代器。以下是你可以如何使用该迭代器向 `vector` 插入一系列值：

```
for(int i = 0; i < 100; i++)
  iter_anywhere = i + 1;
```

此循环将从 1 到 100 的值插入到 `values` 容器的开头。执行此操作后，前 100 个元素将是 1、2 等，直到 100。

你也可以使用 `inserter()` 函数按反序插入元素：

```
for(int i = 0; i < 100; i++)
  inserter(values, begin(values)) = i + 1;
```

`inserter()` 的第一个参数是容器，第二个参数是标识数据插入位置的迭代器。值将按从 100 到 1 的反序排列。

插入迭代器可以以一种特别有用方式与 `copy()` 算法结合使用。以下是你可以如何从 `cin` 读取值并将其传输到 `list<T>` 容器：

```
list<double> values;
cout << "Enter a series of values separated by spaces "
cout << " followed by Ctrl+2 or a letter to enter:" << endl;
istream_iterator<double> input(cin), input_end;
copy(input, input_end, back_inserator(values));
```

你首先创建一个包含 `double` 值的列表。在提示输入后，你创建了两个 `double` 值的输入流迭代器。第一个迭代器指向 `cin`，第二个是由于默认构造函数创建的流结束迭代器。你通过这两个迭代器为 `copy()` 函数指定输入；拷贝操作的目标是你在 `copy()` 函数的第三个参数中创建的后置插入器。该后置插入器将 `copy` 操作传输的数据添加到列表容器中。这非常强大。如果你忽略提示，只需两条语句，就可以从标准输入流读取任意数量的值并将其传输到列表容器中。

## 使用输出流迭代器

作为输入流迭代器模板的补充，`ostream_iterator<T>` 模板提供了输出流迭代器，用于向输出流写入类型为 `T` 的对象。输出流迭代器有两个构造函数。其中一个创建一个可以将数据传输到目标流的迭代器：

```
std::ostream_iterator<int> out(cout);
```

模板参数 `int` 指定了要处理的数据类型，而构造函数参数 `cout` 指定了作为数据目的流，因此 `out` 迭代器可以向标准输出流写入 `int` 类型的值。以下是你可能使用该迭代器的方式：

```
int data[] = {1, 2, 3, 4, 5, 6, 7, 8, 9};
std::copy(begin(data), end(data), out);
// Contents 1 2 3 4 5 6 7 8 9
copy begin(numbers, end(numbers), out);
```

`copy()` 算法定义在 `<algorithm>` 头文件中，它将前两个迭代器参数指定的对象序列拷贝到第三个参数指定的输出迭代器。在这里，函数将元素从 `data` 数组拷贝到 `out` 迭代器，该迭代器将元素写入 `cout`。执行这段代码的结果将是

123456789

如你所示，值被写入输出流且中间没有空格。第二个构造函数可以改进这一点：

```
std::ostream_iterator<int> out(cout, " ");
```

第二个参数被用作输出值的分隔符。如果你将此迭代器作为 `copy()` 函数的第三个参数，输出将是：1, 2, 3, 4, 5, 6, 7, 8, 9。

让我们看看迭代器在实践中如何工作。假设你想从 `cin` 读取一系列整数并存储在 `vector` 中。然后你输出这些值。这是一个示例：

```cpp
#include <iostream>
#include <vector>
#include <iterator>
#include <numeric>
int main()
{
    vector<int> numbers;
    cout << "Enter a series of values separated by spaces "
    cout << "followed by Ctrl+2 or a letter to enter:" << endl;
    std::istream_iterator<int> input(cin), input_end;
    copy(input, input_end, std::back_inserter(numbers));
    cout << "You entered the following values:" << endl;
    std::ostream_iterator<int> out(cout, " ");
    copy(begin(numbers), end(numbers), out);
    cout << endl << "The sum of these values is "
    << std::accumulate(begin(numbers), end(numbers), 0) << endl;
    return 0;
}
```

## 关于函数对象的更多

`<functional>` 头文件定义了一系列模板，用于创建供算法和容器使用的函数对象。我将不会详细讨论它们，但会总结最实用的几个。比较函数对象如下表所示：

### 关于函数对象的更多 | 583

| 函数对象模板 | 描述 |
|---|---|
| `less<T>` | 创建一个表示类型 `T` 的对象之间 `<` 操作的二元谓词。例如，`less<string>()` 定义了一个用于比较字符串类型对象的函数对象。 |
| `less_equal<T>` | 创建一个表示类型 `T` 的对象之间 `<=` 操作的二元谓词。例如，`less_equal<double>()` 定义了一个用于比较双精度浮点类型对象的函数对象。 |
| `equal_to<T>` | 创建一个表示类型 `T` 的对象之间 `==` 操作的二元谓词。 |
| `not_equal_to<T>` | 创建一个表示类型 `T` 的对象之间 `!=` 操作的二元谓词。 |
| `greater_equal<T>` | 创建一个表示类型 `T` 的对象之间 `>=` 操作的二元谓词。 |
| `greater<T>` | 创建一个表示类型 `T` 的对象之间 `>` 操作的二元谓词。 |
| `not2<B>` | 创建一个类型 `B` 的二元谓词的反反二元谓词。例如，`not2(less<int>)` 创建了一个比较整型类型对象的二元谓词，当左操作数不小于右操作数时返回真。模板参数 `B` 是根据构造函数的类型推导出来的。 |

以下是你可以使用 `not2<B>` 模板来定义用于 `sort()` 算法的二元谓词：

```
sort(begin(v), end(v), not2(greater<string>()));
```

传递给 `not2` 构造函数的参数是 `greater<string>()`，这是对 `greater<string>` 类构造函数的调用，因此 `sort()` 函数使用“不大于”作为容器 `v` 中对象之间的比较方式进行排序。

`functional` 头文件还定义了用于对元素执行算术操作的函数对象。你可以使用这些对象通过 `algorithm` 头文件中定义的 `transform()` 算法对数值值序列应用操作。这些函数对象描述在下表中。

### 584 | 第 10 章 标准模板库

| 函数对象模板 | 描述 |
|---|---|
| `plus<T>` | 计算两个类型为 `T` 的元素的和。 |
| `minus<T>` | 通过从第一个操作数减去第二个操作数，计算两个类型为 `T` 的元素的差。 |
| `multiplies<T>` | 计算两个类型为 `T` 的元素的积。 |
| `divides<T>` | 将类型为 `T` 的第一个操作数除以第二个。 |
| `modulus<T>` | 计算类型为 `T` 的第一个操作数除以第二个后的余数。 |
| `negate<T>` | 返回类型为 `T` 的操作数的负值。 |

要使用这些，你需要应用 `transform()` 函数。我将在下一节解释它是如何工作的。

## 关于算法的更多内容

`algorithm` 和 `numeric` 头文件定义了大量的算法。`numeric` 头文件中的算法主要用于处理数值数组，而 `algorithm` 头文件中的算法更具通用性，提供了诸如对迭代器指定的对象序列进行搜索、排序、复制和合并的能力。在这个介绍性章节中，要讨论的内容太多了，因此我将只介绍 `algorithm` 头文件中几个最实用的算法，让你对如何使用它们有一个基本的了解。

你已经见过了 `algorithm` 头文件中的 `sort()` 和 `copy()` 算法。让我们简单看看 `algorithm` 头文件中一些更有趣的函数：

### `fill()` 算法

`fill()` 算法的格式如下：

```
fill(ForwardIterator begin, ForwardIterator end, const Type& value)
```

它用 `value` 填充由迭代器 `begin` 和 `end` 指定元素。例如，对于一个包含超过 10 个 `string` 类型元素的 `vector` `v`，可以写成：

```
fill(v.begin(), v.begin()+10, "invalid");
```

### `replace()` 算法

`replace()` 算法的格式如下：

```
replace(ForwardIterator begin, ForwardIterator end, const Type& oldValue, const Type& newValue)
```

此函数检查 `begin` 和 `end` 指定范围内的每个元素，并将每个 `oldValue` 出现处替换为 `newValue`。对于一个存储对象的 `vector` `v`，你可以可以使用语句将 "yes" 替换为 "no"：

```
replace(v.begin(), v.end(), string("yes"), string("no"));
```

与所有接收一对迭代器定义的区间的算法一样，`replace()` 函数也可以与指针工作。例如：

```
char str[] = "A node is as good as a wink to a blind horse";
replace(str, str+strlen(str), 'o', '*');
cout << str << endl;
```

这将把空终止字符串 `str` 中的每个 'o' 替换为 '*'，因此执行该函数的结果将是：

A nod is g*d as a wink t* a blind h*rse.

### `find()` 算法

`find()` 算法的格式如下：

```
find(InputIterator begin, InputIterator end, const Type& value)
```

它在在前两个参数指定的序列中搜索 `value` 的第一次出现处。例如，给定一个包含整型值的 `vector` `v`，你可以写道：

```
auto iter = find(v.begin(), end(v), 21);
```

通过使用 `iter` 作为新搜索的起点，你可以找到 `value` 的所有出现处：

```cpp
auto iter = v.begin();
int value = 21;
int count = 0;
while((iter = find(iter, end(v), value)) != end(v)) {
    iter++;
    count++;
}
cout << "The vector contains " << count << " occurrences" << endl;
```

你也可以将其写为 for 循环：

```cpp
for(auto iter = find(v.begin(), end(v), value); iter != end(v); iter = find(iter, end(v), value)) {
    count++;
}
```

### `transform()` 算法

`transform()` 有两个版本。第一个应用一对迭代器指定的操作，格式如下：

```
transform(InputIterator begin, InputIterator end, OutputIterator result, UnaryFunction f)
```

它对 `begin` 和 `end` 指定范围内的所有元素应用一元函数 `f`，并从 `result` 迭代器开始存储结果。`result` 迭代器可以是 `begin`，在这种情况下结果将替换原有元素。该函数返回指向结果之后的迭代器。这里有一个例子：

```cpp
double values[] = { 2.5, -3.5, 4.5, -5.5, 6.5, -7.5};
vector<double> data(countof(values));
transform(begin(data), end(data), begin(data), negate<double>());
```

`transform()` 对 `vector` `data` 中的所有元素应用 `negate<double>` 函数对象。结果存回 `data` 并覆盖原有值。

`transform()` 的第二个版本应用一个二元函数，其操作数来自由迭代器指定的两个范围。其函数为：

```
transform(InputIterator begin1, InputIterator end1, InputIterator begin2, OutputIterator result, BinaryFunction f)
```
