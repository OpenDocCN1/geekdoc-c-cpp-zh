
这创建了一个类型为 `stream_iterator<int>` 的迭代器 `numbersInput`，它可以指向流中类型为 `int` 的对象。构造函数的参数指定了迭代器关联的流，因此这是一个可以从 `cin`（标准输入流）读取的迭代器。

默认的 `stream_iterator<T>` 构造函数会创建一个流结束迭代器（end-of-stream），这等同于通过调用 `end()` 函数获取的容器的迭代器。以下是创建一个流结束迭代器的方法，它与 `numbersInput` 迭代器互补：

```cpp
stream_iterator<int> numbersEnd;
```

现在你拥有一对迭代器，定义了从 `cin` 开始的一系列 `int` 类型的值。你可以使用这些值从 `cin` 加载到 `vector<int>` 容器中：

```cpp
vector<int> numbers;

cout << "Enter integers separated by spaces a letter to end:" << endl;

stream_iterator<int> numbersInput(cin, numbersEnd);

while(numbersInput != numbersEnd)
  numbers.push_back(*numbersInput++);
```

## 第 10 章 标准模板库

在定义了用于存储 `int` 类型值的 `vector` 后，你创建了两个输入流迭代器：`numbersInput` 从 `cin` 读取 `int` 类型的值，而 `numbersEnd` 是流结束迭代器。只要 `numbersInput` 不等于流结束迭代器 `numbersEnd`，`while` 循环就会继续。当你执行这段代码片段时，输入会持续进行，直到 `cin` 被识别为流结束。但是什么产生了该条件呢？如果你输入 Ctrl+Z 关闭流，或者输入一个无效字符作为字母，就会出现流结束条件。

当然，你并不局限于使用输入整数作为循环控制变量。你可以使用它们将数据传递给算法，例如定义在 `numeric` 头文件中的 `accumulate()`：

```cpp
cout << "Enter integers by spaces a letter to end:" << endl;

istream_iterator<int> numbersInput(cin, numbersEnd);

cout << "The sum of the values that you entered is " \
accumulate(numbersInput, numbersEnd, 0) << endl;
```

这段代码片段输出了你获得的任何整数的总和。你会记得 `accumulate()` 的参数是一个指向序列中第一个值的迭代器，以及一个指向用于求和的最后一个值的迭代器。你正在将数据直接从 `cin` 传输到算法。

`sstream` 头文件定义了 `basic_istream<char>` 模板，它定义了一个可以使用类似字符串对象的方式从缓冲区访问数据的对象。该头文件还定义了 `istream` 作为 `basic_istream<char>` 的别名，你可以从字符串对象构造一个 `istream` 对象，这意味着你可以从字符串对象中读取数据，就像从 `cin` 读取数据一样。由于 `istream` 对象是一个对象，你可以将其传递给输入构造函数，并使用迭代器访问底层缓冲区流中的数据。这里有一个示例：

```cpp
string data("2.4 2.5 3.6 2.1 6.7 6.8 9.5 1.1 1.4 32");

iostream input(data);

istream_iterator<double> begin(input, end);

cout << "The sum of the values from the data is " \
accumulate(begin, end, 0.0) << endl;
```

你从字符串对象 `data` 创建了 `istream` 对象 `input`，这样你可以像流一样读取数据。你创建了两个可以处理输入中值的迭代器，并使用它们将数据流的内容传递给 `accumulate()` 算法。注意，`accumulate()` 函数参数的类型决定了结果的类型，因此必须将其指定为 `double` 值以正确产生总和。让我们尝试一个示例。

## 尝试使用输入流迭代器

此示例使用流迭代器从标准输入流读取文本并将其传输到 `map` 容器中以产生文本的词频。以下是代码：

```cpp
// Ex10_3.cpp

// 一个简单的词组统计

#include <iostream>

#include <string>

#include <map>

#include <iterator>

using std::cout;

using std::cin;

using std::endl;

using std::string;

int main() {

    std::map<string, int> words; // 用于存储单词和词频的 Map

    cout << "Enter some text and press followed by Ctrl+Z then Enter to end:";

    cout << endl;

    std::istream_iterator<string> begin(cin); // 流迭代器

    std::istream_iterator<string> end; // 流结束迭代器

    while(begin != end) { // 遍历流中的单词

        words[*begin++]++; // 增加并存储单词计数

    }

    // 输出单词计数及其频率

    cout << endl << "Here are the word counts for the text you entered:" << endl;

    const int wordsPerLine(4);

    int wordCount(0);

    cout << std::setflags(std::ios::left); // 左对齐输出

    for (auto& word : words) {

      cout << std::setw(15) << word.first << " * " << std::setw(5) << word.second << endl;

      if (++wordCount % wordsPerLine == 0) cout << endl;

    }

    return 0;

}
```

## 工作原理

你首先定义了一个用于存储 `int` 类型值的 `map`：

```cpp
std::map<string, int> words; // 用于存储单词和词频的 Map
```

该容器存储每个 `int` 类型的计数，使用 `string` 类型的单词作为键。当你使用流迭代器从输入读取时，这将轻松累加每个单词的计数：

```cpp
std::istream_iterator<string> begin(cin); // 流迭代器

std::istream_iterator<string> end; // 流结束迭代器
```

`begin` 迭代器是标准输入的流迭代器，而 `end` 是流结束迭代器。

你在循环中读取单词并累加计数：

```cpp
while(begin != end)
  words[*begin++] // 增加
```

这个简单的循环完成了大量工作。循环控制表达式遍历标准输入中的单词，直到达到流结束状态。迭代器从 `cin` 读取单词，就像 `cin` 的重载运算符一样。你使用 `map` 的下标运算符来存储计数；记住，下标运算符的参数是键。表达式 `*begin` 访问单词，表达式 `begin++` 在访问单词后增加迭代器。

当第一次读取单词时，它不在 `map` 中，因此 `words[*begin++]` 会存储一个值为 0 的新条目，并将迭代器指向下一个单词，准备进行下一次迭代。整个表达式 `words[*begin++]` 会增加条目的计数，无论它是否是新条目。因此，现有的条目只是增加计数，而新条目将创建创建并将计数从 0 增加到 1。

最后，通过 `for` 循环输出每个单词的计数：

```cpp
for (auto& word : words) {

  cout << std::setw(15) << word.first << " * " << std::setw(5) << word.second << endl;

}
```

`back_insert_iterator<T>` 在类型为 `T` 的容器末尾插入元素。该容器必须提供 `push_back()` 函数来完成此工作。

`front_insert_iterator<T>` 在类型为 `T` 的容器头部插入元素。这取决于容器是否支持 `push_front()`。

`insert_iterator<T>` 在类型为 `T` 的容器内，从指定位置开始插入元素。该容器必须有一个 `insert()` 函数，该函数接受一个迭代器作为第一个参数，并将一个要插入的项作为第二个参数。

前两种插入器类型的构造函数期望一个指定容器的单一参数。例如：

```cpp
list<int> numbers;

front_insert_iterator<list<int>> iter(numbers);
```

在这里，你创建了一个可以在 `list<int>` 容器 `numbers` 头部插入数据的迭代器。

向容器插入值非常简单：

```cpp
*iter = 99; // 在 numbers 容器的头部插入 99
```

你也可以对 `numbers` 容器使用 `front_inserter()`，如下所示：

```cpp
front_inserter(numbers) = 99;
```

这为 `numbers` 列表创建了一个插入器，允许其将 99 插入到列表头部。`front_inserter()` 函数的参数是要应用于该迭代器的容器。

`insert_iterator<T>` 的构造函数需要两个参数：

```cpp
vector<int> values;

insert_iterator<vector<int>> iter_anywhere(values, begin(values));
```

第二个参数是一个指定数据插入位置的迭代器——在本例中是序列的起始。你可以完全像使用上一个一样使用这个迭代器。以下是你如何使用此迭代器向 `vector` 插入一系列值：

```cpp
for(int i = 0; i < 100; i++)
  iter_anywhere = i + 1;
```

此循环将 1 到 100 的值插入到 `values` 容器的开头。执行此操作后，前 100 个元素将是 1、2 等，直到 100。

你也可以使用 `inserter()` 函数反向插入元素：

```cpp
for(int i = 0; i < 100; i++)
inserter(values, begin(values)) = i + 1;
```

`inserter()` 的第一个参数是容器，第二个参数是标识数据要插入位置的迭代器。这些值将以从 100 到 1 的反序排列。

插入器可以用特别有用的方式与 `copy()` 算法结合使用。以下是你如何从 `cin` 读取值并将其传输到 `list<T>` 容器：

```cpp
list<double> values;

cout << "输入一系列用空格分隔的数值 "
cout << "然后按 Ctrl+Z 或输入字母结束:" << endl;

istream_iterator<double> input(cin), input_end;

copy(input, input_end, back_inserter<double>(values));
```

你首先创建一个存储 `double` 值的列表。在提示输入后，你创建了两个用于 `double` 值的输入流迭代器。第一个迭代器指向 `cin`，第二个是由于默认构造函数创建的流结束结束迭代器。你用这两个迭代器为 `copy()` 函数指定输入；copy 操作的目标是你在 `copy()` 函数的第三个参数中创建的后置插入器。后置插入器将 copy 操作传输的数据添加到列表容器中。这是一种非常强大的功能。如果你忽略提示，可以从标准输入流读取任意数量的值，并将其传输到列表容器中。

# 使用输出流迭代器

作为输入流迭代器模板的补充，`ostream_iterator<T>` 模板提供了用于向输出流写入类型为 `T` 的对象的输出迭代器。输出流迭代器有两个构造函数。其中一个创建一个将数据传输到目标流的迭代器：

```cpp
std::ostream_iterator<int> out(cout);
```

模板类型参数 `int` 指定了要处理的数据的类型，而构造函数参数 `cout` 指定了将作为数据目的地的流，因此 `ostream_iterator` 迭代器可以向输出流写入 `int` 类型的值。以下是你可能如何使用此迭代器：

```cpp
int data[] = {1, 2, 3, 4, 5, 6, 7, 8, 9};

std::copy(begin(data), end(data), out);

// 1 2 3 4 5 6 7 8 9

copy(begin(numbers), end(numbers), out);
```

在 `<algorithm>` 头文件中定义的 `copy()` 算法将前两个参数指定的对象序列拷贝到第三个参数指定的输出迭代器。在这里，函数将元素从 `data` 数组拷贝到 `out` 迭代器，迭代器会将元素写入 `cout`。执行该函数的结果将是：

123456789

如你所示，值被写入输出流且中间没有空格。第二个构造函数可以改进这一点：

```cpp
std::ostream_iterator<int> out(cout, " ", " ");
```

第二个参数是一个作为输出值分隔符的字符串。如果你在前一个片段中使用此迭代器作为 `copy()` 函数的第三个参数，输出将是：

1, 2, 3, 4, 5, 6, 7, 8, 9,

你在第二个构造函数参数指定的指定的符字符串会被写入每个值之后的流中。

让我们看看输出迭代器在实践中工作的。

# 尝试一下

假设你想从 `cin` 读取一系列整数值并将它们存储在 `vector` 中。然后你可以输出这些值及其和。以下是你使用 STL 实现的方法：

```cpp
// Ex10_iter.cpp

// 使用流和插入器迭代器

#include <iostream>

#include <numeric>

#include <vector>

#include <iterator>

using std::cout;

using std::cin;

using std::endl;

using std::vector;

int main()

{

    vector<int> numbers;

    cout << "输入一系列用空格分隔的整数 "
         << "然后按 Ctrl+Z 或输入字母: *" << endl;

    std::istream_iterator<int> input(cin, input_end);

    std::ostream_iterator<int> out(cout, " ");

    // 注意：原始 OCR 在声明前使用了 input_end； 
    // 在实际代码中这需要定义或处理。

    copy(input, input_end, back_inserter(numbers));

    cout << "你输入了以下值:" << endl;

    copy(begin(numbers), end(numbers), out);

    cout << endl << "这些值的和为 " << std::accumulate(numbers.begin(), end(numbers), 0) << endl;

    return 0;

}
```
